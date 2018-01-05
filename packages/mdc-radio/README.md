<!--docs:
title: "Radio Buttons"
layout: detail
section: components
iconId: radio_button
path: /catalog/input-controls/radio-buttons/
-->

# Radio Buttons

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/radio.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/radios.png" width="60" alt="Radio buttons screenshot">
  </a>
</div>-->

MDC Radio Button コンポーネントは [マテリアルデザイン仕様](https://material.io/guidelines/components/selection-controls.html#selection-controls-radio-button) に準拠したラジオボタンを提供します。必ずしも JavaScript を必要としませんが、JavaScript を使うことにより拡張可能であり、より優れた双方向 UX や状態変化に関するコンポーネントレベルの API も提供しています。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/selection-controls.html#selection-controls-radio-button">マテリアルデザインガイドライン: 選択コントロール – ラジオボタン</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/radio.html">Demo</a>
  </li>
</ul>

## インストール

```
npm install --save @material/radio
```

## 使用法

```html
<div class="mdc-radio">
  <input class="mdc-radio__native-control" type="radio" id="radio-1" name="radios" checked>
  <div class="mdc-radio__background">
    <div class="mdc-radio__outer-circle"></div>
    <div class="mdc-radio__inner-circle"></div>
  </div>
</div>
<label id="radio-1-label" for="radio-1">Radio 1</label>

<div class="mdc-radio">
  <input class="mdc-radio__native-control" type="radio" id="radio-2" name="radios">
  <div class="mdc-radio__background">
    <div class="mdc-radio__outer-circle"></div>
    <div class="mdc-radio__inner-circle"></div>
  </div>
</div>
<label id="radio-2-label" for="radio-2">Radio 2</label>
```

> TODO(TK): Talk about `mdc-form-field` here.

#### 無効なラジオボタン

```html
<div class="mdc-radio mdc-radio--disabled">
  <input class="mdc-radio__native-control" type="radio" id="radio-1" name="radios" disabled>
  <div class="mdc-radio__background">
    <div class="mdc-radio__outer-circle"></div>
    <div class="mdc-radio__inner-circle"></div>
  </div>
</div>
<label id="radio-1-label" for="radio-1">Disabled Radio 1</label>
```

JS を使うときには、リップル要素がポインタイベントを処理してしまうことを避けるため、ルート要素に `mdc-radio--disabled` が必要になることに気を付けてください。CSS だけで使用するときにも、ホバー状態が有効にならないようにするために必要です。

### JS コンポーネントの使用

MDC Radio には [mdc-ripple](../mdc-ripple) を通じて高度な双方向 UX やプログラムからにラジオボタンの状態を変更するための API を提供する コンポーネント/ファンデーション の各クラスが附属しています。

#### コードへのインクルード

##### ES2015

```javascript
import {MDCRadio, MDCRadioFoundation} from '@material/radio';
```

##### CommonJS

```javascript
const mdcRadio = require('mdc-radio');
const MDCRadio = mdcRadio.MDCRadio;
const MDCRadioFoundation = mdcRadio.MDCRadioFoundation;
```

##### AMD

```javascript
require(['path/to/mdc-radio'], mdcRadio => {
  const MDCRadio = mdcRadio.MDCRadio;
  const MDCRadioFoundation = mdcRadio.MDCRadioFoundation;
});
```

##### Global

```javascript
const MDCRadio = mdc.radio.MDCRadio;
const MDCRadioFoundation = mdc.radio.MDCRadioFoundation;
```

#### 自動的なインスタンス化

ラジオボタンのコンポーネントインスタンスの保持に関して特に気にしないのであれば、単純に `attachTo()` に DOM 要素を渡して呼んでください。

```javascript
mdc.radio.MDCRadio.attachTo(document.querySelector('.mdc-radio'));
```

#### 手動でのインスタンス化

Radio はコンストラクタを使って `attachTo` と同様に簡単に初期化できます。

```javascript
import {MDCRadio} from '@material/radio';

const radio = new MDCRadio(document.querySelector('.mdc-radio'));
```

#### MDCRadio API

通常の DOM 要素と同様に、アクセサメソッドを通じて `MDCRadio` の機能が公開されています。

##### MDCRadio.checked

真偽値。取得/設定の際のファンデーションの `isChecked`/`setChecked` メソッドをプロキシする。

##### MDCRadio.disabled

真偽値。取得/設定の際のファンデーションの `isDisabled/setDisabled` メソッドをプロキシする。

##### MDCRadio.value

真偽値。取得/設定の際のファンデーションの `getValue/setValue` メソッドをプロキシする。

### ファンデーションクラスの使用

MDC Radio は主にネイティブなコントロールに基づき動作するので、アダプタ API は極めて単純です。

| メソッド | 説明 |
| --- | --- |
| `getNativeControl() => HTMLInputElement?` | 利用できる状態であればネイティブなチェックボックスコントロールを返す。コントロールが利用できない状態であれば、直ちにそれに依存するメソッドは終了する。 |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |


#### 完全なファンデーション API

##### MDCRadioFoundation.isChecked() => boolean

`adapter.getNativeControl().checked` の値を返します。`getNativeControl()` がオブジェクトを返さないときは `false` を返します。

##### MDCRadioFoundation.setChecked(checked: boolean) => void

`adapter.getNativeControl().checked` の値を設定します。`getNativeControl()` がオブジェクトを返さないときは何もしません。

##### MDCRadioFoundation.isDisabled() => boolean

`adapter.getNativeControl().disabled` の値を返します。`getNativeControl()` がオブジェクトを返さないときは `false` を返します。

##### MDCRadioFoundation.setDisabled(disabled: boolean) => void

`adapter.getNativeControl().disabled` の値を設定します。`disabled` が true かどうかに応じて `mdc-radio--disabled` クラスを追加/削除もします。`getNativeControl()` の戻り値がなくても正常に処理がなされます。

##### MDCRadioFoundation.getValue() => string

`adapter.getNativeControl().value` の値を返します。`getNativeControl()` がオブジェクトを返さないときは `null` を返します。

##### MDCRadioFoundation.setValue(value: string) => void

`adapter.getNativeControl().value` の値を設定します。`getNativeControl()` がオブジェクトを返さないときは何もしません。

## テーマ

MDC Radio はデフォルトではチェックの状態の表示にテーマのセカンダリカラーを使い、ダークテーマも完全に認識します。

### Sass ミキシン

以下のミキシンは <em>有効な</em> ラジオボタンにのみ適用されます。現在、<em>無効な</em> ラジオボタンの色をカスタマイズすることはできません。

ミキシン | 説明
--- | ---
`mdc-radio-unchecked-stroke-color($color)` | チェックされていないラジオボタンの枠線の色を設定する。
`mdc-radio-checked-stroke-color($color)` | チェックされているラジオボタンの枠線の色を設定する。
`mdc-radio-ink-color($color)` | インクの色を設定する。
`mdc-radio-focus-indicator-color($color)` | フォーカス時のインジケータの色を設定する。

Radio Button コンポーネントのリップルエフェクトは [MDC Ripple](../mdc-ripple) のミキシンを使って設定されています。

### 注意: Edge と CSS 変数

CSS 変数を完全にサポートしているブラウザでは、MDC Radio はテーマプロパティが使用されているすべてのところで CSS 変数を参照します。しかし、Edge の CSS 変数サポートのバグのため、Edge では `.mdc-radio__background::before` の `background-color` に CSS 変数が利用されません。もし、プライマリカラー（訳注: 原文で primary color となっているがセカンダリカラーの誤り）の CSS 変数を変更したいのであれば Edge のためにスタイルを手動で上書きする必要がある、ということをこれは意味しています。
