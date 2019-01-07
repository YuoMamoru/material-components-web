<!--docs:
title: "Layout Grid"
layout: detail
section: components
excerpt: "A CSS only responsive grid."
iconId: responsive_layout
path: /catalog/layout-grid/
-->

# Layout Grid

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/layout-grid">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/layout.png" width="256" alt="Layout grid screenshot">
  </a>
</div>-->

マテリアルデザインのレスポンシブ UI は列可変のグリッドレイアウトに基づいています。この UI はデスクトップでは 12 列、タブレットでは 8 列、スマートフォンでは 4 列持っています。


## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/layout/responsive-ui.html#responsive-ui-grid">マテリアルデザインガイドライン: レイアウトグリッド</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/layout-grid">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/layout-grid
```

## 使用法

### HTML 構造

```html
<div class="mdc-layout-grid">
  <div class="mdc-layout-grid__inner">
    <div class="mdc-layout-grid__cell"></div>
    <div class="mdc-layout-grid__cell"></div>
    <div class="mdc-layout-grid__cell"></div>
  </div>
</div>
```

#### ネストした grid

コンテンツが単一のレイアウトグリッドでは表現できない特別な構造を必要としているとき、それぞれの中にレイアウトグリッドをネストさせることができます。レイアウトグリッドをネストするには `mdc-layout-grid__cell` の中にネストした `mdc-layout-grid__cell` の周りを囲むために新たな `mdc-layout-grid__inner` を追加します。

ネストしたレイアウトグリッドはネストしていないときと同じようにふるまいます。例えば、デスクトップでは 12、タブレットでは 8、スマートフォンでは 4 つの列を持ちます。親と **同じ幅の境界** を使用し、マージンは別のセル内にあるため再導入されません。

ただし、マテリアルデザインガイドラインでは過度に複雑な UX であるので深くネストすることは推奨されていません。

```html
<div class="mdc-layout-grid">
  <div class="mdc-layout-grid__inner">
    <div class="mdc-layout-grid__cell">
      <div class="mdc-layout-grid__inner">
        <div class="mdc-layout-grid__cell"><span>Second level</span></div>
        <div class="mdc-layout-grid__cell"><span>Second level</span></div>
      </div>
    </div>
    <div class="mdc-layout-grid__cell">First level</div>
    <div class="mdc-layout-grid__cell">First level</div>
  </div>
</div>
```

### スタイル

```scss
@import "@material/layout-grid/mdc-layout-grid";
```

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-layout-grid` | 必須。レイアウトグリッド要素に付ける。
`mdc-layout-grid__inner` | 必須。グリッドのセルをラップするために使う。
`mdc-layout-grid__cell` | 必須。グリッドのセルにつける。
`mdc-layout-grid__cell--span-<NUMBER_OF_COLUMNS>` | オプション。セルのスパンの列数を指定する。
`mdc-layout-grid__cell--span-<NUMBER_OF_COLUMNS>-<TYPE_OF_DEVICE>` | オプション。デバイス（desktop、tablet、phone）ごとのセルのスパンの列数を指定する。
`mdc-layout-grid__cell--order-<INDEX>` | オプション。セルの並び順を指定する。
`mdc-layout-grid__cell--align-<POSITION>` | オプション。セルの配置を指定する。
`mdc-layout-grid--fixed-column-width` | オプション。グリッドが固定の列幅をもつときに指定する。
`mdc-layout-grid--align-<GRID_POSITION>` | オプション。グリッド全体の配置を指定する。

#### `mdc-layout-grid__cell--span-<NUMBER_OF_COLUMNS>`

`mdc-layout-grid__cell--span-{columns}` の形式のスパンクラスの一つを指定することにより、セルのスパンを設定します。ここで、`{columns}` は 1 から 12 までの整数です。現在のスクリーンサイズで利用可能な列数より大きなスパンサイズを指定したときは、スクリーンサイズで有効な列数と同じスパンサイズが選ばれたものとして振舞います。スパンクラスが設定されていないときは、`mdc-layout-grid__cell` はデフォルトのスパンサイズである 4 列であるとして扱われます。


#### `mdc-layout-grid__cell--span-<NUMBER_OF_COLUMNS>-<TYPE_OF_DEVICE>`

`mdc-layout-grid__cell--span-<NUMBER_OF_COLUMNS>` と同じですが、特定のデバイス（`desktop`, `tablet` or `phone`）のためのものです。


#### `mdc-layout-grid__cell--order-<INDEX>`

デフォルトでは項目はソースの順番で並びます。しかし、`mdc-layout-grid__cell--order-<INDEX>` クラスを使うことにより順番を並び替えることができます。ここで、`<INDEX>` は 1 から 12 までの整数です。スクリーンリーダやその他のツールではソースの順番にしたがうことが多いので、アクセシビリティに影響があることを覚えておいてください。

#### `mdc-layout-grid__cell--align-<POSITION>`

デフォルトでは、項目は対応する行の高さまで伸びるように定義されています。`mdc-layout-grid__cell--align-<POSITION>` 整列クラスの一つを使うことにより、異なった動作に変更することができます。ここで、`<POSITION>` は `top`、`middle`、`bottom` のいずれか一つです。


#### `mdc-layout-grid--fixed-column-width`

`mdc-layout-grid--fixed-column-width` 修飾クラスを使うと各列に特定の幅を指定することができます。列幅は sass マップ `$mdc-layout-grid-column-width` もしくは CSS カスタムプロパティ `--mdc-layout-grid-column-width-{screen_size}` を通じて指定することができます。列幅はデフォルトですべてのデバイスで 72px が設定されています。


#### `mdc-layout-grid--align-<GRID_POSITION>`

グリッドはデフォルトで中央揃えになっています。この挙動を変えるために `mdc-layout-grid--align-left` もしくは `mdc-layout-grid--align-right` 修飾クラスを追加することができます。これらの修飾クラスはグリッドのコンテナが既にいっぱいになっているときは作用しません。

### Sass ミキシン

ミキシン | 説明
--- | ---
`mdc-layout-grid($size, $margin, $max-width)` | 特定のデバイス上でのグリッドコンテナのための CSS を生成する。
`mdc-layout-grid-inner($size, $margin, $gutter)` | 特定のデバイス上でのグリッドセルのラッパーのための CSS を生成する。
`mdc-layout-grid-cell($size, $default-span, $gutter)` | 特定のデバイス上でのグリッドセルのための CSS を生成する。
`mdc-layout-grid-fixed-column-width($size, $margin, $gutter, $column-width)` | 特定のデバイス上でのコンテナを固定の列幅にする CSS を生成する。
`mdc-layout-grid-cell-order($order)` | グリッド内のセルを並び替える。
`mdc-layout-grid-cell-align($position)` | グリッド内のセルの垂直方向の整列を行う。


#### `mdc-layout-grid($size, $margin, $max-width)`

特定のデバイス上でのグリッドコンテナのための CSS を生成します。このミキシンは 3 つのパラメーターを取ります。

- `$size`: 対象とするプラットフォーム。`desktop`、`tablet`、`phone`のいずれか。
- `$margin`: グリッドのマージンの大きさ。
- `$max-width`（オプション）: グリッドの幅の最大値。Point space stops being distributed by the columns at the grid.

#### `mdc-layout-grid-inner($size, $margin, $max-width)`

特定のデバイス上でのグリッドセルのラッパーのための CSS を生成します。このミキシンは 3 つのパラメーターを取ります。
- `$size`: 対象とするプラットフォーム。`desktop`、`tablet`、`phone`のいずれか。
- `$margin`: グリッドのマージンの大きさ。
- `$gutter`: セルの間の幅の大きさ。

#### `mdc-layout-grid-cell($size, $default-span, $gutter)`

特定のデバイス上でのグリッドセルのための CSS を生成します。このミキシンは 3 つのパラメーターを取ります。
- `$size`: 対象とするプラットフォーム。`desktop`、`tablet`、`phone`のいずれか。
- `$default-span`（オプション、初期値: 4）: このセルの列スパンの数（1 から 12）。
- `$gutter`:セルの間の幅の大きさ。親グリッドと同じ値を指定する。

> 引数の一つとして size が渡されても、`media-query` ルールは適用されないことに注意してください。これは実行時にマージンとセル間の幅を上書きする正しい CSS カスタムプロパティを使用するように設定されているからです（詳細は [マージンとセル間の幅](#margins-and-gutters) の節を参照）（訳注: 「マージンとセル間の幅（Margins and gutters）」の節は削除されており、現在このドキュメントにはありません）。

#### `mdc-layout-grid-fixed-column-width($size, $margin, $gutter, $column-width)`

特定のデバイス上でのコンテナを固定の列幅にする CSS を生成する。このミキシンは 4 つのパラメーターを取ります。
- `$size`: 対象とするプラットフォーム。`desktop`、`tablet`、`phone`のいずれか。
- `$margin`: グリッドのマージンの大きさ。
- `$gutter`: セルの間の幅の大きさ。
- `$column-width`: グリッド内のカラムの幅。

### Sass 変数

変数 | 説明
--- | ---
`mdc-layout-grid-breakpoints` | ブレークポイントの幅が設定されている SASS の Map。
`mdc-layout-grid-columns` | カラム数が設定されている SASS の Map。
`mdc-layout-grid-default-margin` | グリッドの端と最初のセルの端との間隔が設定されている SASS の Map。
`mdc-layout-grid-default-gutter` | 隣接したセルの間隔が設定されている SASS の Map。
`mdc-layout-grid-column-width` | グリッドの列幅が設定されている SASS の Map。
`mdc-layout-grid-default-column-span` | セルのデフォルトのスパンが設定されている。
`mdc-layout-grid-max-width` | レイアウトグリッドの幅の最大値を制限している。


### CSS カスタムプロパティ

CSS カスタムプロパティ | 説明
--- | ---
`mdc-layout-grid-margin-<TYPE_OF_DEVICE>` | グリッドの端と最初のセルの端の間隔を指定する。
`mdc-layout-grid-gutter-<TYPE_OF_DEVICE>` | 隣接するセルの間隔を指定する。
