<!--docs:
title: "Checkboxes"
layout: detail
section: components
excerpt: "Checkboxes allow the user to select multiple options from a set."
iconId: selection_control
path: /catalog/input-controls/checkboxes/
-->

# Checkboxes

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/checkbox">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/checkboxes.png"
    width="99" alt="Checkbox screenshot">
  </a>
</div>-->

チェックボックスは複数の選択肢から一つもしくはそれ以上をユーザーに選ばせるものです。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-checkboxes">マテリアルデザインガイドライン: 選択コントロール – チェックボックス</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/checkbox">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/checkbox
```

## 基本的な使用法

ラベルの配置、ラベルが有効な際のリップルのインタラクティブな効果、そしてRTL認識といった機能強化のために MDC Checkbox は [MDC Form Field](../mdc-form-field) と共に使用することを推奨します。

```html
<div class="mdc-form-field">
  <div class="mdc-checkbox">
    <input type="checkbox"
           class="mdc-checkbox__native-control"
           id="checkbox-1"/>
    <div class="mdc-checkbox__background">
      <svg class="mdc-checkbox__checkmark"
           viewBox="0 0 24 24">
        <path class="mdc-checkbox__checkmark-path"
              fill="none"
              d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
      </svg>
      <div class="mdc-checkbox__mixedmark"></div>
    </div>
    <div class="mdc-checkbox__ripple"></div>
  </div>
  <label for="checkbox-1">Checkbox 1</label>
</div>
```

> **注意**: IE を使うときはコンソールに警告が出るのを避けるために終了タグ `</path>` を入れる必要があります。

### スタイル

```scss
@import "@material/form-field/mdc-form-field";
@import "@material/checkbox/mdc-checkbox";
```

### JavaScript のインスタンス化

チェックボックスは JavaScript なしでも動作しますが、`mdc-checkbox` 要素上の `MDCCheckbox` をインスタンス化することによりリップルエフェクトをつけることができます。ラベルにインタラクティブなリップルエフェクトを有効にするには、`mdc-form-field` 要素上の `MDCFormField` のインスタンス化と `input` のように  `MDCCheckbox` インスタンスを設定しなくてはなりません。

```js
import {MDCFormField} from '@material/form-field';
import {MDCCheckbox} from '@material/checkbox';

const checkbox = new MDCCheckbox(document.querySelector('.mdc-checkbox'));
const formField = new MDCFormField(document.querySelector('.mdc-form-field'));
formField.input = checkbox;
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。


## バリエーション

### 無効の状態

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
      <path class="mdc-checkbox__checkmark-path"
            fill="none"
            d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
    </svg>
    <div class="mdc-checkbox__mixedmark"></div>
  </div>
  <div class="mdc-checkbox__ripple"></div>
</div>
<label for="basic-disabled-checkbox" id="basic-disabled-checkbox-label">This is my disabled checkbox</label>
```

## 追加情報

### アクセシビリティ

マテリアルデザイン仕様ではタッチの対象は少なくとも  48 x 48 px にすることを勧めています。この要件を満たすために以下のようにチェックボックスに `mdc-checkbox--touch` クラスを追加してください。

```html
<div class="mdc-touch-target-wrapper">
  <div class="mdc-checkbox mdc-checkbox--touch">
    <input type="checkbox"
           class="mdc-checkbox__native-control"
           id="checkbox-1"/>
    <div class="mdc-checkbox__background">
      <svg class="mdc-checkbox__checkmark"
           viewBox="0 0 24 24">
        <path class="mdc-checkbox__checkmark-path"
              fill="none"
              d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
      </svg>
      <div class="mdc-checkbox__mixedmark"></div>
    </div>
    <div class="mdc-checkbox__ripple"></div>
  </div>
</div>
```

隣接している要素において、潜在的に（マージンを縮小するために）タッチ対象が重なってしまうのを避けたい場合は、外側に `mdc-touch-target-wrapper` 要素だけが必要なことに注意してください。

## スタイルのカスタマイズ

MDC Checkbox は「マーク」の状態（例えばチェックされているとか不確定とか）としてデフォルトで [MDC Theme](../mdc-theme) の `secondary` カラーを使います。

### Sass ミキシン

ミキシン | 説明
--- | ---
`mdc-checkbox-container-colors($unmarked-stroke-color, $unmarked-fill-color, $marked-stroke-color, $marked-fill-color, $generate-keyframes)` | 有効なチェックボックスのマークされているものとマークされていなものの両方について枠線と塗りの色を設定する。ミキシンが @keyframes を生成しないようにするには $generate-keyframes を false にする
`mdc-checkbox-disabled-container-colors($unmarked-stroke-color, $unmarked-fill-color, $marked-stroke-color, $marked-fill-color)` | 無効なチェックボックスのマークされているものとマークされていなものの両方について枠線と塗りの色を設定する。
`mdc-checkbox-ink-color($color)` | 有効なチェックボックスのチェックと未確定のアイコンのインクの色を設定する
`mdc-checkbox-disabled-ink-color($color)` | 無効なチェックボックスのチェックと未確定のアイコンのインクの色を設定する
`mdc-checkbox-focus-indicator-color($color)` | チェックボックスが選択されたとき、または未確定状態のときのフォーカスインジケーター（リップル）の色を設定する
`mdc-checkbox-ripple-size($ripple-size)` | チェックボックスのリップルの大きさを設定する
`mdc-checkbox-density($density-scale)` | チェックボックスの密度スケールを設定する。サポートしている密度スケールは `-3`、`-2`、`-1` そして `0`（デフォルト）

Checkbox コンポーネントのリップルエフェクトは [MDC Ripple](../mdc-ripple) のミキシンを使って設定されています。

## `MDCCheckbox` プロパティとメソッド

プロパティ | 型 | 説明
--- | --- | ---
`checked` | `boolean` | チェックボックスのチェック状態を設定/取得する
`indeterminate` | `boolean` | チェックボックスの未確定状態を設定/取得する
`disabled` | `boolean` | チェックボックスの無効状態を設定/取得する
`value` | `string` | チェックボックスの値を設定/取得する

## Web フレームワークでの使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のチェックボックスを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCCheckboxAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`forceLayout() => void` | ルート要素のレイアウトを強制的に設定する。この処理はアニメーションを正しく再起動させるために必要。これが不要であることが明らかであれば、この処理を何もしないようにすることもできる。
`isAttachedToDOM() => boolean` | コンポーネントが正しく DOM にアタッチされていれば true を返し、そうでなければ false を返す。
`isIndeterminate() => boolean` | コンポーネントが未確定状態のとき true を返す。
`isChecked() => boolean` | コンポーネントがチェックされていれば true を返す。
`hasNativeControl() => boolean` | コンポーネント内に input があれば true を返す。
`setNativeControlDisabled(disabled: boolean) => void` | input を利用不可にする。
`setNativeControlAttr(attr: string, value: string) => void` | ネイティブな input 要素の HTML 属性を与えられた値に設定する。
`removeNativeControlAttr(attr: string) => void` | ネイティブな input 要素から属性を削除する。

### `MDCCheckboxFoundation`

メソッド | 説明
--- | ---
`setDisabled(disabled: boolean) => void` | 基盤となっている input 要素の `disabled` プロパティを更新する。基盤となる input 要素が存在しないときは何もしない。
`handleAnimationEnd() => void` | ルート要素に適用された `animationend` イベントハンドラー。
`handleChange() => void` | チェックボックス要素に適用された `change` イベントハンドラー。
