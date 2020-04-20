<!--docs:
title: "Auto Init"
layout: detail
section: components
excerpt: "Utilities for declarative, DOM-based initialization of components on simple web sites."
path: /catalog/auto-init/
-->

# Auto Init

`mdc-auto-init` は、単純な Web サイト上の MDC Web コンポーネントを初期化するための DOM ベースで宣言的な方法を提供するユーティリティパッケージです。より高度なユースケースや複雑なサイトではコンポーネントを手動で初期化したほうが柔軟に扱えることがあることを知っておいてください。しかし、`mdc-auto-init` は静的な Web サイトやプロトタイプ、簡潔さと利便性が求められるユースケースに適しています。

## インストール

```
npm install @material/auto-init
```

## 使用法

### `material-components-web` の一部としての使用

[material-components-web](../material-components-web) パッケージの一部として mdc-auto-init を使うのであれば、単にコンポーネントが必要な DOM に書くだけです。ルート要素の `data-mdc-auto-init` 属性にコンポーネントの JavaScript クラス名（例: `MDCTextField`）を設定します。そしてマークアップを書いたら、`mdc.autoInit()` を呼び出す script タグを単に追加するだけです。正しく動作させるにはすべてのスクリプトが読み込まれた後に `mdc.autoInit()` を呼びしてください。

```html
<label class="mdc-text-field mdc-text-field--filled" data-mdc-auto-init="MDCTextField">
  <span class="mdc-text-field__ripple"></span>
  <input class="mdc-text-field__input" type="text" aria-labelledby="label">
  <span id="label" class="mdc-floating-label">Input Label</span>
  <span class="mdc-line-ripple"></span>
</label>

<!-- ページの最後に -->
<script type="text/javascript">
  window.mdc.autoInit();
</script>
```

これで `<div>` 要素に [MDCTextField](../mdc-textfield) インスタンスがアタッチされます。

#### コンポーネントのインスタンスへのアクセス

コンポーネントが要素にアタッチされるときに `data-mdc-auto-init` の値と同じ名称を持つ要素のプロパティにインスタンスが設定されます。例えば次コードがあったとします。

```html
<label class="mdc-text-field mdc-text-field--filled" data-mdc-auto-init="MDCTextField">
  <span class="mdc-text-field__ripple"></span>
  <input class="mdc-text-field__input" type="text" aria-labelledby="label">
  <span id="label" class="mdc-floating-label">Input Label</span>
  <span class="mdc-line-ripple"></span>
</label>
```

`mdc.autoInit()` を呼ぶと、要素の `MDCTextField` プロパティを通じてコンポーネントのインスタンスアクセスできます。

```js
document.querySelector('.mdc-text-field').MDCTextField.disabled = true;
```

#### 後続の `mdc.autoInit()` の呼び出し

最初の `mdc.autoInit()` の後に DOM に新しい要素を追加しようとするなら、そのあとに `mdc.autoInit()` を呼び出すことができます。これにより、既に存在するコンポーネントが再び初期化されることはありません。これは mdc-auto-init が `data-mdc-auto-init-state="initialized"` 属性を追加することによるもので、この属性によってこんっぽーねんとが既に初期化されているかどうかをトラッキングしています。`mdc.autoInit()` を呼んだ後にはコンポーネントは次のようになっています。

```html
<label class="mdc-text-field mdc-text-field--filled" data-mdc-auto-init="MDCTextField" data-mdc-auto-init-state="initialized">
  ...
</label>
```

### 単独モジュールとしての使用

#### コンポーネントの登録

`material-components-web` を使わずに `mdc-auto-init` を使うときは `data-mdc-auto-init` 属性値とコンポーネントとの間のマッピングを手動で書かなくてはなりません。これは `mdcAutoInit.register` を通じて行います。

```js
import mdcAutoInit from '@material/auto-init';
import {MDCTextField} from '@material/textfield';

mdcAutoInit.register('MDCTextField', MDCTextField);
```

`mdcAutoInit.register()` は、`"MDCTextField"` が設定されている `data-mdc-auto-init` 属性を持つ要素が見つかったとき、その要素上に `MDCTextField` インスタンスを初期化するよう、  `mdc-auto-init` に伝えます。`material-components-web` パッケージは使いやすくするためにすべてのコンポーネントに対してこの処理を行っています。

また、コンポーネントには任意の文字列をマッピングできます。必ずしもコンストラクターの名称である必要はありません。

```js
import mdcAutoInit from '@material/auto-init';
import {MDCTextField} from '@material/textfield';

mdcAutoInit.register('My amazing text field!!!', MDCTextField);
```

```html
<label class="mdc-text-field mdc-text-field--filled" data-mdc-auto-init="My amazing text field!!!">
  <!-- ... -->
</label>
<script>window.mdc.autoInit();</script>
```

### コンポーネントの登録解除

コンポーネントを登録したときの名前を付けて `mdcAutoInit.deregister` を呼ぶことにより、どのコンポーネントも登録解除できます。

```js
mdcAutoInit.deregister('MDCTextField');
```

これは単に 名前 -> コンポーネント のマッピングを削除するだけです。すでにインスタンス化されているページ上のコンポーネントに影響を与えることは <em>ありません</em>。

すべての 名前 -> コンポーネント のマッピングを削除するには `mdcAutoInit.deregisterAll()` を使います。

## `mdc-auto-init` は何をやっているのか

`mdc-auto-init` は、文字列識別子、言い換えると **名前**、とコンポーネントのコンストラクターを紐づける登録オブジェクトを管理しています。デフォルトのエクスポート関数 - `mdcAutoInit()` - が呼ばれると、`mdc-auto-init` は  `data-mdc-auto-init` 属性を持つすべての要素を DOM に対して問い合わせます。返ってきた各要素に対して以下の手順を実行します。

1. `data-mdc-auto-init` 要素に関連付けられた値がないときはエラーを投げる。
2. `data-mdc-auto-init` の値が登録されていないときはエラーを投げる。
3. `data-mdc-auto-init` の値と同じ名前のプロパティを要素が持っているときは、すでに初期化されているものとして扱う。つまり初期化をとばし、警告をコンソールに書き出す（この動作はオーバライド可能）。
4. `Ctor` に、与えられた名称に関連付けられたコンポーネントのコンストラクターを代入する。
5. `Ctor.attachTo()` に引数として対象要素を渡し、呼んだ結果を `instance` に代入する。
6. 名前が `data-mdc-auto-init` の値で、値が `instance`であり、書き込み禁止、列挙不可のプロパティをノードに生成する。

### ページの一部に限った初期化

デフォルトで `mdc-auto-init` はどのコンポーネントを初期化するのかを決めるためにページ全体を確認します。この動作をオーバライドするために、インスタンス化が必要は子要素を持つルートノードをオプションの第一引数 `root` に渡すことができます。

```html
<div id="mdc-section">
  <!-- MDC Web コンポーネントなど -->
</div>
<script>window.mdc.autoInit(document.getElementById('mdc-section'));</script>
```

上の例では、`<div id="mdc-section">` 内の要素に対してのみ初期化の対象になります。

### autoInit() の複数回の呼び出し

デフォルトでは `mdc-auto-init` はページのロード時の一度だけ呼び出されることを想定しています。しかし、`mdc-auto-init` を使って、無限ににスクロールできる MDC Web コンポーネントを含んだブログ投稿要素のリストを持つ Wordpress サイトのような場合、複数回 `mdcAutoInit()` を呼ぶことが必要になる場面もあるでしょう。コンポーネントが複数回初期化された際に利用するオプションの第二引数を `mdcAutoInit()` は持っています。デフォルトでこの引数は `console.warn()` をするだけです。すでに初期化されているコンポーネントで警告を出さないように処理をスキップさせるには、単に何もしない処理を渡すだけです。

```html
<script>window.mdc.autoInit(/* root */ document, () => {});</script>
```

これですでに初期化されている要素で警告が抑制されます。

### イベント

#### MDCAutoInit:End
すべてのコンポーネントの初期化が完了したときに発生します。

`document.addEventListener("MDCAutoInit:End", () => {...});`
