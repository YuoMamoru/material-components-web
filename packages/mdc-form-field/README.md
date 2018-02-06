<!--docs:
title: "Form Fields"
layout: detail
section: components
path: /catalog/input-controls/form-fields/
-->

# Form Fields

MDC Form Field はテーマ対応、RTL 対応のフィールドとラベルの組み合わせを容易に作成できる `mdc-form-field` ヘルパークラスを提供しています。これはラベルのイベントに反応する input 要素のリップルを容易に実現するための `MDCFormField` クラスも提供しています。

## インストール

```
npm install --save @material/form-field
```

## CSS の使用

`mdc-form-field` クラスは隣り合った `input` と `label` の任意の組み合わせを直接の子に持つ親要素で使うことができます。

```html
<div class="mdc-form-field">
  <input type="checkbox" id="input">
  <label for="input">Input Label</label>
</div>
```

デフォルトでは、input の後ろに label を配置します。`align-end` 修飾クラスを使用すると、この振る舞いを変更できます。

```html
<div class="mdc-form-field mdc-form-field--align-end">
  <input type="checkbox" id="input">
  <label for="input">Input Label</label>
</div>
```

こうすると、ラベルはチェックボックスの前に来ます。

### MDC Web コンポーネントとともに使用

`mdc-form-field` は `input` 要素に対してだけでなく、連続した兄弟要素が `label` 要素であれば <em>任意の</em> 直接の子要素に対して作用します。このことは、Checkbox や Radio のような MDC Web フォームコントロールでも動作するということを意味しています。

```html
<div class="mdc-form-field">
  <div class="mdc-checkbox">
    <input type="checkbox"
           id="my-checkbox"
           class="mdc-checkbox__native-control"/>
    <div class="mdc-checkbox__background">
      <svg class="mdc-checkbox__checkmark"
           viewBox="0 0 24 24">
        <path class="mdc-checkbox__checkmark-path"
              fill="none"
              stroke="white"
              d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
      </svg>
      <div class="mdc-checkbox__mixedmark"></div>
    </div>
  </div>
  <label for="my-checkbox" id="my-checkbox-label">This is my checkbox</label>
</div>
```

> MDC Form Field は label と input が既にその他のコンポーネントのスタイルやロジックによってともに処理されている状況を想定して **いません**。例えば JavaScript で拡張された MDC Text Field のインスタンスは既に label と input の両方が固有のルート要素のもとで管理されています。

### RTL サポート

`mdc-form-field` は自動的に RTL 対応がなされており、RTL コンテキストの中では要素を再配置します。`mdc-form-field` はその要素もしくはその祖先の要素に `dir="rtl"` があれば RTL スタイルが適用されます。


## JS の使用

### コードへのインクルード

#### ES2015

```javascript
import {MDCFormField, MDCFormFieldFoundation} from '@material/form-field';
```

#### CommonJS

```javascript
const mdcFormField = require('mdc-form-field');
const MDCFormField = mdcFormField.MDCFormField;
const MDCFormFieldFoundation = mdcFormField.MDCFormFieldFoundation;
```

#### AMD

```javascript
require(['path/to/mdc-form-field'], mdcFormField => {
  const MDCFormField = mdcFormField.MDCFormField;
  const MDCFormFieldFoundation = mdcFormField.MDCFormFieldFoundation;
});
```

#### Global

```javascript
const MDCFormField = mdc.formField.MDCFormField;
const MDCFormFieldFoundation = mdc.formField.MDCFormFieldFoundation;
```

### インストール

```javascript
import {MDCFormField} from '@material/form-field';

const formField = new MDCFormField(document.querySelector('.mdc-form-field'));
```

### MDCFormField API

`MDCFormField` の機能はたった一つのアクセサメソッドを公開しています。

#### MDCFormField.input

MDC Web の input 要素のインスタンスとともに動作する読み書き可能なプロパティです。

適切に動作するラベルのリップルを統合するために、このプロパティには `ripple` ゲッタを持つ MDC Web の input 要素の有効なインスタンスを設定する必要があります。

```javascript
const formField = new MDCFormField(document.querySelector('.mdc-form-field'));
const radio = new MDCRadio(document.querySelector('.mdc-radio'));

formField.input = radio;
```

`input` プロパティが設定されていない、もしくは input インスタンスが `ripple` ゲッタを持っていないときは何もしません。


### アダプタ

| メソッド | 説明 |
| --- | --- |
| `registerInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー  `handler` をラベルに登録する。 |
| `deregisterInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー  `handler` をラベルから削除する。 |
| `activateInputRipple() => void` | input 要素のリップルを利用できるようにする。input 要素の `ripple` プロパティが `activate` を呼べなくてはならない。 |
| `deactivateInputRipple() => void` | input 要素のリップルを利用できないようにする。input 要素の `ripple` プロパティが `deactivate` を呼べなくてはならない。 |
