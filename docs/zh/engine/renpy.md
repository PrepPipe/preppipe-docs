# Ren'Py 引擎

链接：

  * [中文网站首页](https://www.renpy.cn/)
  * [中文文档](https://doc.renpy.cn/zh-CN/)
  * [英文（原版）网站首页](https://renpy.org/)
  * [英文（原版）文档](https://renpy.org/doc/html/)

现阶段， Ren'Py 引擎是语涵编译器支持能力最高的引擎。（文档还没写完，敬请期待。。）

## 文件导出规则

除非功能上平替或超越，语涵编译器不会覆盖已有的工程文件。从默认新建工程起，语涵编译器只会覆盖 `script.rpy` 使其跳转至入口。每个剧本文件都会导出为一个独立的 `.rpy` 文件。

