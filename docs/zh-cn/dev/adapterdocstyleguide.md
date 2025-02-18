---
title: 文档风格指南
lastChanged: 06.05.2021
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/zh-cn/dev/adapterdocstyleguide.md
translatedFrom: de
translatedWarning: 如果您想编辑此文档，请删除“translatedFrom”字段，否则此文档将再次自动翻译
hash: gVPviuMsPHyCd+k12PaNgL3hB9dKVQ9VYcYm4GfPQkg=
---
# 创建适配器文档的风格指南
* 文档是使用“Markdown”语言创建的。
* 适配器文档的文件存储规定如下：
  * 每个适配器项目都有一个文件夹

    `/doc`。

  * 如果文档是德语，它将在子文件夹中

`de` 已保存。当前支持的语言和文件夹名称是：`en, de, ru, pt, nl, fr, it, es, pl`。

  * 实际的适配器文档在文件 `README.md` 中，

    它直接位于相应的语言文件夹中。

  * 媒体存储在子文件夹 `media` 中，该子文件夹也位于

    语言文件夹位于。

  * 除 README.md 外，文件和文件夹名称均以小写字母书写。

允许使用字符 `a-z`、`0-9`、下划线 `_` 和小数点 `.`。

* 文件应有 80 个字符的换行符。
* 最好像在文件`.editorconfig` 中那样完成文本格式化

  描述。

  * 自动应用这些规则的 [plugin] [] 是为了

    不同的编辑器可用。

* 对于德语文本，需要遵守新的德语拼写

  首选。

* 在参考文档中，人称代词的使用（例如

  应避免使用“我”、“你”、“我们”）。

  * 使用中性代词和多个名词。
    * OK: "they (several)", "their (property)", "persons",

      “人”、“开发者”

    * 不好：“他的”、“她的”、“他”、“她（女人）”、“男孩”、“女孩”
* 如果使用括号元素（所有括号形式和

  引号），标点符号设置如下：

  * 如果括号元素是完整的，则在括号内

    句子包含（主语、谓语、宾语）。

  * 如果括号元素只是一个子集，则在括号之外

    包含。

* 文档总是以 H1 级的标题开头。
* 链接不是内嵌的（例如使用`[a link] (http://example.com)`），

但借助文档末尾的内联 `[a link][]` 和 `[a link]: https://a.link/to/know`。

* 使用破折号时，使用短符号

  在 OSX 中使用减号而不是“-”或 `Option+Shift+"-"`。

* 附加内容：
  * 二进制文件、图像、视频或录音等文件将被

    存储在文件夹 `media` 中。

  * 媒体包含在一般文件的文本中

通过 `§§LLLLL_0§§` 和图像通过 `![媒体术语](../../de/dev/media/{dateiname})`。

  * 图像最好以 SVG 格式存储。当 SVG

不可能，然后作为 PNG 文件。请注意文件大小。

  * 短视频可以嵌入为 GIF 文件。
  * 每张图片下方都有斜体字对内容的简短说明

    来指定。

* 以下适用于源代码部分：
  * 根据源代码语言，必须选择相应的标记。到

    JavaScript 的示例 `\` \ `\``。

  * 源文本可以但不必是完整的。源代码块

举例说明刚才描述的观点。因此不需要提供完全可执行的程序。但是，如果要提供完全可执行的程序，则可以将其作为文件夹 `media/{code_beispieldatei}` 中的媒体文件并在文档中提供相应链接。

* 如果使用下划线、引号、星号或反斜杠

正确的转义字符必须使用：`\_`，`\*`，`\\`和``\``` anstelle von `_`, `*§§SSSSS_6§ § \ ` und `` ` ``。

* 为了使笔记脱颖而出，以下是指导方针

  要注意：

 *"Note:" 标识符必须设置为斜体，即`* Note* `。
  * 在“注意：”标识符之后，继续使用大写字母。
  * 注释必须放在新段落的开头，以便

    更明显。

* 适配器文档有一个 [模板] []。有关的

  模板部分将以存储的顺序和形式使用。

[Plugin]: http://editorconfig.org/#download

[Vorlage]: dev/adaptertemplate