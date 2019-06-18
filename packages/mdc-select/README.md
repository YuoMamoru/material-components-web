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

MDC Select はマテリアルデザインの単一選択ができるセレクトメニューを提供します。これはブラウザのネイティブな `<select>` 要素、もしくは MDC Menu の利用をサポートしています。これは完全に RTL 対応しています。

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

この節のドキュメントはネイティブな `<select>` 要素を使う MDC Select の使い方を説明します。MDC Menu を使った MDC Select の使い方の情報は次の [バリエーション](#variants) を参照してください。

### HTML構造

```html
<div class="mdc-select">
  <i class="mdc-select__dropdown-icon"></i>
  <select class="mdc-select__native-control">
    <option value="" disabled selected></option>
    <option value="grains">
      Bread, Cereal, Rice, and Pasta
    </option>
    <option value="vegetables">
      Vegetables
    </option>
    <option value="fruit">
      Fruit
    </option>
  </select>
  <label class="mdc-floating-label">Pick a Food Group</label>
  <div class="mdc-line-ripple"></div>
</div>
```

### スタイル

ネイティブな select に対しては、単に `mdc-select` Sass ファイルを含めることができます。

```scss
@import "@material/select/mdc-select";
```

### JavaScript オブジェクトのインスタンス化

```js
import {MDCSelect} from '@material/select';

const select = new MDCSelect(document.querySelector('.mdc-select'));

select.listen('MDCSelect:change', () => {
  alert(`Selected option at index ${select.selectedIndex} with value "${select.value}"`);
});
```

JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## <a name="variants"></a>バリエーション

### 拡張セレクト

拡張セレクトはリストの項目を含んだ [`MDCMenu`](../mdc-menu) コンポーネントのインスタンスを使用しますが、 項目の値を表すのに `value` 属性の代わりに `data-value` 属性を使います。

> 注意: `data-value` 属性は各項目に <em>必ず</em> 存在しなくてはなりません。

拡張セレクトではルート要素（`mdc-select` クラスを含んでいる要素）に `mdc-select__menu` 要素に合う幅を設定した `width` を設定する必要があります。これは別のクラス（例えば以下の HTML と CSS の例における `demo-width-class`）の利用を通じて行うのがよいです。

HTML フォーム内で拡張セレクトを使うなら、ルートの `mdc-select` 要素内に `<input type="hedden">` 要素を含めることができ、ユーザーの操作やプログラムにより値が更新されたときに同期するようにしておきます。

```html
<div class="mdc-select demo-width-class">
  <input type="hidden" name="enhanced-select">
  <i class="mdc-select__dropdown-icon"></i>
  <div class="mdc-select__selected-text"></div>
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
  <span class="mdc-floating-label">Pick a Food Group</span>
  <div class="mdc-line-ripple"></div>
</div>
```

拡張セレクトを使うときには、Menu と List のコンポーネントのスタイルを読み込んでおくことも必要です。

```scss
@import "@material/list/mdc-list";
@import "@material/menu-surface/mdc-menu-surface";
@import "@material/menu/mdc-menu";
@import "@material/select/mdc-select";

.demo-width-class {
  width: 400px;
}
```

#### ユーザビリティに関する注意

拡張セレクトはマテリアルデザインに沿った一貫性のあるルックアンドフィードを提供しますが、ネイティブな `<select>` 要素の利用を選択する際に考慮する必要のあるトレードオフがあります。

* **キーボードの先読み:** ネイティブなセレクトでは、通常、OS の実装しているキーボードの先読みサポートが有効です（つまり、入力された文字で始まる項目が自動的に選択されます）。この機能は拡張セレクトにはありません。
* **モバイル UI:** モバイル OS ネイティブなセレクトをモーダルダイアログやボトムシートとして実装しています。拡張セレクトでは常に MDC Menu が使用され、小さな画面では最適な体験を提供できません。

#### アクセシビリティ (a11y)

ユーザーにアクセス可能なコンポーネントを提供するために、[Collapsible Dropdown Listbox](https://www.w3.org/TR/wai-aria-practices/examples/listbox/listbox-collapsible.html) の WAI-ARIA の例にしたがうことをお勧めします。以下は必要な aria 属性をすべて付加した拡張セレクトコンポーネントの例です。

```html
<div class="mdc-select">
  <input type="hidden" name="enhanced-select">
  <i class="mdc-select__dropdown-icon"></i>
  <div id="demo-selected-text" class="mdc-select__selected-text" role="button" aria-haspopup="listbox" aria-labelledby="demo-label demo-selected-text">Vegetables</div>
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
  <span id="demo-label" class="mdc-floating-label mdc-floating-label--float-above">Pick a Food Group</span>
  <div class="mdc-line-ripple"></div>
</div>
```

### アウトラインされたセレクト

アウトラインされたセレクトにおいては `mdc-line-ripple` 要素の代わりに `mdc-notched-outline` が使用し、ルート要素に `mdc-select--outlined` 修飾クラスを追加します。セレクトの様々な他のすべての要素は変わっていません。

```html
<div class="mdc-select mdc-select--outlined">
  <!-- ネイティブもしくは拡張セレクトのほかの要素を残す。 -->
   <div class="mdc-notched-outline">
     <div class="mdc-notched-outline__leading"></div>
     <div class="mdc-notched-outline__notch">
       <label class="mdc-floating-label">Pick a Food Group</label>
     </div>
     <div class="mdc-notched-outline__trailing"></div>
   </div>
</div>
```

### 追加情報

#### 選択済みの選択肢を持つセレクト

選択済みの値を持つセレクトコンポーネントを扱う際には、`mdc-floating-label` 要素に `mdc-floating-label--float-above` 修飾クラスを追加し、選択する要素に `selected` 要素を付加します。これによりラベルが選択された値の上に移動し、Flash Of Unstyled Content (**FOUC**) を防ぐことができます。（訳注: [Flash Of Un-styled Content](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) はスタイルの設定が完全でない状態でレンダリングされてしまうこと。クラスが正しく設定されていないと値のあるテキスト欄の上にラベルが重なった状態で表示されてしまうので、その状態を避けるために、クラスを設定する必要がある、ということを言っている。）

```html
<div class="mdc-select">
  <i class="mdc-select__dropdown-icon"></i>
  <select class="mdc-select__native-control">
    <option value="vegetables">
      Vegetables
    </option>
    <option value="fruit">
      Fruit
    </option>
    <option value="dairy" selected>
      Milk, Yogurt, and Cheese
    </option>
  </select>
  <label class="mdc-floating-label mdc-floating-label--float-above">Pick a Food Group</label>
  <div class="mdc-line-ripple"></div>
</div>
```

拡張セレクトでも同じようにしますが、選択されている項目に `mdc-list-item--selected` クラスを使います。拡張セレクトでも選択されている要素から `mdc-select__selected-text` 要素にコピーされたテキストが必要です。

```html
<div class="mdc-select demo-width-class">
  <input type="hidden" name="enhanced-select">
  <i class="mdc-select__dropdown-icon"></i>
  <div class="mdc-select__selected-text">Vegetables</div>
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
  <span class="mdc-floating-label mdc-floating-label--float-above">Pick a Food Group</span>
  <div class="mdc-line-ripple"></div>
</div>
```

#### プレースホルダーとしてのフローティングラベルの使用

デフォルトでは、`<select>` 要素は最初の利用可能なオプションが選択されています。その代わりに初期表示にプレースフォルダーを表示するには、最初の `<option>` 要素に `selected` 属性を設定し（オプションで `disabled` も、フィールドが必須なら）、 `value` を `""` にします。

```html
<option value="" disabled selected></option>
```

各行セレクトでは、`mdc-select__selected-text` 要素を空のままにした状態で、要素を選択しないでください。フィールドを空のままにするには、`mdc-list-item` 要素を空の `data-value` 属性を持つリストの先頭に入れます。

```html
<li class="mdc-list-item mdc-list-item--selected" aria-selected="true" role="option" data-value=""></li>
```

#### 無効なセレクト

初期表示で無効な状態の MDC Select を表示するには、`mdc-select` 要素に `mdc-select--disabled` クラスを追加し、`<select>` 要素に `disabled` 属性を追加してください。

```html
<div class="mdc-select mdc-select--disabled">
  <i class="mdc-select__dropdown-icon"></i>
  <select class="mdc-select__native-control" disabled>
    ...
  </select>
  <label class="mdc-floating-label">Pick a Food Group</label>
  <div class="mdc-line-ripple"></div>
</div>
```

拡張セレクトでは、`mdc-select--disabled` クラスを `mdc-select` 要素に追加し、あれば `disabled` 属性を `<input type="hidden>` 要素に追加します。

```html
<div class="mdc-select mdc-select--disabled">
  <input type="hidden" name="enhanced-select" disabled>
  <i class="mdc-select__dropdown-icon"></i>
  <div class="mdc-select__selected-text"></div>
  <div class="mdc-select__menu mdc-menu mdc-menu-surface">
    ...
  </div>
  <span class="mdc-floating-label">Pick a Food Group</span>
  <div class="mdc-line-ripple"></div>
</div>
```

#### 無効な選択肢

ネイティブな `select` では、単に無効にしたい個々のオプションに `disabled` 属性を追加してください。

```html
<div class="mdc-select">
  <select class="mdc-select__native-control">
    <option value="grains">
      Bread, Cereal, Rice, and Pasta
    </option>
    <option value="vegetables" disabled>
      Vegetables
    </option>
    <option value="fruit">
      Fruit
    </option>
  </select>
  <label class="mdc-floating-label">Pick a Food Group</label>
  <div class="mdc-line-ripple"></div>
</div>
```

拡張セレクトでは、無効にする項目に `mdc-list-item--disabled` クラスを追加しなくてはなりません。ネイティブなセレクトとは異なり、無効なリスト項目はリスト項目のインデックスから削除され、完全に無視されます。拡張セレクトではプログラム的に無効なリスト項目を選択することはできません。

```html
<div class="mdc-select">
  <input type="hidden" name="enhanced-select">
  <i class="mdc-select__dropdown-icon"></i>
  <div class="mdc-select__selected-text">Vegetables</div>
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
  <span class="mdc-floating-label mdc-floating-label--float-above">Pick a Food Group</span>
  <div class="mdc-line-ripple"></div>
</div>
```

### ヘルパーテキストのあるセレクト

ヘルパーテキストは補足情報や検証メッセージをユーザーに提供します。セレクト要素がフォーカスされているときに表示され、デフォルトでフォーカスを失うと非表示なる、もしくは永続化することができます。ヘルパーテキストの使用についてのより詳しい情報は [ここ](helper-text/) を参照してください。

### 先頭にアイコンのあるセレクト

対話のターゲットとしてだけでなく視覚的インジケーターとして MDC Select の標準型、もしくはアウトラン型のものに対して先頭アイコンを追加することができます。アイコンの使用についてのより詳しい情報は [ここ](icon/) を参照してください。

## スタイルのカスタマイズ

### CSS クラス

| クラス | 説明 |
| --- | --- |
| `mdc-select` | 必須。 |
| `mdc-select__menu` | 拡張セレクトを使う際は必須。このクラスは `mdc-select` 要素内の `mdc-menu` 要素に設定しなくてはならない。 |
| `mdc-select__dropdown-icon` | 必須。`mdc-select` 要素内の `i` 要素に設定しなくてはならない。ドロップダウンの三角印 svg とアニメーションに使われる。 |
| `mdc-select__icon` | オプション。`mdc-select` 要素内の `i` もしくは `svg` 要素に設定しなくてはならない。先頭アイコンに使われる。 |
| `mdc-select--activated` | オプション。セレクトのアクティブ状態のスタイル。このクラスはメニューが開かれた際に自動的に追加される。 |
| `mdc-select--disabled` | オプション。無効となっているセレクトのスタイル。このクラスは `<select>` 要素に `disabled` 属性が適用されている際にルート要素に適用しなくてはならない。 |
| `mdc-select--outlined` | オプション。アウトラインされたセレクトのようなセレクトのスタイル。 |
| `mdc-select__native-control` | ネイティブセレクトでは必須。ネイティブな `<select>` 要素。 |
| `mdc-select__selected-text` | 拡張セレクトでは必須。このクラスは `mdc-select` 要素内の `div` に設定しなくてはならない。 |
| `mdc-select--with-leading-icon` | 先頭アイコンのあるセレクトとしてスタイルを設定する。 |

> 注意: セレクト内に含まれる [MDCMenu](./../mdc-menu) や [MDCList](./../mdc-list) コンポーネントをさらにカスタマイズするには、それぞれのドキュメントを参照してください。

### Sass ミキシン

ミキシンはコンポーネントのルート要素に `.my-select` のようにカスタムクラスを適用しているコンテキストに含めなくてはなりません。

Mixin | Description
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

> 注意: これ以上にフローティングラベルを変更する方法は [フローティングラベルのドキュメント](./../mdc-floating-label/README.md) を参照してください。

### `MDCSelect` API

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
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `hasClass(className: string) => boolean` | ルート要素がクラスリストにクラス名を持っていれば true を返す。 |
| `activateBottomLine() => void` | 下線のコンポーネントを有効にする。 |
| `deactivateBottomLine() => void` | 下線のコンポーネントを無効にする。 |
| `getValue() => string` | `select` 要素の選択されている `option` か拡張セレクトの選択されたリスト項目の `data-value` の値を返す。 |
| `floatLabel(value: boolean) => void` | ラベルを上に動かしたり戻したりする。 |
| `getLabelWidth() => number` | ラベル要素の offsetWidth を返す。 |
| `hasOutline() => boolean` | `select` にへこんだ輪郭要素があれば true を返す。 |
| `notchOutline(labelWidth: number) => void` | へこんだ輪郭要素を "へこんだ状態" に切り替える。 |
| `closeOutline() => void` | へこんだ輪郭要素を閉じた状態に切り替える。 |
| `openMenu() => void` | 拡張セレクトのメニュー要素を開く。 |
| `closeMenu() => void` | 拡張セレクトのメニュー要素を閉じる。 |
| `setValue(value: string) => void` | セレクトの値または選択されたテキスト要素のテキストコンテンツを設定する。 |
| `isMenuOpen() => boolean` | 拡張セレクトのメニューが現在開いていれば true を返す。 |
| `setSelectedIndex(index: number) => void` | 指定したインデックスの位置の option もしくはリスト項目を選択する。 |
| `setDisabled(isDisabled: boolean) => void` | ネイティブもしくは拡張セレクトを利用できなくする。 |
| `setRippleCenter(normalizedX: number) => void` | ラインリップルの中心を与えた normalizedX の値に設定する。 |
| `notifyChange(value: string) => void` | 要素が選択された際に `MDCSelect:change` イベントを発生させる。 |
| `checkValidity() => boolean` | コンポーネントが現在有効かどうかを返す。ネイティブセレクトの `checkValidity` もしくは拡張セレクトの同党のロジックを利用している。 |
| `setValid(isValid: boolean) => void` | 無効なスタイルを追加もしく削除する。 |

### `MDCSelectFoundation`

| メソッド | 説明 |
| --- | --- |
| `notchOutline(openNotch: boolean) => void` | へこんだ輪郭を開く、もしくは閉じる。 |
| `setDisabled(isDisabled: boolean) => void` | 無効の状態に応じて外観を更新する。`disabled` の状態が変わるたびにこれを呼び出す必要がある。 |
| `handleFocus() => void` | `select` 要素の focus イベントを処理する。 |
| `handleBlur() => void` | `select` 要素の blur イベントを処理する。 |
| `handleClick(normalizedX: number) => void` | ラインリップルの中心を normalizedX に設定する。 |
| `handleMenuOpened() => void` | メニューもしくはメニュー表面の opened イベントを処理する。 |
| `handleMenuClosed() => void` | メニューもしくはメニュー表面の closed イベントを処理する。 |
| `handleChange() => void` | `select` 要素の値の変更を処理する。`change` イベントとコンポーネント API を通じて要求されたプログラム上での変更の両方でこれを呼び出す必要がある。 |
| `handleKeydown(event: KeyboardEvent) => void` | `mdc-select__selected-text` 要素がフォーカスを持っており、ユーザーが `Enter` または `Space` キーを押した際にメニュー（拡張セレクト）が開くことをハンドリングする。 |
| `setSelectedIndex(index: number) => void` | `mdc-select__selected-text` 要素を設定しメニューを閉じる（拡張セレクトのみ）ことをハンドリングする。必要であればラベルを浮かせ、輪郭をへこませる。 |
| `setValue(value: string) => void` | アダプターを介して値の設定をハンドリングし、必要であればラベルを浮かせ、輪郭をへこませる。 |
| `getValue() => string` | アダプターを介して値の取得をハンドリングする。 |
| `setValid(isValid: boolean) => void` | アダプターを介して有効状態を設定する。 |
| `isValid() => boolean` | アダプターの `checkValidity` API を介して有効状態を取得する。 |
| `layout() => void` | へこんだ輪郭をへこませるべきかどうかの判断をハンドリングする。 |
| `setLeadingIconAriaLabel(label: string) => void` | 先頭アイコンの aria ラベルを設定する。 |
| `setLeadingIconContent(content: string) => void` | 先頭アイコンのテキストコンテンツを設定する。 |
| `setHelperTextContent(content: string) => void` | ヘルパーテキストのコンテンツを設定する。 |

`MDCSelectFoundation` は複数のオプションのサブ要素（ヘルパーテキストとアイコン）をサポートしています。これらのサブ要素のファンデーションは `MDCSelectFoundation` にコンストラクターの引数として渡さなくてはなりません。
