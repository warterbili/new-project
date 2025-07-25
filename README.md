NEW_FILE_CODE
# ChemTDSGrabber/化工TDS采集器

这是一个tds和pdf文件爬虫项目，主要用于化工企业的tds文件收集。目前还在优化中。。。。===

## 目录结构

- `src/` - 源代码文件夹
  - `services/` - 服务相关代码
  - `utils/` - 工具函数
- `data/` - 数据文件夹
- `test/` - 测试文件
- `package.json` - 项目配置文件
- `README.md` - 项目文档

## 项目介绍
这个是一个puppeteer爬虫项目，用于企业级的tds和pdf文件的爬取。
主要给化工企业网上搜集tds文件。

## 项目各文件介绍
在使用前先需要将你的csv企业网站数据放在data文件夹下，文件名自己随意。在-`datapath.js`中修改数据路径。
其中readpath参数就是你csv企业网站数据的文件路径，savepath参数是你转换完成后的json文件的保存路径。

在爬虫使用前，先要用`fileConversion.js`将csv文件转换成json文件。
- `fileConversion.js` - 文件转换相关代码
这个文件用于将csv文件转成json文件。
其中csv文件包含的是企业的网站数据
转换完成后类似
// ... existing code ...
## 示例数据

以下是一个示例数据的展示：

// ... existing code ...
## 示例数据

以下是一个示例数据的展示：

```json
{
  "供应商名称": "东莞市宏福新材料有限公司",
  "员工工号": "",
  "花名": "",
  "属地": "",
  "部门": "",
  "小组": "",
  "职位名称": "",
  "直属上司": "",
  "部门负责人": "",
  "官网首页网址": "http://www.acr168.com/",
  "产品TDS下载页面入口网址": "http://www.acr168.com/products.html",
  "是否有TDS下载": "否",
  "是否需要注册账号": "不用",
  "是否已经手工下载完成": ""
}
```
2.`utils`文件夹下是所有的参数配置。
- `browserconfig.js` - 浏览器配置相关代码
这个文件用于配置浏览器的可执行路径和其他浏览器相关设置。
- `datapath.js` - 数据路径配置
这个文件用于配置数据文件的路径，包括读取的csv文件路径和保存的json文件路径。
- `config.js` - 爬取配置相关代码
因为我这个爬虫使用的是，广度优先算法。这里配置的是爬取的深度和每个网页最大爬取页面数量。
建议爬取深度不要太深。三层深度以下就可以了。
- `pagewait.js` - 页面等待时间配置
这个文件用于配置页面加载等待时间。主要是配置page.goto()方法等待时间。
- `wordsdata.js` - 关键词数据
这个文件用于配置关键词数据，主要是爬取tds文件的关键词。用于区分网页是否是普通pdf还是tds的pdf文件。
最后输出结果会分类保存。普通pdf和tds的pdf文件会分开保存。

3.`services`文件夹下是爬虫的主要逻辑代码。
- `fileConversion.js` - 文件转换相关代码
这个文件用于将csv文件转换成json文件。
- `isValidUrl.js` - URL验证相关代码
这个文件用于验证URL的有效性，确保爬虫只处理有效的链接。是否为网页同一域名下。防止跑到别的网页。
- `crawler.js` - 爬虫主逻辑
这个文件是爬虫的核心逻辑，负责处理网页的爬取。解析和保存。采用广度优先算法，先入先出的方式。
其中还会记录每次爬取时的a链接文本内容。方便人工后期删选pdf文件。
- `downloadfile.js` - 文件下载相关代码。
这个文件用于下载网页中的PDF文件。使用axios库进行pdf文件下载，并保存到指定目录。是http下载的一种方式。

4.`other.js`是爬虫的主入口文件。
使用时直接在终端，node other.js 即可开始爬虫。
- `index.js` - 是最早的主入口文件。功能还可以用。但是不全面现已废弃。
