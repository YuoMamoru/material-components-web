<!--docs:
title: "Buttons"
layout: detail
section: components
excerpt: "Material Design-styled buttons."
iconId: button
path: /catalog/buttons/
-->

# Buttons

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/button">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/buttons.png" width="363" alt="Buttons screenshot">
  </a>
</div>-->

ボタンは一度タップすることにより、ユーザーにアクションを起こさせ、選択肢を生成します。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-buttons">マテリアルデザインガイドライン: ボタン</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/button">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/button
```

## 基本的な使用法

### HTML 構造

```html
<button class="mdc-button">
  Button
</button>
```

> <em>注意</em>: ここの例は一般的な `<button>` を使用していますが、`<a>` 要素に `mdc-button` を適用することができます。

### スタイル

```scss
@import "@material/button/mdc-button";
```

### JavaScript のインスタンス化

ボタンは JavaScript なしでも動作しますが、ルート要素上の `MDCRipple` をインスタンス化することによりリップルエフェクトをつけることができます。詳細は [MDC Ripple](../mdc-ripple) を参照してください。

```js
import {MDCRipple} from '@material/ripple';

const buttonRipple = new MDCRipple(document.querySelector('.mdc-button'));
```

> JavaScript をインポートするより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## 様々な使用法

### 囲まれたボタン

囲まれたボタンにするには、浮き上がっいる囲まれているボタンにするため `<button>` 要素に `mdc-button--raised` クラスを追加するか、画面の表面と同一平面上の囲まれているボタンにするために `mdc-button--unelevated` クラスを追加します。

### 枠線付きボタン

枠線付きボタンにするには、`<button>` 要素にクラス `mdc-button--outlined` を追加します。

### アイコン

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

To add an icon, add an element with the `mdc-button__icon` class inside the button element and set the attribute `aria-hidden="true"`. The icon is set to 18px to meet legibility requirements.
アイコンを追加するには、`mdc-button__icon` クラスをボタン要素の中に追加し、`aria-hidden="true"` 属性を設定します。アイコンは可視性が必要であるので 18px に設定します。

```html
<button class="mdc-button">
  <i class="material-icons mdc-button__icon" aria-hidden="true">favorite</i>
  Button
</button>
```

SVG アイコンを使うことも可能です。

```html
<button class="mdc-button">
  <svg class="mdc-button__icon" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" viewBox="...">
  ...
  </svg>
  Button
</button>
```

### 無効の状態

ボタンを無効にするには、`<button>` に直接 `disabled` 属性を追加するか、ボタンを含んでいる `<fieldset>` に `disabled` 属性を設定します。無効になったボタンは利用できなくなり、視覚的にも利用できるようなエフェクトがなくなります。

```html
<button class="mdc-button" disabled>
  Button
</button>
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-button` | 必須。デフォルトでは画面の表面と同一平面上にあるテキストボタン
`mdc-button--raised` | オプション。画面の表面から浮き上がったボタンにする
`mdc-button--unelevated` | オプション。画面の表面と同一平面上にあるボタンにする
`mdc-button--outlined` | オプション。画面の表面と同一平面上にあり、枠付きボタンにする
`mdc-button--dense` | オプション。ボタンのテキストとボタン自体を縮める
`mdc-button__icon` | オプション。アイコン要素であることを示す

### Sass ミキシン

ボタンの色やスタイルをカスタマイズする目的で以下のミキシンを使うことができます。

#### 基本的な Sass ミキシン

MDC Button はデフォルトで [MDC Theme](../mdc-theme) の `primary` カラーを使います。カスタマイズするには次のミキシンを使います。

ミキシン | 説明
--- | ---
`mdc-button-filled-accessible($container-fill-color)` | 囲まれた (_raised_ or _unelevated_) ボタンでの囲みの色を設定し、ボタンのインク、アイコン、リップルの色をアクセシビリティ標準に適合したものにします。

#### 高度な Sass ミキシン

これらのミキシンはコンテナやインク、境界線、リップルの色を上書きします。ボタンをアクセシビリティ標準に適合させることはあなたの責務になります。

ミキシン | 説明
--- | ---
`mdc-button-container-fill-color($color)` | 与えた色にコンテナの塗りの色を設定する
`mdc-button-icon-color($color)` | 与えられた色にアイコンの色を設定する
`mdc-button-ink-color($color)` | 与えた色にインクの色を設定し、`mdc-button-icon-color` を使わないときはアイコンの色も与えられた色にする
`mdc-button-shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にボタンを設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`mdc-button-horizontal-padding($padding)` | 与えた大きさに水平方向のパディングを設定する
`mdc-button-outline-color($color)` | 与えた色に境界の色を設定する
`mdc-button-outline-width($width, $padding)` | 与えた大きさ（デフォルトは 2px）に境界線の太さを設定し、適切なパディングに調整する。`$padding` は `mdc-button-horizontal-padding` に固有の値が設定されている場合に限り必須

#### 注意: Edge と CSS カスタムプロパティ

CSS カスタムプロパティを完全にサポートしているブラウザでは、引数として [MDC Theme](../mdc-theme) プロパティ（例えば `primary`）を与えても上記のミキシンは動作します。しかし、Edge は CSS カスタムプロパティを完全にサポートしていません。`mdc-button-container-fill-color` ミキシンを使うときは、Edge をサポートするためには実際の色を指定する必要があります。
