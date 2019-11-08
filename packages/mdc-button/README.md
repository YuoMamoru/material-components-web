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
  <div class="mdc-button__ripple"></div>
  <span class="mdc-button__label">Button</span>
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

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## バリエーション

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

アイコンを追加するには、`mdc-button__icon` クラスをボタン要素の中に追加し、`aria-hidden="true"` 属性を設定します。アイコンは可視性が必要であるので 18px に設定します。

```html
<button class="mdc-button">
  <div class="mdc-button__ripple"></div>
  <i class="material-icons mdc-button__icon" aria-hidden="true">favorite</i>
  <span class="mdc-button__label">Button</span>
</button>
```

SVG アイコンを使うことも可能です。

```html
<button class="mdc-button">
  <div class="mdc-button__ripple"></div>
  <svg class="mdc-button__icon" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" viewBox="...">
  ...
  </svg>
  <span class="mdc-button__label">Button</span>
</button>
```

#### 後置アイコン

一部のアイコンはボタンのテキストラベルの前にあるよりも後ろにあるほうがより分かりやすくなります。アイコンのマークアップを `mdc-button__label` 要素の <em>後ろ</em> に置くことによって実現できます。

```html
<button class="mdc-button">
  <div class="mdc-button__ripple"></div>
  <span class="mdc-button__label">Button</span>
  <i class="material-icons mdc-button__icon" aria-hidden="true">favorite</i>
</button>
```

> <em>注意</em>: `mdc-button__label` 要素は後置アイコンが適切にスタイルされるためには <em>必須</em> です。

### 無効の状態

ボタンを無効にするには、`<button>` に直接 `disabled` 属性を追加するか、ボタンを含んでいる `<fieldset>` に `disabled` 属性を設定します。無効になったボタンは利用できなくなり、視覚的にも利用できるようなエフェクトがなくなります。

```html
<button class="mdc-button" disabled>
  <div class="mdc-button__ripple"></div>
  <span class="mdc-button__label">Button</span>
</button>
```

## 追加情報

### アクセシビリティ

マテリアルデザイン仕様ではタッチの対象は少なくとも  48 x 48 px にすることを勧めています。この要件を満たすためにボタンに以下のものを追加してください。

```html
<div class="mdc-touch-target-wrapper">
  <button class="mdc-button mdc-button--touch">
    <div class="mdc-button__ripple"></div>
    <span class="mdc-button__label">My Accessible Button</span>
    <div class="mdc-button__touch"></div>
  </button>
</div>
```

隣接している要素において、潜在的に（マージンを縮小するために）タッチ対象が重なってしまうのを避けたい場合は、外側に `mdc-touch-target-wrapper` 要素だけが必要なことに注意してください。

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-button` | 必須。デフォルトでは画面の表面と同一平面上にあるテキストボタン。
`mdc-button__ripple` | 必須。リップルスタイルで表示される要素であることを示す。
`mdc-button--raised` | オプション。画面の表面から浮き上がったボタンにする。
`mdc-button--unelevated` | オプション。画面の表面と同一平面上にあるボタンにする。
`mdc-button--outlined` | オプション。画面の表面と同一平面上にあり、枠付きボタンにする。
`mdc-button__label` | 推奨\*。ボタンのテキストラベルを含む要素であることを示す。
`mdc-button__icon` | オプション。ボタンのアイコンを含む要素であることを示す。

> \*<em>注意</em>: `mdc-button__label` 要素は後置アイコンのあるボタンでは必須ですが、現状ではアイコンのないボタンや前置アイコンのボタンではオプションです。後者の場合、テキストラベルは単に直接 `mdc-button` 要素の中にあってもかまいません。しかし、`mdc-button__label` クラスは今後すべての場合で必須となるかもしれないので、今後のために常に含めることを推奨します。

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
`mdc-button-container-fill-color($color)` | 有効なボタンにおいて与えた色にコンテナの塗りの色を設定する。
`mdc-button-disabled-container-fill-color($color)` | 無効なボタンにおいて与えた色にコンテナの塗りの色を設定する。
`mdc-button-icon-color($color)` | 有効なボタンにおいて与えられた色にアイコンの色を設定する。
`mdc-button-disabled-icon-color($color)` | 無効なボタンにおいて与えられた色にアイコンの色を設定する。
`mdc-button-ink-color($color)` | 有効なボタンにおいて与えた色にインクの色を設定し、`mdc-button-icon-color` を使わないときはアイコンの色も与えられた色にする。
`mdc-button-disabled-ink-color($color)` |  無効なボタンにおいて与えた色にインクの色を設定し、`mdc-button-icon-color` を使わないときはアイコンの色も与えられた色にする。
`mdc-button-density($density-scale)` | ボタンの密度スケールを設定する。サポートしている密度スケール値は (`-3`, `-2`, `-1`, `0`)。
`mdc-button-height($height)` | ボタンのカスタムの高さを設定する。
`mdc-button-shape-radius($radius, $density-scale, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にボタンを設定する。`$density-scale` は `$radius` 値がパーセント単位のときのみ必須で、デフォルトは `$mdc-button-density-default-scale`。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`mdc-button-horizontal-padding($padding)` | 与えた大きさに水平方向のパディングを設定する。
`mdc-button-outline-color($color)` | 有効なボタンにおいて与えた色に境界の色を設定する。
`mdc-button-disabled-outline-color($color)` | 無効なボタンにおいて与えた色に境界の色を設定する。
`mdc-button-outline-width($width, $padding)` | 与えた大きさ（デフォルトは 2px）に境界線の太さを設定し、適切なパディングに調整する。`$padding` は `mdc-button-horizontal-padding` に固有の値が設定されている場合に限り必須。

#### 注意: Edge と CSS カスタムプロパティ

CSS カスタムプロパティを完全にサポートしているブラウザでは、引数として [MDC Theme](../mdc-theme) プロパティ（例えば `primary`）を与えても上記のミキシンは動作します。しかし、Edge は CSS カスタムプロパティを完全にサポートしていません。`mdc-button-container-fill-color` ミキシンを使うときは、Edge をサポートするためには実際の色を指定する必要があります。
