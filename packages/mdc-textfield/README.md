<!--docs:
title: "Text Field"
layout: detail
section: components
iconId: text_field
path: /catalog/input-controls/text-field/
-->

# Text Field

Text Field はユーザーのテキストの入力、編集、選択に対応しています。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-text-fields">マテリアルデザインガイドライン: テキスト欄</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/text-field">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/textfield
```

## 基本的な使用法

### HTML 構造

```html
<div class="mdc-text-field">
  <input type="text" id="my-text-field" class="mdc-text-field__input">
  <label class="mdc-floating-label" for="my-text-field">Hint text</label>
  <div class="mdc-line-ripple"></div>
</div>
```

> 注意: 詳細については、[MDC Line Ripple](../mdc-line-ripple/README.md) と [MDC Floating Label](../mdc-floating-label/README.md) を参照してください。

### スタイル

```scss
@import "@material/textfield/mdc-text-field";
```

### JavaScript のインスタンス化

```js
import {MDCTextField} from '@material/textfield';

const textField = new MDCTextField(document.querySelector('.mdc-text-field'));
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## バリエーション

### フル幅のテキスト欄

フル幅のテキスト欄は詳細な作業や複雑な情報の入力の際に便利です。

```html
<div class="mdc-text-field mdc-text-field--fullwidth">
  <input class="mdc-text-field__input"
         type="text"
         placeholder="Full-Width Text Field"
         aria-label="Full-Width Text Field">
</div>
```

> <em>注意</em>: `mdc-text-field--outlined` はフル幅のテキスト欄では使えません。

> <em>注意</em>: `mdc-text-field--fullwidth` の内部で `mdc-floating-label` を使わないでください。フル幅のテキスト欄の DOM 構造の一部としてラベルを含めることはできません。

### 複数行テキスト欄

```html
<div class="mdc-text-field mdc-text-field--textarea">
  <textarea id="textarea" class="mdc-text-field__input" rows="8" cols="40"></textarea>
  <div class="mdc-notched-outline">
    <div class="mdc-notched-outline__leading"></div>
    <div class="mdc-notched-outline__notch">
      <label for="textarea" class="mdc-floating-label">Textarea Label</label>
    </div>
    <div class="mdc-notched-outline__trailing"></div>
  </div>
</div>
```

### アウトライン

```html
<div class="mdc-text-field mdc-text-field--outlined">
  <input type="text" id="tf-outlined" class="mdc-text-field__input">
  <div class="mdc-notched-outline">
    <div class="mdc-notched-outline__leading"></div>
    <div class="mdc-notched-outline__notch">
      <label for="tf-outlined" class="mdc-floating-label">Your Name</label>
    </div>
    <div class="mdc-notched-outline__trailing"></div>
  </div>
</div>
```

ノッチ付きアウトラインサブコンポーネントの使用についてのより詳しい情報は [ここ](../mdc-notched-outline/) を参照してください。

> <em>注意</em>: <em>`mdc-text-field--outlined` を使うときは</em>、`mdc-text-field` の内部で `mdc-line-ripple` を使わないでください。ラインリップルはアウトラインの付いたテキスト欄の DOM 構造の一部として入れてはいけません。

### 無効の状態

テキスト欄を無効にするには、`<input>` 要素に `disabled` 属性を追加し、`mdc-text-field` 要素に `mdc-text-field--disabled` クラスを追加します。

```html
<div class="mdc-text-field mdc-text-field--disabled">
  <input type="text" id="disabled-text-field" class="mdc-text-field__input" disabled>
  <label class="mdc-floating-label" for="disabled-text-field">Disabled text field</label>
  <div class="mdc-line-ripple"></div>
</div>
```

### ラベルなしテキスト欄

テキスト欄の横に別の明確な文言表示がすでにあるなら、テキスト欄にラベルは必要ではありません。そのような場合、クラス名 `mdc-text-field--no-label` を追加し、ラベル要素を構成から削除してください。

#### フル幅

```html
<div class="mdc-text-field mdc-text-field--no-label">
  <input type="text" class="mdc-text-field__input" placeholder="Placeholder text" aria-label="Label">
  <div class="mdc-line-ripple"></div>
</div>
```

#### アウトライン

```html
<div class="mdc-text-field mdc-text-field--outlined mdc-text-field--no-label">
  <input type="text" class="mdc-text-field__input" aria-label="Label">
  <div class="mdc-notched-outline">
    <div class="mdc-notched-outline__leading"></div>
    <div class="mdc-notched-outline__trailing"></div>
  </div>
</div>
```

#### 複数行

```html
<div class="mdc-text-field mdc-text-field--textarea mdc-text-field--no-label">
  <textarea class="mdc-text-field__input" rows="8" cols="40" aria-label="Label"></textarea>
  <div class="mdc-notched-outline">
    <div class="mdc-notched-outline__leading"></div>
    <div class="mdc-notched-outline__trailing"></div>
  </div>
</div>
```

### ヘルプテキスト付きテキスト欄

ヘルプテキストは補足の情報や検証のメッセージをユーザーに対して提供します。デフォルトではテキスト欄がフォーカスされたときに表示され、フォーカスを失たときに非表示になりますが、常に表示させておくこともできます。ヘルプテキストは `.mdc-text-field` の直接の兄弟要素である `.mdc-text-field-helper-line` 要素の中に書く必要があります。ヘルプテキストを使う上でのより詳細な情報は [ここ](helper-text/) を参照してください。

```html
<div class="mdc-text-field">
  <input type="text" id="my-text-field" class="mdc-text-field__input">
  <label class="mdc-floating-label" for="my-text-field">My Label</label>
  <div class="mdc-line-ripple"></div>
</div>
<div class="mdc-text-field-helper-line">
  <div class="mdc-text-field-helper-text">helper text</div>
</div>
```

### 文字数カウンター付きテキスト欄

文字数に制限がある場合、文字数カウンターが使われます。これは文字数制限の上限と入力された文字数の比率を表示するものです。文字数カウンターは `.mdc-text-field` の直接の兄弟要素である `.mdc-text-field-helper-line` 要素の中に書く必要があります。文字数カウンターの使用に関するより多くの情報は [ここ](character-counter/) を参照してください。

```html
<div class="mdc-text-field">
  <input type="text" id="my-text-field" class="mdc-text-field__input" maxlength="10">
  <label class="mdc-floating-label" for="my-text-field">My Label</label>
  <div class="mdc-line-ripple"></div>
</div>
<div class="mdc-text-field-helper-line">
  <div class="mdc-text-field-character-counter">0 / 10</div>
</div>
```

### 文字数カウンター付き複数行テキスト欄 (Textarea)

複数行テキスト欄 (textarea) での文字数カウンターでは、テキスト欄のコンポーネント内にカウンターを表示するため、レイアウト構造が少々異なります。

```html
<div class="mdc-text-field mdc-text-field--textarea">
  <div class="mdc-text-field-character-counter">0 / 140</div>
  <textarea id="textarea" class="mdc-text-field__input" rows="8" cols="40" maxlength="140"></textarea>
  <div class="mdc-notched-outline">
    <div class="mdc-notched-outline__leading"></div>
    <div class="mdc-notched-outline__notch">
      <label for="textarea" class="mdc-floating-label">Textarea Label</label>
    </div>
    <div class="mdc-notched-outline__trailing"></div>
  </div>
</div>
```

ヘルプテキストと文字数カウンターは独立して共存できるテキスト欄のオプションサブコンポーネントです。適切なレイアウトのために `.mdc-text-field` 要素と `.mdc-text-field-helper-line` 要素は同じ幅にすることを推奨します。

### 先頭と末尾のアイコン

双方向ターゲットとしてだけでなく視覚インジケーターとして MDC Text Fields のデフォルトのもしくはアウトライン内部に先頭と末尾のアイコンを追加することができます。アイコンを使う上でのより詳細な情報は [ここ](icon/) を参照してください。

### HTML5 バリデーション

`MDCTextFieldFoundation` は HTML5 フォームバリデーション API の提供する `:invalid` と `:required` 属性を使用した入力の妥当性検証の機能を持っています。

```html
<div class="mdc-text-field">
  <input type="password" id="pw" class="mdc-text-field__input" required minlength=8>
  <label for="pw" class="mdc-floating-label">Password</label>
  <div class="mdc-line-ripple"></div>
</div>
```

`MDCTextFieldFoundation` は required 属性が設定されていると自動的にラベルにアスタリスクを追加します。

### 入力済みのテキスト欄

値をすでに持っている JS を利用するテキスト欄を扱うときには、`mdc-floating-label--float-above` 修飾クラスをもつ `mdc-floating-label` を記述してください。そうすればラベルはテキスト欄のところから離れ、Flash Of Un-styled Content (**FOUC**) を防ぐことができます。（訳注: [Flash Of Un-styled Content](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) はスタイルの設定が完全でない状態でレンダリングされてしまうこと。クラスが正しく設定されていないと値のあるテキスト欄の上にラベルが重なった状態で表示されてしまうので、その状態を避けるために、クラスを設定する必要がある、ということを言っている。）

```html
<div class="mdc-text-field">
  <input type="text" id="pre-filled" class="mdc-text-field__input" value="Pre-filled value">
  <label class="mdc-floating-label mdc-floating-label--float-above" for="pre-filled">
    Label in correct place
  </label>
  <div class="mdc-line-ripple"></div>
</div>
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-text-field` | 必須。
`mdc-text-field--outlined` | アウトラインされたテキスト欄として表示する。
`mdc-text-field--fullwidth` | フル幅のテキスト欄として表示する。
`mdc-text-field--textarea` | テキスト欄が `<textarea>` であることを表す。
`mdc-text-field--disabled` | 無効なテキスト欄として表示する。
`mdc-text-field--dense` | 高密度のテキスト欄として表示する。\*
`mdc-text-field--with-leading-icon` | 先頭にアイコンのあるテキスト欄として表示する。
`mdc-text-field--with-trailing-icon` | 末尾にアイコンのあるテキスト欄として表示する。
`mdc-text-field--focused` | フォーカスを持つテキスト欄として表示する。
`mdc-text-field--no-label` | ラベルのないテキスト欄として表示する。
`mdc-text-field-helper-line` | ヘルプテキストと文字数カウンタ要素のコンテナのスタイル。

#### 非推奨のお知らせ

\* テキスト欄の `--dense` のタイプは将来のリリースで削除されます。詳細は [github issue](https://github.com/material-components/material-components-web/issues/4142) を参照してください。

### Sass ミキシン

テキスト欄の任意の部分の色をカスタマイズするには以下のミキシンを使用します。フォーカスのないテキスト欄を選択するには `.foo-text-field:not(.mdc-text-field--focused)`、フォーカスのあるテキスト欄を選択するには `.foo-text-field.mdc-text-field--focused` のような CSS セレクター内にこれらのミキシンを適用することを推奨しています。テキスト欄を無効にするには `.foo-text-field.mdc-text-field--invalid` のような CSS セレクター内にこれらのミキシンを適用します。

> <em>注意</em>: `mdc-line-ripple-color` ミキシンは非フォーカスクラス（`foo-text-field:not(.mdc-text-field--focused)`）から適用する必要があります。

#### すべてのテキスト欄のためのミキシン

ミキシン | 説明
--- | ---
`mdc-text-field-ink-color($color)` | テキスト欄に入力されたテキストの色を設定する。
`mdc-text-field-label-color($color)` | ラベルのテキスト色を設定する。
`mdc-text-field-caret-color($color)` | テキスト欄のカーソルキャレットの色を設定する。

#### 塗りつぶされたテキスト欄のためのミキシン

ミキシン | 説明
--- | ---
`mdc-text-field-shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にボックス型テキスト欄を設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`mdc-text-field-fill-color($color)` | テキスト欄の背景色を設定する。
`mdc-text-field-bottom-line-color($color)` | アウトラインされたものとテキストエリアを除いてテキスト欄下部の線の色を設定する。
`mdc-text-field-hover-bottom-line-color($color)` | アウトラインされたものとテキストエリアを除いてホバー時のテキスト欄下部の線の色を設定する。
`mdc-text-field-line-ripple-color($color)` | テキスト欄のデフォルトのラインリップルの色を設定する。

#### アウトラインされたテキスト欄のためのミキシン

ミキシン | 説明
--- | ---
`mdc-text-field-focused-outline-color($color)` | アウトラインされたテキスト欄がフォーカスされているときの境界線の色を設定する。
`mdc-text-field-hover-outline-color($color)` | アウトラインされたテキスト欄の境界線のホバー時の色を設定する。
`mdc-text-field-outline-color($color)` | アウトラインされたテキスト欄の境界線の色を設定する。
`mdc-text-field-outline-shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にアウトラインされたテキスト欄を設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。

#### テキストエリアのためのミキシン

ミキシン | 説明
--- | ---
`mdc-text-field-textarea-shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にテキストエリアを設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`mdc-text-field-textarea-fill-color($color)` | textarea の背景色を設定する。
`mdc-text-field-textarea-stroke-color($color)` | textarea の境界線の色を設定する。


#### フル幅のテキスト欄のためのミキシン

Mixin | Description
--- | ---
`mdc-text-field-fullwidth-bottom-line-color($color)` | フル幅のテキスト欄のボトムラインの色を設定する。

## `MDCTextField` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`value` | `string` | ファンデーションの `getValue`/`setValue` メソッドの代替
`disable` | `boolean` | ファンデーションの `isDisabled`/`setDisabled` メソッドの代替
`useNativeValidation` | `boolean` (書込専用) | ファンデーションの `setUseNativeValidation` メソッドの代替
`valid` | `boolean` | ファンデーションの `isValid`/`setValid` の代替
`helperTextContent` | `string` (書込専用) | ファンデーションの `setHelperTextContent` の設定時のおける代替
`ripple` | `MDCRipple` (書込専用) | `MDCTextField` が初期化したルート要素のための `MDCRipple` インスタンス。これはデフォルトのテキスト欄にのみ適用され、それ以外のタイプでは `null` が設定される
`leadingIconAriaLabel` | `string` (書込専用) | ファンデーションの `setLeadingIconAriaLabel` メソッドの代替
`trailingIconAriaLabel` | `string` (書込専用) | ファンデーションの `setTrailingIconAriaLabel` メソッドの代替
`leadingIconContent` | `string` (書込専用) | ファンデーションの `setLeadingIconContent` メソッドの代替
`trailingIconContent` | `string` (書込専用) | ファンデーションの `setTrailingIconContent` メソッドの代替

上に挙げたものに加えて、以下のプロパティが同名の `input` 要素のプロパティの代替として用意されている。

* `required`
* `pattern`
* `minLength`
* `maxLength`
* `min`
* `max`
* `step`

メソッド | 説明
--- | ---
`focus() => void` | `input` もしくは `textarea` 要素にフォーカスする。
`layout() => void` | すべてのサブ要素の大きさと位置を調整する。

## Web フレームワークでの使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のテキスト欄を作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCTextFieldAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`hasClass(className: string) => boolean` | ルート要素に与えられたクラス名が含まれているときに true を返す。
`registerTextFieldInteractionHandler(evtType: string, handler: EventListener) => void` | ルート要素に与えたイベントのイベントハンドラーを登録する。
`deregisterTextFieldInteractionHandler(evtType: string, handler: EventListener) => void` | ルート要素から与えたイベントのイベントハンドラーの登録を解除する。
`registerInputInteractionHandler(evtType: string, handler: EventListener) => void` | ネイティブな input 要素に与えたイベントのイベントリスナーを登録する。
`deregisterInputInteractionHandler(evtType: string, handler: EventListener) => void` | ネイティブな input 要素から与えたイベントのイベントリスナーの登録を解除する。
`registerValidationAttributeChangeHandler(handler: (attributeNames: string[]) => void) => MutationObserver` | 検証属性の変更のイベントリスナーを input 要素に対して登録する。リスナーは属性変更のリストを受け取る。
`deregisterValidationAttributeChangeHandler(!MutationObserver) => void` | 検証属性の変更のオブザーバーとの接続を input 要素から削除する。
`getNativeInput() => NativeInputType \| null` | ネイティブな input 要素の代わりになる類似した API を持つオブジェクトを返す。[types.ts](types.ts) 参照。
`isFocused() => boolean` | 入力欄にフォーカスがあるかどうかを返す。
`shakeLabel(shouldShake: boolean) => void` | 入力された値が無効であることを示すためにラベルを震わせる。
`floatLabel(shouldFloat: boolean) => void` | ラベルを上に移動させる。
`hasLabel() => boolean` | テキスト欄がラベルを持っているかどうかを調べる。
`getLabelWidth() => number` | ラベル要素の幅をピクセルで返す。
`activateLineRipple() => void` | テキスト欄のラインリップルサブ要素を有効にする。
`deactivateLineRipple() => void` | テキスト欄のラインリップルサブ要素を無効にする。
`setLineRippleTransformOrigin(normalizedX: number) => void` | テキスト欄のラインリップル要素（あれば）の CSS の `transform-origin` 属性を与えられた値に設定する。
`hasOutline() => boolean` | テキスト欄にアウトラインサブ要素があるかどうかを調べる。
`notchOutline(labelWidth: number) => void` | テキスト欄のノッチ付きアウトラインサブ要素の幅を設定する。
`closeOutline() => void` | テキスト欄のノッチ付きアウトランサブ要素を閉じる。

#### `MDCTextFieldAdapter.getNativeInput()`

ネイティブな input 要素の代わりになる類似した API を持つオブジェクトを返します。私たちはコード内で値を変えることはありませんが、disabled プロパティは更新します。もしあなたがこのメソッドの実装でダックタイピングをを選択するなら、このことを念頭に置いておく必要があります。また、このメソッドは null を返しても構わないことを覚えておいてください。その場合でもファンデーションは適切に動作します。

#### `MDCTextFieldAdapter.getIdleOutlineStyleValue(propertyName: string)`

`propertyName` に与えられた CSS プロパティ値を計算して返します。素の実装は `getComputedStyle(...).getPropertyValue(propertyName)` を通じて処理がなされます。

### `MDCTextFieldFoundation`

プロパティ | 値の型 | 説明
--- | --- | ---
`shouldFloat` | `boolean` (読取専用) | ラベルが上に移動すべきかどうかを調べる。
`shouldShake` | `boolean` (読取専用) | ラベルが震わせるべきかどうかを調べる。

メソッド | 説明
--- | ---
`getValue() => string` | input 要素の値を返す。
`setValue(value: string)` | input 要素の値を設定する。
`setUseNativeValidation(useNativeValidation: boolean)` | ネイティブな HTML の検証を使う（`true`、初期値）か、スタイルを更新によるカスタム検証使う（`false`）かを設定する。
`setValid(isValid: boolean)` | カスタム検証を設定し、それにそったスタイルで更新する。`setUseNativeValidation(false)` も呼ばない限り、ネイティブ検証が引き続き利用されることに気を付けること。
`isValid() => boolean` | コンポーネントの現在の検証状態（ネイティブもしくはカスタムのいずれか、`setUseNativeValidation()` がどのように設定されたかによる）を返す。
`isDisabled() => boolean` | input 要素が無効かどうかを返す。
`setDisabled(disabled: boolean) => void` | input 要素の無効かどうか状態を更新する。
`handleTextFieldInteraction(evt: Event) => void` | Text Field コンポーネント内で発生した click イベントと keydown イベントを処理する。
`handleInput() => void` | text と textarea の input イベントを処理する。
`handleValidationAttributeChange(attributesList: !Array<string>) => void` | 属性変更の検証を処理する。
`activateFocus() => void` | Text Field をフォーカス状態にする。通常は input の focus イベントの処理中に呼ばれる。
`deactivateFocus() => void` | Text Field をフォーカス状態を失った状態にする。通常は input の blur イベントの処理中に呼ばれる。
`setHelperTextContent(content: string) => void` | ヘルプテキストの内容を設定する。
`setLeadingIconAriaLabel(label: string) => void` | 先頭のアイコンの領域ラベルを設定する。
`setLeadingIconContent(content: string) => void` | 先頭のアイコンのテキストコンテンツを設定する。
`setTrailingIconAriaLabel(label: string) => void` | 末尾のアイコンの領域ラベルを設定する。
`setTrailingIconContent(content: string) => void` | 末尾のアイコンのテキストコンテンツを設定する。
`notchOutline(openNotch: boolean) => void` | ノッチ化したアウトラインを開く、もしくは閉じる。
`setTransformOrigin(evt: TouchEvent \| MouseEvent) => void` | ラインリップルのアニメーションがユーザーがクリックされた位置から始まるように、ラインリップルの transform origin を設定する。
`autoCompleteFocus() => void` | 入力値がプログラム的に変更された（つまり、ユーザーの操作なしで）ときにテキスト欄のフォーカス状態をアクティブにする。

`MDCTextFieldFoundation` は複数のオプションのサブ要素 - ヘルパーテキストとアイコン - をサポートしています。これらのサブ要素のファンデーションはコンストラクターの引数として `MDCTextFieldFoundation` に渡さなくてはなりません。
