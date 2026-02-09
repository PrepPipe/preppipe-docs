# UI解决方案

## UI的需求

我们在考虑UI的解决方案时认为，要同时满足“可视化编辑”和“跨引擎”两个需求。语涵编译器本身并不具备UI设计功能，从头开发一个UI编辑器的成本也过于高昂。因此，我们选择了FairyGUI作为UI的设计与编辑工具。

当前的进度为，用户可以直接使用语涵编译器内置的UI预制件(Preset)生成Ren'Py项目的UI，也可以下载UI预制件的FairyGUI工程文件并根据自身需要进行修改，甚至可以完全使用FariyGUI编辑器创建整套UI。

## FairyGUI简介

FairyGUI是一套专业的UI解决方案，具体介绍详见 [FairyGUI官网](https://www.fairygui.com/)。

FairyGUI包括编辑器和运行库两部分。我们只使用编辑器部分，有免费版本，可以满足大多数的UI设计需求。
FairyGUI的运行库支持多种游戏引擎，但**不包括Ren'Py和WebGal**。

学习FairyGUI需要一点点时间成本。本文档的后续篇幅会以内置的预制件为例，将学习成本降低。

## UI资源的发布与转换

FairyGUI发布的资源可以在Unity等游戏引擎上直接使用。如果用户想要在Ren'Py引擎上使用FairyGUI的资源，需要使用语涵编译器的“UI资源转换”功能，将其转为Ren'Py的界面语言(Screen Language)脚本，并发布到对应的Ren'Py项目目录中。

由于Ren'Py的限制，游戏运行中的UI可能与FairyGUI设计的效果有一些差异。
