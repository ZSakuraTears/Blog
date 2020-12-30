---
title: 'PyQt5总结'
date: 2020-10-30 20:24:46
tags: [Python]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(4).jpg.webp
isTop: false
---
[TOC]

#  基本功能
## 基本操作
```python
from PyQt5.QtWidgets import QApplication, QWidget
```
```python
app = QApplication(sys.argv)
```

每一pyqt5应用程序必须创建一个应用程序对象。sys.argv参数是一个列表，从命令行输入参数

```python
w = QWidget()
```

QWidget部件是pyqt5所有用户界面对象的基类。他为QWidget提供默认构造函数。

```python
w.resize(250, 250)
```

resize方法调整窗口大小

```python
w.move(300, 300)
```

move方法移动窗口在屏幕的位置

```python
w.setWindowTitle('Simple')
```

设置窗口标题

```python
w.show()
```

显示在屏幕上

```python
self.setGeometry(300, 300, 300, 300)
```

设置窗口位置和大小



## 图标

```python
self.setWindowIcon(QIcon('路径'))
```

设置窗口的图标

## 提示语

```python
from PyQt5.QtWidgets import (QWidget, QToolTip, 
    QPushButton, QApplication)
from PyQt5.QtGui import QFont   
```

```python
QToolTip.setFont(QFont('SansSerif', 10))
```

这种静态的方法设置一个用于显示工具提示的字体。我们使用10px滑体字体

```python
self.setToolTip('This is a <b>QWidget</b> widget')
```

创建一个提示，我们称之为settooltip()方法。我们可以使用丰富的文本格式

```python
btn = QPushButton('Button', self)
btn.setToolTip('This is a <b>QPushButton</b> widget')
```

创建一个PushButton并为他设置一个tooltip

```python
btn.resize(btn.sizeHint())
```

btn.sizeHint()为默认尺寸

## 关闭窗口

```python
qbtn = QPushButton('Quit', self)
qbtn.clicked.connect(QCoreApplication.instance().quit)
```

## 消息框

```python
from PyQt5.QtWidgets import QWidget, QMessageBox, QApplication
```

```python
def closeEvent(self, event):
        
        reply = QMessageBox.question(self, 'Message',
            "Are you sure to quit?", QMessageBox.Yes | 
            QMessageBox.No, QMessageBox.No)
 
        if reply == QMessageBox.Yes:
            event.accept()
        else:
            event.ignore()
```

关闭窗口是出发QCloseEvent。我们需要重写closeEvent方法

## 窗口显示在屏幕的中间

```python
#控制窗口显示在屏幕中心的方法    
    def center(self):
        #获得窗口
        qr = self.frameGeometry()
        #获得屏幕中心点
        cp = QDesktopWidget().availableGeometry().center()
        #显示到屏幕中心
        qr.moveCenter(cp)
        self.move(qr.topLeft())
```

QtGui,QDesktopWidget类提供了用户的桌面信息,包括屏幕大小。



# 布局管理

## 绝对定位

```python
lbl1 = QLabel('Zetcode', self)
lbl1.move(15, 10)
 
lbl2 = QLabel('tutorials', self)
lbl2.move(35, 40)
        
lbl3 = QLabel('for programmers', self)
lbl3.move(55, 70)        
        
self.setGeometry(300, 300, 250, 150)
self.setWindowTitle('Absolute')    
self.show()
```

## 框布局 Boxlayout

```python
okButton = QPushButton("OK")
cancelButton = QPushButton("Cancel")
 
hbox = QHBoxLayout()
hbox.addStretch(1)
hbox.addWidget(okButton)
hbox.addWidget(cancelButton)
 
vbox = QVBoxLayout()
vbox.addStretch(1)
vbox.addLayout(hbox)
        
self.setLayout(vbox)    
        
self.setGeometry(300, 300, 300, 150)
self.setWindowTitle('Buttons')    
self.show()
```

我们使用QHBoxLayout和QVBoxLayout，来分别创建横向布局和纵向布局。

```python
hbox = QHBoxLayout()
hbox.addStretch(1)
hbox.addWidget(okButton)
hbox.addWidget(cancelButton)
```

我们创建一个水平布局和添加一个伸展因子和两个按钮。两个按钮前的伸展增加了一个可伸缩的空间。这将推动他们靠右显示。

```python
vbox = QVBoxLayout()
vbox.addStretch(1)
vbox.addLayout(hbox)
```

创建一个垂直布局，并添加伸展因子，让水平布局显示在窗口底部

```python
self.setLayout(vbox)
```

最后,我们设置窗口的布局界面

## 表格布局 QGridLayout

```python
grid = QGridLayout()
self.setLayout(grid)

names = ['Cls', 'Bck', '', 'Close',
          '7', '8', '9', '/',
           '4', '5', '6', '*',
          '1', '2', '3', '-',
             '0', '.', '=', '+']

 positions = [(i, j) for i in range(5) for j in range(4)]

  for position, name in zip(positions, names):

       if name == '':
            continue
        button = QPushButton(name)
        grid.addWidget(button, *position)

```

```python
grid = QGridLayout()
self.setLayout(grid)
```

QGridLayout的实例被创建并设置应用程序窗口的布局。

names列表为这些按钮的标签

## 评论的例子

```python
def initUI(self):

    title = QLabel('Title')
    author = QLabel('Author')
    review = QLabel('Review')

    titleEdit = QLineEdit()
    authorEdit = QLineEdit()
    reviewEdit = QTextEdit()

    grid = QGridLayout()
    grid.setSpacing(10)

    grid.addWidget(title, 1, 0)
    grid.addWidget(titleEdit, 1, 1)

    grid.addWidget(author, 2, 0)
    grid.addWidget(authorEdit, 2, 1)

    grid.addWidget(review, 3, 0)
    grid.addWidget(reviewEdit, 3, 1, 5, 1)

    self.setLayout(grid)

    self.setGeometry(300, 300, 350, 300)
    self.setWindowTitle('Review')
    self.show()
```

我们创建一个窗口,其中有三个标签,两个行编辑和一个文本编辑窗口小控件。然后使用QGridLayout完成布局。

```python
grid = QGridLayout()
grid.setSpacing(10)
```

创建一个网格布局和设置组件之间的间距。

```python
grid.addWidget(reviewEdit, 3, 1, 5, 1)
```

在添加一个小的控件到网格的时候,我们可以提供小部件的行和列跨。在例子中,reviewEdit控件跨度5行。

# 菜单和工具栏

## 状态栏

```python
def initUI(self):

    self.statusBar().showMessage('Ready')

    self.setGeometry(300, 300, 250, 150)
    self.setWindowTitle('Statusbar')
    self.show()

```

用QMainWindow创建状态栏的小窗口

```python
self.statusBar().showMessage('Ready')
```

QMainWindow类第一次调用statusBar()方法创建一个状态栏。后续调用返回的状态栏对象。showMessage()状态栏上显示一条消息。

## 菜单栏

菜单栏是常见的窗口应用程序的一部分。(Mac OS将菜单条不同。得到类似的结果,我们可以添加以下行:menubar.setNativeMenuBar(假)。)

```python
def initUI(self):

    exitAction = QAction(QIcon('exit.png'), '&Exit', self)
    exitAction.setShortcut('Ctrl+Q')
    exitAction.setStatusTip('Exit application')
    exitAction.triggered.connect(qApp.quit)

    self.statusBar()

    # 创建一个菜单栏
    menubar = self.menuBar()
    # 添加菜单
    fileMenu = menubar.addMenu('&File')
    # 添加事件
    fileMenu.addAction(exitAction)

    self.setGeometry(300, 300, 300, 200)
    self.setWindowTitle('Menubar')
    self.show()

```

```python
exitAction = QAction(QIcon('exit.png'), '&Exit', self)        
exitAction.setShortcut('Ctrl+Q')
exitAction.setStatusTip('Exit application')
```

QAction可以操作菜单栏,工具栏,或自定义键盘快捷键。上面三行,我们创建一个事件和一个特定的图标和一个“退出”的标签。然后,在定义该操作的快捷键。
第三行创建一个鼠标指针悬停在该菜单项上时的提示。

```python
exitAction.triggered.connect(qApp.quit)
```

当我们点击菜单的时候，调用qApp.quit,终止应用程序。

## 工具栏

```python
def initUI(self):

    exitAction = QAction(QIcon('exit24.png'), 'Exit', self)
    exitAction.setShortcut('Ctrl+Q')
    exitAction.triggered.connect(qApp.quit)

    self.toolbar = self.addToolBar('Exit')
    self.toolbar.addAction(exitAction)

    self.setGeometry(300, 300, 300, 200)
    self.setWindowTitle('Toolbar')
    self.show()

```

在上面的例子中,我们创建一个简单的工具栏。工具栏有有一个按钮,点击关闭窗口。

```python
exitAction = QAction(QIcon('exit24.png'), 'Exit', self)
exitAction.setShortcut('Ctrl+Q')
exitAction.triggered.connect(qApp.quit)
```

类似于上面的菜单栏的例子,我们创建一个QAction事件。该事件有一个标签、图标和快捷键。退出窗口的方法

## 把他们放在一起

```python
import sys
from PyQt5.QtWidgets import QMainWindow, QTextEdit, QAction, QApplication
from PyQt5.QtGui import QIcon
 
 
class Example(QMainWindow):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):               
        
        textEdit = QTextEdit()
        self.setCentralWidget(textEdit)
 
        exitAction = QAction(QIcon('exit24.png'), 'Exit', self)
        exitAction.setShortcut('Ctrl+Q')
        exitAction.setStatusTip('Exit application')
        exitAction.triggered.connect(self.close)
 
        self.statusBar()
 
        menubar = self.menuBar()
        fileMenu = menubar.addMenu('&File')
        fileMenu.addAction(exitAction)
 
        toolbar = self.addToolBar('Exit')
        toolbar.addAction(exitAction)
        
        self.setGeometry(300, 300, 350, 250)
        self.setWindowTitle('Main window')    
        self.show()
        
        
if __name__ == '__main__':
    
    app = QApplication(sys.argv)
    ex = Example()
    sys.exit(app.exec_())
```

```python
textEdit = QTextEdit()
self.setCentralWidget(textEdit)
```

我们创建了一个QTextEdit,并把他设置为窗口的布局