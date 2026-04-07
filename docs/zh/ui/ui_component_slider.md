# FairyGUI的滑动条与转换逻辑

## 滑动条

滑动条常用于在某个区间内控制一个变量。

FairyGUI中的滑动条是带一个“把手”的进度条，其中的“把手”是一个独立的按钮组件。

Ren'Py中的滑动条只是具有*thumb*样式特性的bar。其中的滑块并非独立组件，只渲染图像而没有单独的系统事件(event)处理机制。

目前UI资源转换器只处理FairyGUI滑动条引用的图片和图形，生成的Ren'Py样式，效果与FairyGUI略有差异。具体可转换的内容详见本章后续内容。

## 创建滑动条

在FairyGUI编辑器中通过功能菜单“资源->新建滑动条”或快捷按钮可以创建滚动条，弹出“创建滑动条”提示窗口：
![创建滚动条](screenshots\fguieditor\create_slider.png)

其中的“标题类型”不会被UI转换器处理。我们建议需要显示滑动条关联数值的组件中使用独立的标签组件或文本控件，在FairyGUI中设计文本样式，转换为Ren'Py代码后手动将固定文本改为变量相关的表达式。

创建完成后，滑动条组件包含3个固定元素：
1. n0：滑动条背景，一个图片或图形。
2. bar或v_bar：滑动条前景，一个图片或图形。表示滑动条对应变量生效的值。
3. grip：滑块，一个FairyGUI按钮。UI资源转换器会查找该按钮引用的图片，并用作转换后bar样式特性thumb的值。

!!! note "FairyGUI滑动条的背景没有鼠标指针悬垂状态"

    滑动条内的n0是固定背景。

### 前景图片的差异

FairyGUI对滑动条前景的处理方式为缩放。以水平滑动条为例，滑块移动到滑动条中间时，前景图在水平方向上缩小为原长度的一半。
![FairyGUI中的滑动条前景缩放](screenshots\fguieditor\fairygui_slider_foreground_screenshot.png)

Ren'Py对滑动条前景的默认处理方式为剪裁。以水平滑动条为例，滑块移动到滑动条中间时。前景图只截取显示左边一半。
![Ren'Py中的滑动条前景缩放](screenshots\fguieditor\renpy_slider_foreground_screenshot.png)

为了尽量使FairyGUI编辑器预览效果与转换后的Ren'Py运行结果一致，UI资源转换器会根据滑动条的前景和背景图片生成Ren'Py中的Frame对象，并将bar的*bar_resizing*样式特性值改为True。

实际缩放和剪裁两种方式在不同游戏项目中都可能用到。若需要滑动条前景使用剪裁，请在生成的bar样式中手动将*bar_resizing*的值改为False。

### 滑动条属性

FairyGUI的滑动条属性只有一项，与标题相关。UI资源转换器不处理，可以忽略。
