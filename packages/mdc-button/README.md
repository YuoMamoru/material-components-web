<!--docs:
title: "Buttons"
layout: detail
section: components
excerpt: "Material Design-styled buttons."
iconId: button
path: /catalog/buttons/
-->

# Buttons

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/button.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/buttons.png" width="363" alt="Buttons screenshot">
  </a>
</div>-->

MDC Button コンポーネントは [マテリアルデザインボタン要件](https://material.io/guidelines/components/buttons.html) に準拠したボタンコンポーネントです。このコンポーネントは JavaScritp を使用しなくても基本的な機能を備えており、あらゆる状況で機能します。`MDCRipple` をインスタンス化することにより `button` 要素にリップルエフェクトを持つようにボタンを拡張することができます。詳細は [MDC Ripple](../mdc-ripple) や [Demo](https://material-components-web.appspot.com/button.html) を参照してください。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/buttons.html">マテリアルデザインガイドライン: ボタン</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/button.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/button
```

## 使用法

### HTML 構造
```html
<button class="mdc-button">
  Button
</button>
```

> 注意: 例とドキュメントでは一般的な `<button>` を使用していますが、`<a class="mdc-button">Link Button</a>` のように意味的に適切な場所に `mdc-button` を適用することができます。

### アイコンの追加

アイコンを付けるためにボタン要素内に `mdc-button__icon` をネストすることができます。視認性の要件を満足するために、ボタン内のアイコンは 18px に設定されます。

私たちは Google Fonts から [Material Icons](https://material.io/icons/) を読み込むことを推奨しています。

```html
<head>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>

<button class="mdc-button">
  <i class="material-icons mdc-button__icon">favorite</i>
  Button
</button>
```

SVG アイコンを使うことも可能です。

```html
<button class="mdc-button">
  <svg class="mdc-button__icon" xmlns="http://www.w3.org/2000/svg" viewBox="...">
  ...
  </svg>
  SVG Icon
</button>
```

### CSS クラス


CSS クラス | 説明
--- | ---
`mdc-button` | 必須。デフォルトでは画面の表面と同一平面上にあるテキストボタン
`mdc-button__icon`    | オプション。アイコン要素用
`mdc-button--raised` | オプション。画面の表面から浮き上がったボタンにつける
`mdc-button--unelevated` | オプション。画面の表面と同一平面上にあるボタンにつける
`mdc-button--stroked` | オプション。画面の表面と同一平面上にあり、境界線のあるボタンにつける
`mdc-button--dense` | オプション。少し小さくするためにボタンのテキストを縮める


### 無効になったボタン

ボタン要素に直接 `disabled` を追加することも、ボタンを含んでいるフィールドセットに `disabled` を設定しボタンを無効にすることもできます。無効になったボタンは利用できなくなり、視覚的にも利用できるようなエフェクトがなくなります。

```html
<button class="mdc-button mdc-button--raised" disabled>
  Raised disabled button
</button>
```

### MDC Ripple の追加

ボタンにインクのリップルエフェクトを追加するには [ripple](../mdc-ripple) インスタンスをボタン要素にアタッチします。

```js
mdc.ripple.MDCRipple.attachTo(document.querySelector('.mdc-button'));
```

[material-components-web](../material-components-web) パッケージを使えば宣言的に行うこともできます。

```html
<button class="mdc-button" data-mdc-auto-init="MDCRipple">
  Flat button
</button>
```

ボタンは完全にリップルのスタイルを認識しているので、リップルエフェクトを使う上で DOM や CSS の変更は必要ありません。

### Sass ミキシン

デフォルトでは、MDC Button はテーマから色を引き継ぎ、 [マテリアルデザインボタン要件](https://material.io/guidelines/components/buttons.html) を適用します。ボタンの色やスタイルをカスタマイズする目的で以下のミキシンを使うことができます。

#### `mdc-button-filled-accessible($container-fill-color)`

このミキシンは <em>浮かび上がった (raised)</em> もしくは <em>同一平面上 (unelevated)</em> のボタンの色をカスタマイズするために提供されています。このミキシンはボタンのコンテナの色を指定した色に変え、アクセシビリティ標準に沿うようにボタンのインクとリップルの色を更新します。

### 高度な Sass ミキシン

> **高度なミキシンに関する注釈**: 以下のミキシンは上級者向けです。これらのミキシンはコンテナやインク、境界線、リップルの色を上書きします。完全にボタンをカスタマイズしたいのであればこれらのすべてを使えます。もしくは、例えばリップルの色だけを変えたいのであれば、これらの一つだけを使うことも可能です。**一緒に使われるコンテナ、インク、境界線、リップルの色を選び、アクセシビリティ標準を満たすことはあなたの責務になります。**

ミキシン | 説明
--- | ---
`mdc-button-container-fill-color($color)` | 与えた色にコンテナの色を設定する
`mdc-button-icon-color($color)` | 与えられた色にアイコンの色を設定する
`mdc-button-ink-color($color)` | 与えた色にインクの色を設定する。`mdc-button-icon-color` を使わないときはテキストとアイコンの両方に作用する
`mdc-button-corner-radius($corner-radius)` | 与えた大きさ（デフォルトは 2px）に角の丸め半径を設定する
`mdc-button-horizontal-padding($padding)` | 与えた大きさに水平方向のパディングを設定する
`mdc-button-stroke-color($color)` | 与えた色に境界の色を設定する
`mdc-button-stroke-width($width, $padding)` | 与えた大きさ（デフォルトは 2px）に境界線の太さを設定し、適切なパディングに調整する。`$padding` は `mdc-button-horizontal-padding` に固有の値が設定されている場合に限り必須

Button コンポーネントのリップルエフェクトは [MDC Ripple](../mdc-ripple) のミキシンを使って設定されています。

#### 注意: Edge と CSS 変数

CSS 変数を完全にサポートしているブラウザでは、テーマプロパティが渡されたら上記のミキシンは CSS 変数を使ってスタイルを設定します。しかし、Edge の CSS 変数サポートのバグのため、Edge では `mdc-button-container-fill-color` は CSS 変数が利用されません。もしテーマプロパティ（浮き上がったボタンや同一平面上のボタンは塗りつぶしの色にデフォルトでプライマリカラーを使っています）のために関係している CSS 変数を変えたいのであればコンテナのスタイルを手動で上書する必要がある、ということをこれは意味しています。
