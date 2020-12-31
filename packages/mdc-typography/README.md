<!--docs:
title: "Typography"
layout: detail
section: components
excerpt: "Typographic scale that handles a set of type sizes"
iconId: typography
path: /catalog/typography/
-->

# Typography

マテリアルデザインのテキストサイズとスタイルは一般的な利用状況下でのコンテンツの密度と読みやすさのバランスをとるために作られました。

MDC Typography は MDC Web コンポーネントにこれらのスタイルを適用する基盤となるモジュールです。このモジュールの書式は以下の13個のスタイルから派生しています。

* Headline 1
* Headline 2
* Headline 3
* Headline 4
* Headline 5
* Headline 6
* Subtitle 1
* Subtitle 2
* Body 1
* Body 2
* Caption
* Button
* Overline

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-typography">マテリアルデザインガイドライン: タイポグラフィ</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/typography">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/typography
```

## 基本的な使用法

### HTML 構造

Google フォントにある Roboto を使うことを推奨します。

```html
<head>
  <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500" rel="stylesheet">
</head>
<body class="mdc-typography">
  <h1 class="mdc-typography--headline1">Big header</h1>
</body>
```

### スタイル

```css
@use "@material/typography/mdc-typography";
```

## スタイルのカスタマイズ

### <a name="typography-styles"></a>タイポグラフィスタイル

型システム内で使用されるタイポグラフィスタイル（以下、`<STYLE>` と呼びます）

スケール | 説明
--- | ---
`headline1` | 画面上で最大のテキストで、短く重要なテキストもしくは数値のために用意されている
`headline2` | 見出しのバリエーション 2
`headline3` | 見出しのバリエーション 3
`headline4` | 見出しのバリエーション 4
`headline5` | 見出しのバリエーション 5
`headline6` | 見出しのバリエーション 6
`subtitle1` | 見出しよりも小さいもので、中程度に重要で長さが短いテキストのために用意されている
`subtitle2` | サブタイトルのバリエーション 2
`body1` | 長い表記に使用する
`body2` | ボディのバリエーション 2
`caption` | 画像に注釈をつけ、控えめに使用する
`button` | 異なるタイプのボタンによる操作の呼び出し
`overline` | 見出しを紹介するために、控えめに使用する

### CSS クラス

いくつかのコンポーネントには書式セットがあります。例えば、浮き上がったように表示される MDC Card は Body 1 と Body 2、そして Headline というスタイルが使われています。

マテリアルデザインのコンポーネントではない要素に書式を設定したいときは、以下の CSS クラスを適用することができます。

CSS クラス | 説明
--- | ---
`mdc-typography` | フォントを Roboto に設定する。
`mdc-typography--<STYLE>` | フォントプロパティを STYLE として設定する。[タイポグラフィスタイルの節](#typography-styles) を参照。

例えば、`headline1` スタイルにするには CSS クラスを `mdc-typography--headline1` にします。

### CSS カスタムプロパティ

CSS カスタムプロパティ | 説明
--- | ---
`--mdc-typography-font-family` | 基本のフォントファミリ
`--mdc-typography-<STYLE>-font-family` | STYLE のフォントファミリ。[タイポグラフィスタイルの節](#typography-styles) 参照
`--mdc-typography-<STYLE>-font-size` | STYLE のフォントサイズ。[タイポグラフィスタイルの節](#typography-styles) 参照
`--mdc-typography-<STYLE>-line-height` | STYLE の行の高さ。[タイポグラフィスタイルの節](#typography-styles) 参照
`--mdc-typography-<STYLE>-font-weight` | STYLE のフォントの太さ。[タイポグラフィスタイルの節](#typography-styles) 参照
`--mdc-typography-<STYLE>-letter-spacing` | STYLE のフォントの文字間隔。[タイポグラフィスタイルの節](#typography-styles) 参照
`--mdc-typography-<STYLE>-text-decoration` | STYLE のテキスト装飾。[タイポグラフィスタイルの節](#typography-styles) 参照
`--mdc-typography-<STYLE>-text-transform` | STYLE の文字変換。[タイポグラフィスタイルの節](#typography-styles) 参照

### Sass 変数とミキシン

Mixin | Description
--- | ---
`base` | フォントを Roboto に設定する。
`typography($style)` | フォントを Roboto にするなど、Typography の書式の一つを適用する。
`smooth-font` | タイポグラフィにアンチエイリアスを追加する。
`overflow-ellipsis` | 省略記号を付けてはみ出しているテキストを1行に切り詰める。
`baseline($top, $bottom, $display)` | テキストコンテンツを整列させるベースラインを設定する。
`zero-width-prefix` | コンテナのテキストに非表示、ゼロ幅のプレフィックスを追加する。デフォルトではテキストが空のときにコンテナの下に配置される代わりに、これによりベースラインがテキストの場所に常に来ることが保証されます。`baseline` ミキシンが既に適用されている場合は個のミキシンを使わないこと。
`text-baseline($top, $bottom, $display)` | フローテキストコンテンツのベースラインを設定する。

> **`overflow-ellipsis` に関する注釈**: `overflow-ellipsis` は要素が `display: block` であるか `display: inline-block` であるときにしか使ってはいけません。

#### `$style` の値

これらのスタイルは `mdc-typography` ミキシンにおいて `$style` 引数として使うことができます。

* `headline1`
* `headline2`
* `headline3`
* `headline4`
* `headline5`
* `headline6`
* `subtitle1`
* `subtitle2`
* `body1`
* `body2`
* `caption`
* `button`
* `overline`

#### スタイルの上書き

CSS カスタムプロパティか Sass のモジュール変数/グローバル変数を使うことにより、すべてのスタイルを上書きできます。

Sass **モジュール** 変数を使う際には、`$mdc-typography-styles-{style}` という名前を使うそのほかの `@use` ステートメントの _前に_ モジュールを設定しなくてはなりません。変数には特定のスタイルで上書きするすべてのプロパティを含むマップを割り当てる必要があります。

Sass **グローバル** 変数を使う際には、コンポーネントをインポートする _前に_ `$mdc-typography-styles-{style}` という名前のグローバル変数を設定することにより、これらの変数を定義しなくてはなりません。

**例:** `font-size` と `text-transform` プロパティを上書きする

CSS カスタムプロパティの場合:

```css
html {
  --mdc-typography-button-font-size: 16px;
  --mdc-typography-button-text-transform: none;
}
```

Sass モジュール変数の場合:

```scss
@use "@material/typography" with (
  $styles-button: (
    font-size: 16px,
    text-transform: none,
  )
);

@use "@material/button";
@include button.core-styles;
```

Sass グローバル変数の場合:

```scss
$mdc-typography-styles-button: (
  font-size: 16px,
  text-transform: none,
);

@import "@material/button/mdc-button";
```

**例:** グローパルな `font-family` プロパティを上書きする

CSS カスタムプロパティの場合:

```css
html {
  --mdc-typography-font-family: Arial, Helvetica, sans-serif;
}
```

Sass モジュール変数の場合:

```scss
@use "@material/typography" with (
  $font-family: unquote("Arial, Helvetica, sans-serif")
);

@use "@material/button";
@include button.core-styles;
```

Sass グローバル変数の場合:

```scss
$mdc-typography-font-family: unquote("Arial, Helvetica, sans-serif");

@import "@material/button/mdc-button";
```

**例:** `headline1` の `font-family` プロパティと `headline2` の `font-family` と `font-size` を上書きする

CSS カスタムプロパティの場合:

```css
html {
  --mdc-typography-headline1-font-family: Arial, Helvetica, sans-serif;
  --mdc-typography-headline2-font-family: Arial, Helvetica, sans-serif;
  --mdc-typography-headline2-font-size: 3.25rem;
}
```

Sass モジュール変数の場合:

```scss
@use "@material/typography" with (
  $styles-headline1: (
    $font-family: unquote("Arial, Helvetica, sans-serif")
  ),
  $styles-headline2: (
    $font-family: unquote("Arial, Helvetica, sans-serif"),
    $font-size: 3.25rem
  )
);

@use ...
```

Sass グローバル変数の場合:

```scss
$mdc-typography-styles-headline1: (
  font-family: unquote("Arial, Helvetica, sans-serif")
);
$mdc-typography-styles-headline2: (
  font-family: unquote("Arial, Helvetica, sans-serif"),
  font-size: 3.25rem
);

@import ...
```
