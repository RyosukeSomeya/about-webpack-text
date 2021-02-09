# console.logを削除する

TerserWebpack pluginインストール
※デフォルトでも入っているが新しいものにする。

```shell
npm install --save-dev terser-webpack-plugin@3.0.8
```

webpack.prod.js

```js
const { merge } = require('webpack-merge');
const commonConfig = require('./webpack.common');
const TerserPlugin = require('terser-webpack-plugin');

module.exports = merge(commonConfig, {
    mode: 'production',
    // 以下、terser-webpack-pluginの設定
    optimization: {
        minimizer: [
            new TerserPlugin({
                extractComments: false, // ライブラリのコメント抽出ファイルなどをしない
                terserOptions: {
                    compress: {
                        drop_console: true, // console.logを削除する
                    },
                },
            }),
        ]
    }
})
```
