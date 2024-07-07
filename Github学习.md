# Github学习

***

整理始于2024.7.5晚

***

## Git本地配置

Git Bash 是 Git for Windows 的一个组件，它提供了一个基于 MinGW 的命令行仿真环境，允许用户在 Windows 操作系统上使用 Git 命令行工具，就像在 Unix 或 Linux 系统上一样。
Git for Windows 是 Git 的官方版本，它包括了 *Git 命令行工具*、*Git GUI（图形用户界面）*以及 *Git Bash*。

Git Bash 提供了一些类似于 Unix shell 的特性，包括常用的 Unix 命令（如 `ls`、`cat`、`grep` 等），以及通过 SSH 进行远程操作的能力。
它还支持对 Windows 文件系统的访问，允许用户在 Git Bash 中执行 Windows 应用程序和访问 Windows 文件路径。

安装 Git for Windows 后，用户可以在 Windows 的开始菜单中找到 Git Bash，或者在文件资源管理器中任意文件夹的上下文菜单中找到“Git Bash Here”选项，从而启动 Git Bash。
在 Git Bash 中，用户可以执行 Git 相关的操作，如克隆仓库、提交更改、推送分支等。

### 安装

略

![Git常用命令](./pictures/git-common-orders.png)

### Git与Github的绑定——SSH密钥

在 Git bash 中输入 `cd ~/.ssh`，返回 "no such file or directory" 表明电脑没有ssh key，需要创建ssh key；

输入ssh-keygen -t rsa -C “git账号”；git bash 会生成ssh密钥，并显示ssh密钥存储的目录

按路径进入 .ssh，里面存储的是两个 ssh key 的秘钥，id_rsa.pub 文件里面存储的是公钥，id_rsa 文件里存储的是私钥，不能告诉别人。打开 id_rsa.pub 文件，复制里面的内容。

在Github的settings中找到ssh密钥，填写复制的公钥（id_rsa.pub内容）

在Git bash中通过`ssh -T git@github.com`来检查Git是否成功绑定

    git config --global user.name “gitname”
    git config --global user.email “git邮箱”

至此，基本完成本地Git和Github的绑定

### 管理代码

***push***：本地的代码有了更新，为了保持远程与本地的代码同步，我们就需要把本地的代码push到远程的仓库，代码示例：

    git push origin master

***pull***：远程仓库的代码有了更新，为了保持本地与远程的代码同步，我们就需要把远程的代码pull到本地，代码示例： 

    git pull origin master

***clone***：将库(repository)克隆至本地，便于以后上传代码
点进仓库之后点击 Code，点击 ssh 会看到一串网址（http也可以），这个地址就是代码地址。
通过Git bash进入欲克隆仓库所至的路径（可以在Windows文件资源管理器中通过邮件在所在目录打开Git bash）
在Git bash中使用如下命令clone库

    git clone <url>

之后，在本地所选定目录下就会出现一个文件夹，表示即刚刚克隆的库

同样的，在本地库目录里创建了新文件，则需要在库的目录里使用Git bash并通过

    git add 文件名
来添加文件，并通过

    git commit -m “commit的description”
来提交commit