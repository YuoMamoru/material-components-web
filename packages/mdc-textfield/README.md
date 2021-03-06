<!--docs:
title: "Text field"
layout: detail
section: components
excerpt: "MDC Web text field"
iconId: text_field
path: /catalog/input-controls/text-field/
-->

# Text field

[Text fields](https://material.io/components/text-fields) はユーザーにテキストの入力と編集をさせます。

さらなる情報は [API](#api) ドキュメントを参照してください。

テキスト欄クラスには以下のタイプが含まれています。

* [塗られたテキスト](#filled-text)
* [枠付きテキスト](#outlined-text)

<img src="images/text-field-generic.png" alt="Text field examples of both filled and outlined types, and each type showing both inactive and focused states.">

## テキスト欄を使う

テキスト欄は UI 内でユーザーのテキスト入力をサポートします。一般的にはフォームやダイアログの中にでてきます。

### インストール

```
npm install @material/textfield
```

### スタイル

```scss
@use "@material/floating-label/mdc-floating-label";
@use "@material/line-ripple/mdc-line-ripple";
@use "@material/notched-outline/mdc-notched-outline";
@use "@material/textfield";

@include textfield.core-styles;
```

### JavaScript のインスタンス化

```js
import {MDCTextField} from '@material/textfield';

const textField = new MDCTextField(document.querySelector('.mdc-text-field'));
```

**注意: JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。**

## <a name="filled-text"></a>塗られたテキスト欄

[塗られたテキスト欄](https://material.io/components/text-fields/#filled-text-field) は枠付きテキスト欄より強調されており、そのほかのコンテンツやコンポーネントに囲まれても目立ちます。

### 塗られたテキスト欄の例

```html
<label class="mdc-text-field mdc-text-field--filled">
  <span class="mdc-text-field__ripple"></span>
  <span class="mdc-floating-label" id="my-label-id">Hint text</span>
  <input class="mdc-text-field__input" type="text" aria-labelledby="my-label-id">
  <span class="mdc-line-ripple"></span>
</label>
```

## <a name="outlined-text"></a>枠付きテキスト欄

[枠付きテキスト欄](https://material.io/components/text-fields/#outlined-text-field) は塗られたテキスト欄より強調されません。多くのテキスト欄が一緒に配置されるフォームのようなところで使えば、強調を抑えてレイアウトを簡素化するにに役立ちます。

### 枠付きテキスト欄の例

```html
<label class="mdc-text-field mdc-text-field--outlined">
  <span class="mdc-notched-outline">
    <span class="mdc-notched-outline__leading"></span>
    <span class="mdc-notched-outline__notch">
      <span class="mdc-floating-label" id="my-label-id">Your Name</span>
    </span>
    <span class="mdc-notched-outline__trailing"></span>
  </span>
  <input type="text" class="mdc-text-field__input" aria-labelledby="my-label-id">
</label>
```

ノッチのある枠付きサブコンポーネントの使用についてのさらなる情報は [ここ](../mdc-notched-outline/) を参照してください。

**注意: <em>`mdc-text-field--outlined` を使うときは</em>、`mdc-text-field` の内部で `mdc-line-ripple` を使わないでください。ラインリップルはアウトラインの付いたテキスト欄の DOM 構造の一部として入れてはいけません。**

## その他のバリエーション

### テキストエリア

#### 幅いっぱい

```html
<label class="mdc-text-field mdc-text-field--filled mdc-text-field--textarea mdc-text-field--no-label">
  <span class="mdc-text-field__ripple"></span>
  <span class="mdc-text-field__resizer">
    <textarea class="mdc-text-field__input" rows="8" cols="40" aria-label="Label"></textarea>
  </span>
  <span class="mdc-line-ripple"></span>
</label>
```

#### 枠付き

```html
<label class="mdc-text-field mdc-text-field--outlined mdc-text-field--textarea mdc-text-field--no-label">
  <span class="mdc-notched-outline">
    <span class="mdc-notched-outline__leading"></span>
    <span class="mdc-notched-outline__trailing"></span>
  </span>
  <span class="mdc-text-field__resizer">
    <textarea class="mdc-text-field__input" rows="8" cols="40" aria-label="Label"></textarea>
  </span>
</label>
```

**注意: `mdc-text-field__resizer` 要素はサイズ変更のできないテキストエリアでは省略できます。**

### ラベルなしテキスト欄

テキスト欄の横に別の明確な文言表示がすでにあるなら、テキスト欄にラベルは必要ではありません。そのような場合、クラス名 `mdc-text-field--no-label` を追加し、ラベル要素を構成から削除してください。

#### 幅いっぱい

```html
<label class="mdc-text-field mdc-text-field--filled mdc-text-field--no-label">
  <span class="mdc-text-field__ripple"></span>
  <input class="mdc-text-field__input" type="text" placeholder="Placeholder text" aria-label="Label">
  <span class="mdc-line-ripple"></span>
</label>
```

#### 枠付き

```html
<label class="mdc-text-field mdc-text-field--outlined mdc-text-field--no-label">
  <span class="mdc-notched-outline">
    <span class="mdc-notched-outline__leading"></span>
    <span class="mdc-notched-outline__trailing"></span>
  </span>
  <input class="mdc-text-field__input" type="text" aria-label="Label">
</label>
```

#### 複数行

```html
<label class="mdc-text-field mdc-text-field--outlined mdc-text-field--textarea mdc-text-field--no-label">
  <span class="mdc-notched-outline">
    <span class="mdc-notched-outline__leading"></span>
    <span class="mdc-notched-outline__trailing"></span>
  </span>
  <span class="mdc-text-field__resizer">
    <textarea class="mdc-text-field__input" rows="8" cols="40" aria-label="Label"></textarea>
  </span>
</label>
```

### 無効なテキスト欄

テキスト欄を無効にするには、`<input>` 要素に `disabled` 属性を追加し、`mdc-text-field` 要素に `mdc-text-field--disabled` クラスを追加します。

```html
<label class="mdc-text-field mdc-text-field--filled mdc-text-field--disabled">
  <span class="mdc-text-field__ripple"></span>
  <span class="mdc-floating-label" id="my-label-id">Disabled text field</span>
  <input class="mdc-text-field__input" type="text" aria-labelledby="my-label-id" disabled>
  <span class="mdc-line-ripple"></span>
</label>
```

### ヘルプテキスト付きテキスト欄

ヘルプテキストは補足の情報や検証のメッセージをユーザーに対して提供します。デフォルトではテキスト欄がフォーカスされたときに表示され、フォーカスを失たときに非表示になりますが、常に表示させておくこともできます。ヘルプテキストは `.mdc-text-field` の直接の兄弟要素である `.mdc-text-field-helper-line` 要素の中に書く必要があります。ヘルプテキストを使う上でのより詳細な情報は [ここ](helper-text/) を参照してください。

```html
<label class="mdc-text-field mdc-text-field--filled">
  <span class="mdc-text-field__ripple"></span>
  <span class="mdc-floating-label" id="my-label-id">My Label</span>
  <input class="mdc-text-field__input" type="text"
         aria-labelledby="my-label-id"
         aria-controls="my-helper-id"
         aria-describedby="my-helper-id">
  <span class="mdc-line-ripple"></span>
</label>
<div class="mdc-text-field-helper-line">
  <div class="mdc-text-field-helper-text" id="my-helper-id" aria-hidden="true">helper text</div>
</div>
```

### 文字数カウンター付きテキスト欄

文字数に制限がある場合、文字数カウンターが使われます。これは文字数制限の上限と入力された文字数の比率を表示するものです。文字数カウンターは `.mdc-text-field` の直接の兄弟要素である `.mdc-text-field-helper-line` 要素の中に書く必要があります。文字数カウンターの使用に関するより多くの情報は [ここ](character-counter/) を参照してください。

```html
<label class="mdc-text-field mdc-text-field--filled">
  <span class="mdc-text-field__ripple"></span>
  <span class="mdc-floating-label" id="my-label-id">My Label</span>
  <input class="mdc-text-field__input" type="text" aria-labelledby="my-label-id" maxlength="10">
  <span class="mdc-line-ripple"></span>
</label>
<div class="mdc-text-field-helper-line">
  <div class="mdc-text-field-character-counter">0 / 10</div>
</div>
```

### 文字数カウンター付き複数行テキスト欄 (textarea)

文字数カウンターはヘルパー行に含めることにより、textarea に付属させることができます。この場合、カウンターは textarea の下、ヘルパーテキストに隣接して表示されます。

```html
<label class="mdc-text-field mdc-text-field--textarea">
  <span class="mdc-notched-outline">
    <span class="mdc-notched-outline__leading"></span>
    <span class="mdc-notched-outline__notch">
      <span class="mdc-floating-label" id="my-label-id">Textarea Label</span>
    </span>
    <span class="mdc-notched-outline__trailing"></span>
  </span>
  <span class="mdc-text-field__resizer">
    <textarea class="mdc-text-field__input" aria-labelledby="my-label-id" rows="8"
      cols="40" maxlength="140"></textarea>
  </span>
</label>
<div class="mdc-text-field-helper-line">
  <div class="mdc-text-field-character-counter">0 / 140</div>
</div>
```
あるいは、文字数カウンターを textarea の下入れ、`mdc-text-field--with-internal-counter` 修飾クラスをテキスト欄に負荷することにより、文字数カウンターを textarea の内部に配置することができます。

```html
<label class="mdc-text-field mdc-text-field--outlined mdc-text-field--textarea mdc-text-field--with-internal-counter">
  <span class="mdc-notched-outline">
    <span class="mdc-notched-outline__leading"></span>
    <span class="mdc-notched-outline__notch">
      <span class="mdc-floating-label" id="my-label-id">Textarea Label</span>
    </span>
    <span class="mdc-notched-outline__trailing"></span>
  </span>
  <span class="mdc-text-field__resizer">
    <textarea class="mdc-text-field__input" aria-labelledby="my-label-id" rows="8" cols="40" maxlength="140"></textarea>
    <span class="mdc-text-field-character-counter">0 / 140</span>
  </span>
</label>
```

ヘルプテキストと文字数カウンターは独立して共存できるテキスト欄のオプションサブコンポーネントです。適切なレイアウトのために `.mdc-text-field` 要素と `.mdc-text-field-helper-line` 要素は同じ幅にすることを推奨します。

### プレフィックスとサフィックスのテキストあるテキスト欄

通貨記号のプレフィックスや大きさの単位記号のサフィックスのようなプレフィックスやサフィックステキストをテキスト欄の内容に追加することができます。プレフィックス、サフィックス、もしくはその両方をテキスト欄のデフォルト、またはアウトライン変数内に追加できます。

```html
<label class="mdc-text-field mdc-text-field--filled">
  <span class="mdc-text-field__ripple"></span>
  <span class="mdc-floating-label" id="my-label-id">Currency Value</span>
  <span class="mdc-text-field__affix mdc-text-field__affix--prefix">$</span>
  <input class="mdc-text-field__input" type="text" aria-labelledby="my-label-id">
  <span class="mdc-text-field__affix mdc-text-field__affix--suffix">.00</span>
  <span class="mdc-line-ripple"></span>
</label>
```

**注意: `mdc-text-field--textarea` 内では `mdc-text-field--affix` を使用できません。**

### 先頭と末尾のアイコン

双方向ターゲットとしてだけでなく視覚インジケーターとして MDC Text Fields のデフォルトのもしくはアウトライン内部に先頭と末尾のアイコンを追加することができます。アイコンを使う上でのより詳細な情報は [ここ](icon/) を参照してください。

## その他の機能

### HTML5 バリデーション

`MDCTextFieldFoundation` は HTML5 フォームバリデーション API の提供する `:invalid` と `:required` 属性を使用した入力の妥当性検証の機能を持っています。

```html
<label class="mdc-text-field mdc-text-field--filled">
  <span class="mdc-text-field__ripple"></span>
  <span class="mdc-floating-label" id="my-label-id">Password</span>
  <input class="mdc-text-field__input" type="password" aria-labelledby="my-label-id" required minlength="8">
  <span class="mdc-line-ripple"></span>
</label>
```

`MDCTextFieldFoundation` は required 属性が設定されていると自動的にラベルにアスタリスクを追加します。

### 入力済みのテキスト欄

値をすでに持っている JS を利用するテキスト欄を扱うときには、 `mdc-floating-label--float-above` 修飾クラスを持つ `mdc-floating-label` を付けるとともに、`mdc-text-field--label-floating` 修飾クラスをもつ `mdc-text-field` を記述してください。そうすればラベルはテキスト欄のところから離れ、Flash Of Un-styled Content (**FOUC**) を防ぐことができます。（訳注: [Flash Of Un-styled Content](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) はスタイルの設定が完全でない状態でレンダリングされてしまうこと。クラスが正しく設定されていないと値のあるテキスト欄の上にラベルが重なった状態で表示されてしまうので、その状態を避けるために、クラスを設定する必要がある、ということを言っている。）

```html
<label class="mdc-text-field mdc-text-field--filled mdc-text-field--label-floating">
  <span class="mdc-text-field__ripple"></span>
  <span class="mdc-floating-label mdc-floating-label--float-above" id="my-label-id">
    Label in correct place
  </span>
  <input class="mdc-text-field__input" type="text" aria-labelledby="my-label-id" value="Pre-filled value">
  <span class="mdc-line-ripple"></span>
</label>
```

### ベースラインを揃える

デフォルトで、テキスト欄はベースラインを基準にして他の要素と揃えられます。入力テキストのベースラインはテキスト欄の位置を決定するのに用いられ、バリエーションによって異なったものになります。強制的にベースラインの替わりにテキスト欄のコンテナに揃えるには、flexbox を使って整列させます。

```html
<div>
  <label class="mdc-text-field mdc-text-field--outlined">
    <span class="mdc-notched-outline">
      <span class="mdc-notched-outline__leading"></span>
      <span class="mdc-notched-outline__trailing"></span>
    </span>
    <input type="text" class="mdc-text-field__input" value="Baseline">
  </label>
  <span>テキスト欄の値に揃えられたテキスト</span>
</div>

<div style="display: flex; flex-direction: row; align-items: flex-end;">
  <label class="mdc-text-field mdc-text-field--outlined">
    <span class="mdc-notched-outline">
      <span class="mdc-notched-outline__leading"></span>
      <span class="mdc-notched-outline__trailing"></span>
    </span>
    <input type="text" class="mdc-text-field__input" value="Baseline">
  </label>
  <span>テキストフィールドのアウトラインの底辺に揃えられたテキスト</span>
</div>
```

## API

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-text-field` | 必須。
`mdc-text-field--filled` | テキスト欄を塗られたテキスト欄として表示する。
`mdc-text-field--outlined` | アウトラインされたテキスト欄として表示する。
`mdc-text-field--textarea` | テキスト欄が `<textarea>` であることを表す。
`mdc-text-field--disabled` | 無効なテキスト欄として表示する。
`mdc-text-field--with-leading-icon` | 先頭にアイコンのあるテキスト欄として表示する。
`mdc-text-field--with-trailing-icon` | 末尾にアイコンのあるテキスト欄として表示する。
`mdc-text-field--focused` | フォーカスを持つテキスト欄として表示する。
`mdc-text-field--no-label` | ラベルのないテキスト欄として表示する。
`mdc-text-field--end-aligned` | テキスト欄を後ろ揃え（訳注：RTL でなければ右揃えのこと）で表示する。
`mdc-text-field--label-floating` | 上に移動したラベルと入力済みもしくはフォーカスされた値を伴うテキスト欄として表示する。
`mdc-text-field--ltr-text` | 方向が RTL のときにテキスト欄の要素（入力、プレフィックス、サフィックス）を LTR として表示する。分数表記に LTR を使う RTL 言語で役立つ。
`mdc-text-field--with-internal-counter` | 文字数カウンターを伴うテキストエリアとしてテキストエリアを表示する。
`mdc-text-field-helper-line` | ヘルプテキストと文字数カウンタ要素のコンテナのスタイル。

### Sass ミキシン

テキスト欄の任意の部分の色をカスタマイズするには以下のミキシンを使用します。フォーカスのないテキスト欄を選択するには `.foo-text-field:not(.mdc-text-field--focused)`、フォーカスのあるテキスト欄を選択するには `.foo-text-field.mdc-text-field--focused` のような CSS セレクター内にこれらのミキシンを適用することを推奨しています。テキスト欄を無効にするには `.foo-text-field.mdc-text-field--invalid` のような CSS セレクター内にこれらのミキシンを適用します。

> <em>注意</em>: `mdc-line-ripple-color` ミキシンは非フォーカスクラス（`foo-text-field:not(.mdc-text-field--focused)`）から適用する必要があります。

#### すべてのテキスト欄のためのミキシン

ミキシン | 説明
--- | ---
`ink-color($color)` | 有効なテキスト欄に入力されたテキストの色を設定する。
`placeholder-color($color)` | 有効なテキスト欄のプレースホルダーの色を設定する。
`disabled-ink-color($color)` | 無効なテキスト欄に入力されたテキストの色を設定する。
`disabled-placeholder-color($color)` | 無効なテキスト欄のプレースホルダーの色を設定する。
`label-color($color)` | 有効なテキスト欄のラベルのテキスト色を設定する。
`disabled-label-color($color)` | 無効なテキスト欄のラベルのテキスト色を設定する。
`caret-color($color)` | テキスト欄のカーソルキャレットの色を設定する。
`prefix-color($color)` | 有効なテイスト欄のプレフィックステキストの色を設定する。
`disabled-prefix-color($color)` | 無効なテイスト欄のプレフィックステキストの色を設定する。
`suffix-color($color)` | 有効なテイスト欄のサフィックステキストの色を設定する。
`disabled-suffix-color($color)` | 無効なテイスト欄のサフィックステキストの色を設定する。
`floating-label-float-transition($duration-ms, $timing-function)` | ラベルの移動の際のデュレーションとオプションでタイミング関数を設定する。

#### 塗りつぶされたテキスト欄とテキストエリアのためのミキシン

Mixin | Description
--- | ---
`fill-color($color)` | 有効である場合のテキスト欄もしくはテキストエリアの背景色を設定する。
`disabled-fill-color($color)` | 無効である場合のテキスト欄もしくはテキストエリアの背景色を設定する。

#### 塗りつぶされたテキスト欄のみのためのミキシン

ミキシン | 説明
--- | ---
`shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にボックス型テキスト欄を設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`bottom-line-color($color)` | テキスト欄下部の線の色を設定する。
`hover-bottom-line-color($color)` | ホバー時のテキスト欄下部の線の色を設定する。
`disabled-bottom-line-color($color)` | 無効なテキスト欄下部の千の色を設定する。
`line-ripple-color($color)` | テキスト欄のデフォルトのラインリップルの色を設定する。
`density($density-scale)` | デフォルト型のテキスト欄の密度スケールを設定する。サポートしている密度スケールは `-4`、`-3`、`-2`、`-1` そして `0`。
`height($height)` | デフォルト型のテキスト欄の高さを設定する。

#### 枠付きテキスト欄とテキストエリアのためのミキシン

Mixin | Description
--- | ---
`focused-outline-color($color)` | テキスト欄かテキストエリアがフォーカスされているときのアウトラインされた境界線の色を設定する。
`hover-outline-color($color)` | テキスト欄かテキストエリアがホバーされているときのアウトラインされた境界線の色を設定する。
`disabled-outline-color($color)` | テキスト欄かテキストエリアが無効なときのアウトラインされた境界線の色を設定する。
`outline-color($color)` | アウトラインされたテキスト欄もしくはテキストエリアの境界線の色を設定する。

#### 枠付きテキスト欄のみのためのミキシン

ミキシン | 説明
--- | ---
`outline-shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にアウトラインされたテキスト欄を設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`outlined-density($density-scale)` | アウトラインされたテキスト欄（先頭アイコン付きのアウトラインテキスト欄を除く）の密度スケールを設定する。サポートしている密度スケールは `-4`、`-3`、`-2`、`-1` そして `0`。
`outlined-height($height)` | アウトラインされたテキスト欄（先頭アイコン付きのアウトラインテキスト欄を除く）の高さを設定する。
`outlined-with-leading-icon-density($density-scale)` | 先頭アイコン付きのアウトラインテキスト欄の密度スケールを設定する。サポートしている密度スケールは `-4`、`-3`、`-2`、`-1` そして `0`。
`outlined-with-leading-icon-height($height)` | 先頭アイコン付きのアウトラインテキスト欄の高さを設定する。

#### テキストエリアのみのためのミキシン

ミキシン | 説明
--- | ---
`textarea-shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にテキストエリアを設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`outlined-textarea-density($density-scale)` | アウトラインされたテキスト欄の密度スケールを設定する。サポートしている密度スケールは `-4`、`-3`、`-2`、`-1`、`0`。
`textarea-min-rows($rows)` | テキストエリアのサイズを変更する際の最小の行数を設定する。

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
`prefixText` | `string` | プレフィックスのテキストコンテンツが存在するなら、その値を取得もしくは設定する
`suffixText` | `string` | サフィックスのテキストコンテンツが存在するなら、その値を取得もしくは設定する

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
`setAutovalidate(shouldAutovalidate: boolean) => void` | `value` が変更されたときにテキスト欄が入力を検証するかどうかを設定する。
`getAutovalidate() => boolean` | `value` が変更されたときにテキスト欄が入力を検証するかどうか。デフォルトは `true`。

`MDCTextFieldFoundation` は複数のオプションのサブ要素 - ヘルパーテキストとアイコン - をサポートしています。これらのサブ要素のファンデーションはコンストラクターの引数として `MDCTextFieldFoundation` に渡さなくてはなりません。
