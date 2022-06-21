# django切换mysql数据库

## BUG1

出现错误如下:

![iShot2022-01-06 10.57.45](/Users/cobb/Documents/屏幕截图/iShot2022-01-06 10.57.45.png)

原因:

大概率是因为Mysqldb 不兼容 python3.5 以后的版本

解决办法:

使用pymysql代替使用pymysql代替MySQLdb

步骤：

- 安装pymysql：pip install pymysql

- 打开项目在setting.py的**init**.py,或直接在当前py文件最开头添加如下

  ~~~
  import pymysql
  pymysql.version_info = (1, 4, 13, "final", 0)    #指定版本
  pymysql.install_as_MySQLdb()
  ~~~

  

  ## bug2

  出现如图错误:

  ![iShot2022-01-06 14.45.04](/Users/cobb/Documents/屏幕截图/iShot2022-01-06 14.45.04.png)

  AttributeError: 'str' object has no attribute 'decode'

  

  解决办法:

  进入该文件,修改该值

  

  将decode 改为 encode

  