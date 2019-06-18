<!--docs:
title: "Icon Buttons"
layout: detail
section: components
iconId: button
path: /catalog/buttons/icon-buttons/
-->

# Icon Buttons

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/icon-button">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/icon-toggles.png" width="20" alt="Icon buttons screenshot">
  </a>
</div>-->

アイコンボタンは一回のタップでユーザーに操作を実行させたり選択させたりすることができます。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-buttons#toggle-button">マテリアルデザインガイドライン: 切り替えボタン</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/icon-button">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/icon-button
```

## 使用法

### HTML 構造

```html
<button class="mdc-icon-button material-icons">favorite</button>
```

> 注意: MDC Icon Button では `<button>` タグと `<a>` タグを使うことができます。

> 注意: IE11 ではアイコンのテキストの後に改行かスペースがあるとアイコンを正しく中央揃えにしません。

### スタイル

```scss
@import "@material/icon-button/mdc-icon-button";
```

### JavaScript のインストール

アイコンボタンは JavaScript なしでも動作しますが、ルート要素に `MDCRipple` をインスタンス化することによりリップル効果を持つように拡張できます。詳細は [MDC Ripple](../mdc-ripple) を参照してください。

```js
import {MDCRipple} from '@material/ripple';

const iconButtonRipple = new MDCRipple(document.querySelector('.mdc-icon-button'));
iconButtonRipple.unbounded = true;
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## バリエーション

### 切り替えアイコンボタン

アイコンボタンはオンとオフのアイコンを切り替えるために使用することができます。切り替えアイコンボタンとしてアイコンボタンを表示するには、オンオフ両方のアイコンを子要素として追加し、オン要素を表すアイコンに `mdc-icon-button__icon--on` クラスを設定します。「オン」の状態で初期化するなら親要素である `button` に `mdc-icon-button--on` を追加します。そしてルート要素に `MDCIconButtonToggle` をインスタンス化します。

```html
<button id="add-to-favorites"
   class="mdc-icon-button"
   aria-label="Add to favorites"
   aria-hidden="true"
   aria-pressed="false">
   <i class="material-icons mdc-icon-button__icon mdc-icon-button__icon--on">favorite</i>
   <i class="material-icons mdc-icon-button__icon">favorite_border</i>
</button>
```

```js
var toggleButton = new mdc.iconButton.MDCIconButtonToggle(document.getElementById('add-to-favorites'));
```

#### SVG を使った切り替えアイコンボタン

アイコン切り替えボタンでは SVG を使うことができます。

```html
<button id="star-this-item"
   class="mdc-icon-button mdc-icon-button--on"
   aria-label="Unstar this item"
   aria-hidden="true"
   aria-pressed="true">
   <svg class="mdc-icon-button__icon">
     ...
   </svg>
   <svg class="mdc-icon-button__icon mdc-icon-button__icon--on">
     ...
  </svg>
</button>
```

#### 画像を使った切り替えアイコンボタン

アイコン切り替えボタンでは `img` タグを使うことができます。

```html
<button id="star-this-item"
   class="mdc-icon-button mdc-icon-button--on"
   aria-label="Unstar this item"
   aria-hidden="true"
   aria-pressed="true">
   <img src="" class="mdc-icon-button__icon"/>
   <img src="" class="mdc-icon-button__icon mdc-icon-button__icon--on"/>
</button>
```

### アイコン

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

### 無効の状態

アイコンを無効にするには `<button>` 要素に直接 `disabled` 属性を追加します。`<a>` タグを使ったアイコンボタンは無効にはできません。無効になったボタンは利用できなくなり、視覚的にも利用できるようなエフェクトがなくなります。

```html
<button class="mdc-icon-button material-icons" disabled>favorite</button>
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-icon-button` | 必須。
`mdc-icon-button--on` | このクラスはルート要素に設定し、切り替えアイコンボタンを「オン」の状態であるかどうかを示すために使われる。
`mdc-icon-button__icon` | このクラスはアイコン切り替えボタンの各アイコン要素に設定する。
`mdc-icon-button__icon--on` | このクラスはアイコン要素に設定し、「オン」の状態を表す切り替えボタンのアイコンであることを示すために使われる。

### Sass ミキシン

アイコンボタンの色やプロパティをカスタマイズするために、以下のミキシンを使うことができます。

ミキシン | 説明
--- | ---
`mdc-icon-button-size($width, $height, $padding)` | アイコンとリップルの幅、高さ、フォントサイズ、そしてパディングを設定する。`$height` はオプションで、デフォルトでは  `$width` の値が使われる。`$padding` もオプションで、デフォルトでは `max($width, $height)/2` になる。`font-size` には `max($width, $height)` が設定される。
`mdc-icon-button-ink-color($color)` | フォント色とリップルの色を指定した色に設定する。

## `MDCIconButtonToggle` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`on` | Boolean | 切り替え状態を指定した `isOn` の値に設定する。

### イベント

イベント | イベントデータの構造 | 説明
--- | --- | ---
`MDCIconButtonToggle:change` | `{"detail": {"isOn": boolean}}` | アイコンが切り換えられた時に発生する。

## Web フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用の切り替えアイコンボタンを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCIconButtonToggleAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`hasClass(className: string) => boolean` | ルート要素が与えられた CSS クラス名を持っているかどうかを調べる。
`setAttr(name: string, value: string) => void` | ルート要素の属性 `name` に `value` を設定する。
`notifyChange(evtData: {isOn: boolean}) => void` | 変更通知を行い、`evtData` を環境のイベントハンドリングシステムに渡す。素の実装ではカスタムイベントはこれを利用している。

### ファンデーション: `MDCIconButtonToggleFoundation`

メソッド | 説明
--- | ---
`handleClick()` | クリックイベントにおけるイベントハンドラの引き金になる。オン/オフのアイコンを切り替えたり、領域の属性を更新したりする。
