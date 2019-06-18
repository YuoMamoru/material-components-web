<!--docs:
title: "Tab Bar"
layout: detail
section: components
excerpt: "Manages a set of Tabs."
iconId: tabs
path: /catalog/tabs/tab-bar/
-->

# Tab Bar

タブを使うと関連した同じ階層のコンテンツのグループ間を移動できるようになります。Tab Bar には Tab Scroller と Tab コンポーネントが含まれています。

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
npm install @material/tab-bar
```

## 基本的な使用法

### HTML 構造

```html
<div class="mdc-tab-bar" role="tablist">
  <div class="mdc-tab-scroller">
    <div class="mdc-tab-scroller__scroll-area">
      <div class="mdc-tab-scroller__scroll-content">
        <button class="mdc-tab mdc-tab--active" role="tab" aria-selected="true" tabindex="0">
          <span class="mdc-tab__content">
            <span class="mdc-tab__icon material-icons" aria-hidden="true">favorite</span>
            <span class="mdc-tab__text-label">Favorites</span>
          </span>
          <span class="mdc-tab-indicator mdc-tab-indicator--active">
            <span class="mdc-tab-indicator__content mdc-tab-indicator__content--underline"></span>
          </span>
          <span class="mdc-tab__ripple"></span>
        </button>
      </div>
    </div>
  </div>
</div>
```

### スタイル

```scss
@import "@material/tab-bar/mdc-tab-bar";
@import "@material/tab-scroller/mdc-tab-scroller";
@import "@material/tab-indicator/mdc-tab-indicator";
@import "@material/tab/mdc-tab";
```

### JavaScript のインスタンス化

```js
import {MDCTabBar} from '@material/tab-bar';

const tabBar = new MDCTabBar(document.querySelector('.mdc-tab-bar'));
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## バリエーション

MDC Tab Bar にはバリエーションはありませんが、サブコンポーネントにはあります。より詳細な情報は [Tab Scroller](../mdc-tab-scroller) や [Tab](../mdc-tab)、[Tab Indicator](../mdc-tab-indicator) を参照してください。

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
`mdc-tab-bar` | 必須。

### Sass ミキシン

タブバーの幅を変更するには、以下のミキシンを使います。

ミキシン | 説明
--- | ---
`mdc-tab-bar-width($width)` | タブバーの幅を変更する。

## `MDCTabBar` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`focusOnActivate` | `boolean` (書込専用) | 有効になった際にタブにフォーカスを合わせるかどうかを設定する。デフォルトは `true`。
`useAutomaticActivation` | `boolean` (書込専用) | キーボード操作に対してタブがどのように有効になるかを設定する。自動 (`true`) では方向キーでフォーカスされたらすぐに有効になり、手動 (`false`) ではユーザーがスペースキーかエンターキーを押したときにだけ有効になる。デフォルトは自動 (`true`)。

メソッド | 説明
--- | ---
`activateTab(index: number) => void` | 与えられたインデックスのタブを有効にする。
`scrollIntoView(index: number) => void` | 与えられたインデックスのタブが見える位置にスクロールする。

イベント | イベントデータの構造 | Description
--- | --- | ---
`MDCTabBar:activated` | `{"detail": {"index": number}}` | アクティブなタブのインデックスの位置が有効になった際に発生する。タブが有効になったときにコンテンツを更新するために使用する。

## Web フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のタブバーを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCTabBarAdapter`

メソッド | 説明
--- | ---
`scrollTo(scrollX: number) => void` | 与えられた位置にタブスクローラーをスクロールする。
`incrementScroll(scrollXIncrement: number) => void` | タブスクローラーを与えられた値だけ増やす。
`getScrollPosition() => number` | タブスクローラーのスクロール位置を返す。
`getScrollContentWidth() => number` | タブスクローラーのスクロールコンテンツ要素の幅を返す。
`getOffsetWidth() => number` | ルート要素の offsetWidth を返す。
`isRTL() => boolean` | テキストの方向が RTL であるかどうかを返す。
`setActiveTab(index: number) => void` | 与えられたインデックスのタブを有効にする。
`activateTabAtIndex(index: number, clientRect: ClientRect) => void` | 与えられた clientRect 内にある与えられたインデックスのタブを有効にする。
`deactivateTabAtIndex(index) => void` | 与えられたインデックスのタブを有効でないようにする。
`focusTabAtIndex(index: number) => void` | 与えられたインデックスのタブにフォーカスを移動する。
`getTabIndicatorClientRectAtIndex(index: number) => ClientRect` | 与えられたインデックスのタブの ClientRect を返す。
`getTabDimensionsAtIndex(index) => MDCTabDimensions` | 与えられたインデックスのタブの大きさを返す。
`getTabListLength() => number` | タブコンポーネントの子の数を返す。
`getPreviousActiveTabIndex() => number` | 有効なタブの一つ前のタブのインデックスを返す。
`getFocusedTabIndex() => number` | フォーカスされたタブのインデックスを返す。
`getIndexOfTabById(id: string) => number` | 与えられたタブ ID のインデックスを返す。
`notifyTabActivated(index: number) => void` | `MDCTabBar:activated` イベントを発生させる。

### `MDCTabBarFoundation`

メソッド | 説明
--- | ---
`activateTab(index: number) => void` | 与えられたインデックスのタブを有効にする。
`setUseAutomaticActivation(useAutomaticActivation: boolean) => void` | キーボード操作に対してタブがどのように有効になるかを設定する。自動 (`true`) では方向キーでフォーカスされたらすぐに有効になり、手動 (`false`) ではユーザーがスペースキーかエンターキーを押したときにだけ有効になる。
`handleKeyDown(evt: Event) => void` | `"keydown"` イベントの動作をハンドリングする。
`handleTabInteraction(evt: Event) => void` | `"MDCTab:interacted"` イベントの動作をハンドリングする。
`scrollIntoView(index: number) => void` | 与えられたインデックスのタブが見える位置にスクロールする。
