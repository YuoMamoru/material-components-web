<!--docs:
title: "Importing JS Components"
navTitle: "Importing JS Components"
layout: landing
section: docs
path: /docs/importing-js/
-->

# JS コンポーネントのインポート

大半のコンポーネントは完全忠実なマテリアルデザインコンポーネントを提供するために使用される コンポーネント/ファンデーション クラスが付属しています。これまでどのようなテクノロジーを使ってきたかによって、JavaScript をインポートする方法はいくつかあります。

### ES モジュール

```js
import {MDCFoo, MDCFooFoundation} from '@material/foo';
```

互換性を最大化するために MDC Web のパッケージは `dist` 内のプリコンパイル済み UMD モジュールに対して `main` を指していることに注意してください。ビルドツールチェーンは `node_modules` 内の依存関係がすでに ES5 であると仮定しているため、トランスパイルの工程をスキップします。

ただし、構築されたアセットのサイズを小さくするために MDC Web のコード内でツリーシェイキングと依存関係の共有を利用するには、パッケージの `index.js` を明示的に参照することが必要です。

```js
import {MDCFoo, MDCFooFoundation} from '@material/foo/index';
```

あるビルドツールは `package.json` の [`module`](https://github.com/rollup/rollup/wiki/pkg.module) プロパティを検出します。それは ES モジュールを指し、そうでない場合は ES5 構文のみを含めます。[Webpack](https://webpack.js.org/) や [Rollup](https://rollupjs.org/guide/en) を使っているのなら、`/index` を直接参照する必要はなく、インポートパス構文により短い `@material/foo` を使い続けることができます。

この場合には、ビルドツールチェーンにあなた自身のモジュールと同様に MDC Web のモジュールも設定されていることを確認しなくてはなりません。

環境設定の詳細については [Getting Started guide](getting-started.md) を参照してください。

#### TypeScript

TypeScript を使っているのであれば、MDC Web のパッケージは `.d.ts` ファイルもインクルードします。ほとんどの場合、TypeScript のコンパイラは `package.json` から見つけた `types` プロパティを通じて自動的にこれらのファイルを見つけるため、明示的に参照する必要はないはずです。それぞれの UMD モジュールにマッピングされた `dist` ディレクトリの下に `.d.ts` はあります。パッケージ内に各 foundation/component/adapter 等に対応する `.d.ts` ファイルがあります。

> 注意: 私たちは故意に `.ts` ソースファイルを省いています。これは `.d.ts` ファイルとトランスパイルされた `.js`（UMD もしくは ES モジュールフォーマット）は広く使われているからです。

### CommonJS

```js
const mdcFoo = require('mdc-foo');
const MDCFoo = mdcFoo.MDCFoo;
const MDCFooFoundation = mdcFoo.MDCFooFoundation;
```

### AMD

```js
require(['path/to/mdc-foo'], mdcFoo => {
  const MDCFoo = mdcFoo.MDCFoo;
  const MDCFooFoundation = mdcFoo.MDCFooFoundation;
});
```

### グローバル変数の使用

```js
const MDCFoo = mdc.foo.MDCFoo;
const MDCFooFoundation = mdc.foo.MDCFooFoundation;
```

## CSS セレクタークエリによるコンポーネントのインスタンス化

MDC Web のドキュメントの多く例ではページ内の単一の要素のコンポーネントインスタンスを生成する方法が説明されています。

```js
const foo = new MDCFoo(document.querySelector('.mdc-foo'));
```

これはページ全体で関心のある要素が一つだけであることを前提にしています。なぜなら、 `document.querySelector` は常に最大で一つの要素（見つけた最初のもの）しか返さないからです。

一度に **複数** の要素のコンポーネントをインスタンス化するには `querySelectorAll` を使います。

```js
const foos = [].map.call(document.querySelectorAll('.mdc-foo'), function(el) {
  return new MDCFoo(el);
});
```
