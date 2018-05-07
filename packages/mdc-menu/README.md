<!--docs:
title: "Menus"
layout: detail
section: components
excerpt: "Non-cascading Material Design menus."
iconId: menu
path: /catalog/menus/
-->

# Menus

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/menu.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/menus.png" width="178" alt="Menus screenshot">
  </a>
</div>-->

MDC Menu コンポーネントは [マテリアルデザインメニュー仕様](https://material.io/go/design-menus) に準拠したメニューコンポーネントです。メニューが開く際に正しい位置に配置するには JavaScript が必要です。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-menus">マテリアルデザインガイドライン: メニュー</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/menu.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/menu
```

## 使用法

### HTML 構造

メニューは最初は非表示で、JS の API を通じて開かれるときに表示されます。

```html
<div class="mdc-menu" tabindex="-1">
  <ul class="mdc-menu__items mdc-list" role="menu" aria-hidden="true">
    <li class="mdc-list-item" role="menuitem" tabindex="0">
      A Menu Item
    </li>
    <li class="mdc-list-item" role="menuitem" tabindex="0">
      Another Menu Item
    </li>
  </ul>
</div>
```

#### 親要素に基づく配置

メニューは開く際に親要素に基づいて自動的に配置されます。

```html
<div id="toolbar" class="toolbar mdc-menu-anchor">
  <div class="mdc-menu">
  ...
  </div>
</div>
```

#### ラッパーを持つ要素への配置

メニューはアンカークラスをもつほかの要素でラップすることで、その要素に基づいて配置することもできます。

```html
<div id="demo-menu" class="mdc-menu-anchor">
  <button id="menu-button">Open Menu</button>
  <div class="mdc-menu">
  ...
  </div>
</div>
```

#### 無効なメニュー項目

MDC Menu のようなコンポーネントを使うとリスト項目を無効にすることができます。リスト項目を無効にするには `aria-disabled` プロパティに `"true"` を設定し、`tabindex` を `"-1"` にします。

```html
<div class="mdc-menu" tabindex="-1">
  <ul class="mdc-menu__items mdc-list" role="menu" aria-hidden="true">
    <li class="mdc-list-item" role="menuitem" tabindex="0">
      A Menu Item
    </li>
    <li class="mdc-list-item" role="menuitem" tabindex="-1" aria-disabled="true">
      Disabled Menu Item
    </li>
  </ul>
</div>
```

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-menu` | 必須
`mdc-menu--animating-open` | メニューが現在開くアニメーションを実行していることを示します。アニメーションが完了するとこのクラスは削除されます。
`mdc-menu--open` | メニューが現在開いている、もしくは、開くアニメーションを実行していることを示します。
`mdc-menu--animating-closed` | メニューが現在閉じるアニメーションを実行していることを示します。アニメーションが完了するとこのクラスは削除されます。

### JS の例

```js
  // インスタンス化
  var menuEl = document.querySelector('#toolbar');
  var menu = new mdc.menu.MDCMenu(menuEl);
  var menuButtonEl = document.querySelector('#menu-button');

  // メニューの 開く/閉じる を切り替える
  menuButtonEl.addEventListener('click', function() {
    menu.open = !menu.open;
  });

  // 選択項目の取得
  menuEl.addEventListener('MDCMenu:selected', function(evt) {
     var detail = evt.detail;
  });

  // Bottom End に基準の角を設定
  menu.setAnchorCorner(Corner.BOTTOM_END);

  // メニューを開くアニメーションをオフにする
  menu.quickOpen = true;
```

### `MDCMenu`

JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

プロパティ | 型 | 説明
--- | --- | ---
`open` | Boolean | ファンデーションの `isOpen`/(`open`, `close`) メソッドの代替。
`items` | Array<Element> | すべての `.mdc-list-item[role]` 要素を取得するファンデーションのコンテナの代替。
`itemsContainer` | Element | ファンデーションのルート要素に対して `mdc-menu__items` コンテナ要素を照会する。
`quickOpen` | Boolean | ファンネーションの `setQuickOpen()` メソッドの代替。

メソッド | 説明
--- | ---
`show({focusIndex: ?number}) => void` | ファンデーションの `open()` メソッドの代替。オプションのパラメータを使うと、メニューが開いた後にどの項目がフォーカスを受けるかを指定できる。
`hide() => void` | ファンデーションの `close()` メソッドの代替。
`setAnchorCorner(Corner) => void` | ファンデーションの `setAnchorCorner(Corner)` メソッドの代替。
`setAnchorMargin(AnchorMargin) => void` | ファンデーションの `setAnchorMargin(AnchorMargin)` メソッドの代替。
`getDefaultFoundation() => MDCMenuFoundation` | ファンデーションを返す。

### `MDCMenuAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`hasClass(className: string) => boolean` | ルート要素が与えられたクラスをもっているかどうかを表す真偽値を返す。
`hasNecessaryDom() => boolean` | 必要な DOM が存在しているかどうか（つまり `mdc-menu__items` コンテナがあるか）を表す真偽値を返す。
`getAttributeForEventTarget(target: EventTarget, attributeName: string) => string` | イベントの対象の与えられた属性の値を返す。
`getInnerDimensions() => {width: number, height: number}` | 項目のコンテナの幅と高さを持つオブジェクトを返す。
`hasAnchor: () => boolean` | メニューが位置を決めるためのアンカーを持っているかどうかを返す。
`getAnchorDimensions() => {width: number, height: number, top: number, right: number, bottom: number, left: number}` | アンカーの大きさと位置を持つオブジェクト（意味的には `DOMRect` と同じ）を返す。
`getWindowDimensions() => {width: number, height: number}` | ページのピクセル単位の幅と高さを持つオブジェクトを返す。
`getNumberOfItems() => number` | 項目のコンテナ内にある <em>項目</em> 要素の数を返す。素のコンポーネントでは、`role` 属性がメニューリスト要素にあるロールの正しい子ロールと一致するリスト項目の数を数えることによって決めている。例えば、リスト要素が `menu` というロールを持っているなら、`menuitem` というロールを持っているすべての要素を照会する。
`registerInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー `handler` を追加する。
`deregisterInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー `handler` を削除する。
`registerBodyClickHandler(handler: EventListener) => void` | `click` イベントのイベントリスナー `handler` を追加する。
`deregisterBodyClickHandler(handler: EventListener) => void` | `click` イベントのイベントリスナー `handler` を削除する。
`getIndexForEventTarget(target: EventTarget) => number` | イベントの `target` がメニュー項目の一つであるかどうかを確認し、そうならその項目の index を返す。target がメニュー項目の一つでないなら -1 を返す。
`notifySelected(evtData: {index: number}) => void` | メニュー項目が選択されたということをリスナーに通知するイベントを送出する。この関数は選択された項目の位置を表す `index` プロパティを持つオブジェクトを含んだ `evtData` パラメータを受け取る。実装ではこのデータに項目自身のような追加データを追加することもできる。
`notifyCancel() => void` | 項目が選択されずに閉じられたということをリスナーに通知するイベントを送出する。
`saveFocus() => void` | 現在、ドキュメント上のフォーカスのある要素を保存する。復帰させるには `restoreFocus` を使う。
`restoreFocus() => void` | 以前フォーカスされていた要素を再びフォーカスさせることにより、以前保存したフォーカスの状態を復元する。
`isFocused() => boolean` | メニューのルート要素がフォーカスされているかどうかを表す真偽値を返す。
`focus() => void` | メニューのルート要素にフォーカスをあてる。
`getFocusedItemIndex() => number` | 現在フォーカスのあるメニュー項目のインデックスを返す（なければ -1 を返す）。
`focusItemAtIndex(index: number) => void` | 与えられたインデックスを持つメニュー項目にフォーカスをあてる。
`isRtl() => boolean` | 現在の環境が RTL かどうかを表す真偽値を返す。
`setTransformOrigin(value: string) => void` | メニュー要素の transform origin を設定する。
`setPosition(position: {top: string, right: string, bottom: string, left: string}) => void` | メニュー要素の位置を設定する。
`setMaxHeight(value: string) => void` | メニュー要素の `max-height` スタイルを設定する。


### `MDCMenuFoundation`

メソッド | 説明
--- | ---
`setAnchorCorner(corder: Corner) => void` | メニューが基準とする角を設定する。[constants.js](https://github.com/material-components/material-components-web/blob/cc299230728ba5a994866ebd31aaaf1a0f4cc87f/packages/mdc-menu/constants.js#L73) を参照のこと。
`setAnchorMargin(margin: AnchorMargin) => void` | メニューを表示する基準点からの距離を設定する。
`open({focusIndex: ?number}) => void` | メニューを開く。オプションで、メニューが開いた際にフォーカスを受けるリスト項目を指定する `focusIndex` パラメータを持つオブジェクトを指定できる。
`close(evt: ?Event)` | メニューを閉じる。オプションで、メニューが閉じる前にターゲットが無効であるかどうかを確認するためのイベントを指定できる。
`isOpen() => boolean` | メニューが開いているかどうかを表す真偽値を返す。
`setQuickOpen(quickOpen: boolean) => void` | メニューが `open`/`close` メソッドを呼ばれたときにアニメーションなしで開閉するかどうかを設定する。

### イベント

イベント名 | データ | 説明
--- | --- | ---
`MDCMenu:selected` | `{detail: {item: HTMLElement, index: number}}` | 要素が選択されたことを示すために使用する。このイベントには選択された項目とその項目のリストのインデックスも含まれている。
`MDCMenu:cancel` | none | メニューが何も選択されずに閉じたとき（例えば、開いているときに `Esc` を押したり、ページ上のほかの場所をクリックしたときなど）に送出されるイベント。
