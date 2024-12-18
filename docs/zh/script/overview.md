# 总览

该部分将介绍与剧本读取有关的一切，主要包括剧本可以按什么格式写、有哪些命令等。

## 文件读取类型

语涵编译器目前接受以下输入剧本格式：

  * docx 文档 (*.docx)，兼容性以 Office Word 为标准。（读取功能由 [`python-docx`](https://pypi.org/project/python-docx/) 实现。）
  * odt 文档 (*.odt)，兼容性以 LibreOffice Writer 为标准。（读取功能由 [`odfpy`](https://pypi.org/project/odfpy/) 实现。）
  * Markdown (*.md)，兼容性以 [GFM](https://github.github.com/gfm/) 为标准。（读取功能由 [`marko`](https://pypi.org/project/marko/) 实现。）
  * 纯文本 (*.txt)，建议使用 UTF-8 编码。

以上格式的剧本可能包含语涵编译器不支持的功能（比如内嵌文本框、内嵌音视频），程序会忽略所有不支持的功能。程序会使用部分文字样式（加粗、前景色等）、段落样式（背景色，居中）和内嵌图片等，不支持的输入格式（比如纯文本）无法直接使用此类功能，不过涉及到的功能都可以用别的方式实现。
