#Git使用教程*-file  = 文件名                                                ##设置用户名和邮箱```不设置无法提交```> git config --global user.name ""> git config --global user.email ""##进入目录后，把目录变成Git可管理的仓库(工作区)> git init######//变成可管理库后会出现.git文件，如果没有 请输入>ls -al##Git分为工作区、暂存区、历史区三个部分，通过输入以下命令，把文件添加到暂存区>git add fileName(-A)##输入以下命令，提交到历史区里面>git commit -m"本次提交描述"##克隆项目>git clone 仓库地址##查看git仓库历史记录>git log##流程0.clone 项目，修改工作区。  1.通过git add fileName(如果需要全部提交则替换成 -A) 提交到暂存区。2.通过git commit -m"描述" 提交到历史区。  3.最后通过 git push origin master 提交到服务器。  4.发一个pull request  ##push速度太慢的解决办法1.需要SSH来连接git服务器，使用以下命令  >ssh -v git@git-server2.之后打开/etc/ssh/ssh_config  3.找到 GSSAPIAuthentication no 这句话，将#删掉  >服务器端启用了GSSAPI。登陆的时候客户端需要对服务器端的IP地址进行反解析，如果服务器的IP地址没有配置PTR记录，那么就容易在这里卡住了。 >是否允许使用基于 GSSAPI 的用户认证。默认值为"no"。仅用于SSH-2。
##添加```git add 的各种区别```>git add -A   // 添加所有改动>git add *     // 添加新建文件和修改，但是不包括删除>git add .    // 添加新建文件和修改，但是不包括删除>git add -u   // 添加修改和删除，但是不包括新建文件
```在commit前撤销add```>git reset -file // 撤销提交单独文件>git reset        // unstage all due changes##修改```查看修改过但未提交的文件```>git status```查看修改内容```>git diff -file

```撤销对文件的修改```
>git checkout -- -file

```add添加后再次进行查看提交的修改是否包括文件```
>git status

##查看

```查看提交历史记录```
> git log --pretty=oneline

```查看文件内容```
>cat -file

```查看工作区和版本库里最新版本的区别```
>git diff HEAD -- -file

##回退
```版本用HEAD表示，上一个版本就是HEAD^ ，上上个版本就是HEAD^^ 上一百个就是HEAD~100```
>git reset --hard HEAD^
>git reset HEAD -file //撤销暂存区的修改

```如果想回到最新版就用commit id去回退 ```
>git reset --hard commit_id

```记录历史版本更新命令```
>git reflog

##删除

>rm -file

```两种选择  ```

```1.一是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit```
>git rm -file
>git commit

```2.另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本```
>git checkout -- -file

##远程库

```第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件```
```如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key```
> ssh-keygen -t rsa -C "youremail@example.com"

```第二部本地关联git库，或者从git库克隆新的库到本地```
 
>git remote add origin "https://github.com/username/objectname.git

>git push -u origin master //第一次加-u 是关联master分支，为以后推送拉取简化命令

```如果关联写错地址，可在.git文件夹中的config进行修改url```


```克隆```

>git clone githubObjectAddress