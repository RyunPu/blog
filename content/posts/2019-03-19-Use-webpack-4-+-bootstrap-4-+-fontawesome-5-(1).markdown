---
layout: post
title:  "Use webpack 4 + bootstrap 4 + fontawesome 5 (1)"
date:   2019-03-19
categories: ['web development']
tags: ['tool']
---

从零开始使用 webpack 4 创建一个 bootstrap 4 + fontawesome 5 的项目，有兴趣的同学可以跟着做下。

### 准备工作

#### 创建目录

```
❯ mkdir webpack-demo && cd webpack-demo
```

#### 添加 package.json

```
❯ yarn init -y
```

> 要安装 yran，可以访问 https://yarnpkg.com/lang/en/docs/install

package.json:

```
{
  "name": "webpack-demo",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT"
}
```

去掉入口和设置私有:

```
{
  "name": "webpack-demo",
  "version": "1.0.0",
  "private": true
}
```

#### 添加 .editorconfig

```
❯ ec init
```

> 要安装 editorconfig-cli，可以使用 yarn global add editorconfig-cli

```
root = true

[*]
charset = utf-8
indent_style = space
indent_size = 2
end_of_line = lf
trim_trailing_whitespace = true
insert_final_newline = true
```

#### 添加 .eslintrc.js

```
❯ yarn add -D eslint
❯ npx eslint --init
```

> 关于 npx，可以访问 https://github.com/npm/npx

.eslintrc.js:

```js
module.exports = {
  env: {
    browser: true,
    es6: true
  },
  extends: "eslint:recommended",
  globals: {
    Atomics: "readonly",
    SharedArrayBuffer: "readonly"
  },
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: "module"
  },
  rules: {}
}
```

通常情况下我还会选择使用 `babel-eslint`，当然你也可以选择 `eslint-loader` 等:

```
❯ yarn add -D babel-eslint
```

.eslintrc.js:

```js
module.exports = {
  parser: "babel-eslint",
  rules: {
    "semi": ["error", "never"],
    "comma-dangle": ["error", "only-multiline"],
    "indent": ["error", 2],
    "quotes": [2, "single", "avoid-escape"],
    "no-unused-vars": 1
  }
}
```

基本的准备工作就完成了，大家可以根据自己的需要选择是否忽略某些步骤。

### 创建文件

#### 添加 index.html、src/js/index.js 和 src/styles/main.scss

```
❯ touch index.html
❯ mkdir -p src/js && touch src/js/index.js
❯ mkdir -p src/styles && touch src/styles/main.scss
```

在 index.html 中加一些 bootstrap 和 fontawesome 的代码:

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">

<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
  <title>webpack-demo</title>
</head>

<body>
  <!-- Button trigger modal -->
  <div class="d-flex justify-content-center" style="height: 100vh;">
    <button type="button" class="btn btn-primary align-self-center" data-toggle="modal" data-target="#exampleModal">
      Launch webpack-demo modal <i class="fas fa-eye"></i>
    </button>
  </div>

  <!-- Modal -->
  <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          Hello There
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">
            Close
          </button>
          <button type="button" class="btn btn-primary">Save changes</button>
        </div>
      </div>
    </div>
  </div>
</body>

</html>
```

### 配置 webpack

#### 添加 webpack webpack-cli webpack-dev-server

```
❯ yarn add -D webpack webpack-cli webpack-dev-server
```

> 你也可以使用 [`@webpack-cli/init`](https://www.npmjs.com/package/@webpack-cli/init) 自动创建一个新 webpack 配置

#### 添加 webpack.config.js

```
❯ touch webpack.config.js
```

webpack.config.js:

```js
const path = require('path')

module.exports = (env, argv) => {
  const publicPath = ''
  const isProd = argv.mode === 'production'
  const resolve = (dir) => path.resolve(__dirname, dir)

  return {
    entry: {
      main: './src/js/index.js',
    },

    output: {
      path: resolve('dist'),
      filename: 'static/js/[name]_[hash:5].js',
      publicPath
    },
  }
}
```

现在可以让我们的项目跑起来了：

```
❯ npx webpack-dev-server --mode development
```

为了使用方便，我们在 package.json 添加相应的 scripts：

```
{
  "name": "webpack-demo",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "build": "webpack --mode production",
    "dev": "webpack-dev-server --mode development"
  },
  ...
}
```

现在我们可以使用：

```
❯ yarn run dev
```

现在的页面:

![image](https://user-images.githubusercontent.com/6168498/72239068-b6137700-361a-11ea-87fa-d5fc149491ca.png)

#### 添加 html-webpack-plugin

```
❯ yarn add -D html-webpack-plugin
```

> `html-webpack-plugin` 简化了 HTML 文件的创建，以便为 webpack 包提供服务

在 webpack.config.js 中引入并使用 HtmlWebpackPlugin

```js
...
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = (env, argv) => {
  ...

  return {
    ...

    plugins: [
      new HtmlWebpackPlugin({
        template: './index.html',
        minify: {
          removeComments: true,
          collapseWhitespace: true,
          removeAttributeQuotes: true
        }
      }),
    ],
  }
}
```

重新运行 `yarn run dev` 后，你可以发现页面已经自动注入了 script，更改页面后还能自动刷新。

在开使用 bootstrap 前，我们先添加好相应的 loader。

#### 添加 css 相应的 loader

```
❯ yarn add -D style-loader css-loader postcss-loader autoprefixer node-sass sass-loader
```

在 webpack.config.js 中添加相应的 rules:

```js
...

module.exports = (env, argv) => {
  ...

  return {
    ...

    module: {
      rules: [
        {
          test: /\.scss$/,
          use: [
            {
              loader: 'style-loader',
              options: { injectType: 'singletonStyleTag' }
            },
            'css-loader',
            {
              loader: 'postcss-loader',
              options: {
                ident: 'postcss',
                plugins: [
                  require('autoprefixer')()
                ]
              }
            },
            'sass-loader'
          ]
        },
      ]
    },
  }
}
```

在 package.json 中添加 browserslist 来配置 `autoprefixer` 的作用范围:

```
{
  ...
  "browserslist": [
    "> 2%",
    "last 1 versions"
  ]
}
```

> 关于 browserslist，可以访问 https://github.com/browserslist/browserslist

#### 添加 js 相应的 loader

```
❯ yarn add -D @babel/core @babel/preset-env babel-loader
❯ yarn add @babel/runtime
```

> 你或许会需要 `@babel/runtime` 来支持部分编译

在 webpack.config.js 中添加相应的 rules:

```js
...

module.exports = (env, argv) => {
  ...

  return {
    ...

    module: {
      rules: [
        ...

        {
          test: /\.m?js$/,
          exclude: /node_modules/,
          use: [
            {
              loader: 'babel-loader',
              options: {
                presets: ['@babel/preset-env']
              }
            }
          ]
        },
      ]
    }
  }
}
```

基本的配置工作就完成了，大家可以根据自己的需要选择是否使用某些 loader。

### 使用 bootstrap

#### 添加 jquery popper.js bootstrap

```
❯ yarn add jquery popper.js bootstrap
```

#### 在 src/styles/main.scss 中引入 bootstrap

```scss
@import '~bootstrap/scss/bootstrap';
```

或者按需引入:

```scss
@import '~bootstrap/scss/bootstrap-reboot';
@import '~bootstrap/scss/_modal';
...
```

#### 在 src/js/index.js 中添加:

```js
import '../styles/main.scss'
import 'bootstrap/js/dist/modal'
```

现在的页面:

![image](https://user-images.githubusercontent.com/6168498/72238250-3389b800-3618-11ea-99ae-22f224217e5a.png)

bootstrap 的使用就告一段落了，下面我们看下 fontawesome 的使用。

### 使用 fontawesome

#### 添加相应的依赖包

```
❯ yarn add @fortawesome/fontawesome-svg-core @fortawesome/free-regular-svg-icons @fortawesome/free-solid-svg-icons
```

> 使用 svg 的形式，我们可以按需引入自己所需的图标

#### 修改 src/js/index.js 为:

```js
import '../styles/main.scss'
import 'bootstrap/js/dist/modal'
import { library, dom } from '@fortawesome/fontawesome-svg-core'
import { faEye } from '@fortawesome/free-solid-svg-icons/faEye'

library.add(faEye)
dom.i2svg()
```

现在的页面:

![image](https://user-images.githubusercontent.com/6168498/72238397-90856e00-3618-11ea-8734-5c19e1c316cb.png)

fontawesome 的使用到此就结束了，下面我们处理下图片。

### 处理图片

#### 添加 html-loader file-loader url-loader

```
❯ yarn add -D html-loader file-loader url-loader
```

> `html-loader` 用来将 HTML 导出为字符串，我们通常使用它来解析生成 img 的 src

在 webpack.config.js 中添加相应的 rules:

```js
...

module.exports = (env, argv) => {
  ...

  return {
    ...

    module: {
      rules: [
        ...

        {
          test: /\.html$/,
          use: [
            {
              loader: 'html-loader',
              options: {
                attrs: ['img:src']
              }
            }
          ]
        },

        {
          test: /\.(png|jpe?g|gif)$/i,
          use: [
            {
              loader: 'url-loader',
              options: {
                limit: 8192,
                outputPath: 'static/images',
                publicPath: `${publicPath}/static/images`,
                esModule: false
              }
            },
          ]
        },
      ]
    }
  }
}
```

### 生产环境

#### 使用 mini-css-extract-plugin 分离 css

```
❯ yarn add -D mini-css-extract-plugin
```

在 webpack.config.js 中引入并使用 MiniCssExtractPlugin，根据 `isProd` 判断使用 `MiniCssExtractPlugin.loader` 或者 `style-loader`:

```js
...
const MiniCssExtractPlugin = require('mini-css-extract-plugin')

module.exports = (env, argv) => {
  ...

  return {
    ...

    plugins: [
      ...
      new MiniCssExtractPlugin({
        filename: 'static/css/[name].css',
        chunkFilename: 'static/css/[id].css'
      }),
    ],

    module: {
      rules: [
        {
          test: /\.scss$/,
          use: [
            isProd
              ? MiniCssExtractPlugin.loader
              : {
                loader: 'style-loader',
                options: { injectType: 'singletonStyleTag' }
              },
            'css-loader',
            {
              loader: 'postcss-loader',
              options: {
                ident: 'postcss',
                plugins: [
                  require('autoprefixer')()
                ]
              }
            },
            'sass-loader'
          ]
        },
        ...
      ]
    }
  }
}
```

#### 使用 clean-webpack-plugin 清理 dist 文件夹

```
❯ yarn add -D clean-webpack-plugin
```

在 webpack.config.js 中引入并使用 CleanWebpackPlugin:

```js
...
const { CleanWebpackPlugin } = require('clean-webpack-plugin')

module.exports = (env, argv) => {
  ...

  return {
    ...

    plugins: [
      ...
      isProd ? new CleanWebpackPlugin() : new Function
    ],

    ...
  }
}
```

> 这里我们第二次根据 `isProd` 进行了判断，稍后我将使用 `webpack-merge` 进行优化

### 最终的 package.json

```
{
  "name": "webpack-demo",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "build": "webpack --mode production",
    "dev": "webpack-dev-server --mode development"
  },
  "devDependencies": {
    "@babel/core": "^7.8.3",
    "@babel/preset-env": "^7.8.3",
    "autoprefixer": "^9.7.3",
    "babel-eslint": "^10.0.3",
    "babel-loader": "^8.0.6",
    "clean-webpack-plugin": "^3.0.0",
    "css-loader": "^3.4.2",
    "eslint": "^6.8.0",
    "file-loader": "^5.0.2",
    "html-loader": "^0.5.5",
    "html-webpack-plugin": "^3.2.0",
    "mini-css-extract-plugin": "^0.9.0",
    "node-sass": "^4.13.0",
    "postcss-loader": "^3.0.0",
    "sass-loader": "^8.0.2",
    "style-loader": "^1.1.2",
    "url-loader": "^3.0.0",
    "webpack": "^4.41.5",
    "webpack-cli": "^3.3.10",
    "webpack-dev-server": "^3.10.1"
  },
  "browserslist": [
    "> 2%",
    "last 1 versions"
  ],
  "dependencies": {
    "@babel/runtime": "^7.8.3",
    "@fortawesome/fontawesome-svg-core": "^1.2.26",
    "@fortawesome/free-regular-svg-icons": "^5.12.0",
    "@fortawesome/free-solid-svg-icons": "^5.12.0",
    "bootstrap": "^4.4.1",
    "jquery": "^3.4.1",
    "popper.js": "^1.16.0"
  }
}
```

### 最终的 webpack.config.js

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin')
const { CleanWebpackPlugin } = require('clean-webpack-plugin')

module.exports = (env, argv) => {
  const publicPath = ''
  const isProd = argv.mode === 'production'
  const resolve = (dir) => path.resolve(__dirname, dir)

  return {
    entry: {
      main: './src/js/index.js',
    },

    output: {
      path: resolve('dist'),
      filename: 'static/js/[name]_[hash:5].js',
      publicPath
    },

    plugins: [
      new HtmlWebpackPlugin({
        template: './index.html',
        minify: {
          removeComments: true,
          collapseWhitespace: true,
          removeAttributeQuotes: true
        }
      }),
      new MiniCssExtractPlugin({
        filename: 'static/css/[name].css',
        chunkFilename: 'static/css/[id].css'
      }),
      isProd ? new CleanWebpackPlugin() : new Function
    ],

    module: {
      rules: [
        {
          test: /\.scss$/,
          use: [
            isProd
              ? MiniCssExtractPlugin.loader
              : {
                loader: 'style-loader',
                options: { injectType: 'singletonStyleTag' }
              },
            'css-loader',
            {
              loader: 'postcss-loader',
              options: {
                ident: 'postcss',
                plugins: [
                  require('autoprefixer')()
                ]
              }
            },
            'sass-loader'
          ]
        },

        {
          test: /\.m?js$/,
          exclude: /node_modules/,
          use: [
            {
              loader: 'babel-loader',
              options: {
                presets: ['@babel/preset-env']
              }
            }
          ]
        },

        {
          test: /\.html$/,
          use: [
            {
              loader: 'html-loader',
              options: {
                attrs: ['img:src']
              }
            }
          ]
        },

        {
          test: /\.(png|jpe?g|gif)$/i,
          use: [
            {
              loader: 'url-loader',
              options: {
                limit: 8192,
                outputPath: 'static/images',
                publicPath: `${publicPath}/static/images`,
                esModule: false
              }
            },
          ]
        },
      ]
    },
  }
}
```
