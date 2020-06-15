---
layout: post
title:  "Use webpack 4 + bootstrap 4 + fontawesome 5 (2)"
date:   2019-03-20
categories: ['web development']
tags: ['tool']
---

接上一篇文章，我将在这一篇文章中分离 webpack 开发环境和生产环境，并使用 `webpack-merge` 来进行合并。

#### 添加 webpack-merge

```
❯ yarn add -D webpack-merge
```

#### 新建 webpack.dev.config.js

```
❯ touch webpack.dev.config.js
```

在 webpack.dev.config.js 添加:

```js
module.exports = () => ({
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: [
          {
            loader: 'style-loader',
            options: { injectType: 'singletonStyleTag' }
          }
        ]
      },
    ]
  }
})
```

#### 新建 webpack.prod.config.js

```
❯ touch webpack.prod.config.js
```

在 webpack.prod.config.js 添加:

```js
const MiniCssExtractPlugin = require('mini-css-extract-plugin')
const { CleanWebpackPlugin } = require('clean-webpack-plugin')

module.exports = () => ({
  plugins: [
    new CleanWebpackPlugin(),
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
          MiniCssExtractPlugin.loader
        ]
      },
    ]
  }
})
```

#### 更改 webpack.config.js

更改 webpack.config.js 为:

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const merge = require('webpack-merge')

module.exports = (env, argv) => {
  const publicPath = ''
  const isProd = argv.mode === 'production'
  const resolve = (dir) => path.resolve(__dirname, dir)
  const config = isProd ? require('./webpack.prod.config') : require('./webpack.dev.config')

  return merge(config(), {
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
    ],

    module: {
      rules: [
        {
          test: /\.scss$/,
          use: [
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
    }
  })
}
```

除了移除开发环境和生产环境的代码，主要的更改涉及:

```js
...
const merge = require('webpack-merge')

module.exports = (env, argv) => {
  ...
  const config = isProd ? require('./webpack.prod.config') : require('./webpack.dev.config')

  return merge(config(), {
    ...
  })
}
```

我这里选择利用 webpack 默认读取 `webpack.config.js` 而将其作为公共的部分并在这里进行合并，通常你也可以在 webpack.dev.config.js 和 webpack.prod.config.js 里进行合并，然后手动设置配置文件，比如:

```
npx webpack-dev-server --mode development --config webpack.dev.config.js
```

#### 几个常用的 babel 插件

```
❯ yarn add -D @babel/plugin-proposal-class-properties @babel/plugin-transform-runtime
```

> `@babel/plugin-proposal-class-properties` 用来使用属性初始化语法或者将绑定函数绑定到类实例上  
`@babel/plugin-transform-runtime` 用来复用 Babel 注入的辅助函数以节省代码体积

修改 webpack.config.js 里 `babel-loader` 相应的规则并添加 plugins 字段:

```js
{
  test: /\.m?js$/,
  exclude: /node_modules/,
  use: [
    {
      loader: 'babel-loader',
      options: {
        presets: ['@babel/preset-env'],
        plugins: [
          '@babel/plugin-proposal-class-properties',
          '@babel/plugin-transform-runtime'
        ]
      }
    }
  ]
},
```

我将在下一篇文章中进一步优化 webpack 和其他的配置。
