### 前端

1. Vue执行打包时报错
 > ERROR in static/js/0.js from UglifyJs jsts-es Unexpected token name «key», expected punc «;» [./~/jsts-es/src/

 项目中引用了turfjs,而这个文件依赖jsts-es。UglifyJs执行代码混淆时是对es5操作的，而jsts-es代码应该先要转码再进行压缩混淆。所以转码时把它包含进去就好了：
 ```
  {
    test: /\.js$/,
    loader: 'babel-loader',
    include: [resolve('src'), resolve('test'), resolve('node_modules/jsts-es/src')]
  },
```

2. Openlayers中的某些函数无法使用了，提示not a function 

  在ol-debug.js中存在的函数在ol.js中就不一定存在了。
  类似于 ```(new ol.format.GeoJSON()).readFeaturesFromObject(maskObj)```
 就不能使用了， 会提示readFeaturesFromObject is not a function。
 
 为避免再次遇到这类问题，还是以官方文档作为依据。

 ### 后端

 1. Jacob利用word模板导出word文档，总是报错。
 
 根据[Java2word](http://blog.csdn.net/fishroad/article/details/47951061)用于生成word，自己创建了template.docx。 但在运行时报错 `com.jacob.com.ComFailException: Invoke of: HomeKey 方法或属性无效因为该命令不可用于读取`。

 问题出在template.docx上，新版本word默认设置为“在阅读视图下打开电子邮件附件及其他不可编辑的文件”，解决办法很简单，进入WORD选项/常规，取消该选项即可。