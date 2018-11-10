<!--docs:
title: "Form Fields"
layout: detail
section: components
path: /catalog/input-controls/form-fields/
-->

> ✨ あなたは Material Design web コミュニティの一員ですか？この <a href='https://bit.ly/materialwebsurvey'>**10分調査**</a> にご記入ください。 ✨

# Form Fields

MDC Form Field は MDC Web フォームフィールド（例えばチェックボックス）をラベルで整列させ、RTL 対応を提供します。また、ラベルにインタラクティブな [ripple](../mdc-ripple) エフェクトを有効にします。

## インストール

```
npm install @material/form-field
```

## デモ

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/radio">ラジオボタンのデモ</a>
  </li>
</ul>

## 基本的な使用法

### HTML 構造

[MDC Checkbox](../mdc-checkbox) や [MDC Radio](../mdc-radio) のような MDC Web フォームコントロールの _input_ と _label_ 要素の組み合わせをラップするには `mdc-form-field` 要素を使用します。ここに MDC Checkbox の例を記載します。

```html
<div class="mdc-form-field">
  <div class="mdc-checkbox">
    <input type="checkbox" id="my-checkbox" class="mdc-checkbox__native-control"/>
    <div class="mdc-checkbox__background">
      ...
    </div>
  </div>
  <label for="my-checkbox">This is my checkbox</label>
</div>
```

> <em>注意</em>: MDC Form Field は label と input が既にコンポーネントのスタイルやロジックによってともに処理されている状況を想定して **いません**。例えば JavaScript で拡張された [MDC Text Field](../mdc-textfield) のインスタンスは既に label と input の両方が固有のルート要素のもとで管理されています。

### JavaScript のインスタンス化

MDC Form Field を [ripple](../mdc-ripple) エフェクトのある MDC Web コンポーネントと共に使うときは、ラベルにインタラクティブなリップルエフェクトを有効にするために `MDCFormField` をインスタンス化し、[`input` プロパティ](#mdcformfield-properties-and-methods) を設定することができます。

```js
import {MDCFormField} from '@material/form-field';
import {MDCCheckbox} from '@material/checkbox';

const formField = new MDCFormField(document.querySelector('.mdc-form-field'));
const checkbox = new MDCCheckbox(document.querySelector('.mdc-checkbox'));
formField.input = checkbox;
```

> See [Importing the JS component](../../docs/importing-js.md) for more information on how to import JavaScript.

## 様々な使用法

### ラベルの位置

デフォルトでは、input はラベルの前に配置されます。`mdc-form-field--align-end` クラスを追加することにより input をラベルの後ろに配置することができます。

```html
<div class="mdc-form-field mdc-form-field--align-end">
  <div class="mdc-checkbox">
    <input type="checkbox" id="my-checkbox" class="mdc-checkbox__native-control"/>
    <div class="mdc-checkbox__background">
      ...
    </div>
  </div>
  <label for="my-checkbox">This is my checkbox</label>
</div>
```

## <a name="mdcformfield-properties-and-methods"></a>`MDCFormField` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`input` | String | フォームフィールドの input を取得/設定する。

ラベルのリップル作用を正しく動作させるために、`input` プロパティには `ripple` ゲッタを公開している MDC Web input 要素の有効なインスタンスが設定されている必要があります。`input` プロパティが設定されていなかったり input インスタンスが `ripple` ゲッタを公開していない時には動作しません。

## Web フレームワークでの使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワークのセレクトを作ることができます。ニーズに合わせて <em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCFormFieldAdapter`

| メソッド | 説明 |
| --- | --- |
| `registerInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー  `handler` をラベルに登録する。 |
| `deregisterInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー  `handler` をラベルから削除する。 |
| `activateInputRipple() => void` | input 要素のリップルを利用できるようにする。input 要素の `ripple` プロパティが `activate` を呼べなくてはならない。 |
| `deactivateInputRipple() => void` | input 要素のリップルを利用できないようにする。input 要素の `ripple` プロパティが `deactivate` を呼べなくてはならない。 |
