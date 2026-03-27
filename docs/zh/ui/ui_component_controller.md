# Fairy组件中的控制器

FairyGUI中的控制器是组件状态机的一种实现。可以通过切换状态使组件显示不同内容。

语涵编译器的UI资源转换器可以将部分控制器的功能转换为具有相同效果的Ren'Py代码。具体的转换方案详见下文。

## 控制器面板

组件编辑模式下的，左上角可以看到控制器面板，包括已有控制器和“增加控制器”按钮。
[控制器面板](screenshots\fguieditor\component_controller_panel.png)

点击“增加控制器”按钮，会弹出如下窗口，可创建新的控制器：
[增加控制器](screenshots\fguieditor\component_add_controller_window.png)

点击某个控制器名称，会弹出如下窗口，可修改现有控制器：
[修改控制器](screenshots\fguieditor\component_modify_controller_window.png)

点击某个控制器名称后面的序列号按钮，可以切换控制器当前状态。如果界面内的元件设置了“属性控制”，也会切换到对应索引号的状态。

## 组件控制器转换逻辑

UI资源转换器只关注控制器名称和首页。FairyGUI组件转换后的Ren'Py界面代码开头会有控制器同名变量，并根据首页设置初始值。
例如，preferences组件具有控制器*tab_controller*，并设置首页为“指定页面-1:text”，那么转换后的Ren'Py界面代码开头可以看到：
```
screen preferences():
    # 由组件控制器生成的界面内控制变量：
    default tab_controller = 1
```

!!! note "控制器首页限制"

    FairGUI编辑器中还可以将控制器首页类型设置为“匹配分支名称”和“匹配变量名称”。UI资源转换器不处理这两种首页类型(因为以非二进制文件发布的资源中缺少这两类信息)，都以编辑器发布资源时的编辑器当前选中索引为初始值。

更改组件控制器状态需要绑定组件内的元件，比如按钮。目前UI资源转换器只支持使用按钮切换控制器状态。

## 按钮的控制器模板

FairyGUI的控制器设置窗口有一个按钮控制器模板按钮：
[按钮控制器模板](screenshots\fguieditor\button_controller_template.png)

点击后可以从4种按钮控制器模板中选择，将当前控制器改名为button并设置对应的索引。

新建按钮默认则固定包含一个名为“button”的控制器，并使用4索引：up/down/over/selectedOver。

UI资源转换器只处理默认4索引和6索引(多了disabled和selectedDisabled)的按钮。同时我们建议不要修改button控制的索引顺序和名称。
