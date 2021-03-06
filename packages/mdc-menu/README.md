<!--docs:
title: "Menus"
layout: detail
section: components
excerpt: "Non-cascading Material Design menus."
iconId: menu
path: /catalog/menus/
-->

# Menus

MDC Menu コンポーネントは [マテリアルデザインメニュー仕様](https://material.io/go/design-menus) に準拠したメニューコンポーネントです。メニューが開く際に正しい位置に配置するには JavaScript が必要です。

メニューは一時的な領域に選択肢のリストを表示します。ユーザーがボタン、アクション、その他のコントロールを使う際に選択肢のリストは表示されます。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-menus">マテリアルデザインガイドライン: メニュー</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/menu">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/menu
```

## 基本的な使用法

### HTML 構造

```html
<div class="mdc-menu mdc-menu-surface">
  <ul class="mdc-list" role="menu" aria-hidden="true" aria-orientation="vertical" tabindex="-1">
    <li class="mdc-list-item" role="menuitem">
      <span class="mdc-list-item__ripple"></span>
      <span class="mdc-list-item__text">A Menu Item</span>
    </li>
    <li class="mdc-list-item" role="menuitem">
      <span class="mdc-list-item__ripple"></span>
      <span class="mdc-list-item__text">Another Menu Item</span>
    </li>
  </ul>
</div>
```

### スタイル

```scss
@use "@material/list/mdc-list";
@use "@material/menu-surface/mdc-menu-surface";
@use "@material/menu/mdc-menu";
```

### JavaScript のインスタンス化

```js
import {MDCMenu} from '@material/menu';

const menu = new MDCMenu(document.querySelector('.mdc-menu'));
menu.open = true;
```

> JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## バリエーション

### 選択肢をグループ化したメニュー

メニューにはグループ内の要素の選択状態を表すことの可能なリスト項目のグループを含めることができます。

```html
<div class="mdc-menu mdc-menu-surface" id="demo-menu">
  <ul class="mdc-list" role="menu" aria-hidden="true" aria-orientation="vertical" tabindex="-1">
    <li>
      <ul class="mdc-menu__selection-group">
        <li class="mdc-list-item" role="menuitem">
          <span class="mdc-list-item__ripple"></span>
          <span class="mdc-list-item__graphic mdc-menu__selection-group-icon">
            ...
          </span>
          <span class="mdc-list-item__text">Single</span>
        </li>
        <li class="mdc-list-item" role="menuitem">
          <span class="mdc-list-item__ripple"></span>
          <span class="mdc-list-item__graphic mdc-menu__selection-group-icon">
           ...
          </span>
          <span class="mdc-list-item__text">1.15</span>
        </li>
      </ul>
    </li>
    <li class="mdc-list-divider" role="separator"></li>
    <li class="mdc-list-item" role="menuitem">
      <span class="mdc-list-item__ripple"></span>
      <span class="mdc-list-item__text">Add space before paragraph</span>
    </li>
    ...
  </ul>
</div>
```

### 利用不可のメニュー項目

メニュー項目は `mdc-list-item--disabled` 修飾クラス（[MDC List](../mdc-list) にある）を追加することにより利用不可できます。利用不可のメニュー項目はキーボード操作から除外されます。

### アンカーと配置

#### 親要素へのアンカー

メニューは開く際に親要素に基づいて自動的に配置されます。

```html
<div id="toolbar" class="toolbar mdc-menu-surface--anchor">
  <div class="mdc-menu mdc-menu-surface">
  ...
  </div>
</div>
```

#### ラッパーを持つ要素への配置

メニューはアンカークラスをもつほかの要素でラップすることで、その要素に基づいて配置することもできます。

```html
<div id="demo-menu" class="mdc-menu-surface--anchor">
  <button id="menu-button">Open Menu</button>
  <div class="mdc-menu mdc-menu-surface">
  ...
  </div>
</div>
```

#### 固定配置

メニューは表示の際に固定された配置を使うことができます。

```html
<div class="mdc-menu mdc-menu-surface">
...
</div>
```

```js
// ...
menu.setFixedPosition(true);
```

#### 絶対座標配置

The menu can use absolutely positioned when being displayed.
メニューは表示する際に絶対座標で配置することができます。

```html
<div class="mdc-menu mdc-menu-surface">
...
</div>
```

```js
// ...
menu.setAbsolutePosition(100, 100);
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-menu` | ルート要素に必須
`mdc-menu-surface` | ルート要素に必須。その他の `mdc-menu-surface` クラスに関しては[`mdc-menu-surface` ドキュメント](../mdc-menu-surface) を参照のこと。
`mdc-list` | ネストした `ul` 要素に必須。その他の `mdc-list` クラスに関しては[`mdc-list` ドキュメント](../mdc-list) を参照のこと。
`mdc-menu__selection-group` | 選択肢のグループを表す `mdc-list-item` 要素のグループをラップする際に利用する。
`mdc-menu__selection-group-icon` | どの項目が選択されているかを表すために選択肢グループを使う場合は必須。リスト項目の選択状態を表すアイコンもしくは SVG を含めなくてはならない。
`mdc-menu-item--selected` | 選択肢グループ内のどの項目が選ばれているかを表すために使用する。

### Sass ミキシン

ミキシン | 説明
--- | ---
`width($width)` | メニューの `width` を設定するために使う。単位なし（例えば `4` or `5`）で使うときにはベースの幅（`56px`）をかけて `width` を計算する。単位あり（例えば `240px`、`15%` や `calc(200px + 10px)`）で使うときには与えられた値を厳密に利用して `width` を設定する。
`min-width($min-width)` | メニューの `min-width` を設定する。単位を付けた場合だけ（例えば `240px`、`15%` や `calc(200px + 10px)`）使用できる。

> 追加でスタイルをカスタマイズするオプションについては [メニュー表面](../mdc-menu-surface/README.md#sass-mixins) と [リスト](../mdc-list/README.md#sass-mixins) のドキュメントを参照してください。

### アクセシビリティ

メニューボタン（メニュを開くボタン）の推奨されるロール、状態、プロパティについては WAI-ARIA の慣習についての記事 [Menu Button](https://www.w3.org/TR/wai-aria-practices/#menubutton) を参照してください。

メニューボタンのフォーカスについては

  * <kbd>Enter</kbd> および <kbd>Space</kbd>、<kbd>Down Arrow</kbd> はメニューを開き、最初のメニュー項目にフォーカスを合わせます。
  * <kbd>Up Arrow</kbd> はメニューを開き、最後のメニュー項目にフォーカスを移します。
  * クリックもしくはタッチされたときはリストのルート要素（`role="menu"` が設定されているところ）にフォーカスが設定されます。MDC リストはフォーカスされるとキーボードの操作を処理します。

メニューが開かれたときに常にデフォルトのフォーカス状態を設定するには `setDefaultFocusState` を使います。

フォーカス状態 | 説明
--- | ---
`DefaultFocusState.FIRST_ITEM` | 最初のメニュー項目にフォーカスする。メニューボタンが <kbd>Enter</kbd>、<kbd>Space</kbd>、<kbd>Down Arrow</kbd> を受け取ったときに設定される。
`DefaultFocusState.LAST_ITEM` | 最後のメニュー項目にフォーカスする。 メニューボタンが <kbd>Up arrow</kbd> を受け取ったときに設定される。
`DefaultFocusState.LIST_ROOT` | リストのルート要素にフォーカスする。 メニューボタンがクリックもしくはタッチされたときに設定される。
`DefaultFocusState.NONE` | フォーカスを変更しない。メニューが開いているときにフォーカスを取得したくないなら設定する。（例えばオートコンプリートのドロップダウンメニュー）

## `MDCMenu` のプロパティとメソッド

JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

プロパティ | 値の型 | 説明
--- | --- | ---
`open` | Boolean | メニュー表面の `open` プロパティの代替。
`items` | `Array<Element>` | 全 `.mdc-list-item` 要素の問い合わせ用のリストの代替。
`quickOpen` | Boolean | メニュー表面の `quickOpen` プロパティの代替。
`wrapFocus` | Boolean | リストの `wrapFocus` プロパティの代替。
`hasTypeahead` | Boolean | リストの `hasTypeahead` プロパティの代替。

メソッド | 説明
--- | ---
`setAnchorCorner(Corner) => void` | メニュー表面の `setAnchorCorner(Corner)` メソッドの代替。
`setAnchorMargin(Partial<MDCMenuDistance>) => void` | メニュー表面の `setAnchorMargin(Partial<MDCMenuDistance>)` メソッドの代替。
`setAbsolutePosition(x: number, y: number) => void` | メニュー表面の `setAbsolutePosition(x: number, y: number)` メソッドの代替。
`setFixedPosition(isFixed: boolean) => void` | メニュー表面の `setFixedPosition(isFixed: boolean)` メソッドの代替。
`setSelectedIndex(index: number) => void` | 指定したインデックスのリスト項目を選択状態に設定する。
`setIsHoisted(isHoisted: boolean) => void` | メニュー表面の `setIsHoisted(isHoisted: boolean)` メソッドの代替。
`setAnchorElement(element: Element) => void` | メニュー表面の `setAnchorElement(element)` メソッドの代替。
`getOptionByIndex(index: number) => Element \| null` | `index` に指定したところにあるリスト項目を返す。
`getPrimaryTextAtIndex(index: number) => string` | 指定した `index` のプライマリテキストを返す。
`getDefaultFoundation() => MDCMenuFoundation` | ファンデーションを返す。
`setDefaultFocusState(focusState: DefaultFocusState) => void` | メニューが開かれたときに常にメニューのフォーカスされる場所のデフォルトを設定する。デフォルトではリストのルート要素（`DefaultFocusState.LIST_ROOT`）がフォーカスされる。
`setEnabled(index: number, isEnabled: boolean) => void` | 与えられた `index` のメニュー項目の無効かどうかの状態を `isEnabled` に設定する。
`layout() => void` | リストの `layout` メソッドの代替。
`typeaheadMatchItem(nextChar: string) => number` | タイプアヘッドバッファーに文字を追加し、バッファーに一致するリスト内の次の項目のインデックスを返す。

> プロキシメソッドとプロパティについてのより詳細な情報は [メニュー表面](../mdc-menu-surface/README.md) and [リスト](../mdc-list/README.md)  を参照してください。

## Web フレームワーク内での使用

React や Angular といった JavaScript フレームワークを使っているなら、そのフレームワーク用のメニューを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> か <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCMenuAdapter`

メソッド | 説明
--- | ---
`addClassToElementAtIndex(index: number, className: string) => void` | `index` に指定したところにある要素に `className` のクラスを追加する。
`removeClassFromElementAtIndex(index: number, className: string) => void` | `index` に指定したところにある要素から `className` のクラスを削除する。
`addAttributeToElementAtIndex(index: number, attr: string, value: string) => void` | `index` に指定したところにある要素に値 `value` を持つ `attr` 属性を追加する。
`removeAttributeFromElementAtIndex(index: number, attr: string) => void` | `index` に指定したところにある要素から `attr` 属性を削除する。
`elementContainsClass(element: Element, className: string) => boolean` | `element` が `className` のクラスを含んでいれば true を返す。
`closeSurface(skipRestoreFocus?: boolean) => void` | メニューを閉じる。`skipRestoreFocus` が true なら、以前フォーカスされていた要素に対するフォーカスの復元をスキップする。
`getElementIndex(element: Element) => number` | `element` の `index` の値を返す。
`notifySelected(index: number) => void` | `index` に指定したところにある要素に対して `MDCMenu:selected` イベントを発行する。
`getMenuItemCount() => number` | メニュー項目の数を返す。
`focusItemAtIndex(index: number)` | 与えられたインデックスのメニュー項目にフォーカスする。
`focusListRoot() => void` | リストのルート要素にフォーカスする。
`getSelectedSiblingOfItemAtIndex(index: number) => number` | 与えられた `index` の兄弟要素である同じグループ内にある選択されたリスト項目のインデックスを返す。
`isSelectableItemAtIndex(index: number) => boolean` | 指定したインデックスのメニュー項目が `.mdc-menu__selection-group` 要素を含んでいれば true を返す。

### `MDCMenuFoundation`

メソッド | 説明
--- | ---
`handleKeydown(evt: Event) => void` | メニュー内の `keydown` イベントのイベントハンドラー。
`handleItemAction(listItem: Element) => void` | リストのアクションイベントのイベントハンドラー。
`handleMenuSurfaceOpened() => void` | メニュー表面を開くイベントのイベントハンドラー。
`setDefaultFocusState(focusState: DefaultFocusState) => void` | メニューが開かれたときに常にメニューのフォーカスされる場所のデフォルトを設定する。デフォルトではリストのルート要素（`DefaultFocusState.LIST_ROOT`）がフォーカスされる。
`setSelectedIndex(index: number) => void` | 与えられた `index` のメニュー項目を選択する。
`setEnabled(index: number, isEnabled: boolean) => void` | 与えられた `index` のメニュー項目の無効かどうかの状態を設定する。

### イベント

イベント | データ | 説明
--- | --- | ---
`MDCMenu:selected` | `{detail: {item: Element, index: number}}` | 要素が選択されたことを示すために使用する。このイベントには選択された項目とその項目のリストのインデックスも含まれている。
