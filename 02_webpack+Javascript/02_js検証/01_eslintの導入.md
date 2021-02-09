# eslintの導入

## eslintとeslint-loaderのインストール

```shell
npm install --save-dev eslint-loader@4.0.2 eslint@7.5.0
```

## eslint設定ファイルの作成

.eslintrc.js

```js
module.exports = {
    root: true, // .eslintrc.jsがあるディレクトリより親の階層に設定ファイルを探しに行かないよう設定
    env: {
        browser: true, // browserで使用するJSかどうか
        es2020: true, // es2020の記法でもerrorを出さない
    },
    parseOptions: {
        sourceType: 'module', // import exportでエラーを出さない
    },
    extends: ['eslint:recommended'], // 適用するルール(まとまったルール)
    rules: {
        'prefer-const': 'error'
    }
}
```

## webpack設定ファイルの編集

```js
module: {
    rules: [
        {
            enforce: 'pre', // 他のloaderよりも先に動作する指定
            test: /\.js$/,
            exclude: /node_modules/, // 処理対象から除外する指定
            loader: 'eslint-loader',
            options: {
                // fix: true, // 一部のエラーを自動で修正
            }
        },
        // 省略
```
