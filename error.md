
http://blog.51cto.com/chen3888015/986841
1��Զ��Ȩ�����⣺
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;
ERROR 1410 (42000): You are not allowed to create a user with GRANT

��ִ�� use mysql;
��GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;

2��select host,user from user;
��һ��user ��Ӧ��host��û��% ��û�еĻ� 
update user set host = '%' where user = 'root'