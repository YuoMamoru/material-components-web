<!--docs:
title: "Theme"
layout: detail
section: components
excerpt: "Color theming for MDC Web components."
iconId: theme
path: /catalog/theme/
-->

# Theme

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/theme/index.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/themes.png" width="241" alt="Themes screenshot">
  </a>
</div>-->

あなたのブランドやスタイルを反映した色の体系を作るためにマテリアルデザインのカラーシステムは使用されます。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-theming">マテリアルデザインガイドライン: カラー</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/theme/index.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/theme
```

## 使用法

### 色の体系

MDC Web のコンポーネントをインポートする前にテーマカラーの変数を定義できます。

```scss
$mdc-theme-primary: #fcb8ab;
$mdc-theme-secondary: #feeae6;
$mdc-theme-on-primary: #442b2d;
$mdc-theme-on-secondary: #442b2d;

@import "@material/button/mdc-button";
```

on-primary や on-secondary などの値を決める際には、Web Content Accessibility Guidelines 2.0 にしたがうことを推奨します。これらの値は primary や secondary といった該当する値の上で視認性を確保する必要があります。

https://www.w3.org/TR/WCAG20

### 高度なカスタマイズ

色の体系ではよく設計されたアプリにおける道のりの80%しか得られません。必然的に「枠の外」には動作しないコンポーネントがでてきます。視認性とデザインの問題を解決するためには、`mdc-button-filled-accessible` のような Sass ミキシンを使うとよいでしょう。詳細は各コンポーネントのドキュメントを参照してください。

### Sass を使わないカスタマイズ

マテリアルデザインの色のカスタマイズ機能の中の非常に限定されたものですが、Sass を使わない方法を提供しています。CSS カスタムプロパティを設定する方法と CSS クラスを設定する方ホです。

#### CSS カスタムプロパティ

> **`<TEXT_STYLE>` に関する注釈**: `<TEXT_STYLE>` は上でリストにあげたテキストのスタイルを小文字にしたものを表しています（例: `hint`）。

CSS カスタムプロパティ | 説明
--- | ---
`--mdc-theme-primary` | テーマのプライマリカラー
`--mdc-theme-secondary` | テーマのセカンダリカラー
`--mdc-theme-background` | テーマのバックグランドカラー
`--mdc-theme-surface` | テーマのサーフェイスカラー
`--mdc-theme-on-primary` | プライマリカラーの背景の上にあるテキストの色
`--mdc-theme-on-secondary` | セカンダリカラーの背景の上にあるテキストの色
`--mdc-theme-on-surface` | サーフェイスカラーの背景の上にあるテキストの色
`--mdc-theme-text-<TEXT_STYLE>-on-light` | 明るい色の背景上にある TEXT_STYLE のテキストの色
`--mdc-theme-text-<TEXT_STYLE>-on-dark` | 暗い色の背景上にある TEXT_STYLE のテキストの色

#### CSS クラス

> **`<TEXT_STYLE>` に関する注釈**: `<TEXT_STYLE>` は上でリストに挙げたテキストのスタイルを小文字にしたものを表しています（例: `hint`）。

CSS クラス | 説明
--- | ---
`mdc-theme--primary` | テキスト色としてテーマのプライマリカラーを設定する
`mdc-theme--secondary` | テキスト色としてテーマのセカンダリカラーを設定する
`mdc-theme--background` | 背景色としてテーマのバックグランドカラーを設定する
`mdc-theme--surface` | 表面色としてテーマのサーフェイスカラーを設定する
`mdc-theme--on-primary` | プライマリカラーの背景の上に適切なテキスト色を設定する
`mdc-theme--on-secondary` | セカンダリカラーの背景の上に適切なテキスト色を設定する
`mdc-theme--on-surface` | サーフェイスカラーの背景の上に適切なテキスト色を設定する
`mdc-theme--primary-bg` | 背景色としてテーマのプライマリカラーを設定する
`mdc-theme--secondary-bg` | 背景色としてテーマのセカンダリカラーを設定する
`mdc-theme--text-<TEXT_STYLE>-on-light` | 明るい背景の上に、TEXT_STYLE に適切なテキスト色を設定する
`mdc-theme--text-<TEXT_STYLE>-on-dark` | 暗い背景の上に、TEXT_STYLE に適切なテキスト色を設定する

### Sass ミキシンと変数と関数

ミキシン | 説明
--- | ---
`mdc-theme-prop($property, $style, $important, $edgeOptOut)` | テーマカラーもしくは CSS プロパティ形式のカスタムカラーを、必要であれば `!important` を付けて適用する。`$edgeOptOut` が `true` でテーマカラーが渡されたときは、バグのある CSS 変数のサポートの問題を回避するため Edge においてスタイルを除外し、 `@supports` 句でスタイルをラップする。

#### `mdc-theme-prop` のプロパティ

`mdc-theme-prop` ミキシンでは以下のプロパティを `$style` 引数として使用することができます。これらの代わりに色リテラル（例: `rgba(0, 0, 0, .75)`）を使うこともできます。

> **`<TEXT_STYLE>` に関する注釈**: `<TEXT_STYLE>` は上でリストに挙げたテキストのスタイルを小文字にしたものを表しています（例: `hint`）。

プロパティ名 | 説明
--- | ---
`primary` | テーマのプライマリカラー
`secondary` | テーマのセカンダリカラー
`background` | テーマのバックグランドカラー
`surface` | テーマのサーフェイスカラー
`text-<TEXT_STYLE>-on-light` | 明るい色の背景上にある TEXT_STYLE
`text-<TEXT_STYLE>-on-dark` | 暗い色の背景上にある TEXT_STYLE
`on-primary` | プライマリカラーの背景の上に使用されるテキスト/アイコンの色
`on-secondary` | セカンダリカラーの背景の上に使用されるテキスト/アイコンの色
`on-surface` | サーフェイスカラーの背景の上に使用されるテキスト/アイコンの色

#### `mdc-theme-luminance($color)`

与えられた色の輝度値（0～1）を計算します。

```scss
@debug mdc-theme-luminance(#9c27b0); // 0.11654
```

#### `mdc-theme-contrast($back, $front)`

2つの色のコントラスト比を計算します。

```scss
@debug mdc-theme-contrast(#9c27b0, #000); // 3.33071
```

#### `mdc-theme-tone($color)`

与えられた色が「明るい」か「暗い」かを判定します。

入力された色が `"light"` もしくは `"dark"` と等しい文字列リテラルのときは、入力値をそのまま返します。

```scss
@debug mdc-theme-tone(#9c27b0); // dark
@debug mdc-theme-tone(light);   // light
```

#### `mdc-theme-contrast-tone($color)`

与えられた色の上にのせるテキストを明るくすべきか暗くすべきかを判定します。

```scss
@debug mdc-theme-contrast-tone(#9c27b0); // light
```

#### `mdc-theme-prop-value($property)`

`$property` が色リテラル（例: `blue` や `#fff`）のときは入力値をそのまま返します。そうでないときはテーマのプロパティと一致する値（`$mdc-theme-property-values` に収められています）を返します。`$property` が色でもテーマプロパティに存在する値でもないときはエラーがスローされます。

これは主に `mdc-theme-prop` を直接利用できない状況（例: `box-shadow`）で役立ちます。

`mdc-theme-prop` ミキシンと違って、この関数は CSS カスタムプロパティをサポートして <em>いません</em>。テーマプロパティに指定された生の色だけを返します。

> 注意: 循環インポートを避けるため、この関数は `_functions.scss` ではなく、`_variables.scss` で定義されています。

```scss
@debug mdc-theme-prop-value(primary); // #3f51b5
@debug mdc-theme-prop-value(blue);    // blue
```

#### `mdc-theme-accessible-ink-color($fill-color, $text-style: primary)`

与えられた塗りの色に対して十分なコントラストを持ち視認性のあるインクの色を返します。

引数:

- `$fill-color`: `mdc-theme-prop-value` と同様な値をサポートしています。
- `$text-style`: 以下のいずれかの値でなくてはなりません: `primary`, `secondary`, `hint`, `disabled`, `icon`（`$mdc-theme-text-colors` を参照）。

> 注意: 循環インポートを避けるため、この関数は `_functions.scss` ではなく、`_variables.scss` で定義されています。

```scss
@debug mdc-theme-accessible-ink-color(secondary); // rgba(0, 0, 0, .87) (text-primary-on-light)
@debug mdc-theme-accessible-ink-color(blue);      // white              (text-primary-on-dark)
```
