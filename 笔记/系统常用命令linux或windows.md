# linux常用命令

- nohup node app.js &            后台启动node程序

- ps aux|grep node                 查看进程

- netstat -ntlup                          列出所有程序

- netstat -ntlup|grep node     查看node进程
  ![image-20200109135045738](E:\ideaProjects\my\ospNote\asserts\image-20200109135045738.png)

- lsof -i:8080   查看端口

- ubuntu 开启防火墙端口

  firewall-cmd --zone=public --add-port=3306/tcp --permanent

  firewall-cmd --reload

- df -h 查看磁盘存储

- du -sh /目录   查看某个文件的目录

- history    查看历史命令   如：history |grep restart

- linux命令导入 sql                    mysql -u root -p coin_test < /mnt/dbback/1120-0200.sql 

