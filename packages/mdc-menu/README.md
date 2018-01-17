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
     href="https://material-components-web.appspot.com/simple-menu.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/menus.png" width="178" alt="Menus screenshot">
  </a>
</div>-->

MDC Menu コンポーネントは [マテリアルデザインメニュー仕様](https://material.io/guidelines/components/menus.html) に準拠したメニューコンポーネントです。このコンポーネントはシンプルメニューを実装しています。メニューが正しく動作するには JavaScript が必要ですが、最初の描画時に開いた状態と閉じた状態は正しく表示されます。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/menus.html">マテリアルデザインガイドライン: メニュー</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/simple-menu.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install --save @material/menu
```

## シンプルメニューの使用

シンプルメニューは通常閉じた状態で、開かれるときに表示されます。任意の画面サイズに対応しています。

```html
<div class="mdc-simple-menu" tabindex="-1">
  <ul class="mdc-simple-menu__items mdc-list" role="menu" aria-hidden="true">
    <li class="mdc-list-item" role="menuitem" tabindex="0">
      A Menu Item
    </li>
    <li class="mdc-list-item" role="menuitem" tabindex="0">
      Another Menu Item
    </li>
  </ul>
</div>
```
> 注意: メニューの項目に `0` の `tabindex` を追加するとタブの順序が自動で決まります。ルート要素に `-1` の `tabindex` を追加すると、タブの順序が指定されるのではなく、ルート要素に対してプログラム的にフォーカスをあてることができるようになります。これはメニューが開くとメニューがフォーカスされ、次にタブキーが押されると最初のメニュー項目にフォーカスが移動します。そうではなく、最初のメニュー項目に自動的にフォーカスをあてたいならルート要素から `tabindex="-1"` を削除してください。

```js
let menu = new mdc.menu.MDCSimpleMenu(document.querySelector('.mdc-simple-menu'));
// メニューのオン・オフを切り替えるためにイベントリスナーをボタンに追加
document.querySelector('.some-button').addEventListener('click', () => menu.open = !menu.open);
```

`mdc-simple-menu--open` クラスを HTML に追加し、開いた状態のメニューから始めることもできます。

```html
<div class="mdc-simple-menu mdc-simple-menu--open">
...
</div>
```

### メニューの位置

メニューはそれをアンカー対象の要素によって手動もしくは自動のいずれかで配置することができます。

#### 自動的な配置

メニューにはアンカーという概念があります。メニューはアンカーを使ってどこに配置するか、アンカーのどの角をもとに配置するのかを決めます。

アンカーはメニューを子要素に持ち、表示されている要素です。

```html
<div class="toolbar mdc-menu-anchor">
  <div class="mdc-simple-menu">
  ...
  </div>
</div>
```

もしくは実際に表示されている要素をラップしている要素でも構いません。

```html
<div class="mdc-menu-anchor">
  <button>Open Menu</button>
  <div class="mdc-simple-menu">
  ...
  </div>
</div>
```

> 注意: メニューが正しく配置・表示されるように `overflow: visible` と `position: relative` が `mdc-menu-anchor` のある要素に設定されます。

メニューは親要素に `mdc-menu-anchor` クラスが設定されているかどうかを確認し、設定されているならアンカー要素を基準に自動的に配置します。アンカーの角が指定されていないなら、デフォルトでアンカーの左上（RTL であれば右上）の角からメニューは開きますが、画面の端が近いときは適当な別の角を選択します。

#### 手動での配置

メニューはデフォルトで `position: absolute` となっており、手動で配置したいならユーザが配置しなくてはいけません。

```html
<div class="container">
  <div class="mdc-simple-menu" style="top:0; left: 0;">
  ...
  </div>
</div>
```

メニューはデフォルトで左上（RTL では右上）から開きます。どのようにボタンを配置したかによって開く起点を変えることができます。開く起点を上書きするには `transform-origin` を直接設定するか、以下の便利なクラスを使うことができます。

| クラス                                    | 説明                                 |
| ----------------------------------------- | ------------------------------------ |
| `mdc-simple-menu--open-from-top-left`     | 左上からメニューを開く。             |
| `mdc-simple-menu--open-from-top-right`    | 右上からメニューを開く。             |
| `mdc-simple-menu--open-from-bottom-left`  | 左下からメニューを開く。             |
| `mdc-simple-menu--open-from-bottom-right` | 右下からメニューを開く。             |


#### 無効なメニュー項目

MDC Menu のようなコンポーネントを使うと `mdc-list-item` を無効にすることができます。リスト項目を無効にするには `aria-disabled` に `"true"` を設定し、`tabindex` を `"-1"` にします。

```html
<div class="mdc-simple-menu" tabindex="-1">
  <ul class="mdc-simple-menu__items mdc-list" role="menu" aria-hidden="true">
    <li class="mdc-list-item" role="menuitem" tabindex="0">
      A Menu Item
    </li>
    <li class="mdc-list-item" role="menuitem" tabindex="-1" aria-disabled="true">
      Disabled Menu Item
    </li>
  </ul>
</div>
```

### JS コンポーネントの使用

フレームワークが適切なメニューの動作を慣用的なコンポーネントとコンポーネント / ファンデーション の組み合わせが MDC Simple Menu には付属しています。

コンポーネントには読み書き可能な `open` プロパティがあり、このプロパティはコンポーネントの表示状況を追跡しています。

```js
// 現在の状況を表示
console.log('The menu is ' + (menu.open ? 'open' : 'closed'));
// メニューを開く
menu.open = true;
// メニューを閉じる
menu.open = false;
```

また、コンポーネントにはメニューを表示する（開く）ため、隠す（閉じる）ための 2 つの低レベルなメソッドもあり、メニューを直接制御できます。

```js
// メニューを表示する（開く）
menu.show();
// メニューを隠す（閉じる）
menu.hide();
// メニューを表示し（開き）、index が 1 の位置のメニュー項目にフォーカスをあてる
menu.show({focusIndex: 1});
```

直接表示したり隠したりするときでも `open` ゲッタプロパティを使用することができます。

```js
menu.show();
console.log(`Menu is ${menu.open ? 'open' : 'closed'}.`);
```


#### コードへのインクルード

##### ES2015

```javascript
import {MDCSimpleMenu, MDCSimpleMenuFoundation, util} from '@material/menu';
```

##### CommonJS

```javascript
const mdcMenu = require('mdc-menu');
const MDCSimpleMenu = mdcMenu.MDCSimpleMenu;
const MDCSimpleMenuFoundation = mdcMenu.MDCSimpleMenuFoundation;
const util = mdcMenu.util;
```

##### AMD

```javascript
require(['path/to/mdc-menu'], mdcMenu => {
  const MDCSimpleMenu = mdcMenu.MDCSimpleMenu;
  const MDCSimpleMenuFoundation = mdcMenu.MDCSimpleMenuFoundation;
  const util = mdcMenu.util;
});
```

##### Global

```javascript
const MDCSimpleMenu = mdc.menu.MDCSimpleMenu;
const MDCSimpleMenuFoundation = mdc.menu.MDCSimpleMenuFoundation;
const util = mdc.menu.util;
```

#### 自動的なインスタンス化

シンプルメニューのコンポーネントインスタンスの保持に関して特に気にしないのであれば、単純に `attachTo()` に DOM 要素を渡して呼んでください。

```javascript
mdc.MDCSimpleMenu.attachTo(document.querySelector('.mdc-simple-menu'));
```

#### 手動でのインスタンス化

シンプルメニューはコンストラクタを使って `attachTo` と同様に簡単に初期化できます。

```javascript
import {MDCSimpleMenu} from '@material/menu';

const menu = new MDCSimpleMenu(document.querySelector('.mdc-simple-menu'));
```

#### 選択イベントの制御

メニュー項目が選択されるとメニューコンポーネントは以下の `detail` データを含む `MDCSimpleMenu:selected` カスタムイベントを発生させます。

| プロパティ | 型 | 説明 |
| --- | --- | --- |
| `item` | `HTMLElement` | 選択された項目の DOM 要素 |
| `index` | `number` | 選択された項目の index |

メニューが何も選択されずに閉じると（例えばメニューが開いているときにユーザが `Escape` を押したとか）、何のデータも付随しない `MDCSimpleMenu:cancel` カスタムイベントが代わりに発生します。

### ファンデーションクラスの使用

外部のフレームワークやライブラリがコンポーネントを統合するために使用可能な `MDCSimpleMenuFoundation` クラスが MDC Simple Menu には付属しています。すべてのファンデーションクラスでアダプタオブジェクトが提供されなくてはなりません。シンプルメニューのアダプタは以下の関数を提供しなくてはいけません。

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `hasClass(className: string) => boolean` | 要素が与えられたクラスをもっているかどうかを表す真偽値を返す。 |
| `hasNecessaryDom() => boolean` | 必要な DOM が存在しているかどうか（つまり `mdc-simple-menu__items` コンテナがあるか）を表す真偽値を返す。 |
| `getAttributeForEventTarget(target: EventTarget, attributeName: string) => string` | イベントの対象の与えられた属性の値を返す。 |
| `eventTargetHasClass: (target: EventTarget, className: string) => boolean` | イベントの対象に与えられたクラスがあれば true を返す。 |
| `getInnerDimensions() => {width: number, height: number}` | 項目のコンテナの幅と高さを持つオブジェクトを返す。 |
| `hasAnchor: () => boolean` | メニューが位置を決めるためのアンカーを持っているかどうかを返す。 |
| `getAnchorDimensions() => { width: number, height: number, top: number, right: number, bottom: number, left: number }` | アンカーの大きさと位置を持つオブジェクト（意味的には `DOMRect` と同じ）を返す。 |
| `getWindowDimensions() => {width: number, height: number}` | ページのピクセル単位の幅と高さを持つオブジェクトを返す。 |
| `getNumberOfItems() => numbers` | 項目のコンテナ内にある項目要素の数を返す。素のコンポーネントでは、`role` 属性がメニューリスト要素にあるロールの正しい子ロールと一致するリスト項目の数を数えることによって決めている。例えば、リスト要素が `menu` というロールを持っているなら、`menuitem` というロールを持っているすべての要素を照会する。 |
| `registerInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー `handler` を追加する。 |
| `deregisterInteractionHandler(type: string, handler: EventListener) => void` | イベント `type` のイベントリスナー `handler` を削除する。 |
| `registerBodyClickHandler(handler: EventListener) => void` | 'click' イベントのイベントリスナー `handler` を追加する。 |
| `deregisterBodyClickHandler(handler: EventListener) => void` | 'click' イベントのイベントリスナー `handler` を削除する。 |
| `getIndexForEventTarget(target: EventTarget) => number` | イベントの `target` がメニュー項目の一つであるかどうかを確認し、そうならその項目の index を返す。target がメニュー項目の一つでないなら -1 を返す。上記の `index` と同じ注意がここでも必要。（訳注: 「上記（as above）」は既に削除されたメソッドの説明を指している。そこでは `index` はメニュー項目の要素におけるインデックスで、リストのすべての子要素がメニュー項目である必要はないことに注意するよう記載されている） |
| `notifySelected(evtData: {index: number}) => void` | メニュー項目が選択されたということをリスナーに通知するイベントを送出する。この関数は選択された項目の位置を表す `index` プロパティを持つオブジェクトを含んだ `evtData` パラメータを受け取る。実装ではこのデータに項目自身のような追加データを追加することもできる。 |
| `notifyCancel() => void` | 項目が選択されずに閉じられたということをリスナーに通知するイベントを送出する。 |
| `saveFocus() => void` | 現在、ドキュメント上のフォーカスのある要素を保存する。復帰させるには `restoreFocus` を使う。 |
| `restoreFocus() => void` | 以前フォーカスされていた要素を再びフォーカスさせることにより、以前保存したフォーカスの状態を復元する。 |
| `isFocused() => boolean` | シンプルメニューのルート要素がフォーカスされているかどうかを表す真偽値を返す。 |
| `focus() => void` | シンプルメニューのルート要素にフォーカスをあてる。 |
| `getFocusedItemIndex() => number` | 現在フォーカスのあるメニュー項目のインデックスを返す（なければ -1 を返す）。 |
| `focusItemAtIndex(index: number) => void` | 与えられたインデックスを持つメニュー項目にフォーカスをあてる。 |
| `isRtl() => boolean` | 現在の環境が RTL かどうかを表す真偽値を返す。 |
| `setTransformOrigin(value: string) => void` | メニュー要素の transform origin を設定する。 |
| `setPosition(position: { top: string, right: string, bottom: string, left: string }) => void` | メニュー要素の位置を設定する。 |
| `setMaxHeight(value: string) => void` | メニュー要素の `max-height` スタイルを設定する。 |

### 完全なファンデーション API

#### MDCSimpleMenuFoundation.open({focusIndex: number} = {}) => void

メニューを開きます。フォーカスをあてるメニュー項目の位置を表す `focusIndex` プロパティを含むオブジェクトをオプション引数として取ります。オプションオブジェクトもしくは `focusIndex` を省略したときはメニュー項目にはフォーカスがあたりません。

#### MDCSimpleMenuFoundation.close() => void

メニューを閉じます。

#### MDCSimpleMenuFoundation.isOpen() => boolean

メニューが開いているかどうかを返します。

#### MDCSimpleMenuFoundation.setAnchorCorner(Corner = Corner.TOP_START) => void

メニュー全体を表示するのに十分なスペースがある状態で、メニューの開始位置(ltr では左上、rll では右上）を配置するアンカーの角を指定します。メニュー表示がビューポートの端で制限されてしまう場合、`TOP` は `BOTTOM` であると解釈して表示します。同様に `START` を `END` と解釈することもあります。`BOTTOM_START` か `BOTTOM_END` の位置を指定すると、メニューはアンカーの完全に上もしくは下のいずれかに表示されます。このような場合、メニューの最大の高さが制限されます。`TOP_START` か `TOP_END` の位置を指定すると、アンカーの上もしくは下に収まらないならメニューはより高くなります。（訳注: `BOTTOM_START` か `BOTTOM_END` のときはメニューはアンカーとは重ならないようにアンカーの上か下に表示し、そのとき表示可能な縦方向のスペースが足りなければメニューの高さは表示可能な高さに制限され、メニューがスクロールできるようになる。`TOP_START` か `TOP_END` を指定して縦方向のスペースが足りないとき、メニューはアンカーのさらに上もしくはさらに下の領域も使ってメニュー全体を表示させようとする。）

#### MDCSimpleMenuFoundation.setAnchorMargin({top: number, right: number, bottom: number, left: number}) => void

メニュー表示でのアンカーの 4 辺からのオフセットであるマージンをピクセル単位で指定する。メニューがアンカー（デフォルトではアンカーの角）に重なり、メニューの高さがメニューを収める領域の高さより高くなってしまう（ビューポートの端を超えて拡張されることはない）ときは、マージンは無視され、メニューはアンカーを完全に覆ってしまいます。そのような場合、メニューはアンカーの角をもとに厳格に配置されるわけではなく、この場合のメニューの最大の高さはビューポートの高さによって制限されます。


### ユーティリティ API
コンポーネントと統合する際に、外部のフレームワークやライブラリは以下のユーティリティメソッドを使用できます。

#### util.getTransformPropertyName(globalObj, forceRefresh = false) => String

現在のブラウザで使用されている正確な transform プロパティの名前を返します。

#### util.clamp(value, min = 0, max = 1) => Number

value を最小値と最大値の間に寄せ、寄せた値を返します。

#### util.bezierProgress(time, x1, y1, x2, y2) => Number

与えられた 3 次ベジェ曲線に対して時刻 t 時点でのイージング値を返します。

```
制御点 P0 と P3 をそれぞれ (0,0) と (1,1) とする。
パラメータは以下の通り。
 - time: 0 から 1 の間にスケーリングされたアニメーションの現在時刻。
 - x1: 制御点 P1 の x の値。
 - y1: 制御点 P1 の y の値。
 - x2: 制御点 P2 の x の値。
 - y2: 制御点 P2 の y の値。 
```
