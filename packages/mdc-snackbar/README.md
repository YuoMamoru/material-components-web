<!--docs:
title: "Snackbars"
layout: detail
section: components
excerpt: "Snackbars provide brief messages about app processes at the bottom of the screen."
iconId: toast
path: /catalog/snackbars/
-->

> ✨ あなたは Material Design web コミュニティの一員ですか？この <a href='https://bit.ly/materialwebsurvey'>**10分調査**</a> にご記入ください。 ✨

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

## 基本的な使用法

### HTML 構造

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

### スタイル

```scss
@import "@material/snackbar/mdc-snackbar";
```

### JavaScript のインスタンス化

MDC Snackbar にはオプションである動作とともにスナックバーメッセージを表示するための API を提供するコンポーネント/ファンデーションの組み合わせが付属しています。

```js
import {MDCSnackbar} from '@material/snackbar';

const snackbar = new MDCSnackbar(document.querySelector('.mdc-snackbar'));
```

> JavaScript をインポートするより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## 様々な使用法

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

### 追加の情報

#### Flash-Of-Unstyled-Content (FOUC) の回避

`mdc-snackbar` の CSS を非同期で読み込んだ際に、CSS が読み込まれるとスナックバーの移動の動きが走ってしまうため、一瞬 flash-of-unstyled-content (FOUC) が発生するかもしれません。一時的な FOUC を避けるには、`mdc-snackbar` の CSS が読み込まれる前に次のような単純なスタイルを加えます。（訳注: [Flash Of Un-styled Content](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) はスタイルの設定が完全でない状態でレンダリングされてしまうこと。）

```css
.mdc-snackbar { transform: translateY(100%); }
```
これで CSS が完全に読み込まれるまでスナックバーが画面外に移動し、読み込みによる移動の動きを避けることができます。

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-snackbar` | 必須。スナックバー要素のコンテナ。
`mdc-snackbar__action-wrapper` | 必須。操作ボタンをラップする。
`mdc-snackbar__action-button` | 必須。操作ボタン。
`mdc-snackbar__text` | 必須。スナックバーのテキスト。
`mdc-snackbar--align-start` | オプション。LTR 依存の開始位置にスナックバーを整列させるためのクラス。
`mdc-snackbar--action-on-bottom` | mdc-snackbar 要素につけるオプション。スナックバーを下に動かす。js で適用される。
`mdc-snackbar--multiline` | mdc-snackbar 要素につけるオプション。スナックバーを複数行にする。js で適用される。

## `MDCSnackbar` プロパティとメソッド

プロパティ | 型 | 説明
--- | --- | ---
`dismissesOnAction` | `boolean` | 操作ボタンがクリックされたときにスナックバーを終了するかどうか、もしくはタイムアウトまで待機しているかどうか。デフォルトは `true`。

メソッド | 説明
--- | ---
`show(data: DataObject=) => void` | スナックバーを表示する。`data` でスナックバーに設定がなされ、オプション（以下で説明）が設定される。

### DataObject プロパティ

 プロパティ | 型 | 説明
--- | --- | ---
 `message` | string | 必須。表示するテキストメッセージ。
 `timeout` | number | スナックバーを表示する時間（ミリ秒）。デフォルトは `2750`。
 `actionHandler` | function | 操作ボタンをクリックされたときに実行する関数。
 `actionText` | string | `actionHandler` を設定するときは必須。操作ボタンに表示するテキスト。
 `multiline` | boolean | 複数行テキスト用のスペースを持つスナックバーを表示するかどうか。
 `actionOnBottom` | boolean | 複数行テキストの下に操作ボタンを表示するかどうか（`multiline` が true のときだけ適用できる）。

### イベント

イベント名 | `event.detail` | 説明
--- | --- | ---
`MDCSnackbar:hide` | `{}` | スナックバーが隠れたときに発生する。
`MDCSnackbar:show` | `{}` | スナックバーが表示されたときに発生する。

## フレームワーク内での使用

React や Angular といった JavaScript フレームワークを使用しているなら、フレームワークのためのスイッチを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> か <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) の説明に沿ってみてください。

### `MDCSnackbarAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`setAriaHidden() => void` | ルート要素に `aria-hidden="true"` を追加する。
`unsetAriaHidden() => void` | ルート要素から `aria-hidden` 属性を削除する。
`setActionAriaHidden() => void` | 操作ボタン要素に `aria-hidden="true"`  を追加する。
`unsetActionAriaHidden() => void` | 操作ボタン要素から `aria-hidden` 属性を削除する。
`setActionText(actionText: string) => void` | 操作ボタン要素のテキストを設定する。
`setMessageText(message: string) => void` | メッセージ要素のテキストを設定する。
`setFocus() => void` | 操作ボタンにフォーカスを設定する。
`isFocused() => boolean` | アクションボタンにフォーカスがあるかどうかを検出します。
`visibilityIsHidden() => boolean` | document.hidden プロパティを返す。
`registerBlurHandler(handler: EventListener) => void` | 操作ボタン上で `blur` イベントが発生した際に呼ばれるイベントハンドラーを登録する。
`deregisterBlurHandler(handler: EventListener) => void` | 操作ボタンから `blur` イベントハンドラーの登録を解除する。
`registerVisibilityChangeHandler(handler: EventListener) => void` | `visibilitychange` イベントが発生した際に呼ばれるイベントハンドラーを登録する。
`deregisterVisibilityChangeHandler(handler: EventListener) => void` | `visibilitychange` イベントが発生した際に呼ばれるイベントハンドラーの登録を解除する。
`registerCapturedInteractionHandler(evtType: string, handler: EventListener) => void` | `body` に与えられたイベントタイプのイベントが発生した際に呼ばれるイベントハンドラーを登録する。
`deregisterCapturedInteractionHandler(evtType: string, handler: EventListener) => void` | `body` からイベントハンドラーの登録を解除する。
`registerActionClickHandler(handler: EventListener) => void` | 操作ボタン要素で `click` イベントが発生した際に呼ばれるイベントハンドラーを登録する。
`deregisterActionClickHandler(handler: EventListener) => void` | 操作ボタン要素から `click` イベントハンドラーの登録を解除する。これまでに `registerActionClickHandler` を通じて設定されたイベントハンドラーに対してのみ呼びだす。
`registerTransitionEndHandler(handler: EventListener) => void` | ルート要素上で `transitionend` イベントが呼び出された際に呼ばれるイベントハンドラーを登録する。これが正しく動作するにはベンダプレフィックスを考慮する必要があることに注意。
`deregisterTransitionEndHandler(handler: EventListener) => void` | `transitionend` イベントリスナーからイベントハンドラーの登録を解除する。これまでに `registerTransitionEndHandler` を通じて設定されたイベントハンドラーに対してのみ呼びだす。
`notifyShow() => void` | スナックバーが表示されたことをリスナーに通知するイベントを発生させる。
`notifyHide() => void` | スナックバーが非表示になったことをリスナーに通知するイベントを発生させる。
