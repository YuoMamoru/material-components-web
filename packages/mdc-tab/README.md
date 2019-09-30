<!--docs:
title: "Tab"
layout: detail
section: components
excerpt: "Governs the visibility of one of several groups of content."
iconId: tabs
path: /catalog/tabs/tab/
-->

# Tab

タブは同階層にある関連つけられたコンテンツのグループ間の操作を構成、提供します。各タブは視覚的にコンテンツの一グループに束ねられます。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-tabs">マテリアルデザインガイドライン: タブ</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/tabs">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/tab
```

## 基本的な使用法

### HTML 構造

```html
<button class="mdc-tab" role="tab" aria-selected="false" tabindex="-1">
  <span class="mdc-tab__content">
    <span class="mdc-tab__icon material-icons" aria-hidden="true">favorite</span>
    <span class="mdc-tab__text-label">Favorites</span>
  </span>
  <span class="mdc-tab-indicator">
    <span class="mdc-tab-indicator__content mdc-tab-indicator__content--underline"></span>
  </span>
  <span class="mdc-tab__ripple"></span>
</button>
```

### スタイル

```scss
@import "@material/tab/mdc-tab";
```

### JavaScript のインストール

```js
import {MDCTab} from '@material/tab';

const tab = new MDCTab(document.querySelector('.mdc-tab'));
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## バリエーション

### アクティブなタブ

> *注意*: `mdc-tab-indicator` サブコンポーネントに `mdc-tab-indicator--active` クラスを追加することを忘れないでください。

```html
<button class="mdc-tab mdc-tab--active" role="tab" aria-selected="true">
  <span class="mdc-tab__content">
    <span class="mdc-tab__icon material-icons" aria-hidden="true">favorite</span>
    <span class="mdc-tab__text-label">Favorites</span>
  </span>
  <span class="mdc-tab-indicator mdc-tab-indicator--active">
    <span class="mdc-tab-indicator__content mdc-tab-indicator__content--underline"></span>
  </span>
  <span class="mdc-tab__ripple"></span>
</button>
```

### コンテンツのみにまたがるインジケーターを持つタブ

基本的な使い方の例では、タブのインジケーターはすべてのタブにまたがっていました。代わりに `mdc-tab__content` 要素の <em>中に</em> インジケーターを置けばタブインジケーターはタブのそのコンテンツにのみ設定することができます。

```html
<button class="mdc-tab" role="tab" aria-selected="false" tabindex="-1">
  <span class="mdc-tab__content">
    <span class="mdc-tab__icon material-icons" aria-hidden="true">favorite</span>
    <span class="mdc-tab__text-label">Favorites</span>
    <span class="mdc-tab-indicator">
      <span class="mdc-tab-indicator__content mdc-tab-indicator__content--underline"></span>
    </span>
  </span>
  <span class="mdc-tab__ripple"></span>
</button>
```

### タブアイコン

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-tab` | 必須。
`mdc-tab__content` | 必須。タブのアイコン、テキストラベル、タブインジケーターのコンテナ。
`mdc-tab__ripple` | 必須。タブのリップル面であることを示す。
`mdc-tab--active` | オプション。タブがアクティブであることを示す。
`mdc-tab--stacked` | オプション。タブのアイコントラベルが水平方向でなく垂直方向に表示されていることを示す。
`mdc-tab--min-width` | オプション。タブがテキストを折り返すことなくできるだけサイズが縮小されることを示す。
`mdc-tab__text-label` | オプション。タブのテキストラベルであることを示す。
`mdc-tab__icon` | オプション。タブの先頭のアイコンであることを示す。

### Sass ミキシン

タブの任意の場所の色を変更するには以下のミキシンを使用します。

ミキシン | 説明
--- | ---
`mdc-tab-text-label-color($color)` | タブのテキストラベルの色を変更する。
`mdc-tab-icon-color($color)` | タブのアイコンの色を変更する。
`mdc-tab-states-color($color)`| 基本状態の色を変更する。この色はホバー/フォーカス状態とリップルが起きた際に影響する。
`mdc-tab-ink-color($color)` | 文字ラベル、アイコン及び基本状態の色を変更する。
`mdc-tab-active-text-label-color($color)`  | アクティブなタブのテキストラベルの色を変更する。
`mdc-tab-active-icon-color($color)`  | アクティブなタブのアイコンの色を変更する。
`mdc-tab-active-states-color($color)`  | アクティブなタブの状態の色を変更する。
`mdc-tab-parent-positioning` | `MDCTab.computeDimensions()` がすべてのブラウザで同じ値になるように MDCTab の親要素の位置を設定する。
`mdc-tab-fixed-width($width)` | タブの幅を固定にする。タブが与えられた幅より小さくなることがなくなる。
`mdc-tab-horizontal-padding($padding)` | タブの水平方向のパディングを設定する。

## `MDCTab` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`id` | `string` | ルートのタブ要素の `id` 属性の値。
`active` | `boolean` (読取専用) | タブのアクティブな状態の取得する。
`focusOnActivate` | `boolean` (書込専用) | 有効にする際にタブが自身にフォーカスするかどうかを設定する。デフォルトは `true`。

メソッド | 説明
--- | ---
`activate(previousIndicatorClientRect?: ClientRect) => void` | インジケーターを有効にする。`previousIndicatorClientRect` はオプションの引数。
`deactivate() => void` | インジケーターを無効にする。
`focus() => void` | タブにフォーカスをあてる。
`computeIndicatorClientRect() => ClientRect` | インジケーターの境界のクライアントレクトを返す。
`computeDimensions() => MDCTabDimensions` | タブの寸法を返す。

イベント | イベントデータの構造 | 説明
--- | --- | ---
`MDCTab:interacted` | `{"detail": {"tabId": string}}` | アクティブであるかにかかわらず、タブが操作されたときに発生する。どのタブをアクティブにするかを知るために親コンポーネントが使用する。

## Web フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のタブを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCTabAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`hasClass(className: string) => boolean` | ルート要素が与えられたクラスを含んでいれば true を返す。
`setAttr(attr: string, value: string) => void` | ルート要素に与えられた値を属性として設定する。
`activateIndicator(previousIndicatorClientRect?: ClientRect) => void` | タブインジケーターサブコンポーネントを有効にする。`previousIndicatorClientRect` はオプション引数。
`deactivateIndicator() => void` | タブインジケーターサブコンポーネントを無効にする。
`getOffsetLeft() => number` | ルート要素の `offsetLeft` の値を返す。
`getOffsetWidth() => number` | ルート要素の `offsetWidth` の値を返す。
`getContentOffsetLeft() => number` | コンテンツ要素の `offsetLeft` の値を返す。
`getContentOffsetWidth() => number` | コンテンツ要素の `offsetWidth` の値を返す。
`notifyInteracted() => void` | `MDCTab:interacted` イベントを発生させる。
`focus() => void` | ルート要素にフォーカスをあてる。

### `MDCTabFoundation`

メソッド | 説明
--- | ---
`handleClick() => void` | `"click"` イベントのロジックをハンドリングする。
`isActive() => boolean` | タブがアクティブかどうかを返す。
`setFocusOnActivate(focusOnActivate: boolean) => void` | 有効にする際にタブが自身にフォーカスするかどうかを設定する。
`activate(previousIndicatorClientRect?: ClientRect) => void` | タブを有効にする。`previousIndicatorClientRect` はオプション引数。
`deactivate() => void` | タブを無効にする。
`computeDimensions() => MDCTabDimensions` | タブの寸法を返す。

### `MDCTabFoundation` イベントハンドラー

タブコンポーネントをラップする際には、以下のイベントハンドラーを登録する必要があります。この例としては [`MDCTab`](component.ts) コンポーネントの `initialSyncWithDOM` メソッドを参照してください。

イベント | 要素 | ファンデーションハンドラー
--- | --- | ---
`click` | ルート要素 | `handleClick()`
