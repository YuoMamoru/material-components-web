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

### CSS クラス

いくつかのコンポーネントには書式セットがあります。例えば、浮き上がったように表示される MDC Card は Body 1 と Body 2、そして Headline というスタイルが使われています。

マテリアルデザインのコンポーネントではない要素に書式を設定したいときは、以下の CSS クラスを適用することができます。

CSS クラス | 説明
--- | ---
`mdc-typography` | フォントを Roboto に設定する。
`mdc-typography--headline1` | フォントのプロパティを Headline 1 に設定する。
`mdc-typography--headline2` | フォントのプロパティを Headline 2 に設定する。
`mdc-typography--headline3` | フォントのプロパティを Headline 3 に設定する。
`mdc-typography--headline4` | フォントのプロパティを Headline 4 に設定する。
`mdc-typography--headline5` | フォントのプロパティを Headline 5 に設定する。
`mdc-typography--headline6` | フォントのプロパティを Headline 6 に設定する。
`mdc-typography--subtitle1` | フォントのプロパティを Subtitle 1 に設定する。
`mdc-typography--subtitle2` | フォントのプロパティを Subtitle 2 に設定する。
`mdc-typography--body1` | フォントのプロパティを Body 1 に設定する。
`mdc-typography--body2` | フォントのプロパティを Body 2 に設定する。
`mdc-typography--caption` | フォントのプロパティを Caption に設定する。
`mdc-typography--button` | フォントのプロパティを Button に設定する。
`mdc-typography--overline` | フォントのプロパティを Overline に設定する。

### Sass 変素とミキシン

ミキシン | 説明
--- | ---
`base` | フォントを Roboto に設定する。
`mdc-typography($style)` | フォントを Roboto にするなど、Typography の書式の一つを適用する。
`overflow-ellipsis` | 省略記号を付けてはみ出しているテキストを1行に切り詰める。
`baseline-top($distance)` | テキスト要素の上からベースラインまでの高さを設定する。
`baseline-bottom($distance)` | テキストのベースラインから下までの間隔を設定する。子のミキシンはベースラインから次のテキスト要素までの間隔を設定したいときは、`baseline-top` と組み合わせる必要がある。

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

コンポーネントをインポートする <em>前に</em> `$mdc-typography-styles-{style}` という名前のグローバル変数を設定することにより、すべてのスタイルを上書きできます。この変数には上書きしたい具体的スタイルのすべてを含んだマップを指定する必要があります。

例: `font-size` と `text-transform` プロパティを上書きする

```scss
$mdc-typography-styles-button: (
  font-size: 16px,
  text-transform: none,
);

@use "@material/button/mdc-button";
```

例: グローパルな `font-family` プロパティを上書きする
```scss
$mdc-typography-font-family: unquote("Arial, Helvetica, sans-serif");

...
@use ...
```

例:  `headline1` の `font-family` プロパティと `headline2` の `font-family` と `font-size` を上書きする
```scss
$mdc-typography-styles-headline1: (
  font-family: unquote("Arial, Helvetica, sans-serif")
);
$mdc-typography-styles-headline2: (
  font-family: unquote("Arial, Helvetica, sans-serif"),
  font-size: 3.25rem
);

...
@use ...
```
