# webpack4 react antd redux项目构建

React, React-Router4, Redux, React-Redux, Redux-thunk, antd, eslint, Prettier

首先让我们来思考下整个项目的目录的结构

1. 我们需要一个public目录，放置index.html, favicon.ico 这种静态文件， 事实上放在根目录下也可以，弄个public目录放只是使目录看起来更清晰点
2. webpack配置文件我们也集中放在一个目录里，就叫build吧
3. 构建好的代码放置的目录 dist (不需要手动创建，构建时自动生成)
4. 源码目录 src

好， 所以我们最初始的目录结构就是如下

```
myapp
  |      package.json
  |      .babelrc
  |      .eslintrc.js
  |      .prettierrc
  +----- public // 静态资源
  |        index.html
  |        favicon.ico
  +----- build // webpck 配置
  |         webpack.base.config.js
  |         webpack.dev.config.js
  |         webpack.prod.config.js
  +----- src  // 源码目录
  |         App.js  // 入口文件
  |         assets  // 静态资源目录
  +-----dist  // build构建好的代码目录
```

现在我们来开始创建我们的目录

```
mkdir myapp

cd myapp

// 初始化项目， 生成package.json
npm init 或 yarn init

// 新建目录
mkdir public
mkdir build
mkdir src

```

接下来我们来安装依赖
```
// 打包依赖
yarn add react react-dom prop-types react-router-dom redux react-redux redux-thunk husky history

// 开发依赖
// babel
// 一种直接引入babel-polyfill
yarn add --dev babel-loader @babel/core @babel/polyfill @babel/preset-env @babel/preset-react babel-plugin-import

// 使用transfrom-runtime + 各种plugins
yarn add --dev babel-loader @babel/core @babel/runtime @babel/plugin-transform-runtime @babel/preset-env @babel/preset-react babel-plugin-import
	@babel/plugin-proposal-object-rest-spread 
	@babel/plugin-proposal-class-properties 	
	@babel/plugin-proposal-decorators 
	@babel/plugin-proposal-export-default-from 
	@babel/plugin-proposal-export-namespace-from

// webpack
yarn add --dev webpack webpack-dev-server html-webpack-plugin mini-css-extract-plugin 

// 静态文件相关loader (css, less, 图片，音频，视频， 字体 )
yarn add --dev css-loader style-loader postcss-loader file-loader url-loader less less-loader autoprefixer postcss-preset-env postcss-safe-parser


// eslint
yarn add --dev eslint babel-eslint eslint-loader  eslint-config-airbnb  eslint-plugin-import  eslint-plugin-react  eslint-plugin-jsx-a11y


// prettier
yarn add --dev prettier eslint-plugin-prettier eslint-config-prettier


// 其它
yarn add --dev　cross-env rimraf lint-staged

```




创建 .babelrc 

```
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "loose": true,
        "modules": false,
        "useBuiltIns": "usage",
        "targets": {
          "browsers": [
            "> 1%",
            "last 2 versions",
            "Android >= 4"
          ]
        }
      }
    ],
    "@babel/preset-react"
  ]
}
```