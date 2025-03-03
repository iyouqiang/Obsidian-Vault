---
date: <% tp.date.now("YYYY-MM-DD HH:mm:ss") %>
status: doing
excerpt: 为啥要做？做完后有何收获感想体会？
tags: []
aliases: 
rating: ⭐
---

### 彩色code

通过dataview插件，设置查询条件，查询到数据自动生成表格（csv文件），代码如下
自己把代码换成dataviewjs，并更换`<source>`查询条件，`<field1>`为查询字段即可。
```js
let source = dv.pages("<source>");
const table = source.map(p => [p.<field1>,p.<field2>,p.<field3>]);
let csvContent = "data:text/csv;charset=utf-8," + table.map(e => e.join(",")).join("\n");
var encodedUri = encodeURI(csvContent);
var link = document.createElement("a");
link.setAttribute("href", encodedUri);
link.setAttribute("download","my_data.csv");
document.body.appendChild(link);
link.click();
```


### TODO

- [ ] 多喝水，避免久坐不动
- [x] 阅读一篇文献

## Tracking

- 17:10 在新版obsidian上重新构建一个面向研究生的模板库，力求精简实用。 #TODO


### 警告框

本人将资料库存放于移动固态硬盘中，并将硬盘盘符自定义为`X`，然后将资料库解压存放于`X:\projects`目录下，并把该 vault 重命名为 `working`。您可以按照个人喜好选择存储方案和仓库命名。**后续模板库路径均以`X:\projects\working`为例**。

>[!warning]
title: 更新请注意
对于已经使用该模板库早期版本的用户，一般而言，由于涉及修改的文件主要是插件配置代码等与个人资料无关的内容。您可以直接下载最新的 release 覆盖之前的库进行更新。但是请注意 [[README]] 文档中的说明，如果您自己有自定义的流程或插件配置方面的修改，则不建议更新。


插入图片

这里推荐配合 Snipaste 截屏工具使用（详见后续章节：[[Snipaste - 超好用的截图工具]]），当使用该工具截取屏幕之后，图片被复制到粘贴板，您只需要在草稿中按下` Ctrl+V` 即可完成图片的插入，obsidian 会将粘贴板中的图片拷贝到附件目录（`08-Assets`），并且自动生成指向该附件的链接，如下所示：

![[Pasted image 20220321194108.png]]

注意插入的图片`![[image.png]]`最好独占一行，而且前后均有空行。

#### 图片细节样式控制

本模板库使用的 [Blue Topaz 主题](https://github.com/cumany/Blue-topaz-examples)提供了丰富的对内容样式的调整方法。如果想控制图片的大小，可以是：

`![[img.png|300]]`

此时图片的宽度显示为 300 px。如果想插入 figure caption，建议如下操作：

`![[img.png#center|figure 1. 这是一张图表|500]]`

简单说明一下，图片文件名后面跟的 `#center` 指明了图片至于中间的位置，然后接下来 `|` 后面就是图注内容，再到后面则是指定显示宽度。

### 插入表格

更推荐插入excel的电子表格文件作为附件。


### 插入其它附件

除了可以在草稿中插入图片，您还可以插入视频，音频等多媒体文件。您可以通过快捷键 `Ctrl+E` 进行「全局预览」并播放。当然也可以按住 Ctrl 键，将鼠标悬停于这些附件链接上方实现「局部预览」。

《原神·晨曦酒庄-陈致逸》

![[陈致逸,HOYO-MiX - Dawn Winery Theme 晨曦酒庄.mp3]]

> 仅支持 mp3 音频文件在预览模式下播放

《原神·游戏片段截取》

![[PM.mp4]]

> 仅支持 mp4 格式视频文件在预览模式下播放



>[!tip]
>quickAdd命令全局生效，意味着你不必停留在该日志页面也能够插入track记录。如果你想从别处快速进入到当天后者其他某天的日志，可以使用界面右上角的日历。
>你还可以为一些track添加标签，比如添加了 TODO 标签，则这条track会被👇[[愿望清单]]自动收集。



***


### 代表作
<!-- 可以从 google scholar 或者 web of science 中找，5 篇左右即可 -->
