> ✨ あなたは Material Design web コミュニティの一員ですか？この <a href='https://bit.ly/materialwebsurvey'>**10分調査**</a> にご記入ください。 ✨

# Material Components Web (MDC Web)

このページは Material Components Web のマスタライブラリを含んでいます。利便性を考え、単にパッケージのすべてを一つの包括的なライブラリにまとめただけです。

## インストール

```
npm install material-components-web
```

## 使用法

### Sass のインクルード

```scss
@import "material-components-web/material-components-web";
```

### Javascript のインクルード

```js
import * as mdc from 'material-components-web';
const checkbox = new mdc.checkbox.MDCCheckbox(document.querySelector('.mdc-checkbox'));
// または
import { checkbox } from 'material-components-web';
const checkbox = new checkbox.MDCCheckbox(document.querySelector('.mdc-checkbox'));
```

> 注意: switch は JS の予約語なので、代わりに `switchControl` という名前になっています。

> 注意: ビルドされた CSS ファイルと UMD JS バンドルはポストアルファパッケージの一部として利用できます。

### コンポーネントの自動初期化

`material-components-web` パッケージはすべての MDC Web コンポーネントを [mdc-auto-init](../mdc-auto-init) に自動的に登録するので、設定や手作業なしでコンポーネントの生成と初期化を非常に簡単に行えます。

例として  [トグルアイコンボタン](../mdc-icon-button) を使いたい場合で言うと、必要な DOM を記述し、`data-mdc-auto-init="MDCIConButtonToggle"` 属性を追加するだけです。

```html
<button class="mdc-icon-button" 
   aria-label="Add to favorites"
   aria-pressed="false"
   data-mdc-auto-init="MDCIconButtonToggle">
  <i class="material-icons mdc-icon-button__icon mdc-icon-button__icon--on">favorite</i>
  <i class="material-icons mdc-icon-button__icon">favorite_border</i>
</button>
```

HTML の最後のほうに次のスクリプトタグを追加します。

```html
<script>mdc.autoInit()</script>
```

これでトグルアイコンボタンだけでなく、`data-mdc-auto-init` をつけたそのほかのコンポーネントも自動で初期化されます。詳しい情報は [mdc-auto-init](../mdc-auto-init) を参照してください。
