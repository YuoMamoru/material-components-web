<!--docs:
title: "Icon Toggle Buttons"
layout: detail
section: components
iconId: button
path: /catalog/buttons/icon-toggle-buttons/
-->

> ✨ Are you a part of the Material Design web community? Help us improve by filling out this <a href='https://bit.ly/materialwebsurvey'>**10 minute survey**</a>. ✨

## Important - Deprecation Notice

The existing `MDCIconToggle` component and styles will be removed in a future release. Some of its functionality
will be available in the [MDC Icon Button](../mdc-icon-button) package instead. Bugs and feature requests
will no longer be accepted for the `mdc-icon-toggle` package. It is recommended that you migrate to the
`mdc-icon-button` package to continue to receive new features and updates.

# Icon Toggle Buttons

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/icon-button">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/icon-toggles.png" width="20" alt="Icon toggles screenshot">
  </a>
</div>-->

MDC Icon Toggle はマテリアルデザインのアイコン切り替えボタンを提供します。これは完全にアクセス可能で、どのようなアイコンセットでも動作するように設計されています。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-buttons#toggle-button">マテリアルデザインガイドライン: 切り替えボタン</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/icon-button">デモ（アイコンボタン）</a>
  </li>
</ul>

## インストール

```
npm install @material/icon-toggle
```

## 基本的な使用法

### HTML 構造

```html
<i class="mdc-icon-toggle material-icons" role="button" aria-pressed="false"
   aria-label="Add to favorites" tabindex="0"
   data-toggle-on='{"label": "Remove from favorites", "content": "favorite"}'
   data-toggle-off='{"label": "Add to favorites", "content": "favorite_border"}'>
  favorite_border
</i>
```

JS では次のようにします。

```js
import {MDCIconToggle} from '@material/icon-toggle';

MDCIconToggle.attachTo(document.querySelector('.mdc-icon-toggle'));
```

CommonJS/AMD の使用を通じて `require` なオブジェクトの `default` プロパティを使って `MDCIconToggle` にアクセスする以外に、グローバルな `mdc.IconToggle` を通じてアクセスすることもできます。

初期化時の `aria-label` 属性と `favorite_border` コンテンツは省略することもできます。これはコンポーネントがそれらを追加するからです。しかし、最初にスタイルの設定されていないコンテンツが表示されてしまうことを防ぐためにつけることをお勧めします。

### アイコンセット

MDC Icon Toggle を使うには、アイコンセットをインポートする必要があります。

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、あなたの好きなアイコンセットを使うこともできます。詳細は [Font Awesome の節](#font-awesome) を参照してください。

<a id="font-awesome"></a>
#### Font Awesome とそれに類似したライブラリを使用する

[Font Awesome](https://fontawesome.com/) とそのほかのポピュラーなアイコンフォントライブラリはアイコンを表示するために `content` プロパティを通じて疑似要素を使います。また、MDC Web はリップルスタイルに疑似要素を使います。これに対応するため、アイコントグル内にアイコン自体をネストすることができます。

```html
<span class="mdc-icon-toggle" role="button" aria-pressed="false"
      aria-label="Star this item" tabindex="0"
      data-icon-inner-selector=".fa"
      data-toggle-on='{"cssClass": "fa-star", "label": "Unstar this item"}'
      data-toggle-off='{"cssClass": "fa-star-o", "label": "Star this item"}'>
  <i class="fa fa-star-o" aria-hidden="true"></i>
</span>
```

`data-icon-inner-selector` は MDCIconToggle にその属性値と一致するセレクタを持つ要素を探し、アイコンを含んだ要素として扱うよう、指示します。アイコン上の `aria-hidden` 属性にも注目してください。これは要素を描画する際に、スクリーンリーダーが適切な出力を生成することを保証するために重要です。

### アイコン切り替え状態の設定

上のサンプルで `data-toggle-on` と `data-toggle-off` の使い方に注意してください。MDCIconToggle インスタンスを切り替える際、どのように要素を更新するかを決めるためにこのデータが参照されます。これにより MDCIconToggle は柔軟性を持つことができます。`data-toggle-on` の設定は MDCIconToggle の切り替えがオンの時に使われ、`data-toggle-off` は逆のケースで使われます。双方の data 属性は JSON にエンコードされます。この属性には以下のプロパティを含めることができます。

プロパティ | 説明
--- | ---
`label` | 要素の aria-label 属性に適用する値。
`content` | 要素に設定するテキストコンテンツ。内部にアイコンを使用しているなら、代わりにテキストコンテンツがその要素に設定されることに注意。
`cssClass` | 与えられた切り替え状態のアイコン要素に適用される CSS クラス。`content` に適用されたものと同じルールが内部のアイコン要素にして適用される。

### 無効になったアイコン切り替え

```html
<i class="material-icon mdc-icon-toggle mdc-icon-toggle--disabled"
   role="button" tabindex="-1" aria-pressed="false" aria-disabled="true"
   data-toggle-on='{"content": "favorite"}' data-toggle-off='{"content": "favorite_border"}'></i>
```

### 変更イベントの取得

<em>ユーザーの操作により</em> アイコン切り替えの値が変わったときに、`MDCIconToggle` は `MDCIconToggle:change` カスタムイベントを発生させます。通常の入力における `change` イベントと連携して動作します。加えて、これらのイベントはバブリングせず、キャンセルもできません。

カスタムイベントの `detail` オブジェクトはコンポーネントがオンになっているかどうかを示す `isOn` プロパティを持っています。

```js
const iconEl = document.querySelector('.mdc-icon-toggle');
const status = document.getElementById('status');
iconEl.addEventListener('MDCIconToggle:change', ({detail}) => {
  status.textContent = `Icon Toggle is ${detail.isOn ? 'on' : 'off'}`;
});
```

### 素のコンポーネントを通じての切り替えのリフレッシュ

アイコン切り替えを初期化した際に、要素の相互作用時に冗長な JSON の解析を避けるために `data-toggle-on` と `data-toggle-off` 属性はキャッシュされます。しかし、必要であれば `refreshToggleData()` を呼ぶことも可能です。

```js
iconToggle.refreshToggleData();
```

これは単純にファンデーションの `refreshToggleData()` メソッド呼び出しをするだけで、`data-toggle-*` 属性を再び解析し、更新します。

このメソッドは DOM を漸進的に描画していくフレームワークにとって有益です。アイコン切り替えのデータ属性が変わる際に、コンポーネントは自身を更新する方法が必要になります。このメソッドがファンデーション上で公開され、単純に素のコンポーネントによってプロキシされる理由のはそのためです。

### `MDCIconToggle` API

通常の DOM 要素と同様に `MDCIconToggle` の機能はアクセサメソッドを通じて公開されています。

#### `MDCIconToggle.on`

真偽値。現在、アイコン切り替えがオンになっているかどうかを返します。このプロパティを設定すると切り替えの状態が更新されます。

#### `MDCIconToggle.disabled`

真偽値。現在、アイコン切り替えが無効になっているかどうかを返します。このプロパティを設定すると無効かどうかの状態が更新されます。

### ファンデーションクラスの使用

最小限の労力で独自の MDCIconToggle コンポーネントを構築できるように外部のフレームワークやライブラリが利用できる `MDCIconToggleFoundation` クラスが MDCIconToggle には付属しています。すべてのファンデーションクラスと同様に、アダプターオブジェクトを提供しなくてはなりません。アイコン切り替えのアダプターは以下の関数を提供しなくてはなりません。

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素、もしくは内部のアイコン要素にクラスを追加する。
`removeClass(className: string) => void` | ルート要素、もしくは内部のアイコン要素からクラスを削除する。
`registerInteractionHandler(type: string, handler: EventListener) => void` | `click` や `keydown` のようなインタラクションイベントのためのイベントハンドラーを登録する。
`deregisterInteractionHandler(type: string, handler: EventListener) => void` | `click` や `keydown` のようなインタラクションイベントのためのイベントハンドラーの登録を解除する。
`setText(text: string) => void` | ルート要素、もしくは内部のアイコン要素のテキストコンテンツを設定する。
`getTabIndex() => number` | ルート要素のタブインデックスを返す。
`setTabIndex(tabIndex: number) => void` | ルート要素のタブインデックスを設定する。
`getAttr(name: string) => string` | ルート要素の `name` に指定した属性の値を返す。`getAttribute()` と同様に `null` を返すこともできる。
`setAttr(name: string, value: string) => void` | ルート要素の `name` に指定した属性に `value` の値を設定する。
`rmAttr(name: string) => void` | ルート要素の `name` に指定した属性を削除する。
`notifyChange(evtData: {isOn: boolean}) => void` | 変更の通知を受け取り、環境のイベントハンドリンクシステムに `evtData` を伝達する。素の実装ではこのメソッドのためにカスタムイベントが使用される。

#### アダプターの実装者の考慮事項

あなたが独自のアダプターを作成する際に考慮すべきことの一つは `data-icon-inner-selector` の使用についてです。これは <em>コンポーネント</em> のレベルで処理されます。このことは、ファンデーションは完全にこれを関知しないということを意味します。そのため、あなたのフレームワークの Icon Toggle が内部のアイコン要素を持っているなら、`addClass` と `removeClass`、`setText` はアイコン要素に対して作用することを保証しなくはなりません。

<em>リップルはコンポーネントレベルで独自のファンデーションを必要とする</em> ことにも注意が必要です。出発点として `index.js` における私たちの素の実装を確かめてください。

#### 完全なファンデーション API

##### `MDCIconToggleFoundation.refreshToggleData() => void`

前述の通り、`data-toggle-*` 属性は冗長な解析を行わないようにキャッシュされます。あなたのフレームワークが漸進的な描画をしており、かつこれらの属性はコンポーネント自身を再描画せずに変更されているなら、data 属性を再解析してファンデーションを最新の状態に保つためにこのメソッドを呼ぶことができます。

##### `MDCIconToggleFoundation.isOn() => boolean`

ファンデーションの状態がオンになっているときは true を返し、それ以外の場合は false を返します。

##### `MDCIconToggleFoundation.toggle(isOn: boolean = !this.isOn()) => void`

ファンデーションの状態を切り替え、アダプターメソッドを通じてコンポーネントを更新します。引数が与えられていないときは、現在の状態の反対の状態にします。引数が与えられているときは、true ならオンに、false ならオフにします。

##### `MDCIconToggleFoundation.isDisabled() => boolean`

ファンデーションが無効の状態なら `true` を返し、そうでないときは `false` を返します。

##### `MDCIconToggleFoundation.setDisabled(isDisabled: boolean) => void`

ファンデーションの状態を有効または無効にし、アダプターメソッドを通じてコンポーネント更新します。

##### `MDCIconToggleFoundation.isKeyboardActivated() => boolean`

ファンデーションが現状、キーボードイベントを有効にしていれば `true` を返し、そうでなければ `false` を返します。`MDCRippleFoundation.isSurfaceActive()` アダプターメソッドで役立ちます。

### Sass ミキシン

ミキシン | 説明
--- | ---
`mdc-icon-toggle-ink-color($color)` | アイコン切り替えのインク色を設定する。
