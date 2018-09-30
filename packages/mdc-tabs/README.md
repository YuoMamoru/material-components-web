<!--docs:
title: "Tabs (Deprecated)"
layout: detail
section: components
excerpt: "A tabbed navigation component."
iconId: tabs
path: /catalog/tabs/legacy/
-->

## Important - Deprecation Notice

The `mdc-tabs` package is deprecated and no longer maintained, and is no longer included in the all-in-one
`material-components-web` package. Improved functionality is available across the `mdc-tab-bar`, `mdc-tab-scroller`,
`mdc-tab-indicator`, and `mdc-tab` packages, which are now included in the `material-components-web` package.
Bugs and feature requests will no longer be accepted for this package. It is recommended that you migrate to the new
packages to continue to receive new features and updates.

# MDC Tabs

MDC Tabs コンポーネントには [マテリアルデザインタブガイドライン](https://material.io/go/design-tabs) に準拠したタブナビゲーションコンポーネントを作成するためのコンポーネントが含まれています。これらのコンポーネントは以下の通りです。

- **mdc-tab**: 個別のタブ要素
- **mdc-tab-bar**: `mdc-tab` 要素で構成されるメインコンポーネント
- **mdc-tab-bar-scroller**: コンテナからあふれた `mdc-tab-bar` で水平スクロールをコントロールするコンポーネント

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-tabs">マテリアルデザインガイドライン: タブ</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/tabs">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/tabs
```

## タブの使用

`mdc-tab-bar` は CSS のみのコンポーネントとしても使用で可能であり、より動的な JavaScript コンポーネントとしても使用できます。

タブのラベルには3つの異なるタイプがあります。テキスト、アイコンのみ、そしてアイコン付きテキストです。それぞれの例はデモサイトで見ることができます。

### Icons

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

#### テキストラベルのタブ

```html
<nav id="basic-tab-bar" class="mdc-tab-bar">
  <a class="mdc-tab mdc-tab--active" href="#one">Home</a>
  <a class="mdc-tab" href="#two">Merchandise</a>
  <a class="mdc-tab" href="#three">About Us</a>
  <span class="mdc-tab-bar__indicator"></span>
</nav>
```

#### アイコンラベルのタブ

```html
<nav class="mdc-tab-bar mdc-tab-bar--icon-tab-bar">
  <a class="mdc-tab mdc-tab--active" href="#recents">
    <i class="material-icons mdc-tab__icon" aria-label="Recents">phone</i>
  </a>
  <a class="mdc-tab" href="#favorites">
    <i class="material-icons mdc-tab__icon" aria-label="Favorites">favorite</i>
  </a>
  <a class="mdc-tab" href="#nearby">
    <i class="material-icons mdc-tab__icon" aria-label="nearby">person_pin</i>
  </a>
  <span class="mdc-tab-bar__indicator"></span>
</nav>
```

#### アイコンとテキストのラベルのタブ

```html
<nav id="icon-text-tab-bar" class="mdc-tab-bar mdc-tab-bar--icons-with-text">
  <a class="mdc-tab mdc-tab--with-icon-and-text mdc-tab--active" href="#recents">
    <i class="material-icons mdc-tab__icon" aria-hidden="true">phone</i>
    <span class="mdc-tab__icon-text">Recents</span>
  </a>
  <a class="mdc-tab mdc-tab--with-icon-and-text" href="#favorites">
    <i class="material-icons mdc-tab__icon" aria-hidden="true">favorite</i>
    <span class="mdc-tab__icon-text">Favorites</span>
  </a>
  <a class="mdc-tab mdc-tab--with-icon-and-text" href="#nearby">
    <i class="material-icons mdc-tab__icon" aria-hidden="true">person_pin</i>
    <span class="mdc-tab__icon-text">Nearby</span>
  </a>
  <span class="mdc-tab-bar__indicator"></span>
</nav>
```

#### CSS のみでの実装

CSS だけを利用してインジケータを表示するにはマークアップを変更する必要があります。各 `.mdc-tab` に以下のようにクラス `.mdc-tab__indicator` を伴った子要素を持たせます。

```html
<nav id="basic-tab-bar" class="mdc-tab-bar">
  <a class="mdc-tab mdc-tab--active" href="#one">
    Home
    <span class="mdc-tab__indicator"></span>
  </a>
  <a class="mdc-tab" href="#two">
    Merchandise
    <span class="mdc-tab__indicator"></span>
  </a>
  <a class="mdc-tab" href="#three">
    About Us
    <span class="mdc-tab__indicator"></span>
  </a>
</nav>
```

#### RTL のサポート

祖先の要素に属性 `dir="rtl"` をもつとき、Tab Bars はタブの順序を逆転します。

```html
<html dir="rtl">
  <!--...-->
  <nav id="basic-tab-bar" class="mdc-tab-bar">
    <a class="mdc-tab mdc-tab--active" href="#one">Home</a>
    <a class="mdc-tab" href="#two">Merchandise</a>
    <a class="mdc-tab" href="#three">About Us</a>
    <span class="mdc-tab-bar__indicator"></span>
  </nav>
</html>
```

### 動的な表示の切り替え

表示の切り替えを容易にすることは開発者に託されていますが、デモサイトでは JavaScript を使用する方法の最小限の例を提供しています。以下にも示しておきます。

#### マークアップ:
```html
<section id="dynamic-demo-toolbar">
  <nav id="dynamic-tab-bar" class="mdc-tab-bar" role="tablist">
    <a role="tab" aria-controls="panel-1"
       class="mdc-tab mdc-tab--active" href="#panel-1">Item One</a>
    <a role="tab" aria-controls="panel-2"
       class="mdc-tab" href="#panel-2">Item Two</a>
    <a role="tab" aria-controls="panel-3"
       class="mdc-tab" href="#panel-3">Item Three</a>
    <span class="mdc-tab-bar__indicator"></span>
  </nav>
</section>
<section>
  <div class="panels">
    <p class="panel active" id="panel-1" role="tabpanel" aria-hidden="false">Item One</p>
    <p class="panel" id="panel-2" role="tabpanel" aria-hidden="true">Item Two</p>
    <p class="panel" id="panel-3" role="tabpanel" aria-hidden="true">Item Three</p>
  </div>
  <div class="dots">
    <a class="dot active" data-trigger="panel-1" href="#panel-1"></a>
    <a class="dot" data-trigger="panel-2" href="#panel-2"></a>
    <a class="dot" data-trigger="panel-3" href="#panel-3"></a>
  </div>
</section>
```

#### スクリプト:

```js
var dynamicTabBar = window.dynamicTabBar = new mdc.tabs.MDCTabBar(document.querySelector('#dynamic-tab-bar'));
var dots = document.querySelector('.dots');
var panels = document.querySelector('.panels');

dynamicTabBar.tabs.forEach(function(tab) {
  tab.preventDefaultOnClick = true;
});

function updateDot(index) {
  var activeDot = dots.querySelector('.dot.active');
  if (activeDot) {
    activeDot.classList.remove('active');
  }
  var newActiveDot = dots.querySelector('.dot:nth-child(' + (index + 1) + ')');
  if (newActiveDot) {
    newActiveDot.classList.add('active');
  }
}

function updatePanel(index) {
  var activePanel = panels.querySelector('.panel.active');
  if (activePanel) {
    activePanel.classList.remove('active');
  }
  var newActivePanel = panels.querySelector('.panel:nth-child(' + (index + 1) + ')');
  if (newActivePanel) {
    newActivePanel.classList.add('active');
  }
}

dynamicTabBar.listen('MDCTabBar:change', function ({detail: tabs}) {
  var nthChildIndex = tabs.activeTabIndex;

  updatePanel(nthChildIndex);
  updateDot(nthChildIndex);
});

dots.addEventListener('click', function (evt) {
  if (!evt.target.classList.contains('dot')) {
    return;
  }

  evt.preventDefault();

  var dotIndex = [].slice.call(dots.querySelectorAll('.dot')).indexOf(evt.target);

  if (dotIndex >= 0) {
    dynamicTabBar.activeTabIndex = dotIndex;
  }

  updatePanel(dotIndex);
  updateDot(dotIndex);
})
```

### Sass ミキシン

タブ部分のインクの色をカスタマイズするために以下のミキシンが使用できます。アクティブでないタブを選ぶには `.foo-tab:not(.mdc-tab--active)`、ホバー状態のセレクタには `foo-tab:hover`、アクティブなセレクタには `.foo-tab.mdc-tab--active` といった CSS セレクタを使用してこれらのミキシンを適用することを推奨します。

#### `mdc-tab-ink-color`

タブのすべてのインクの色を設定するにはこのミキシンを使います。

#### `mdc-tab-icon-ink-color`

このミキシンはアイコンのインクの色をカスタマイズします。

#### `mdc-tab-label-ink-color`

このミキシンはラベルのインクの色をカスタマイズします。

#### `mdc-tab-bar-indicator-ink-color`

このミキシンはインジケータのインクの色をカスタマイズします。

### CSS のみのコンポーネントの使用

`mdc-tab-bar` にはマテリアルデザイン仕様に準じたタブのレイアウトを整える CSS が付属しています。CSS のみのタブを使うには単に利用可能なクラス名を使うだけです。利用できる `mdc-tab--active` 修飾クラスに注意してください。これは現在アクティブになっているタブを表すのに使用します。

```html
<nav class="mdc-tab-bar">
  <a class="mdc-tab mdc-tab--active" href="#one">Item One</a>
  <a class="mdc-tab" href="#two">Item Two</a>
  <a class="mdc-tab" href="#three">Three</a>
  <span class="mdc-tab-bar__indicator"></span>
</nav>
```

### JavaScript コンポーネントの使用

`mdc-tab-bar` には `mdc-tab`（タブ）のインスタンスを取り込むためのコンポーネントとファンデーションの組が付属しています。`mdc-tab-bar` は `initialize()` メソッド呼び出しを使い、ルート要素である `mdc-tab-bar` の子のタブ要素を収集し、インスタンス化するファクトリ関数を呼び出します。

#### コードへのインクルード

##### ES2015

```javascript
import {MDCTab, MDCTabFoundation} from '@material/tabs';
import {MDCTabBar, MDCTabBarFoundation} from '@material/tabs';
```

##### CommonJS

```javascript
const mdcTabs = require('@material/tabs');
const MDCTab = mdcTabs.MDCTab;
const MDCTabFoundation = mdcTabs.MDCTabFoundation;

const MDCTabBar = mdcTabs.MDCTabBar;
const MDCTabBarFoundation = mdcTabs.MDCTabBarFoundation;
```

##### AMD

```javascript
require(['path/to/@material/tabs'], mdcTabs => {
  const MDCTab = mdcTabs.MDCTab;
  const MDCTabFoundation = mdcTabs.MDCTabFoundation;

  const MDCTabBar = mdcTabs.MDCTabBar;
  const MDCTabBarFoundation = mdcTabs.MDCTabBarFoundation;
});
```

##### Global

```javascript
const MDCTab = mdc.tabs.MDCTab;
const MDCTabFoundation = mdc.tabs.MDCTabFoundation;

const MDCTabBar = mdc.tabs.MDCTabBar;
const MDCTabBarFoundation = mdc.tabs.MDCTabBarFoundation;
```

#### 自動的なインスタンス化

タブのコンポーネントインスタンスの保持に関して特に気にしないのであれば、単純に `attachTo()` に DOM 要素を渡して呼んでください。

```javascript
mdc.tabs.MDCTabBar.attachTo(document.querySelector('#my-mdc-tab-bar'));
```

#### 手動でのインスタンス化

タブはデフォルトのコンストラクタを使って `attachTo` と同様に簡単に初期化できます。`MDCTabBar` の初期化フェーズ中に `mdc-tab-bar` ノードの内部の各タブ要素から MDCTab のインスタンスを生成する工程がこの過程には含まれています。例えば以下のようにします。

```html
<nav id="my-mdc-tab-bar" class="mdc-tab-bar">
  <a class="mdc-tab mdc-tab--active" href="#one">Item One</a>
  <a class="mdc-tab" href="#two">Item Two</a>
  <a class="mdc-tab" href="#three">Three</a>
  <span class="mdc-tab-bar__indicator"></span>
</nav>
```

```javascript
import {MDCTabBar, MDCTabBarFoundation} from '@material/tabs';

const tabBar = new MDCTabBar(document.querySelector('#my-mdc-tab-bar'));
```

### JavaScript Tab Bar Scroller コンポーネントの使用

`mdc-tab-bar-scroller` には `mdc-tab-bar` のインスタンスをラップするコンポーネントとファンデーションの組が付属しています。`mdc-tab-bar-scroller` は `initialize()` メソッド呼び出しを使い、ルート要素である `mdc-tab-bar-scroller` の子の tab bar 要素を収集し、インスタンス化するファクトリ関数を呼び出します。

`mdc-tab-bar-scroller` の構造には `mdc-tab-bar` のインスタンス、RTL 対応の前方及び後方のインジケータとスクロールフレームが含まれています。インジケータは操作された際にタブバーを左右に動かします。スクロールフレームはタブバーの親要素で、利用可能な幅からタブバーがあふれたときにタブバーを隠す役割を担います。

#### コードへのインクルード

##### ES2015

```javascript
import {MDCTab, MDCTabFoundation} from '@material/tabs';
import {MDCTabBar, MDCTabBarFoundation} from '@material/tabs';
import {MDCTabBarScroller, MDCTabBarFoundationScroller} from '@material/tabs';
```

##### CommonJS

```javascript
const mdcTabs = require('@material/tabs');
const MDCTab = mdcTabs.MDCTab;
const MDCTabFoundation = mdcTabs.MDCTabFoundation;

const MDCTabBar = mdcTabs.MDCTabBar;
const MDCTabBarFoundation = mdcTabs.MDCTabBarFoundation;

const MDCTabBarScroller = mdcTabs.MDCTabBarScroller;
const MDCTabBarScrollerFoundation = mdcTabs.MDCTabBarScrollerFoundation;
```

##### AMD

```javascript
require(['path/to/@material/tabs'], mdcTabs => {
  const MDCTab = mdcTabs.MDCTab;
  const MDCTabFoundation = mdcTabs.MDCTabFoundation;

  const MDCTabBar = mdcTabs.MDCTabBar;
  const MDCTabBarFoundation = mdcTabs.MDCTabBarFoundation;

  const MDCTabBarScroller = mdcTabs.MDCTabBarScroller;
  const MDCTabBarScrollerFoundation = mdcTabs.MDCTabBarScrollerFoundation;
});
```

##### Global

```javascript
const MDCTab = mdc.tabs.MDCTab;
const MDCTabFoundation = mdc.tabs.MDCTabFoundation;

const MDCTabBar = mdc.tabs.MDCTabBar;
const MDCTabBarFoundation = mdc.tabs.MDCTabBarFoundation;

const MDCTabBarScroller = mdc.tabs.MDCTabBarScroller;
const MDCTabBarScrollerFoundation = mdc.tabs.MDCTabBarScrollerFoundation;
```

#### 自動的なインスタンス化

タブのコンポーネントインスタンスの保持に関して特に気にしないのであれば、単純に `attachTo()` に DOM 要素を渡して呼んでください。

```javascript
mdc.tabs.MDCTabBarScroller.attachTo(document.querySelector('#my-mdc-tab-bar-scroller'));
```

#### 手動でのインスタンス化

Tab Bar Scroller はデフォルトのコンストラクタを使って `attachTo` と同様に簡単に初期化できます。`MDCTabBarScroller` の初期化フェーズ中に `mdc-tab-bar-scroller` ノードの内部の `mdc-tab-bar` 要素から `MDCTabBar` のインスタンスを生成する工程がこの過程には含まれています。例えば以下のようにします。

```html
<div id="my-mdc-tab-bar-scroller" class="mdc-tab-bar-scroller">
  <div class="mdc-tab-bar-scroller__indicator mdc-tab-bar-scroller__indicator--back">
    <a class="mdc-tab-bar-scroller__indicator__inner material-icons" href="#" aria-label="scroll back button">
      navigate_before
    </a>
  </div>
  <div class="mdc-tab-bar-scroller__scroll-frame">
    <nav id="my-scrollable-tab-bar" class="mdc-tab-bar mdc-tab-bar-scroller__scroll-frame__tabs">
      <a class="mdc-tab mdc-tab--active" href="#one">Item One</a>
      <a class="mdc-tab" href="#two">Item Two</a>
      <a class="mdc-tab" href="#three">Item Three</a>
      <a class="mdc-tab" href="#four">Item Four</a>
      <a class="mdc-tab" href="#five">Item Five</a>
      <a class="mdc-tab" href="#six">Item Six</a>
      <a class="mdc-tab" href="#seven">Item Seven</a>
      <a class="mdc-tab" href="#eight">Item Eight</a>
      <a class="mdc-tab" href="#nine">Item Nine</a>
      <span class="mdc-tab-bar__indicator"></span>
    </nav>
  </div>
  <div class="mdc-tab-bar-scroller__indicator mdc-tab-bar-scroller__indicator--forward">
    <a class="mdc-tab-bar-scroller__indicator__inner material-icons" href="#" aria-label="scroll forward button">
      navigate_next
    </a>
  </div>
</div>
```

```javascript
import {MDCTabBarScroller, MDCTabBarScrollerFoundation} from '@material/tabs';

const tabBarScroller = new MDCTabBarScroller(document.querySelector('#my-mdc-tab-bar-scroller'));
```

Tab Bar Scroller は DOM 要素をもとにビルドインのファクトリ関数を使用して `mdc-tab-bar` をインスタンス化できます。

```js
import {MDCTabBarScroller, MDCTabBarScrollerFoundation} from '@material/tabs';

const tabBarEl = document.querySelector('#my-mdc-tab-bar');
const scrollerEl = document.querySelector('#my-mdc-tab-bar-scroller');

const tabBarScroller = new MDCTabBarScroller(scrollerEl, undefined, tabBarEl);
```

これにより、Tab Bar Scroller の初期化フェーズ中に MDC Tab Bar のインスタンスが生成されます。

## Tab

### Tab コンポーネント API

#### プロパティ

| プロパティ | 型 | 説明 |
| --- | --- | --- |
| `computedWidth` | `number` | <em>（読み取り専用）</em> タブの幅。 |
| `computedLeft` | `number` | <em>（読み取り専用）</em> タブの左側オフセット。 |
| `isActive` | `boolean` | タブがアクティブかどうか。これを設定するとタブがアクティブになる。 |
| `preventDefaultOnClick` | `boolean` | タブがイベント発生時に `preventDefault()` を呼び出せるかどうか。これを設定するとタブがイベント発生時に `preventDefault()` を呼び出せるようになる。 |

### Tab イベント

#### MDCTab:selected

タブ上でのユーザの操作を通知する。

### ファンデーションクラスの使用

外部のフレームワークやライブラリコンポーネントを統合するために使用可能な `MDCTabFoundation` クラスが MDC Tab には付属しています。すべてのファンデーションクラスでアダプタオブジェクトが提供されなくてはなりません。

### アダプタ API

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `registerInteractionHandler(evt: string, handler: EventListener) => void` | ルート要素に指定したイベント名のためのイベントハンドラを登録する。 |
| `deregisterInteractionHandler(evt: string, handler: EventListener) => void` | ルート要素から指定したイベント名のためのイベントハンドラの登録を解除する。 |
| `getOffsetWidth() => number` | タブの幅を返す。 |
| `getOffsetLeft() => number` | タブの左端から親要素の左端までの距離を返す。 |
| `notifySelected() => {}` | ユーザがタブに対して起こしたアクションを示すイベントを通知する。 |

### 完全なファンデーション API

#### MDCTabFoundation.getComputedWidth() => number

タブの幅を計算して返します。

#### MDCTabFoundation.getComputedLeft() => number

タブの左側オフセットを計算して返します。

#### MDCTabFoundation.isActive() => boolean

タブがアクティブなら true を返します。

#### MDCTabFoundation.setActive(isActive = false) => void

タブをアクティブにします。`isActive` が true ならアクティブであることを表す修飾クラスを追加し、そうでないなら、修飾クラスを削除します。

#### MDCTabFoundation.preventsDefaultOnClick() => boolean

タブがデフォルトのクリックアクションを妨げているときに true を返します。

#### MDCTabFoundation.setPreventDefaultOnClick(preventDefaultOnClick = false) => void

タブの `preventDefaultOnClick` プロパティに渡された `preventDefaultOnClick` 引数の値を設定します。

#### MDCTabFoundation.measureSelf() => void

タブに `computedWidth_` と `computedLeft_` を設定します。

## Tab Bar

### Tab Bar コンポーネント API

#### プロパティ

| プロパティ | 型 | 説明 |
| --- | --- | --- |
| `tabs` | `MDCTab[]` | <em>（読み取り専用）</em> タブバーが所有する MDC Tab のインスタンスの配列。 |
| `activeTab` | `MDCTab` | 現在アクティブなタブ。これを設定するとそのタブがアクティブになる。 |
| `activeTabIndex` | `number` | 現在アクティブなタブのインデックス。これを設定すると与えられたインデックスの位置のタブがアクティブになる。 |

#### MDCTabBar.layout() => void

ファンデーションの `layout()` メソッドの代替です。

### Tab Bar イベント

#### MDCTabBar:change

タブに対してユーザがアクションをしたときに通知をし、選択したタブの変更が行われます。

### ファンデーションクラスの使用

外部のフレームワークやライブラリコンポーネントを統合するために使用可能な `MDCTabBarFoundation` クラスが `mdc-tab-bar` には付属しています。すべてのファンデーションクラスでアダプタオブジェクトが提供されなくてはなりません。

### アダプタ API

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `bindOnMDCTabSelectedEvent() => void` | `MDCTab:selected` イベントのリスナーをルート要素に追加する。 |
| `unbindOnMDCTabSelectedEvent() => void` | `MDCTab:selected` イベントのリスナーをルート要素から削除する。 |
| `registerResizeHandler(handler: EventListener) => void` | ルート要素に resize イベントのイベントリスナーを追加する。 |
| `deregisterResizeHandler(handler: EventListener) => void` | ルート要素から resize イベントのイベントリスナーを削除する。 |
| `getOffsetWidth() => number` | ルート要素の幅を返す。 |
| `setStyleForIndicator(propertyName: string, value: string) => void` | インジケータのスタイルプロパティを設定する。 |
| `getOffsetWidthForIndicator() => number` | インジケータの幅を返す。 |
| `notifyChange(evtData: Object) => void` | evtData を渡して `MDCTabBar:change` イベントを発生させる。 |
| `getNumberOfTabs() => number` | MDC Tabs インスタンスのタブの番号を返す。 |
| `getActiveTab() => MDCTab` | 現在アクティブな MDCTab のインスタンスを返す。 |
| `isTabActiveAtIndex(index: number) => boolean` | index の位置にあるタブがアクティブなら true を返す。 |
| `setTabActiveAtIndex(index: number) => void` | 与えられた index の位置のタブをアクティブにする。 |
| `isDefaultPreventedOnClickForTabAtIndex(index: number) => boolean` | タブがデフォルトのクリックアクションを妨げないなら true を返す。 |
| `setPreventDefaultOnClickForTabAtIndex(index: number, preventDefaultOnClick: boolean)` | 与えられた index の位置のタブに preventDefaultOnClick を設定する。 |
| `measureTabAtIndex(index: number) => void` | 与えられた index の位置のタブの寸法（幅と左側オフセット）を設定する。 |
| `getComputedWidthForTabAtIndex(index: number) => number` | 与えられた index の位置のタブの幅を返す。 |
| `getComputedLeftForTabAtIndex(index: number) => number` | 与えられた index の位置のタブの左側オフセットを返す。 |

### 完全なファンデーション API

#### MDCTabBarFoundation.layout() => void

Tab Bar コンポーネントのレイアウトを設定します。

#### MDCTabBarFoundation.getActiveTabIndex() => number

現在アクティブなタブの位置を返します。

#### MDCTabBarFoundation.getComputedWidth() => number

タブを含んでいる要素の幅を返します。

#### MDCTabBarFoundation.switchToTabAtIndex(index, shouldNotify) => void

アクティブなタブを指定されたインデックスの位置のタブに更新し、`shouldNotify` が true なら `MDCTabBar:change` を発生させます。

#### MDCTabBarFoundation.getActiveTabIndex() => number

現在アクティブなタブの位置を返します。

## Tab Bar Scroller

### Tab Bar Scroller コンポーネント API

#### プロパティ

| プロパティ | 型 | 説明 |
| --- | --- | --- |
| `tabBar` | `MDCTabBar` | <em>（読み取り専用）</em> スクローラのタブバー。 |

#### MDCTabBarScroller.layout() => void

ファンデーションの `layout()` メソッドの代替です。

### ファンデーションクラスの使用

外部のフレームワークやライブラリコンポーネントを統合するために使用可能な `MDCTabBarScrollerFoundation` クラスが MDC Tab Bar Scroller には付属しています。すべてのファンデーションクラスでアダプタオブジェクトが提供されなくてはなりません。

### アダプタ API

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `eventTargetHasClass(target: HTMLElement, className: string) => boolean` | target が与えられたクラス名を持っているとき true を返す。 |
| `addClassToForwardIndicator(className: string) => void` | 前方インジケータに与えられたクラスを追加する。 |
| `removeClassFromForwardIndicator(className: string) => void` | 前方インジケータから与えられたクラスを削除する。 |
| `addClassToBackIndicator(className: string) => void` | 後方インジケータに与えられたクラスを追加する。 |
| `removeClassFromBackIndicator(className: string) => void` | 後方インジケータから与えられたクラスを削除する。 |
| `isRTL() => boolean` | RTL コンテキストを含む場合は true を返し、そうでないときは false を返す。 |
| `registerBackIndicatorClickHandler(handler: EventListener) => void` | `click` イベントが後方インジケータに発生したときに呼ばれるイベントハンドラを登録する。 |
| `deregisterBackIndicatorClickHandler(handler: EventHandler) => void` | `click` イベントが後方インジケータに発生したときに呼ばれるイベントハンドラの登録を解除する。 |
| `registerForwardIndicatorClickHandler(handler: EventHandler) => void` | `click` イベントが前方インジケータに発生したときに呼ばれるイベントハンドラを登録する。 |
| `deregisterForwardIndicatorClickHandler(handler: EventHandler) => void` | `click` イベントが前方インジケータに発生したときに呼ばれるイベントハンドラの登録を解除する。 |
| `registerCapturedInteractionHandler(evt: string, handler: EventHandler) => void` | `focus` や `touchstart`、`mousedown` イベントがコンポーネントのルート要素に発生したときに呼ばれるイベントハンドラを登録する。これらのイベントはキャプチャフェーズ中にリスナーに送られる。これらはタブに対してアクションを起こされたときのスクロールの挙動を制御する。 |
| `deregisterCapturedInteractionHandler(evt: string, handler: EventHandler) => void` | `focus` や `touchstart`、`mousedown` イベントがコンポーネントのルート要素に発生したときに呼ばれるイベントハンドラの登録を解除する。 |
| `registerWindowResizeHandler(handler: EventHandler) => void` | `resize` イベントが `window` に発生したときに呼ばれるイベントハンドラを登録する。 |
| `deregisterWindowResizeHandler(handler: EventHandler) => void `| `resize` イベントが `window` に発生したときに呼ばれるイベントハンドラの登録を解除する。 |
| `getNumberOfTabs() => number` | スクローラのタブバーにあるタブの数を返す。 |
| `getComputedWidthForTabAtIndex(index: number) => number` | 与えられた位置にあるタブの幅を返す。 |
| `getComputedLeftForTabAtIndex(index: number) => number` | 与えられた位置にあるタブの左側オフセットを返す。 |
| `getOffsetWidthForScrollFrame() => number` | スクロールフレームの幅を返す。これは実際に見えているタブの幅と一致する。 |
| `getScrollLeftForScrollFrame() => number` | スクロールフレームの `scrollLeft` の値を返す。 |
| `setScrollLeftForScrollFrame(scrollLeftAmount: number) => void` | スクロールフレームの `scrollLeft` の値を設定する。 |
| `getOffsetWidthForTabBar() => number` | 隠されたものも含めたタブバー <em>全体</em> の幅を返す。 |
| `setTransformStyleForTabBar(value: string) => void` | タブバーの `translateX` `transform` プロパティの値を設定する。 |
| `getOffsetLeftForEventTarget(target: HTMLElement) => number`| 与えられた要素の左側オフセットを返す。 |
| `getOffsetWidthForEventTarget(target: HTMLElement) => number` | 与えられた要素の幅を返す。 |

### 完全なファンデーション API

#### MDCTabBarScrollerFoundation.scrollBack() => void

最も左側のタブがスクロールフレームを横切って一番右のタブになるようにタブバーをスクロールさせます。最も右側に移動するタブは部分的に隠れた状態になり、完全に表示されるわけでも見えなくなる位置に来るわけでもありません。

#### MDCTabBarScrollerFoundation.scrollForward() => void

最も右側のタブがスクロールフレームを横切って一番左のタブになるようにタブバーをスクロールさせます。左端に移動するタブの左端がスクロールフレームの左端に一致する位置になり、部分的に隠れたり完全に見えなくなる位置に来るわけではありません。

> **注意:** イベントの動作に癖があるので、右端のタブが部分的に隠れることを許容しています。そうしているのはそのようなタブをクリックした際に `focus` イベントでフレームを動かすようになっているからです。これは `mouseup` や `click` イベントが発生するより前にタブバーを動かしてしまうため、リップルが発生し、意図したタブが選択されないというシナリオをもたらしてしまいます。（訳注: 動作を確認したところ、`mouseup` や `click` 時のフォーカスではタブがスクロールしないので、ここに書いてあるような問題は生じない。何かの勘違いか、古いバージョンの問題点が記載されたままなのかではないかと思われる。もしくは私の誤訳か...）

#### MDCTabBarScrollerFoundation.scrollToTabAtIndex(index: number) => void

index の位置のタブがスクロールフレーム上を動いて左端に来るようにタブバーをスクロールします。

#### MDCTabBarScrollerFoundation.layout() => void

タブバーが利用できる幅を超えているとき、このメソッドは新しい幅に合わせて前方および後方インジケータを適切な状態（表示/非表示）に再設定します。
