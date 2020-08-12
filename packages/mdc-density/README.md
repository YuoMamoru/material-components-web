<!--docs:
title: "Density"
layout: detail
section: components
excerpt: "Density subsystem provides adaptive layout to components."
path: /catalog/density/
-->

# Density

Density サブシステムはコンポーネントに適応性のあるレイアウトを提供します。マテリアルデザインはデフォルトでは低密度空間を使いますが、ユーザーエクスペリエンスを向上させるときには高密度空間を提供します。高密度コンポーネントはユーザーが大量の情報をより管理しやすい方法で処理し、操作を実行できるようにします。リスト、表、そして大きなフォームは密度をあげることにより利益を受けるコンポーネントです。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/design/layout/applying-density.html">マテリアルデザインガイドライン: 密度の適用</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://glitch.com/~material-density" target="_blank">デモ: Glitch</a>
  </li>
</ul>

## インストール

```
npm install @material/density
```

> 注意: 直接、`@material/density` に依存する必要はなく、デンシティ Sass ミキシンを代わりに提供しているコンポーネントを使います。

## 基本的な使用法

ボタンコンポーネントインスタンスにデンシティを摘要したスタイルにするには次のようにします。

```scss
@use "@material/button";

.my-custom-button {
  // ボタンの密度スケールを `-3`、すなわち `24px` の高さにする
  @include button.density(-3);
}
```

これはボタンコンポーネントのインスタンスに `-3`（高密度）を摘要します。

> 適切なコンポーネントの高さに設定に処理を行う各コンポーネントのミキシンを通じて Density API を間接的に使うことになります。

デンシティ Sass ミキシンを提供するコンポーネントは以下の通りです。

  * [Button](../mdc-button/README.md#sass-mixins)
  * [Checkbox](../mdc-checkbox/README.md#sass-mixins)
  * [Chip](../mdc-chips/README.md#sass-mixins)
  * [Data Table](../mdc-data-table/README.md#sass-mixins)
  * [Icon Button](../mdc-icon-button/README.md#sass-mixins)
  * [List](../mdc-list/README.md#sass-mixins)
  * [Radio](../mdc-radio/README.md#sass-mixins)
  * [Switch](../mdc-switch/README.md#sass-mixins)
  * [Tab Bar](../mdc-tab-bar/README.md#sass-mixins)
  * [Text Field](../mdc-textfield/README.md#sass-mixins)

## デンシティミキシン

デンシティをサポートするコンポーネントはコンポーネントの密度をカスタマイズする Sass ミキシンを提供します。各デンシティミキシンは密度スケールの数値、例えば 0（デフォルト）もしくは -1（高密度）、を引数に取ります。 

現在、デンシティシステムでは高密度にカスタマイズするために負の数値のみが使えます。より低い密度スケールは高いコンポーネント密度になります。実際の密度スケールの範囲はコンポーネントによります。スケールの数値がコンポーネントのデンシティミキシンのサポートしていない値のときは、コンパイラはビルド時にエラーを報告します。

コンポーネントの高さまたは大きさは以下の式で計算されます。

```scss
@use "@material/button";
@use "@material/density";

$height: button.$height + density.$interval * $density-scale
/// @example 36px + 4px * (-3) => 24px
```

密度間隔は視覚的な一貫性のために 4px に設定されます。

コンポーネントの高さを独自に摘要するのではなく、提供されたデンシティミキシンを通じて密度をカスタマイズすることが推奨されます。

注意: デンシティミキシンを摘要するとタッチターゲットは自動的に無効になります。これは高密度コンポーネントはオプションで有効にすべきであり、したがって同じデフォルトアクセサビリティが必要とされるわけではないためです。

## コンポーネントのバリエーション

異なるバリエーションをもつコンポーネントではそれぞれ独自のデンシティミキシンを持ちます。

例えば、Tab Bar には2つのデンシティミキシンがあります。

  * `tab-bar.density()`: 標準のタブバーのデンシティミキシン。
  * `tab-bar.stacked-density()`: ラベルのうえにアイコンのあるタブバーのデンシティミキシン。

同様に、テキスト欄はそれぞれのバリエーションにもとづいた3つの異るデンシティミキシンを提供しています。

## ネストされたコンポーネント

他のコンポーネントの内部に描画するマテリアルコンポーネントはそれぞれ独自の密度スケールを設定する必要があります。親コンポーネントへのデンシティミキシンの適用により、子要素に密度を自動的に適用されるわけではありません。

例えば、データテーブルへの密度の適用により、自動的に行のチェックボックスに密度が適用されることはありません。明示的に子要素に対して密度スケールを設定しなくてはなりません。これにより、クライアントはレイアウトを完全に制御することができます。

## スタイルのカスタマイズ

このパッケージは他のコンポーネントのデンシティミキシンのためのユーティリティとして使われます。このパッケージにより提供されるカスタマイズは開発者が直接的に利用することを想定したものではなく、代わりにコンポーネントのデンシティミキシンを使ってください。

### Sass 変数

変数 | 説明
--- | ---
`$interval` | 各密度スケール間の密度間隔。この間隔はベースラインコンポーネントのたかさにもとづき、密度の高さを計算するために密度スケールの番号で使われます。
`$minimum-scale` | デンシティシステムによりサポートする密度スケールの最小値。この大きさは常に最高の密度スケールにマッピングされる。
`$maximum-scale` | デンシティシステムによりサポートする密度スケールの最大値。この大きさは常に最小の密度スケールにマッピングされる。
`$supported-scales` | 密度リテラルが使用されるときに差ボールする密度スケール（例えば `minimum`）。

### Sass 関数

関数 | 説明
--- | ---
`prop-value($density-config, $density-scale, $property-name)` | 与えられた密度設定と密度スケールにもとづき、コンポーネントのプロパティ値を返す。
