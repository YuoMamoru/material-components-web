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
  <div class="mdc-tab__content">
    <span class="mdc-tab__icon">heart</span>
    <span class="mdc-tab__text-label">Favorites</span>
  </div>
  <span class="mdc-tab-indicator">
    <span class="mdc-tab-indicator__content mdc-tab-indicator__content--underline"></span>
  </span>
  <div class="mdc-tab__ripple"></div>
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

> JavaScript をインポートするより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## 様々な使用法

### アクティブなタブ

> *注意*: `mdc-tab-indicator` サブコンポーネントに `mdc-tab-indicator--active` クラスを追加することを忘れないでください。

```html
<button class="mdc-tab mdc-tab--active" role="tab" aria-selected="true">
  <div class="mdc-tab__content">
    <span class="mdc-tab__icon">heart</div>
    <span class="mdc-tab__text-label">Favorites</div>
  </div>
  <span class="mdc-tab-indicator mdc-tab-indicator--active">
    <span class="mdc-tab-indicator__content mdc-tab-indicator__content--underline"></span>
  </span>
  <div class="mdc-tab__ripple"></div>
</button>
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-tab` | 必須。
`mdc-tab__content` | 必須。タブのテキストラベルであることを示す。
`mdc-tab__ripple` | 必須。タブのリップル面であることを示す。
`mdc-tab--active` | オプション。タブがアクティブであることを示す。
`mdc-tab--stacked` | オプション。タブのアイコントラベルが水平方向でなく垂直方向に表示されていることを示す。
`mdc-tab--min-width` | オプション。タブがテキストを折り返すことなくできるだけサイズが縮小されることを示す。
`mdc-tab__text-label` | オプション。タブ内のアイコンであることを示す。
`mdc-tab__icon` | オプション。タブの先頭のアイコンであることを示す。

### Sass ミキシン

タブの任意の場所の色を変更するには以下のミキシンを使用します。

ミキシン | 説明
--- | ---
`mdc-tab-text-label-color($color)` | タブのテキストラベルの色を変更する。
`mdc-tab-icon-color($color)` | タブのアイコンの色を変更する。
`mdc-tab-parent-positioning` | `MDCTab.computeDimensions()` がすべてのブラウザで同じ値になるように MDCTab の親要素の位置を設定する。
`mdc-tab-fixed-width($width)` | タブの幅を固定にする。タブが与えられた幅より小さくなることがなくなる。

## `MDCTab` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`active` | `boolean` | タブのアクティブな状態の取得する。

メソッド | 説明
--- | ---
`activate(previousIndicatorClientRect: ClientRect=) => void` | インジケーターを有効にする。`previousIndicatorClientRect` はオプションの引数。
`deactivate() => void` | インジケーターを無効にする。
`computeIndicatorClientRect() => ClientRect` | インジケータの境界のクライアントレクトを返す。
`computeDimensions() => MDCTabDimensions` | タブの寸法を返す。

イベント | イベントのデータ構造 | 説明
--- | --- | ---
`MDCTab:interacted` | `{"detail": {"tab": MDCTab}}` | アクティブであるかにかかわらず、タブが操作されたときに発生する。どのタブをアクティブにするかを知るために親コンポーネントが使用する。

## Web フレームワーク内での使用

React や Angular といった JavaScript フレームワークを使用しているなら、フレームワークのためのスイッチを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> か <em>高度な方法: ファンデーションアダプタを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) の説明に沿ってみてください。

### `MDCTabAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`hasClass(className: string) => boolean` | ルート要素が与えられたクラスを含んでいれば true を返す。
`registerEventHandler(evtType: string, handler: EventListener) => void` | ルート要素にイベントリスナーを登録する。
`deregisterEventHandler(evtType: string, handler: EventListener) => void` | ルート要素からイベントリスナーの登録を解除する。
`setAttr(attr: string, value: string) => void` | ルート要素に与えられた値を属性として設定する。
`activateIndicator(previousIndicatorClientRect: ClientRect=) => void` | タブインジケータサブコンポーネントを有効にする。`previousIndicatorClientRect` はオプション引数。
`deactivateIndicator() => void` | タブインジケータサブコンポーネントを無効にする。
`computeIndicatorClientRect() => ClientRect` | タブインジケータサブコンポーネントのコンテンツ境界のクライアントレクトを返す。
`getOffsetLeft() => number` | ルート要素の `offsetLeft` の値を返す。
`getOffsetWidth() => number` | ルート要素の `offsetWidth` の値を返す。
`getContentOffsetLeft() => number` | コンテンツ要素の `offsetLeft` の値を返す。
`getContentOffsetWidth() => number` | コンテンツ要素の `offsetWidth` の値を返す。
`notifyInteracted() => void` | `MDCTab:interacted` イベントを発生させる。
`focus() => void` | ルート要素にフォーカスをあてる。

### `MDCTabFoundation`

メソッド | 説明
--- | ---
`handleTransitionEnd(evt: Event) => void` | `"transitionend"` イベントのためのロジックを制御する。
`handleClick() => void` | `"click"` イベントのロジックをハンドリングする。
`isActive() => boolean` | タブがアクティブかどうかを返す。
`activate(previousIndicatorClientRect: ClientRect=) => void` | タブを有効にする。`previousIndicatorClientRect` はオプション引数。
`deactivate() => void` | タブを無効にする。
`computeIndicatorClientRect() => ClientRect` | タブインジケータサブコンポーネントのコンテンツ境界のクライアントレクトを返す。
`computeDimensions() => MDCTabDimensions` | タブの寸法を返す。
