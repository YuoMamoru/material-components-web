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

MDC Typography は MDC Web コンポーネントにこれらのスタイルを適用する基盤となるモジュールです。このモジュールの書式は以下の10個のスタイルから派生しています。

* Display 4
* Display 3
* Display 2
* Display 1
* Headline
* Title
* Subheading 2
* Subheading 1
* Body 2
* Body 1
* Caption
* Button

### 使用法

```html
<head>
  <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500" rel="stylesheet">
</head>
<body class="mdc-typography">
  <h1 class="mdc-typography--display4">Big header</h1>
</body>
```

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/style/typography.html">マテリアルデザインガイドライン: タイポグラフィ</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/typography.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install --save @material/typography
```

## 使用法

### Roboto フォントのロード

私たちは Google Fonts から Roboto を読み込むことを推奨しています。

```html
<head>
  <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500" rel="stylesheet">
</head>
<body class="mdc-typography">
  <h1 class="mdc-typography--display4">Big header</h1>
</body>
```

### CSS クラス

いくつかのコンポーネントには書式セットがあります。例えば、浮き上がったように表示される MDC Card は Body 1 と Body 2、そして Headline というスタイルが使われています。

マテリアルデザインのコンポーネントではない要素に書式を設定したいときは、以下の CSS クラスを適用することができます。

CSS クラス | 説明
--- | ---
`mdc-typography` | フォントを Roboto に設定する。
`mdc-typography--display4` | フォントのプロパティを Display 4 に設定する。
`mdc-typography--display3` | フォントのプロパティを Display 3 に設定する。
`mdc-typography--display2` | フォントのプロパティを Display 2 に設定する。
`mdc-typography--display1` | フォントのプロパティを Display 1 に設定する。
`mdc-typography--headline` | フォントのプロパティを Headline に設定する。
`mdc-typography--title` | フォントのプロパティを Title に設定する。
`mdc-typography--subheading2` | フォントのプロパティを Subheading 2 に設定する。
`mdc-typography--subheading1` | フォントのプロパティを Subheading 1 に設定する。
`mdc-typography--body2` | フォントのプロパティを Body 2 に設定する。
`mdc-typography--body1` | フォントのプロパティを Body 1 に設定する。
`mdc-typography--caption` | フォントのプロパティを Caption に設定する。
`mdc-typography--button` | フォントのプロパティを Button に設定する。
`mdc-typography--adjust-margin` | テキストを整列させる。上にあるフォントクラスと共に使用する。

> **`mdc-typography--adjust-margin` に関する注釈**: `mdc-typography--adjust-margin` は適用された要素の margin プロパティを変更し、テキストを正しく整列させます。`mdc-typography--adjust-margin` はテキストコンテンツでのみ使用するべきで、ボタンのような UI 要素で使用しても正しく整列しないことがあります。

### Sass 変素とミキシン

ミキシン | 説明
--- | ---
`mdc-typography-base` | フォントを Roboto に設定する。
`mdc-typography($style)` | フォントを Roboto にするなど、Typography の書式の一つを適用する。
`mdc-typography-adjust-margin($style)` | テキストを整列させる。
`mdc-typography-overflow-ellipsis` | 省略記号を付けてはみ出しているテキストを1行に切り詰める

> **`mdc-typography-adjust-margin` に関する注釈**: `mdc-typography-adjust-margin` は適用された要素の margin プロパティを変更し、テキストを正しく整列させます。`mdc-typography-adjust-margin` はテキストコンテンツでのみ使用するべきで、ボタンのような UI 要素で使用しても正しく整列しないことがあります。

> **`mdc-typography-overflow-ellipsis` に関する注釈**: `mdc-typography-overflow-ellipsis` は要素が `display: block` であるか `display: inline-block` であるときにしか使ってはいけません。

#### `$style` の値

これらのスタイルは `mdc-typography` ミキシンと `mdc-typography-adjust-margin` ミキシンにおいて `$style` 引数として使うことができます。

* `display4`
* `display3`
* `display2`
* `display1`
* `headline`
* `title`
* `subheading2`
* `subheading1`
* `body2`
* `body1`
* `caption`
* `button`
