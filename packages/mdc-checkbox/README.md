<!--docs:
title: "Checkboxes"
layout: detail
section: components
iconId: selection_control
path: /catalog/input-controls/checkboxes/
-->

# Checkboxes

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/checkbox.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/checkboxes.png" width="99" alt="Checkboxes screenshot">
  </a>
</div>-->

MDC Checkbox コンポーネントは [マテリアルデザインチェックボックス要件](https://material.io/guidelines/components/selection-controls.html#selection-controls-checkbox) に準拠したチェックボックスコンポーネントです。このコンポーネントは JavaScritp を使用しなくても基本的な機能を備えており、あらゆる状況で機能します。JavaScript オブジェクトをチェックボックスで使用すれば、状態を切り替える際により複雑なアニメーション効果を加えることができます。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/selection-controls.html#selection-controls-checkbox">マテリアルデザインガイドライン: 選択コントロール – チェックボックス</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/checkbox.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install --save @material/checkbox
```

## 使用法

### 単独のチェックボックス

```html
<div class="mdc-checkbox">
  <input type="checkbox"
         class="mdc-checkbox__native-control"/>
  <div class="mdc-checkbox__background">
    <svg class="mdc-checkbox__checkmark"
         viewBox="0 0 24 24">
      <path class="mdc-checkbox__checkmark__path"
            fill="none"
            stroke="white"
            d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
    </svg>
    <div class="mdc-checkbox__mixedmark"></div>
  </div>
</div>
```

チェックボックスコンポーネントはネイティブなチェックボックス要素を基盤として動作しています。この要素はチェックボックス自体と同じ方法でサイズと位置を決め、補助デバイスにとって適切な動作をします。

ダークテーマのチェックボックススタイルを使うために `mdc-checkbox--theme-dark` 修飾クラスをコンポーネントに追加することもできます。

加えて、チェックボックスは [mdc-form-field](../mdc-form-field) とともに使って、簡単にチェックボックスとラベルを配置できます。

```html
<div class="mdc-form-field">
  <div class="mdc-checkbox">
    <input type="checkbox"
           id="my-checkbox"
           class="mdc-checkbox__native-control"/>
    <div class="mdc-checkbox__background">
      <svg class="mdc-checkbox__checkmark"
           viewBox="0 0 24 24">
        <path class="mdc-checkbox__checkmark__path"
              fill="none"
              stroke="white"
              d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
      </svg>
      <div class="mdc-checkbox__mixedmark"></div>
    </div>
  </div>

  <label for="my-checkbox">My Checkbox Label</label>
</div>
```

> **注意**: IE を使うときはコンソールに警告が出るのを避けるために終了タグ `</path>` を入れる必要があります。

#### 無効なチェックボックス

ホバー状態のときにアクティブにならないようにするために CSS のみのチェックボックスのルート要素には `mdc-checkbox--disabled` が必要なことに注意してください。JavaScript コンポーネントを使用したチェックボックスではこのクラスは不要です。`<input>` 要素に `disabled` 属性をつけるだけで十分です。

```html
<div class="mdc-checkbox mdc-checkbox--disabled">
  <input type="checkbox"
         id="basic-disabled-checkbox"
         class="mdc-checkbox__native-control"
         disabled />
  <div class="mdc-checkbox__background">
    <svg class="mdc-checkbox__checkmark"
         viewBox="0 0 24 24">
      <path class="mdc-checkbox__checkmark__path"
            fill="none"
            stroke="white"
            d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
    </svg>
    <div class="mdc-checkbox__mixedmark"></div>
  </div>
</div>
<label for="basic-disabled-checkbox" id="basic-disabled-checkbox-label">This is my disabled checkbox</label>
```

### JS コンポーネントの使用

チェックボックスの状態を切り替える際に、マテリアルデザインモーションに完全に準拠したチェックボックスの状態変化を段階的な行う コンポーネント / ファンデーション の組み合わせが MDC Checkbox には付属しています。

#### コードへのインクルード

##### ES2015

```javascript
import {MDCCheckbox, MDCCheckboxFoundation} from '@material/checkbox';
```

##### CommonJS

```javascript
const mdcCheckbox = require('mdc-checkbox');
const MDCCheckbox = mdcCheckbox.MDCCheckbox;
const MDCCheckboxFoundation = mdcCheckbox.MDCCheckboxFoundation;
```

##### AMD

```javascript
require(['path/to/mdc-checkbox'], mdcCheckbox => {
  const MDCCheckbox = mdcCheckbox.MDCCheckbox;
  const MDCCheckboxFoundation = mdcCheckbox.MDCCheckboxFoundation;
});
```

##### Global

```javascript
const MDCCheckbox = mdc.checkbox.MDCCheckbox;
const MDCCheckboxFoundation = mdc.checkbox.MDCCheckboxFoundation;
```

#### 自動的なインスタンス化

チェックボックスのコンポーネントインスタンスの保持に関して特に気にしないのであれば、単純に `attachTo()` に DOM 要素を渡して呼んでください。

```javascript
mdc.checkbox.MDCCheckbox.attachTo(document.querySelector('.mdc-checkbox'));
```

#### 手動でのインスタンス化

Checkbox はコンストラクタを使って `attachTo` と同様に簡単に初期化できます。

```javascript
import {MDCCheckbox} from '@material/checkbox';

const checkbox = new MDCCheckbox(document.querySelector('.mdc-checkbox'));
```

#### MDCCheckbox API

MDCCheckbox API はネイティブなチェックボックス要素で見られるものに似たアクセサプロパティをを提供しています。

##### MDCCheckbox.checked

真偽値。チェックボックスがチェックされているかどうかを返す。このプロパティを設定すると基盤となっているチェックボックス要素が更新されます。

##### MDCCheckbox.indeterminate

真偽値。チェックボックスが未確定かどうかを返す。このプロパティを設定すると基盤となっているチェックボックス要素が更新されます。

##### MDCCheckbox.disabled

真偽値。チェックボックスが無効かどうかを返す。このプロパティを設定すると基盤となっているチェックボックス要素が更新されます。

##### MDCCheckbox.value

文字列。チェックボックスの値を返す。このプロパティを設定すると基盤となっているチェックボックス要素が更新されます。

### ファンデーションクラスの使用

外部のフレームワークやライブラリがコンポーネントを統合するために使用可能な `MDCCheckboxFoundation` クラスが MDC Checkbox には付属しています。すべてのファンデーションクラスでアダプタオブジェクトが提供されなくてはなりません。チェックボックスのアダプタは以下の関数を提供しなくてはいけません。

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `registerAnimationEndHandler(handler: EventListener) => void` | `animationend` イベントが発生したときに呼ばれるイベントハンドラをルート要素に登録する。これを正しく動作させるにはベンダプレフィックスを考慮しなくてはいけないことに注意が必要。 |
| `deregisterAnimationEndHandler(handler: EventListener) => void` | `animationend` イベントリスナーからイベントハンドラの登録を解除する。あらかじめ `registerAnimationEndHandler` の呼び出しを通じて設定されたハンドラに対してのみ呼びされる。 |
| `registerChangeHandler(handler: EventListener) => void` | `change` イベントが発生したときに呼ばれるイベントハンドラをネイティブなコントロール（ルート要素では <em>ない</em>）に登録する。 |
| `deregisterChangeHandler(handler: EventListener) => void` | あらかじめ `registerChangeHandler` を通じて設定されたイベントハンドラの登録を解除する。 |
| `getNativeControl() => HTMLInputElement?` | 利用できる状態であればネイティブなチェックボックスコントロールを返す。コントロールが利用できない状態であれば、直ちにそれに依存するメソッドは終了する。 |
| `forceLayout() => void` | ルート要素のレイアウトを強制的に設定する。この処理はアニメーションを正しく再起動させるために必要。これが不要であることが明らかであれば、この処理を何もしないようにすることもできる。 |
| `isAttachedToDOM() => boolean` | コンポーネントが正しく DOM にアタッチされていれば true を返し、そうでなければ false を返す。 |


#### MDCCheckboxFoundation API

##### MDCCheckboxFoundation.isChecked() => boolean

基盤となっている input 要素がチェックされているかどうかを返します。利用できない状態のときは false を返します。

##### MDCCheckboxFoundation.setChecked(checked: boolean)

基盤となっている input 要素の `checked` プロパティを更新します。基盤となる input 要素が存在しないときは何もしません。

##### MDCCheckboxFoundation.isIndeterminate() => boolean

基盤となっている input 要素が未確定かどうかを返します。利用できない状態のときは false を返します。

##### MDCCheckboxFoundation.setIndeterminate(indeterminate: boolean)

基盤となっている input 要素の `indeterminate` プロパティを更新します。基盤となる input 要素が存在しないときは何もしません。

##### MDCCheckboxFoundation.isDisabled() => boolean

基盤となっている input 要素が無効かどうかを返します。利用できない状態のときは false を返します。

##### MDCCheckboxFoundation.setDisabled(disabled: boolean)

基盤となっている input 要素の `disabled` プロパティを更新します。基盤となる input 要素が存在しないときは何もしません。

##### MDCCheckboxFoundation.getValue() => string

`adapter.getNativeControl().value` の値を返します。`getNativeControl()` がオブジェクトを返さないときは `null` を返します。

##### MDCCheckboxFoundation.setValue(value: string) => void

`adapter.getNativeControl().value` の値を設定します。`getNativeControl()` がオブジェクトを返さないときは何もしません。

## テーマ

MDC Checkbox はデフォルトでは「マーク」状態（チェックもしくは未確定）にテーマのセカンダリカラーを使い、ダークテーマも完全に認識します。

### Sass ミキシン

以下のミキシンは <em>有効な</em> チェックボックスにのみ適用されます。現在、<em>無効な</em> チェックボックスの色をカスタマイズすることはできません。

ミキシン | 説明
--- | ---
`mdc-checkbox-container-colors($unmarked-stroke-color, $unmarked-fill-color, $marked-fill-color, $generate-keyframes)` | チェックボックスの枠線と塗りの色の設定とアニメーションのための CSS クラスを生成する。
`mdc-checkbox-ink-color($color)` | チェックと未確定のアイコンのインクの色を設定する。
`mdc-checkbox-focus-indicator-color($color)` | フォーカス時のインジケータの色を設定する。

Checkbox コンポーネントのリップルエフェクトは [MDC Ripple](../mdc-ripple) のミキシンを使って設定されています。

#### `mdc-checkbox-container-colors($unmarked-stroke-color, $unmarked-fill-color, $marked-fill-color, $generate-keyframes)`

チェックボックスがマークされている/マークされていないの各状態を表す枠線と塗りの色の設定とアニメーションのための CSS クラスを生成します。マークされていないときは枠線と塗りの色を個別にカスタマイズできます。マークされているときは塗りの色だけをカスタマイズでき、枠線には自動的に塗りの色が使われます。

すべてのパラメータはオプションで、指定されていないものにはデフォルト値が使われます。

CSS だけのチェックボックスを使うときは、ミキシンが `@keyframes` と JavaScript コンポーネントが使う CSS クラスを生成しないようにするため、 `$generate-keyframes` に `false` を設定してください。

### 注意: Edge と CSS 変数

CSS 変数を完全にサポートしているブラウザでは、MDC Checkbox はテーマプロパティが使用されているすべてのところで CSS 変数を参照します。しかし、Edge の CSS 変数サポートのバグのため、Edge では `.mdc-checkbox__background::before` の `background-color` に CSS 変数が利用されません。もし、プライマリカラー（訳注: 原文で primary color となっているがセカンダリカラーの誤り）の CSS 変数を変更したいのであれば Edge のためにスタイルを手動で上書きする必要がある、ということをこれは意味しています。
