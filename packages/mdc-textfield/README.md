<!--docs:
title: "Text Field"
layout: detail
section: components
iconId: text_field
path: /catalog/input-controls/text-field/
-->

# Text Field

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/text-field.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/textfields.png" width="240" alt="Text fields screenshot">
  </a>
</div>-->

Text Field はユーザのテキストの入力、編集、選択に対応しています。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/text-fields.html">マテリアルデザインガイドライン: テキスト欄</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/text-field.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install --save @material/textfield
```

## 使用法

### HTML 構造

```html
<div class="mdc-text-field">
  <input type="text" id="my-text-field" class="mdc-text-field__input">
  <label class="mdc-text-field__label" for="my-text-field">Hint text</label>
  <div class="mdc-text-field__bottom-line"></div>
</div>
```

#### HTML5 バリデーション

`MDCTextFieldFoundation` は HTML5 フォームバリデーション API の提供する `:invalid` と `:required` 属性を使用した入力の妥当性検証の機能を持っています。

```html
<div class="mdc-text-field">
  <input type="password" id="pw" class="mdc-text-field__input" required minlength=8>
  <label for="pw" class="mdc-text-field__label">Password</label>
  <div class="mdc-text-field__bottom-line"></div>
</div>
```

`MDCTextFieldFoundation` は required 属性が設定されていると自動的にラベルにアスタリスクを追加します。

#### 入力済みのテキスト欄

値をすでに持っている JS を利用するテキスト欄を扱うときには、`mdc-text-field__label--float-above` 修飾クラスをもつ `mdc-text-field__label` と `mdc-text-field--upgraded` 修飾クラスをもつ `mdc-text-field` を記述してください。そうすればラベルはテキスト欄のところから離れ、Flash Of Un-styled Content (**FOUC**) を防ぐことができます。（訳注: [Flash Of Un-styled Content](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) はスタイルの設定が完全でない状態でレンダリングされてしまうこと。クラスが正しく設定されていないと値のあるテキスト欄の上にラベルが重なった状態で表示されてしまうので、その状態を避けるために、クラスを設定する必要がある、ということを言っている。）

```html
<div class="mdc-text-field mdc-text-field--upgraded">
  <input type="text" id="pre-filled" class="mdc-text-field__input" value="Pre-filled value">
  <label class="mdc-text-field__label mdc-text-field__label--float-above" for="pre-filled">
    Label in correct place
  </label>
  <div class="mdc-text-field__bottom-line"></div>
</div>
```
> <em>注意</em>: <em>JavaScript を利用するときには</em> `mdc-text-field` の内側に `mdc-text-field__label` を配置してください。そうでないときは、ラベルは次項で見るように `mdc-text-field` の外側に置かなくてはなりません。

#### CSS のみでの使用

```html
<label for="text-field-no-js">TextField with no JS: </label>
<div class="mdc-text-field">
  <input type="text" id="text-field-no-js" class="mdc-text-field__input" placeholder="Hint text">
</div>
```

> <em>注意</em>: <em>JavaScript を使用せず、 `mdc-text-field--box` もしくは `mdc-text-field--outlined` を使うときは</em> `mdc-text-field` の内側に `mdc-text-field__bottom-line`、`mdc-text-field__outline`、`mdc-text-field__idle-outline` を使わないでください。ボトムラインとアウトラインは CSS のみによるテキスト欄の DOM 構造の一部として入れてはいけません。

```html
<label for="css-only-text-field-box">Your name:</label>
<div class="mdc-text-field mdc-text-field--box">
  <input type="text" class="mdc-text-field__input" id="css-only-text-field-box" placeholder="Name">
</div>
```

#### フル幅のテキスト欄

```html
<div class="mdc-text-field mdc-text-field--fullwidth">
  <input class="mdc-text-field__input"
         type="text"
         placeholder="Full-Width Text Field"
         aria-label="Full-Width Text Field">
</div>
```

> <em>注意</em>: `mdc-text-field--fullwidth` の内部で `mdc-text-field__label` を使わないでください。フル幅のテキスト欄の DOM 構造の一部としてラベルを含めることはできません。

#### 複数行テキスト欄

```html
<div class="mdc-text-field mdc-text-field--textarea">
  <textarea id="textarea" class="mdc-text-field__input" rows="8" cols="40"></textarea>
  <label for="textarea" class="mdc-text-field__label">Textarea Label</label>
</div>
```

> <em>注意</em>: JavaScript を使うときには、`mdc-text-field--textarea` の内部では `mdc-text-field__label` のみを使ってください。そうでないときは以下のように `placeholder` 属性を使ってください。

```html
<div class="mdc-text-field mdc-text-field--textarea">
  <textarea id="textarea-css-only"
    class="mdc-text-field__input"
    rows="8"
    cols="40"
    placeholder="Enter something about yourself"></textarea>
</div>
```

#### 無効な状態

`mdc-text-field` を無効にするときは `<input>` に `disabled` 属性を加えてください。`mdc-text-field` に `mdc-text-field--disabled` を追加する必要もあります。

```html
<div class="mdc-text-field mdc-text-field--disabled">
  <input type="text" id="disabled-text-field" class="mdc-text-field__input" disabled>
  <label class="mdc-text-field__label" for="disabled-text-field">Disabled text field</label>
  <div class="mdc-text-field__bottom-line"></div>
</div>
```

#### アウトライン

```html
<div class="mdc-text-field mdc-text-field--outlined">
  <input type="text" id="tf-outlined" class="mdc-text-field__input">
  <label for="tf-outlined" class="mdc-text-field__label">Your Name</label>
  <div class="mdc-text-field__outline">
    <svg>
      <path class="mdc-text-field__outline-path"/>
    </svg>
  </div>
  <div class="mdc-text-field__idle-outline"></div>
</div>
```

アウトラインサブコンポーネントを使うにあたり、より詳細な情報は [ここ](outline/) を参照してください。

> <em>注意</em>: <em>`mdc-text-field--outlined` を使うときは</em>、`mdc-text-field` の内部で `mdc-text-field__bottom-line` を使わないでください。ボトムラインはアウトラインの付いたテキスト欄の DOM 構造の一部として入れてはいけません。

#### ヘルプテキスト

ヘルプテキストは補足の情報や検証のメッセージをユーザに対して提供します。デフォルトではテキスト欄がフォーカスされたときに表示され、フォーカスを失たときに非表示になりますが、常に表示させておくこともできます。ヘルプテキストを使う上でのより詳細な情報は [ここ](helper-text/) を参照してください。

#### 先頭と末尾のアイコン

双方向ターゲットとしてだけでなく視覚インジケータとして MDC Text Fields に先頭と末尾のアイコンを追加することができます。アイコンを使う上でのより詳細な情報は [ここ](icon/) を参照してください。

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-text-field` | 必須
`mdc-text-field--upgraded` | テキスト欄がアップグレードされたことを表す。通常は JavaScript によってアップグレード処理がなされる。
`mdc-text-field--box` | ボックス型のテキスト欄として表示する。
`mdc-text-field--outlined` | アウトラインされたテキスト欄として表示する。
`mdc-text-field--fullwidth` | フル幅のテキスト欄として表示する。
`mdc-text-field--textarea` | テキスト欄が `<textarea>` であることを表す。
`mdc-text-field--disabled` | 無効なテキスト欄として表示する。
`mdc-text-field--dense` | 高密度のテキスト欄として表示する。
`mdc-text-field--with-leading-icon` | 先頭にアイコンのあるテキスト欄として表示する。
`mdc-text-field--with-trailing-icon` | 末尾にアイコンのあるテキスト欄として表示する。
`mdc-text-field--focused` | フォーカスを持つテキスト欄として表示する。

### Sass ミキシン

テキスト欄の任意の部分の色をカスタマイズするには以下のミキシンを使用します。フォーカスのないテキスト欄を選択するには `.foo-text-field:not(.mdc-text-field--focused)`、フォーカスのあるテキスト欄を選択するには `.foo-tab.mdc-text-field--focused` のような CSS セレクタ内にこれらのミキシンを適用することを推奨しています。テキスト欄を無効にするには `.foo-text-field.mdc-text-field--invalid` のような CSS セレクタ内にこれらのミキシンを適用します。

> <em>注意</em>: `mdc-text-field-focused-bottom-line-color` ミキシンは非フォーカスクラス（`foo-text-field:not(.mdc-tab--focused)`）から適用する必要があります。

ミキシン | 説明
--- | ---
`mdc-text-field-box-corner-radius($radius)` | ボックス型テキスト欄の角の半径を設定する。
`mdc-text-field-textarea-corner-radius($radius)` | `<textarea>` の角の半径を設定する。
`mdc-text-field-bottom-line-color($color)` | テキスト欄のデフォルトの下線の色を設定する。
`mdc-text-field-hover-bottom-line-color($color)` | テキスト欄の下線のホバー時の色を設定する。
`mdc-text-field-focused-bottom-line-color($color)` | テキスト欄がフォーカスを得たときの下線のリップルの色を設定する。
`mdc-text-field-ink-color($color)` | テキスト欄の入力されたテキストの色を設定する。
`mdc-text-field-label-color($color)` | テキスト欄のラベルの色を設定する。

### `MDCTextField`

JavaScript をインポートする方法の詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

プロパティ | 型 | 説明
--- | --- | ---
`value` | String | ファンデーションの `getValue`/`setValue` メソッドの代替
`disable` | Boolean | ファンデーションの `isDisabled`/`setDisabled` メソッドの代替
`valid` | Boolean | ファンデーションの `isValid`/`setValid` の代替
`required` | Boolean | ファンデーションの `isRequired`/`setRequired` の代替
`helperTextContent` | String | ファンデーションの `setHelperTextContent` の設定時のおける代替
`ripple` | `MDCRipple` | `MDCTextField` が初期化したルート要素のための `MDCRipple` インスタンス

メソッド | 説明
--- | ---
`layout() => void` | すべてのサブ要素の大きさと位置を調整する。

#### `MDCTextField.ripple`

`MDCRipple` のインスタンス。ルート要素に `mdc-text-field--box` が与えられているとき、ルート要素には `MDCRipple` インスタンスが設定されます。ルート要素に `mdc-text-field--outlined` が与えられているとき、`mdc-text-field__outline` 要素には `MDCRipple` インスタンスが設定されます。どちらでもないときはこのフィールドには `null` が設定されます。

### `MDCTextFieldAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`hasClass(className: string) => boolean` | ルート要素に与えられたクラス名が含まれているときに true を返す。
`registerTextFieldInteractionHandler(evtType: string, handler: EventListener)` => void | ルート要素に与えたイベントのイベントハンドラを登録する。
`deregisterTextFieldInteractionHandler(evtType: string, handler: EventListener)` => void | ルート要素から与えたイベントのイベントハンドラの登録を解除する。
`registerInputInteractionHandler(evtType: string, handler: EventListener)` => void | ネイティブな input 要素に与えたイベントのイベントリスナーを登録する。
`deregisterInputInteractionHandler(evtType: string, handler: EventListener)` => void | ネイティブな input 要素から与えたイベントのイベントリスナーの登録を解除する。
`registerBottomLineEventHandler(evtType: string, handler: EventListener)` => void | ボトムラインの要素に与えたイベントのイベントリスナーを登録する。
`deregisterBottomLineEventHandler(evtType: string, handler: EventListener)` => void | ボトムラインの要素から与えたイベントのイベントリスナーの登録を解除する。
`getNativeInput() => {value: string, disabled: boolean, badInput: boolean, checkValidity: () => boolean}?` | ネイティブな input 要素の代わりになる類似した API を持つオブジェクトを返す。
`isFocused() => boolean` | 入力欄にフォーカスがあるかどうかを返す。
`isRtl() => boolean` | ルート要素の方向に RTL が設定されているかどうかを返す。

#### `MDCTextFieldAdapter.getNativeInput()`

ネイティブな input 要素の代わりになる類似した API を持つオブジェクトを返します。返されるオブジェクトは `value`、`disabled`、`badInput` の各プロパティと `checkValidity()` 関数を持っていなければなりません。私たちはコード内で値を変えることはありませんが、disabled プロパティは更新します。もしあなたがこのメソッドの実装でダックタイピングをを選択するなら、このことを念頭に置いておく必要があります。また、このメソッドは null を返しても構わないことを覚えておいてください。その場合でもファンデーションは適切に動作します。

#### `MDCTextFieldAdapter.getIdleOutlineStyleValue(propertyName: string)`

`propertyName` に与えられた CSS プロパティ値を計算して返します。素の実装は `getComputedStyle(...).getPropertyValue(propertyName)` を通じて処理がなされます。

### `MDCTextFieldFoundation`

メソッド | 説明
--- | ---
`getValue() => string` | input 要素の値を返す。
`setValue(value: string)` | input 要素の値を設定する。
`isValid() => boolean` | カスタムバリデーションが設定されていればその値を返す。そうでないときはネイティブなバリデーションチェックの結果を返す。
`setValid(isValid: boolean)` | カスタムバリデーションを設定する。一度設定するとネイティブなバリデーションチェックは無効になる。
`isDisabled() => boolean` | input 要素が無効かどうかを返す。
`setDisabled(disabled: boolean) => void` | input 要素の無効かどうか状態を更新する。
`isRequired() => boolean` | input 要素が必須であるかどうかを返す。
`setRequired(isRequired: boolean)` | input 要素が必須であるかどうかを設定する。
`handleTextFieldInteraction(evt: Event) => void` | Text Field コンポーネント内で発生したクリックイベントとキーダウンイベントを処理する。
`activateFocus() => void` | Text Field をフォーカス状態にする。通常は input の focus イベントの処理中に呼ばれる。
`deactivateFocus() => void` | Text Field をフォーカス状態を失った状態にする。通常は input の blur イベントの処理中に呼ばれる。
`handleBottomLineAnimationEnd(evt: Event) => void` | ボトムラインのアニメーションの終了処理を行い、アニメーションが終わるまで待たなくてはいけない処理を実行する。transition-end イベントの処理を想定している。
`setHelperTextContent(content: string) => void` | ヘルプテキストの内容を設定する。
`updateOutline() => void` |アウトラインされたテキスト欄のフォーカスされたアウトラインを更新する。

`MDCTextFieldFoundation` は複数のオプションのサブ要素 - ボトムライン、ヘルプテキスト、アイコン、ラベル、アウトライン - をサポートしています。これらのサブ要素のファンデーションはコンストラクタの引数として `MDCTextFieldFoundation` に渡さなくてはなりません。
