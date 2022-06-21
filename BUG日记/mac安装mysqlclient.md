# MAC 安装 mysqlclient

## 步骤一

### 安装mysql

进入 [mysql官网](https://www.mysql.com/) 安装

1. ![image-20220104141819580](/Users/cobb/Library/Application Support/typora-user-images/image-20220104141819580.png)
2. ![image-20220104142025796](/Users/cobb/Library/Application Support/typora-user-images/image-20220104142025796.png)
3. ![image-20220104142108148](/Users/cobb/Library/Application Support/typora-user-images/image-20220104142108148.png)



## 步骤二

### 配置环境变量

[快捷查看教程](https://www.cnblogs.com/xxpblog/articles/15760818.html)

## 步骤四

### 安装mysqlclient

~~~
pip3 install mysqlclient
~~~

#### 若出现**mysql_config: command not found 错误**

![img](https://upload-images.jianshu.io/upload_images/16735552-9397042459fa55db.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

##### 解决办法

执行如下命令

~~~
brew install mysql-connector-c
~~~

类似如图

![img](https://upload-images.jianshu.io/upload_images/16735552-5a728bdcda9a4a74.png?imageMogr2/auto-orient/strip|imageView2/2/w/885/format/webp)

根据出现的提示添加环境变量到~/.zshrc或者.bash_profile中



再次安装mysqlclient

~~~
pip3 install mysqlclient
~~~

##### 检查是否成功安装mysqlclient

~~~
➜ pip3 freeze|grep -i 'mysql'
~~~





