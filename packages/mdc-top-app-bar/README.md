<!--docs:
title: "Top App Bar"
layout: detail
section: components
excerpt: "A container for items such as application title, navigation icon, and action items."
iconId: toolbar
path: /catalog/top-app-bar/
-->

# Top App Bar

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/top-app-bar">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/top-app-bar.png"
         width="494" alt="Top App Bar screenshot">
  </a>
</div>-->

MDC Top App Bar はアプリケーションタイトル、ナビゲーションアイコンや操作アイテムといったアイテムのコンテナとして振舞います。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-app-bar-top">Material Design guidelines: Top app bar</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/top-app-bar">Demo</a>
  </li>
</ul>

## インストール

```
npm install @material/top-app-bar
```

## 基本的な使用法

### HTML 構造

```html
<header class="mdc-top-app-bar">
  <div class="mdc-top-app-bar__row">
    <section class="mdc-top-app-bar__section mdc-top-app-bar__section--align-start">
      <a href="#" class="material-icons mdc-top-app-bar__navigation-icon">menu</a>
      <span class="mdc-top-app-bar__title">Title</span>
    </section>
  </div>
</header>
```

#### メニューアイコン

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

### スタイル

```scss
@import "@material/top-app-bar/mdc-top-app-bar";
```

### JavaScript のインストール

```js
import {MDCTopAppBar} from '@material/top-app-bar/index';

// インスタンス化
const topAppBarElement = document.querySelector('.mdc-top-app-bar');
const topAppBar = new MDCTopAppBar(topAppBarElement);
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## 様々な使用法

### 操作アイテムを伴う Top App Bar

トップアプリバーはナビゲーションアイコンの反対側に配置した操作アイテムを入れることができます。

```html
<header class="mdc-top-app-bar">
  <div class="mdc-top-app-bar__row">
    <section class="mdc-top-app-bar__section mdc-top-app-bar__section--align-start">
      <a href="#" class="material-icons mdc-top-app-bar__navigation-icon">menu</a>
      <span class="mdc-top-app-bar__title">Title</span>
    </section>
    <section class="mdc-top-app-bar__section mdc-top-app-bar__section--align-end" role="toolbar">
      <a href="#" class="material-icons mdc-top-app-bar__action-item" aria-label="Download">file_download</a>
      <a href="#" class="material-icons mdc-top-app-bar__action-item" aria-label="Print this page">print</a>
      <a href="#" class="material-icons mdc-top-app-bar__action-item" aria-label="Bookmark this page">bookmark</a>
    </section>
  </div>
</header>
```

### 短い Top App Bar

短いトップアプリバーはスクロール時にナビゲーションアイコン側に折りたたむことができるトップアプリバーです。

```html
<header class="mdc-top-app-bar mdc-top-app-bar--short">
  <div class="mdc-top-app-bar__row">
    <section class="mdc-top-app-bar__section mdc-top-app-bar__section--align-start">
      <a href="#" class="material-icons mdc-top-app-bar__navigation-icon">menu</a>
      <span class="mdc-top-app-bar__title">Title</span>
    </section>
    <section class="mdc-top-app-bar__section mdc-top-app-bar__section--align-end" role="toolbar">
      <a href="#" class="material-icons mdc-top-app-bar__action-item" aria-label="Bookmark this page">bookmark</a>
    </section>
  </div>
</header>
```

> 短いトップアプリバーは1つ以下の操作アイテムと共に使う必要があります。

### 常に折りたたまれている短い Top App Bar

コンポーネントをインスタンス化する前に `mdc-top-app-bar--short-collapsed` を適用すると常に折りたたまれて表示されるように設定することができます。

```html
<header class="mdc-top-app-bar mdc-top-app-bar--short mdc-top-app-bar--short-collapsed">
  ...
</header>
```

### 固定された Top App Bar

Fixed top app bars stay at the top of the page and elevate above the content when scrolled.
固定されたトップアプリバーはスクロール時にページの上部にとどまり、コンテンツの上に表示されます。

```html
<header class="mdc-top-app-bar mdc-top-app-bar--fixed">
  ...
</header>
```

### 目立つ Top App Bar

目立つトップアプリバーはより高さのあるものです。

```html
<header class="mdc-top-app-bar mdc-top-app-bar--prominent">
  ...
</header>
```

### 高密度の Top App Bar

高密度トップアプリバーはより高さのないものです。

```html
<header class="mdc-top-app-bar mdc-top-app-bar--dense">
  ...
</header>
```

## スタイルのカスタマイズ

### CSS クラス

クラス | 説明
--- | ---
`mdc-top-app-bar` | 必須。
`mdc-top-app-bar--fixed` | 固定されたトップアプリバーとしてトップアプリバーをスタイルするために使われるクラス。
`mdc-top-app-bar--fixed-adjust` | トップアプリバーがコンテンツを隠すことを防ぐために標準のトップアップバーおよび固定されたトップアプリバーの下のコンテンツをスタイルするのに使われるクラス。
`mdc-top-app-bar--prominent` | 目立つトップアプリバーとしてトップアプリバーをスタイルするために使われるクラス。
`mdc-top-app-bar--prominent-fixed-adjust` | トップアプリバーがコンテンツを隠すことを防ぐために目立つトップアプリバーの下のコンテンツをスタイルするのに使われるクラス。
`mdc-top-app-bar--dense` | 高密度トップアプリバーとしてトップアプリバーをスタイルするために使われるクラス。
`mdc-top-app-bar--dense-fixed-adjust` | トップアプリバーがコンテンツを隠すことを防ぐために高密度トップアプリバーの下のコンテンツをスタイルするのに使われるクラス。
`mdc-top-app-bar--dense-prominent-fixed-adjust` | トップアプリバーがコンテンツを隠すことを防ぐために、高密度と目立つの両方を指定したトップアプリバーの下のコンテンツをスタイルするのに使われるクラス。
`mdc-top-app-bar--short` | 短いトップアプリバーとしてトップアプリバーをスタイルするために使われるクラス。
`mdc-top-app-bar--short-collapsed` | 短いトップアプリバーが折りたたまれていることを表すのに使われるクラス。
`mdc-top-app-bar--short-fixed-adjust` | トップアプリバーがコンテンツを隠すことを防ぐために短いトップアプリバーの下のコンテンツをスタイルするのに使われるクラス。

### Sass ミキシン

ミキシン | 説明
--- | ---
`mdc-top-app-bar-ink-color($color)` | トップアプリバーのインク色を設定する。
`mdc-top-app-bar-icon-ink-color($color)` | トップアプリバーのアイコンのインク色を設定する。
`mdc-top-app-bar-fill-color($color)` | トップアプリバーの塗りの色を設定する。
`mdc-top-app-bar-fill-color-accessible($color)` | トップアプリバーの塗りの色を設定し、自動的にハイコントラストなインク色を設定する。
`mdc-top-app-bar-short-shape-radius($radius, $rtl-reflexive)` | 短いトップアプリバーの（折りたたまれているときの）角の丸みを指定した半径のサイズに設定する。RTL コンテキスト内で、半径の値をひっくり返すには `$rtl-reflexive` を true に設定する。デフォルトは true。

## `MDCTopAppBar` プロパティとメソッド

メソッド | 説明
--- | ---
`setScrollTarget(target: element) => void` | 異なる DOM ノード（デフォルトは window）にスクロールの対象を設定する。

### イベント

イベント | イベントデータの構造 | 説明
--- | --- | ---
`MDCTopAppBar:nav` | None | ナビゲーションアイコンがクリックされたときに発生する。

## Web フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のトップアプリバーを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCTopAppBarAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | コンポーネントのルート要素にクラスを追加する。
`removeClass(className: string) => void` | コンポーネントのルート要素からクラスを削除する。
`hasClass(className: string) => boolean` | コンポーネントのルート要素が与えられたクラス名を持つかどうかをチェックする。
`setStyle(property: string, value: string) => void` | ルート要素の指定した CSS プロパティに与えられた値を設定する。
`getTopAppBarHeight() => number` | トップアプリバーの高さをピクセルで取得する。
`getViewportScrollY() => number` | ページトップから body のコンテンツがスクロールしたピクセル数を取得する。
`getTotalActionItems() => number` | トップアプリバー上の操作アイテムの数を取得する。
`notifyNavigationIconClicked() => void` | ナビゲーションアイコンがクリックされたときにカスタムイベント `MDCTopAppBar:nav` を発生させる。
`registerNavigationIconInteractionHandler(evtType: string, handler: EventListener) => void` | ネイティブナビゲーションアイコン要素に与えられたイベントのイベントリスナーを登録する。
`deregisterNavigationIconInteractionHandler(evtType: string, handler: EventListener) => void` | ネイティブナビゲーションアイコン要素から与えられたイベントのイベントリスナーの登録を解除する。
`registerScrollHandler(handler: EventListener) => void` | ユーザーがスクロールさせた際に呼び出すハンドラーを登録する。デフォルトの実装では window の `scroll` イベントにリスナーとしてハンドラーを追加する。
`deregisterScrollHandler(handler: EventListener) => void` | ユーザーがスクロールさせた際に呼び出すハンドラーの登録を解除する。デフォルトの実装では window の `scroll` イベントにリスナーとして登録されたハンドラーを削除する。
`registerResizeHandler(handler: EventListener) => void` | 画面（もしくはそのビューポート）がリサイズされた際に呼び出すハンドラーを登録する。デフォルトの実装では window の `resize` イベントにリスナーとしてハンドラーを追加する。
`deregisterResizeHandler(handler: EventListener) => void` | 画面（もしくはそのビューポート）がリサイズされた際に呼び出すハンドラーの登録を解除する。デフォルトの実装では window の `resize` イベントにリスナーとして登録されたハンドラーを削除する。

### ファンデーション

#### `MDCTopAppBarBaseFoundation`、`MDCTopAppBarFoundation`、`MDCFixedTopAppBarFoundation` および `MDCShortTopAppBarFoundation`

すべてのファンデーションは以下のメソッドを提供します。

メソッド | 説明
--- | ---
`initScrollHandler(handler: EventListener) => void` | 指定したターゲット要素にスクロールハンドラーを登録する。
`destroyScrollHandler(handler: EventListener) => void` | ファンデーションにより設定された現在のスクロールハンドラの登録を解除する。

#### `MDCShortTopAppBarFoundation`

上で挙げたメソッドに加えて、短いトップアプリバーでは以下のパブリックプロパティが提供されています。

プロパティ | 値の型 | 説明
--- | --- | ---
`isCollapsed` | `boolean` (読取専用) | 短いトップアプリバーが折りたたまれた状態かどうかを示す。
