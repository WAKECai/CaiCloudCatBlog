---
date: 
    created: 2024-11-17
categories:
    - AI
tags:
    - Programme
    - PyQt5
    - Homework
---
# 农夫过河 Farmer Crossing River

本篇文章将讲述一个经典的状态空间搜索问题，通过使用Python语言来进行解决，并辅助于图形化界面，添加交互性更加明显的观察到具体的实现细节。
<!-- more -->

## 题目介绍
有一个农夫带一只狐狸、一只小羊和一篮菜过河。假设农夫每次只能带一样东西过河，考虑安全，无农夫看管时，狐狸和小羊不能在一起，小羊和菜篮不能在一起。试设计求解该问题的状态空间，并画出状态空间图。

## 问题描述

- 农夫有三样东西：狐狸（$F$）、羊（$S$）、菜篮（$C$）
- 农夫每次只能带一样东西过去
- 如果农夫不在一边
  - 狐狸 和 小羊 不能独处
  - 小羊 和 菜篮 不能独处

目标：将农夫和三种物品安全地从左岸（Initial State）运到右岸（Goal State）

## 状态空间表示

使用元组 $(F, S, C, R)$ 来表示当前状态，其中：

-  $F, S, C$ 分别表示狐狸、小羊、菜篮的位置（左岸用 0 表示，右岸用 1 表示）
-  $R$ 表示农夫的位置（0 表示左岸，1 表示右岸）。

**初始状态** ：$(0,0,0,0)$
**目标状态** ：$(1,1,1,1)$

状态转移的规则：

- 农夫每次只能带自己和一种物品过河（或单独过河）。
- 转移后必须满足 **约束条件**，即不能让 ：
  - $S = C  \neq R$
  - $F = S \neq R$

## 设计

### 步骤



### 流程图

### UML图
``` mermaid
classDiagram
RiverGameUI <|-- State
class State{
    +int r
    +int f
    +int s
    +int c
    +bool is_safe()
    +[State] generate_next_states()
    +int other_side(current_side)
}
class RiverGameUI{
    +tk.Tk master
    +tk.Canvas canvas
    +State state
    +State goal_state
    +float start_time
    +draw_river_scene()
    +create_controls()
    +move(choice: str)
    +State calculate_next_state(choice: str)
    +update_canvas()
    +check_game_status()
    +start_game()
}
```


## 实现

### 界面设计
#### 界面组成
- 标题：显示`农夫过河问题-AI-名字-学号`
- 状态提示：当前游戏提示
- 河流场景：左岸、右岸、河流
- 动物和物品：农夫、狐狸、小羊、菜篮
#### 交互功能
按钮：

- 农夫单独过河
- 带狐狸过河
- 带小羊过河
- 带菜篮过河

动画：

- 物品和农夫的过河

提示：

- 非法操作：弹出警告框
- 游戏成功提示：弹出完成时间

### 功能模块

### 测试与展示


## 总代码

```python
import sys
import time
from PyQt5.QtWidgets import (
    QApplication, QMainWindow, QGraphicsView, QGraphicsScene,
    QGraphicsEllipseItem, QGraphicsRectItem, QPushButton, QLabel, QVBoxLayout, QWidget, QMessageBox
)
from PyQt5.QtGui import QBrush
from PyQt5.QtCore import Qt


class State:
    """状态类"""
    def __init__(self, r, f, s, c):
        self.r, self.f, self.s, self.c = r, f, s, c

    def is_safe(self):
        if self.r != self.s:
            if self.s == self.c or self.f == self.s:
                return False
        return True

    @staticmethod
    def other_side(current_side):
        return 1 if current_side == 0 else 0

    def __eq__(self, other):
        return (self.r, self.f, self.s, self.c) == (other.r, other.f, other.s, other.c)

    def __hash__(self):
        return hash((self.r, self.f, self.s, self.c))


class RiverGameUI(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("农夫过河问题 - AI - 俞晨聪 - 2022333541026")
        self.setGeometry(100, 100, 900, 600)

        # 初始化状态
        self.state = State(0, 0, 0, 0)
        self.goal_state = State(1, 1, 1, 1)
        self.start_time = None

        # 创建主窗口和布局
        self.central_widget = QWidget(self)
        self.setCentralWidget(self.central_widget)
        self.layout = QVBoxLayout(self.central_widget)

        # 创建场景
        self.scene = QGraphicsScene()
        self.view = QGraphicsView(self.scene, self)
        self.layout.addWidget(self.view)

        # 创建状态显示标签
        self.status_label = QLabel("请选择农夫要携带的物品并过河", self)
        self.status_label.setAlignment(Qt.AlignCenter)
        self.layout.addWidget(self.status_label)

        # 创建控制按钮
        self.buttons = {
            "alone": QPushButton("农夫单独过河", self),
            "fox": QPushButton("带狐狸过河", self),
            "sheep": QPushButton("带小羊过河", self),
            "cabbage": QPushButton("带菜篮过河", self),
        }
        for button in self.buttons.values():
            self.layout.addWidget(button)

        # 连接按钮事件
        self.buttons["alone"].clicked.connect(lambda: self.move("alone"))
        self.buttons["fox"].clicked.connect(lambda: self.move("fox"))
        self.buttons["sheep"].clicked.connect(lambda: self.move("sheep"))
        self.buttons["cabbage"].clicked.connect(lambda: self.move("cabbage"))

        # 初始化场景
        self.init_scene()
        self.start_game()

    def init_scene(self):
        # 左岸
        left_bank = QGraphicsRectItem(50, 300, 150, 70)
        left_bank.setBrush(QBrush(Qt.green))
        self.scene.addItem(left_bank)

        # 右岸
        right_bank = QGraphicsRectItem(700, 300, 150, 70)
        right_bank.setBrush(QBrush(Qt.green))
        self.scene.addItem(right_bank)

        # 河流
        river = QGraphicsRectItem(200, 300, 500, 70)
        river.setBrush(QBrush(Qt.blue))
        self.scene.addItem(river)

        # 农夫、狐狸、羊、菜篮
        self.positions = {0: 90, 1: 750}

        # 农夫
        self.farmer = QGraphicsEllipseItem(0, 0, 50, 50)
        self.farmer.setBrush(QBrush(Qt.yellow))
        self.scene.addItem(self.farmer)
        self.farmer_label = self.create_label("农夫", Qt.yellow)

        # 狐狸
        self.fox = QGraphicsEllipseItem(0, 0, 50, 50)
        self.fox.setBrush(QBrush(Qt.red))
        self.scene.addItem(self.fox)
        self.fox_label = self.create_label("狐狸", Qt.red)

        # 羊
        self.sheep = QGraphicsEllipseItem(0, 0, 50, 50)
        self.sheep.setBrush(QBrush(Qt.white))
        self.scene.addItem(self.sheep)
        self.sheep_label = self.create_label("小羊", Qt.white)

        # 菜篮
        self.cabbage = QGraphicsEllipseItem(0, 0, 50, 50)
        self.cabbage.setBrush(QBrush(Qt.green))
        self.scene.addItem(self.cabbage)
        self.cabbage_label = self.create_label("菜篮", Qt.green)

        # 初始化位置
        self.update_scene()

    def create_label(self, text, color):
        text_item = self.scene.addText(text)
        text_item.setDefaultTextColor(color)
        return text_item

    def update_item_position(self, item, label, position_key, y_offset):
        """更新单个物体的位置和标签"""
        item.setPos(self.positions[position_key], y_offset)
        # 更新标签的位置，使其居中对齐
        label.setPos(
            item.x() + item.boundingRect().width() / 2 - label.boundingRect().width() / 2,
            item.y() + item.boundingRect().height()/ 2 - label.boundingRect().height() / 2,
        )
        # 设置标签默认颜色
        label.setDefaultTextColor(Qt.black)

    def update_scene(self):
        """根据状态更新场景"""
        # 农夫的位置
        self.update_item_position(self.farmer, self.farmer_label, self.state.r, 260)
        # 狐狸的位置
        self.update_item_position(self.fox, self.fox_label, self.state.f, 200)
        # 小羊的位置
        self.update_item_position(self.sheep, self.sheep_label, self.state.s, 140)
        # 菜篮的位置
        self.update_item_position(self.cabbage, self.cabbage_label, self.state.c, 80)


    def move(self, choice):
        next_state = self.calculate_next_state(choice)
        if next_state and next_state.is_safe():
            self.state = next_state
            self.update_scene()
            self.check_game_status()
        else:
            QMessageBox.warning(self, "非法操作", "这个选择会导致危险！请重新选择。")

    def calculate_next_state(self, choice):
        f_next = self.state.f
        s_next = self.state.s
        c_next = self.state.c
        r_next = self.state.r
        if choice == 'alone':
            r_next = State.other_side(self.state.r)
        elif choice == 'fox' and self.state.r == self.state.f:
            r_next = State.other_side(self.state.r)
            f_next = State.other_side(self.state.f)
        elif choice == 'sheep' and self.state.r == self.state.s:
            r_next = State.other_side(self.state.r)
            s_next = State.other_side(self.state.s)
        elif choice == 'cabbage' and self.state.r == self.state.c:
            r_next = State.other_side(self.state.r)
            c_next = State.other_side(self.state.c)

        return State(r_next, f_next, s_next, c_next)

    def check_game_status(self):
        if self.state == self.goal_state:
            elapsed_time = time.time() - self.start_time
            QMessageBox.information(self, "游戏成功", f"恭喜你完成了游戏！\n通关时间：{elapsed_time:.2f}秒")
            self.close()

    def start_game(self):
        self.start_time = time.time()
        self.status_label.setText("游戏开始，选择农夫要携带的物品并过河")


if __name__ == "__main__":
    app = QApplication(sys.argv)
    game = RiverGameUI()
    game.show()
    sys.exit(app.exec_())

```