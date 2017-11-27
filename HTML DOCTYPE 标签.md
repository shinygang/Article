
##  HTML DOCTYPE 标签

@(HTML学习)

#### Doctype是什么？[点击查看详解](http://baike.baidu.com/link?url=m22fNdtgIp-_H25sPY4D-29MqjQAZ1Ei3WOXvNCs1ag-C-9aQwLLmoQ0XDP4M-MTiMbEOAisya8kyIZjrQCLR_)
* <!DOCTYPE> 声明帮助浏览器正确地显示网页。
* web世界中存在着很多不同的文档，只有了解了文档类型，浏览器才能正确的显示文档。这就是` <!DOCTYPE> `的用处。
* <!DoCTYPE>并不是html标签，它为浏览器提供一项信息（声明），即HTML是什么版本编写的。
* 所有浏览器都支持 `<!DOCTYPE>`声明。
#### 实例
带有 HTML5 DOCTYPE 的 HTML 文档：
```
<!doctype html>
<html>
	<head>
		<title>Title of the document</title>
	</head>
	<body>
	The content of the document......
	</body>
</html>
```
#### HTML 发展版本
从 Web 诞生早期至今，已经发展出多个 HTML 版本：
| 版本     | 年份 |
|:--------|:-------|
|HTML     |1991    |
|HTML+    |1992    |
|HTML2.0  |1995    |
|HTML3.2  |1997    |
|HTML 4.01|1999    |
|XHTML 1.0|2000    |
|HTML5    |2012    |
|XHTML5   |2013    |
#### 定义和用法
> 提示：请始终向 HTML 文档添加`<!DOCTYPE>`声明，这样浏览器才能获知文档类型。

* `<!DOCTYPE>` 声明必须是 HTML 文档的第一行，位于<html>标签之前
* `<!DOCTYPE>` 不是html标签，它是只是web浏览器关于使用哪个HTML版本经行编写的指令
* 在 HTML 4.01 中，<!DOCTYPE> 声明引用 DTD，因为 HTML 4.01 基于 [SGML](http://baike.baidu.com/link?url=lLkTzGmAcVG4ggZoPciTk2M-2AvOklW3wCAuVo_Z7UQ8azh2fCLTKegub_hzqccfYJwCkct7TCPvAb88DLsw9g8ygC32TxY9p-_4sCLDSfhaJd3kL9qc-2NmGvb72sgNHK-XXmukTvWWPIc4KkCEWa)。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。
* HTML5 不基于 SGML，所以不需要引用 DTD。

**HTML 4.01 与 HTML5 之间的差异**
在 HTML 4.01 中有三种 <!DOCTYPE> 声明。在 HTML5 中只有一种：
```
<!DOCTYPE html>
```
[点击查看HTML 元素表](http://www.w3school.com.cn/tags/html_ref_dtd.asp)，其中列出了每种元素会出现在哪个文档类型中。
#### 提示和注释
* 注释：`<!DOCTYPE>` 声明没有结束标签。
* 提示：`<!DOCTYPE>` 声明对大小写不敏感。
* 提示：请使用 [W3C 的验证器](http://validator.w3.org/)来检查您是否编写了有效的 HTML / XHTML 文档！
####常用的 DOCTYPE 声明
**HTML5**
```
<!DOCTYPE html>
```

**HTML 4.01 Strict**
该DTD包含所有html元素和属性，但不包括展示性和启用的元素（如font）,不允许框架Framesets。
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```
**HTML 4.01 Transitional**
该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
"http://www.w3.org/TR/html4/loose.dtd">
```
**HTML 4.01 Frameset**
该 DTD 等同于 HTML 4.01 Transitional，但允许框架集内容。
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" 
"http://www.w3.org/TR/html4/frameset.dtd">
```
**XHTML 1.0 Strict**
该 DTD 包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。必须以格式正确的 XML 来编写标记
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```
**XHTML 1.0 Transitional**
该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。必须以格式正确的 XML 来编写标记。
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "
http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```
**XHTML 1.0 Frameset**
该 DTD 等同于 XHTML 1.0 Transitional，但允许框架集内容。
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```
**XHTML 1.1**
该 DTD 等同于 XHTML 1.0 Strict，但允许添加模型（例如提供对东亚语系的 ruby 支持）。
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
```
