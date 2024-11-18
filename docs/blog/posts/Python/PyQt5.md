---
date: 
    created: 2024-11-18
categories:
    - Python
tags:
    - GUI
---
# PyQt5 Python桌面开发
PyQt是一个创建GUI应用程序的工具包。它是Python 编程语言和Qt库的成功融合。Qt库是最强大的库之一。 PyQt 是由Phil Thompson 开发。
<!-- more -->
## PyQt5 介绍与安装
### Qt
Qt （官方发音 `[kju:t]` ）是一个跨平台的C++开发库 ，主要用来开发图形用户界面 （Graphical User Interface ， GUl） 程序

Qt是纯 C++开发的，正常情况下需要先学习C语言、然后在学习C++然后才能使用Qt开发带界面的程序

多亏了开源社区使得Qt 还可以用Python 、 Ruby 、 Perl 等脚本语言进行开发。 

Qt 支持的操作系统有很多，例如通用操作系统 Windows、Linux、Unix，智能手机系统Android 、iOS，嵌入式系统等等。可以说是跨平台的。

Qt 官网 ：https://doc.qt.io/qt-5/index.html

### PyQt

PyQt 实现了一个Python模块集。它有超过300类，将近6000个函数和方法。它是一个多平台的工具包，可以运行在所有主要操作系统上，包括UNX Windows和Mac。 PyQt采用双许可证，开发人员可以选择GPL和商业许可。在此之前， GPL的版本只能用在Unix上，从PyQt的版本4开始， GPL许可证可用于所有支持的平台。最新版本是PyQt6。

PyQt是Python语言的GUI （Graphical User Interface ，简称 GUI ，又称图形用户接口）编程解决方案之一

可以用来代替Python内置的 Tkinter 。其它替代者还有 PyGTK 、  wxPython 等，与Qt一样，PyQt是一个自由软件。

### Python GUI开发热门选择
- Tkinter

Python官方采用的标准，优点是作为Python标准库、稳定、发布程序较少，缺点是控件相对较少。

- wxPython

基于wxWidgets的Python库，优点是控件比较丰富 ，缺点是稳定性相对差点、文档少、用户少。

- PySide2、PyQt5

基于Qt的Python库，优点是控件比较丰富、跨平台体验好、文档完善、用户多。缺点是库比较大，发布出来的程序比较大。

### 安装

首先可以使用虚拟环境进行安装，这里不做演示。
安装pyqt5的命令：
```shell
pip install pyqt5 -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## PyQt基本UI
### 第一个PyQt程序
```python
import sys

from PyQt5.QtWidgets import QApplication, QWidget

if __name__ == '__main__':
    # 1.只要是Qt制作的app,必须有且只有1个QApplication对象
    # 2.sys.argv当做参数的目的是将运行时的命令参数传递给QApplication对象
    app = QApplication(sys.argv)

    w = QWidget()
    
    # 设置窗口标题
    w.setWindowTitle("第一个PyQt")

    # 展示窗口
    w.show()

    # 程序进行循环等待状态
    app.exec()

```

### 模块介绍
PyQt中有非常多的功能模块，开发中最常用的功能模块主要有三个：
- QtCore:包含了核心的非GUI的功能。主要和时间、文件与文件夹、各种数据、流、URLs、mime类文件、进程与线程一起使用

- QtGui::包含了窗口系统、事件处理、2D图像、基本绘画、字体和文字类

- QtWidgets:包含了一些列创建桌面应用的UI元素

可以参考PyQt官网的所有模块，地址：
[https:/www.riverbankcomputing.com/static/Docs/PyQt5/module_.index.html#ref-module-index](https:/www.riverbankcomputing.com/static/Docs/PyQt5/module_.index.html#ref-module-index)

C++具体实现的API文档，地址：
[https://doc.qt.io/qt-5/qtwidgets-module.html](https://doc.qt.io/qt-5/qtwidgets-module.html)

!!! info "提示"
     用到什么功能就它相关的api或者别人分享的使用心得，这是学习最快的方式

### 基本UI
窗口内的所有控件，若想在窗口中显示，都需要表示它的父亲是谁，而不能直接使用show函数表示。
#### 1.按钮
按钮对应的控件名称为`QPushButton`，位于`PyQt5.QtWidgets`里面
```python
import sys

from PyQt5.QtWidgets import QApplication, QWidget, QPushButton

if __name__ == '__main__':
    app = QApplication(sys.argv)

    w = QWidget()

    # 设置窗口标题
    w.setWindowTitle("第一个PyQt")

    # 在窗口里面添加控件
    btn = QPushButton("按钮")

    # 设置按钮的父亲是当前窗口，等于是添加到窗口中显示
    btn.setParent(w)

    # 展示窗口
    w.show()

    # 程序进行循环等待状态
    app.exec()
```

#### 2.文本
纯文本控件名称为`QLabel`，位于`PyQt5.QtWidgets`里面
纯文本控件仅仅作为标识显示而已，类似输入内容前的一段标签提示（账号、密码）
```python
import sys

from PyQt5.QtWidgets import QApplication, QWidget, QLabel

if __name__ == '__main__':
    app = QApplication(sys.argv)

    w = QWidget()

    # 设置窗口标题
    w.setWindowTitle("第一个PyQt")

    # 下面创建一个Label（纯文本），在创建的时候制指定了父对象
    label = QLabel("账号:    ", w)

    # 显示位置与大小: x, y, w, h
    label.setGeometry(20, 20, 30, 30)

    # 展示窗口
    w.show()

    # 程序进行循环等待状态
    app.exec()

```

### 输入框
输入框的控件名称为`QLineEdit`，位于`PyQt5.QtWidgets`里面
```python
import sys

from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QLabel, QLineEdit

if __name__ == '__main__':
    app = QApplication(sys.argv)

    w = QWidget()

    # 设置窗口标题
    w.setWindowTitle("第一个PyQt")

    # 纯文本
    label = QLabel("账号", w)
    label.setGeometry(20, 20, 30, 20)

    # 文本框
    edit = QLineEdit(w)
    edit.setPlaceholderText("请输入账号")
    edit.setGeometry(55, 20, 200, 20)

    # 在窗口里面添加控件
    btn = QPushButton("注册", w)
    btn.setGeometry(50, 80, 70, 30)

    # 展示窗口
    w.show()

    # 程序进行循环等待状态
    app.exec()

```

### 调整窗口
```python
import sys

from PyQt5.QtWidgets import QApplication, QWidget, QDesktopWidget

if __name__ == '__main__':
    app = QApplication(sys.argv)

    w = QWidget()

    # 设置窗口标题
    w.setWindowTitle("第一个PyQt")

    # 窗口的大小
    w.resize(600, 300)

    # 将窗口设置在屏幕的左上角
    w.move(0, 0)

    # 调整窗口在屏幕中央显示
    center_pointer = QDesktopWidget().availableGeometry().center()
    x = center_pointer.x()
    y = center_pointer.y()
    # w.move(x,y)
    # w.move(X-150,y-150)
    print(w.frameGeometry())
    print(w.frameGeometry().getRect())
    print(type(w.frameGeometry().getRect()))
    old_x, old_y, width, height = w.frameGeometry().getRect()
    w.move(int(x - width / 2), int(y - height / 2))
    
    # 展示窗口
    w.show()

    # 程序进行循环等待状态
    app.exec()


```

### 设置窗口icon

```python
import sys

from PyQt5.QtGui import QIcon
from PyQt5.QtWidgets import QApplication, QWidget, QDesktopWidget

if __name__ == '__main__':
    app = QApplication(sys.argv)

    w = QWidget()

    # 设置窗口标题
    w.setWindowTitle("图标ICON")

    # 设置图标
    w.setWindowTitle('panda.png')

    # 显示QWidget
    w.show()

    app.exec()
```