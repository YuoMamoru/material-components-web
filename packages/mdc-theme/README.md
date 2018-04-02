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

このカラーパレットはイラストやブランドカラーの表現に使用できるプライマリカラーとセカンダリカラーから構成されています。

MDC Theme は MDC Web コンポーネントのテーマを表現する基盤となるモジュールです。このモジュール内の色は3つのテーマカラーから得られています。

* プライマリ(Primary): アプリケーションで使用される主たる色で、様々な UI 要素に適用されます。
* セカンダリ(Secondary): アプリケーションで使用される補助的な色で、様々な UI 要素に適用されます。（かつては「アクセント」と呼んでいました。）
* バックグランド(Background): アプリケーションの背景色、つまり、UI はその色の上に描画されます。

そして、5つのスタイルがあります。

* 主要(Primary): 大部分のテキストに使用されます。
* 副次的(Secondary): 視覚階層上の下位のテキストに使用されます。
* ヒント(Hint): 文字入力欄やラベルのヒントのようなヒントのテキストに使用されます。
* 利用できない項目(Disabled): 利用不可となっているコンポーネントやコンテンツのテキストに使用されます。
* アイコン(Icon): アイコンに使用されます。

> **Primary と Secondary に関する注釈**: primary/secondary _color_ を primary/secondary _text_ と混同しないでください。前者は視覚的な独自性を持たせるために、アプリケーションの様々な場所に色を付けることを目的とした primary/secondary _theme_ color を指します。後者はより目立たせる（低い不透明度や高いコントラスト）ために表示されるほとんどの要素に対して使用されるテキストのスタイルを指します。（訳注: この訳では _primary/secondary_ を前者は「プライマリ/セカンダリ」と、後者は「主要/副次的」と訳し分けています。）

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/style/color.html">マテリアルデザインガイドライン: カラー</a>
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

### テーマカラーの変更

MDC Theme はブランドカラーを表現することを容易に実現してくれます。Sass か CSS カスタムプロパティを通じてデフォルトのテーマカラーを上書きすればよいのです。CSS カスタムプロパティはランタイムテーマを可能にしてくれます。

> **Sass 変数に関する注釈**: mdc-theme や それに依存する MDC Web のコンポーネントをインポートする前に、次のように、 3つのテーマカラーの変数を定義する必要があります。

```scss
$mdc-theme-primary: #9c27b0; // Purple 500
$mdc-theme-secondary: #ffab40; // Orange A200
$mdc-theme-background: #fff; // White

@import "@material/theme/mdc-theme";
```

> **`$mdc-theme-secondary` に関する注釈**: この変数は以前、`$mdc-theme-accent` という名前でした。下位互換のために `$mdc-theme-accent` はまだ存在しますが、この変数は **非推奨** です。かつて `$mdc-theme-accent` をカスタマイズしたアプリは引き続き動作しますが、新しいアプリでは `$mdc-theme-secondary` を代わりに使ってください。

これらの選択されたテーマカラー上に配置されるテキストの色はコントラストに基いてプログラム上で計算されます。私たちは Web Content Accessibility Guidelines 2.0 にしたがっています。

https://www.w3.org/TR/WCAG20

#### CSS カスタムプロパティ

> **`<TEXT_STYLE>` と `<THEME_COLOR>` に関する注釈**: `<TEXT_STYLE>` は上でリストにあげたテキストのスタイルを小文字にしたものを表しています（例: `hint`）。`<THEME_COLOR>` は上でリストに挙げたテーマカラーを小文字にした名前を表しています（例: `secondary`）。両方配置すると `--mdc-theme-text-hint-on-secondary` といった具合になります。

CSS カスタムプロパティ | 説明
--- | ---
`--mdc-theme-primary` | テーマのプライマリカラー
`--mdc-theme-secondary` | テーマのセカンダリカラー
`--mdc-theme-background` | テーマのバックグランドカラー
`--mdc-theme-text-<TEXT_STYLE>-on-<THEME_COLOR>` | THEME_COLOR の背景の上にある TEXT_STYLE のテキストの色
`--mdc-theme-text-<TEXT_STYLE>-on-light` | 明るい色の背景上にある TEXT_STYLE のテキストの色
`--mdc-theme-text-<TEXT_STYLE>-on-dark` | 暗い色の背景上にある TEXT_STYLE のテキストの色

### CSS クラス

MDC Web はコンポーネントのカスタマイズを容易にするために `mdc-button-filled-accessible` のような Sass ミキシンも提供しています。より詳しい情報は各コンポーネントのドキュメントを調べてください。

マテリアルデザインのコンポーネント以外の要素を変更したいなら、以下の CSS 修飾クラスが使えます。

> **`<TEXT_STYLE>` と `<THEME_COLOR>` に関する注釈**: `<TEXT_STYLE>` は上でリストに挙げたテキストのスタイルを小文字にしたものを表しています（例: `hint`）。`<THEME_COLOR>` は上でリストに挙げたテーマカラーを小文字にした名前を表しています（例: `secondary`）。両方配置すると `mdc-theme--text-hint-on-secondary` といった具合になります。

CSS クラス | 説明
--- | ---
`mdc-theme--primary` | テキスト色としてテーマのプライマリカラーを設定する
`mdc-theme--secondary` | テキスト色としてテーマのセカンダリカラーを設定する
`mdc-theme--background` | 背景色としてテーマのバックグランドカラーを設定する
`mdc-theme--primary-bg` | 背景色としてテーマのプライマリカラーを設定する
`mdc-theme--secondary-bg` | 背景色としてテーマのセカンダリカラーを設定する
`mdc-theme--text-<TEXT_STYLE>-on-<THEME_COLOR>` | THEME_COLOR の背景の上に、TEXT_STYLE に適切なテキスト色を設定する
`mdc-theme--text-<TEXT_STYLE>-on-light` | 明るい背景の上に、TEXT_STYLE に適切なテキスト色を設定する
`mdc-theme--text-<TEXT_STYLE>-on-dark` | 暗い背景の上に、TEXT_STYLE に適切なテキスト色を設定する

### Sass ミキシンと変数と関数

ミキシン | 説明
--- | ---
`mdc-theme-prop($property, $style, $important, $edgeOptOut)` | テーマカラーもしくは CSS プロパティ形式のカスタムカラーを、必要であれば `!important` を付けて適用する。`$edgeOptOut` が `true` でテーマカラーが渡されたときは、バグのある CSS 変数のサポートの問題を回避するため Edge においてスタイルを除外し、 `@supports` 句でスタイルをラップする。

#### `mdc-theme-prop` のプロパティ

`mdc-theme-prop` ミキシンでは以下のプロパティを `$style` 引数として使用することができます。これらの代わりに色リテラル（例: `rgba(0, 0, 0, .75)`）を使うこともできます。

> **`<TEXT_STYLE>` と `<THEME_COLOR>` に関する注釈**: `<TEXT_STYLE>` は上でリストに挙げたテキストのスタイルを小文字にしたものを表しています（例: `hint`）。`<THEME_COLOR>` は上でリストに挙げたテーマカラーを小文字にした名前を表しています（例: `secondary`）。両方配置すると `text-hint-on-secondary` といった具合になります。

プロパティ名 | 説明
--- | ---
`primary` | テーマのプライマリカラー
`secondary` | テーマのセカンダリカラー
`background` | テーマのバックグランドカラー
`text-<TEXT_STYLE>-on-<THEME_COLOR>` | THEME_COLOR の背景の上にある TEXT_STYLE
`text-<TEXT_STYLE>-on-light` | 明るい色の背景上にある TEXT_STYLE
`text-<TEXT_STYLE>-on-dark` | 暗い色の背景上にある TEXT_STYLE

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
