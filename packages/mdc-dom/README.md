<!--docs:
title: "DOM"
layout: detail
section: components
excerpt: "Provides commonly-used utilities for inspecting, traversing, and manipulating the DOM."
path: /catalog/dom/
-->

# DOM

MDC DOM は DOM の検査、解析、操作のための一般的に使用されるユーティリティを提供します。

多くの場合、`mdc-dom` を直接的に依存する必要はないでしょう。しかし、MDC Web のパターンにしたがい、MDC Web のエコシステムとエレガントに統合されたカスタムコンポーネントを作る際には、これは便利です。

## インストール

```
npm install @material/dom
```

## 基本的な使用法

```js
import * as ponyfill from '@material/dom/ponyfill';
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## Ponyfill 関数

`ponyfill` モジュールは以下の関数を提供しています。

関数 | 説明
--- | ---
`closest(element: Element, selector: string) => ?Element` | 与えられたセレクターにマッチする与えられた要素の祖先（与えられた要素がマッチするならそれ自身）を返す。
`matches(element: Element, selector: string) => boolean` | 与えられた要素が与えられた CSS セレクターにマッチするなら true を返す。
