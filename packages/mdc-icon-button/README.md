<!--docs:
title: "Icon buttons"
layout: detail
section: components
excerpt: "Web icon buttons"
iconId: button
path: /catalog/buttons/icon-buttons/
-->

# Icon buttons

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/icon-button">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/icon-toggles.png" width="20" alt="Icon buttons screenshot">
  </a>
</div>-->

[Icon buttons](https://material.io/components/buttons/) は一回のタップでユーザーに操作を実行させたり選択させたりすることができます。

**注意**: アイコンとテキストの両方のあるボタンについては、`mdc-button` コンポーネントを使ってください。さらなる情報は `mdc-button` [ドキュメント](../mdc-button) を参照してください。

## アイコンボタンを使う

### インストール

```
npm install @material/icon-button
```

### スタイル

```scss
@use "@material/icon-button";

@include icon-button.core-styles;
```

### JavaScript のインスタンス化

アイコンボタンは JavaScript なしでも動作しますが、ルート要素に `MDCRipple` をインスタンス化することによりリップル効果を持つように拡張できます。詳細は [MDC Ripple](../mdc-ripple) を参照してください。

```js
import {MDCRipple} from '@material/ripple';

const iconButtonRipple = new MDCRipple(document.querySelector('.mdc-icon-button'));
iconButtonRipple.unbounded = true;
```

**注意**: JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

### アイコン

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

## アイコンボタン

```html
<button class="mdc-icon-button material-icons">favorite</button>
```

**注意**: MDC Icon Button では `<button>` タグと `<a>` タグの両方を使うことができます。

**注意**: IE11 ではアイコンのテキストの後に改行かスペースがあるとアイコンを正しく中央揃えにしません。

## トグルアイコンボタン

アイコンボタンはオンとオフのアイコンを切り替えるために使用することができます。

トグルアイコンボタンとしてアイコンボタンを表示するには、オンオフ両方のアイコンを子要素として追加し、オン要素を表すアイコンに `mdc-icon-button__icon--on` クラスを設定します。「オン」の状態で初期化するなら親要素である `button` に `mdc-icon-button--on` を追加します。そしてルート要素に `MDCIconButtonToggle` をインスタンス化します。

```html
<button id="add-to-favorites"
   class="mdc-icon-button"
   aria-label="Add to favorites"
   aria-pressed="false">
   <i class="material-icons mdc-icon-button__icon mdc-icon-button__icon--on">favorite</i>
   <i class="material-icons mdc-icon-button__icon">favorite_border</i>
</button>
```

Then, instantiate an `MDCIconButtonToggle` on the root element.

```js
import {MDCIconButtonToggle} from '@material/icon-button';
const iconToggle = new MDCIconButtonToggle(document.querySelector('.mdc-icon-button'));
```

#### SVG を使ったトグルアイコンボタン

トグルアイコンボタンでは SVG を使うことができます。

```html
<button id="star-this-item"
   class="mdc-icon-button mdc-icon-button--on"
   aria-label="Unstar this item"
   aria-pressed="true">
   <svg class="mdc-icon-button__icon">
     ...
   </svg>
   <svg class="mdc-icon-button__icon mdc-icon-button__icon--on">
     ...
  </svg>
</button>
```

#### 画像を使ったトグルアイコンボタン

アイコン切り替えボタンでは `img` タグを使うことができます。

```html
<button id="star-this-item"
   class="mdc-icon-button mdc-icon-button--on"
   aria-label="Unstar this item"
   aria-pressed="true">
   <img src="" class="mdc-icon-button__icon"/>
   <img src="" class="mdc-icon-button__icon mdc-icon-button__icon--on"/>
</button>
```

### トグルされる aria label を伴うトグルアイコンボタン

一部のデザインではアイコンボタンの状態に応じて aria label を変更する必要があります。この場合、`data-aria-label-on`（オンの状態の aria label）属性と `aria-data-label-off`（オフの状態の aria label）属性を指定し、`aria-pressed` 属性を省きます。

```html
<button id="add-to-favorites"
   class="mdc-icon-button"
   aria-label="Add to favorites"
   data-aria-label-on="Remove from favorites"
   data-aria-label-off="Add to favorites">
   <i class="material-icons mdc-icon-button__icon mdc-icon-button__icon--on">favorite</i>
   <i class="material-icons mdc-icon-button__icon">favorite_border</i>
</button>
```

## API

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
`density($density-scale)` | アイコンボタンの密度スケールを設定する。サポートしている密度スケールの範囲は `-5` から `0`（`0` がデフォルト）。
`size($size)` | 全体のサイズをもとにアイコンボタンのパディングを設定する。
`ink-color($color)` | フォント色とリップルの色を指定した色に設定する。
`disabled-ink-color($color)` | 無効なアイコンボタンのフォント色を指定した色に設定する。
`flip-icon-in-rtl()` | RTL コンテンツ内でのみ反転させる。

## `MDCIconButtonToggle` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`on` | Boolean | 切り替え状態を指定した `isOn` の値に設定する。

### イベント

イベント | イベントデータの構造 | 説明
--- | --- | ---
`MDCIconButtonToggle:change` | `{"detail": {"isOn": boolean}}` | アイコンが切り換えられた時に発生する。

### `MDCIconButtonToggleAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`hasClass(className: string) => boolean` | ルート要素が与えられた CSS クラス名を持っているかどうかを調べる。
`setAttr(name: string, value: string) => void` | ルート要素の属性 `name` に `value` を設定する。
`notifyChange(evtData: {isOn: boolean}) => void` | 変更通知を行い、`evtData` を環境のイベントハンドリングシステムに渡す。素の実装ではカスタムイベントはこれを利用している。

### `MDCIconButtonToggleFoundation`

メソッド | 説明
--- | ---
`handleClick()` | クリックイベントにおけるイベントハンドラの引き金になる。オン/オフのアイコンを切り替えたり、領域の属性を更新したりする。
