# Django学习

## 安装django

安装django ：pip3 install django==2.2.12



检查安装的django版本：python -m django --version



1. 创建项目

   django-amdin startproject mysite

2. 启动服务

   1、进入项目文件夹

   2、python3 manage.py runserver

3. 改变端口号

   python manage.py runserver 端口号

## 项目结构



- `manage.py`: 一个让你用各种方式管理 Django 项目的命令行工具

  - runserver：启动服务
  - startapp：创建应用
  - migrate：数据库迁移
  - python3 manage.py：查看所有命令

- 里面一层的 `mysite/` 目录包含你的项目，它是一个纯 Python 包。它的名字就是当你引用它内部任何东西时需要用到的 Python 包名。 (比如 `mysite.urls`).

- `mysite/__init__.py`：一个空文件，告诉 Python 这个目录应该被认为是一个 Python 包。

- `mysite/settings.py`：Django 项目的配置文件。

  公有配置、自定义配置

  ~~~python
  import os
  
  
  项目绝对路径
  BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
  
  
  项目启动模式
  DEBUG = True
  true 调试模式
  false 上线模式
  
  
  过滤请求头Host头
  ALLOWED_HOSTS = []
  
  
  # Application definition
  
  INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
  ]
  
  
  中间件
  MIDDLEWARE = [
  
  ]
  
  
  
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
      }
  }
  
  
  
  页面显示语言
  zh-hans
  LANGUAGE_CODE = 'en-us'
  
  
  时区
  Asia/Shanghai
  TIME_ZONE = 'UTC'
  
  USE_I18N = True
  
  USE_L10N = True
  
  USE_TZ = True
  
  
  # Static files (CSS, JavaScript, Images)
  # https://docs.djangoproject.com/en/2.2/howto/static-files/
  
  STATIC_URL = '/static/'
  ~~~
  
  
  
- `mysite/urls.py`：Django 项目的 URL 声明，就像你网站的“目录”。

- `mysite/wsgi.py`：作为你的项目的运行在 WSGI 兼容的Web服务器上的入口。



## URL和视图函数



- ### 样例

  ~~~python
  #file：<项目同名文件夹下>/views.py
  from django.http import HttpResponse
  
  def page1_view(request):
    html = "<h1>这是第一个页面<h1>"
    return HttpResponse(html)
  
  同时配置url文件 
  添加path路径
  ~~~

  



## 路由配置



- ### 样例

  ~~~python
  setting.py 文件中的 root_urlconf 指定了主路由配置列表urlpatterns的文件位置
  
  
  path函数
  导入 - from django.urls import path
  语法 - path(route,views,name-None)
  参数：
  1、route：字符串型，匹配的请求路径
  2、views：指定路径所对应的视图处理函数的名称
  3、name：为地址别名，在模板中地址反向解析时使用
  ~~~



- ### path转换器

  ~~~python
  语法：<转换器类型：自定义名>
  作用：若转换器类型匹配到对应类型的数据，则将数据按照关键字传参的方式传递给视图函数
  
  例子：path('page/<int:page>',views.xxx)
  ~~~

- ### re_path()函数

  在URL的匹配过程中可以使用正则表达式进行精确匹配





## 请求和响应



`请求`是指浏览器端通过HTTP协议发送给服务器端的数据

- path_info：url字符串

- method：字符串，表示HTTP请求方法，常用值：“GET”、“POST”

- GET：QUeryDict查询字典的对象，包含get请求方式的所有数据

- POST：QUeryDict查询字典的对象，包含post请求方式的所有数据

- FILES：类似于字典的对象，包含所有的上传文件信息

- cookies：python字典，包含所有的cookies，键和值都为字符串

- session：类似于字典的对象，表示当前会话

- body：字符串，请求体的内容

- scheme：

- request.get_full_path():

- Request.META:请求中的元数据（消息头）

  

`响应`是指服务器端接收到请求之后做相应的处理在回复给浏览器端的数据

- 响应状态码
  - 200：请求成功
  - 301：永久重定向-资源（网页等）被永久转移到其他的URL
  - 302：临时重定向
  - 404：请求的资源（网页等）不存在
  - 500：内部服务器错误
- django的响应对象



## POST和GET请求



- 处理逻辑

  ~~~python
  if request.requestmethod == 'GET':
    处理GET请求
  else request.method == 'POST':
    处理POST请求
  else:
    其他请求
  ~~~

- 报错403,取消csrf验证

  禁止掉settings.py中middleware中的CrfsViewsMiddleWare的的中间件

## Django设计模式和模板层

1. #### 设计模式

   MTV

2. #### 模板层

   ##### 什么是模版?

   1. 是可以根据字典数据动态变化的html网页
   2. 可以根据视图中传递的字典数据动态生成相应的html网页
   
   ##### 模板配置
   
   - 创建模板文件夹<项目名>/template
   - 在settings.py中templates配置项
     1. BACKEND:制定模板的引擎
     2. **DIRS:模板的搜索目录**     *只需要修改*（设置DIRS - ‘DIRS’：[os.path.join(BASE_DIR,'templates')],)
     3. APP_DIRS:是否要在应用中的template文件夹中搜索模板文件
     4. OPTIONS：有关模板的选项
   
   ##### 模板的加载方式
   
   - 通过loader获取模板,通过HttpResponse进行响应
   
     1. 在views文件中
   
        ~~~python
        def test_html(request):
        	from django.temlates import loader
        	t = loader.get_template("模板文件名")
        	html = t.render(字典数据)  //转换成字符串
        	return HttpResponse(html)
        ~~~
   
     2. 在templates文件夹中创建文件
   
     3. 在urls.py文件中添加路径
     
   - 使用render()直接加载并响应模板
   
     1. 在视图函数中
   
        ~~~python
        from django.shortcuts import render
        return render(request,'模板名',字典数据)
        ~~~
   
   ##### 视图层和模板层之间的交互
   
   1. 视图函数中可以将python变量封装到字典中传递到模板层
   
      ~~~python
      def xx_view(request):
        dic = {
          "变量1":"值1",
          "变量2":"值2",
        }
        return render(request,'xx.html',dic)
      ~~~
   
      
   
   2. 模板中,可以使用{{变量名}}的语法调用视图传进来
   
   ##### 模板层变量和标签
   
   1. 模板层变量
   
      - 能传递到模板中的数据类型
        - str - 字符串
        - list - 数组
        - dict - 字典
        - obj - 类实例化对象
        - int - 整型
        - tuple - 元组
        - func - 方法
      - 在模板中使用变量语法
        - {{变量名}}
        - {{变量名.index}}
        - {{变量名.key}}
        - {{对象.方法}}
        - {{函数名}}
   
   2. 模板标签
   
      标签语法
   
      ~~~
      {% 标签 %}
      ...
      {% 结束标签 %}
      ~~~
   
   ##### 模板层 - 过滤器和继承
   
   - 过滤器
   
   - 继承   
   
     1. 在父模板中
   
        - 定义父模板中的块block标签
        - 标识出安歇在子模块是允许被修改的
        - block标签:在父模块中定义,可以在子模块中覆盖
   
     2. 在子模块中
   
        - 继承模板extends标签(写在模板文件第一行)
   
          ~~~
          {%extends 'base.html'%}
          ~~~
   
        - 子模板 重写父模块中的内容模块
   
          ~~~
          {% block block_name%}
          子模板用来覆盖父模板中 block_name块的内容
          {% endblock block_name %}
          ~~~
   
          

## URL反向解析





url反向解析是指在视图或模板中,用path定义的名臣来动态查找或计算出相应的路由



### 路由转换器

https://www.cnblogs.com/wanglan/p/11639611.html



### path函数的语法

~~~python
path(route,views,name = "别名")

path('page',views.page_view,name="page_url")
~~~

根据path中的'name='关键字传参给url确定了个唯一确定的名字,在模板或视图中,可以通过这个名字反向推断出url信息



### 模板中 - 通过url标签实现地址的反向解析

~~~python
{% url  '别名' %}

{% url '别名' '参数值1' '参数值2' %}

ex:
{% url 'pagen' '400' %}
{% url 'person' age='18' name='gxn' %}
~~~

### 在视图函数中 ->可调用django中的reverse方法进行反向解析

~~~python
from django.urls import reverse
reverse('别名',args=[],kwargs={})
~~~



## 静态文件

### 静态文件配置 - settings.py中



1. 配置静态文件访问路径

   - 通过哪个url地址查找静态文件

   - static_url = '/static/'

   - 说明

     指定访问静态文件时需要通过/static/xxx或http://127.0.0.1:8000/static/xxx[xxx 表示具体文件位置]

2. 配置静态文件的存储路径STATICFILES_DIRS

   保存的是静态文件在服务器端的存储位置

   ~~~python
   STATICFILES_DIRS= (
   	os.path.join(BASE_DIR,"static"),
   	)
   ~~~

3. 模板中访问静态文件 - img标签为例 **更动态的写法**

   通过{% static %}标签访问静态文件

   - 加载static - {% load static %}

   - 使用使用静态资源 -- {% static '静态资源路径' %}

   - 样例

     ~~~
     <img src="{% static 'image/lena.jpg' %}">
     ~~~

     

## Django应用和分布式路由

### 应用

应用是在django项目中是一个独立的业务模块,可以包含自己的路由,视图,模板,模型

#### 创建应用

1. 使用manage.py中的子命令startapp创建应用文件夹

   ~~~
   python3 manage.py startapp music
   ~~~

2. 在settings.py的INSTALLED_APPS列表中配置安装此应用

### 分布式路由

Django中,主路由配置文件(urls.py)可以不处理用户具体路由,主路由配置文件可以做请求的分发(分布式请求处理).具体的请求可以由各自的应用来进行处理

1. 主路由中调用include函数

   *语法 :* include('app名字.url模块名')

   *作用 :*用于将当前路由转到各个应用的路由配置文件的urlpatterns进行分布式处理

   ~~~
   path('music/',include('music.urls'))
   ~~~

1. 应用下配置urls.py

   应用下手动创建urls.py

   内容结构同主路由完全一样



## 模型层

### 模型层 - 负责跟数据库之间进行通信



#### 什么是模型

- 模型是一个类,由django.db.models.MODEL派生出的子类
- 一个模型类代表数据库中的一张数据表
- 模型类中每一个类属性都代表数据库中的一个字段
- 模型是数据交互的接口,表示和操作数据库的方法和方式



#### 模型类 - 创建

 ~~~python
 from django.db import models
 class 模型类名(models.Model):
 	字段名 = models.字段类型(字段选项)
 ~~~



#### Django配置mysql

##### [安装mysqlclient](https://www.cnblogs.com/xxpblog/p/15762922.html)



- 创建数据库

- 进入mysql数据库 执行
  - create datebase 数据库名 default charset utf8;
  - 通常数据库名称和项目名保持一致
  
- settings.py中配置数据库
  
  ~~~python
  ENGINE - 指定数据库存储引擎
  	'django.db.backends.mysql'
  	'django.db.backends.sqlite3'
  	'django.db.backends.oracle'
  	'django.db.backends.postgresql'
  NAME-指定要连接的数据库名字
  USER-指定登录到数据库的用户名
  PASSWORD-数据库的密码
  HOST/PORT-连接数据库的IP和端口
  ~~~

##### django数据库从sqlite3切换到mysql

[切换数据库到mysql]()

##### 数据库迁移

迁移是django同步您对模型所做的更改(添加字段,删除模型等)到您的数据库模式的方式

1. 生成迁移文件

   执行 

    ~~~
    python3 manage.py makemigrations
    ~~~

   

   将应用下的models.py文件生成一个中间文件,,并保存在migrations文件夹下

2. 执行迁移脚本程序

   执行 

    ~~~
    python3 manage.py migrate
    ~~~

   

   执行迁移程序实现迁移,将每个应用下的migrations目录中的中间文件同步回数据库



## ORM



### ORM框架

- **定义**:ORM即对象关系映射,它允许你实用类和对象对数据库进行操作,从而避免通过SQL语句操作数据库

- **作用**:

  1. 建立模型类和表之间的对应关系,允许我们通过面向对象的方式来操作数据库
  2. 根据设计的模型类生成数据库的表格
  3. 通过简单的配置就可以进行数据库的切换

  

  对应关系

  | ORM  |   DB   |
  | :--: | :----: |
  |  类  | 数据表 |
  | 对象 | 数据行 |
  | 属性 |  字段  |

  

### ORM - 基础字段及选项

#### 创建模型类流程

- 创建应用

- 在应用的models.py中编写模型类

   ~~~
   from django.db import models
   calss 模型类名(models.Model):
   	字段名 = models.字段类型(字段选项)
   ~~~

- 迁移同步 makemigration  & migrate

- 任何关于表结构的修改,务必在对应模型类上修改

  

  例如:为bookstore_book表 添加一个名为info的字段 varchar(100)

  步骤:

  - 模型类中添加对应类属性
  - 执行数据库迁移

  

#### 模型类 - 字段类型

- BooleanField()

  数据库类型:tinyint(1)

  编程语言中:使用True或False来表示值

  在数据库中:使用1或0来表示具体的值

- Charfield()

  数据库类型:varchar

  tips:*必须要指定max_length参数值*

- DateField()

  数据库类型:date 

  作用:表示日期

  参数:

  1. auto_now:每次保存对象时,自动设置该字段为当前时间(True/False)
  2. suto_now_add:当对象第一次被创建时自动设置当前时间(True/False)
  3. default:设置当前时间(取值:字符串时间格式:2019-6-1)

- DateTimeField()

  数据库类型:datetime(6)

  作用:表示日期和时间

  参数同DateField

- FloatField()

  数据库类型:double

  编程语言中和数据库中都使用小数表示

- DecimalField()

  数据库类型:decimal(x,y)

  编程语言中:使用小数点表示该列的值

  在数据库中:使用小数

  参数:

  mac_digits:位数总数,包括小数点后的位数.该值必须大于等于decimal_place

  decimal_place:小数点后的数字数量

- EmailField()

  数据库类型:varchar

  编程语言和数据库中使用字符串

- IntergerField()

  数据库类型:int

  编程语言和数据库中使用整数

- ImageField()

  数据库类型:varchar(100)

  作用:在数据库中为了保存图片的路径

  编程语言和数据库中使用字符串

- TextField()

  数据库类型:longtext

  作用:表示不定长的字符数据



#### 模型类 - 字段选项

- 字段类型,指定创建的列的额外信息

- 允许出现多个字段选项,多个选项之间使用,隔开

- primary_key

  如果设置为True,表示该列为主键,如果指定一个字段为主键,则此数据库表不会创建id字段

- blank

  设置为True时,字段可以为空.设置False时,字段是必须填写的

- null

  True,表示该列允许为空

  False,如果此项为False,建议加default选项来设置默认值

- default

  设置所在列的默认值

- db_index

  True,表示为该列增加索引

- unique

  True,表示该字段在数据库中的值必须是唯一

- db_column

  指定列的名称,如果不指定的话采用属性名来作为列名

- verbose_name

  设置此字段在admin界面上的显示名称

例如:

 ~~~
 name = models.CharField(max_length = 30 , unique = True, null = False, db_index = True)
 ~~~



#### 模型类 - Meta类

##### mate类 - 定义

使用内部Mate类 来给模型赋予属性,Mate类下有很多内建的类属性,可对模型类做一些控制

 ~~~python
 from django.db import models
 
 class Book(models.Model):
 	title = models.CharField("书名",max_length=50,default='')
 	price = models.DecimalField('定价',max_digits=7,decimal_place=2,default=0.0)
 	class Mate:
 		1.db_table= 'book'   #可改变当前模型类对应的表名(设置后须立即更新数据库)
        2.verbose_name = '单数名' #给模型对象一个单数名称,用于显示在/admin界面
        3verbose_name_plural = '复数名' #该对象复数形式显示在/admin界面
 ~~~

#### ORM - 基本操作 - 创建数据

##### 常见问题处理

1. 问题一

   ![iShot2022-01-07 13.13.28](/Users/cobb/Documents/屏幕截图/iShot2022-01-07 13.13.28.png)

   错误原因:

   当对模型类添加一个新字段时可出现的错误,添加新字段后,数据库不知道原来已有数据对于新建字段该如何赋值,所以新增字段时,务必添加default值

   解决办法:

   1. 进入到shell中,手动输入一个默认值
   2. 退出当前生成迁移文件过程,自己去修改models.py,新增加一个'default=xxx'的缺省值(推荐)

2. 问题二

   数据库的迁移文件混乱

   原因:

   数据库中django_migration表记录了migrate的'全过程',项目个应用中的migrate文件应与之对应,否则migrate会出现错误

   解决:

   1. 删除 所有migration里所有000?_ xxx.py ( _ init _.py除外)
   2. 删除 数据库
   3. 重新创建数据库
   4. 重新生成mogrations里所有的000?_xxx.py
   5. 重新更新数据库

##### ORM - 操作

基本操作包括增删改查,即(CRUD操作)

CRUD是指在做计算处理时的增加(create),读取操作(Read),更新(update)和删除(delete)

ORM CRUD 核心 -> 模型类.管理器对象

**管理器对象**

​	每个继承自models.Model的模型类,都会有objects对象被同样继承下来,这个对象叫      		做管理其对象

​	数据库的增删改查可以通过模型的管理器来实现

 ~~~python
 class MyModel(models.Model):
 	...
 MyModel.objects.create(...)    #objects是管理器对象 
 ~~~

###### 创建数据

创建数据中每一条记录就是创建一个数据对象

1. 方法一

   MyModels.objects.create(属性1=值1,属性2=值2,...)

   成功:返回创建好的实体对象

   失败:抛出异常

2. 方法二

   创建MyModel实例对象,并调用save()进行保存

    ~~~python
    obj = MyModel(属性=值,属性=值)
    obj.属性 = 值
    obj.save()
    ~~~

##### ORM - 查询

数据库的查询需要使用管理器对象

通过MyModel.objects管理器方法调用查询方法

|   方法    |               说明                |
| :-------: | :-------------------------------: |
|   all()   | 查询全部记录,返回queryset查询对象 |
|   get()   |      查询符合条件的单一记录       |
| filter()  |      查询符合条件的多条记录       |
| exclude() |      查询符合条件之外的记录       |

**all()方法:**

​	用法:MyModel.object是.all()

​	作用:查询MyModel试题中所有的数据,等同于select * from table

​	返回值:QuerySet()容器对象,内部存放MyModel实例



 ~~~python
 from bookstore.models import Book
 books = Book.objects.all()
 for book in books:
 	print("书名",book.title,'出版社',book.pub)
  
 ~~~

​	可以在模型类中定义__ str _方法,自定义QuerrySet中的输出格式

 ~~~
 def __str__(self):
 	return '%s_%s_%s_%s'%(self.title,self.price,self.pub,self.market_price)
 ~~~

**values('列1','列2'...):**

​	用法:MyModel.objects.values(...)

​	作用:查询部分列的数据并返回,等同于select 列1 ,列2 from xxx

​	返回值:QuerySet,返回查询结果容器,容器内存字典,每个字典代表一条数据

**values_list('列1','列2'...):**

​	用法:MyModel.objects.values_list(...)

​	作用:返回元组形式的查询结果 ,等同于select 列1,列2 from xxx

​	返回值:QuerySet容器对象,内部存放'元组'

**order_by():**

​	用法:MyModel.objects.order_by('-列','列')

​	作用:与all()方法不同,他会用sql语句的order by子句对查询结果进行根据某个字段选择性的进行排序

​	返回值:QuerySet,返回查询结果容器,容器内存字典,每个字典代表一条数据

​	说明:默认是按照升序排序,降序排序需要在列前增加'-'表示

**filter(条件):**

​	用法:MyModel.objects.filter(属性1 = 值1,属性2 = 值2 )

​	作用:返回包含此条件的全部数据集

​	返回值:QuerySet容器对象,内部存放MyModel实例

**exclude(条件):**

​	用法:MyModel.objects.exclude()

​	作用:返回不包含此条件的全部数据集

**get(条件):**

​	用法:MyModel.objects.get(条件)

​	作用:返回满足条件的唯一一条数据

​	说明:该方法只能返回一条数据,查询结果多余一条数据则抛出出,Model/MultipleObjectsReturned异常,如果查询没有数据则抛出异常Model.DoesNotExist异常

**非等值条件的查询:**

​	*查询谓词*

​		定义:做更灵活的条件查询时需要使用查询谓词

​		说明:每一个查询谓词是一个独立的查询功能

​		_exact:等值匹配

 ~~~python
 Author.objects.filter(id_exact=1)
 # select * from author where id = 1
 ~~~

​		_contains:包含指定值

​		_startswith:以XXX开始

​		_endswith:以xxx结束

​		_gt:大于指定值

​		_gte:大于等于

​		_lt:小于

​		_lte:小于等于

​		_in:查找数据是否在指定范围内

​		_range:查找数据是否在指定的区间范围内



##### 聚合查询和原生数据库操作

###### 聚合查询

定义:聚合查询是指对一个数据表中的一个字段进行部分或全部进行统计查询,查bookstore数据表中的全部书的平均价格,查询所有书的总个数等,都要使用聚合查询

分类:

- 整表聚合

  将全部数据进行集中统计查询

  聚合函数[需导入]:

   ~~~
   导入方法: from django.对比.models import *
   聚合函数: Sum,Avg,Count,Max,Min
   ~~~

  语法:

   ~~~
   MyModels.objects.aggregate(结果变量名=聚合函数('列'))
   -返回结果:结果变量名和值组成的字典
   ~~~

  

- 分组聚合

  分组聚合是指通过计算查询结果中每一个对象所关联的对象集合,从而得出总计值(也可以是平均值或总和),即为查询集的每一项生成聚合

  语法:

  QuerySet.annotate(结果变量名 = 聚合函数('列'))

  返回值:

  QuerySet

  1. 通过先用查询结果MyModel.objects.values查找查询要分组聚合的列

     MyModel.objects.values('列1','列2')

  2. 通过返回结果的QuerySet.annotate方法分组聚合的到分组结果

     QuerySet.annotate(名=聚合函数('列'))

###### 原生数据库操作

Django也可以支持 直接用sql语句的方式通信数据库

查询:使用MyModel.objects.raw()进行 数据库查询操作

语法:MyModel.objects.raw(sql语句,拼接参数)

返回值:RawQuerySet集合对象[只支持基础操作,比如循环]

 ~~~python
 books = models.Book.objects.raw('select * from bookstore_book')
 for book in books:
 	print(book)
 ~~~

使用原生语句时小心sql注入

定义:用户通过数据上传,将恶意的sql语句提交给服务器,从而达到攻击效果



###### orm多表查询

[多表查询教程](https://www.cnblogs.com/moyui/articles/12634902.html)



##### ORM - 删除

单个数据删除

1. 查找查询结果对应的一个数据对象

2. 调用这个数据对象的delete()方法实现删除

    ~~~python
    try :
    	auth = Author.objects.get(id=1)
    	auth.delete()
    except:
    	print(删除失败)
    
    ~~~

批量删除

1. 查找查询结果集中满足条件的全部QuerySet查询集合对象

2. 调用查询结合对象的delete()方法实现删除

    ~~~
    auths = Author.objects.filter(age_gt=65)
    auth.delete()
    ~~~

   



**伪删除**

1. 通常不会轻易在业务里把数据真正删掉，取而代之的是做伪删除，即在表中添加一个布尔型字段(is_active)，默认是True；执行删除时，将欲删除数据的is_active字段置为False
2. 注意：用伪删除时，确保显示数据的地方均加了is_active=true的过滤查询



##### F对象和Q对象

###### F对象

- 一个F对象代表数据库中某条记录的字段的信息

- 作用:

  通常是对数据库中的字段值再不获取的情况下进行操作

  用于类属性(字段)之间的比较

- 语法

   ~~~python
   from django.db.models import  F
   F('列名')
   ~~~

- 示例1:

   ~~~python
   Book.objects.all().update(market_price=F('market_price')+10)
   ~~~

- 示例2:对数据库两个字段的值进行比较

   ~~~
   from django.models import F 
   from bookstore.models import Book
   books = Book,objects.filter(market_price__gt=F('price'))
   ~~~

##### Q对象

当在获取查询结果集,使用复杂的逻辑或|,逻辑非~和&(and)操作时可以借助Q对象进行操作

Q对象在数据包django.对比.models中,需先导入

 ~~~
 Book.objects.filter(Q(price__lt=20|Q(pub='清华大学出版社'))
 ~~~















##### Django shell

在django提供了一个交互式的操作项目交django shell ,能够在交互模式用项目工程的代码执行相应的操作

利用django shell 可以代替编写view的代码进行直接操作

**tips:**项目代码发生变化时,重新进入Django shell 

启动方式:

 ~~~python
 python3 manage.py shell
 ~~~

使用方法:

![iShot2022-01-07 14.34.55](/Users/cobb/Documents/屏幕截图/iShot2022-01-07 14.34.55.png)

![iShot2022-01-07 14.41.20](/Users/cobb/Documents/屏幕截图/iShot2022-01-07 14.41.20.png)

## admin管理后台

### 创建后台管理账号 - 该账号为管理后台最高权限账号

~~~
python3 manage.py createsuperuser
~~~

### 注册自定义类型类

若要自己定义的模型类也能在admin后台管理界面显示和管理

需要将自己的类注册到后台管理界面

注册步骤:

1. 在应用app中的admin.py中导入注册要管理的模型models类,如:

    ~~~python
    from .models import Book
    ~~~

2. 调用admin.site.register方法进行注册,如:

    ~~~
    admin.site.register(自定义模型类)
    ~~~

   

### 模型管理器类

作用:为后台界面添加便于操作的新功能

说明:后台管理器类须继承自django.contrib.admin里的ModelAdmin类

使用方法:

1. 在<应用app>/admin.py里定义模型管理器类

    ~~~python
    class XXXXManager(admin.Modeladmin):
    	....
    ~~~

2. 绑定注册模型管理器和模型类

    ~~~python
    from django.contrib import admin
    from .models import *
    admin.site.register(YYYY,XXXXManager)   #绑定 YYYY模型类与管理器类 XXXXManager 
    ~~~

   

 ~~~python
 class BookManager(admin.ModelAdmin):
     #列表显示哪些字段的列
     list_display = ['id','title','pub','price']
     #控制哪些字段可以链接到修改页
     list_display_links = ['title']
     #添加过滤器
     list_filter = ['title']
     #添加搜索框[模糊查询]
     search_fields = ['title']
     #添加可在列表页编辑的字段
     list_editable = ['price']
 
 admin.site.register(Book,BookManager)
 ~~~



### 关系映射

#### 一对一

#####  创建

语法:OneToOneField(类名,on_delete=xxx)

~~~python
 class A(model.Model):
 	...
 class B(model.Model):
 	属性 = models.OneToOneField(A,on_delete = xxx)
~~~

特殊字段选项(必须)

on_delete : 级联删除

1. moedls.CASCADE 级联删除.Django模拟sql约束ON DELETE CASCADE的行为,并删除包含ForeignKey的对象
2. models.PROTECT抛出ProtectedError以阻止被引用对象的删除,等同于mysql默认的RESTRICT
3. SET_NULL设置ForeignKey null,需指定null = True
4. SET_DEFAULT 将ForeignKey设置为其默认值,必须设置ForeignKey的默认值



示例:

 ~~~python
 from django.db import models
 class Author(models.Model):
 	name = models.CharField('作家',max_length=50)
 class wife(models.Model):
 	name = models.CharField('妻子',max_length=50)
 	#增加一对一属性
 	author = models.OneToOneField(Author,on_delete=models.CASCADE)
 ~~~

##### 创建数据

- 无外键的模型列[Author]:

  author1 = Author.objects.create(name='王老师')

- 有外键的模型类 [wife]

  wife1=wife. objects createname 王夫人，author= Author1）#关联王老师 obj
  wife1=wife. objects. create name-'王夫人，author id=1）#关联王老师对应主键值

##### 查询数据

1. 正向查询:直接通过外键属性查询,称为正向查询

    ~~~
    #通过wife 找到author
    from .models import wife
    wife = wife.objects.get(name = '王夫人')
    print(wife.name,'的老公是',wife.author.name)
    ~~~

2. 反向查询:没有外键属性的一方,可以调用反向属性查询到关联的另一方



#### 一对多

##### 创建

语法:当一个A类对象可以关联多个B对象时

 ~~~python
 class A(models.Model):
 	...
 class B(models.Model):
 	属性 = models.ForeignKey("一"的模型类,on_delete=xx)
 ~~~



##### 创建数据

先创建一，再创建

~~~python
from .models import *
pub1 = Publisher.objects.create(name = '清华大学出版社')
Book.objects.create(title = 'c++',publisher = pub1)
Book.objects.create(title = 'java',publisher_id = 1)
~~~



##### 查询数据

1. 正向查询 [通过Book 查询 Publisher]

    ~~~python
    通过 publisher 属性查询即可
    book.publisher
    
    abook = Book.objects.get(id= 1)
    print(abook.title,'出版社是:',abook.publisher.name )
    ~~~

2. 反向查询 [通过Publisher 查询 对应的所有的Book]

   需要用到反向属性

    ~~~python
    #通过出版社查询对应的书
    pub1 Pub lisher. objects. get（name=清华大学出版社） 
    books= pub. book set.a1   #通过 book set 获取 pub1 对应的多个 Book 数据对象
    # books = Book. objects. filter（publisher=pub1）#也可以采用此方式获取
     prInt（"清华大学出版社的书有："）
     for book in books
     print(book title)
    ~~~



#### 多对多

语法:在关联的两个类中的任意一个类中,增加

 ~~~
 属性 = models.ManyToManyField(MyModel)
 ~~~



##### 创建

示例:

一个作者可以出版多个书籍

一本书可以同时被多个作者同时编写

 ~~~python
 class Author (models.Model):
 	...
 class Book(models.Model):
 	...
 	author = models.ManyToManyField(Author)
 ~~~



##### 创建数据

方案一:先创建author 再关联 book

 ~~~python
 author1 = Author.objects.create(name='吕老师')
 author2 = Author.objects.create(name='王老师')
 book11 = author1.book_set.create(title='python')
 author2.book_set.add(book11)
 ~~~



方案二:先创建book 再关联author

 ~~~python
 book = Book.objects.create(title= 'python')
 author3 = book.authors.create(name= 'guoxiaonao')
 book.authors.add(author1)
 ~~~



##### 查询数据

1. 正向查询 有多对多属性的对象 查 另一方

   通过Book查询对应的所有的Author

   此时多对多属性 等价于 objects

    ~~~python
    book.authors.all()  # 获取book对应的所有的author 信息
    book.authors.filter(age__gt=80)  # 获取book对应的作者中年龄大于80的作者
    ~~~

2. 反向查询

   通过Author查询对应的所有的Book

   利用反向属性book_set

    ~~~
    author.book_set.all()
    author.book_set.filter()
    ~~~

   

## cookies 和 session

### 会话

- 从打开浏览器访问一个网站，到关闭浏览器结束此次访问，称之为一次会话
- HTTP 协议是无状态的，导致会话状态难以保持
-  *Cookies 和 Session 就是为了保持会话状态而诞生的两个存储技术*



![image-20220111172759218](/Users/cobb/Library/Application Support/typora-user-images/image-20220111172759218.png)



### Cookies    ---长期存储

#### 定义

cookies 是保存在刻画段浏览器上的存储空间

#### 特点

-  cookies 在浏览器上是以键-值对的形式进行存储的，键和值都是以 ASCII 字符串的形存储（不能是中文字符串）
- 存储的数据带有生命周期 
- cookies 中的数据是按域存储隔离的，不同的域之间无法访问 
- cookies 的内部的数据会在每次访问此网时都会携带到服务器端，如果 cookies 过大会降低响应速度

#### Cookies的使用 

##### 存储

 ~~~
  HttpResponse. set_cookie(key, value='' , max_age=None, expires=None)
  -key cookie 的名字 
  -value： cookie 的值 
  -max_ age： cookie 存活时间，秒为单位 
  -expIres：具体过期时间
  -当不指定 max age 和 expires 时关闭浏览器时此数据失效
 ~~~

##### 删除 或 获取

删除 Cookies 

- HttpResponse. delete_cookie(key)

- 删除指定的 key 的 Cookie。如果 key 不存在则什么也不发生

获取 Cookies

- 通过 request. COOKIES 绑定的字典（dict）获取客户端的 COOKIES

数据

- value = request. COOKIES.get ('cookies 名'，'默认值'）



### session     ---短期存储

session是在服务器上开辟一段空间用于保留浏览器和服务器交互时的重要数据

实现方式:

- 使用session需要在浏览器客户端启动cookies,且在cookies中存储sessionid
- 每个客户端都可以在客户端都可以在服务器端有一个独立的session
- 注意:不同的请求者之间不会共享这个数据,与请求者一一对应



#### session 初始配置

settings.py中配置session

1. 向INSTALLED_APPS列表中添加

    ~~~python
    INSTALLED_APPS = [
    	#启用 session应用
    	'django.contrib.session',
    ]
    ~~~

2. 向MIDDLEWARE列表中添加

    ~~~python
    MIDDLAEWARE = [
    	# 启用 Session 中间件
    	'django.contrib.sessions.middleware.SessionMiddleware'
    	]
    ~~~



#### session的使用

session对于对象是一个类似于字典的SessionStore类型的对象,可以用类似于字典的方式进行操作

session能够存储如字符串,整型,字典,列表等

1. 保存session的值到服务器

   request.session['KEY'] = VALUE

2. 获取session的值

   value = request.session['KEY']

   value = request.session.get('KEY',默认值)

3. 删除session

   del request.session['KEY']



![image-20220111192926827](/Users/cobb/Library/Application Support/typora-user-images/image-20220111192926827.png)

![image-20220111193019999](/Users/cobb/Library/Application Support/typora-user-images/image-20220111193019999.png)





## djang实现前后端数据交互

Django 从后台往前台传递数据时有多种方法可以实现。

最简单的后台是这样的：

```
from django.shortcuts import render

def main_page(request):
    return render(request, 'index.html')
```

这个就是返回index.html的内容，但是如果要带一些数据一起传给前台的话，该怎么办呢？

### 一 view -> HTML 使用Django模版

这里是这样：后台传递一些数据给html，直接渲染在网页上，不会有什么复杂的数据处理（如果前台要处理数据，那么就传数据给JS处理）

Django 代码：

```
from django.shortcuts import render

def main_page(request):
    data = [1,2,3,4]
    return render(request, 'index.html', {'data': data})
```

html使用 `{{ }}` 来获取数据

```
<div>{{ data }}</div>
```

可以对可迭代的数据进行迭代：

```
{% for item in data%}
<p>{{ item }}</p>
{% endfor %}
```

该方法可以传递各种数据类型，包括list，dict等等。
而且除了 `{% for %}` 以外还可以进行if判断，大小比较等等。具体的用法读者可以自行搜索。

### 二 view-> JavaScript

如果数据不传给html用，要传给js用，那么按照上文的方式写会有错误。
需要注意两点：

1. views.py中返回的函数中的值要用 `json.dumps()` 处理
2. 在网页上要加一个 safe 过滤器。

代码：
views.py

```
# -*- coding: utf-8 -*-
 
import json
from django.shortcuts import render
 
def main_page(request):
    list = ['view', 'Json', 'JS']
    return render(request, 'index.html', {
            'List': json.dumps(list),
        })
```

JavaScript部分：

```
var List = {{ List|safe }};
```

### 三 JavaScript Ajax 动态刷新页面

这个标题的意思是：网页前台使用Ajax发送请求，后台处理数据后返回数据给前台，前台不刷新网页动态加载数据

Django 代码：

```
def scene_update_view(request):
    if request.method == "POST":
            name = request.POST.get('name')
            status = 0
            result = "Error!"
            return HttpResponse(json.dumps({
                "status": status,
                "result": result
            }))
```

JS 代码：

```
        function getSceneId(scece_name, td) {
            var post_data = {
                "name": scece_name,
            };

            $.ajax({
                url: {% url 'scene_update_url' %},
                type: "POST",
                data: post_data,
                success: function (data) {
                    data = JSON.parse(data);
                    if (data["status"] == 1) {
                        setSceneTd(data["result"], scece_name, td);
                    } else {
                        alert(data["result"]);
                    }
                }
            });
        } 
```

JS 发送ajax请求，后台处理请求并返回status, result
在 `success:` 后面定义回调函数处理返回的数据，需要使用 `JSON.parse(data)`



 
