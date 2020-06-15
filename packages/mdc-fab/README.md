<!--docs:
title: "Floating Action Button"
layout: detail
section: components
excerpt: "A floating action button represents the primary action in an application"
iconId: button
path: /catalog/buttons/floating-action-buttons/
-->

# Floating action buttons

フローティング操作ボタン（FAB）は画面の主要な操作を表すものです。

FAB には3つのタイプがあります。

1. [通常の FAB](#regular-fabs)
2. [小さな FAB](#mini-fabs)
3. [拡張 FAB](#extended-fabs)

![通常 FAB の例](images/FAB_types.png)

## FAB の使用法

FAB は画面上の主要な、もしくは最も一般的な操作を実行します。画面のすべてのコンテンツの前面に表示され、典型的には中心にアイコンのある丸い形状をしています。

### インストール

```
npm install @material/fab
```

### スタイル

```scss
@use "@material/fab";

@include fab.core-styles;
```

### アイコンの読み込み

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

### JavaScript のインスタンス化

FAB は JavaScript なしでも動作しますが、ルート要素上の `MDCRipple` をインスタンス化することによりリップルエフェクトをつけることができます。詳細は [MDC Ripple](../mdc-ripple) を参照してください。

```js
import {MDCRipple} from '@material/ripple';

const fabRipple = new MDCRipple(document.querySelector('.mdc-fab'));
```

> JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

### FAB を操作しやすくする

マテリアルデザイン仕様ではタッチの対象は少なくとも  48 x 48 px にすることを勧めています。FAB はデフォルトで 48 x 48 px で、ミニ FAB は 40 x 40 px です。ミニ FAB ではこの要件を満たすために以下のものを追加します。

```html
<div class="mdc-touch-target-wrapper">
  <button class="mdc-fab mdc-fab--mini mdc-fab--touch">
    <div class="mdc-fab__ripple"></div>
    <span class="material-icons mdc-fab__icon">add</span>
    <span class="mdc-fab__label">Create</span>
    <div class="mdc-fab__touch"></div>
  </button>
</div>
```

**注意: 隣接している要素において、潜在的に（マージンを縮小するために）タッチ対象が重なってしまうのを避けたい場合は、外側に `mdc-touch-target-wrapper` 要素だけが必要です。**

## <a name="regular-fabs"></a>通常の FAB

通常の FAB は拡張のない通常のサイズの FAB です。

### 通常の FAB の例

```html
<button class="mdc-fab" aria-label="Favorite">
  <div class="mdc-fab__ripple"></div>
  <span class="mdc-fab__icon material-icons">favorite</span>
</button>
```

**注意: フローティング操作ボタンには `span`、`i`、`img` もしくは `svg` 要素を使うことができます。**

**注意: マテリアルアイコンテキストの後ろに改行もしくはスペースがあるとき、IE 11 はアイコンを正しく中央に配置しません。**

## <a name="mini-fabs"></a>小さな FAB

小さな FAB はより小さな画面で使われるものです。

小さな FAB は他の画面要素との視覚的な連続性を作り出すこともできます。

### 小さな FAB の例

```html
<button class="mdc-fab mdc-fab--mini" aria-label="Favorite">
  <div class="mdc-fab__ripple"></div>
  <span class="mdc-fab__icon material-icons">favorite</span>
</button>
```

## <a name="extended-fabs"></a>拡張 FAB

拡張 FAB は広く、テキストラベルを含んでいます。

### 拡張 FAB の例

```html
<button class="mdc-fab mdc-fab--extended">
  <div class="mdc-fab__ripple"></div>
  <span class="material-icons mdc-fab__icon">add</span>
  <span class="mdc-fab__label">Create</span>
</button>
```

**注意: 拡張 FAB はアイコンがオプションであるのに対してラベルは必ず入れる必要があります。アイコントラベルはコンテキストに基づいて適切な順序で指定することができます。**

## API

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-fab` | 必須。ボタン要素用
`mdc-fab__icon` | 必須。アイコン要素用
`mdc-fab__ripple` | 必須。リップルスタイルで表示される要素用。
`mdc-fab__label` | オプション。テキストラベルで使われる。拡張 FAB にのみ適用される。
`mdc-fab--mini` | オプション。FAB を小さいサイズにする
`mdc-fab--extended` | オプション。FAB をテキストラベルが収まる大きさにする。
`mdc-fab--exited` | オプション。FAB をビューの外にアニメーションさせる。<br>このクラスが削除されると FAB がビューに戻ってくる。

> **`:disabled` に関する注釈**: FAB には無効なスタイルが定義されていません。FAB は操作を促すもので、無効な状態で表示すべきではありません。もし操作を行わない FAB を置きたいのであればユーザーへの説明も書いておかなくてはなりません。

### Sass ミキシン

#### 基本的な Sass ミキシン

MDC FAB はデフォルトで [MDC Theme](../mdc-theme) の `secondary` カラーを使います。カスタマイズするには次のミキシンを使います。

ミキシン | 説明
--- | ---
`accessible($container-color)` | FAB のコンテナの色を指定した色に変え、アクセシビリティ標準に沿うように FAB のインクとリップルの色を更新する。
`extended-fluid` | 拡張 FAB をスクリーン幅やレイアウトグリッドのようなコンテナに対してリキッドレイアウトにする。`@media` クエリの使用をサポートする幹審として公開されている。

#### 高度な Sass ミキシン

> **高度なミキシンに関する注釈**: 以下のミキシンは上級者向けです。これらのミキシンはコンテナやインク、リップルの色を上書きします。完全に FAB をカスタマイズしたいのであればこれらのすべてを使えます。もしくは、例えばリップルの色だけを変えたいのであれば、これらの一つだけを使うことも可能です。**一緒に使われるコンテナ、インク、リップルの色を選び、アクセシビリティ標準を満たすことはあなたの責務になります。**

ミキシン | 説明
--- | ---
`container-color($color)` | 与えた色にコンテナの色を設定する
`icon-size($width, $height)` |  `width` と `height` を指定することにより、アイコンの `width`、`height` と `font-size` プロパティを設定する。`$height` はオプションで省略した際には `$width` の値が設定される。`font-size` は `$width` の値に応じて設定される。
`ink-color($color)` | 与えた色にインクの色を設定する
`extended-padding($icon-padding, $label-padding)` | アイコンの両側およびラベルと FAB の端の間のパディングを設定する。アイコンがないときは、`$label-padding` は両側に適用される。
`extended-label-padding($label-padding)` | 拡張 FAB のラベルの両側のパディングを設定する。アイコンのない拡張 FAB のスタイルを設定するする際に便利。
`shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状に通常 FAB とミニ FAB に限ってを設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`extended-shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状に拡張 FAB を設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
