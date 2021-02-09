# source mapの作成

```js
const { merge } = require('webpack-merge');
const commonConfig = require('./webpack.common');

module.exports = merge(commonConfig, {
    mode: 'development',
    watch: true, // 監視と自動ビルド
    devtool: 'cheap-module-eval-source-map' // source-mapを指定
})
```
