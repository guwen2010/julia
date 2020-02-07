#webpack 在我们传统站点的作用
        1、统一管理css,js
        2、对css进行压缩
        3、对js进行混沌压缩
#webpack 压缩问题（author:徐彦广）
##压缩的配置
        1)	获取需要压缩的所有js、css的文件名称的字符串
        2)	将字符串转化成可以被webpack识别的对口文件以及想对
        应路径
        3)	全局的函数需要写成window.name=function(){};的
        形式，告知压缩插件不需要对此函数进行混淆，因为混
        淆后的函数 无法被全局调用。
```
    /*将字符串编辑成对象格式  */
    function mapCSS(str, output, input, type) {
        var cssArr = str.split('.' + type);
        var cssObj = {};
        for (let i = 0; i < cssArr.length; i++) {
            let key = cssArr[i].replace(/\s*/g, "");
            if (key == '') {
                continue;
            }
            cssObj[output + "/" + key] = input + "/" + key + "." + type;
        }
        return cssObj;
    };
    /*end 将字符串编辑成对象格式  */
```
    需要用到以下插件及loader:
```
    "css-loader": "^3.4.2",
        "file-loader": "^5.0.2",
        "mini-css-extract-plugin": "^0.9.0",
        "optimize-css-assets-webpack-plugin": "^5.0.3",
        "style-loader": "^1.1.2",
        "uglifyjs-webpack-plugin": "^2.2.0",
        "url-loader": "^3.0.0",
        "webpack": "^4.41.5",
        "webpack-cli": "^3.3.10",
        "webpack-fix-style-only-entries": "^0.4.0"
    const MiniCssExtractPlugin = require('mini-css-extract-plugin');//压缩css
    const optimizeCss = require('optimize-css-assets-webpack-plugin');//将入口css单独打包
    const UglifyJsPlugin = require('uglifyjs-webpack-plugin');//压缩js
    const FixStyleOnlyEntriesPlugin = require('webpack-fix-style-only-entries'); //剔除入口css生成的多余的js
```

具体的细节请看站点目录下 webpack.config.js 文件