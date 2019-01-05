# 基于 `gulp` 的 APICloud 脚手架

## 介绍

为了方便开发 APICloud 应用，本脚手架提供了 `less`、`pug`、`ES6` 语法编译支持，同时集成了 `autoprefixer`。并且，在生产环境编译时，会自动把页面引用的所有 `css`、 `js` 以内联的方式注入到html页面中，从而提高APP的性能。

在生产环境下，为了易于调试、支持`source map`(目前只配置了css的`source map`)，只会编译`less`及`ES6`语法，并且实时监视`src`目录下的文件变动并动态编译到目标目录，再配合 APICloud Studio 2 的WIFI自动同步功能，从而实现改完文件APP自动刷新。

推荐每个`html`文件都建立对应名称的`less`与`js`文件，打包时会自动把这些文件以内联的方式注入到`html`中。

**注意：** `es6` 语法只能在js文件中使用，不能在html文件的内联script标签中使用！

**注意：** 运行打包或开发命令时会删除`dist`下的 `html`、`css`、`script`、`image`、`res`文件夹！

## 目录说明

```dir
apicloud-gulp-template
├── dist    // 最终编译后的文件目录，在gulpfile中把它改成你项目的实际目录
│   ├── config.xml
│   ├── html
│   │   └── main.html
│   ├── image
│   │   └── loading_more.gif
│   └── index.html
├── gulpfile.js
├── package-lock.json
├── package.json
├── Readme.md
├── src   // 源文件目录
│   ├── common // 公共css、less文件夹，不要在html中直接引用本文件夹的内容，本文件夹用于存放布局模板、mixin等代码，然后由css文件夹里的less文件用@import引入
│   │   └── common.less
│   ├── config.xml // app配置文件
│   ├── css // css文件夹，在html引用less文件时，请把less扩展名改成css，如在index.html引用index.less的写法为src="./css/index.css"
│   │   ├── api.css
│   │   ├── index.less
│   │   └── main.less
│   ├── html // html文件夹
│   │   └── main.pug
│   ├── image // 图片文件夹
│   │   └── loading_more.gif
│   ├── index.pug  // app主页文件
│   ├── layout  // 存放pug布局文件，不要在html中直接引用本文件夹的内容，在html文件夹的pug文件中用extend或include的方式引入
│   │   └── layout.pug
│   ├── res // 资源文件目录
│   └── script // js 文件夹
│       ├── api.js
│       ├── index.js
│       └── main.js
└── tmp // 本文件夹为临时文件目录，用于存放编译后的less、js文件，最后再读取本文件夹的内容内联到html中
    ├── css
    │   ├── api.css
    │   ├── index.css // 事实上，上面的 src="./css/index.css" 引用的是这个文件！
    │   └── main.css
    ├── html
    │   └── main.html
    ├── index.html
    └── script
        ├── api.js
        ├── index.js
        └── main.js
```

## 使用

```bash
git clone https://github.com/lyswhut/apicloud-gulp-template.git

npm install

# 检查gulp是否全局安装及版本
# gulp版本要求4.x
# 若不符合要求请全局安装或更新到4.x
gulp -v
```

然后把你的源代码放到src目录中对应的目录里。

再打开 `gulpfile.js` 修改 `paths` 对象里的 `dist` 值为你的最终输出目录。

> 再说一遍，运行打包或开发命令时会删除 `dist` 下的 `html`、`css`、`script`、`image`、`res`文件夹！

最后

```bash
# 开发模式
npm run dev

# 打包
npm run build
```

## LICENSE

MIT