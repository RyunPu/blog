---
layout: post
title:  "Use webpack 4 + bootstrap 4 + fontawesome 5 (3)"
date:   2019-03-21
categories: ['web development']
tags: ['tool']
---

接上一篇文章，我将在这一篇文章中进一步优化 webpack 和其他的配置。

### 基础优化

#### 使用 hard-source-webpack-plugin 提升构建速度

```
❯ yarn add -D hard-source-webpack-plugin
```

在 webpack.config.js 中引入并使用 HardSourceWebpackPlugin

```js
...
const HardSourceWebpackPlugin = require('hard-source-webpack-plugin')

module.exports = (env, argv) => {
  ...

  return merge(config(), {
    ...

    plugins: [
      ...
      new HardSourceWebpackPlugin(),
    ],
  })
}
```

第一次运行的 Time:

```
$ webpack --mode production
[hardsource:79b1fb26] Writing new cache 79b1fb26...
[hardsource:79b1fb26] Tracking node dependencies with: yarn.lock.
Hash: f900197047d13d1149d1
Version: webpack 4.41.5
Time: 1561ms
```

第二次运行的 Time:

```
$ webpack --mode production
[hardsource:79b1fb26] Using 2 MB of disk space.
[hardsource:79b1fb26] Tracking node dependencies with: yarn.lock.
[hardsource:79b1fb26] Reading from cache 79b1fb26...
Hash: 3bac00f3a8f8ef5e024c
Version: webpack 4.41.5
Time: 266ms
```

#### 使用模块热替换

在 webpack.dev.config.js 中使用 devtool 和 devServer:

```js
module.exports = () => ({
  devtool: 'cheap-module-eval-source-map',

  devServer: {
    hot: true,
    clientLogLevel: 'error'
  },

  ...
})
```

> 关于 devtool，可以访问 https://webpack.docschina.org/configuration/devtool/

复制 src/js/index.js 为 src/js/main.js:

```
❯ cp src/js/index.js src/js/main.js
```

修改 src/js/index.js 为:

```js
import './main'

if (module.hot) {
  module.hot.accept('./main')
}
```

现在我们再更改 src/js/main.js，就会发现只有页面的局部刷新了。

现在去更改 index.html，我们会发现页面不再刷新了，这个或许是使用 `html-webpack-plugin` 的问题，我们在 devServer 里加个 before 钩子来修复这个问题:

```js
devServer: {
  hot: true,
  clientLogLevel: 'error',
  before(app, server) {
    server._watch('./index.html')
  }
},
```

> before 钩子用来在服务内部的所有其他中间件之前，提供执行自定义中间件的功能

#### 添加 resolve

在 webpack.prod.config.js 中使用 resolve:

```js
...
const merge = require('webpack-merge')

module.exports = (env, argv) => {
  ...

  return merge(config(), {
    ...

    output: {
      ...
    },

    resolve: {
      modules: [
        resolve('node_modules')
      ],
      extensions: ['.js'],
      alias: {
        '@': resolve('./src')
      }
    },

    ...
  })
}
```

> modules 告诉 webpack 解析模块时应该搜索的目录，使用该选项以优化搜索  
使用 alias 来简化模块引入:  
~~import \'../src/styles/main.scss\'~~  
import \'@/styles/main.scss\'

### 压缩代码

#### 压缩 css 和 js

```
❯ yarn add -D optimize-css-assets-webpack-plugin terser-webpack-plugin
```

在 webpack.prod.config.js 中引入插件并使用 devtool 和 optimization:

```js
...
const OptimizeCSSAssetsPlugin = require('optimize-css-assets-webpack-plugin')
const TerserJSPlugin = require('terser-webpack-plugin')

module.exports = () => ({
  devtool: 'none', // or 'source-map'

  optimization: {
    minimizer: [
      new TerserJSPlugin(),
      new OptimizeCSSAssetsPlugin({
        cssProcessorPluginOptions: {
          preset: ['default', { discardComments: { removeAll: true } }]
        }
      })
    ],
  },

  ...
})
```

#### 根据需要压缩图片

```
❯ yarn add -D imagemin@^6.0.0 img-loader imagemin-mozjpeg imagemin-pngquant
```

> `img-loader` 依赖指定的版本的 `imagemin`，可以根据需要选择是否去掉版本号

在 webpack.config.js 中图片的规则处使用 img-loader:

```js
...

module.exports = (env, argv) => {
  ...

  return merge(config(), {
    ...

    module: {
      rules: [
        ...

        {
          test: /\.(png|jpe?g|gif)$/i,
          use: [
            {
              loader: 'url-loader',
              ...
            },
            {
              loader: 'img-loader',
              options: {
                plugins: isProd && [
                  require('imagemin-mozjpeg')({
                    quality: 50
                  }),
                  require('imagemin-pngquant')({
                    quality: [0.4, 0.6]
                  }),
                ]
              }
            },
          ]
        },
      ]
    }
  })
}
```

> `img-loader` 需要放在 `url-loader` 的后面，所以这里通过 `isProd` 进行了简单的处理

#### 根据需要使用 gzip

```
❯ yarn add -D compression-webpack-plugin
```

在 webpack.prod.config.js 中引入插件并使用 CompressionPlugin:

```js
...
const CompressionPlugin = require('compression-webpack-plugin')

module.exports = () => ({
  ...

  plugins: [
    ...
    new CompressionPlugin(),
  ],

  ...
})
```

### 代码分离

#### 使用 splitChunks

在 webpack.prod.config.js 的 optimization 选项中使用 splitChunks:

```js
...

module.exports = () => ({
  ...

  optimization: {
    splitChunks: {
      chunks: 'all'
    },
    ...
  },

  ...
})
```

> 关于 splitChunks，可以访问 https://github.com/npm/npx

#### 使用动态导入

```js
import('bootstrap/js/dist/modal' /* webpackChunkName: "bootstrap-modal" */)
```

#### 使用预加载

```js
import('bootstrap/js/dist/modal' /* webpackPrefetch: true */)
```

#### 使用 autodll-webpack-plugin

```
❯ yarn add -D autodll-webpack-plugin
```

> 使用 `autodll-webpack-plugin` 可以把指定的依赖打包在一起

在 webpack.config.js 中引入插件并使用 AutoDllPlugin:

```js
...
const AutoDllPlugin = require('autodll-webpack-plugin')

module.exports = (env, argv) => {
  ...

  return merge(config(), {
    ...

    plugins: [
      ...
      new AutoDllPlugin({
        inject: true,
        filename: 'dll~[name]_[hash:5].js',
        path: './static/js',
        entry: {
          main: [
            'jquery',
            'popper.js',
            'bootstrap',
          ]
        }
      }),
    ],

    ...
  })
}
```

修改 src/js/main.js 中 bootstrap 部分的引入:

```js
// import 'bootstrap/js/dist/modal'
import 'bootstrap'
```

#### 使用 webpack-cdn-plugin

```
❯ yarn add -D webpack-cdn-plugin
```

> 使用 `webpack-cdn-plugin` 可以把指定的依赖指向线上的地址，开发环境仍然使用本地的依赖

在 webpack.config.js 中引入插件并使用 WebpackCdnPlugin:

```js
...
// const AutoDllPlugin = require('autodll-webpack-plugin')
const WebpackCdnPlugin = require('webpack-cdn-plugin')

module.exports = (env, argv) => {
  ...

  return merge(config(), {
    ...

    plugins: [
      ...
      /*new AutoDllPlugin({
        inject: true,
        filename: 'dll~[name]_[hash:5].js',
        path: './static/js',
        entry: {
          main: [
            'jquery',
            'popper.js',
            'bootstrap',
          ]
        }
      }),*/
      new WebpackCdnPlugin({
        modules: [
          {
            name: 'bootstrap',
            cssOnly: true,
            style: 'dist/css/bootstrap.min.css'
          },
          {
            name: 'jquery',
            var: 'jQuery',
            path: 'dist/jquery.slim.min.js'
          },
          {
            name: 'popper.js',
            path: 'dist/umd/popper.min.js'
          },
          {
            name: 'bootstrap',
            path: 'dist/js/bootstrap.min.js'
          }
        ],
        prod: isProd,
        prodUrl: '//cdn.jsdelivr.net/npm/:name@:version/:path',
        publicPath: '/node_modules'
      }),
    ],

    ...
  })
}
```

去掉 src/js/main.js 中 bootstrap 部分的引入:

```js
// import 'bootstrap'
```

去掉 src/css/main.scss 中 bootstrap 部分的引入:

```scss
// @import '~bootstrap/scss/bootstrap';
```

### 分析工具

```
❯ yarn add -D webpack-bundle-analyzer
```

> `webpack-bundle-analyzer` 将 bundle 内容展示为便捷的、交互式、可缩放的树状图形式

在 webpack.prod.config.js 中引入插件并使用 BundleAnalyzerPlugin:

```js
...
const { BundleAnalyzerPlugin } = require('webpack-bundle-analyzer')

module.exports = () => ({
  ...

  plugins: [
    ...
    new BundleAnalyzerPlugin(),
  ],

  ...
})
```

分析工具截图:

![image](https://user-images.githubusercontent.com/6168498/72322471-60ee6880-36e1-11ea-92e6-6c9ae27a0402.png)

当你需要分析页面的性能时，可以使用 chrome Audits:

![image](https://user-images.githubusercontent.com/6168498/72323463-c5aac280-36e3-11ea-8a1d-9791821fc069.png)

Use webpack 4 + bootstrap 4 + fontawesome 5 系列到此就结束了，你可以在 [webpack-demo](https://github.com/RyunPu/webpack-demo) 查看最终代码。
