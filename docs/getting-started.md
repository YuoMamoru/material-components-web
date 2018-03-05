<!--docs:
title: "Getting Started"
layout: landing
section: docs
path: /docs/getting-started/
-->

# 入門ガイド

このガイドでは [MDC Web Node モジュールのインストール](https://www.npmjs.com/org/material) の方法と [Webpack](https://webpack.js.org/) の設定によってこれらの Node モジュールから Sass と JavaScript をバンドルする方法を説明します。

> 注意: このガイドは npm がローカルにインストールされていることを前提にしています。

### ステップ 1: Webpack の Sass の設定

webpack-dev-server を使ってどのように webpack が Sass と JavaScript をバンドルするのかを見ていきます。まず、次のような package.json を作成します。

```json
{
  "scripts": {
    "start": "webpack-dev-server"
  }
}
```

以下の Node 依存関係がすべて必要です。:
- [webpack](https://www.npmjs.com/package/webpack): Sass と JavaScript をバンドルする
- [webpack-dev-server](https://www.npmjs.com/package/webpack-dev-server): 開発サーバー
- [sass-loader](https://www.npmjs.com/package/sass-loader): Sass ファイルを読み込み CSS にコンパイルする
- [node-sass](https://www.npmjs.com/package/node-sass): Node.js を Sass にバインドし、sass-loader と同等の依存関係を提供する
- [css-loader](https://www.npmjs.com/package/css-loader): CSS の @import と url() のパスを解決する
- [extract-loader](https://github.com/peerigon/extract-loader): .css ファイル内の CSS を抽出する
- [file-loader](https://github.com/webpack-contrib/file-loader): .css ファイルを公開 URL として扱う

次のコマンドでこれらすべてをインストールできます。

```
npm install --save-dev webpack@3 webpack-dev-server@2 css-loader sass-loader node-sass extract-loader file-loader
```

> 注意: 私たちは webpack 3 を使うことを推奨します。なぜなら、webpack 4 がまだ調査中だからです。また、webpack-dev-server 2 の使用を推奨します。このバージョンが webpack 3 上で動作しているからです。

webpack が Sass をどのようにバンドルかを確認するには index.html が必要です。この HTML ファイルには CSS を含める必要があります。この CSS は sass-loader によって生成され、sass-loader が Sass から CSS にコンパイルします。CSS は .css ファイルから extract-loader によって抽出されます。単純な「hello world」の index.html を作成してください。

```html
<html>
 <head>
   <link rel="stylesheet" href="bundle.css">
 </head>
 <body>Hello World</body>
</html>
```

そして、app.scss という単純な Sass ファイルを作ってください。

```scss
body {
  color: blue;
}
```

次に、app.scss を bundle.css に変換する webpack を設定します。それには新たな webpack.config.js が必要です。

```js
module.exports = [{
  entry: './app.scss',
  output: {
    // この部分は webpack がコンパイルするために必要です
    // しかし、style-bundle.js は使いません
    filename: 'style-bundle.js',
  },
  module: {
    rules: [{
      test: /\.scss$/,
      use: [
        {
          loader: 'file-loader',
          options: {
            name: 'bundle.css',
          },
        },
        { loader: 'extract-loader' },
        { loader: 'css-loader' },
        { loader: 'sass-loader' },
      ]
    }]
  },
}];
```

webpack の設定をテストしましょう。

```
npm start
```

ブラウザで localhost:8080 を開いてください。青い “Hello World” が見れるはずです。

![Hello World](hello_world.png)

### ステップ 2: コンポーネントに CSS を含める

Sass から CSS にコンパイルするように webpack を設定したので、マテリアルデザインボタン用の Sass ファイルを入れてみましょう。まず、Node の依存関係をインストールします。

```
npm install @material/button
```

@material/button の Sass ファイルをインポートするように app.scss に記述する必要があります。ボタンをカスタマイズするために Sass ミキシンを使うことができます。以下のコードで「hello world」の app.scss を置き換えてください。

```scss
@import "@material/button/mdc-button";

.foo-button {
  @include mdc-button-ink-color(teal);
  @include mdc-states(teal);
}
```
@material/button にはボタンに必要な HTML についての [ドキュメント](packages/mdc-button/README.md) があります。index.html を以下の HTML を含めるように修正し、要素に foo-button クラスを加えてください。

```html
<body>
  <button class="foo-button mdc-button">
    Button
  </button>
</body>
```

@material 構文を解釈できるようにするために Sass ローダを設定する必要があります。webpack.config.js の `{ loader: 'sass-loader' }` を次のように修正してください。

```javascript
{
  loader: 'sass-loader',
  options: {
    importer: function(url, prev) {
      if(url.indexOf('@material') === 0) {
        var filePath = url.split('@material')[1];
        var nodeModulePath = `./node_modules/@material/${filePath}`;
        return { file: require('path').resolve(nodeModulePath) };
      }
      return { file: url };
    }
  }
}
```

さあ、npm start を再び実行して localhost:8080 を開いてください。マテリアルデザインボタンが確認できたでしょ！

![Button](button.png)

### ステップ 3: Webpack の ES2015 の設定

[babel](https://babeljs.io) を通して、ES2015 JavaScript を標準 JavaScript に変換するように webpack を設定する必要があります。以下の依存関係すべてが必要です。

- [babel-core](https://www.npmjs.com/package/babel-core)
- [babel-loader](https://www.npmjs.com/package/babel-loader): babel を使って JavaScript ファイルをコンパイルする
- [babel-preset-es2015](https://www.npmjs.com/package/babel-preset-es2015): ES2015 をコンパイルするための調整をする

以下のコマンドを実行するとこれらのすべてがインストールできます。

```
npm install --save-dev babel-core babel-loader babel-preset-es2015
```

webpack が JavaScript をどのようにバンドルかを確認するには JavaScript を含むように index.html を変更する必要があります。JavaScript ファイルは babel-loader によって生成され、babel-loader が ES2015 ファイルを JavaScript にコンパイルします。以下の script タグを index.html に追加してください。

```html
<script src="bundle.js" async></script>
```

そして app.js という単純な ES2015 ファイルを作ってください。

```javascript
console.log('hello world');
```

次に、app.js を bundle.js に変換する webpack を設定します。それには webpack.config.js ファイルに次のコードの追加が必要です。

```javascript
module.exports.push({
  entry: "./app.js",
  output: {
    filename: "bundle.js"
  },
  module: {
    loaders: [{
      test: /\.js$/,
      loader: 'babel-loader',
      query: {
        presets: ['es2015']
      }
    }]
  },
});
```

さあ、npm start を再び実行して localhost:8080 を開いてください。コンソールに「hello world」が確認できたでしょ！

### ステップ 4: コンポーネントに JavaScript を含める 

ES2015 から JavaScript にコンパイルするように webpack を設定したので、マテリアルデザインリップル用の ES2015 ファイルを入れてみましょう。まず、Node の依存関係をインストールします。

```
npm install @material/ripple
```

@material/ripple の ES2015 ファイルをインポートするように app.js に記述する必要があります。DOM 要素を使って MDCRipple を初期化することができます。以下のコードで「hello world」の app.js を置き換えてください。

```javascript
import {MDCRipple} from '@material/ripple';
const ripple = new MDCRipple(document.querySelector('.foo-button'));
```

さあ、npm start を再び実行して localhost:8080 を開いてください。ボタン上にマテリアルデザインリップルが確認できたでしょ！

![リップル付きボタン](button_with_ripple.png)

TODO: Write a getting started guide for our CDN users
