# Tab

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/tab.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/tab.png" width="363" alt="Tab screenshot">
  </a>
</div>-->

タブはアクティブな状態を持つ選択可能な要素です。

## デザインと API ドキュメント

<!--
<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/chips.html">Material Design guidelines: Chips</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/chips.html">Demo</a>
  </li>
</ul>
-->

## インストール
```
npm install --save @material/tab
```

## 使用法

### HTML 構造

```html
<button class="mdc-tab" role="tab" aria-selected="false">
  <div class="mdc-tab__content">
    <span class="mdc-tab__icon">heart</div>
    <span class="mdc-tab__text-label">Favorites</div>
  </div>
</button>
```

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-tab` | 必須
`mdc-tab--active` | オプション。タブがアクティブであることを示す
`mdc-tab__content` | 必須。タブのテキストラベルであることを示す
`mdc-tab__text-label` | オプション。タブ内のアイコンであることを示す
`mdc-tab__icon` | オプション。タブの先頭のアイコンであることを示す

### Sass ミキシン

タブの任意の場所の色を変更するには以下のミキシンを使用します。

ミキシン | 説明
--- | ---
`mdc-tab-text-label-color($color)` | タブのテキストラベルの色を変更する
`mdc-tab-icon-color($color)` | タブのアイコンの色を変更する

### `MDCTab`

プロパティ | 値の型 | 説明
--- | --- | ---
`active` | `boolean` | タブのアクティブな状態の取得/設定をする
`ripple` | `MDCRipple` | `MDCChip` が初期化したルート要素の `MDCRipple` インスタンス

### `MDCTabAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する
`removeClass(className: string) => void` | ルート要素からクラスを削除する
`hasClass(className: string) => boolean` | ルート要素が与えられたクラスを含んでいれば true を返す
`registerEventHandler(evtType: string, handler: EventListener) => void` | ルート要素にイベントリスナーを登録する
`deregisterEventHandler(evtType: string, handler: EventListener) => void` | ルート要素からイベントリスナーの登録を解除する
`setAttr(attr: string, value: string) => void` | ルート要素に与えられた値を属性として設定する

### `MDCTabFoundation`

メソッド | 説明
--- | ---
`handleTransitionEnd(evt: Event) => void` | `"transitionend"` イベントのためのロジックを制御する
`isActive() => boolean` | タブがアクティブかどうかを返す
`activate() => void` | タブをアクティブにする
`deactivate() => void` | タブをアクティブでないようにする
