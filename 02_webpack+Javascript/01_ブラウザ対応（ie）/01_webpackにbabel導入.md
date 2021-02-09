# webpackにbabel導入

## 1.プラグインインストール

- babel-loader@8.1.0
- @babel/core@7.10.5
- @babel/preset-env@7.10.4

```shell
npm install --save-dev babel-loader@8.1.0 @babel/core@7.10.5 @babel/preset-env@7.10.4
```

## 2.webpack設定ファイルの編集

`webpack.common.js`

```js
module: {
        test: /\.js$/, // 処理対象とするファイルの指定
        exclude: /node_modules/, // 処理対象から除外する指定
        loader: 'babel-loader' // 利用するローダーを指定
    },
```

## 3 babel設定ファイルの作成

`babel.config.js`

```js
module.exports = {
    presets: ['@babel/preset-env'],
}
```
