# pdfjs-vueDemo

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```
# 页面
官方demo：http://mozilla.github.io/pdf.js/web/viewer.html<br>
1. 预览本地pdf<br>
 将viewer.js 的 10053 放开，10054注释，输入路径 http://localhost:8080/static/pdf/web/viewer.html
 或者  访问  http://localhost:8080/static/pdf/web/viewer.html?file=/static/pdf/web/demo.pdf
2. 预览服务器的pdf<br>
2.1  let url = 'http://somedomain/doc/manuals/R-intro.pdf'<br>
2.2  let url = 'http://image.cache.timepack.cn/nodejs.pdf'<br>
 这两个url 都是我网上自己找的，虽然都是服务器pdf路径，通过（http://localhost:8080/static/pdf/web/viewer.html?file=http://image.cache.timepack.cn/nodejs.pdf）访问但是上面第一个会报错，第二个可以正常预览是因为第一个的服务器端没有设置Access-Control-Allow-Origin:*，允许跨域，so R-intro.pdf的预览就会报 '意外的服务器相应，Unexpected server response (0) while retrieving PDF "http://somedomain/doc/manuals/R-intro.pdf". 
 猜测会有人报'file origin does not match viewer.js' 我没报的原因是我简单粗暴的将viewer.js的1863行注释了！
但是配置服务器允许跨域不安全也不好，so，这就需要后台来配合了，后台需要返回你一个流的形式的pdf，pdf.js插件是可以识别的，也不会报跨域问题！！！ <br>
2.3  let url = 'https://dluat.hscf.com/api/esm/v1/contractTemplates/load/c08def54aa40412b8b511406fc0271d2/0?access_token=b6cce0c8428c55531d206b4f008fe44e&name=cehsi.pdf'
将上面的url放入浏览器直接 是以流的形式呈现出来，例如下面的乱码形式：<br>

%PDF-1.4<br>
5 0 obj<br>
<<
/Type /Page<br>
/Parent 3 0 R<br>
/Resources 4 0 R<br>
/Contents 6 0 R<br>
/MediaBox[ 0 0 595.3 841.9 ]<br>
/CropBox[ 0 0 595.3 841.9 ]<br>
/Rotate 0<br>
>>
endobj<br>
6 0 obj<br>
<< /Length 273 /Filter /FlateDecode >><br>
.......还有很多这种码<br>
这种带有参数的url必须编码，encodeURIComponent了解一下，当然以流的方式在浏览器打开是进行下载的，pdf.js也是可以进行预览，而不下载。<br>
// 启动项目<br>
npm install or cnpm install<br>
npm run dev<br>
For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
