# eslintとPrettierでコードを整形する

## プラグインのインストール

- Prettier
  - jsを整形するプラグイン
- eslint-config-prettier
  - eslintの整形ルールを無効にするプラグイン
- eslint-plugin-prettier
  - eslintからPrettierを使用するプラグイン

```shell
npm install --save-dev prettier@2.0.5 eslint-config-prettier@6.11.0 eslint-plugin-prettier@3.1.4
```

## eslintの設定ファイルの更新

```js
module.exports = {
    root: true, // .eslintrc.jsがあるディレクトリより親の階層に設定ファイルを探しに行かないよう設定
    env: {
        browser: true, // browserで使用するJSかどうか
        es2020: true, // es2020の記法でもerrorを出さない
    },
    parserOptions: {
        sourceType: 'module', // import exportでエラーを出さない
    },
    extends: ['eslint:recommended', 'plugin:prettier/recommend'], // 適用するルール(まとまったルール), 'plugin:prettier/recommend'は最後に記述
    rules: {
        'prefer-const': 'error'
    }
}
```

## prettierの設定ファイルの追加

.prettierrc.js

```js
module.exports = {
    singleQuote: true,
}
```
