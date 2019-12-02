<!--docs:
title: "Select Menus"
layout: detail
section: components
iconId: menu
path: /catalog/input-controls/select-menus/
-->

# Select Menus

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/select">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/selects.png" width="376" alt="Select screenshot">
  </a>
</div>-->

MDC Select は MDC メニューを利用してマテリアルデザインの単一選択ができるセレクトメニューを提供します。MDC Select コンポーネントは完全なアクセス可能で RTL 描画をサポートしています。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-text-fields">マテリアルデザインガイドライン: テキスト欄</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/select">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/select
```

## 基本的な使用法

セレクトは項目のリストを含んだ [`MDCMenu`](../mdc-menu) コンポーネントのインスタンスを使用しますが、 項目の値を表すのに `value` 属性の代わりに `data-value` 属性を使います。

> _注意_: `data-value` 属性は各項目に <em>必ず</em> 存在しなくてはなりません。

セレクトでは、`mdc-select__anchor` 要素の `width` を設定するのはもちろん、`mdc-select__menu` 要素の幅を合うように設定する必要があります。これは別のクラス（例えば以下の HTML と CSS の例の `demo-width-class`）を使うのが最適です。

### HTML

```html
<div class="mdc-select">
  <div class="mdc-select__anchor demo-width-class">
    <i class="mdc-select__dropdown-icon"></i>
    <div class="mdc-select__selected-text"></div>
    <span class="mdc-floating-label">Pick a Food Group</span>
    <div class="mdc-line-ripple"></div>
  </div>

  <div class="mdc-select__menu mdc-menu mdc-menu-surface demo-width-class">
    <ul class="mdc-list">
      <li class="mdc-list-item mdc-list-item--selected" data-value="" aria-selected="true"></li>
      <li class="mdc-list-item" data-value="grains">
        Bread, Cereal, Rice, and Pasta
      </li>
      <li class="mdc-list-item" data-value="vegetables">
        Vegetables
      </li>
      <li class="mdc-list-item" data-value="fruit">
        Fruit
      </li>
    </ul>
  </div>
</div>
```

### スタイル

セレクトを使う際には Menu と List コンポーネントのスタイルをロードしておく必要もあり案す。

```scss
@import "@material/list/mdc-list";
@import "@material/menu-surface/mdc-menu-surface";
@import "@material/menu/mdc-menu";
@import "@material/select/mdc-select";

.demo-width-class {
  width: 400px;
}
```

### JavaScript オブジェクトのインスタンス化

```js
import {MDCSelect} from '@material/select';

const select = new MDCSelect(document.querySelector('.mdc-select'));

select.listen('MDCSelect:change', () => {
  alert(`Selected option at index ${select.selectedIndex} with value "${select.value}"`);
});
```

See [Importing the JS component](../../docs/importing-js.md) for more information on how to import JavaScript.
JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

#### アクセシビリティ (a11y)

ユーザーにアクセス可能なコンポーネントを提供するために、[Collapsible Dropdown Listbox](https://www.w3.org/TR/wai-aria-practices/examples/listbox/listbox-collapsible.html) の WAI-ARIA の例にしたがうことをお勧めします。以下は必要な aria 属性をすべて付加したセレクトコンポーネントの例です。

```html
<div class="mdc-select">
  <div class="mdc-select__anchor">
    <i class="mdc-select__dropdown-icon"></i>
    <div id="demo-selected-text" class="mdc-select__selected-text" role="button" aria-haspopup="listbox" aria-labelledby="demo-label demo-selected-text">Vegetables</div>
    <span id="demo-label" class="mdc-floating-label mdc-floating-label--float-above">Pick a Food Group</span>
    <div class="mdc-line-ripple"></div>
  </div>

  <div class="mdc-select__menu mdc-menu mdc-menu-surface" role="listbox">
    <ul class="mdc-list">
      <li class="mdc-list-item mdc-list-item--selected" data-value="" role="option"></li>
      <li class="mdc-list-item" data-value="grains" role="option">
        Bread, Cereal, Rice, and Pasta
      </li>
      <li class="mdc-list-item mdc-list-item--disabled" data-value="vegetables" aria-selected="true" aria-disabled="true" role="option">
        Vegetables
      </li>
      <li class="mdc-list-item" data-value="fruit" role="option">
        Fruit
      </li>
    </ul>
  </div>
</div>
```

## バリエーション

### アウトラインされたセレクト

アウトラインされたセレクトにおいては `mdc-line-ripple` 要素の代わりに `mdc-notched-outline` が使用し、ルート要素に `mdc-select--outlined` 修飾クラスを追加します。セレクトの様々な他のすべての要素は変わっていません。

```html
<div class="mdc-select mdc-select--outlined">
  <div class="mdc-select__anchor">
    <i class="mdc-select__dropdown-icon"></i>
    <div id="demo-selected-text" class="mdc-select__selected-text" aria-labelledby="outlined-select-label"></div>
    <div class="mdc-notched-outline">
      <div class="mdc-notched-outline__leading"></div>
      <div class="mdc-notched-outline__notch">
        <label id="outlined-select-label" class="mdc-floating-label">Pick a Food Group</label>
      </div>
      <div class="mdc-notched-outline__trailing"></div>
    </div>
  </div>

  <!-- セレクトに残っているその他の要素 -->
  <div class="mdc-select__menu mdc-menu mdc-menu-surface" role="listbox">...</div>
</div>
```

### 追加情報

#### 選択済みの選択肢を持つセレクト

事前に選択された値を持つセレクトコンポーネントを表示するには、選択している項目に `mdc-list-item--selected` クラスを使います。セレクトは選択された要素から `mdc-select__selected-text` 要素にテキストをコピーすることも必要です。

```html
<div class="mdc-select">
  <div class="mdc-select__anchor demo-width-class">
    <i class="mdc-select__dropdown-icon"></i>
    <div class="mdc-select__selected-text">Vegetables</div>
    <span class="mdc-floating-label mdc-floating-label--float-above">Pick a Food Group</span>
    <div class="mdc-line-ripple"></div>
  </div>

  <div class="mdc-select__menu demo-width-class mdc-menu mdc-menu-surface">
    <ul class="mdc-list">
      <li class="mdc-list-item" data-value=""></li>
      <li class="mdc-list-item" data-value="grains">
        Bread, Cereal, Rice, and Pasta
      </li>
      <li class="mdc-list-item mdc-list-item--selected" data-value="vegetables" aria-selected="true">
        Vegetables
      </li>
      <li class="mdc-list-item" data-value="fruit">
        Fruit
      </li>
    </ul>
  </div>
</div>
```

#### プレースホルダーとしてのフローティングラベルの使用

`mdc-select__selected-text` 要素を空のままで選択された要素を指定しないでください。空のフィールドを有効な選択肢としたいなら、リストの最初に `data-value` 属性を空にした `mdc-list-item` 要素を入れてください。

```html
<li class="mdc-list-item mdc-list-item--selected" aria-selected="true" role="option" data-value=""></li>
```

#### 必須のセレクト

必須で検証が有効なセレクトをスタイルするには、`mdc-select--required` クラスを `mdc-select` 要素に追加し、`mdc-select__selected-text` 要素の `aria-required` 属性を `"true"` にします。

```html
<div class="mdc-select mdc-select--required">
  <div class="mdc-select__anchor">
    <i class="mdc-select__dropdown-icon"></i>
    <div class="mdc-select__selected-text" aria-required="true"></div>
    <span class="mdc-floating-label">Pick a Food Group</span>
    <div class="mdc-line-ripple"></div>
  </div>

  <div class="mdc-select__menu mdc-menu mdc-menu-surface">
    ...
  </div>
</div>
```

> _注意_: プログラムによりセレクトを必須にするには `MDCSelect` API の `required` プロパティを使います。

#### 無効なセレクト

`mdc-select--disabled` クラスを `mdc-select` 要素に追加し、`mdc-select__selected-text` 要素の `aria-disabled` 属性を `"true"` にします。

```html
<div class="mdc-select mdc-select--disabled">
  <div class="mdc-select__anchor">
    <i class="mdc-select__dropdown-icon"></i>
    <div class="mdc-select__selected-text" aria-disabled="true"></div>
    <span class="mdc-floating-label">Pick a Food Group</span>
    <div class="mdc-line-ripple"></div>
  </div>

  <div class="mdc-select__menu mdc-menu mdc-menu-surface">
    ...
  </div>
</div>
```

> _注意_: プログラムによりセレクトを無効にするには `MDCSelect` API の `disabled` プロパティを使います。

#### 無効な選択肢

`mdc-list-item--disabled` クラスを無効にするリスト項目に追加します。無効なリスト項目はリスト項目のインデックスから除外され、完全に無視されます。プログラムから無効なリスト項目を選択することはできません。

```html
<div class="mdc-select">
  <div class="mdc-select__anchor">
    ...
  </div>

  <div class="mdc-select__menu mdc-menu mdc-menu-surface">
    <ul class="mdc-list">
      <li class="mdc-list-item" data-value=""></li>
      <li class="mdc-list-item" data-value="grains">
        Bread, Cereal, Rice, and Pasta
      </li>
      <li class="mdc-list-item mdc-list-item--selected mdc-list-item--disabled" data-value="vegetables">
        Vegetables
      </li>
      <li class="mdc-list-item" data-value="fruit">
        Fruit
      </li>
    </ul>
  </div>
</div>
```

### ヘルパーテキストのあるセレクト

ヘルパーテキストは補足情報や検証メッセージをユーザーに提供します。セレクト要素がフォーカスされているときに表示され、デフォルトでフォーカスを失うと非表示なる、もしくは永続化することができます。ヘルパーテキストの使用についてのより詳しい情報は [ここ](helper-text/) を参照してください。

### 先頭にアイコンのあるセレクト

対話のターゲットとしてだけでなく視覚的インジケーターとして MDC Select の標準型、もしくはアウトラン型のものに対して先頭アイコンを追加することができます。アイコンの使用についてのより詳しい情報は [ここ](icon/) を参照してください。

### ラベルのないセレクト

別の場所で個別の隣接したラベルが提供されているならラベルは必須ではありません。ラベルなしで MDC Select を適切にスタイルするには、クラス `mdc-select--no-label` を追加し、構造からラベルを削除します。

#### 幅いっぱい

```html
<div class="mdc-select mdc-select--no-label">
  <div class="mdc-select__anchor demo-width-class">
    <i class="mdc-select__dropdown-icon"></i>
    <div class="mdc-select__selected-text"></div>
    <div class="mdc-line-ripple"></div>
  </div>

  <div class="mdc-select__menu mdc-menu mdc-menu-surface demo-width-class">
    <ul class="mdc-list">
      <li class="mdc-list-item mdc-list-item--selected" data-value="" aria-selected="true"></li>
      <li class="mdc-list-item" data-value="grains">
        Bread, Cereal, Rice, and Pasta
      </li>
      <li class="mdc-list-item" data-value="vegetables">
        Vegetables
      </li>
      <li class="mdc-list-item" data-value="fruit">
        Fruit
      </li>
    </ul>
  </div>
</div>
```

#### アウトラインされたもの

```html
<div class="mdc-select mdc-select--outlined mdc-select--no-label">
  <div class="mdc-select__anchor demo-width-class">
    <i class="mdc-select__dropdown-icon"></i>
    <div class="mdc-select__selected-text"></div>
    <div class="mdc-notched-outline">
      <div class="mdc-notched-outline__leading"></div>
      <div class="mdc-notched-outline__trailing"></div>
    </div>
  </div>

  <!-- セレクトに残っているその他の要素 -->
  <div class="mdc-select__menu mdc-menu mdc-menu-surface demo-width-class">...</div>
</div>
```

## スタイルのカスタマイズ

### CSS クラス

| クラス | 説明 |
| --- | --- |
| `mdc-select` | 必須。 |
| `mdc-select__anchor` | 必須。この要素は `mdc-select` 要素内に配置されなくてはならない。 |
| `mdc-select__menu` | 必須。このクラスは `mdc-select` 要素内の `mdc-menu` 要素に配置されなくてはならない。 |
| `mdc-select__dropdown-icon` | 必須。`mdc-select__anchor` 要素内の `i` 要素に配置されなくてはならない。ドロップダウンの矢印 SVG とアニメーションに使用される。 |
| `mdc-select__selected-text` | 必須。このクラスは `mdc-select__anchor` 要素内の `div` に配置されなくてはならない。 |
| `mdc-select__icon` | オプション。`mdc-select__anchor` 要素内の `i` 要素か `svg` 要素に配置されなくてはならない。先頭アイコンに使用される。 |
| `mdc-select--activated` | オプション。セレクトのアクティブ状態のスタイル。このクラスはメニューが開かれた際に自動的に追加される。 |
| `mdc-select--disabled` | オプション。無効となっているセレクトのスタイル。このクラスは `<select>` 要素に `disabled` 属性が適用されている際にルート要素に適用しなくてはならない。 |
| `mdc-select--outlined` | オプション。セレクトをアウトラインされたセレクトとしてスタイルを設定する。 |
| `mdc-select--with-leading-icon` | セレクトを先頭アイコンのあるセレクトとしてスタイルを設定する。 |
| `mdc-select--no-label` | セレクトをラベルのないセレクトとしてスタイルを設定する。 |
> _注意_: セレクト内に含まれる [MDCMenu](./../mdc-menu) や [MDCList](./../mdc-list) コンポーネントをさらにカスタマイズするには、それぞれのドキュメントを参照してください。

### Sass ミキシン

ミキシンはコンポーネントのルート要素に `.my-select` のようにカスタムクラスを適用しているコンテキストに含めなくてはなりません。

ミキシン | 説明
--- | ---
`mdc-select-ink-color($color)` | セレクト内の選択された項目を表示する色を設定する。
`mdc-select-container-fill-color($color)` | セレクトの背景色を設定する。
`mdc-select-label-color($color)` | フォーカスのないセレクトのラベルの色を設定する。
`mdc-select-focused-label-color($color)` | フォーカス時のセレクトのラベルの色を設定する。
`mdc-select-bottom-line-color($color)` | セレクトのデフォルトの下線の色を設定する。
`mdc-select-focused-bottom-line-color($color)` | フォーカス時のセレクトの下線の色を設定する。
`mdc-select-shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にボックス型セレクトを設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`mdc-select-hover-bottom-line-color($color)` | セレクトがホバーされた際の下線の色を設定する。
`mdc-select-outline-color($color)` | へこんだ輪郭の色を設定する。
`mdc-select-outline-shape-radius($radius, $rtl-reflexive)` | アウトラインされたタイプのセレクトの角の丸めを設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`mdc-select-focused-outline-color($color)` | フォーカス時のセレクトのアウトラインの色を設定する。
`mdc-select-hover-outline-color($color)` | セレクトがホバーされた際のアウトラインの色を設定する。

> _注意_: これ以上にフローティングラベルを変更する方法は [フローティングラベルのドキュメント](./../mdc-floating-label/README.md) を参照してください。

## `MDCSelect` API

`MDCSelect` コンポーネント API は `HTMLSelectElement` の機能のサブセットをもとに作られています。

プロパティ | 型 | 説明
--- | --- | ---
`value` | `string` | 現在選択されているオプションの `value`/`data-value`。
`selectedIndex` | `number` | 現在選択されている選択肢のインデックス。選択肢が選ばれていないときは -1 が設定される。このプロパティを変更するとセレクト要素が更新される。
`disabled` | `boolean` | コンポーネントが無効かどうか。これを設定するとコンポーネントの無効かどうかの状態が設定される。
`valid` | `boolean` | コンポーネントが有効な状態かどうか。これを設定すると、コンポーネントのスタイルが更新されるが、ネイティブな有効状態には影響しない。
`required` | `boolean` | コンポーネントが必須かどうか。これおw設定すると、コンポーネントの `required` または `aria-required` 属性が更新され、検証が有効になる。
`leadingIconAriaLabel` | `string` (書込専用) | ファンデーションの `setLeadingIconAriaLabel` メソッドの代替。
`leadingIconContent` | `string` (書込専用) | ファンデーションの `setLeadingIconContent` メソッドの代替。
`helperTextContent` | `string` (書込専用)| 設定時のファンデーションの `setHelperTextContent` メソッドの代替。
`ripple` | `MDCRipple` | アウトラインされたセレクトにアタッチされた Ripple インスタンス。アウトラインされたセレクトでなければ `null`。

### イベント

イベント | データ | 説明
--- | --- | ---
`MDCSelect:change` | `{value: string, index: number}` | 要素が選択されたことを示すのに使用します。このイベントには項目の値とインデックスも含まれています。

## Web フレームワークでの使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のセレクトを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCSelectAdapter`

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | セレクト要素にクラスを追加する。 |
| `removeClass(className: string) => void` | セレクト要素からクラスを削除する。 |
| `hasClass(className: string) => boolean` | セレクト要素がクラスリストにクラス名を持っていれば true を返す。 |
| `activateBottomLine() => void` | 下線のコンポーネントを有効にする。 |
| `deactivateBottomLine() => void` | 下線のコンポーネントを無効にする。 |
| `getSelectedMenuItem() => Element` | 選択されたメニュー項目要素を返す。 |
| `hasLabel() => boolean` | セレクトがレベルを含んでいる場合は true を返す。 |
| `floatLabel(value: boolean) => void` | ラベルを上に動かしたり戻したりする。 |
| `getLabelWidth() => number` | ラベル要素の offsetWidth を返す。 |
| `hasOutline() => boolean` | `select` にへこんだ輪郭要素があれば true を返す。 |
| `notchOutline(labelWidth: number) => void` | へこんだ輪郭要素を "へこんだ状態" に切り替える。 |
| `closeOutline() => void` | へこんだ輪郭要素を閉じた状態に切り替える。 |
| `setDisabled(isDisabled: boolean) => void` | セレクトを利用できなくする。 |
| `setRippleCenter(normalizedX: number) => void` | ラインリップルの中心を与えた normalizedX の値に設定する。 |
| `notifyChange(value: string) => void` | 要素が選択された際に `MDCSelect:change` イベントを発生させる。 |
| `setSelectedText(text: string) => void` | selectedText 要素のテキストコンテンツを与えられた文字列に設定する。 |
| `isSelectedTextFocused() => boolean` | 選択されたテキスト要素がフォーカスされているかどうかを返す。 |
| `getSelectedTextAttr(attr: string) => string` | 選択されたテキスト要素の与えられた属性を取得する。 |
| `setSelectedTextAttr(attr: string, value: string) => void` | 選択されたテキスト要素の与えられた属性を設定する。 |
| `openMenu() => void` | セレクトのメニュー要素を開く。 |
| `closeMenu() => void` | セレクトのメニュー要素を閉じる。 |
| `getAnchorElement() => Element` | セレクトのアンカー要素を返す。 |
| `setMenuAnchorElement(anchorEl: Element) => void` | メニューのアンカー要素を設定する。 |
| `setMenuAnchorCorner(anchorCorner: Corner) => void` | メニューのアンカーの角を設定する。 |
| `setMenuWrapFocus(wrapFocus: boolean) => void` | メニューがフォーカスをラップするかどうかを設定する。 |
| `setAttributeAtIndex(index: number, attributeName: string, attributeValue: string) => void` | 与えられたインデックスのメニュー項目の属性を設定する。 |
| `removeAttributeAtIndex(index: number, attributeName: string) => void` | 与えられたインデックスのメニュー項目の属性を削除する。 |
| `focusMenuItemAtIndex(index: number) => void` | 与えられたインデックスのメニュー項目にフォーカスをあてる。 |
| `getMenuItemValues() => string[]` | 各メニュー項目の VALUE_ATTR 属性を表す配列を返す。 |
| `getMenuItemCount() => number` | メニュー項目の数を返す。 |
| `getMenuItemAttr(menuItem: Element, attr: string) => string` | メニュー項目要素の与えられた属性を返す。 |
| `getMenuItemTextAtIndex(index: number) => string` | 与えられたインデックスのメニュー項目要素のテキストコンテンツを取得する。 |
| `addClassAtIndex(menuItem: Element, className: string) => void` | 与えられたインデックスのメニュー項目にクラス名を追加する。 |
| `removeClassAtIndex(menuItem: Element, className: string) => void` | 与えられたインデックスのメニュー項目からクラス名を削除する。 |

### `MDCSelectFoundation`

| メソッド | 説明 |
| --- | --- |
| `notchOutline(openNotch: boolean) => void` | へこんだ輪郭を開く、もしくは閉じる。 |
| `getDisabled() => boolean` | 無効状態を取得する。 |
| `setDisabled(isDisabled: boolean) => void` | 無効状態を更新する。 |
| `handleFocus() => void` | `select` 要素の focus イベントを処理する。 |
| `handleBlur() => void` | `select` 要素の blur イベントを処理する。 |
| `handleClick(normalizedX: number) => void` | ラインリップルの中心を normalizedX に設定する。 |
| `handleMenuOpened() => void` | メニューもしくはメニュー表面の opened イベントを処理する。 |
| `handleMenuClosed() => void` | メニューもしくはメニュー表面の closed イベントを処理する。 |
| `handleMenuItemAction() => void` | メニュー選択イベントをハンドリングする。 |
| `handleChange() => void` | `select` 要素の値の変更を処理する。`change` イベントとコンポーネント API を通じて要求されたプログラム上での変更の両方でこれを呼び出す必要がある。 |
| `handleKeydown(event: KeyboardEvent) => void` | `mdc-select__selected-text` 要素を設定しメニューを閉じることをハンドリングする。必要であればラベルを浮かせ、輪郭をへこませる。 |
| `getSelectedIndex() => number` | 現在選択されているメニュー項目のインデックスを返す。 |
| `setSelectedIndex(index: number) => void` | `mdc-select__selected-text` 要素を設定しメニューを閉じることをハンドリングする。必要であればラベルを浮かせ、輪郭をへこませる。 |
| `getValue() => string` | アダプターを介して値の取得をハンドリングする。 |
| `setValue(value: string) => void` | 選択したインデックスを、与えられた値を持つメニュー項目のインデックスに設定する。 |
| `setValid(isValid: boolean) => void` | アダプターを介して有効状態を設定する。 |
| `isValid() => boolean` | アダプターの `checkValidity` API を介して有効状態を取得する。 |
| `setRequired(isRequired: boolean) => void` | アダプターを介して必須状態を設定する。 |
| `getRequired() => boolean` | アダプターを介して必須状態を取得する。 |
| `init() => void` | ファンデーションを初期化する。 |
| `layout() => void` | へこんだアウトラインがへこんでいるかどうかの決定をハンドリングする。 |
| `setLeadingIconAriaLabel(label: string) => void` | 先頭アイコンの aria ラベルを設定する。 |
| `setLeadingIconContent(content: string) => void` | 先頭アイコンのテキストコンテンツを設定する。 |
| `setHelperTextContent(content: string) => void` | ヘルパーテキストのコンテンツを設定する。 |

`MDCSelectFoundation` は複数のオプションのサブ要素（ヘルパーテキストとアイコン）をサポートしています。これらのサブ要素のファンデーションは `MDCSelectFoundation` にコンストラクターの引数として渡さなくてはなりません。
