# 组件内的元素

## FairyGUI组件内的元素

FairyGUI编辑器中编辑与设计组件时，可以使用左侧的工具栏向组件内添加元素。
![组件菜单](screenshots\fguieditor\component_tool_menu.png)

可以添加的元素类型，从上往下依次为：文本、富文本、输入文本、图形、列表、装载器和3D装载器。
目前语涵编译器的“UI资源转换”功能只处理文本、输入文本、图形和列表，其他类型的元素不会出现了转换后的RenPy界面代码中。

### FairyGUI组件元素的基本属性

FairyGUI组件元素有以下基本属性：id、名称、引用源、位置、尺寸、缩放、倾斜、轴心、锚点、不透明度、旋转、是否可见、是否变灰、是否可触摸。
![基本属性](screenshots\fguieditor\basic_attributes.png)

基本属性是所有类型组件元素都拥有的属性。但在转换为RenPy脚本语言时不一定都有效。

## 文本

*文本*是FairyGUI组件内的一种元素。在发布的资源描述文件中是displayList中的text标签，例如：

> <text id="n6_uluf" name="n6" xy="123,1" size="727,179" font="SourceHanSansLite" fontSize="140" color="#ffffff" vAlign="middle" leading="0" autoSize="none" italic="true" shadowColor="#9933cc" shadowOffset="3,3" text="Game Title"/>

除了基本属性，text的标签属性还有：字体名、字号、字体颜色、水平对齐方式、垂直对齐方式、字间距、行间距、自动大小类型、是否UBB语法、是否启用模板、是否单行、是否粗体、是否斜体、是否下划线、是否删除线、描边粗细、描边颜色、投影偏移、投影颜色。
![文本属性](screenshots\fguieditor\text_attributes.png)


