[TOC]

# Sublime安装包管理插件

在控制台输入以下代码：

```
import  urllib.request,os;pf='Package Control.sublime-package';ipp=sublime.installed_packages_path();urllib.request.install_opener(urllib.request.build_opener(urllib.request.ProxyHandler()));open(os.path.join(ipp,pf),'wb').write(urllib.request.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read())
```

Package Control下载其他包时：“Package Control: Error parsing JSON from channel https://packagecontrol.io/channel_v3.json.”

这是由于GFW，导致的无法访问该网页，可以将channel v3.json下载下来，再修改配置文件中channel的路径。

### 如何在Sublime Text3中运行python程序

[教程](https://blog.csdn.net/zxy987872674/article/details/81707241)

### pip

由于第三方包默认下载地址在国外，故可以自己配置软件源，提高下载速度。

（1）打开文件资源管理器
--------在地址栏中输入 %appdata%
（2）手动创建一个文件夹叫做 pip
（3）在pip的文件夹里面新建一个文件 pip.ini
（4）文件中写如下内容(豆瓣源)

```
[global]
index-url = http://pypi.douban.com/simple
[install]
trusted-host=pypi.douban.com
```



# Python语法

### python程序出错

python解释器提供traceback，指出程序在哪里出错了。

<img src="C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1569418961618.png" alt="1569418961618" style="float: left;" />





### 字符串

用单引号或双引号括起来。

方法：

```python
"""title():首字母大写，其余字母小写
upper():都大写
lower():都小写
lstrip():删除开头的所有空格
rstrip()：删除结尾的所有空格
strip()：删除开头和结尾的所有空格
str():把字符串转为数值
"""

name='adA love'
print(name.title())		#Ada Love
print(name.upper())		#ADA LOVE
print(name.lower())		#ada love

str='   xxxx   y   '
print(str+"!")
str_l=str.lstrip()
print(str_l+"!")
str_r=str.rstrip()
print(str_r+"!")
str_all=str.strip()
print(str_all+"!")
"""   xxxx   y   !
xxxx   y   !
   xxxx   y!
xxxx   y!
"""
```



### 列表

+ 修改

```
list=['one','two','three']
list[0]=1
```

+ 增加
  + append()
  + insert()

```python
#声明列表
list=['one','two','three']
#遍历列表
for el in list:
	print(el)
#末尾添加元素
list.append('four')
print(list[3])
print(list[-1])
#任意地方添加元素
list.insert(0,'zero')
print(list[0])
```

+ 删除

  + del
  + pop():按下标删除
  + remove()：按值删除（不过本质仍旧是基于下标的）

  ```python
  #del删除任一元素
  del list[3]
  for el in list:
  	print(el)
  #pop()删除元素,删除的是最后一个元素，删除的元素可以被继续使用
  #pop(index)，删除指定下标的元素
  num=list.pop()
  num2=list.pop(1)
  print("\n")
  print(num)
  print(num2)
  for el in list:
  	print(el)
  print("\n")
  #根据值删除元素,remove(),单次值删除一个值
  list.remove('zero')
  for el in list:
  	print(el)
  ```

+ 排列（reverse=True:逆序排）

  + sort():列表中元素是排好序后的
  + sorted():列表中的元素仍是原来的

+ range()

  + `range(101)`可以产生一个0到100的整数序列。
  + `range(1, 100)`可以产生一个1到99的整数序列。
  + `range(1, 100, 2)`可以产生一个1到99的奇数序列，其中2是步长，即数值序列的增量。

```python
for value in range(1,5):
	print(value)
number=list(range(1,6))			#创建列表
print(number)
number=[value**2 for value in range(1,11)]	#列表解析
print( number)

"""
1
2
3
4
[1, 2, 3, 4, 5]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
"""
```



+ 切片

```python
number=[1,2,3,4,5]
num1=number[:3]
print(num1)
num1=number[-3:]
print(num1)
num1=number[1:2]
print(num1)
num1=number		#两者指向同一个列表
print(num1)
num1.append(10)
print(number)

"""
[1, 2, 3]
[3, 4, 5]
[2]
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5, 10]
"""
```



### 思维导图（变量、列表、元组、列表操作）

<img src="E:\新建文件夹\0001.jpg"  />



### 函数

函数的参数可以是默认的，也可以是可变的，故Python不像	其他语言一样支持函数的重载。

```python
#默认参数
def add (a=0,b=1,c=2):
	return a+b+c

print(add('xy','2','3'))		#xy23
print(add(10))					#13

#可变参数
def add_1(*args):
	sum=0
	for i in args:
		sum+=i
	return sum

print(add_1())	#0
print(add_1(10))	#10
print(add_1(10,20))	#30

```



如果一个文件中有多个同名函数，那么最后一个函数会覆盖上面所有函数。

```python
def a():
	print('a')

def a():
	print('aa')

a()		#aa

```

如何解决呢？

<font color=red>用模块管理函数</font>

```python
import module1
import module2
module1.a()
module2.a()

```



### IO

+ 文本数据读写

```python
with open('file.txt','w') as filename:
	filename.write("hello world\n")
	filename.write("さよなら")

```

‘w’:将原文件中的数据全部清除，再写入

```python
#执行读取操作时，最终指向文件末尾，故之后再读取的值为空
with open('file.txt','r') as filename:
	file=filename.read()
	print(type(file))		#str
	print(file)

	list=filename.readlines();
	print(type(list))
	print(list)

	for line in filename:
		print(line.strip())

```

+ spilt():分析文本

  以空格为间隔符

```python
with open('num.txt','r') as filename:     #1 2 3 4 5 6 7 8 9 10
	list=filename.read().split()
	for i in list:
		print(int(i)**2)

```

+ 复制图片(读写二进制文件)

```python
with open('E:/lenovo/Pictures/ibus.PNG','rb') as img:
	data=img.read();
	print(type(data))		#bytes
	print(data)
with open('copy_img.gif','wb') as img2:
	img2.write(data)

```

+ 读写JOSN文件

  用于处理列表和字典

  ```python
  import json
  mydict = {
          'name': '骆昊',
          'age': 38,
          'qq': 957658,
          'friends': ['王大锤', '白元芳'],
          'cars': [
              {'brand': 'BYD', 'max_speed': 180},
              {'brand': 'Audi', 'max_speed': 280},
              {'brand': 'Benz', 'max_speed': 320}
          ]
      }
  with open('dict.json','w',encoding='utf-8') as f_obj:
  	json.dump(mydict,f_obj)
  
  with open('dict.json','r') as f_obj:
  	dict=json.load(f_obj)
  	print(dict)
  
  ```

  

### 异常

+ try..except...else

  如果无异常执行else中的语句

+ try...except...finally

  无论有无异常都会执行finally中的语句

  ```python
  with open('file.txt','w') as filename:
  
  	try:
  		file=filename.read()
  	except Exception as err:
  		print(err)
  	finally:
  		filename.write("hello world\n")
  		filename.write("さよなら")	
  
  ```

+ pass语句

  可以在代码块中使用，让python什么都不要做

# 实例

### import this

输出：

The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!



### import turtle

绘制矩形：

```python
import turtle
turtle.pensize(10)
turtle.pencolor('green')
turtle.forward(100)
turtle.left(90)
turtle.forward(100)
turtle.left(90)
turtle.forward(100)
turtle.left(90)
turtle.forward(100)
turtle.mainloop()


```

<img src="C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1569488902752.png" alt="1569488902752" style="zoom:80%;float:left" />

### 最大公约数和最小公倍数

```python
a=int(input())
b=int(input())
num=a*b
while True:
	if b==0:
		break;
	else:
		c=a%b
		a,b=b,c
print('最大公约数为：',a)
print('最小公倍数为：',num/a)

```



### 爬网站



# 错误

### OSError: [Errno 22] Invalid argument: '\u202a\u202aE:/lenovo/Pictures/ibus.PNG'

1. 路径用“/”
2. 复制的路径带有特殊字符，所以出错

### ModuleNotFoundError

```
pip install [module]

#很容易撞墙

```

