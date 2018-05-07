<!--docs:
title: "Floating Action Button"
layout: detail
section: components
excerpt: "A floating action button represents the primary action in an application"
iconId: button
path: /catalog/buttons/floating-action-buttons/
-->

# Floating Action Button

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/fab.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/fabs.png" width="78" alt="Floating action button screenshot">
  </a>
</div>-->

フローティング操作ボタンはアプリケーションの主要な操作を表すものです。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-fab">マテリアルデザインガイドライン: フローティング操作ボタン</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/fab.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/fab
```

## 基本的な使用法

### Material Icons のロード

私たちは Google Fonts から [Material Icons](https://material.io/icons/) を読み込むことを推奨しています。

```html
<head>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
```

### HTML 構造

```html
<button class="mdc-fab material-icons" aria-label="Favorite">
  <span class="mdc-fab__icon">
    favorite
  </span>
</button>
```

> _注意:_ フローティング操作ボタンには `span`、`i`、`img` もしくは `svg` 要素を使うことができます。

### スタイル

```scss
@import "@material/fab/mdc-fab";
```

### JavaScript のインスタンス化

FAB は JavaScript なしでも動作しますが、ルート要素上の `MDCRipple` をインスタンス化することによりリップルエフェクトをつけることができます。詳細は [MDC Ripple](../mdc-ripple) を参照してください。

```js
import {MDCRipple} from '@material/ripple';

const fabRipple = new MDCRipple(document.querySelector('.mdc-fab'));
```

> JavaScript をインポートするより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-fab` | 必須。ボタン要素用
`mdc-fab__icon` | 必須。アイコン要素用
`mdc-fab--mini` | オプション。FAB を小さいサイズにする
`mdc-fab--exited` | オプション。FAB をビューの外にアニメーションさせる。<br>このクラスが削除されると FAB がビューに戻ってくる。

> **`:disabled` に関する注釈**: FAB には無効なスタイルが定義されていません。FAB は操作を促すもので、無効な状態で表示すべきではありません。もし操作を行わない FAB を置きたいのであればユーザへの説明も書いておかなくてはなりません。

### Sass ミキシン

#### 基本的な Sass ミキシン

MDC FAB はデフォルトで [MDC Theme](../mdc-theme) の `secondary` カラーを使います。カスタマイズするには次のミキシンを使います。

ミキシン | 説明
--- | ---
`mdc-fab-accessible($container-color)` | FAB のコンテナの色を指定した色に変え、アクセシビリティ標準に沿うように FAB のインクとリップルの色を更新する。

#### 高度な Sass ミキシン

> **高度なミキシンに関する注釈**: 以下のミキシンは上級者向けです。これらのミキシンはコンテナやインク、リップルの色を上書きします。完全に FAB をカスタマイズしたいのであればこれらのすべてを使えます。もしくは、例えばリップルの色だけを変えたいのであれば、これらの一つだけを使うことも可能です。**一緒に使われるコンテナ、インク、リップルの色を選び、アクセシビリティ標準を満たすことはあなたの責務になります。**

ミキシン | 説明
--- | ---
`mdc-fab-container-color($color)` | 与えた色にコンテナの色を設定する
`mdc-fab-icon-size($width, $height)` |  `width` と `height` を指定することにより、アイコンの `width`、`height` と `font-size` プロパティを設定する。`$height` はオプションで省略した際には `$width` の値が設定される。`font-size` は `$width` の値に応じて設定される。
`mdc-fab-ink-color($color)` | 与えた色にインクの色を設定する


FAB コンポーネントのリップルエフェクトは [MDC Ripple](../mdc-ripple) のミキシンを使って設定されています。

### 注意: Edge と CSS 変数

CSS カスタムプロパティを完全にサポートしているブラウザでは、引数として [MDC Theme](../mdc-theme) プロパティ（例えば `primary`）を与えても上記のミキシンは動作します。しかし、Edge は CSS カスタムプロパティを完全にサポートしていません。`mdc-fab-container-color` ミキシンを使うときは、Edge をサポートするためには実際の色を指定する必要があります。

### 追加情報

#### 配置

必要に応じてアプリケーションのデザイン内に MDC FAB を配置しなくてはいけません。

```html
<!--
  ここでは FAB を右下の隅に配置している。
  デザインの要件に合わせて変更すること。
-->
<style>
.app-fab--absolute {
  position: fixed;
  bottom: 1rem;
  right: 1rem;
}

@media(min-width: 1024px) {
   .app-fab--absolute {
    bottom: 1.5rem;
    right: 1.5rem;
  }
}
</style>
<button class="mdc-fab material-icons app-fab--absolute" aria-label="Favorite">
  <span class="mdc-fab__icon">
    favorite
  </span>
</button>
```
