<!--docs:
title: "Elevation"
layout: detail
section: components
excerpt: "Shadows and elevation as Sass mixins and CSS classes."
iconId: shadow
path: /catalog/elevation/
-->

# Elevation

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/elevation">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/elevation.png" width="247" alt="Elevation screenshot">
  </a>
</div>-->

影はオブジェクトの深さや奥行方向の動きを知る重要な視覚的な手がかりを与えます。それらは表面の離れている量を表す唯一の視覚的手がかりなのです。オブジェクトのエレベーションはそれらの影の見た目で決まります。エレベーションの値は「z-space」で表現され、 `0` から `24` までの範囲です。

> **「z-space」に関する注意**: 仕様では、エレベーションは通常 `dp` 値により表現されます。言い換えると、基本となるマテリアルから何「ピクセル」上にあるかということです。コンピュータ上では、通常 3D 座標系で表されます。私たちは `z-space`（もしくは短く単に「z」）というのが好きです。なぜなら、それは 3D 座標系の技術的定義や命名法に沿っているからです。したがって、私たちは「dp」よりそれがセンスがあると感じています。しかし、私たちが「z-space」（または「z」）を参照する際に、仕様にある「dp」と入れ替えて使うことができます。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-elevation">マテリアルデザインガイドライン: 影とエレベーション</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/elevation">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/elevation
```

## 基本的な使用法

### HTML

エレベーションはしばしば別のコンポーネント（例えば、浮き上がりボタンや浮き上がりカード）の基本スタイルに既に含まれています。

しかし、指定したコンポーネントで `mdc-elevation--z<N>` クラスを使うことによりエレベーションを適用することもできます。

```html
  <div class="mdc-elevation--z1">
    <!-- ... コンテンツ ... -->
  </div>
```

#### エレベーションオーバーレイ

エレベーションオーバーレイは積み上げられたコンテンツ内でコンポーネントコンテナの*上に*、リップルの*下に*表示されます。これを実現するために、`.mdc-elevation-overlay` 要素は DOM コンテンツの `.mdc-<component>__ripple` 要素の前に表示する必要があります。タッチターゲットを伴うボタンのマークアップ例を以下に示します。

```html
<button class="mdc-button mdc-button--raised">
  <div class="mdc-elevation-overlay"></div>
  <div class="mdc-button__ripple"></div>
  <i class="material-icons mdc-button__icon" aria-hidden="true">favorite</i>
  <span class="mdc-button__label">Font Icon</span>
</button>
```

これによりリップル部分はオーバーレイの*上に*描画されます。

### スタイル

```scss
@import "@material/elevation/mdc-elevation";
```

## スタイルのカスタマイズ

### CSS クラス

いくつかのコンポーネントはエレベーションが設定されています。例えば、浮き上がり MDC ボタンは エレベーション 2 です。

マテリアルデザインコンポーネント以外の要素にエレベーションを設定したいなら、以下の CSS クラスを適用できます。

CSS クラス | 説明
--- | ---
`mdc-elevation--z<N>` | (N)dp のエレベーションを設定する。N は 1 <= N <= 24 の範囲。
`mdc-elevation-transition` | エレベーション間の要素のトランジッションをするにあたり適切な CSS ルールを適用する。

### Sass ミキシン、変数と関数

ミキシン | 説明
--- | ---
`mdc-elevation($z-value, $color, $opacity-boost)` | エレベーションを与えるためにエレベーションを z-space に設定し、オプションで影の色の設定や不透明度を高める
`mdc-elevation-overlay-common` | ユニバーサルエレベーションオーバレイスタイルを設定するためにアプリケーションごとに1回呼び出される
`mdc-elevation-shadow($box-shadow)` | 最も近い親セレクターの `box-shadow` を設定する
`mdc-elevation-overlay-surface-position` | オーバーレイを中央に適切に配置できるように、オーバーレイの表層要素の位置を設定する
`mdc-elevation-overlay-size($width, $height: $width)` | エレベーションオーバーレイの幅と高さを設定する
`mdc-elevation-overlay-fill-color($color)` | エレベーションオーバーレイの色を設定する
`mdc-elevation-overlay-opacity($opacity)` | エレベーションオーバーレイの不透明度を設定する


関数 | 説明
--- | ---
`mdc-elevation-transition-value($duration, $easing)` | エレベーション間の要素のトランジッションの際の `transision` プロパティの値を返す
`mdc-elevation-overlay-transition-value($duration, $easing)` | エレベーション間のエレベーションオーバーレイの遷移のための `transition` プロパティの値を返す

変数 | 説明
--- | ---
`$mdc-elevation-property` | エレベーショントランジッションのデフォルトプロパティ
`$mdc-elevation-transition-duration` | エレベーショントランジッションのデフォルトの duration 値
`$mdc-elevation-transition-timing-function` | エレベーショントランジッションのデフォルトの easing 値
`$mdc-elevation-overlay-color` | エレベーションオーバーレイのデフォルトの色
`$mdc-elevation-overlay-property` | エレベーションオーバーレイトランジッションのデフォルトプロパティ

よりトランジッションに関して設定が必要なら、エクスポートした sass 変数とともに `mdc-elevation-transition-value` 関数を使用します。

```scss
.my-component-with-custom-transitions {

  transition:
    mdc-elevation-transition-value(),
    /* エレベーションと同じ duration と easing 値を使って不透明度を設定する */
    opacity $mdc-elevation-transition-duration $mdc-elevation-transition-timing-function;
  opacity: .7;
  will-change: $mdc-elevation-property, opacity;
}
```
