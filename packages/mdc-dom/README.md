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
`estimateScrollWidth(element: Element) => number`  | 表示されている場合は実際の視覚上の幅を返し、親要素が `display: none;` によって非表示となっている場合は推測して返す。

## イベント関数

外部のフレームワークとライブラリは以下のイベントユーティリティメソッドを使うことが可能です。

メソッド | 説明
--- | ---
`util.applyPassive(globalObj = window) => object` | 現在のブラウザがパッシブイベントリスナーをサポートしているか確認する

## フォーカストラップ

`FocusTrap` ユーティリティは与えられた要素内にフォーカスをとどめます。これはダイアログやモーダルドロワーのような MDC 内部コンポーネントからの仕様を目的としています。

メソッド | 説明
--- | ---
`trapFocus() => void` | フォーカスをルート要素内にとどめます。`initialFocusEl` が設定されているとそこにもフォーカスし、そうでなければ子要素の最初のフォーカス可能な要素にフォーカスします。
`releaseFocus() => void` | ルート要素からフォーカスを開放します。また、以前にフォーカスしていた要素にフォーカスを戻します。

## アナウンス

`announce` ユーティリティファイルには `aria-live` リージョンを通じてメッセージを通知するための単一のヘルパーメソッドが含まれます。これは MDC 内部コンポーネントからの使用を目的としています。

メソッド | 説明
--- | ---
`announce(message: string, priority?: AnnouncerPriority) => void` | 与えられた優先度（デフォルトは polite）で `aria-live` リージョンを通じてメッセージを通知する
<!-- TODO(b/148462294): Remove once only exported members are required in docs `say()` --> <!-- | --> <!-- DO NOT USE -->
