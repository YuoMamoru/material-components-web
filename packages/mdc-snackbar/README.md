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
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/snackbars.png" width="336" alt="Snackbar screenshot">
  </a>
</div>-->

スナックバーは画面の下部にアプリのプロセスに関する簡素なメッセージを提供します。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-snackbar">マテリアルデザインガイドライン: スナックバー</a>
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
<div class="mdc-snackbar">
  <div class="mdc-snackbar__surface">
    <div class="mdc-snackbar__label"
         role="status"
         aria-live="polite">
      Can't send photo. Retry in 5 seconds.
    </div>
    <div class="mdc-snackbar__actions">
      <button type="button" class="mdc-button mdc-snackbar__action">Retry</button>
    </div>
  </div>
</div>
```

### スタイル

```scss
@import "@material/snackbar/mdc-snackbar";
```

### JavaScript のインスタンス化

```js
import {MDCSnackbar} from '@material/snackbar';
const snackbar = new MDCSnackbar(document.querySelector('.mdc-snackbar'));
```

> JavaScript をインポートするより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## 様々な使用法

### スタック

長いテキストを伴う操作ボタンはラベルの横ではなく、ラベルの下に配置するべきです。これはルート要素に `mdc-snackbar--stacked` 修飾クラスを追加することによって実現できます。

```html
<div class="mdc-snackbar mdc-snackbar--stacked">
  ...
</div>
```

あるいは、Sass から `mdc-snackbar-layout-stacked` ミキシンを呼ぶこともできます。

```scss
@media (max-width: $mdc-snackbar-mobile-breakpoint) {
  .my-snackbar {
    @include mdc-snackbar-layout-stacked;
  }
}
```

### 前方配置 (タブレットとデスクトップのみ)

デフォルトでは、スナックバーはビューポートの水平中央に配置されます。

大きな画面では、オプションで `mdc-snackbar--leading` 修飾クラスをルート要素に追加することにより画面の前方の端（LTR では左側、RTL では右側）に表示させることができます。

```html
<div class="mdc-snackbar mdc-snackbar--leading">
  ...
</div>
```

あるいは、Sass から `mdc-snackbar-position-leading` ミキシンを呼ぶこともできます。

```scss
@media (min-width: $mdc-snackbar-mobile-breakpoint) {
  .my-snackbar {
    @include mdc-snackbar-position-leading;
  }
}
```

### ワイド (タブレットとデスクトップのみ)

大きな画面でスナックバーとビューポートの間のマージンを増やすには、メディアクエリ内で `mdc-snackbar-viewport-margin` ミキシンを呼びます。

```scss
@media (min-width: $mdc-snackbar-mobile-breakpoint) {
  .my-snackbar {
    @include mdc-snackbar-viewport-margin($mdc-snackbar-viewport-margin-wide);
  }
}
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-snackbar` | 必須。スナックバー要素のコンテナ。
`mdc-snackbar__label` | 必須。メッセージテキスト。
`mdc-snackbar__actions` | オプション。操作ボタン/アイコン要素があればラップする。
`mdc-snackbar__action` | オプション。操作ボタン。
`mdc-snackbar__dismiss` | オプション。閉じるアイコン ("X")。
`mdc-snackbar--opening` | オプション。スナックバーを開くアニメーションをしている際に自動的に適用される。
`mdc-snackbar--open` | オプション。スナックバーが開いて表示されていることを示す。
`mdc-snackbar--closing` | オプション。スナックバーを閉じるアニメーションをしている際に自動的に適用される。
`mdc-snackbar--leading` | オプション。スナックバーを画面の中央ではなく、前方の端（LTR では左側、RTL では右側）に配置する。
`mdc-snackbar--stacked` | オプション。操作ボタン/アイコンをラベルの横ではなく下に配置する。

### Sass ミキシン

ミキシン | 説明
--- | ---
`mdc-snackbar-fill-color($color)` | スナックバーの塗りの色を設定する。
`mdc-snackbar-label-ink-color($color)` | スナックバーのラベルテキストの色を設定する。
`mdc-snackbar-shape-radius($radius, $rtl-reflexive)` | スナックバー表面の角の丸みを与えられた値に設定する。`$rtl-reflexive` に true を設定すると RTL コンテキストで半径の値を反転する。デフォルトは false。
`mdc-snackbar-min-width($min-width, $mobile-breakpoint)` | タブレット/デスクトップデバイス上でスナックバーの `min-width` を設定する。モバイルでは幅は自動的に 100% が設定される。
`mdc-snackbar-max-width($max-width)` | スナックバーの `max-width` を設定する。
`mdc-snackbar-elevation($z-index)` | スナックバーの重なりの順序を設定する。
`mdc-snackbar-viewport-margin($margin)` | スナックバーとビューポートの間の距離を設定する。
`mdc-snackbar-z-index($z-index)` | スナックバーの `z-index` を設定する。
`mdc-snackbar-position-leading()` | スナックバーを画面の中央ではなく、前方の端（LTR では左側、RTL では右側）に配置する。
`mdc-snackbar-layout-stacked()` | 操作ボタン/アイコンをラベルの横ではなく下に配置する。

> **注意**: `mdc-snackbar__action` と `mdc-snackbar__dismiss` 要素は [`mdc-button`](../mdc-button) と [`mdc-icon-button`](../mdc-icon-button) ミキシンでさらにカスタマイズできます。

## JavaScript API

### `MDCSnackbar` プロパティ

プロパティ | 型 | 説明
--- | --- | ---
`isOpen` | `boolean` (読取専用) | スナックバーが現在開いているかどうかを取得する。
`timeoutMs` | `number` | 自動で閉じるまでのタイムアウト時間をミリ秒単位で取得/設定する。値は `4000` から `10000` でなくてはならず、そうでないとエラーが投げられる。デフォルトは `5000`（5秒）。
`closeOnEscape` | `boolean` | スナックバーがフォーカスされている状態で <kbd>ESC</kbd> キーを押された時にスナックバーを閉じるかどうかを取得/設定する。デフォルトは `true`。
`labelText` | `string` | ラベル要素の `textContent` を取得/設定する。
`actionButtonText` | `string` | 操作ボタン要素の`textContent` を取得/設定する。

> **注意**: スナックバーが開いているときに `labelText` を設定すると、スクリーンリーダーは新しいラベルを表示します。より詳細な情報は [スクリーンリーダー](#screen-readers) を参照してください。

### `MDCSnackbar` メソッド

メソッド | 説明
--- | ---
`open() => void` | スナックバーを開く。
`close(reason: string=) => void` | スナックバーを閉じる。オプションで閉じる理由を指定する。

### イベント

イベント名 | `event.detail` | 説明
--- | --- | ---
`MDCSnackbar:opening` | `{}` | スナックバーが開くアニメーションを開始していることを示す。
`MDCSnackbar:opened` | `{}` | スナックバーが開くアニメーションを終えたことを示す。
`MDCSnackbar:closing` | `{reason: ?string}` | スナックバーが閉じるアニメーションを開始したことを示す。`reason` にはスナックバーが閉じた理由（`dismiss` もしくは `action`）が含まれる。
`MDCSnackbar:closed` | `{reason: ?string}` | スナックバーが閉じるアニメーションを終えたことを示す。`reason` にはスナックバーが閉じた理由（`dismiss` もしくは `action`）が含まれる。

### フレームワーク内での使用

React や Angular といった JavaScript フレームワークを使用しているなら、フレームワークのためのスイッチを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> か <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) の説明に沿ってみてください。

#### `MDCSnackbarAdapter` メソッド

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素からクラスを削除する。
`announce() => void` | スナックバーのラベルテキストをスクリーンリーダーのユーザーに通知する。
`notifyOpening() => void` | スナックバーが開き始めたことを示すイベントを送出する。
`notifyOpened() => void` | スナックバーが開き終えたことを示すイベントを送出する。
`notifyClosing(reason: string) {}` | スナックバーが閉じ始めたことを示すイベントを送出する。`reason` か空でないとき、イベントの `detail` オブジェクトは `reason` プロパティにその値を含む。
`notifyClosed(reason: string) {}` | スナックバーが閉じ終えたことを示すイベントを送出する。`reason` か空でないとき、イベントの `detail` オブジェクトは `reason` プロパティにその値を含む。

#### `MDCSnackbarFoundation` メソッド

メソッド | 説明
--- | ---
`open()` | スナックバーを開く。
`close(action: string)` | スナックバーを閉じる。オプションで閉じる原因となった操作を指定できる。
`isOpen() => boolean` | スナックバーが開いているかどうかを返す。
`getTimeoutMs() => number` | 自動で閉じるまでのタイムアウト時間をミリ秒単位で返す。
`setTimeoutMs(timeoutMs: number)` | 自動で閉じるまでのタイムアウト時間をミリ秒単位で設定する。値は `4000` から `10000` でなくてはならず、そうでないとエラーが投げられる。
`getCloseOnEscape() => boolean` | スナックバーがフォーカスされている状態で <kbd>ESC</kbd> キーを押された時にスナックバーを閉じるかどうかを返す。
`setCloseOnEscape(closeOnEscape: boolean) => void` | スナックバーがフォーカスされている状態で <kbd>ESC</kbd> キーを押された時にスナックバーを閉じるかどうかを設定する。
`handleKeyDown(event: !KeyEvent)` | スナックバーのルート要素上、もしくはルート要素内で `keydown` イベントを処理する。
`handleActionButtonClick(event: !MouseEvent)` | 操作ボタン上、もしくは操作ボタン内で `click` イベントを処理する。
`handleActionIconClick(event: !MouseEvent)` | 閉じるアイコン上、もしくは閉じるアイコン内で `click` イベントを処理する。

#### イベントハンドラー

スナックバーファンデーションをラップするときには、以下のイベントを指定されたファンデーションメソッドにバインドしなくてはなりません。

イベント | 対象 | ファンデーションハンドラー | 登録 | 削除
--- | --- | --- | --- | ---
`keydown` | `.mdc-snackbar` | `handleKeyDown` | 初期の際に | 破棄する際に
`click` | `.mdc-snackbar__action` | `handleActionButtonClick` | 初期の際に | 破棄する際に
`click` | `.mdc-snackbar__dismiss` | `handleActionIconClick` | 初期の際に | 破棄する際に

#### ユーティリティ API

外部フレームワークとライブラリは独自のコンポーネントを実装する際に `util` モジュールから以下のユーティリティメソッドを利用することができます。

メソッド | 説明
--- | ---
`announce(ariaEl: !HTMLElement, labelEl: !HTMLElement=) => void` | ラベルテキストをスクリーンリーダーのユーザーに通知する。

あるいは、フレームワークは [クロージャライブラリの `goog.a11y.aria.Announcer#say()` メソッド](https://github.com/google/closure-library/blob/bee9ced776b4700e8076a3466bd9d3f9ade2fb54/closure/goog/a11y/aria/announcer.js#L80) を使うことができます。

## アクセシビリティ

### スクリーンリーダー

スナックバーは `open()` が呼ばれると、 ["polite" 通知](https://www.w3.org/TR/wai-aria-1.1/#aria-live) を使って自動的にスクリーンリーダーのユーザーにラベルテキストを通知します。

しかし、要素の `textContent` が <em>変わった</em> ときにスクリーンリーダーは [ARIA Live Regions](https://mdn.io/ARIA_Live_Regions) を通知するだけなので、一時的にラベル要素の `textContent` をクリアたり復元するためにMDC スナックバーは `util.announce()` メソッドを提供しています。

> **注意**: スナックバーを開いている間に `labelText` を設定するとスクリーンリーダーは新しいラベルを通知します。

`util.announce()` は以下のスクリーンリーダーとブラウザの最新バージョンをサポートしています。

* [ChromeVox](https://chrome.google.com/webstore/detail/chromevox/kgejglhpjiefppelpmljglcjbhoiplfn)
* [NVDA](https://www.nvaccess.org/):
    - Chrome
    - Firefox
    - IE 11
* [JAWS](https://www.freedomscientific.com/Products/Blindness/JAWS):
    - Chrome
    - Firefox
    - IE 11

現時点で macOS VoiceOver はサポートして<em>いません</em>。

### 閉じるアイコン

スナックバーは数秒後に勝手に消えるようになっていますが、アクセシビリティ向上のために閉じるためのアイコンをオプションで含めることができます。

### 閉じるキー

スナックバーの子要素（例えば操作ボタン）にフォーカスがあるときに <kbd>ESC</kbd> キーを押すとスナックバーは閉じます。

この動作を無効にするには `closeOnEscape` を `false` に設定します。

### JS リップルを使用しない

`mdc-snackbar__action` と `mdc-snackbar__dismiss` 要素は JavaScript で利用可能な [`MDCRipple`](../mdc-ripple) の動作を<em>**するべきではありません**</em>。

スナックバーの終了アニメーションと組み合わさると、リップルはあまりに動作が多く、ユーザーの注意を紛らわせ混乱させてしまいます。
