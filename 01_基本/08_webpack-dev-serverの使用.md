# 8. webpack-dev-serverの利用

## webpack-dev-serverのインストール

```shell
npm install --save-dev webpack-dev-server@3.11.0
```

## package.jsonの更新

startで起動できるようscriptsに追加

```js
 "scripts": {
    "start": "webpack-dev-server --config webpack.dev.js",
    "dev": "webpack --config webpack.dev.js",
    "build": "webpack --config webpack.prod.js"
  },
```

### webpack設定ファイルの更新

※webpack.common.js

```js
const { merge } = require('webpack-merge');
const commonConfig = require('./webpack.common');
const path = require('path');

module.exports = merge(commonConfig, {
    mode: 'development',
    watch: true, // 監視と自動ビルド
    devtool: 'cheap-module-eval-source-map',
    devServer: {
        open: true,
        port: 9000,
        contentBase: path.resolve(__dirname, 'public'), // ルートディレクトリ
    }
})
```
