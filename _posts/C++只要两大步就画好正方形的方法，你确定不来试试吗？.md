---
title: 用C++只要两大步就画好正方形的方法，你确定不来试试吗？
top: false
cover: false
password: 'null'
toc: true
mathjax: true
summary: 'null'
tags:
  - C++
categories:  
date: 2020-03-03 22:34:59
---

# 准备工作

//准备工作![](http://q6mgt5ib5.bkt.clouddn.com/C%2B%2B%E7%94%BB%E6%AD%A3%E6%96%B9%E5%BD%A2.png)


void initialize()
    {
        pen.cls();
        pen.showXY(100, 1, 2);
        pen.up();
        pen.moveTo(-150, -150);
        pen.setAngle(90);
        pen.down();
    }

# 画正方形

//画正方形![](http://q6mgt5ib5.bkt.clouddn.com/C%2B%2B%E7%94%BB%E6%AD%A3%E6%96%B9%E5%BD%A2%E6%88%90%E5%8A%9F.png)
void draw_square()
{
    pen.fd(300);
    pen.lt(90);
    pen.fd(300);
    pen.lt(90);
    pen.fd(300);
    pen.lt(90);
    pen.fd(300);
    pen.lt(90);
}

int main()
{
    initialize();
    draw_square();
    return 0;
}