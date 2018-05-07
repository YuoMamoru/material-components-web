<!--docs:
title: "Theming Guide"
layout: landing
section: docs
path: /docs/theming/
-->

# テーマガイド

## 概要

MDC Web はアプリケーションの配色の変更を容易にできるように設計されたテーマシステムを含んでいます。これはテーマを実装するための多くのオプションを提供しており、最大限の柔軟性が得られます。現在、 MDC Web は Sass と CSS カスタムプロパティによってテーマをサポートしています。CDN サービスが利用可能になった時点での CDN サポートも計画しています。

## 配色

MDC Web のテーマはマテリアルデザインのテーマのように **プライマリ(primary)** と **セカンダリ(secondary)** という2つのメインカラーを使います。プライマリカラーはアプリケーションやコンポーネントのいたることろで使用され、アプリケーションのメインカラーとなります。セカンダリカラーはフローティング操作ボタンやそのほかのインタラクティブな要素に使用され、プライマリカラーと視覚的な対比として役立ちます。

プライマリカラーとセカンダリーカラーに加えて MDC Web では <em>バックグランド(background)</em> カラーも定義します。バックグランドカラーはコンポーネントの背景として使用され、通常はページの背景となります。

最後になりますが、MDC Web はテキストカラーをいくつか持っており、プライマリカラー・セカンダリーカラー・バックグランドカラーの上にテキストや図形を描くのに使われます。背景との十分なコントラストを保つためにテキストカラーには暗いか明るいかのいずれかを指定され、[用途に応じた異なるレベルの透明度](https://material.io/go/design-theming#color-color-schemes) を持ちます。用途は以下の通りです。
- 主要部分(Primary)、大部分のテキストに使用されます。
- 副次的部分(Secondary)、視覚階層上の下位にあるテキストに使用されます。
- ヒント(Hint)、ヒントのテキスト（文字入力欄やラベルのヒントなど）に使用されます。
- 利用できない項目(Disabled)、利用不可となっているコンポーネントやコンテンツのテキストに使用されます。
- アイコン(Icon)、アイコンに使用されます。

## テーマを持ったアプリケーションの構築

簡単なアプリケーションから始めてみましょう。異なるカテゴリのいくつかのカードを表示するアプリです。最終的にはカテゴリにあった色を各カードに持たせたいのですが、初めは MDC Web の提供するデフォルトのテーマを持たせてみましょう。

[最終的に完成したものはここで見ることができます](https://plnkr.co/edit/qxt7qpPsXgkt9UbMnE36?p=preview) が、一から始めてみましょう。

> 注意: このガイドでは MDC Web のプロジェクトを開始するための基本事項は扱いません。詳しい情報が必要なら [入門ガイド](./getting-started.md) を見てください。

### ステップ 1: テーマなし

以下のマークアップがあります。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Elements</title>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <link
      rel="stylesheet"
      href="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.css">
    <style>
      .cards {
        display: flex;
        flex-wrap: wrap;
      }

      .element-card {
        width: 16em;
        margin: 16px;
      }

      .element-card > .mdc-card__media {
        height: 9em;
      }

      #demo-absolute-fab {
        position: fixed;
        bottom: 1rem;
        right: 1rem;
        z-index: 1;
      }
    </style>
  </head>
  <body class="mdc-typography">
    <h1>Choose your element</h1>
    <div class="cards">
      <div class="mdc-card element-card earth">
        <section class="mdc-card__media">
          <h1 class="mdc-card__title mdc-card__title--large">Earth</h1>
          <h2 class="mdc-card__subtitle">A solid decision.</h2>
        </section>
        <section class="mdc-card__supporting-text">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </section>
      </div>

      <div class="mdc-card element-card wind">
        <section class="mdc-card__media">
          <h1 class="mdc-card__title mdc-card__title--large">Wind</h1>
          <h2 class="mdc-card__subtitle">Stormy weather ahead.</h2>
        </section>
        <section class="mdc-card__supporting-text">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </section>
      </div>

      <div class="mdc-card element-card fire">
        <section class="mdc-card__media">
          <h1 class="mdc-card__title mdc-card__title--large">Fire</h1>
          <h2 class="mdc-card__subtitle">Hot-headed much?</h2>
        </section>
        <section class="mdc-card__supporting-text">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </section>
      </div>

      <div class="mdc-card element-card water">
        <section class="mdc-card__media">
          <h1 class="mdc-card__title mdc-card__title--large">Water</h1>
          <h2 class="mdc-card__subtitle">Go with the flow.</h2>
        </section>
        <section class="mdc-card__supporting-text">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </section>
      </div>
    </div>
    <button class="mdc-fab material-icons" id="demo-absolute-fab" aria-label="Favorite">
      <span class="mdc-fab__icon">
        favorite
      </span>
    </button>
  </body>
</html>
```

白い背景に黒のテキストのこぎれいなカードがいくつかあります。配色に関する唯一の手がかりは FAB です。FAB はデフォルトではセカンダリカラーを使います。


### ステップ 2: マークアップに MDC Web の配色を使う

すべてが `--primary` オプションを持っているというわけではないです。特にあたながマークアップルするところにおいてはそうです。（訳注: よく意味が分からないが、この次にやるメディア領域の背景色は別に `--primary` でなくても `--secondary` や `--primary-light` やそのほかの色でもよい、という意味だと思う。）

カードのメディア領域の背景色にプライマリカラーを使うことにより、少しばかり面白い見た目にしてみましょう。その方法の一つはカスタム CSS ルールを作ることで、プライマリカラーと同じ色を背景に設定することです。

```css
/* 悪い方法 */
.element-card > .mdc-card__media {
  background-color: #3f51b5;
}
```

しかし、その方法は MDC Web のテーマの有用性を活かさないので扱いにくいものになります。テーマを変えるには CSS ルールをコピーする必要がでてくるのでメンテナンスコストが増大します。

よりメンテナンスしやすい方法でこの問題に取り組むために MDC Web は `mdc-theme` モジュールの一部としていくつかの CSS クラスを提供しています。プライマリカラー、セカンダリカラー、バックグランドカラーとして利用できるクラスをあげます。

| クラス                          | 説明                                                                    |
| ------------------------------- | ----------------------------------------------------------------------- |
| `mdc-theme--primary`            | テキスト色としてテーマのプライマリカラーを設定する。                    |
| `mdc-theme--primary-light`      | テキスト色としてテーマのプライマリカラーを設定する（明るいバリエーション）。 |
| `mdc-theme--primary-dark`       | テキスト色としてテーマのプライマリカラーを設定する（暗いバリエーション）。 |
| `mdc-theme--secondary`          | テキスト色としてテーマのセカンダリカラーを設定する。                    |
| `mdc-theme--secondary-light`    | テキスト色としてテーマのセカンダリカラーを設定する（明るいバリエーション）。 |
| `mdc-theme--secondary-dark`     | テキスト色としてテーマのセカンダリカラーを設定する（暗いバリエーション）。 |
| `mdc-theme--background`         | 背景色としてテーマのバックグランドカラーを設定する。                    |
| `mdc-theme--primary-bg`         | 背景色としてテーマのプライマリカラーを設定する。                        |
| `mdc-theme--primary-light-bg`   | 背景色としてテーマのプライマリカラーを設定する（明るいバリエーション）。 |
| `mdc-theme--primary-dark-bg`    | 背景色としてテーマのプライマリカラーを設定する（暗いバリエーション）。  |
| `mdc-theme--secondary-bg`       | 背景色としてテーマのセカンダリカラーを設定する。                        |
| `mdc-theme--secondary-light-bg` | 背景色としてテーマのセカンダリカラーを設定する（明るいバリエーション）。 |
| `mdc-theme--secondary-dark-bg`  | 背景色としてテーマのセカンダリカラーを設定する（暗いバリエーション）。  |

この表からカードのメディア領域に `mdc-theme--primary-bg` を使うとよいことがわかります。

```html
<div class="mdc-card element-card">
  <section class="mdc-card__media mdc-theme--primary-bg">
    <h1 class="mdc-card__title mdc-card__title--large">Earth</h1>
    <h2 class="mdc-card__subtitle">A solid decision.</h2>
  </section>
  <section class="mdc-card__supporting-text">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
  </section>
</div>
```

今すぐ、すべてのカードにメディア領域の背景色としてデフォルトのプライマリカラー（マテリアルパレットの Indogo 500）を使ってみましょう。

しかし、メディア領域のテキストはまだ黒で、デフォルトのプライマリカラーとはほとんどコントラストがありません。すべてのプライマリカラーが暗い色というわけではないので、テキスト色を白に変えて終わりというわけにはいきません。理想的には `mdc-theme--primary-bg` クラスのようにメンテナンスしやすいく、白いテキストか黒いテキストかを決めるためにプライマリーカラーを考慮している解決策がほしいのです。

`mdc-theme` はこれをも意図した汎用クラスを提供しています。つまり、プライマリカラーの背景色にテキストをのせるためのもので、以下の通りになっています。

| クラス                                       | 説明                                                                                                      |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `mdc-theme--text-primary-on-primary`         | テーマのプライマリカラーの背景色の上にのせる主要なテキストに適切な色を設定します。                        |
| `mdc-theme--text-primary-on-primary-light`   | テーマのプライマリカラーの背景色の上にのせる主要なテキストに適切な色を設定します（明るいバリエーション）。 |
| `mdc-theme--text-primary-on-primary-dark`    | テーマのプライマリカラーの背景色の上にのせる主要なテキストに適切な色を設定します（暗いバリエーション）。  |
| `mdc-theme--text-secondary-on-primary`       | テーマのプライマリカラーの背景色の上にのせる副次的なテキストに適切な色を設定します。                      |
| `mdc-theme--text-secondary-on-primary-light` | テーマのプライマリカラーの背景色の上にのせる副次的なテキストに適切な色を設定します（明るいバリエーション）。 |
| `mdc-theme--text-secondary-on-primary-dark`  | テーマのプライマリカラーの背景色の上にのせる副次的なテキストに適切な色を設定します（暗いバリエーション）。 |
| `mdc-theme--text-hint-on-primary`            | テーマのプライマリカラーの背景色の上にのせるヒントのテキストに適切な色を設定します。                      |
| `mdc-theme--text-hint-on-primary-light`      | テーマのプライマリカラーの背景色の上にのせるヒントのテキストに適切な色を設定します（明るいバリエーション）。 |
| `mdc-theme--text-hint-on-primary-dark`       | テーマのプライマリカラーの背景色の上にのせるヒントのテキストに適切な色を設定します（暗いバリエーション）。 |
| `mdc-theme--text-disabled-on-primary`        | テーマのプライマリカラーの背景色の上にのせる利用できない項目のテキストに適切な色を設定します。            |
| `mdc-theme--text-disabled-on-primary-light`  | テーマのプライマリカラーの背景色の上にのせる利用できない項目のテキストに適切な色を設定します（明るいバリエーション）。 |
| `mdc-theme--text-disabled-on-primary-dark`   | テーマのプライマリカラーの背景色の上にのせる利用できない項目のテキストに適切な色を設定します（暗いバリエーション）。 |
| `mdc-theme--text-icon-on-primary`            | テーマのプライマリカラーの背景色の上にのせるアイコンに適切な色を設定します。                              |
| `mdc-theme--text-icon-on-primary-light`      | テーマのプライマリカラーの背景色の上にのせるアイコンに適切な色を設定します（明るいバリエーション）。      |
| `mdc-theme--text-icon-on-primary-dark`       | テーマのプライマリカラーの背景色の上にのせるアイコンに適切な色を設定します（暗いバリエーション）。        |

> 注意:  `primary`、`secondary`、`hint`、`disabled`、`icon` はテキストの機能を意味しています。 _primary color_ と _primary function text_ とでは異なる意味でで _primary_ という単語を使っており、初めのうちは混乱することがあるでしょう。（訳注: この訳では _primary_ という語を _primary color_ という文脈では「プライマリ」、  _primary function text_ という文脈では「主要な」と訳しています。 _secondary_ も同様に「セカンダリ」「副次的」としています。）

この表から正しい選択が `mdc-theme--text-primary-on-primary` であるとわかります。メディア領域にそれを適用すればよいと思うかもしれませんが、スコープの問題でそれはうまくいきません。直接タイトルやサブタイトルに適用するなら次のようになるでしょう。

```html
<div class="mdc-card element-card">
  <section class="mdc-card__media mdc-theme--primary-bg">
    <h1 class="mdc-card__title mdc-card__title--large mdc-theme--text-primary-on-primary">Earth</h1>
    <h2 class="mdc-card__subtitle mdc-theme--text-primary-on-primary">A solid decision.</h2>
  </section>
  <section class="mdc-card__supporting-text">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
  </section>
</div>
```

テキストが白になり、コントラストがより向上しましした。プライマリカラーを明るい色にしたければ、コントラストを向上させるためにテキストは再び暗くなります。それではどうやってプライマリカラーを変更したらよいのでしょうか？


### ステップ 3: Sass を使いテーマを変える

あなたのすべてのアプリケーションでデフォルトで使用されている統一的なテーマカラーは Sass で設定できます。MDC Web のどのモジュールを読み込むより前に Sass ファイル内に3つの変数（`$mdc-theme-primary`、`$mdc-theme-secondary`、`$mdc-theme-background`）を定義することにより、簡単に設定できます。

```scss
// メインとなる Sass ファイル
$mdc-theme-primary: #9c27b0;
$mdc-theme-secondary: #76ff03;
$mdc-theme-background: #fff;

@import "material-components-web/material-components-web";
```

これらの定義は `mdc-theme` モジュール内の初期値を上書きし、テーマを利用するすべてのコンポーネントはこれに依存します。テキストの色については `mdc-theme` 内で Sass 定義の一部として与えられたプライマリ/セカンダリ/バックグランドの各色から自動的に計算されます。とっても簡単でしょ！

> 注意: テーマカラーはマテリアルパレットから選はなくてはいけないということはありません。任意の有効な色を使えます。マテリアルデザイン仕様の [色の節](https://material.io/go/design-theming) を読むと良いでしょう。他のパレットを使ってもよいのです。


### ステップ 4: CSS カスタムプロパティを使いテーマを変更する

Sass を使ったテーマカラーの変更はアプリケーション全体に影響し、画面全体に一貫性を求めている場合に優れた方法です。しかし、私たちがここで求めているものは少々違っており、各カードはカード内で一貫したテーマを持つようにしたいのです。

それでは異なる場所には異なるテーマを使う場合、現在のテーマカラーの「配管」のすべてをメンテナンスしやすく保つにはどうしたらよいでしょうか？CSS カスタムプロパティが救ってくれます！

MDC Web が生成した CSS はハードコードされた CSS カスタムプロパティを使っています。そこには Sass で提供した配色が設定されています。あなたの設定した Sass のデフォルトテーマを（先ほどやったのと同じように）あなた自身が定義できますが、状況やユーザの好みの合わせて CSS を上書きすることもできるということです。

MDC Web がどのようにやっているのか見てみましょう。コンパイルされた MDC Web の CSS ルールの一部がこれです。

```css
.mdc-fab {
  background-color: #ff4081;
  background-color: var(--mdc-theme-secondary, #ff4081);
}
```

ここで、CSS カスタムプロパティをサポートしていないブラウザのために MDC Web が色を2重に設定しているのがわかります。宣言は `var()` により上書きされ、デフォルト値として同じ予備の設定（カスタムプロパティの定義が見つからない場合に備えて）が使われています。

したがって、単にカスタムプロパティを再定義することにより MDC Web コンポーネント内で利用する色を簡単に上書きできます。カードに適用したいときは設定した要素クラスを利用できます。

```css
.element-card.earth {
  --mdc-theme-primary: #795548;
}

.element-card.wind {
  --mdc-theme-primary: #9e9e9e;
}

.element-card.fire {
  --mdc-theme-primary: #f44336;
}

.element-card.water {
  --mdc-theme-primary: #00bcd4;
}
```

うまくいったでしょ！背景に色が適用されたのがわかります。カードが他のコンポーネントを持っていたとしても同じように適切な色が使われるはずです。

MDC Web が使っているカスタムプロパティは Sass 変数や CSS クラスと同じ命名規則にしたがっています。

| カスタムプロパティ            | 説明                                        |
| ----------------------------- | ------------------------------------------- |
| `--mdc-theme-primary`         | テーマのプライマリカラー。                  |
| `--mdc-theme-primary-light`   | テーマのプライマリカラー（明るいバリエーション）。 |
| `--mdc-theme-primary-dark`    | テーマのプライマリカラー（暗いバリエーション）。 |
| `--mdc-theme-secondary`       | テーマのセカンダリカラー。                  |
| `--mdc-theme-secondary-light` | テーマのセカンダリカラー（明るいバリエーション）。 |
| `--mdc-theme-secondary-dark`  | テーマのセカンダリカラー（暗いバリエーション）。 |
| `--mdc-theme-background`      | テーマのバックグランドカラー。              |

しかし、ページを詳しく見るとまだ完全には完成していないのがわかります。テキストの色が適切ではありません。Wind と Water のカードは暗いテキストにするべきですが、まだ白いままです。なぜそうなっているのでしょう？

問題点は `--mdc-theme-primary` カスタムプロパティだけを設定していることです。Sass での `$mdc-theme-primary` の設定は関連するテキストの色を計算を可能にしいるのですが、現時点では CSS で複雑なコントラストの計算を行うことはできません。これは関連するテキストの色も設定しなくてはいけないということです。

| カスタムプロパティ                            | 説明                                                                       |
| --------------------------------------------- | -------------------------------------------------------------------------- |
| `--mdc-theme-text-primary-on-primary`         | テーマのプライマリカラーの背景上にある主要なテキスト。                     |
| `--mdc-theme-text-primary-on-primary-light`   | テーマのプライマリカラーの背景上にある主要なテキスト（明るいバリエーション）。 |
| `--mdc-theme-text-primary-on-primary-dark`    | テーマのプライマリカラーの背景上にある主要なテキスト（暗いバリエーション）。  |
| `--mdc-theme-text-secondary-on-primary`       | テーマのプライマリカラーの背景上にある副次的なテキスト。                   |
| `--mdc-theme-text-secondary-on-primary-light` | テーマのプライマリカラーの背景上にある副次的なテキスト（明るいバリエーション）。 |
| `--mdc-theme-text-secondary-on-primary-dark`  | テーマのプライマリカラーの背景上にある副次的なテキスト（暗いバリエーション）。 |
| `--mdc-theme-text-hint-on-primary`            | テーマのプライマリカラーの背景上にあるヒントのテキスト。                   |
| `--mdc-theme-text-hint-on-primary-light`      | テーマのプライマリカラーの背景上にあるヒントのテキスト（明るいバリエーション）。 |
| `--mdc-theme-text-hint-on-primary-dark`       | テーマのプライマリカラーの背景上にあるヒントのテキスト（暗いバリエーション）。 |
| `--mdc-theme-text-disabled-on-primary`        | テーマのプライマリカラーの背景上にある利用できない項目のテキスト。         |
| `--mdc-theme-text-disabled-on-primary-light`  | テーマのプライマリカラーの背景上にある利用できない項目のテキスト（明るいバリエーション）。 |
| `--mdc-theme-text-disabled-on-primary-dark`   | テーマのプライマリカラーの背景上にある利用できない項目のテキスト（暗いバリエーション）。 |
| `--mdc-theme-text-icon-on-primary`            | テーマのプライマリカラーの背景上にあるアイコン。                           |
| `--mdc-theme-text-icon-on-primary-light`      | テーマのプライマリカラーの背景上にあるアイコン（明るいバリエーション）。   |
| `--mdc-theme-text-icon-on-primary-dark`       | テーマのプライマリカラーの背景上にあるアイコン（暗いバリエーション）。     |

<em>セカンダリ</em> や <em>バックグランド</em> 上のテキストの色についても同様のものがあります。

| カスタムプロパティ                              | 説明                                                                         |
| ------------------------------------------------| ---------------------------------------------------------------------------- |
| `--mdc-theme-text-primary-on-secondary`         | テーマのセカンダリカラーの背景上にある主要なテキスト。                       |
| `--mdc-theme-text-primary-on-secondary-light`   | テーマのセカンダリカラーの背景上にある主要なテキスト（明るいバリエーション）。 |
| `--mdc-theme-text-primary-on-secondary-dark`    | テーマのセカンダリカラーの背景上にある主要なテキスト（暗いバリエーション）。 |
| `--mdc-theme-text-secondary-on-secondary`       | テーマのセカンダリカラーの背景上にある副次的なテキスト。                     |
| `--mdc-theme-text-secondary-on-secondary-light` | テーマのセカンダリカラーの背景上にある副次的なテキスト（明るいバリエーション）。 |
| `--mdc-theme-text-secondary-on-secondary-dark`  | テーマのセカンダリカラーの背景上にある副次的なテキスト（暗いバリエーション）。 |
| `--mdc-theme-text-hint-on-secondary`            | テーマのセカンダリカラーの背景上にあるヒントのテキスト。                     |
| `--mdc-theme-text-hint-on-secondary-light`      | テーマのセカンダリカラーの背景上にあるヒントのテキスト（明るいバリエーション）。 |
| `--mdc-theme-text-hint-on-secondary-dark`       | テーマのセカンダリカラーの背景上にあるヒントのテキスト（暗いバリエーション）。 |
| `--mdc-theme-text-disabled-on-secondary`        | テーマのセカンダリカラーの背景上にある利用できない項目のテキスト。           |
| `--mdc-theme-text-disabled-on-secondary-light`  | テーマのセカンダリカラーの背景上にある利用できない項目のテキスト（明るいバリエーション）。 |
| `--mdc-theme-text-disabled-on-secondary-dark`   | テーマのセカンダリカラーの背景上にある利用できない項目のテキスト（暗いバリエーション）。 |
| `--mdc-theme-text-icon-on-secondary`            | テーマのセカンダリカラーの背景上にあるアイコン。                             |
| `--mdc-theme-text-icon-on-secondary-light`      | テーマのセカンダリカラーの背景上にあるアイコン（明るいバリエーション）。     |
| `--mdc-theme-text-icon-on-secondary-dark`       | テーマのセカンダリカラーの背景上にあるアイコン（暗いバリエーション）。       |

| カスタムプロパティ                         | 説明                                                       |
| ------------------------------------------ | ---------------------------------------------------------- |
| `--mdc-theme-text-primary-on-background`   | テーマのバックグランドカラーの背景上にある主要なテキスト。 |
| `--mdc-theme-text-secondary-on-background` | テーマのバックグランドカラーの背景上にある副次的なテキスト。 |
| `--mdc-theme-text-hint-on-background`      | テーマのバックグランドカラーの背景上にあるヒントのテキスト。 |
| `--mdc-theme-text-disabled-on-background`  | テーマのバックグランドカラーの背景上にある利用できない項目のテキスト。 |
| `--mdc-theme-text-icon-on-background`      | テーマのバックグランドカラーの背景上にあるアイコン。       |

加えて、既知の暗い背景、明るい背景のためのカスタムプロパティも定義しています。


| カスタムプロパティ                         | 説明                                                       |
| ------------------------------------------ | ---------------------------------------------------------- |
| `--mdc-theme-text-primary-on-light`        | 明るい色の背景上にある主要なテキスト。                     |
| `--mdc-theme-text-secondary-on-light`      | 明るい色の背景上にある副次的なテキスト。                   |
| `--mdc-theme-text-hint-on-light`           | 明るい色の背景上にあるヒントのテキスト。                   |
| `--mdc-theme-text-disabled-on-light`       | 明るい色の背景上にある利用できない項目のテキスト。         |
| `--mdc-theme-text-icon-on-light`           | 明るい色の背景上にあるアイコン。                           |

| カスタムプロパティ                         | 説明                                                       |
| ------------------------------------------ | ---------------------------------------------------------- |
| `--mdc-theme-text-primary-on-dark`         | 暗い色の背景上にある主要なテキスト。                       |
| `--mdc-theme-text-secondary-on-dark`       | 暗い色の背景上にある副次的なテキスト。                     |
| `--mdc-theme-text-hint-on-dark`            | 暗い色の背景上にあるヒントのテキスト。                     |
| `--mdc-theme-text-disabled-on-dark`        | 暗い色の背景上にある利用できない項目のテキスト。           |
| `--mdc-theme-text-icon-on-dark`            | 暗い色の背景上にあるアイコン。                             |


MDC Web コンポーネントのどれが使われるかわからないので、理想的にはプライマリ上のテキストの色のすべてを設定しておくべきです。しかし、今回のカードにはテキストのみが含まれ、コンポーネントは含んでいないので簡潔にしておきましょう。

```css
.element-card.earth {
  --mdc-theme-primary: #795548;
  --mdc-theme-text-primary-on-primary: var(--mdc-theme-text-primary-on-dark);
}

.element-card.wind {
  --mdc-theme-primary: #9e9e9e;
  --mdc-theme-text-primary-on-primary: var(--mdc-theme-text-primary-on-light);
}

.element-card.fire {
  --mdc-theme-primary: #f44336;
  --mdc-theme-text-primary-on-primary: var(--mdc-theme-text-primary-on-dark);
}

.element-card.water {
  --mdc-theme-primary: #00bcd4;
  --mdc-theme-text-primary-on-primary: var(--mdc-theme-text-primary-on-light);
}
```

> 注意: 将来的にはすべての生成した色を変更し、今回のユースケースを簡潔にするための JavaScript の汎用メソッドの提供を計画しています。

## カスタムテーマ

大部分の MDC Web コンポーネントは、塗りの色、インクの色、線の太さ等のような見た目を変更するための Sass ミキシンを提供しています。これらのミキシンは各コンポーネントの README ファイル（例えば [Button readme](../packages/mdc-button/README.md#advanced-sass-mixins)）に記載があります。

例えば、ボタンの塗りの色を変更し、見やすいインクの色を自動的に選ぶには、カスタム CSS クラス内で単純に `mdc-button-filled-accessible` ミキシンを呼べばよいのです。

```scss
.accessible-button {
  @include mdc-button-filled-accessible(blue);
}
```

そして、ボタン要素にカスタムクラスを適用します。

```html
<button class="mdc-button accessible-button">
  <i class="material-icons mdc-button__icon" aria-hidden="true">favorite</i>
  Button
</button>
```
