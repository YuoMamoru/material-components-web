<!--docs:
title: "Radio Buttons"
layout: detail
section: components
iconId: radio_button
path: /catalog/input-controls/radio-buttons/
-->

> ✨ あなたは Material Design web コミュニティの一員ですか？この <a href='https://bit.ly/materialwebsurvey'>**10分調査**</a> にご記入ください。 ✨

# Radio Buttons

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/radio">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/radios.png" width="60" alt="Radio buttons screenshot">
  </a>
</div>-->

ラジオボタンは利用できるすべての選択肢を見ながら一つの選択肢をユーザーに選ばせるものです。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-radio-buttons">マテリアルデザインガイドライン: 選択コントロール – ラジオボタン</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/radio">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/radio
```

## 基本的な使用法

ラベルの配置、ラベルが有効な際のリップルのインタラクティブな効果、そしてRTL認識といった機能強化のために MDC Radio は [MDC Form Field](../mdc-form-field) と共に使用することを推奨します。

### HTML 構造

```html
<div class="mdc-form-field">
  <div class="mdc-radio">
    <input class="mdc-radio__native-control" type="radio" id="radio-1" name="radios" checked>
    <div class="mdc-radio__background">
      <div class="mdc-radio__outer-circle"></div>
      <div class="mdc-radio__inner-circle"></div>
    </div>
  </div>
  <label for="radio-1">Radio 1</label>
</div>
```

### スタイル

```scss
@import "@material/form-field/mdc-form-field";
@import "@material/radio/mdc-radio";
```

### JavaScript のインスタンス化

ラジオボタンは JavaScript なしでも動作しますが、`mdc-radio` 要素上の `MDCRadio` をインスタンス化することによりリップルエフェクトをつけることができます。ラベルにインタラクティブなリップルエフェクトを有効にするには、`mdc-form-field` 要素上の `MDCFormField` のインスタンス化と `input` のように  `MDCRadio` インスタンスを設定しなくてはなりません。

```js
import {MDCFormField} from '@material/form-field';
import {MDCRadio} from '@material/radio';

const radio = new MDCRadio(document.querySelector('.mdc-radio'));
const formField = new MDCFormField(document.querySelector('.mdc-form-field'));
formField.input = radio;
```

> JavaScript をインポートするより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## 様々な使用法

### 無効の状態 

ラジオボタンを無効にするには、ルート要素に `mdc-radio--disabled` クラスを追加し、`<input>` 要素に `disabled` 属性を設定します。無効なラジオボタンは入力を受け付けず、視覚的にも入力が受け付けられないように見えます。

```html
<div class="mdc-form-field">
  <div class="mdc-radio mdc-radio--disabled">
    <input class="mdc-radio__native-control" type="radio" id="radio-1" name="radios" disabled>
    <div class="mdc-radio__background">
      <div class="mdc-radio__outer-circle"></div>
      <div class="mdc-radio__inner-circle"></div>
    </div>
  </div>
  <label for="radio-1">Radio 1</label>
</div>
```

## スタイルのカスタマイズ

MDC Checkbox はデフォルトで [MDC Theme](../mdc-theme) の `secondary` カラーを使います。カスタマイズするには以下のミキシンを使います。

### Sass ミキシン

ミキシン | 説明
--- | ---
`mdc-radio-unchecked-stroke-color($color)` | チェックされていないラジオボタンの枠線の色を設定する。
`mdc-radio-checked-stroke-color($color)` | チェックされているラジオボタンの枠線の色を設定する。
`mdc-radio-ink-color($color)` | ラジオボタンのインクの色を設定する。
`mdc-radio-focus-indicator-color($color)` | フォーカス時のインジケーターの色を設定する。

#### 注意: Edge と CSS カスタムプロパティ

CSS カスタムプロパティを完全にサポートしているブラウザでは、引数として [MDC Theme](../mdc-theme) プロパティ（例えば `primary`）を与えても上記のミキシンは動作します。しかし、Edge は CSS カスタムプロパティを完全にサポートしていません。Sassミキシンのいずれかを使うときは、Edge をサポートするためには実際の色を指定する必要があります。

## `MDCRadio` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`checked` | Boolean | ラジオボタンのチェック状態を取得/設定する。
`disabled` | Boolean | ラジオボタンが無効かどうかの状態を取得/設定する。セッタはファンデーションの `setDisabled` の代替。
`value` | String | ラジオボタンの値を取得/設定する。

## Web フレームワークでの使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワークのセレクトを作ることができます。ニーズに合わせて <em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCRadioAdapter`

メソッド | 説明
--- | ---
`setNativeControlDisabled(disabled: boolean) => void` | インプットの `disabled` プロパティを与えられた値に設定する。
`addClass(className: string) => void` | ート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。

### `MDCRadioFoundation`

メソッド | 説明
--- | ---
`setDisabled(disabled: boolean) => void` | ネイティブなコントロールの無効かどうかの値を設定する。
