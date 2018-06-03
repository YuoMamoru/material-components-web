<!--docs:
title: "Select Menus"
layout: detail
section: components
iconId: menu
path: /catalog/input-controls/select-menus/
-->

## 重要 - デフォルトスタイルが非推奨になります

現在のデフォルトの select のスタイルは将来のバージョンで変更される予定です。マテリアルデザイン仕様ではデフォルトのスタイルが塗り変数を使うとなっています（現在、ボックス変数と呼んでいるものです）。これをデフォルトのスタイルに変更します。`mdc-select--box` クラスを追加することですたいるの変更が起こらないようにできます。

# Select Menus

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/select">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/selects.png" width="376" alt="Select screenshot">
  </a>
</div>-->

MDC Select はマテリアルデザインの単一選択ができるセレクトメニューを提供します。これはブラウザのネイティブな `<select>` 要素のラッパーとして機能します。これは完全に RTL 対応しています。

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

### HTML構造

```html
<div class="mdc-select">
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

```scss
@import "@material/select/mdc-select";
```

### JavaScript オブジェクトのインスタンス化

```js
const select = new mdc.select.MDCSelect(document.querySelector('.mdc-select'));
select.listen('change', () => {
  alert(`Selected option at index ${select.selectedIndex} with value "${select.value}"`);
});
```

JavaScript をインポートする方法についてのより多くの情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## 様々な使用法

### セレクトボックス

セレクトボックス形式は標準の形式として多くのマークアップで使用され、ルート要素に `mdc-select--box` 修飾クラスを加えることによって作成します。

```html
<div class="mdc-select mdc-select--box">
  <select class="mdc-select__native-control">
    ...
  </select>
  <label class="mdc-floating-label">Pick a Food Group</label>
  <div class="mdc-line-ripple"></div>
</div>
```

### 追加情報

#### 選択済みの選択肢を持つセレクト

選択済みの値を持つセレクトコンポーネントを扱う際には、`mdc-floating-label` 要素に `mdc-floating-label--float-above` 修飾クラスを追加し、選択する要素に `selected` 要素を付加します。これによりラベルが選択された値の上に移動し、Flash Of Unstyled Content (**FOUC**) を防ぐことができます。（訳注: [Flash Of Un-styled Content](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) はスタイルの設定が完全でない状態でレンダリングされてしまうこと。クラスが正しく設定されていないと値のあるテキスト欄の上にラベルが重なった状態で表示されてしまうので、その状態を避けるために、クラスを設定する必要がある、ということを言っている。）

```html
<div class="mdc-select">
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

#### プレースホルダーとしてのフローティングラベルの使用

デフォルトでは、`<select>` 要素は最初の利用可能はオプションが選択されています。その代わりに初期表示にプレースフォルダーを表示するには、最初の `<option>` 要素に `disabled` 属性<em>と</em> `selected` 属性を設定し、 `value` を `""` にします。

```html
<option value="" disabled selected></option>
```

#### 無効なセレクト

`mdc-select` 要素に `mdc-select--disabled` クラスを追加し、`<select>` 要素に `disabled` 属性を追加してください。

```html
<div class="mdc-select mdc-select--disabled">
  <select class="mdc-select__native-control" disabled>
    ...
  </select>
  <label class="mdc-floating-label">Pick a Food Group</label>
  <div class="mdc-line-ripple"></div>
</div>
```

#### 無効な選択肢

MDC Select のようなコンポーネントを使うと `mdc-list-item` を無効にすることができます。選択肢を無効にするには `aria-disabled` に `"true"` を設定し、`tabindex` を `"-1"` にします。
MDC Select は `<select>` 要素と `<option>` 要素を使っているので、単純に無効にしたい個々のオプションに `disabled` 属性を追加してください。

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

## スタイルのカスタマイズ

### CSS クラス

| クラス | 説明 |
| --- | --- |
| `mdc-select` | 必須。 |
| `mdc-select--box` | ボックスセレクトのようなセレクトのスタイル。 |
| `mdc-select--disabled` | 無効となっているセレクトのスタイル。このクラスは `<select>` 要素に`disabled` 属性が適用されている際にルート要素に適用しなくてはならない。 |
| `mdc-select__native-control` | 必須。ネイティブな `<select>` 要素。 |

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
`mdc-select-hover-bottom-line-color($color)` | セレクトがホバーされた際の下線の色を設定する。

> 注意: これ以上にフローティングラベルを変更する方法は [フローティングラベルのドキュメント](./../mdc-floating-label/README.md) を参照してください。

### `MDCSelect` API

`MDCSelect` コンポーネント API は `HTMLSelectElement` の機能のサブセットをもとに作られています。

| プロパティ | 型 | 説明 |
| --- | --- | --- |
| `value` | `string` | 現在選択されているオプションの `value`。 |
| `selectedIndex` | `number` | 現在選択されている選択肢のインデックス。選択肢が選ばれていないときは -1 が設定される。このプロパティを変更するとセレクト要素が更新される。 |
| `disabled` | `boolean` | コンポーネントが無効かどうか。これを設定するとコンポーネントの無効かどうかの状態が設定される。 |

### イベント

ユーザの操作の結果、選ばれた選択肢が変更されたときに MDC Select JS コンポーネントは `change` イベントを発生させます。

## Web フレームワークでの使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワークのセレクトを作ることができます。ニーズに合わせて <em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプタを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCSelectAdapter`

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `floatLabel(value: boolean) => void` | ラベルを上に動かしたり戻したりする。 |
| `activateBottomLine() => void` | 下線のコンポーネントを有効にする。 |
| `deactivateBottomLine() => void` | 下線のコンポーネントを無効にする。 |
| `setDisabled(disabled: boolean) => void` | `<select>` 要素に `disabled` プロパティを設定する |
| `registerInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー `handler` を `<select>` 要素に追加する。 |
| `deregisterInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー `handler` を `<select>` 要素から削除する。 |
| `getSelectedIndex() => number` | `<select>` 要素の選択されているインデックスを返す。 |
| `setSelectedIndex(index: number) => void` | `<select>` 要素の選択されているインデックスを設定する。 |
| `getValue() => string` | `<select>` 要素の選択されている値を返す。 |
| `setValue(value: string) => void` | `<select>` 要素の値を設定する。 |

### `MDCSelectFoundation`

| メソッド | 説明 |
| --- | --- |
| `setValue(value: string) => void` | コンポーネントの値を設定する。 |
| `setDisabled(disabled: boolean) => void` | disabled クラスを追加/削除し、コンポーネントの disabled 属性を設定する。 |
| `setSelectedIndex(selectedIndex: number) => void` | コンポーネントの選択されているインデックスを設定する。 |


| `setValue(value: string) => void` | Sets the value of the component. |
| `setDisabled(disabled: boolean) => void` | Adds/removes disabled class, and sets disabled attribute on the component. |
| `setSelectedIndex(selectedIndex: number) => void` | Sets the selected index of the component. |
