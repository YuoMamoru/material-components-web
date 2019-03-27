<!--docs:
title: "Grid Lists"
layout: detail
section: components
excerpt: "An RTL-aware Material Design grid list component."
iconId: card
path: /catalog/grid-lists/
-->

## 重要 - 非推奨のお知らせ

既存の `MDCGridList` コンポーネントとスタイルは将来のリリースで削除されます。この機能のいくつかは代わりに [MDC Image List](../mdc-image-list) パッケージで利用できます。バグや機能の要求は `mdc-grid-list` パッケージでは受け付けなくなります。新たな機能や更新を受け取るために `mdc-image-list` パッケージに移行することを推奨します。

# Grid Lists

MDC Grid List はマテリアルデザイングリッドリスト仕様に準拠した RTL 対応の マテリアルデザイングリッドリストコンポーネントです。グリッドリストは均質なデータ、典型的には画像、に最も適しています。グリッド内の各項目は **タイル** と呼ばれます。タイルは画面サイズに応じて一貫した幅、高さ、余白を維持します。

## インストール

```
npm install @material/grid-list
```


## 使用法

基本的なグリッドリストは以下の構造をしています。

```html
<div class="mdc-grid-list">
  <ul class="mdc-grid-list__tiles">
    <li class="mdc-grid-tile">
      <div class="mdc-grid-tile__primary">
        <img class="mdc-grid-tile__primary-content" src="my-image.jpg" />
      </div>
      <span class="mdc-grid-tile__secondary">
        <span class="mdc-grid-tile__title">Title</span>
      </span>
    </li>
    <li class="mdc-grid-tile">
      <div class="mdc-grid-tile__primary">
        <img class="mdc-grid-tile__primary-content" src="my-image.jpg" />
      </div>
      <span class="mdc-grid-tile__secondary">
        <span class="mdc-grid-tile__title">Title</span>
      </span>
    </li>
  </ul>
</div>
```

上記のマークアップは以下のタイルによるグリッドリストを生成します。

- タイルの間隔は 4px
- 1x1 のアスペクト比
- アイコンのない 1 行のタイトルフッタ

あとは `<img class="mdc-grid-tile__primary-content" src="..."/>` の `src` にロードしたいコンテンツを置くだけです。ただし、タイルに指定したアスペクト比と同じアスペクト比の画像を置かないと、画像はゆがんでしまします。[img の場所で div を使う](#using-a-div-in-place-of-an-img) の節ではこのような場合の解決方法を提供しています。


### タイル幅の設定

タイル幅はデフォルトで 200px に設定されています。グリッドリストのデフォルト値を変更する方法は 3 つあります。

1. CSS 変数の使用

  ```css
  .mdc-grid-tile {
    --mdc-grid-list-tile-width: 300px;
  }
  ```

2. SCSS 変数の上書き

  次のように scss 変数を上書きできます。

  ```scss
  $mdc-grid-list-tile-width: 300px;
  @import "@material/grid-list/mdc-grid-list";
  ```

3. タイルに独自のスタイルを追加

  ```html
  <style>
    .my-grid-list .mdc-grid-tile {
      width : 300px;
    }
  </style>
  <div class="mdc-grid-list my-grid-list">
    <ul class="mdc-grid-list__tiles">
      <li class="mdc-grid-tile"></li>
      ...
    </ul>
  </div>
  ```

### タイルの余白の変更

グリッドリストのタイルは `mdc-grid-list--tile-gutter-1` 修飾クラスを加えると 4px の代わりに 1px の余白になります。

```html
<div class="mdc-grid-list mdc-grid-list--tile-gutter-1">
  <ul class="mdc-grid-list__tiles">
  ...
  </ul>
</div>
```

### 画像だけのタイル

グリッドリストは画像だけのタイルをサポートしています。`mdc-grid-tile__secondary` を削除して画像だけのグリッドリストを作ることができます。

```html
<div class="mdc-grid-list mdc-grid-list--tile-gutter-1">
  <ul class="mdc-grid-list__tiles">
    <li class="mdc-grid-tile">
      <div class="mdc-grid-tile__primary">
        <img class="mdc-grid-tile__primary-content" src="images/1-1.jpg" />
      </div>
    </li>
  </ul>
</div>
```

### タイトルヘッダ

グリッドリストはタイトルヘッダをサポートしています。`mdc-grid-list--header-caption` 修飾クラスを追加するだけでタイトルフッタをタイトルヘッダに変えることができます。

```html
<div class="mdc-grid-list mdc-grid-list--header-caption">
  <ul class="mdc-grid-list__tiles">
    ...
  </ul>
</div>
```

### 副次的コンテンツ（説明文）に補助的な文言を追加

グリッドリストはデフォルトで 1 行の説明文を付けることができます。必要に応じて `mdc-grid-list--twoline-caption` 修飾クラスと追加のマークアップを加ることにより、補助的な文言の追加行を加えることができます。

```html
<div class="mdc-grid-list mdc-grid-list--twoline-caption">
  <ul class="mdc-grid-list__tiles">
    <li class="mdc-grid-tile">
      <div class="mdc-grid-tile__primary">
        <img class="mdc-grid-tile__primary-content" src="my-image.jpg" />
      </div>
      <span class="mdc-grid-tile__secondary">
        <span class="mdc-grid-tile__title">Title</span>
        <span class="mdc-grid-tile__support-text">Support text</span>
      </span>
    </li>
  </ul>
</div>
```

### 副次的なコンテンツ（説明文）にアイコンを追加

`mdc-grid-list--with-icon-align-start` もしくは `mdc-grid-list--with-icon-align-end` を追加し、マークアップを変えると、アイコンを説明文に追加できます。

```html
<div class="mdc-grid-list mdc-grid-list--with-icon-align-start">
  <ul class="mdc-grid-list__tiles">
    <li class="mdc-grid-tile">
      <div class="mdc-grid-tile__primary">
        <img class="mdc-grid-tile__primary-content" src="my-image.jpg" />
      </div>
      <span class="mdc-grid-tile__secondary">
        <i class="mdc-grid-tile__icon material-icons">star_border</i>
        <span class="mdc-grid-tile__title">Title</span>
      </span>
    </li>
  </ul>
</div>
```

### タイルのアスペクト比の変更

グリッドリストはマテリアルガイドラインで推奨されているすべてのアスペクト比に対応しています。

- 1x1
- 16x9
- 2x3
- 3x2
- 4x3
- 3x4

グリッドリストにこれらのアスペクト比を適用するには修飾クラス `mdc-grid-list--tile-aspect-$ASPECT_RATIO` をを使います。単純に `$ASPECT_RATIO` を事前に定義された比率のいずれかに置き換えてください。

```html
<!-- 16x9 のタイルの例 -->
<div class="mdc-grid-list mdc-grid-list--tile-aspect-16x9">
  <ul class="mdc-grid-list__tiles">
  ...
  </ul>
</div>
```

前の節で指摘したとおり、タイルに指定したアスペクト比と同じアスペクト比の画像でない場合、画像はゆがんでしまします。[img の場所で div を使う](#using-a-div-in-place-of-an-img) の節ではこのような場合の解決方法を提供しています。

### <a name="using-a-div-in-place-of-an-img"></a>img の場所で div を使う

すべての画像が同じアスペクト比であることを保証できない場合には `img` のマークアップの代わりに `div` を使うことができます。これはタイルを隠すために画像をリサイズし、画像の端を切り取って中心部分を表示します。

```html
<style>
  .my-tile-image {
    background-image: url(my-image.jpg);
  }
</style>

<div class="mdc-grid-list">
  <ul class="mdc-grid-list__tiles">
    <li class="mdc-grid-tile">
      <div class="mdc-grid-tile__primary">
        <div class="mdc-grid-tile__primary-content my-tile-image"></div>
      </div>
      <span class="mdc-grid-tile__secondary">
        <span class="mdc-grid-tile__title">Title</span>
      </span>
    </li>
  </ul>
</div>
```

ただし、この方法はマークアップの意味が薄れるので、私たちはデフォルトではこの方法を使いません。

### RTL のサポート

`mdc-grid-list` は自動的に RTL 対応がなされており、その要素もしくはその祖先の要素に `dir="rtl"` があれば要素は配置しなおされます。

### テーマ

`mdc-grid-list` はテーマをサポートしています。`mdc-grid-tile__primary` は自身の背景色にテーマのバックグランドカラーを使います。`mdc-grid-tile__secondary` は自身の背景色にテーマのプライマリカラーを使い、自身のテキストの色にはテーマの `on-primary` を使います。

### `MDCGridListFoundation`

メソッド | 説明
--- | ---
`alignCenter() => void` | 親コンテナ内で水平方向の中央揃えにする。

### `MDCGridListAdapter`

メソッド | 説明
--- | ---
`getOffsetWidth() => number` | ルート要素 `mdc-grid-list` の offsetWidth を取得する。
`getNumberOfTiles() => number` | グリッドリストに含まれる mdc-grid-tile 要素の数を取得する。
`getOffsetWidthForTileAtIndex(index: number) => number` | 指定した index にある `mdc-grid-tile` の offsetWidth を取得する。
`setStyleForTilesElement(property: string, value: number) => void` | `mdc-grid-list__tiles` スタイルプロパティに指定した値を設定する。
`registerResizeHandler(handler: EventListener) => void` | 外観（もしくはビューポート）をリサイズしたときに呼ばれるイベントハンドラーを登録する。デフォルトの実装では handler をウィンドウの `resize()` イベントのリスナーに追加している。
`deregisterResizeHandler(handler: EventListener) => void` | 外観（もしくはビューポート）をリサイズしたときに呼ばれるイベントハンドラーの登録を解除する。デフォルトの実装では handler をウィンドウの `resize()` イベントのリスナーから削除している。
