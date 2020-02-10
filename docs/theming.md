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

プライマリカラーとセカンダリーカラーに加えて MDC Web では <em>サーフェイス(surface)</em> カラーも定義します。

最後になりますが、MDC Web はテキストカラーをいくつか持っており、プライマリカラー・セカンダリーカラー・バックグランドカラーの上にテキストや図形を描くのに使われます。背景との十分なコントラストを保つためにテキストカラーには暗いか明るいかのいずれかを指定され、[用途に応じた異なるレベルの透明度](https://material.io/go/design-theming#color-color-schemes) を持ちます。用途は以下の通りです。
- 主要部分(Primary)、大部分のテキストに使用されます。
- 副次的部分(Secondary)、視覚階層上の下位にあるテキストに使用されます。
- ヒント(Hint)、ヒントのテキスト（文字入力欄やラベルのヒントなど）に使用されます。
- 利用できない項目(Disabled)、利用不可となっているコンポーネントやコンテンツのテキストに使用されます。
- アイコン(Icon)、アイコンに使用されます。
- サーフェイス上(On-surface)、サーフェイスカラーの背景上のテキストに使用されます。
- セカンダリ上(On-secondary)、セカンダリカラーの背景上のテキストに使用されます。
- プライマリ上(On-primary)、プライマリカラーの背景上のテキストに使用されます。

## テーマを持ったアプリケーションの構築

簡単なアプリケーションから始めてみましょう。異なるカテゴリのいくつかのカードを表示するアプリです。最終的にはカテゴリにあった色を各カードに持たせたいのですが、初めは MDC Web の提供するデフォルトのテーマを持たせてみましょう。

[最終的に完成したものはここで見ることができます](https://plnkr.co/edit/jeBSvWC8mAIhUmUQvHSA?p=preview) が、一から始めてみましょう。

> 注意: このガイドでは MDC Web のプロジェクトを開始するための基本事項は扱いません。詳しい情報が必要なら [入門ガイド](./getting-started.md) を見てください。

### ステップ 1: テーマなし

以下のマークアップがあります。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>Elements</title>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
    <link rel="stylesheet" href="material-components-web.min.css" />
    <style>
      .cards {
        display: flex;
        flex-wrap: wrap;
      }

      .element-card {
        width: 20em;
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
        <div class="mdc-card__media">
          <div class="mdc-card__media-content">
            <h1 class="mdc-typography--headline4">Earth</h1>
            <h2 class="mdc-typography--headline6">A solid decision.</h2>
          </div>
        </div>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </p>
      </div>
      <div class="mdc-card element-card wind">
        <div class="mdc-card__media">
          <h1 class="mdc-typography--headline4">Wind</h1>
          <h2 class="mdc-typography--headline6">Stormy weather ahead.</h2>
        </div>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </p>
      </div>
      <div class="mdc-card element-card fire">
        <div class="mdc-card__media">
          <h1 class="mdc-typography--headline4">Fire</h1>
          <h2 class="mdc-typography--headline6">Hot-headed much?</h2>
        </div>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </p>
      </div>
      <div class="mdc-card element-card water">
        <div class="mdc-card__media">
          <h1 class="mdc-typography--headline4">Water</h1>
          <h2 class="mdc-typography--headline6">Go with the flow.</h2>
        </div>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </p>
      </div>
    </div>
    <button class="mdc-fab" id="demo-absolute-fab" aria-label="Favorite">
      <div class="mdc-fab__ripple"></div>
      <span class="mdc-fab__icon material-icons">favorite</span>
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

| Class                           | Description                                                                  |
| ------------------------------- | -----------------------------------------------------------------------      |
| `mdc-theme--primary`            | テキスト色としてテーマのプライマリカラーを設定する。                         |
| `mdc-theme--primary-bg`         | 背景色としてテーマのプライマリカラーを設定する。                             |
| `mdc-theme--on-primary`         | プライマリカラー上のテキスト色として設定された色を設定する。                 |
| `mdc-theme--secondary`          | テキスト色としてテーマのセカンダリカラーを設定する。                         |
| `mdc-theme--secondary-bg`       | 背景色としてテーマのセカンダリカラーを設定する。                             |
| `mdc-theme--on-secondary`       | セカンダリカラー上のテキスト色として設定された色を設定する。                 |
| `mdc-theme--surface`            | 背景色としてサーフェイス背景色を設定する。                                   |
| `mdc-theme--on-surface`       | サーフェイスカラー上のテキスト色として設定された色を設定する。                 |
| `mdc-theme--background`         | 背景色としてテーマのバックグランドカラーを設定する。                         |

From here, we can see that we want to apply `mdc-theme--primary-bg` to the cards' media areas:

```html
<div class="mdc-card element-card earth">
  <div class="mdc-card__media mdc-theme--primary-bg">
    <div class="mdc-card__media-content">
      <h1 class="mdc-typography--headline4">Earth</h1>
      <h2 class="mdc-typography--headline6">A solid decision.</h2>
    </div>
  </div>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
  </p>
</div>
```

今すぐ、すべてのカードにメディア領域の背景色としてデフォルトのプライマリカラー（マテリアルパレットの Indogo 500）を使ってみましょう。

しかし、メディア領域のテキストはまだ黒で、デフォルトのプライマリカラーとはほとんどコントラストがありません。すべてのプライマリカラーが暗い色というわけではないので、テキスト色を白に変えて終わりというわけにはいきません。理想的には `mdc-theme--primary-bg` クラスのようにメンテナンスしやすいく、白いテキストか黒いテキストかを決めるためにプライマリーカラーを考慮している解決策がほしいのです。

`mdc-theme` はこれをも意図したユーティリティクラスを提供しています。つまり、プライマリカラーの背景色にテキストをのせるためのもので、以下の通りになっています。

| クラス                       | 説明                                                                                |
| -----------------------------| ------------------------------------------------------------------------------------|
| `mdc-theme--on-primary`      | テーマのプライマリカラーの背景上のテキストに適切な色を設定する。                    |
| `mdc-theme--on-secondary`    | テーマのセカンダリカラーの背景上のテキストに適切な色を設定する。                    |
| `mdc-theme--on-surface`      | テーマのサーフェイスカラーの背景上のテキストに適切な色を設定する。                  |

この表から正しい選択が `mdc-theme--on-primary` であるとわかります。メディア領域にこのクラスを適用してみましょう。

```html
      <div class="mdc-card element-card earth">
        <div class="mdc-card__media mdc-theme--primary-bg mdc-theme--on-primary">
          <div class="mdc-card__media-content">
            <h1 class="mdc-typography--headline4">Earth</h1>
            <h2 class="mdc-typography--headline6">A solid decision.</h2>
          </div>
        </div>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </p>
      </div>
```

テキストが白になり、コントラストがより向上しましした。プライマリカラーを明るい色にしたければ、コントラストを向上させるためにテキストは再び暗くなります。それではどうやってプライマリカラーを変更したらよいのでしょうか？


### ステップ 3: Sass を使いテーマを変える

あなたのすべてのアプリケーションでデフォルトで使用されている統一的なテーマカラーは Sass で設定できます。MDC Web のどのモジュールを読み込むより前に Sass ファイル内に3つの変数（`$primary`、`$secondary`、`$background`）を定義することにより、簡単に設定できます。

```scss
@use "@material/theme" with (
  $primary: #9c27b0,
  $secondary: #76ff03,
  $background: #fff,
);
@use "material-components-web";
```

これらの定義は `mdc-theme` モジュール内の初期値を上書きし、テーマを利用するすべてのコンポーネントはこれに依存します。テキストの色については `mdc-theme` 内で Sass 定義の一部として与えられたプライマリ/セカンダリ/バックグランドの各色から自動的に計算されます。とっても簡単でしょ！

> 注意: テーマカラーはマテリアルパレットから選はなくてはいけないということはありません。任意の有効な色を使えます。マテリアルデザイン仕様の [色の節](https://material.io/go/design-theming) を読むと良いでしょう。他のパレットを使ってもよいのです。

If you want to go a step further with your theming then you can override any SASS variable throughout the codebase by
redefining it in your application's SASS file. Exercise caution when doing this, however, as modifying internal variables
may have unintended consequences.


### ステップ 4: CSS カスタムプロパティを使いテーマを変更する

Sass を使ったテーマカラーの変更はアプリケーション全体に影響し、画面全体に一貫性を求めている場合に優れた方法です。しかし、私たちがここで求めているものは少々違っており、各カードはカード内で一貫したテーマを持つようにしたいのです。

それでは異なる場所には異なるテーマを使う場合、現在のテーマカラーの「配管」のすべてをメンテナンスしやすく保つにはどうしたらよいでしょうか？CSS カスタムプロパティが救ってくれます！

MDC Web が生成した CSS はハードコードされた CSS カスタムプロパティを使っています。そこには Sass で提供した配色が設定されています。あなたの設定した Sass のデフォルトテーマを（先ほどやったのと同じように）あなた自身が定義できますが、状況やユーザーの好みの合わせて CSS を上書きすることもできるということです。

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
| `--mdc-theme-secondary`       | テーマのセカンダリカラー。                  |
| `--mdc-theme-surface`         | テーマのサーフェイスカラー。                |
| `--mdc-theme-background`      | テーマのバックグランドカラー。              |

しかし、ページを詳しく見るとまだ完全には完成していないのがわかります。テキストの色が適切ではありません。Wind と Water のカードは暗いテキストにするべきですが、まだ白いままです。なぜそうなっているのでしょう？

問題点は `--mdc-theme-primary` カスタムプロパティだけを設定していることです。Sass での `$mdc-theme-primary` の設定は関連するテキストの色を計算を可能にしいるのですが、現時点では CSS で複雑なコントラストの計算を行うことはできません。これは関連するテキストの色も設定しなくてはいけないということです。

| カスタムプロパティ                            | 説明                                                                       |
| --------------------------------------------- | -------------------------------------------------------------------------- |
| `--mdc-theme-on-primary`                      | プライマリカラーの上の主要なテキスト。                                     |
| `--mdc-theme-on-secondary`                    | プライマリカラーの上の副次的なテキスト。                                   |
| `--mdc-theme-on-surface`                      | プライマリカラーの上のヒントのテキスト。                                   |

<em>バックグラウンド</em> 上の同様のパターンは次のようになります。

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
  --mdc-theme-on-primary: var(--mdc-theme-text-primary-on-dark);
}

.element-card.wind {
  --mdc-theme-primary: #9e9e9e;
  --mdc-theme-on-primary: var(--mdc-theme-text-primary-on-light);
}

.element-card.fire {
  --mdc-theme-primary: #f44336;
  --mdc-theme-on-primary: var(--mdc-theme-text-primary-on-dark);
}

.element-card.water {
  --mdc-theme-primary: #00bcd4;
  --mdc-theme-on-primary: var(--mdc-theme-text-primary-on-light);
}
```

この中のそのほかのコンポーネントがどのように見えるか確認してみましょう。各カードについて `p` タグの直後に以下のコードを追加してください。

```html
<button class="mdc-button mdc-card__actions">
  <i class="material-icons mdc-button__icon">favorite</i>
  Look At My Color
</button>
```
## カスタムテーマ

大部分の MDC Web コンポーネントは、塗りの色、インクの色、線の太さ等のような見た目を変更するための Sass ミキシンを提供しています。これらのミキシンは各コンポーネントの README ファイル（例えば [Button readme](../packages/mdc-button/README.md#advanced-sass-mixins)）に記載があります。

例えば、ボタンの塗りの色を変更し、見やすいインクの色を自動的に選ぶには、カスタム CSS クラス内で単純に `button.filled-accessible` ミキシンを呼べばよいのです。

```scss
@use "@material/button";

.accessible-button {
  @include button.filled-accessible(blue);
}
```

そして、ボタン要素にカスタムクラスを適用します。

```html
<button class="mdc-button accessible-button">
  <div class="mdc-button__ripple"></div>
  <i class="material-icons mdc-button__icon" aria-hidden="true">favorite</i>
  <div class="mdc-button__label">Button</div>
</button>
```
