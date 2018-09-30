<!--docs:
title: "Importing JS Components"
navTitle: "Importing JS Components"
layout: landing
section: docs
path: /docs/importing-js/
-->

# JS コンポーネントのインポート

大半のコンポーネントは完全忠実なマテリアルデザインコンポーネントを提供するために使用される コンポーネント/ファンデーション クラスが付属しています。これまでどのようなテクノロジーを使ってきたかによって、JavaScript をインポートする方法はいくつかあります。

## ES2015

```js
import {MDCFoo, MDCFooFoundation} from '@material/foo';
```

互換性を最大化するために MDC Web のパッケージは `dist` 内のプリコンパイル済み UMD モジュールに対して `main` を指していることに注意してください。ビルドツールチェーンは `node_modules` 内の依存関係がすでに ES5 であると仮定しているため、トランスパイルの工程をスキップします。

ただし、構築されたアセットのサイズを小さくするために MDC Web のコード内でツリーシェイキングと依存関係の共有を利用するには、ES2015+ ソースを含むパッケージの `index.js` を明示的に参照することが必要です。

```js
import {MDCFoo, MDCFooFoundation} from '@material/foo/index';
```

この場合、ビルドツールチェインが MDC Web のモジュールと自分自身のモジュールを処理してトランスパイルするように構成されていることを確認する必要があります。 IE 11 をサポートするには、babel の[`transform-object-assign`](https://www.npmjs.com/package/babel-plugin-transform-object-assign) プラグインも含める必要があります。

環境設定の詳細については [Getting Started guide](getting-started.md) を参照してください。

## CommonJS

```js
const mdcFoo = require('mdc-foo');
const MDCFoo = mdcFoo.MDCFoo;
const MDCFooFoundation = mdcFoo.MDCFooFoundation;
```

## AMD

```js
require(['path/to/mdc-foo'], mdcFoo => {
  const MDCFoo = mdcFoo.MDCFoo;
  const MDCFooFoundation = mdcFoo.MDCFooFoundation;
});
```

## グローバル変数の使用

```js
const MDCFoo = mdc.foo.MDCFoo;
const MDCFooFoundation = mdc.foo.MDCFooFoundation;
```
