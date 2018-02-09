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
     href="https://material-components-web.appspot.com/select.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/selects.png" width="376" alt="Select screenshot">
  </a>
</div>-->

MDC Select はマテリアルデザインの単一選択ができるセレクトメニューを提供します。これはブラウザのネイティブな `<select>` 要素と類似した機能を持っており、ブラウザのネイティブな要素とともに使われる率直に機能を落としたバージョンを含んでいます。ともに完全にアクセス可能で、完全に RTL 対応しています。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/text-fields.html">マテリアルデザインガイドライン: テキスト欄</a>
  </li>
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/menus.html">マテリアルデザインガイドライン: メニュー</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/select.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install --save @material/select
```

## 使用法

### 完全につくりになっている JS コンポーネントの使用

```html
<div class="mdc-select" role="listbox">
  <div class="mdc-select__surface" tabindex="0">
    <div class="mdc-select__label">Pick a Food Group</div>
    <div class="mdc-select__selected-text"></div>
    <div class="mdc-select__bottom-line"></div>
  </div>
  <div class="mdc-menu mdc-select__menu">
    <ul class="mdc-list mdc-menu__items">
      <li class="mdc-list-item" role="option" tabindex="0">
        Bread, Cereal, Rice, and Pasta
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Vegetables
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Fruit
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Milk, Yogurt, and Cheese
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Meat, Poultry, Fish, Dry Beans, Eggs, and Nuts
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Fats, Oils, and Sweets
      </li>
    </ul>
  </div>
</div>
```

JS は次の通りです。

```js
import {MDCSelect} from '@material/select';

const select = new MDCSelect(document.querySelector('.mdc-select'));
select.listen('MDCSelect:change', () => {
  alert(`Selected "${select.selectedOptions[0].textContent}" at index ${select.selectedIndex} ` +
        `with value "${select.value}"`);
});
```

UMD バンドルを通じて mdc-select を含めることができることに注意してください。UMD はポストアルファで利用できます。

> MDC Select の完全に作成されているバージョンは [mdc-menu](../mdc-menu) と [mdc-list](../mdc-list) のスタイルを手動で取り込んでおく必要があることに注意してください。[material-components-web](../material-components-web) パッケージを使っているのなら、パッケージを処理して、単純にメインのスタイルシートをインポートする必要があるだけです。そうでないなら、<em>このコンポーネントが適切に機能するように mdc-list と mdc-menu の両方のスタイル依存関係を手動でインクルードしなくてはなりません</em>。

#### 選択済みの選択肢を持つセレクト

選択済みの値を持つセレクトコンポーネントを扱う際には、`mdc-select__label` に `mdc-select__label--float-above` 修飾クラスを付加し、選択された選択肢に `aria-selected` を付けるようにしてください。これによりラベルが選択された値の上に移動し、Flash Of Un-styled Content (**FOUC**) を防ぐことができます。（訳注: [Flash Of Un-styled Content](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) はスタイルの設定が完全でない状態でレンダリングされてしまうこと。クラスが正しく設定されていないと値のあるテキスト欄の上にラベルが重なった状態で表示されてしまうので、その状態を避けるために、クラスを設定する必要がある、ということを言っている。）

```html
<div class="mdc-select" role="listbox">
  <div class="mdc-select__surface" tabindex="0">
    <div class="mdc-select__label mdc-select__label--float-above">Pick a Food Group</div>
    <div class="mdc-select__selected-text"></div>
    <div class="mdc-select__bottom-line"></div>
  </div>
  <div class="mdc-menu mdc-select__menu">
    <ul class="mdc-list mdc-menu__items">
      <li class="mdc-list-item" role="option" tabindex="0">
        Bread, Cereal, Rice, and Pasta
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Vegetables
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Fruit
      </li>
      <li class="mdc-list-item" role="option" aria-selected tabindex="0">
        Milk, Yogurt, and Cheese
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Meat, Poultry, Fish, Dry Beans, Eggs, and Nuts
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Fats, Oils, and Sweets
      </li>
    </ul>
  </div>
</div>
```

#### 無効なセレクト

```html
<div class="mdc-select" role="listbox" aria-disabled="true">
  <div class="mdc-select__surface" tabindex="-1">
    <div class="mdc-select__label">Pick a Food Group</div>
    <div class="mdc-select__selected-text"></div>
    <div class="mdc-select__bottom-line"></div>
  </div>
  <div class="mdc-menu mdc-select__menu">
    <ul class="mdc-list mdc-menu__items">
      <li class="mdc-list-item" role="option" tabindex="0">
        Bread, Cereal, Rice, and Pasta
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Vegetables
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Fruit
      </li>
      <li class="mdc-list-item" role="option"  tabindex="0">
        Milk, Yogurt, and Cheese
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Meat, Poultry, Fish, Dry Beans, Eggs, and Nuts
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Fats, Oils, and Sweets
      </li>
    </ul>
  </div>
</div>
```

#### 無効な選択肢

MDC Select のようなコンポーネントを使うと `mdc-list-item` を無効にすることができます。選択肢を無効にするには `aria-disabled` に `"true"` を設定し、`tabindex` を `"-1"` にします。

```html
<div class="mdc-select" role="listbox">
  <div class="mdc-select__surface" tabindex="0">
    <div class="mdc-select__label">Pick a Food Group</div>
    <div class="mdc-select__selected-text"></div>
    <div class="mdc-select__bottom-line"></div>
  </div>
  <div class="mdc-menu mdc-select__menu">
    <ul class="mdc-list mdc-menu__items">
      <li class="mdc-list-item" role="option" tabindex="0">
        Bread, Cereal, Rice, and Pasta
      </li>
      <li class="mdc-list-item" role="option" aria-disabled="true" tabindex="-1">
        Vegetables
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Fruit
      </li>
      <li class="mdc-list-item" role="option"  tabindex="0">
        Milk, Yogurt, and Cheese
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Meat, Poultry, Fish, Dry Beans, Eggs, and Nuts
      </li>
      <li class="mdc-list-item" role="option" tabindex="0">
        Fats, Oils, and Sweets
      </li>
    </ul>
  </div>
</div>
```

#### CSS クラス

| クラス                   | 説明                                            |
| ------------------------ | ----------------------------------------------- |
| `mdc-select`             | 必須。                                          |
| `mdc-select--box`        | ボックスセレクトのようなセレクトのスタイル。    |
| `mdc-list-group`         | オプションのグループ。                          |
| `mdc-list-item`          | リストの項目。                                  |
| `mdc-list-divider`       | 分割線。                                        |

分割線は利用できない選択肢であり、アクセスできるかどうかあいまいにしないために `role="presentation"` も設定するようにしてください。

### Sass ミキシン

セレクトの任意の部分の色を変更するには、以下のミキシンを使ってください。スタイルを適用するにあたり、`.foo-select` のような CSS セレクタ内でこれらのミキシンを使用することを推奨します。

Mixin | Description
--- | ---
`mdc-select-ink-color($color)` | セレクト内の選択された項目を表示する色を設定する。
`mdc-select-container-fill-color($color)` | セレクトの背景色を設定する。 
`mdc-select-label-color($color)` | フォーカスのないセレクトのラベルの色を設定する。このミキシンはセレクトの JS バージョンに対してのみ、使用される。
`mdc-select-focused-label-color($color, $opacity: 0.87)` | フォーカス時のセレクトのラベルの色を設定する。フローティングの際のラベルの不透明度の変更はオプション。
`mdc-select-bottom-line-color($color)` | セレクトのデフォルトの下線の色を設定する。
`mdc-select-focused-bottom-line-color($color)` | フォーカス時のセレクトの下線の色を設定する。

リスト項目の色を変更する方法は [リストのドキュメント](../mdc-list/README.md) を参照してください。

### MDC Select コンポーネント API

MDC Select コンポーネント API は `HTMLSelectElement` の機能のサブセットをもとに作られており、以下に概要を記載しておきます。

#### プロパティ

| プロパティ | 型 | 説明 |
| --- | --- | --- |
| `value` | `string` | <em>（読み取り専用）</em> 現在選ばれている選択肢の `id`。選ばれている選択肢に `id` がないときはその選択肢の `textContent` が使われる。選択肢が選ばれていないときは空の文字列を返す。 |
| `options` | `HTMLElement[]` | <em>（読み取り専用）</em> 選択肢を構成しているメニュー項目の <em>配列</em>。 |
| `selectedIndex` | `number` | 現在選択されている選択肢のインデックス。選択肢が選ばれていないときは -1 が設定される。このプロパティを変更するとセレクト要素が更新される。 |
| `selectedOptions` | `HTMLElement[]` | <em>（読み取り専用）</em> 現在選ばれている選択肢の NodeList。何も選ばれていないときは要素を含まない NodeList。 |
| `disabled` | `boolean` | コンポーネントが無効かどうか。これを設定するとコンポーネントの無効かどうかの状態が設定される。 |

#### メソッド

| メソッド | 説明 |
| --- | --- |
| `item(index: number) => HTMLElement?` | `HTMLSelectElement.prototype.item` に類似している。指定した位置にある選択肢を返す。インデックスが範囲外なら `null` を返す。 |
| `nameditem(key: string) => HTMLElement?` | `HTMLSelectElement.prototype.nameditem` に類似している。与えられた `key` と等しい `id` をもつ選択肢、もしくは与えられた `key` と等しい `name` 属性をもつ選択肢。指定した key の `id` または `name` 属性が見つからないときは `null` を返す。 |

#### イベント

ユーザの操作の結果、選ばれた選択肢が変更されたときに MDC Select JS コンポーネントは `MDCSelect:change` イベントを発生させます。

#### カスタム `MDCMenu` コンポーネントを使ったインスタンス化

`MDCSelect` は選択肢を表示するために配下にある [MDCMenu](../mdc-menu) のインスタンスを制御しています。カスタムメニューのインスタンスをインスタンス化したいときは `MDCSelect` のコンストラクタにオプションの第 3 引数である `menuFactory` を与えることができます。

```js
const menuFactory = menuEl => {
  const menu = new MDCMenu(menuEl);
  // menu を使って何かやる
  return menu;
};
const selectEl = document.querySelector('.mdc-select');
const select = new MDCSelect(selectEl, /* foundation */ undefined, menuFactory);
```

`menuFactory` 関数は `HTMLElement` を渡されると、この要素をアタッチした `MDCMenu` インスタンスを返すでしょう。これはテスト目的で使いますが、それでもなおそれが必要であるならこのように使うことができます。

## ファンデーションクラスの使用

MDC Select をカスタムコンポーネントに統合するためにフレームワーク制作者が使用できるファンデーションクラスが MDC Select には付属しています。MDC Select の特性ゆえ、アダプタはかなり複雑です。私たちはできる限り多くの指針を示すように努めていますが、問題に遭遇したときは GH Issues を通じて私たちに連絡するようにしてください。

### コンポーネント実装者への注意

`MDCSelectFoundation` は Select コンポーネントが以下の 2 つの要件に従っていることを前提としています。

1. コンポーネントは選択メニューとして使用している要素、例えば  **メニュー要素**、を持っています。

2. コンポーネントは `MDCMenu`のインスタンスを制御し、`MDCMenu` はメニュー要素にアタッチされています。

オプションのコンストラクタパラメータ `menuFactory` を使ってこれを達成しています。`menuFactory` はメニュー要素を受け取る関数で、`MDCMenu` コンポーネントインスタンスを返すことを前提としています。フレームワーク内で mdc-select を実装しようと試みたが、この方法がうまくいかず、先ほどの 2 つの要件を満たす適当な方法がないなら、[issue に投稿](https://github.com/material-components/material-components-web/issues/new) してください。

`MDCSelectFoundation` は選択肢が変わったら `resize()` メソッドを使って自身の大きさを変えることもできます。初期化時、もしくはメニュー項目が変わったときにはこのメソッドを呼ぶことを推奨します。例えば、react コンポーネントを構築する際には `componentDidUpdate` 内で `resize()` を呼ぶのが良いでしょう。

### アダプタ API

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `addClassToLabel(className: string) => void` | ラベルにクラスを追加する。 |
| `removeClassFromLabel(className: string) => void` | ラベルからクラスを削除する。 |
| `addClassToBottomLine(className: string) => void` | 下線部分にクラスを追加する。 |
| `removeClassFromBottomLine(className: string) => void` | 下線部分からクラスを削除する。 |
| `setBottomLineAttr(attr: string, value: string) => void` | 下線部分に属性を追加する。 |
| `addBodyClass(className: string) => void` | body にクラスを追加する。 |
| `removeBodyClass(className: string) => void` | body からクラスを削除する。 |
| `setAttr(attr: string, value: string) => void` | ルート要素に値 `value` の属性 `attr` を設定する。 |
| `rmAttr(attr: string) => void` | ルート要素から属性 `attr` を削除する。 |
| `computeBoundingRect() => {left: number, top: number}` | `ClientRect` オブジェクトに似た図形を保持するオブジェクトを返す。`left` と `top` プロパティにはビューポートに他する相対的なページ上の位置が設定されている。これを実現する最も簡単な方法はサーフェス要素の `getBoundingClientRect()` を呼ぶことである。（訳注: サーフェス要素とは `mdc-select__surface` クラスが付加された選択結果を表示している要素のこと） |
| `registerInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー `handler` をサーフェス要素に追加する。 |
| `deregisterInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー `handler` をサーフェス要素から削除する。 |
| `focus() => void` | サーフェス要素にフォーカスをあてる。 |
| `makeTabbable() => void` | サーフェス要素がキーボードを通じたタブフォーカスの対象になるようにする。`tabIndex` プロパティに `0` を設定することにより実現している。 |
| `makeUntabbable() => void` | サーフェス要素がキーボードを通じたタブフォーカスの対象にならないようにする。`tabIndex` プロパティに `-1` を設定することにより実現している。 |
| `getComputedStyleValue(propertyName: string) => string` | サーフェスの与えられたダッシュで連結された CSS プロパティ `propertyName` のスタイル値の計算結果を取得する。`getComputedStyle(...).getPropertyValue(propertyName). ` を使用して実現している。 |
| `setStyle(propertyName: string, value: string) => void` | サーフェス要素のダッシュで連結された CSS プロパティ `propertyName` に値 `value` を設定する。`root.style.setProperty(propertyName, value)`を使用して実現している。 |
| `create2dRenderingContext() => {font: string, measureText: (string) => {width: number}}` | CanvasRenderingContext2d インスタンスの図形を持つオブジェクトを返す。つまり、書き込み可能な文字列プロパティ `font`、文字列を与えたとき指定したフォントで描画した際にどれくらいの幅になるかを意味する `width` プロパティを含むオブジェクトを返すメソッド `measureText` を持つオブジェクトを返す。これを実現する簡単な方法は単純に `document.createElement('canvas').getContext('2d');` を使うことである。 |
| `setMenuElStyle(propertyName: string) => void` | メニュー要素のダッシュで連結された CSS プロパティ `propertyName` に値 `value` を設定する。 |
| `setMenuElAttr(attr: string, value: string) => void` | メニュー要素に値 `value` の属性 `attr` を設定する。 |
| `rmMenuElAttr(attr: string) => void` | メニュー要素から属性 `attr` を削除する。 |
| `getMenuElOffsetHeight() => number` | メニュー要素の `offsetHeight` を返す。 |
| `openMenu(focusIndex: string) => void` | セレクトのニューを開き、与えられた `focusIndex` の位置にある選択肢にフォーカスを移す。focusIndex は範囲内にあることが保証される。 |
| `isMenuOpen() => boolean` | メニューが開かれていれば true を返し、そうでなければ false を返す。 |
| `setSelectedTextContent(selectedTextContent: string) => void` | `.mdc-select__selected-text` 要素のテキストコンテンツに `selectedTextContent` を設定する。 |
| `getNumberOfOptions() => number` | セレクトのニューに含まれている選択肢の数を返す。 |
| `getTextForOptionAtIndex(index: number) => string` | セレクトのメニュー内の指定された index の位置の選択肢のテキストコンテンツを返す。 |
| `getValueForOptionAtIndex(index: number) => string` | セレクトのメニュー内の指定された index の位置の選択肢の value を返す。前述の通り、`HTMLSelectElement` の慣習に沿うようにしている。`value` 属性の代わりに選択された選択肢の `id` の値を返し、選択された選択肢の `textContent` を表示する。フレームワークの実装はその要件にふさわしいようにこのメソッドをカスタマイズしなくてはならない。 |
| `setAttrForOptionAtIndex(index: number, attr: string, value: string) => void` | セレクトのメニュー内の指定した index の位置の選択肢の属性 `attr` に値 `value` を設定する。 |
| `rmAttrForOptionAtIndex(index: number, attr: string) => void` | セレクトのメニュー内の指定した index の位置の選択肢の属性 `attr` を削除する。 |
| `getOffsetTopForOptionAtIndex(index: number) => number` | 指定した index の位置の選択肢要素の `offsetTop` を返す。index は範囲内にあることが保証される。 |
| `registerMenuInteractionHandler(type: string, handler: EventListener) => void` | メニューコンポーネントのルート要素にイベントリスナーを登録する。change イベントのために `MDCMenu:selected` を、メニューを閉じる必要があることを知るために `MDCMenu:cancel` を常時監視している。別のイベントシステムを利用するなら、これらの文字列のいずれか一つのイベントタイプを確認することができ、イベントシステムにつなぐための手順を取ることができる。 |
| `deregisterMenuInteractionHandler(type: string, handler: EventListener) => void` | `registerMenuInteractionHandler` の反対の処理。 |
| `notifyChange() => void` | `HTMLSelectElement` の発行する `change` イベントと同様に、change イベントを送出する。私たちのこのメソッドの実装においてはカスタムイベントを使用しているが、コールバックやリアクティブストリームなどのような通知に必要な仕組みを利用することができる。`foundation.getValue()` と `foundation.getSelectedIndex()` を使いさえすれば、イベント内ではデータを渡すことができることに注意。 |
| `getWindowInnerHeight() => number` | `window` 要素の `innerHeight` プロパティを返す。 |

### 完全なファンデーション API

#### MDCSelectFoundation.getValue() => string

現在選択されている選択肢の value を返します。選択されていないときは空の文字列を返します。

#### MDCSelectFoundation.getSelectedIndex() => number

現在選択されている選択肢の index を返します。選択されていないときは -1 を返します。

#### MDCSelectFoundation.setSelectedIndex(selectedIndex: number) => void

コンポーネントの選択されている index を設定します。

#### MDCSelectFoundation.isDisabled() => boolean

セレクトが無効かそうでないかを返します。

#### MDCSelectFoundation.setDisabled(disabled: boolean) => void

セレクトを有効または無効にします。

## テーマ

セレクトの下線部分はフォーカス時に現在のテーマのプライマリカラーが設定されます。
