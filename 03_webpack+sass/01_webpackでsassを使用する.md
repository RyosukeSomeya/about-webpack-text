# webpackでsassを使用する

## packageのインストール

- sass-loader
  - sassをcssにコンパイルする
- node-sass
  - sass-loaderの実行に必要
  - sass-loaderはproductionモードで実行すると圧縮が有効になっている
- css-loader
  - cssをモジュールに変換する
- style-loader
  - バンドルしたcssをhtmlに挿入する

```shell
npm install --save-dev sass-loader@8.0.2 node-sass@4.14.1 css-loader@3.5.3 style-loader@1.2.1
```

## JavaScriptファイルでCSSをバンドルする

### エントリーポイントとなるファイルの編集

```js
import '../scss/style.scss';
```

### webpack設定ファイルの更新

webpack.common.js

```js
{
    test: /\.scss$/, // 処理対象とするファイルの指定
    use: ['style-loader', 'css-loader', 'sass-loader'] // 利用するローダーを指定(右から実行される)
},
```

## 個別のCSSファイルにCSSをバンドルする

### プラグインのインストール

```shell
npm install --save-dev mini-css-extract-plugin@0.9.0
```

※style-loaoderは不要になるので、アンインストールする場合は下記コマンドを実行

```shell
npm uninstall style-loader
```

### webpackの設定ファイルの更新

```js
// 省略
const MiniCssExtractPlugin = require('mini-css-extract-plugin'); // プラグイン読み込み
// 省略
module: {
    // 省略
    {
        test: /\.scss$/, // 処理対象とするファイルの指定
        use: [MiniCssExtractPlugin.loader, 'css-loader', 'sass-loader'] // 利用するローダーを指定(右から実行される)
    },
 // 省略
```

## 複数のエントリーポイントのSASSを複数のCSSとして出力

### エントリーポイントの追加

webpack.common.js

```js
entry: {
        app: './src/js/app.js',　// エントリーポイント1
        another: './src/js/another.js'　,// エントリーポイント2
        pc: './src/scss/style.scss', // エントリーポイント3
        mobile: './src/scss/test.scss' // エントリーポイント3
    },
```

ココまでで、ビルドするとcssのデータがjsファイルとしても出力されてしまうので、*不要なjsファイルを削除するプラグインをインストール

```shell
npm install --save-dev webpack-fix-style-only-entries
```

### webpack設定ファイルを編集

webpack.common.js

```js
plugins: [
    new CleanWebpackPlugin({
        // 削除対象の指定
        // cleanOnceBeforeBuildPatterns: ['**/*', '!**.html'],
    }),
    new HtmlWebpackPlugin({
        template: './src/html/index.html', // テンプレートになるHTML
        chunks: ['app'], // 読み込ませたいファイルの指定
    }),
    new HtmlWebpackPlugin({
        filename: 'another.html', // 出力するファイル名(デフォルトはindex.html)
        template: './src/html/another.html', // テンプレートになるHTML
        chunks: ['another'], // 読み込ませたいファイルの指定
    }),
    new FixStyleOnlyEntries(),
    new MiniCssExtractPlugin({
        filename: './css/[name].[contenthash].css' // 出力の起点はoutputで指定したパス　[name]には、エントリーポイント名が入る
    }),
]
```
