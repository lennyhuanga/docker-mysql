
http://blog.51cto.com/chen3888015/986841
1、远程权限问题：
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;
ERROR 1410 (42000): You are not allowed to create a user with GRANT

先执行 use mysql;
再GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;

2、select host,user from user;
看一下user 对应的host有没有% ，没有的话 
update user set host = '%' where user = 'root'