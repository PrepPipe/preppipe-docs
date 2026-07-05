# Ren'Py特殊界面设计说明

下表列出了使用FairyGUI设计UI时可以使用的特殊组件和制作要求。

| 特殊组件名 | 模态(modal)界面 | 界面tag | 界面zorder | 必须子组件名称 | 必须子组件类型 | 必须子组件说明 | 可修改(自定义)子组件说明 | 界面固定入参 | 其他子组件处理 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| choice | 否 | menu | 默认值0 | caption<br>choice_list | 文本<br>列表 | | | items | 忽略其他子组件 |
| say | 否 | menu | 默认值0 | namebox<br>textbox<br>who<br>what | 图片<br>图片<br>文本<br>文本 | | | who, what | 忽略其他子组件 |
| save | 否 | menu | 默认值0 | save_slot_list | 列表 | | | | 按顺序生成所有子组件 |
| load | 否 | menu | 默认值0 | save_slot_list | 列表 | | | | 按顺序生成所有子组件 |
| history_item | 否 | | 默认值0 | who<br>what | 文本<br>文本 | | | who, what | 按顺序生成其他组件，最后覆盖who和what |
| history | 否 | menu | 默认值0 | history_list | 列表 | 列表默认资源必须为history_item | | | 按顺序生成所有子组件 |
| confirm | 是 | menu | 固定值200 | message<br>yes_button<br>no_button | 文本<br>按钮<br>按钮 | | | message, yes_action, no_action | 按顺序生成所有子组件 |
| main_menu | 否 | menu | 默认值0 | | | | 文本title、图片logo | | 按顺序生成所有子组件 |
| game_menu | 否 | menu | 默认值0 | | | | | | 按顺序生成所有子组件 |
| gallery | 否 | menu | 默认值0 | gallery_button_list | 列表 | 列表默认资源类型必须为按钮 | | | 按顺序生成所有子组件 |
| music_room | 否 | menu | 默认值0 | musicroom_button_list | 列表 | 列表默认资源类型必须为按钮 | | | 按顺序生成所有子组件 |

设计特殊组件时，请务必根据该表在组件内放置固定名称和类型的元件。否则，UI资源转换器可能报错，或者生成的Ren'Py界面无法正确显示和运行。

设计和制作*confirm*时，尺寸请使用项目分辨率创建组件，在FairyGUI编辑器中设置合适的弹窗位置。如果按照弹窗尺寸创建组件，则转换后的项目运行时，弹窗提示可能会出现在画面左上方。

表格中列出的组件名并不是Ren'Py内置特殊界面名的子集，比如*gallery*和*music_roon*。考虑到图鉴类界面是很常见的需求，所以制作了这两个界面的模板。

*about*和*help*并不是Ren'Py内置特殊界面名。UI资源转换器遇到使用这两个名称的组件时，会在生成的Ren'Py界面中添加**tag menu**。

另外，Ren'Py中有几个内置特殊界面未出现在表格中，比如*nvl*、*notify*和*ctc*等。用户依然可以使用FairyGUI编辑器设计和制作同名组件，并通过UI资源转换器生成对应的Ren'Py代码，但对应的界面通常缺少变换动效和互动功能，需要手动修改Ren'Py脚本的代码。

