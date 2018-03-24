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

> 注意: ビルドされた CSS ファイルと UMD JS バンドルはポストアルファパッケージの一部として利用できます。

### コンポーネントの自動初期化

`material-components-web` パッケージはすべての MDC Web コンポーネントを [mdc-auto-init](../mdc-auto-init) に自動的に登録するので、設定や手作業なしでコンポーネントの生成と初期化を非常に簡単に行えます。

例として  [トグルアイコン](../mdc-icon-toggle) を使いたい場合で言うと、必要な DOM を記述し、`data-mdc-auto-init="MDCIconToggle"` 属性を追加するだけです。

```html
<i class="mdc-icon-toggle material-icons" role="button" aria-pressed="false"
   aria-label="Add to favorites" tabindex="0"
   data-toggle-on='{"label": "Remove from favorites", "content": "favorite"}'
   data-toggle-off='{"label": "Add to favorites", "content": "favorite_border"}'
   data-mdc-auto-init="MDCIconToggle">
  favorite_border
</i>
```

HTML の最後のほうに次のスクリプトタグを追加します。

```html
<script>mdc.autoInit()</script>
```

これでトグルアイコンだけでなく、`data-mdc-auto-init` をつけたそのほかのコンポーネントも自動で初期化されます。詳しい情報は [mdc-auto-init](../mdc-auto-init) を参照してください。
