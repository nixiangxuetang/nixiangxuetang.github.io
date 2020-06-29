---
title: 生活中的实用Python（一）
top: false
cover: false
password: 'null'
toc: true
mathjax: true
summary: 'null'
tags:
  - Python
categories: 生活中的实用编程系列
date: 2020-03-01 23:21:41
---

# 做一个软件-恋爱纪念日

```python
import turtle, time

turtle.title("恋爱纪念日")

def drawGap(): #绘制数码管间隔
    turtle.penup()
    turtle.fd(5)
    

def drawLine(draw):   #绘制单段数码管
    drawGap()
    turtle.pendown() if draw else turtle.penup()
    turtle.fd(40)
    drawGap()
    turtle.right(90)

def drawDigit(d): #根据数字绘制七段数码管
    drawLine(True) if d in [2,3,4,5,6,8,9] else drawLine(False)
    drawLine(True) if d in [0,1,3,4,5,6,7,8,9] else drawLine(False)
    drawLine(True) if d in [0,2,3,5,6,8,9] else drawLine(False)
    drawLine(True) if d in [0,2,6,8] else drawLine(False)
    turtle.left(90)
    drawLine(True) if d in [0,4,5,6,8,9] else drawLine(False)
    drawLine(True) if d in [0,2,3,5,6,7,8,9] else drawLine(False)
    drawLine(True) if d in [0,1,2,3,4,7,8,9] else drawLine(False)
    turtle.left(180)
    turtle.penup()
    turtle.fd(20)

def drawDate(date):
    turtle.pencolor("red")
    for i in date:
        if i == '-':
            turtle.write('年',font=("Arial", 18, "normal"))
            turtle.pencolor("green")
            turtle.fd(40)
        elif i == '=':
            turtle.write('月',font=("Arial", 18, "normal"))
            turtle.pencolor("blue")
            turtle.fd(40)
        elif i == '+':
            turtle.write('日',font=("Arial", 18, "normal"))
            turtle.fd(40)
        else:
            drawDigit(eval(i))

def all(day):
    turtle.goto(-350,-300)
    turtle.pencolor("orange")
    turtle.write('总共',font=("Arial", 30, "normal"))
    turtle.fd(110)
    for j in day:
        drawDigit(eval(j))
    turtle.write('天',font=("Arial", 18, "normal"))

def count(t1,t2,t3):
    t=t1*365
    if t2 in [1,2]:
        t+=t2*30
    if t2 in [3]:
        t=t+91
    if t2==4:
        t+=122
    if t2==5:
        t+=152
    if t2==6:
        t+=183
    if t2==7:
        t+=213
    if t2==8:
        t+=244
    if t2==9:
        t+=275
    if t2==10:
        t+=303
    if t2==11:
        t+=334
    t+=t3
    return(str(t))

def text():
    turtle.penup()
    turtle.goto(-350,370)
    turtle.pendown()
    turtle.write('今天是：',font=("Arial", 18, "normal"))
    turtle.pensize(5)
    turtle.penup()
    turtle.goto(-350,300)
    turtle.pendown()
    drawDate(time.strftime('%Y-%m=%d+',time.gmtime()))
    turtle.penup()
    turtle.goto(-350,200)
    turtle.pensize(1)
    turtle.pendown()
    turtle.pencolor("black")
    turtle.write('大钧和琦悦在一起：',font=("Arial", 18, "normal"))
    turtle.penup()
    turtle.goto(-350,100)
    turtle.pendown()
    turtle.pensize(5)
    drawDate('2019-11=3+')
    turtle.penup()
    turtle.goto(-350,0)
    turtle.pensize(1)
    turtle.pendown()
    turtle.pencolor("black")
    turtle.write('我们一起度过了：',font=("Arial", 18, "normal"))
    turtle.penup()
    turtle.goto(0,-100)
    turtle.pensize(1)
    turtle.pendown()

def main():
    turtle.setup(900, 900, 200, 0)
    text()
    turtle.penup()
    turtle.fd(-350)
    turtle.pensize(5)
#    drawDate('2019-10=10+')
    t1=time.gmtime()
    t2=t1.tm_year-2019
    t3=t1.tm_mon-11
    if t3<0:
        t2-=1
        t3+=12
    t4=t1.tm_mday-3
    if t4<0:
        t3-=1
        if t1.tm_mon-1 in [1,3,5,7,8,10,12]:
            t4+=31
        else:
            t4+=30
    
    total=count(t2,t3,t4)
    drawDate(str(t2)+'-'+str(t3)+'='+str(t4)+'+')
    all(total)
    turtle.hideturtle()
    turtle.done()

main()

```



## 1. 在命令行用pip安装 pyinstaller包

```python
pip install pyinstaller
```

## 2.下载安装pyinstaler运行时所需要的windows扩展pywin32

[mhammond/pywin32](https://github.com/mhammond/pywin32/releases)

选择最新版的下载，**注意要选择对应的python版本(version)和python位数(bittedness)**

通过在命令行输入python查看python版本和位数

如下所示为python3.7的64位，需要下载[pywin32-227.win32-py3.7.exe](https://github.com/mhammond/pywin32/releases/download/b227/pywin32-227.win32-py3.7.exe)

```text
Python 3.7.3 ... [MSC v.1900 64 bit (AMD64)] on win32
```

## 3.在命令行中直接输入下面的指令即可

```python
pyinstaller [opts] yourprogram.py 
```

参数opts含义

-D –onedir 创建一个目录，包含exe文件，但会依赖很多文件（默认）

-c –console, –nowindowed 使用控制台，无界面(默认)

-F 指定打包后只生成一个exe格式的文件(必备)

-w –windowed, –noconsole 使用窗口，无控制台

-p 添加搜索路径，让其找到对应的库。

-i 改变生成程序的icon图标 

准备好图片，打开制作ico的网站[ico](http://www.bitbug.net/)

## 实例说明

- 比如你有个python程序叫test.py，绝对路径在[D:\project]，一行命令，软件做好

```text
pyinstaller -F D:\project\test.py
```

- 如果希望更换程序图标

```python
pyinstaller -F -w -i       D:\project\test.ico        D:\project\test.py
```

## 结果展示

然后就会生成**build**和**dist**文件夹，如果是选择了-F参数，那么dist文件夹下就是你要的程序，~~build文件夹可以删除~~

**注意**，路径用英文，不要中文。