# Polyfillの使用

## Polyfillとは

> APIがサポートされていないなど、構文の変換だけでは対応できない機能への対応を行うpolyfillを追加できるようにします。

## Polyfillのインストール

Promise, async, awaitを使う場合

```shell
npm install --save-dev core-js@3.6.5 regenerator-runtime@0.13.7
```

## Poryfillを取り込む

**import文でも取り込めるが、全てのPoryfillを取り込んでしまうため無駄なのでbabelを使用する！**

babel.config.js

```js
module.exports = {
    presets: [
        [
            '@babel/preset-env',
            {
                useBuiltIns: 'usege', // 必要なものだけ取り込む指定
                corejs: 3,   // デフォルトは2なのでエラーとなる
                debug: true, // 確認用
            }
        ],
    ]
}
```
