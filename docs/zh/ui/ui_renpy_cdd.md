# Ren'Py自定义组件

本篇简单介绍转换后在Ren'Py项目中可能会用到的一些自定义组件(Creator Defined Displayable)。

## 按钮容器 {: #button_container}
**ButtonContainer**类继承Ren'Py内置的Button类，注册的界面语言组件名为**button_container**。

button_container有下列特性：

*pressed_scale*
    表示按下状态的子组件的缩放比例。默认值为1.0。

*pressed_dark*
    表示按下状态的子组件的变暗程度。默认值为0。
    FairyGUI中变暗的取值范围为0～1，0完全黑，1完全无效果。(编辑器中允许输入值超过1，但无效果。)
    Ren'Py中使用BrightnessMatrix类处理，入参取值范围-1～1，-1完全变黑，0完全无效果，1完全变白。

## 序列帧动画 {: #sequence_animator}

## 自定义视口 {: #elastic_viewport}

**ElasticViewport**类继承Ren'Py内置的Viewport类，注册的界面语言组件名为**elastic_viewport**。

elastic_viewport支持除*edgescroll*之外的所有原生viewport组件特性，并新增下列特性：

*draggable*
    为True时响应鼠标拖拽，为False时忽略鼠标拖拽。

*scrollable*
    控制允许滚动的方向。
    'vertical'，只允许垂直方向滚动。
    'horizontal'，只允许水平方向滚动。
    'both'，允许任意方向滚动。

*bounds_back*
    为True时启用边缘回弹，为False时禁用边缘回弹。



