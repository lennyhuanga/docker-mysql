
https://blog.csdn.net/zhaobw831/article/details/80141633
mysql������ȡ
docker pull mysql/mysql-server

������ȡ����mysql��һ���������Ż��汾��

����volume���Ͼ�
��docker���������ϴ���mysql�������ļ��У�config��db����config�´���my.cnf

cd / 
mkdir docker/mysql 
cd docker/mysql 
mkdir config 
mkdir db

my.cnf���ݣ�

[mysqld]
user=mysql

ִ�����������������

docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=myroot --name mysql01 -v=/docker/mysql/config/my.cnf:/etc/my.cnf -v=/docker/mysql/data:/var/lib/mysql mysql/mysql-server

����docker ps�鿴���Ѿ�������mysql01�������������²���

ʹ������docker logs mysql01�鿴��־���ҵ���ʼ���룬

�������� : docker exec -it mysql01 bash 
ʹ��root��¼mysql : mysql -u root -p��Ȼ������ղ���־���ҵ������룬����mysql�� 
�������룺SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123456');

�������û�:

mysql> CREATE USER 'root_test'@'localhost' IDENTIFIED BY '123456';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root_test'@'localhost'
    ->     WITH GRANT OPTION;
mysql> CREATE USER 'root_test'@'%' IDENTIFIED BY '123456';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root_test'@'%'
    ->     WITH GRANT OPTION;

�޸�Ĭ���ַ���Ϊutf-8: 
�鿴��ǰ�ַ�����show variables like '%char%'; 
�˳��������޸�֮ǰ�������ϴ�����my.cnf�ļ�,�޸ĺ��������£�

[mysqld]
user=mysql
character-set-server=utf8
[client]
default-character-set=utf8
[mysql]
default-character-set=utf8

����������docker restart mysql01,Ȼ�����mysql01�������鿴�ַ������ѳɹ��޸ġ�