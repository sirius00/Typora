# mysql基本使用

## 命令行基本操作

- 删除数据库

   ~~~
   drop database 数据库名
   
   drop database if exist 数据库名
   ~~~

  

- 连接数据库

  ~~~
  mysql -u root -p
  ~~~

- 显示所有数据库

  ~~~
  show datebases;
  ~~~

- 选择并使用数据库

  ~~~
  use 数据库名字;
  ~~~

- 创建数据库

   ~~~
   create datebase 数据库名字 default charset utf8;
   ~~~

- 



## 使用mysql技巧

- mysql实现oracle中spool功能
  1. tee c:\路径\test.txt
  2. notee

### mysql8.0更改密码

