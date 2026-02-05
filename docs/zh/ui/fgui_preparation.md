# FairyGUI编辑器准备工作

## 下载FairyGUI编辑器

请从[FairyGUI编辑器下载链接](https://www.fairygui.com/download#download-sdk)选择适合自己操作系统的编辑器。不需要下载运行库，而且也不存在Ren'Py的运行库。

## 修改设置

### 项目设置

新建或打开已存在的项目后，点击菜单栏“文件->项目设置”：
![项目设置菜单](screenshots\fguieditor\menu_project_setting.png)

在弹出的“项目设置”弹窗中，将项目类型设置为“Unity”，即默认值。语涵编译器的“UI资源转换”功能基于此类型的资源开发。为保证转换后尽可能保证UI效果的一致性，建议不要修改为其他类型。
![项目类型设置](screenshots\fguieditor\project_setting_base.png)

### 发布设置

!!! note "Unity项目跳过此步骤"

    若发布的资源直接用于Unity引擎，则根据自身需要进行发布设置。无须遵循下面的设置。

新建或打开已存在的项目后，点击菜单栏“文件->发布设置”：
![发布设置菜单](screenshots\fguieditor\menu_publish_setting.png)

或点击快捷菜单的“发布设置”按钮：
![发布设置按钮](screenshots\fguieditor\quickmenu_publish_setting.png)

在弹出的“发布设置”弹窗中，“全局设置->包格式”栏，务必**取消勾选**“使用二进制格式”。
![发布格式设置](screenshots\fguieditor\publish_setting_base.png)

“二进制格式”发布的资源包在搭配对应引擎的FairyGUI运行库时可以有很高的效率，但不存在Ren'Py的运行库。语涵编译器的“UI资源转换功能”只识别文本格式的bytes文件。

