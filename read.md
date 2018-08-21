
https://blog.csdn.net/zhaobw831/article/details/80141633
mysql镜像拉取
docker pull mysql/mysql-server

这里拉取的是mysql的一个服务器优化版本。

挂载volume资料卷
在docker所在主机上创建mysql的俩个文件夹：config和db，在config下创建my.cnf

cd / 
mkdir docker/mysql 
cd docker/mysql 
mkdir config 
mkdir db

my.cnf内容：

[mysqld]
user=mysql

执行以下命令，创建容器

docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=myroot --name mysql01 -v=/docker/mysql/config/my.cnf:/etc/my.cnf -v=/docker/mysql/data:/var/lib/mysql mysql/mysql-server

输入docker ps查看，已经运行了mysql01容器，继续以下操作

使用命令docker logs mysql01查看日志，找到初始密码，

进入容器 : docker exec -it mysql01 bash 
使用root登录mysql : mysql -u root -p，然后输入刚才日志中找到的密码，进入mysql。 
设置密码：SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123456');

创建新用户:

mysql> CREATE USER 'root_test'@'localhost' IDENTIFIED BY '123456';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root_test'@'localhost'
    ->     WITH GRANT OPTION;
mysql> CREATE USER 'root_test'@'%' IDENTIFIED BY '123456';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root_test'@'%'
    ->     WITH GRANT OPTION;

修改默认字符集为utf-8: 
查看当前字符集：show variables like '%char%'; 
退出容器，修改之前在主机上创建的my.cnf文件,修改后内容如下：

[mysqld]
user=mysql
character-set-server=utf8
[client]
default-character-set=utf8
[mysql]
default-character-set=utf8

重启容器：docker restart mysql01,然后进入mysql01容器，查看字符集，已成功修改。