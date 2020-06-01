<!--docs:
title: "Shape"
layout: detail
section: components
excerpt: "Shapes direct attention, identify components, communicate state, and express brand."
path: /catalog/shape/
-->

# Shape

シェイプは注意をひきつけ、コンポーネントを識別し、状態を伝え、ブランドを表現するものです。

> 現在、Web のシェイプシステムは角の丸めだけをサポートしています。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-shape">Material Design guidelines: シェイプ</a>
  </li>
</ul>

## インストール

```
npm install @material/shape
```

## 基本的な使用法

### スタイル

```scss
@use "@material/shape";
```

## スタイルのカスタマイズ

### Sass 変数

マテリアルシェイプシステムではコンポーネントは小さいもの、中程度のもの、大きいものに分類されます。以下の Sass 変数を上書きすることにより、それぞれの分類のすべてのコンポーネントが変更されます。

変数 | 説明
--- | ---
`$small-component-radius` | 小さいコンポーネントの角の丸めの大きさ。デフォルトは `4px`。
`$medium-component-radius` | 中程度のコンポーネントの角の丸めの大きさ。デフォルトは `4px`。
`$large-component-radius` | 大きいコンポーネントの角の丸めの大きさ。デフォルトは `0`。

コンポーネントの分類方法について学ぶには [Material Design guidelines: シェイプ](https://material.io/go/design-shape) を参照してください。

**注意: 現在は丸まったシェイプで残だけをサポートしています。**

### CSS カスタムプロパティ

CSS カスタムプロパティ | 説明
--- | ---
`--mdc-shape-small` | 小さいコンポーネントのための丸まったシェイプの半径の大きさ。デフォルトは `4px`。
`--mdc-shape-medium` | 小さい（訳注: 記載誤りと思われる）コンポーネントのための丸まったシェイプの半径の大きさ。デフォルトは `4px`。
`--mdc-shape-large` | 小さい（訳注: 記載誤りと思われる）コンポーネントのための丸まったシェイプの半径の大きさ。デフォルトは `0`。

**注意: ランタイムで  `shape.radius()` が解決できないため、カスタムプロパティにパーセント値を使用しないでください。**

### Sass ミキシン

ミキシン | 説明
--- | ---
`radius($radius, $rtl-reflexive)` | 適当な角を丸めの半径を適用するためにその他のすべてのコンポーネントが使用するシェープ API。`$radius` には単一の値、もしくは、四隅の角の丸めの半径を指定する。`$rtl-reflexive` を true に設定すると RTL のときに反転される。デフォルトは `false`。

### Sass 関数

関数 | 説明
--- | ---
`resolve-radius($radius, $component-height)` | シェイプ分類 ― `large`、`medium`、`small` ― の解決された半径の値を返す。$radius が分類にないもののとき、この関数は有効な値であればその値を返す。有効な値とは数値かパーセント値です。`$radius` がパーセント値の場合、`$component-height` を指定する必要があります。
`flip-radius($radius)` | RTL コンテンツ内で半径の値を反転します。`$radius` は 2-4 の角の値のリスト。
`mask-radius($radius, $masked-corners)` | 半径の値、もしくは、半径の 2-4 の値のリストを指定し、`$masked-corners` に指定にしたがい、マスクされた 4 つの値のリストを返す。
`unpack-radius($radius)` | border-radius の省略値（すなわち、1個から3個の値のリスト）をアンパックする。4つの値が与えられたときはそのまま返す。

### 追加情報

#### 高さが固定されたコンポーネントのためのシェイプ

ボタンのような高さが固定されたコンポーネントにシェイプを適用するためのスタイルは次のようにします。

```scss
@use "@material/button";

@include shape.radius($radius, $component-height: button.$height);
```

ここで、`button.$height` は標準的なボタンの高さ、`$radius` はシェイプのサイズです。`shape.radius()` はコンポーネントの高さに基づきパーセント単位の値を絶対的な半径の値を解決します。

#### 動的な高さのコンポーネントのためのシェイプ

カードのような動的な高さのコンポーネントにシェイプを適用するためのスタイルは次のようにします。

```scss
@include shape.radius($radius);
```

ここで `$radius` は絶対的な値しか許されません。

#### 特殊な角をもつコンポーネントのためのシェイプ

ドロワーのような特殊な角をもつシェイプを適用するためのスタイルは次のようにします。

```scss
@include shape.radius(0 $radius $radius 0, $rtl-reflexive: true);
```

ここで右上と右下の角だけがカスタマイズできます。`$rtl-reflexive` を true に設定すれば `shape.radius()` は自動的に RTL コンテンツに基づき、半径の値を反転します。

#### コンポーネントのテーマ

カスタムシェイプをボタンコンポーネントに適用するにためのスタイルは次のようにします。

```scss
@use "@material/button";

.my-custom-button {
  @include button.shape-radius(50%);
}
```

この例では、上のスタイルはボタンに 50% 円形シェイプを適用します。また、絶対的な値（例： `8px`）を指定することもできます。

> シェイプ API は通常、各コンポーネントのミキシンを介して暗黙に使用されます。これによって、すべてのバリエーションの高さを設定し、該当する角に丸みに半径を適用します。
