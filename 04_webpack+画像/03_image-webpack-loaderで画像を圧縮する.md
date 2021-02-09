# image-webpack-loaderで画像を圧縮する

## image-webpack-loaderのインストール

```shell
npm install --save-dev image-webpack-loader@6.0.0
```

## webpack設定ファイルの編集

※デフォルトでの圧縮

```js
module: { // ローダー設定
    rules: [
        // 省略
        {
            test: /\.(jpe?g|gif|png|svg)$/, // 処理対象とするファイルの指定
            use: [
                {
                    loader: 'file-loader',
                    options: {
                        name: '[name].[contenthash].[ext]', // 出力するファイル名 [name] → バンドル前のファイル名、[ext] → バンドル前の拡張子名
                        outputPath: 'images', // 出力先
                        publicPath: '../images'　// CSSなどから読み込まれる際のパス
                    },
                },
                'image-webpack-loader', // ココ
            ]
        },
        {
            test: /\.html$/, // 処理対象とするファイルの指定
            loader: 'html-loader',
        },
    ]
},
```

※画像の品質を調整する場合

```js
{
    loader: 'image-webpack-loader',
    options: {
        mozjpeg: { // jpegに関して圧縮
            quality: 10, // 品質 max 100
        },
    }
}
```
