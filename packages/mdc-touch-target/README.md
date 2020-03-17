<!--docs:
title: "Touch Target"
layout: detail
section: components
excerpt: "Increased touch targets for components"
path: /catalog/touchtarget/
-->

# Touch Target

Touch targets はユーザーの入力に応答する画面のパーツです。それらは要素の視覚的境界を超えて広がっています。例えば、ボタンは 48 x 36 px で表示されますが、周囲のパディングを含めると 48 x 48 px のタッチターゲットになります。

マテリアルデザイン仕様では、タッチターゲットは少なくとも 48 x 48 px にする必要があります。MDC Web ライブラリは以下のコンポーネントのタッチターゲットを広げるためのミキシンとガイダンスを提供しています。
* Button
* Chips
* Checkbox
* Radio
* Mini FAB

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/design/usability/accessibility.html#layout-typography">Material Design guidelines: タッチターゲット</a>
  </li>
</ul>

## インストール

```
npm install @material/touch-target
```

## 基本的な使用法

### HTML 構造

ボタンコーンコンポーネントがあります。

```html
<button class="mdc-button">
  <div class="mdc-button__ripple"></div>
  <span class="mdc-button__label">アクセスできないボタン</span>
</button>
```

以下のようにしてタッチターゲットを広げます。

```html
<div class="mdc-touch-target-wrapper">
  <button class="mdc-button mdc-button--touch">
    <div class="mdc-button__ripple"></div>
    <span class="mdc-button__label">アクセスできるボタン</span>
    <div class="mdc-button__touch"></div>
  </button>
</div>
```

隣り合う要素上でタッチターゲットが潜在的に重なることを避けたい場合にだけ、外側に `mdc-touch-target-wrapper` 要素が必要なことに注意してください（マージン縮小のため）。

### スタイル

```css
@use "@material/touch-target/mdc-touch-target";
```

## スタイルのカスタマイズ

### Sass ミキシン

ミキシン | 説明
--- | ---
`wrapper` | タッチターゲット要素のラッパーに適用する。
`touch-target` | タッチターゲット要素の内側に適用する。
`margin` | コンポーネントのルート要素に適用する。大きくなったタッチターゲットを補うためにマージンを追加する。
