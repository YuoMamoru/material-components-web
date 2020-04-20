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

シェイプシステムではコンポーネントは小さいもの、中程度のもの、大きいものに分類されます。以下の sass 変数を上書きすることにより、（角の丸い）シェイプはそれぞれの分類に適用されます。例えば、`$medium-radius` 変数を上書きすると中程度の分類に属するすべてのコンポーネントに対して適用されます。

変数 | 説明
--- | ---
`$small-component-radius` | 小さいコンポーネントの角の丸めの大きさ。デフォルトは `4px`。
`$medium-component-radius` | 中程度のコンポーネントの角の丸めの大きさ。デフォルトは `4px`。
`$large-component-radius` | 大きいコンポーネントの角の丸めの大きさ。デフォルトは `0`。

コンポーネントの分類方法について学ぶには [Material Design guidelines: シェイプ](https://material.io/go/design-shape) を参照してください。

### Sass ミキシン

ミキシン | 説明
--- | ---
`radius($radius, $rtl-reflexive)` | 適当な角を丸めの半径を適用するためにその他のすべてのコンポーネントが使用するシェープ API。`$radius` には単一の値、もしくは、四隅の角の丸めの半径を指定する。`$rtl-reflexive` を true に設定すると RTL のときに反転される。デフォルトは `false`。

> パーセント単位の値を絶対的な半径の大きさにするには `resolve-percentage-radius` sass 関数を使ってください。

### Sass 関数

関数 | 説明
--- | ---
`flip-radius($radius)` | RTL コンテンツ内で半径の値を反転します。`$radius` は 2-4 の角の値のリスト。
`resolve-percentage-radius($component-height, $radius)` | コンポーネントの高さをもとに半径の絶対的な値を計算する。高さが固定されたコンポーネントでのみ使用する。
`mask-radius($radius, $masked-corners)` | 半径の値、もしくは、半径の 2-4 の値のリストを指定し、`$masked-corners` に指定にしたがい、マスクされた 4 つの値のリストを返す。
`prop-value($radius)` | シェイプ分類 - `large`、`medium` または `small` - の`$radius` の値を返す。もしくは、有効であれば `$radius` 自身を返す。`$radius` は単一の値、もしくは最大 4 津の値のリスト。

### 追加情報

#### 高さが固定されたコンポーネントのためのシェイプ

ボタンのような高さが固定されたコンポーネントにシェイプを適用するためのスタイルは次のようにします。

```scss
@use "@material/button";

@include shape.radius(shape.resolve-percentage-radius(button.$height, $radius));
```

ここで、`button.$height` は標準的なボタンの高さ、`$radius` はシェイプのサイズです。`resolve-percentage-radius` 関数はコンポーネントの高さに基づきパーセント単位の値を絶対的な `$radius` の値にsるために使われます。

#### 動的な高さのコンポーネントのためのシェイプ

カードのような動的な高さのコンポーネントにシェイプを適用するためのスタイルは次のようにします。

```scss
@include shape.radius($radius);
```

ここで、`$radius` は絶対的な値しか許されません。

#### 特殊な角をもつコンポーネントのためのシェイプ

ドロワーのような特殊な角をもつシェイプを適用するためのスタイルは次のようにします。

```scss
@include shape.radius(0 $radius $radius 0, $rtl-reflexive: true);
```

ここで、右上と右下の角だけがカスタマイズでき、`$rtl-reflexive` を true に設定すれば自動的に RTL コンテンツに基づき、半径の値が反転されます。

#### コンポーネントのテーマ

カスタムシェイプをボタンコンポーネントインスタンスに適用するにためのスタイルは次のようにします。

```scss
@use "@material/button";

.my-custom-button {
  @include button.shape-radius(50%);
}
```

この例では、上のスタイルはボタンに 50%（円形）シェイプを適用します。また、絶対的な値（例： `8px`）を指定することもできます。

> シェイプ API はそれぞれのコンポーネントのすべてのバリエーションの角に丸みを適用することのできるミキシンを介して暗黙に使用されます。
