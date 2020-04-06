<!--docs:
title: "Tab Scroller"
layout: detail
section: components
excerpt: "Allows for smooth native and animated scrolling of tabs."
iconId: tabs
path: /catalog/tabs/scroller/
-->

# Tab Scroller

Tab Scroller はスムーズなネイティブでアニメーションのあるタブのスクロールを可能にします。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-tabs#scrollable-tabs">マテリアルデザインガイドライン: スクロール可能なタブ</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/tabs">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/tab-scroller
```

## 基本的な使用法

### HTML 構造

```html
<div class="mdc-tab-scroller">
  <div class="mdc-tab-scroller__scroll-area">
    <div class="mdc-tab-scroller__scroll-content"></div>
  </div>
</div>
```

### スタイル

```scss
@use "@material/tab-scroller/mdc-tab-scroller";
```

### JavaScript のインスタンス化

```js
import {MDCTabScroller} from '@material/tab-scroller';

const tabScroller = new MDCTabScroller(document.querySelector('.mdc-tab-scroller'));
```

> JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-tab-scroller` | 必須。タブすクローラのコンテンツに設定する。
`mdc-tab-scroller__scroll-area` | 必須。スクロールする領域を示す。
`mdc-tab-scroller__scroll-content` | 必須。スクロールするコンテンツを示す。
`mdc-tab-scroller--align-start` | オプション。スクロールコンテンツ要素を先頭揃えにするためにスクロールコンテンツ要素の内側の要素に設定する。
`mdc-tab-scroller--align-end` | オプション。スクロールコンテンツ要素を末尾揃えにするためにスクロールコンテンツ要素の内側の要素に設定する。
`mdc-tab-scroller--align-center` | オプション。スクロールコンテンツ要素を中央揃えにするためにスクロールコンテンツ要素の内側の要素に設定する。

> _注意_: コンテンツがタブスクローラーやタブバーの幅に合わなかったり超える場合（つまり、最も一般的には `mdc-tab--min-width` がそれぞれのタブに使用されたとき）に限って、`align` 修飾クラスは適用できます。

### Sass ミキシン

ミキシン | 説明
--- | ---
`transition($duration-ms, $timing-function)` | スクロールアニメーションのデュレーションと、オプションで、タイミング関数を設定する。

## `MDCTabScroller` メソッド

メソッド | 説明
--- | ---
`scrollTo(scrollX: number) => void` | scrollX の値にスクロールする。
`incrementScroll(scrollX: number) => void` | 現在のスクロール値をアニメーションを使用して scrollX の値だけ増やす。
`incrementScrollImmediate(scrollX: number) => void` | 現在のスクロール値をアニメーションを使わずに scrollX の値だけ増やす。
`getScrollPosition() => number` | 現在の見た目のスクロール位置を返す。
`getScrollContentWidth() => number` | スクロールコンテンツ要素の幅を返す。

## Web フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のタブスクローラーを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCTabScrollerAdapter`

メソッド | 説明
--- | ---
`eventTargetMatchesSelector(eventTarget: EventTarget, selector: string) => boolean` | 与えられたイベントターゲットが与えられた CSS セレクターを満たしていれば `true` を返す。
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`addScrollAreaClass(className: string) => void` | スクロール領域要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`setScrollAreaStyleProperty(property: string, value: string) => void` | スクロール領域要素に与えられたスタイルプロパティを設定する。
`setScrollContentStyleProperty(property: string, value: string) => void` | スクロールコンテンツ要素に与えられたスタイルプロパティを設定する。
`getScrollContentStyleValue(property: string) => string` | スクロールコンテンツ要素の与えられたスタイルプロパティの値を返す。
`setScrollAreaScrollLeft(scrollLeft: number) => void` | スクロール領域要素の `scrollLeft` を設定する。
`getScrollAreaScrollLeft() => number` | スクロール領域要素の `scrollLeft` を返す。
`getScrollContentOffsetWidth() => number` | スクロールコンテンツ要素の `offsetWidth` を返す。
`getScrollAreaOffsetWidth() => number` | スクロール領域要素の `offsetWidth` を返す。
`computeScrollAreaClientRect() => ClientRect` | スクロール領域要素の包含された ClientRect を返す。
`computeScrollContentClientRect() => ClientRect` | スクロールコンテンツ要素の包含された ClientRect を返す。
`computeHorizontalScrollbarHeight() => number` | ブラウザの水平スクロールバーの高さを返す（px で）。

#### `util` 関数

MDC Tab Scroller はアダプターメソッドの実行を補助する関数を持つ `util` モジュールを提供しています。

関数 | 説明
--- | ---
`computeHorizontalScrollbarHeight(document: Document) => number` | ブラウザの水平スクロールバーの高さを返す（px で）。

### `MDCTabScrollerFoundation`

メソッド | 説明
--- | ---
`getRTLScroller() => MDCTabScrollerRTL` | 現在のブラウザ用の RTL スクローラーインスタンスを生成する。
`getScrollPosition() => number` | 現在の見た目上のスクロール位置を返す。
`handleInteraction() => void` | マウスやポインター、タッチ、キーボードイベントに応答する。
`handleTransitionEnd(evt: Event) => void` | `mdc-tab-scroller__scroll-content` 要素上の `transitionend` イベントに応答する。
`incrementScroll(scrollX: number) => void` | 現在のスクロール値を scrollX の値だけ増やす。
`scrollTo(scrollX: number) => void` | scrollX の値にスクロールする。

### `MDCTabScrollerRTL`

ブラウザに応じた3つの具象実装を伴う抽象クラスです。

* `MDCTabScrollerRTLDefault`
* `MDCTabScrollerRTLNegative`
* `MDCTabScrollerRTLReverse`

メソッド | 説明
--- | ---
`getAnimatingScrollPosition(scrollX: number, translateX: number) => number` | アニメーション中の現在のスクロール位置を返す。
`getScrollPositionRTL(translateX: number) => number` | ユーザーが水平スクロールした px 数を、先頭の縁からの相対的な値で返す。
`incrementScrollRTL(scrollX: number) => MDCTabScrollerAnimation` | 現在のスクロール位置から新しいスクロール位置へのアニメーションに必要な値を含むオブジェクトを返す。
`scrollToRTL(scrollX: number) => MDCTabScrollerAnimation` | RTL に対応した方法で与えられた位置までコンテンツを水平スクロールする。
