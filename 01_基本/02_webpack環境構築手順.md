# webpack環境構築手順

## 1 package.json作成

```shell
npm init -y
```

### package.jsonから不要記述を削除した初期状態

```json
{
  "name": "webpack-learning",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  }
}
```

## 2 webpackとwebpack-cliのインストール

```shell
npm install --save-dev webpack@4.43.0 webpack-cli@3.3.11
```

## 3 package.jsonについて

### devDependenciesとdependencies

devDependencies →　開発時に必要なモジュール
dependencies    →　実行ファイルに必要なモジュール

```json
  "devDependencies": { // --save-devでインストールしたもの（開発時のみ使用）
    "webpack": "^4.43.0",
    "webpack-cli": "^3.3.11"
  },
  "dependencies": { // --save でインストールしたもの(実行ファイルに必要。webpackでバンドルされるもの。)
    "jquery": "^3.5.1",
    "velocity-animate": "^1.5.2"
  }
```

### npm scripts

コマンドのショートカットを登録できる

```json
  "scripts": {
    "build": "webpack" // webpackをbuildする
  },
```

実行時

```shell
npm run <ショートカット名>

npm run build # ← 'webpack'というコマンドよりも、何をするか明示的になる
```

### webpack設定ファイル(webpack.config.js)作成

```js
const path = require('path');

module.exports = {
    mode: 'development', // 実行モード
    entry: './src/js/app.js',　// エントリーポイント
    output: { // 出力設定
        path: path.resolve(__dirname, 'public'), // 絶対パス
        filename: 'js/bundle.js' // 出力するファイル名
    }
}
```
