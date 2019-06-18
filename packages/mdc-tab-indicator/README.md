<!--docs:
title: "Tab Indicator"
layout: detail
section: components
excerpt: "A visual guide that shows which Tab is active."
iconId: tabs
path: /catalog/tabs/indicator/
-->

# Tab Indicator

タブインジケーターはどのタブがアクティブであるかを示す視覚上のガイドです。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-tabs#anatomy">マテリアルデザインガイドライン: タブの構造</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/tabs">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/tab-indicator
```

## 基本的な使用法

### HTML 構造

```html
<span class="mdc-tab-indicator">
  <span class="mdc-tab-indicator__content"></span>
</span>
```

### スタイル

```scss
@import "@material/tab-indicator/mdc-tab-indicator";
```

### JavaScript のインスタンス化

```js
import {MDCTabIndicator} from '@material/tab-indicator';

const tabIndicator = new MDCTabIndicator(document.querySelector('.mdc-tab-indicator'));
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## バリエーション

### アクティブインジケーター

タブインジケーターをアクティブにするには `mdc-tab-indicator` 要素に `mdc-tab-indicator--active` クラスを追加します。

### インジケーターの種類と推移

タブインジケーターは2つの方法のいずれかで表すことができます。

* 下線、`mdc-tab-indicator__content--underline` クラスによって表される
* アイコン、`mdc-tab-indicator__content--icon` クラスによって表される

> <em>注意</em>: これらのクラスのうち1つはタブインジケーターコンテンツ要素に<em>適用しなくてはなりません</em>。

タブインジケーターは2つの方法のいずれかで推移することができます。

* スライド、デフォルトの動作
* フェード、`mdc-tab-indicator--fade` クラスによって表される

#### スライドする下線インジケーター

```html
<span class="mdc-tab-indicator">
  <span class="mdc-tab-indicator__content mdc-tab-indicator__content--underline"></span>
</span>
```

#### アイコンインジケーター

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

タブ上では `aria-selected` 属性を通じてすでにアクティブインジケーターが示されているため、`aria-hidden="true"` を付けることを忘れないでください。

##### フェードするアイコンインジケーター

```html
<span class="mdc-tab-indicator mdc-tab-indicator--fade">
  <span class="mdc-tab-indicator__content mdc-tab-indicator__content--icon material-icons" aria-hidden="true">star</span>
</span>
```

##### スライドするアイコンインジケーター

```html
<span class="mdc-tab-indicator">
  <span class="mdc-tab-indicator__content mdc-tab-indicator__content--icon material-icons" aria-hidden="true">star</span>
</span>
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-tab-indicator` | 必須。タブインジケーターコンテンツに付ける。
`mdc-tab-indicator__content` | 必須。タブインジケーターコンテンツであることを示す。
`mdc-tab-indicator--active` | オプション。インジケーターを視覚上アクティブにする。
`mdc-tab-indicator--fade` | オプション。タブインジケーターをアクティブにするときにはフェードイン、アクティブでなくするときはフェードアウトするように設定する。
`mdc-tab-indicator__content--underline` | オプション。下線タブインジケーターであることを示す。
`mdc-tab-indicator__content--icon` | オプション。アイコンタブインジケーターであることを示す。

> *注意*: `--underline` か `--icon` のいずれか一方のコンテンツ修飾クラスがなくてはなりません。

### Sass ミキシン

タブインジケーターを変更するには、以下のミキシンを使います。

ミキシン | 説明
--- | ---
`mdc-tab-indicator-surface` | 必須。`mdc-tab-indicator` の親要素に適用しなくてはならない。
`mdc-tab-indicator-underline-color($color)` | 下線の色を変更する。
`mdc-tab-indicator-icon-color($color)` | アイコンサブ要素の色を変更する。
`mdc-tab-indicator-underline-height($height)` | 下線の高さを変更する。
`mdc-tab-indicator-icon-height($height)` | アイコンサブ要素の高さを変更する。
`mdc-tab-indicator-underline-top-corner-radius($radius)` | 下線子要素の左上と右上の角丸の半径を変更する。

## `MDCTabIndicator` メソッド

メソッド | 説明
--- | ---
`activate(previousIndicatorClientRect?: ClientRect) => void` | タブインジケーターをアクティブにする。
`deactivate() => void` | タブインジケーターをアクティブでなくする。
`computeContentClientRect() => ClientRect` | コンテンツ要素の ClientRect を返す。

## Web フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のタブインジケーターを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCTabIndicatorAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`setContentStyleProperty(property: string, value: string) => void` | コンテンツ要素のスタイルプロパティを設定する。
`computeContentClientRect() => ClientRect` | コンテンツ要素の ClientRect を返す。

### `MDCTabIndicatorFoundation`

メソッド | 説明
--- | ---
`handleTransitionEnd(evt: Event) => void` | ルート要素の `"transitionend"` イベントのための処理をハンドリングする。
`activate(previousIndicatorClientRect?: ClientRect) => void` | タブインジケーターをアクティブにする。
`deactivate() => void` | タブインジケーターをアクティブでなくする。
`computeContentClientRect() => ClientRect` | コンテンツ要素の ClientRect を返す。
