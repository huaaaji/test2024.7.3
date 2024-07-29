# Linux常用命令

1. `ls`：列出当前目录中的文件和子目录
2. `pwd`：显示当前工作目录的路径
3. `cd + <目录>`：切换工作目录
4. `mkdir directory_name` 创建新目录
5. `rmdir directory_name` 删除空目录
6. `rm file_name` 删除文件 `rm -r directory_name` 递归删除目录及其内容
7. `cp source_file destination` 复制文件 `cp -r source_directory destination` 递归复制目录及其内容
8. `mv old_name new_name` 移动或重命名文件或目录
9. `touch file_name` 创建空文件或更新文件的时间戳
10. `cat file_name` 连接和显示文件内容
11. `more file_name`/`less file_name`  逐页显示文本文件内容
12. `head -n 10 file_name` 显示文件的前10行 `tail -n 20 file_name` 显示文件的后20行
13. `grep search_term file_name` 在文件中搜索指定文本
14. `ps aux` 显示当前运行的进程
15. `kill process_id` 终止进程
16. `ifconfig`/`ip`：查看和配置网络接口信息
    - ifconfig
    - ip addr show
17. `ping` 测试与主机的连通性:`ping host_name_or_ip`
18. `wget`/`curl` 从网络下载文件
    - `wget URL`
    - `curl -O URL`
19. `chmod` 修改文件或目录的权限 `chmod permissions file_name`
20. `chown` 修改文件或目录的所有者
21. `tar` 用于压缩和解压文件和目录
22. `df`/`du` 显示磁盘使用情况
    - df -h  # 显示磁盘空间使用情况
    - du -h directory_name  # 显示目录的磁盘使用情况
23. `mount`/`umount`：挂载和卸载文件系统
    - `mount /dev/sdX1 /mnt` 挂载分区到指定目录
    - `umount /mnt` 卸载挂载的文件系统
24. `psql`/`mysql` 用于与PostgreSQL或MySQL数据库交互的命令行工具
25. `top`/`htop` 显示系统资源的实时使用情况和进程信息
26. `ssh` 远程登录到其他计算机: `ssh username@remote_host`
27. `scp` 安全地将文件从本地复制到远程主机，或从远程主机复制到本地
28. `find` 在文件系统中查找文件和目录:`find /path/to/search -name "file_pattern"`
29. `grep` 在文本中搜索匹配的行，并可以使用正则表达式进行高级搜索:`grep -r "pattern" /path/to/search`
30. `sed` 流编辑器，用于文本处理和替换:`sed 's/old_text/new_text/' file_name`
31. `awk` 用于文本处理和数据提取的文本处理工具
32. 
