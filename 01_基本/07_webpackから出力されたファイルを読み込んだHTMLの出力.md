# 7. webpackから出力されたファイルを読み込んだHTMLの出力

## html-webpack-pluginのインストール

```shell
npm install --save-dev html-webpack-plugin@4.3.0
```

## 設定ファイル更新

```js
const path = require('path');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');
const HtmlWebpackPlugin = require('html-webpack-plugin'); // プラグイン読み込み

module.exports = {
    entry: './src/js/app.js',　// エントリーポイント
    output: { // 出力設定
        path: path.resolve(__dirname, 'public'), // 絶対パス
        filename: 'js/bundle.js' // 出力するファイル名
    },
    plugins: [
        new CleanWebpackPlugin({
            // 削除対象の指定
            // cleanOnceBeforeBuildPatterns: ['**/*', '!**.html'],
        }),
        new HtmlWebpackPlugin({
            template: './src/html/index.html', // テンプレートになるHTML
        }),
    ]
}
```
