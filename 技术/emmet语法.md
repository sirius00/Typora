# vscode中emmet语法



## 1 html:5

新建文档，输入html:5 然后摁下Tab键，即可创建如下的html5基本结构：



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

也可以先输入`!`然后摁快捷键Tab，同样可以快速创建html5文档

## 2 简写规则

Emmet语法直接简写，常用的简写规则如下：

| 简写（然后使用Tab键） | 描述                                              |
| --------------------- | ------------------------------------------------- |
| E                     | E代表html标签，即直接写标签名+Tab键就快速创建标签 |
| E#id                  | 快速创建带id属性的标签                            |
| E.class               | 快速创建带class属性的标签                         |
| E[attr=foo]           | 快速创建某个特定属性的标签                        |
| E{FOO}                | 快速创建包含内容foo的标签                         |
| E>N                   | 快速创建父子结构，N是E的子元素                    |
| E+N                   | 快速创建兄弟结构，N是E的同级元素                  |
| E^N                   | N是E的上级元素，通常搭配E>N来使用                 |
| E*N                   | 快速创建N个的E标签，N代表数字                     |
| E$*N                  | 快速创建N个带自动编号的的E元素                    |
| E>lorem               | 在E元素中随机添加文本                             |
| E*N>M                 | 等用于（E>M）*N，快速创建N个父子结构              |



eg:

> li*3>a

创建如下结构



```html
<li><a href=""></a></li>
<li><a href=""></a></li>
<li><a href=""></a></li>
```

> div#item$.class$$*3

创建如下结构



```html
<div id="item1" class="class01"></div>
<div id="item2" class="class02"></div>
<div id="item3" class="class03"></div>
```

> ul>li{$}*6

创建如下结构



```html
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
</ul>
```

> table>thead>tr>td*5^^tbody>tr>td*5

创建如下结构



```html
<table>
    <thead>
        <tr>
            <th></th>
            <th></th>
            <th></th>
            <th></th>
            <th></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>
```



![General 3800x2160 digital art digital artwork car vehicle flowers plants yellow flowers Mercedes-Benz Mercedes-Benz 300SL yellow cars](https://w.wallhaven.cc/full/x8/wallhaven-x8o5mo.png)
