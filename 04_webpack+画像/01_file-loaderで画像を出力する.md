# file-loaderで画像を出力する

webpackでバンドルしているcssなどで画像を扱う際に使用する。
※cssで読み込んでいる画像などもバンドル対象になるため。

## file-loaderのインストール

```shell
npm install --save-dev file-loader@6.0.0
```

## webpack設定ファイルの編集

webpack.common.js

```js
module: { // ローダー設定
    rules: [
        // 省略
        {
            test: /\.(jpe?g|gif|png|svg)$/, // 処理対象とするファイルの指定
            loader: 'file-loader',
            options: {
                name: '[name].[contenthash].[ext]', // 出力するファイル名 [name] → バンドル前のファイル名、[ext] → バンドル前の拡張子名
                outputPath: 'images', // 出力先
                publicPath: '../images'　// CSSなどから読み込まれる際のパス
            }
        },
    ]

```
