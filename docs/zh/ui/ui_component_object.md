# 组件内的元素

## FairyGUI编辑器舞台

舞台是FairyGUI编辑器中组件的编辑区域。
编辑组件的基本操作详见 [舞台](https://www.fairygui.com/docs/editor/index#舞台)。
此文档默认用户已学会FairyGUI编辑器对组件的基础编辑。

## 元件

FairyGUI组件内的元素称作元件。

元件类型有很多，包括图片、图形、动画、装载器、文本、富文本、组、组件、标签、按钮、下拉框、滚动条、滑动条、进度条、列表。

其中一些只能通过舞台左侧的工具栏向组件内添加，称为**控件**。
![侧工具栏里的控件](screenshots\fguieditor\component_tool_menu.png)

可以添加的控件类型，从上往下依次为：文本、富文本、输入文本、图形、列表、装载器和3D装载器。
目前语涵编译器的“UI资源转换”功能只处理文本、输入文本、图形和列表，其他类型的控件不会出现了转换后的Ren'Py界面代码中。

### FairyGUI元件的基本属性

FairyGUI元件具有以下基本属性：id、名称、引用源、位置、尺寸、缩放、倾斜、轴心、锚点、不透明度、旋转、是否可见、是否变灰、是否可触摸。
![基本属性](screenshots\fguieditor\basic_attributes.png)

基本属性是任意元件都拥有的属性。但在转换为Ren'Py脚本语言时不一定都有效。

### FairyGUI元件的属性控制

FairyGUI元件具有属性控制，可以通过控制器改变整个组件的显示效果。
![属性控制](screenshots\fguieditor\attribute_control.png)

属性控制总共有9类，分别为：显示控制、位置控制、大小控制、颜色控制、外观控制、文本控制、图标控制、动画控制、字体大小控制。
当前版本的转换器只支持**显示控制**，即通过控制器切换元件是否显示。

### FairyGUI元件的关联系统

FairyGUI元件具有关联设置。
![关联设置](screenshots\fguieditor\relations.png)

关联系统是FairyGUI实现自动布局的核心技术。但是，目前转换器还无法处理FariyGUI元件之间的关联关系。

建议使用FairyGUI编辑器时只设计固定布局。

### 效果属性

FairyGUI元件可以设置显示效果。
![效果设置](screenshots\fguieditor\effects_attributes.png)

FairyGUI的Blend效果属性可以修改元件的渲染混合方式，滤镜效果属性可以修改元件的亮度、对比度、饱和度和色相。目前转换器还无法处理FariyGUI元件的效果属性。

### 其他属性

FairyGUI元件其他设置项包括tooltips和自定义数据。
![其他设置](screenshots\fguieditor\other_attributes.png)

转换器暂不处理tooltips。(后续会支持)

按钮和滑动条的自定义数据会被转换器处理。

按钮的自定义数据将用作按钮的行为(action)。例如，某按钮的自定义数据设置为 *Start()* ，转换后引用该按钮时会将该值作为actions参数的值传入按钮界面:
"""
use main_menu_button_new(title='', actions=Start(), icon=Null())
"""

滑动条的自定义数据将用作滑动条的条值(barvalue)。例如，某滑动条的自定义数据设置为 *Preference('main volume')* ，转换后引用该滑动块的界面会设置为：
"""
bar value Preference('main volume') style 'horizontal_slider'
"""

此设计可以在UI设计层面就指定常用组件的实际功能，用户不需要转换为界面语言代码后再查找对应的按钮或滑动条并修改具体功能，也避免了修改UI重新发布和转换后覆盖actions或barvalue的问题。

具体的action或barvalue功能请查看Ren'Py文档：
[界面行为、值和函数](https://doc.renpy.cn/zh-CN/screen_actions.html)

### 不同元件的独有属性

有些元件具有自己的独有属性，后续篇幅将根据元件类型展开。

## 文本控件

*文本控件*是FairyGUI组件内用于渲染文本的控件。在发布的资源描述文件中是displayList中的text标签，例如：

> <text id="n6_uluf" name="n6" xy="123,1" size="727,179" font="SourceHanSansLite" fontSize="140" color="#ffffff" vAlign="middle" leading="0" autoSize="none" italic="true" shadowColor="#9933cc" shadowOffset="3,3" text="Game Title"/>

除了基本属性，text的标签属性还有：字体名、字号、字体颜色、水平对齐方式、垂直对齐方式、字间距、行间距、自动大小类型、是否UBB语法、是否启用模板、是否单行、是否粗体、是否斜体、是否下划线、是否删除线、描边粗细、描边颜色、投影偏移、投影颜色。
![文本属性](screenshots\fguieditor\text_attributes.png)

转换器对不同类型组件中的文本控件使用不同的处理方式。

对于下面几种特殊名称的文本控件，转换器将生成文本样式：
1. FairyGUI按钮和滑动条中的 *title* 控件(即文本标题)；
2. choice组件中的 *caption* 控件(选项界面标题)；
3. history_item组件中的 *who* 和 *what* 控件(history界面列表元素中的发言者与发言内容)；
4. say组件中的 *who* 和 *what* 控件(say界面的发言者与发言内容)

!!! note "say界面的样式覆盖"

    Ren'Py默认项目模板的say_label样式会影响say界面中的who。转换器会根据say组件中 *who* 控件的设置覆盖say_label。

其他组件中添加的文本控件不会生成文本样式，而是直接在界面定义代码中使用样式特性(style property)赋值。

