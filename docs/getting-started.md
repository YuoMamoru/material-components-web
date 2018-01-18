<!--docs:
title: "Getting Started"
layout: landing
section: docs
path: /docs/getting-started/
-->

# 入門ガイド

このガイドはあなたがサイト構築やプロジェクト内で MDC Web を使い始める手助けになります。

> もしあなたがフレームワークと MDC Web との統合もしくは MDC Web をラップするフレームワークの開発に興味があるなら [フレームワークインストールガイド](./integrating-into-frameworks.md) を参照してください。

## MDC Web クイックスタート: 単純な挨拶アプリの構築

新しい技術を学ぶ最もよい方法はあなた自身の手を動かし、それを使って何かを作ってみることです。つまり、今まさにやろうとしていることです！名前を入力し挨拶を表示する単純な挨拶ページを作っていきます。

このガイドを通して、ガイドに沿ってコードを書いていくことをお勧めします。最後にはあなたは単純なサイトに MDC Web を統合するための基本を身につけるだけでなく、私たちの提供したコンポーネントの一部を使って作業をしていけるようになるでしょう。

### プロジェクトのセットアップ

アプリケーションを提供するプロジェクトのディレクトリを作成してください。

```
mkdir greeting-app
cd greeting-app
```

加えて、[NodeJS](https://nodejs.org) がインストールされているならローカルの開発サーバーとして [Live-server](http://tapiov.net/live-server/) をインストールして利用することをお勧めします。Live-server は簡単に使用でき、HTML を更新したらページがリロードされます。インストールは [npm](https://www.npmjs.com/) を使って次のように行います。

```
npm install --global live-server
```

> 注意: node のインストールの構成によっては npm パッケージをグローバルにインストールするために `sudo` を使う必要があります。

`--global` オプションは npm にパッケージをグローバルにインストールすることを伝えるので、`live-server` のプログラムは `$PATH` 上で利用できます。

### index.html の骨組みの作成

ディレクトリの設定ができたので、単純な `index.html` ファイルを作成し、MDC Web に必要なものを入れていきます。`greeting-app` ディレクトリに以下の内容の `index.html` を作成します。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Greeting App</title>
    <link
      rel="stylesheet"
      href="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.css">
  </head>
  <body class="mdc-typography">
    <h1 class="mdc-typography--display1">Hello, World!</h1>
    <button type="button" class="mdc-button mdc-button--raised">
      Press Me
    </button>
  </body>
</html>
```

`live-server` （もしくはあなたの選んだ Web サーバー）で `greeting-app` ディレクトにあるこのページを見てください。

`live-server` を使っているなら、`index.html` ファイルを示す URL がブラウザで表示されます。このガイドを実行しているあいだ `live-server` は実行したままにしておくことができます。 `live-server` を使っていないなら、サーバーのベース URL に移動しページを確認し、変更するたびに必ず再読み込みをしてください。

この HTML のいくつかの側面を見ていきます。

* **JavaScript が不要 (現時点で)** - 動的コンポーネントを使用していないので、要素に適切な CSS クラスを適用するために MDC Web の CSS を含める必要があります。MDC Web ではページで発生したイベントを検知する必要がある動的コンポーネントの UI だけが JavaScript を必要とします。挨拶アプリを開発するにあたり、必要な JavaScript を追加していきます。
* **自動 DOM レンダリングがない** - すべてのコンポーネントにおいて MDC Web はいかなる DOM オブジェクト自体を描画することはありません。この点において MDC Web は [Bootstrap](http://getbootstrap.com/) に似ています。MDC Web は適切な CSS クラスを使ってあなたが DOM を描画していることを前提にしています。これは MDC Web を複雑なアプリケーションに統合するさいの問題のややこしい話を回避するためです。
* **要素の固有のスタイルに依存しない** - 上記の通り、`<body>` 要素には `mdc-typography` クラスがあり、`<h1>` 要素には `mdc-typography--display1` というクラスがあり、ボタンには `mdc-button` というクラスが複数の <em>装飾クラス</em> とともにあります。MDC Web では <em>決して</em> コンポーネントのどの要素に対して使用されているかは仮定せず、代わりに最大限の柔軟性を持たせるため CSS クラスに依存します。MDC Web の CSS クラス名は [BEM](http://getbem.com/) システムに若干の変更を加えたものにしたがっています。

### 動的コンポーネント用 JavaScript の追加

MDC Web の骨子を確認したので、挨拶アプリの作成を続けていきましょう。

このアプリは2つの入力欄と1つの送信ボタンで構成されています。マテリアルデザインのテキスト入力欄とボタンは多くの JavaScript の使用を必要とする動的要素やアニメーションを含んでいます。

`index.html` 内の `<body>` の内容を以下のものに置き換えましょう。

```html
<main>
  <h1 class="mdc-typography--display1">Tell us about yourself!</h1>

  <form action="#" id="greeting-form">
    <div>
      <div class="mdc-form-field">
        <div class="mdc-text-field" data-mdc-auto-init="MDCTextField">
          <input id="firstname" type="text" class="mdc-text-field__input">
          <label for="firstname" class="mdc-text-field__label">
            First Name
          </label>
          <div class="mdc-text-field__bottom-line"></div>
        </div>
      </div>

      <div class="mdc-form-field">
        <div class="mdc-text-field" data-mdc-auto-init="MDCTextField">
          <input id="lastname" type="text" class="mdc-text-field__input">
          <label for="lastname" class="mdc-text-field__label">
            Last Name
          </label>
          <div class="mdc-text-field__bottom-line"></div>
        </div>
      </div>
    </div>

    <button type="submit"
            class="mdc-button
                   mdc-button--raised
                   mdc-ripple-surface"
            data-mdc-auto-init="MDCRipple">
      Print Greeting
    </button>
  </form>

  <!-- 下の p 要素は挨拶を表示する場所です -->
  <p class="mdc-typography--headline" id="greeting"></p>
</main>

<script src="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.js"></script>
<script>window.mdc.autoInit();</script>
```

変更しブラウザに戻ると、2つの非常に素晴らしいスタイルのフォームフィールドとマテリアルデザインで整えられたボタンを見ることができます。ボタンは押すとインクのリップルのエフェクトがみられます。今のところ、リップルは短い時間だけ処理されるとても巧妙なエフェクトです。

追加されたコードにおいて実際に示された2つの重要点は以下通りです:

#### MDC Web は自動的にインスタンスの生成をしない

これは Material Design Lite (MDC Web の前身) で存在したライフサイクル管理に関連する悩みを回避するためです。初期化は `mdc.autoInit()` が呼ばれたときに初期化する要素に加えられた `data-mdc-auto-init` 属性を通じて行われます。

`mdc.autoInit()` が呼ばれると `data-mdc-auto-init` 属性のあるすべての要素を探してその要素のクラス名をもつ MDC Web JS コンポーネントをアタッチします。そのため、`MDCTextField` を見つけたとき、[MDCTextField](../packages/mdc-textfield) インスタンスが一致した要素にインスタンス化されます（訳注: `data-mdc-auto-init` 属性が `MDCTextField` となっている要素に対して `MDCTextField` クラスがインスタンス化されるということ）。ボタンについても同様で [MDCRipple](../packages/mdc-ripple) インスタンスが要素にアタッチされます。

`mdc.autoInit` が純粋に便利な関数として提供されていることは注目に値し、実際にコンポーネントを使う上では必須ではありません。しかしながらこれは素早く立ち上げて実行するにはもっとも簡単な方法であり、広範囲に `material-components-web` ライブラリを適用する静的サイトには勧められます。

#### すべてのコンポーネントがモジュールとなっている

最初にこのプロジェクトをセットアップしたとき `material-components-web` パッケージをインストールしましたが、このパッケージは [mdc-typography](../packages/mdc-typography)、[mdc-button](../packages/mdc-button)、[mdc-text-field](../packages/mdc-textfield)、 [mdc-ripple](../packages/mdc-ripple) といった個別パッケージをまとめたラッパーにすぎません。`autoInit()` 関数でさえも [固有のパッケージの中に位置し](../packages/mdc-auto-init)、`data-mdc-auto-init` 内で使われている名称のコンポーネントを登録するために `material-components-web` パッケージは `mdc-auto-init` パッケージを使います。各コンポーネントはスタンドアロンパッケージとして利用することができ、また、組み合わせることができます。これにより、カスタムビルドを行えば CSS/JS のコードを必要最小限のサイズにできます。モジュールローディングシステムや最新のフロントエンドツールチェーンとともに使っても MDC Web はきわめてよく機能することを意味してます。

### ビジネスロジックの追加

最後にページの下部に（非常に単純な）ビジネスロジックを追加してみましょう。ページはフォームの送信を受け取って適切な挨拶を表示するために入力欄の値を使用します。`<body>` 内の最後の `<script>` タグに以下の内容を追加してください。

```html
<script>
  document.getElementById('greeting-form').addEventListener('submit', function(evt) {
    evt.preventDefault();
    var firstname = evt.target.elements.firstname.value;
    var lastname = evt.target.elements.lastname.value;
    var greeting = 'Hello';
    if (firstname || lastname) {
      greeting += ', ';
      if (firstname && lastname) {
        greeting += firstname + ' ' + lastname;
      } else if (lastname) {
        greeting += 'Mx. ' + lastname;
      } else {
        greeting += firstname;
      }
    }
    greeting += '!';

    document.getElementById('greeting').textContent = greeting;
  });
</script>
```

ファイルを保存するとページがリロードされ、フォームに名前を入力できるようになり、ボタンを押すと感じのよい挨拶が表示されます :wave:

### テーマの変更

ボタンの背景、ラベルやフォーカスされた入力欄の下線についても注目してください。デフォルトで [マテリアルデザインカラーパレット](https://material.io/guidelines/style/color.html#color-color-palette) の Indigo 500 (`#673AB7`) が設定されています。これは MDC Web がのせているデフォルトテーマの一部です。デフォルトテーマはプライマリカラーとして Indigo 500 を使っており、セカンダリカラーには Pink A200 (`#FF4081`) を使っています。テーマのプライマリカラーを変えてみましょう。

マテリアルデザインを実装する際のよくある誤解として使用する色はマテリアルデザインのカラーパレットから <em>選ばなくてはいけない</em> 、というものがあります。これはまったく正しくありません。マテリアルデザインの色に関する唯一の定められたガイドラインは「落ち着いた環境、濃い影、鮮やかなハイライトと並べられた大胆な色合い」ということだけです。テーマのプライマリカラーを `#0E4EAD` に変えてみましょう。この色は [Deep_Skyblues Colourlovers Palette](http://www.colourlovers.com/palette/334208/Deep_Skyblues) の "Afternoon_Skyblue" の色です。

MDC Web アプリケーションのテーマを変える最も簡単な方法は [CSS 変数](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables) を使うことです。`index.html` の `<head>` タグに以下の内容を単に加えてみてください。

```html
<style>
  :root {
    --mdc-theme-primary: #0e4ead;
  }
</style>
```

CSS 変数をサポートしているブラウザ、IE 11 は置いておいて、を使っているなら、ボタンの背景だけでなく、入力欄のフォーカスされたものの下線やラベルまでいい感じに濃い青になっていることがわかるでしょう。

> 注意: CSS 変数を使う方法は MDC Web の使用しているテーマを設定する方法の一つにすぎません。より多くの情報は [テーマのドキュメント](./theming.md) を参照してください。

### 仕上げ: カスタムスタイルの追加

すべてのサイトは異なっており、ユーザの望むすべてのデザインの選択肢を想定したユーザインターフェースライブラリを構築することを望むことはできません。

#### SASS ミキシン

MDC Web はいくつかのコンポーネントでカスタマイズするための SASS ミキシンを提供しています。これらのミキシンを使ってライズボタンの背景色を明るいオレンジ (#FF9800) に変えてみましょう。

SASS を使っているなら `scss` ファイルに次の内容を追加してください。

```scss
@import "@material/mdc-button/mixins";
.mdc-button.mdc-button--raised {
  @include mdc-button-filled-accessible(#FF9800);
}
```

#### CSS

MDC Web はカスタマイズや好みのスタイルに変えるために普通の古い CSS も使っています。入力欄と送信ボタンの縦方向のスペースを広げるために補助的なスタイルを追加してみましょう。

`<head>` 内の `<style>` タグに以下の内容を追加してください。

```css
#greeting-form > button {
  margin-top: 8px;
}
```

おめでとう！あなたは初めての MDC Web アプリを作り上げました！この過程で MDC Web の基本、ページにコンポーネントを簡単に追加する方法、カスタマイズや好きなように MDC Web のテーマを設定する方法を学びました。

## 次のステップ

MDC Web コンポーネントを Angular や React のようなライブラリに組み込みたいのであれば [フレームワーク統合ガイド](./integrating-into-frameworks.md) を参照してください。

MDC Web プロジェクトに貢献したりあなた自身のコンポーネントを作りたい、もしくは、あなたの目的に合った拡張をしたいのなら、[コンポーネント制作](./authoring-components.md) にあるガイドを参照してください。
