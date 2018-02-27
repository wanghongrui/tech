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

2. 对ol-debug.js打包后操作后也就是某些函数无法访问了。类似于
 ```(new ol.format.GeoJSON()).readFeaturesFromObject(maskObj)```
 就不能使用了。会提示readFeaturesFromObject is not a function，为避免遇到类似问题，请以官方文档为依据。