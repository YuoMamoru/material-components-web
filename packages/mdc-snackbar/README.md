<!--docs:
title: "Snackbars"
layout: detail
section: components
excerpt: "Snackbars provide brief messages about app processes at the bottom of the screen."
iconId: toast
path: /catalog/snackbars/
-->

# Snackbars

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/snackbar">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/snackbars.png" width="336" alt="Snackbars screenshot">
  </a>
</div>-->

スナックバーは画面の下部にアプリのプロセスに関する簡素なメッセージを提供します。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-snackbar">マテリアルデザインガイドライン: スナックバーとトースト</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/snackbar">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/snackbar
```

## 使用法

### スナックバー DOM

```html
<div class="mdc-snackbar"
     aria-live="assertive"
     aria-atomic="true"
     aria-hidden="true">
  <div class="mdc-snackbar__text"></div>
  <div class="mdc-snackbar__action-wrapper">
    <button type="button" class="mdc-snackbar__action-button"></button>
  </div>
</div>
```

### 開始位置に配置したスナックバー（タブレットとデスクトップのみ）

MDC Snackbar は開始位置に配置することができます（RTL コンテンツを含めて）。開始位置に配置したスナックバーを作るには `mdc-snackbar--align-start` 必須クラスをルート要素に追加します。
（訳注: 開始位置に配置 (start aligned) とは通常の環境では画面の左に配置、RTL 環境では右に配置することをいっています）

```html
<div class="mdc-snackbar mdc-snackbar--align-start"
     aria-live="assertive"
     aria-atomic="true"
     aria-hidden="true">
  <div class="mdc-snackbar__text"></div>
  <div class="mdc-snackbar__action-wrapper">
    <button type="button" class="mdc-snackbar__action-button"></button>
  </div>
</div>
```

### JS コンポーネントの使用

スナックバーのメッセージをオプションである操作ボタンとともに表示するための API を提供する コンポーネント / ファンデーション の組み合わせが MDC Snackbar には付属しています。

#### コードへのインクルード

##### ES2015

```javascript
import {MDCSnackbar, MDCSnackbarFoundation} from '@material/snackbar';
```

##### CommonJS

```javascript
const mdcSnackbar = require('mdc-snackbar');
const MDCSnackbar = mdcSnackbar.MDCSnackbar;
const MDCSnackbarFoundation = mdcSnackbar.MDCSnackbarFoundation;
```

##### AMD

```javascript
require(['path/to/mdc-snackbar'], mdcSnackbar => {
  const MDCSnackbar = mdcSnackbar.MDCSnackbar;
  const MDCSnackbarFoundation = mdcSnackbar.MDCSnackbarFoundation;
});
```

##### Global

```javascript
const MDCSnackbar = mdc.snackbar.MDCSnackbar;
const MDCSnackbarFoundation = mdc.snackbar.MDCSnackbarFoundation;
```

#### 自動的なインスタンス化

スナックバーのコンポーネントインスタンスの保持に関して特に気にしないのであれば、単純に `attachTo()` に DOM 要素を渡して呼んでください。

```javascript
mdc.snackbar.MDCSnackbar.attachTo(document.querySelector('.mdc-snackbar'));
```

#### 手動でのインスタンス化

Snackbars はコンストラクターを使って `attachTo` と同様に簡単に初期化できます。

```javascript
import {MDCSnackbar} from '@material/snackbar';

const snackbar = new MDCSnackbar(document.querySelector('.mdc-snackbar'));
```

#### イベントのハンドリング

スナックバーを表示したり破棄したりする際には、データが付随しない `MDCSnackbar:show` もしくは `MDCSnackbar:hide` カスタムイベントをコンポーネントは生成します。

### メッセージの表示と操作

DOM にアタッチされた MDCSnackbar インスタンスを取得したら、オプションである操作ボタンとともにメッセージを表示するトリガーとなる `show` メソッドを使うことができます。`show` メソッドはスナックバーのデータオブジェクトを引数に取ります。以下の表にプロパティと使い方を示します。

| プロパティ | 効果 | 注意 | 型 |
|-----------|--------|---------|---------|
| message   | 表示するテキストメッセージ。 | 必須 | String |
| timeout   | スナックバーを表示する時間（ミリ秒）。 | オプション（初期値は 2750） | Integer |
| actionHandler | 操作ボタンをクリックされたときに実行する関数。 | オプション | Function |
| actionText | 操作ボタンに表示するテキスト。 | actionHandler を設定したときは必須 |  String |
| multiline | 複数行テキスト用のスペースを持つスナックバーを表示するかどうか。 | オプション |  Boolean |
| actionOnBottom | 複数行テキストの下に操作ボタンを表示するかどうか。 | オプション。multiline が true のときのみ適用される |  Boolean |

### スナックバーの操作ボタンの対応

スナックバーの操作ボタンに対応するには、`show` メソッドに渡すオブジェクトの `actionHandler` オプションプロパティに関数を割り当てます。このプロパティを設定したときは `actionText` プロパティも *設定しなくてはなりません*。

```html
<div class="mdc-snackbar"
     aria-live="assertive"
     aria-atomic="true"
     aria-hidden="true">
  <div class="mdc-snackbar__text"></div>
  <div class="mdc-snackbar__action-wrapper">
    <button type="button" class="mdc-snackbar__action-button"></button>
  </div>
</div>
```

```js
import {MDCSnackbar} from '@material/snackbar';

const snackbar = new MDCSnackbar(document.querySelector('.mdc-snackbar'));
const dataObj = {
  message: messageInput.value,
  actionText: 'Undo',
  actionHandler: function () {
    console.log('my cool function');
  }
};

snackbar.show(dataObj);
```


### 操作ボタンを押された際にスナックバーを維持する

デフォルトでは操作ボタンが押されるとスナックバーが破棄されます。タイムアウトになるまで（ユーザーが操作ボタンを押したかどうかにかかわらず）スナックバーを残しておきたいときは `dismissesOnAction` プロパティを `false` に設定します。

```
const snackbar = new MDCSnackbar(document.querySelector('.mdc-snackbar'));
snackbar.dismissesOnAction = false
```

### ファンデーションクラスの使用

外部のフレームワークやライブラリがコンポーネントを統合するために使用可能な `MDCSnackbarFoundation` クラスが MDC Snackbar には付属しています。すべてのファンデーションクラスでアダプターオブジェクトが提供されなくてはなりません。スナックバーのアダプターは以下の関数を提供しなくてはいけません。

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `setAriaHidden() => void` | ルート要素に `aria-hidden="true"` を追加する。 |
| `unsetAriaHidden() => void` | ルート要素から `aria-hidden` 属性を削除する。 |
| `setActionAriaHidden() => void` | 操作ボタン要素に `aria-hidden="true"`  を追加する。 |
| `unsetActionAriaHidden() => void` | 操作ボタン要素から `aria-hidden` 属性を削除する。 |
| `setActionText(actionText: string) => void` | 操作ボタン要素のテキストを設定する。 |
| `setMessageText(message: string) => void` | メッセージ要素のテキストを設定する。 |
| `setFocus() => void` | 操作ボタンにフォーカスを設定する。 |
| `isFocused() => boolean` | アクションボタンにフォーカスがあるかどうかを検出します。 |
| `visibilityIsHidden() => boolean` | document.hidden プロパティを返す。 |
| `registerBlurHandler(handler: EventListener) => void` | 操作ボタン上で `blur` イベントが発生した際に呼ばれるイベントハンドラーを登録する。 |
| `deregisterBlurHandler(handler: EventListener) => void` | 操作ボタンから `blur` イベントハンドラーの登録を解除する。 |
| `registerVisibilityChangeHandler(handler: EventListener) => void` | `visibilitychange` イベントが発生した際に呼ばれるイベントハンドラーを登録する。 |
| `deregisterVisibilityChangeHandler(handler: EventListener) => void` | `visibilitychange` イベントが発生した際に呼ばれるイベントハンドラーの登録を解除する。 |
| `registerCapturedInteractionHandler(evtType: string, handler: EventListener) => void` | `body` に与えられたイベントタイプのイベントが発生した際に呼ばれるイベントハンドラーを登録する。 |
| `deregisterCapturedInteractionHandler(evtType: string, handler: EventListener) => void` | `body` からイベントハンドラーの登録を解除する。 |
| `registerActionClickHandler(handler: EventListener) => void` | 操作ボタン要素で `click` イベントが発生した際に呼ばれるイベントハンドラーを登録する。 |
| `deregisterActionClickHandler(handler: EventListener) => void` | 操作ボタン要素から `click` イベントハンドラーの登録を解除する。これまでに `registerActionClickHandler` を通じて設定されたイベントハンドラーに対してのみ呼びだす。 |
| `registerTransitionEndHandler(handler: EventListener) => void` | ルート要素上で `transitionend` イベントが呼び出された際に呼ばれるイベントハンドラーを登録する。これが正しく動作するにはベンダプレフィックスを考慮する必要があることに注意。 |
| `deregisterTransitionEndHandler(handler: EventListener) => void` | `transitionend` イベントリスナーからイベントハンドラーの登録を解除する。これまでに `registerTransitionEndHandler` を通じて設定されたイベントハンドラーに対してのみ呼びだす。 |
| `notifyShow() => void` | スナックバーが表示されたことをリスナーに通知するイベントを発生させる。 |
| `notifyHide() => void` | スナックバーが非表示になったことをリスナーに通知するイベントを発生させる。 |

## Flash-Of-Unstyled-Content (FOUC) の回避

`mdc-snackbar` の CSS を非同期で読み込んだ際に、CSS が読み込まれるとスナックバーの移動の動きが走ってしまうため、一瞬 flash-of-unstyled-content (FOUC) が発生するかもしれません。一時的な FOUC を避けるには、`mdc-snackbar` の CSS が読み込まれる前に次のような単純なスタイルを加えます。（訳注: [Flash Of Un-styled Content](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) はスタイルの設定が完全でない状態でレンダリングされてしまうこと。）

```css
.mdc-snackbar { transform: translateY(100%); }
```
これで CSS が完全に読み込まれるまでスナックバーが画面外に移動し、読み込みによる移動の動きを避けることができます。
