# 组件内的元素

## FairyGUI编辑器舞台

舞台是FairyGUI编辑器中组件的编辑区域。
编辑组件的基本操作详见 [舞台](https://www.fairygui.com/docs/editor/index#舞台)。
此文档需要用户已学会FairyGUI编辑器的基础操作。

## 元件

FairyGUI组件内的元素称作元件。

元件类型有很多，包括图片、图形、动画、装载器、文本、富文本、组、组件、标签、按钮、下拉框、滚动条、滑动条、进度条、列表。

其中一些只能通过舞台左侧的工具栏向组件内添加，称为**控件**。
![侧工具栏里的控件](screenshots\fguieditor\component_tool_menu.png)

可以添加的控件类型，从上往下依次为：文本、富文本、输入文本、图形、列表、装载器和3D装载器。
目前语涵编译器的“UI资源转换”功能只处理文本、输入文本、图形和列表，其他类型的控件不会出现在转换后的Ren'Py界面代码中。

图片可以从FairyGUI编辑器的**资源库**窗口拖入编辑区域添加到舞台。
组件、标签、按钮、下拉框、滑动条、进度条需要新建对应资源，之后可以从FairyGUI编辑器的**资源库**窗口拖入编辑区域添加到舞台。
![模板工程中的资源库](screenshots\fguieditor\assets_lib.png)

## FairyGUI元件的基本属性

选中舞台中的元素后，FairyGUI编辑器中的**检查器**窗口中可以查看对应元件的各种属性。
FairyGUI元件具有以下基本属性：id、名称、引用源、位置、尺寸、缩放、倾斜、轴心、锚点、不透明度、旋转、是否可见、是否变灰、是否可触摸。
![基本属性](screenshots\fguieditor\basic_attributes.png)

基本属性是任意元件都拥有的属性。但在转换为Ren'Py脚本语言时不一定都生效。
目前，倾斜、是否变灰、是否可触摸，这三项的设置不会对最终结果有影响。

### id

源id，FairyGUI内部属性，用于各种引用关系。在FairyGUI编辑器中无法自由修改。UI资源转换器不处理该属性。

### 名称

元件名，FairyGUI编辑器仅要求同一舞台内不可出现重名元件。UI资源转换器不处理该属性。

### 位置

元件坐标。对应Ren'Py位置样式特性*pos*。
FairyGUI与Ren'Py相同，使用屏幕左上角作为坐标系原点。(Unity使用屏幕左下角作为坐标系原点)

### 尺寸

对应Ren'Py位置样式特性*xysize*。

### 缩放

分别对应Ren'Py变换特性*xzoom*和*yzoom*。Ren'Py中的*zoom*是个浮点型变量而不是元组。

### 倾斜

转换器暂时忽略此属性，不生成对应Ren'Py代码。

### 轴心和锚点

FairyGUI中所有元件的默认锚点和轴心都是(0,0)。可以单独设置轴心，但无法单独设置锚点，只能修改轴心位置后勾选**同时作为锚点**实现锚点的修改。注意，修改锚点后，整个元件的*位置*也会发生改变。
在使用**倾斜**和**旋转**时会用到轴心，此时勾选“同时作为锚点”，便于根据旋转中心设置元件的位置。

Ren'Py中的可视组件的默认锚点不固定，而且会受到*show*和*add*语句影响。与FairyGUI相反，Ren'Py可以单独设置锚点，但无法单独设置旋转轴心，只能通过*transform_anchor*设置为True将轴心与锚点改为同一个值。

### 不透明度

对应Ren'Py变换特性alpha。

### 旋转

对应Ren'Py变换特性rotate。

## FairyGUI元件的属性控制

FairyGUI元件具有属性控制，可以通过控制器改变整个组件的显示效果。
![属性控制](screenshots\fguieditor\attribute_control.png)

属性控制总共有9类，分别为：显示控制、位置控制、大小控制、颜色控制、外观控制、文本控制、图标控制、动画控制、字体大小控制。
当前版本的转换器只支持**显示控制**，即通过控制器切换元件是否显示。

若有需要，可以考虑使用“控制器+显示控制+多个类似组件”的方式实现其他几种属性控制的效果。
例如，某个名为`component_a`的组件中包含名为`controller_a`的控制器和名为`str_a`的文本控件，需要通过控制器索引修改`str_a`显示的文本内容。
可以复制`str_a`并重命名为`str_b`，并使用显示控制将各控制器索引与两个文本控件分别关联。控制器索引号为0时只显示`str_a`，控制器索引号为1时只显示`str_b`。

## FairyGUI元件的关联系统

FairyGUI元件具有关联设置。
![关联设置](screenshots\fguieditor\relations.png)

关联系统是FairyGUI实现自动布局的核心技术。但是，目前转换器还无法处理FariyGUI元件之间的关联关系。

建议使用FairyGUI编辑器时只设计**固定布局**。

## 效果属性

FairyGUI元件可以设置显示效果。
![效果设置](screenshots\fguieditor\effects_attributes.png)

FairyGUI的Blend效果属性可以修改元件的渲染混合方式，滤镜效果属性可以修改元件的亮度、对比度、饱和度和色相。目前转换器还无法处理FariyGUI元件的效果属性。

## 其他属性

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

## 不同元件的独有属性

有些元件具有自己的独有属性，后续篇幅将根据元件类型展开。

## 文本控件

*文本控件*是FairyGUI组件内用于渲染文本的控件。在发布的资源描述文件中是displayList中的text标签，例如：

> <text id="n6_uluf" name="n6" xy="123,1" size="727,179" font="SourceHanSansLite" fontSize="140" color="#ffffff" vAlign="middle" leading="0" autoSize="none" italic="true" shadowColor="#9933cc" shadowOffset="3,3" text="Game Title"/>

除了基本属性，文本控件具有文本属性，包括：字体名、字号、字体颜色、水平对齐方式、垂直对齐方式、字间距、行间距、自动大小类型、是否UBB语法、是否启用模板、是否单行、是否粗体、是否斜体、是否下划线、是否删除线、描边粗细、描边颜色、投影偏移、投影颜色。
![文本属性](screenshots\fguieditor\text_attributes.png)

### UBB语法

[] 按钮决定是否启用UBB语法。Ren'Py不支持UBB语法，建议不启用该功能。

### 文本模板

{} 按钮决定是否启用文本模板。Ren'Py不支持文本，建议不启用该功能。

!!! note "文本标签与内插数值"

    Ren'Py中存在类似`文本模板`的功能，名为**内插数值**。详见 https://doc.renpy.cn/zh-CN/text.html#interpolating-data 。
    虽然官方文档以对话作为样例，但界面中的文本组件也支持该功能特性。
    需要注意，Ren'Py的内插数值使用方括号[]，与FairyGUI中启用UBB语法的预览可能有冲突，所以建议不启用上述两项功能。

### 单行文本

<u>A</u>_ 按钮决定文本是否单行。

启用后，转换器会将文本内容中的换行删除，生成Ren'Py文本组件的样式特性*layout*设置为**nobreak**。

### 粗体、斜体、下划线、删除线

其他几个基础按钮效果都可使用。分别对应Ren'Py*文本样式特性*中的bold、italic、underline和strikethrough。

!!! note "斜体渲染差异"

    FairyGUI与Ren'Py中的渲染斜体文字的结果有差异，倾斜角度不同。
    在FairyGUI编辑器中通过双击字体文件打开字体渲染设置，如果把*渲染方式*改为SDFAA后，可以修改斜体样式(倾斜角度)，在一定程度上解决编辑器预览与Ren'Py最终渲染效果的差别。但使用SDFAA渲染后，文字的描边粗细与投影偏移改为使用归一化(0到1之间)数值，不再使用像素数表示。而且Ren'Py本身也不支持SDF渲染方式。
    对于有较高自定义效果的非静态文本，暂时无法在Ren'Py中实现。
    对于静态文本，可以在FairyGUI中使用SDFAA渲染并编辑为预期效果后，鼠标右键文本控件并使用**转换为位图**功能，将文本转为图片。主要缺点是，转为图片之后若要修改文本内容会比较麻烦。

### 字体

对应Ren'Py文本样式特性中的*font*。

不修改任何设置的情况下，FairyGUI编辑器中使用操作系统默认字体作为文本预览字体，如Windows为*微软雅黑*。
Ren'Py默认字体为*SourceHanSansLite*。因此在不指定字体的情况下，FairyGUI编辑器预览与Ren'Py实际运行结果有明显差别。

可以通过FairyGUI编辑器左上角菜单的“文件->项目设置->默认值->字体”，指定默认字体。

Ren'Py支持otf、ttf和ttc字体文件，最近还新增了woff和woff2字体的支持。编辑文本时请限定使用以上格式的字体。

暂不支持位图字体，后续可能会添加。

### 字体大小

对应Ren'Py文本样式特性中的*size*。

FairyGUI编辑器中字体大小限制为1到200。若需要用到更大的字号，需要通过添加转换器参数或修改生成的Ren'Py代码。

### 颜色、行距、字距

分别对应Ren'Py文本样式特性中的*color*、*line_spacing*、*kerning*。

### 自动大小

FairyGUI中用于自动变换文本控件大小的设置项，编辑器预览与各引擎运行效果略有差别。例如使用斜体的文本属性将自动大小设置为“宽度和高度”后，可能有部分字符右侧不能完全显示，但在Unity等引擎内运行时是完整的。所以FairyGUI编辑器的文本控件设置自动大小后的效果并不完全可靠。

Ren'Py中永远会将整段文本完整渲染，除非单行过长或行数过多超出界面显示范围，不存在文本某一层被截断的情况。转换器会将FairyGUI文本控件的尺寸设置为Ren'Py文本组件的*size*。当单行文本宽度超过文本组件*xsize*时，会自动换行，无视*ysize*的值，相当于FairyGUI中将文本的自动大小设置为“高度”。

我们建议将该项始终设置为(无)或“高度”，仅作预览参考。

若将该项设为“自动收缩”或“显示省略号”，转换器暂时无法生成与FairyGUI效果一致的Ren'Py代码。

### 对齐

FairyGUI编辑器中的对齐有两项：水平对齐和垂直对齐。
水平对齐对应Ren'Py的*textalign*。
垂直对齐在Ren'Py中没有对应的文本样式特性。FairyGUI编辑器预览与转换后的Ren'Py显示效果会有差异。

### 描边和投影

转换器会将FairyGUI的文本描边和投影都处理为Ren'Py的文本特性*outlines*。
转换后，Ren'Py中的文本组件可能会有至多两层描边，分别对应FairyGUI文本属性描边和投影。
由于FairyGUI中的投影包括字符描边，而Ren'Py中*size*固定为0的outlines用于投影，但只包括文字本体，会使投影比带描边的文字要细一些。
因此，同时包含描边和投影的文本，转换后实际Ren'Py代码会是一个三元列表，分别是文字本体投影、描边投影和文字本体描边。

例如，FairyGUI中某个文本描边粗细为1，颜色为纯黑色(#FFFFFF)，投影偏移为(3,3)，颜色为紫色(#9933CC)。转换后的Ren'Py文本outlines可能是：
> outlines [(absolute(0), "#9933cc", absolute(3), absolute(3)), (absolute(1), "#9933cc", absolute(3), absolute(3)), (absolute(1), "#000000", absolute(0), absolute(0))]

### 生成Ren'Py文本样式

转换器对不同类型组件中的文本控件使用不同的处理方式。

对于下面几种特殊名称的文本控件，转换器将生成文本样式：
1. FairyGUI按钮和滑动条中的 *title* 控件(即文本标题)；
2. 名为**choice**组件中的 *caption* 控件(选项界面标题)；
3. 名为**history_item**组件中的 *who* 和 *what* 控件(history界面列表元素中的发言者与发言内容)；
4. 名为**say**组件中的 *who* 和 *what* 控件(say界面的发言者与发言内容)

!!! note "say界面的样式覆盖"

    Ren'Py默认项目模板的say_label样式会影响say界面中的who。转换器会根据say组件中 *who* 控件的设置覆盖say_label。

其他组件中添加的文本控件不会生成文本样式，而是直接在界面定义代码中使用样式特性(style property)赋值。

## 图片

*图片*是FairyGUI中直接引用图片文件资源的组件。在发布的资源描述文件中有三块内容用于存储图片信息。

1. 资源描述文件 “项目名称.bytes” 中的*package.xml*，包含图片id、图片文件名、路径和尺寸等信息。
> <image id="uluf1" name="universal_background" path="/Images/background/" size="1920,1080"/>
2. 资源描述文件 “项目名称.bytes” 中的某个组件的displayList中。引用时使用图片id，即src属性。此处的图片才会有位置属性。
> <image id="n0_uluf" name="bg" src="uluf1" xy="0,0"/>
3. 资源描述文件 “项目名称@sprites.bytes” 中包含图片id与发布图集的对应关系。每个图片拥有7或11个字段，分别为：image id、图集编号、x、y、width、height、rotate，可能加上offset_x、offset_y、source_width、source_height。
> uluf1 101 0 74 1920 1080 0 0 0 1920 1080

除了基本属性，图片具有图片属性和实例属性。

图片属性用于图片文件的信息和可设置项，包括图像大小、数据大小、缩放模式、是否平滑、发布时纹理集选择等。
双击资源库或舞台上的图片，可以查看图片的图片属性。

实例属性用于图片在舞台(组件)的显示效果，包括：颜色、亮度、翻转和填充。
在舞台上选中一个图，可以在检查器窗口查看图片的实例属性。

### 图像大小

仅限SVG文件可以修改。此处修改后，转换后的Ren'Py代码未定义。

### 数据大小

参考信息。

### 缩放模式

缩放模式属性存储在资源描述文件 “项目名称.bytes” 中的*package.xml*里。

*九宫格*对应Ren'Py中的Frame类，*平铺*对应Ren'Py中的Tile类。

### 平滑、质量、纹理集

这3项影响发布后的图集文件。

### 禁止裁剪边缘空白

建议在发布设置的全局设置中就取消“裁剪图片边缘空白”。
如果发现转换后Ren'Py内部分图片显示有误，可以尝试将有问题的图片勾选上该项并重新发布和转换。

### 颜色

图片变色，将图片颜色乘上一个指定颜色。指定颜色会将RGB3个通道的值分别归一化后再进行变色，对应Ren'Py中的TintMatrix类。

### 亮度

FairyGUI中图片的亮度完全等效于把颜色属性改为黑白灰。转换器不处理此亮度。

### 翻转、填充

转换器暂不处理这两项，也不会生成对应的Ren'Py代码。
