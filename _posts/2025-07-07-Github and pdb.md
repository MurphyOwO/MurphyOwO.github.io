#### pdb
###### 非入侵式方法

在命令行下直接运行就能测试
`pyhon -m pdb filename.py`

###### pdb常用命令

当停留在某个地方时,pdb提示符本身通常会显示类似
	/path/to/my_script.py(42)<function_name>()
	-> some_python_code()
文件+行号+当前函数名

查看当前位置前后11行代码`l`
执行下一行不进入函数体`n`
执行下一行进入函数体`s`
查看当前文件路径(栈)`where|w`
查看当前帧的__file__`p __file__`
在指定文件+行设置断点`b 文件.py:行号`
清除断点`cl`

###### pdbpp
pdbpp相比较于pdb增加了自动补全和语法高亮
更加友好

#### Github

###### 关联两个仓库
- 生成两个SSH Key,并将两个公钥分别添加到两个Github账号
- 在~/.ssh/confi里填写不同的配置，有了两个逻辑上的Host
- 在本地仓库指定远程路径
	- cd /path/to/personal-repo
	- git remote set-url origin git@github-personal:yourname/personal-repo.git
- 验证ssh -T github-personal

或者在不同的路径下配置不同的用户名和邮箱去覆盖global配置

在不同的本地仓库关联远程仓库URL里写对Host别名
进入不同的路径就可以进行push隔离

###### ~/.gitconfig

.gtconfig是全局的
两个账号主要影响两个东西
- SSH Key 这个通过.ssh/config区分
- 提交记录的user.email和user.name
所以保证每个仓库的user.name和user.email与想推到的Github账号一致

- 全局配置一个默认账号
- 在需要切换的仓库单独配置

```bash
cd ~/projects/work-repo
git config user.name "Work Name"
git config user.email "work@email.com"

这会写入当前项目的
./.git/config

[user]
	name = Work Name
	email = work@email.com

```


###### ssh -T git@github.com
- Hostname = github.com
- User = git

SSH会按顺序尝试私钥，如果之前使用过则SSH会进行自动连接

###### .ssh/config的用处
- 定义别名
- 用不同的key对应不同的目标
- 指定特殊的端口、代理、转发、选项等
```bash
Host github-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_personal

Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work

```
这样就可以用
```bash
ssh -T github-personal
ssh -T github-work
```
分别用不同的key进行连接github


