# gitbook教程

gitbook的用途

配合使用
GitBook + Typora + Git

### 安装
```
npm install -g gitbook-cli
```

### 使用
```
gitbook init
```
生成文件
```
README.md —— 书籍的介绍写在这个文件里
SUMMARY.md —— 书籍的目录结构在这里配置
```
.md文件用Typora来编辑，可以打开当前文件夹

### demo
编辑SUMMARY.md文件，内容修改为：
```
# 目录

* [前言](README.md)
* [第一章](Chapter1/README.md)
  * [第1节：衣](Chapter1/衣.md)
  * [第2节：食](Chapter1/食.md)
  * [第3节：住](Chapter1/住.md)
* [第二章](Chapter2/README.md)
```

保存后在命令行再次执行
```
gitbook init
```

它会根据SUMMARY.md的索引自动生成目录

![](https://user-gold-cdn.xitu.io/2019/6/6/16b2aaab9f30eca2?w=528&h=403&f=png&s=26319)

### 预览
```
gitbook serve
```
执行命令后会对 Markdown 格式的文档进行转换，默认转换为 html 格式，最后提示 “Serving book on http://localhost:4000”。打开浏览器：

![](https://user-gold-cdn.xitu.io/2019/6/6/16b2ac28ce3aa349?w=613&h=482&f=png&s=61183)
你也可以指定端口
```
gitbook serve --port 9999
```
### 输出
默认快出路径为_book
```
gitbook build
或 gitbook build [书籍路径] [输出路径]
```
如输出到docs文件夹
```
gitbook build . docs
```



### 生成其他格式电子书（如.pdf）

```
pdf格式：gitbook pdf ./ ./mybook.pdf
epub格式：gitbook epub ./ ./mybook.epub
mobi格式：gitbook mobi ./ ./mybook.mobi
```
<p style="color:#f69;font-size:14px">
如果是要导出PDF，ePub或者mobi格式的电子书时，需要安装Calibre电子书阅读/管理器和命令行工具，不然可能会报错“EbookError: Error during ebook generation: 'ebook-convert'”。</p>