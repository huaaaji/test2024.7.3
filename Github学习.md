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

### Git与Github的绑定——SSH密钥

在 Git bash 中输入 `cd ~/.ssh`，返回 "no such file or directory" 表明电脑没有ssh key，需要创建ssh key；

输入ssh-keygen -t rsa -C “git账号”；git bash 会生成ssh密钥，并显示ssh密钥存储的目录

按路径进入 .ssh，里面存储的是两个 ssh key 的秘钥，id_rsa.pub 文件里面存储的是公钥，id_rsa 文件里存储的是私钥，不能告诉别人。打开 id_rsa.pub 文件，复制里面的内容。

在Github的settings中找到ssh密钥，填写复制的公钥（id_rsa.pub内容）

在Git bash中通过`ssh -T git@github.com`来检查Git是否成功绑定

![Git常用命令](./pictures/git-common-orders.png)

