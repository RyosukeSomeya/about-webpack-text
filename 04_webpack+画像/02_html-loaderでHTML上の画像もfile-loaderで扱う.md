# html-loaderでHTML上の画像もfile-loaderで扱う

## html-loaderのインストール

```shell
npm install --save-dev html-loader@1.1.0
```

## webpack設定ファイルの編集

```js
{
    test: /\.html$/, // 処理対象とするファイルの指定
    loader: 'html-loader',
},
```
