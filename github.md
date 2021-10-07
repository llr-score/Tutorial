##### gitHub术语注释
- Repository： repo，仓库。项目存放于仓库之中。
- Issues：问题。
- Star：点赞。
- Fork：拉分支。在某项目基础上开发新功能，即复制一个相同项目到我们的gitHub上且独立于原项目。
- Pull Request：提交请求。在fork功能上，对原项目拥有者提出pull请求，若通过审核则可将我们的修改合并到原项目中。
- Merge：合并。别人fork我们的项目修改并pull了请求。我们可以选择是否merge。
- Watch：观察。watch后若项目有更新则会在第一时间收到项目的更新通知。
- Gist：只分享部分代码片段。（翻墙）

---


gitHub基于版本控制系统git之上。

##### Git
- 下载：官网：git - -fast-version-control  --> download
```
Additional icons -- 桌面创建快捷方式打开git
Windows Explorer integration -- 鼠标右键快速打开git GUI/git Bash
```



- **使用**
1. 进入操作的demo目录，打开Git Bash
2. 查看仓库是否为git仓库，否则初始化仓库
```
// 查看仓库状态
git status  
// 初始化某目录为git仓库
git init
```
3. 添加追踪的文件，即添加文件到仓库中
```
// status:  untraked files: 在该目录但是没有追踪的文件
git add test.txt
```
4. 提交文件到仓库
```
// -m 表提交信息 “ ” 中为具体信息
git commit -m "text commit"
```
5. 一些命令
```
git log	//打印仓库提交日志
git branch // 查看git仓库的分支情况  *为当前所在分支

git branch a // 创建分支a
git checkout a // 切换到分支a 
git checkout -b b // 创建b分支同时切换到b分支

git merge a // 将a分支合并到master分支
git branch -d a // 删除分支a。-D 强制删除

git tag // 查看标签记录
git tag v1.0 // 为当前分支添加标签v1.0
git checkout v1.0 //切换到该标签下的代码状态。
```
```
git config --list // 查看当前git环境所有配置
git config user.email //查看邮箱
git config --global user.email " .com" // 修改邮箱
```

---



##### git与gitHub的绑定

- SSH(安全外壳协议)：gitHub上一般通过SSh授权，大多数git服务器也会选择使用SSH公钥进行授权。因此首先在gitHub上添加SSh key配置
1. 生成SSH Key（git bash）
```
// 这是检查是否有ssh/ key. 若有则不需要再生成
cd ~/.ssh
ls
```


```
// 生成过程
ssh // 检查是否安装SSh
  
  // 1.指定rsa生成密钥
ssh-keygen -t rsa
// 三次回车生成 id_rsa  id_rsa.pub文件
// 默认在目录 ：C:\Documents and Settings\username\\.ssh

 // 2. 普遍生成方式
ssh-keygen -t rsa -C "your_email@example.com"
-t 指定密钥类型，默认是 rsa ，可以省略。
-C 设置注释文字，比如邮箱。
-f 指定密钥文件存储文件名。
```


2. 添加SSH key（gitHUb）

Settings --> SSh and GPG Keys添加id_rsa.pub内容。

SSH key 代码的前后不要留有空格或者回车。

```
// 推荐使用clip进行赋值 windows
clip < ~/.ssh.id_rsa.pub
```



3. 验证绑定是否成功
```
ssh -T git@github.com
```

至此完成**本地Git**与**远程GitHub的绑定**

*注*：
·一台电脑只需要一个 SSH key
·一个 SSH key 可以访问你的所有仓库，即使你有 1000000 个仓库，都没问题
·如果你新买了电脑，就在新电脑上重新生成一个 SSH key，把这个 key 也上传到 GitHub，它可以和之前的 key 共存在 GitHub 上
·如果你把 key 从电脑上删除了，重新生成一个 key 即可，替换之前的 key

**https 和 SSH 的区别**：

1、前者可以随意克隆github上的项目，而不管是谁的；而后者则是你必须是你要克隆的项目的拥有者或管理员，且需要先添加 SSH key ，否则无法克隆。

2、https url 在push的时候是需要验证用户名和密码的；而 SSH 在push的时候，是不需要输入用户名的，如果配置SSH key的时候设置了密码，则需要输入密码的，否则直接是不需要输入密码的。

---



##### git提交代码到github

- push：将本地代码推到远程仓库
```
git push origin master
```
- pull：远程仓库有更新，将远程仓库拉到本地
```
git pull origin master
```

###### 提交代码

*推荐使用ssh链接的方式*

1. 本地没有git仓库，直接将远程仓库clone，则**本身就是一个git仓库**，不用init

只用在这个仓库进行修改、添加操作，然后*commit*
```
// 进入一个新建文件夹
git clone 项目的link

// 进行相关添加add、提交commit等操作后，push
git push origin master
```
2. 本地有git仓库，且进行了多次commit操作。已经init操作了。
```
// 关联远程仓库，origin为远程仓库的名字
git remote add origin 项目link
git remote -v // 查看关联仓库

// 同步远程仓库和本地仓库
git pull origin master
```

###### git仓库
```
// 添加
git remote add [shortname] [url]
// 查看当前仓库
git remote
git remote -v

// 推送到远程仓库
git push [alias] [branch]
   //推送本地的 master 分支到远程 origin，
git push origin master    # 推送到 Github.
// 删除远程仓库
git remote rm [别名]
// 修改仓库地址
git remote set-url origin ....
```

----
##### 一些报错
- 致命的：无法找到远程参考主，也就是报错的意思。错误的提示内容意思是找不到需要连接的对象。
```
fatal: Couldn't find remote ref master
```
master最近发现默认的 git 分支名称是种族主义的，因此已将其更改为默认值main。

因此，我们不是从master分支中拉取，而是从默认main分支中拉取：
```
git pull origin main
```
