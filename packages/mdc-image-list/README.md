<!--docs:
title: "Image List"
layout: detail
section: components
excerpt: "An RTL-aware Material Design image list component."
iconId: card
path: /catalog/image-lists/
-->

# Image List

MDC Image List は RTL 対応のマテリアルデザインイメージリストコンポーネントを提供します。イメージリストはいくつかの項目からできており、それぞれイメージとオプションとなるサポートコンテンツ（例えばテキストラベル）を含んでいます。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-image-list">マテリアルデザインガイドライン: イメージリスト</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/image-list">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/image-list
```

## 基本的な使用法

### HTML 構造

標準的なイメージリストの HTML 構造は次の通りです。

```html
<ul class="mdc-image-list my-image-list">
  <li class="mdc-image-list__item">
    <div class="mdc-image-list__image-aspect-container">
      <img class="mdc-image-list__image" src="...">
    </div>
    <div class="mdc-image-list__supporting">
      <span class="mdc-image-list__label">Text label</span>
    </div>
  </li>
  ...
</ul>
```

### スタイル

```scss
@use "@material/image-list/mdc-image-list";
```

上記の HTML 構造を `standard-columns` ミキシンの呼び出しと組み合わせて、1行に何列表示するかを設定できます。

```scss
@use "@material/image-list";

.my-image-list {
  @include image-list.standard-columns(5);
}
```

標準的なイメージリスト内の画像はデフォルトで 1:1 のアスペクト比が適用されます。これは以下の記述の通り、`aspect` ミキシンを使うことにより上書きできます。

## バリエーション

### 石積イメージリスト

石積イメージリストは、[CSS Columns](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Columns) を使って、いくつかの列内で垂直方向に整列した画像を提供します。このレイアウトではアスペクト比の任意の組み合わせが可能です。

```html
<ul class="mdc-image-list mdc-image-list--masonry my-masonry-image-list">
  <li class="mdc-image-list__item">
    <img class="mdc-image-list__image" src="...">
    <div class="mdc-image-list__supporting">
      <span class="mdc-image-list__label">Text label</span>
    </div>
  </li>
  ...
</ul>
```

> **注意:** 石積イメージリストの項目は `mdc-image-list__image-aspect-container` 要素を含んで <em>いません</em>。これはリスト内の画像が共通のアスペクト比で固定されていることを想定していないからです。

`mdc-image-list-masonry-columns` ミキシンの呼び出しと組み合わせて、何列表示するのか設定することができます。

```scss
.my-masonry-image-list {
  @include image-list.masonry-columns(5);
}
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-image-list` | 必須。イメージリストのルート要素であることを示す。
`mdc-image-list--masonry` | オプション。イメージリストが石積型であることを示す。
`mdc-image-list--with-text-protection` | オプション。サポートコンテンツが各イメージを覆うように配置される（各画像の下に分けて配置されるのではなく）ことを示す。
`mdc-image-list__item` | 必須。イメージリスト内の各項目であることを示す。
`mdc-image-list__image-aspect-container` | オプション。各項目の画像要素の親のアスペクト比を担当する。画像が既に適切なアスペクト比になっているならこの要素は完全に省略できる。
`mdc-image-list__image` | 必須。各項目の画像を表す。
`mdc-image-list__supporting` | オプション。イメージリストがテキストラベルを含んでいるとき、サポートテキストラベルを含んだ各項目の内の領域であることを示す。
`mdc-image-list__label` | オプション。イメージリストがテキストラベルを含んでいるとき、各項目のテキストラベルであることを示す。

### Sass ミキシン

ミキシン | 説明
--- | ---
`aspect($width-height-ratio)` | イメージリスト内のコンテナ要素のアスペクト比を与えられた比率に設定する。1であれば 1:1 にし、1よりも大きくすれば横長に、1より小さくすれば縦長になる。
`shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさにイメージリストの項目の角の丸めを設定する。`$rtl-reflexive` を true にすれば RTL コンテキスト内で反映の値が反転する。デフォルトは false。
`standard-columns($column-count, $gutter-size)` | 標準的なイメージリストを与えられた列数で表示するよう設定する。`$gutter-size` はオプションで、項目間のスペースのデフォルトの大きさを上書きする。
`masonry-columns($column-count, $gutter-size)` | 石積イメージリストを与えられた列数で表示するよう設定する。`$gutter-size` はオプションで、項目間のスペースのデフォルトの大きさを上書きする。

> **注意:** `*-columns` ミキシンは一つだけをイメージリストで指定できます。使用するバリエーションに応じたミキシンを使ってください。

### 追加情報

#### 幅の制限

`*-columns` ミキシンはイメージリスト全体の幅に応じて広げたり縮小させたりします。配置によっては、ビューポートの幅に直接関連し、画像が実際に表示される大きさと比べて非常に大きくすることができます。これはイメージリスト上で `min-width`、`width` や `max-width` のいずれかを使うことで制限できます。

```scss
@use "@material/image-list";

.my-image-list {
  @include image-list.standard-columns(5);

  max-width: 960px;
}
```

> **注意:** 指定した幅はリスト <em>全体</em> に適用されることに注意し、余白も考慮してください。

#### ブレークポイント間での列数の変更

列数を変更するのに必要なのはスタイルだけなので、異なるビューポートの大きさで異なる列数を指定するのは容易です。

```scss
.my-image-list {
  @include image-list.standard-columns(5);
}

@media (max-width: 599px) {
  .my-image-list {
    @include image-list.standard-columns(3);
  }
}
```

#### アスペクト比を強制するために img の替わりに div を使用

> **注意:** このアドバイスはイメージが共通のアスペクト比を共有しない石積イメージリストには適用されません。

イメージリスト内の画像は一般的に `img` 要素が使用されます。しかし、素材がリスト項目に指定する同じアスペクトでない場合、表示が崩れてしまいます。このようなときには `img` 要素の代わりに `div` 要素を使うことができ、各要素の `background-image` に画像を指定します。

> **注意:** 画像をブラウザに配信する前に適切な大きさにすることは、MDC Image List を使う上で最も効率的で理想的な手法です。利便性のために `div` による代替が提供されています。この代替手法を使用するなら、各項目の画像の周りに `mdc-image-list__image-aspect-container` 要素も含めるようにしてください。
