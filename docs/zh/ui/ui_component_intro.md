# FairyGUI的组件与转换逻辑

## 组件

组件FairyGUI中的基础容器。UI资源转换器一般会把组件转换为Ren'Py中的界面(screen)。
组件有一些基础属性，可以设置组件大小和可见区域。
![组件基础属性](screenshots\fguieditor\component_attributes.png)

### 尺寸

组件的宽度与高度。Ren'Py中不能直接指定界面(screen)的尺寸，而是通过界面默认的最顶层fixed指定尺寸。Ren'Py中界面的默认最顶层fixed尺寸初始值等于项目分辨率。

FairyGUI编辑器中最大尺寸与最小尺寸只有在不等于0的情况下才会生效。如果最大尺寸与最小尺寸的高和宽均为0，转换后的Ren'Py界面最顶层fixed将使用size特性设置尺寸。如果最大尺寸与最小尺寸的宽和高任意一项不为0，转换后的Ren'Py界面最顶层fixed将使用maximum和minimum特性设置尺寸。

我们建议，在FairyGUI中，不要将当前组件的实际尺寸设置得比最小尺寸更小或比更大尺寸更大。虽然在FairyGUI编辑器中不影响预览，但转换为Ren'Py代码后可能会产生无法预料的结果。例如，FairyGUI中

### 轴心和锚点

在FairyGUI编辑器组件的轴心与锚点表示被引用时的默认值，修改这两项属性不会改变当前组件的预览效果，组件内的控件和元素坐标也不会随着锚点变化。仅在其他组件内引用此组件作为元件时，会自动用作元件的基础属性中轴心与锚点。详见下面元件部分。

UI资源转换器遇到其他FairyGUI组件内引用该组件的情况，转换结果中会出现一个fixed组件并应用合适的transform设置坐标和旋转等，再使用use语句引用对应组件转换后的screen。
例如，在FairyGUI中建立了一个*main_menu_button_new*按钮，轴心设置为“中心”即(0.5,0.5)，并勾选了**同时作为锚点**。在*main_menu*组件中引用了*main_menu_button_new*按钮，放在位置(1080,218)并设置旋转角度为-15度。转换后的*screen main_menu*中可以看到类似如下的代码：

```
screen main_menu():
    tag menu

        fixed:
            xysize (840, 84)
            pos (1080, 218)
            at transform:
                transform_anchor True
                anchor (0.5,0.5)
                rotate -15
            use main_menu_button_new(title='', actions=Start(), icon=Null())
```

### 溢出处理

该项决定组件内部元素超出组件尺寸时的显示效果。UI资源转换器会根据该项决定是否添加一个viewport可视组件控制显示范围以及是否可以滚动。

!!! note "单向滚动"

    FairyGUI中的组件可以选择只允许在水平或垂直方向滚动，但Ren'Py中的viewport无法设置为单向滚动。因此将组件的溢出处理设置为“垂直滚动”、“水平滚动”、“自由滚动”后，转换器生成的Ren'Py项目中可以在两个方向上自由滚动。
    我们建议需要单向滚动的情况下，在FairyGUI设计层面进行限制：不需要滚动的方向上，让所有元素都限制在组件显示范围内。

!!! note "左侧和顶部的溢出处理"

    FairyGUI的组件如果内部元素在左侧和顶部溢出，即使溢出处理方式设置为“水平滚动”、“垂直滚动”或“自由滚动”，也无法通过滚动让溢出的部分全部进入显示范围。但是内部元素在组件右侧和底部溢出时，可以通过滚动让溢出部分全部进入显示范围。UI资源转换器生成的Ren'Py界面效果与FairyGUI保持一致，viewport内用于包含所有子组件的fixed尺寸仅计算右侧和底部溢出的部分。

该项设置为“水平滚动”、“垂直滚动”或“自由滚动”时，FairyGUI编辑器在该项右侧会出现一个齿轮图标按钮，点击后可对组件的滚动容器进行设置。
滚动容器的内容详见[滚动条与滚动容器](./ui_component_scrollbar.md#可滚动容器)部分。

### 边缘

目前UI资源转换器只处理按钮的*边缘留空*属性，转换后的Ren'Py代码中，button可视组件的padding特性对应FairyGUI中的*边缘留空*属性。

FairyGUI中的*边缘虚化*效果,在Ren'Py中使用着色器实现。效果与FairyGUI编辑器的预览效果略有差异，虚化效果更明显，建议将该设置设置的略微小一些，比如50。

### 自定义遮罩

FairyGUI中的遮罩(和挖洞)使用模板测试(Stencil Op)技术，Ren'Py并不支持。资源转换器暂不处理FairyGUI中设置的自定义遮罩。后续可能会通过shader实现类似效果。

### 扩展

将FairyGUI的组件**扩展**为其他类型的组件，包括按钮、标签、进度条、滚动条、滑动条和下拉框。目前资源转换器支持的类型有按钮、滚动条和滑动条。

### 背景颜色

仅限用于FairyGUI编辑器内，影响预览效果，发布资源时将忽略该项。

## 组件内的元素

组件中可以引用其他组件，包括各种扩展类型的组件，也可以添加元件。关于元件的介绍详见[FairyGUI元件](./ui_component_object.md)

其他扩展类型的组件，详见下列：

[按钮](./ui_component_button.md)
[进度条](./ui_component_progressbar.md)
[滚动条](./ui_component_scrollbar.md)
[滑动条](./ui_component_slider.md)
[下拉框](./ui_component_combobox.md)
[标签](./ui_component_label.md)

