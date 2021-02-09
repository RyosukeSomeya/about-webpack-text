# CSS最適化

## プラグインのインストール

```shell
npm install --save-dev optimize-css-assets-webpack-plugin@5.0.3
```

※postcss-loaderを使っていれば上記のプラグインをインストールせずに、postcss-loaderの設定にcssnanoを使用する設定を追加すれば良い

### webpack設定ファイルの編集

#### optimize-css-assets-webpack-plugin使用時

webpack.prod.js
※いつ最適化させるのかで記述する設定ファイルは変わる

```js
const { merge } = require('webpack-merge');
const commonConfig = require('./webpack.common');
const TerserPlugin = require('terser-webpack-plugin');
const OptimizeCSSAssetsPlugin = require('optimize-css-assets-webpack-plugin');

module.exports = merge(commonConfig, {
    mode: 'production',
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
            new OptimizeCSSAssetsPlugin({})
        ]
    }
})

```

#### postcss-loaderで使用する場合

postcss.config.js

```js
module.exports = {
    plugins: [
        require('autoprefixer'),
        require('cssnano'), // postcssでcssnanoを使うとき
    ],
}
```
