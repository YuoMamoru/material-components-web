<!--docs:
title: "Linear Progress"
layout: detail
section: components
excerpt: "Material Design-styled linear progress indicators."
iconId: progress_linear
path: /catalog/linear-progress/
-->

# Linear Progress

<!--<div class="article__asset">
  <a class="article__asset-link"
      href="https://material-components.github.io/material-components-web-catalog/#/component/linear-progress-indicator">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/linear-progress.png" width="586" alt="Linear progress screenshot">
  </a>
</div>-->

MDC Linear Progress コンポーネントは [マテリアルデザインプログレスと動作の要件](https://material.io/go/design-progress-indicators) に準拠したリニアプログレスインジケーターです。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-progress-indicators">ガイドライン</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/linear-progress-indicator">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/linear-progress
```

## 基本的な使用法

### HTML 構造

```html
<div role="progressbar" class="mdc-linear-progress" aria-label="Example Progress Bar" aria-valuemin="0" aria-valuemax="1" aria-valuenow="0">
  <div class="mdc-linear-progress__buffer">
    <div class="mdc-linear-progress__buffer-bar"></div>
    <div class="mdc-linear-progress__buffer-dots"></div>
  </div>
  <div class="mdc-linear-progress__bar mdc-linear-progress__primary-bar">
    <span class="mdc-linear-progress__bar-inner"></span>
  </div>
  <div class="mdc-linear-progress__bar mdc-linear-progress__secondary-bar">
    <span class="mdc-linear-progress__bar-inner"></span>
  </div>
</div>
```

### アクセシビリティ

プログレスバーは [WAI-ARIA プログレスバー仕様](https://www.w3.org/TR/wai-aria/#progressbar) に準拠しています。プログレスバーのサポートしている ARIA 属性は以下の通りです。

| 属性 | 説明 |
| --------- | ----------- |
| `aria-label` | どのようにプログレスバーをユーザーに通知すべきかを示すラベル。 |
| `aria-valuemin` | プログレスバーの最小数値で、常に `0`。 |
| `aria-valuemax` | プログレスバーの最大数値で、常に `1`。 |
| `aria-valuenow` | 主たるプログレスバーの進行状況を示す `aria-valuemin` と `aria-valuemax` の間の数値。この属性は不定なプログレスバーでは削除される。 |

`aria-label` と `aria-valuemin`、`aria-valuemax` は静的な値で、HTML で指定する必要があることに注意してください。`aria-valuenow` は、対象のプログレスバーで進行値が更新された際に、ファンデーションによって動的に更新されます。

### スタイル
```scss
@use "@material/linear-progress";

@include linear-progress.core-styles;
```

### JavaScript のインスタンス化

```js
import { MDCLinearProgress } from '@material/linear-progress';

const linearProgress = new MDCLinearProgress(document.querySelector('.mdc-linear-progress'));
```

> JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

### CSS 修飾子

提供される修飾子は以下の通りです。

| クラス                | 説明                                                    |
| --------------------- | ------------------------------------------------------- |
| `mdc-linear-progress--indeterminate`   | リニアプログレスインジケーターを不定状態にする。 |
| `mdc-linear-progress--reversed`  | リニアプログレスインジケーターの向きを反転する。 |
| `mdc-linear-progress--closed`  | リニアプログラスインジケーターを隠す。 |

### Sass ミキシン

ミキシン | 説明
--- | ---
`bar-color($color)` | プログレスバーの色を設定する。
`buffer-color($color)` | バッファーバーとドットの色を設定する。

### ファンデーションクラスの使用

MDC リニアプログレスは外部フレームワークや外部ライブラリとコンポーネントを統合するために使用可能な `MDCLinearProgressFoundation` を同梱しています。すべてのファンデーションクラスと同様に、アダプターオブジェクトを指定しなくてはなりません。リニアプログレスのアダプターは適切なシグネチャで以下の関数を提供します。

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeAttribute(attributeName: string) => void` | ルート要素から指定された属性を削除する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `hasClass(className: string) => boolean` | ルート要素が与えられたクラスを持っているかどうかを表す真偽値を返す。 |
| `forceLayout() => void` | ルート要素のレイアウトを強制的に設定する。これは、アニメーションを正しく再起動するために必要。 |
| `setAttribute(attributeName: string, value: string) => void` | ルート要素に指定した属性を設定する。 |
| `setBufferBarStyle(styleProperty: string, value: string) => void` | バッファーバー上のインラインスタイルを設定する。 |
| `setPrimaryBarStyle(styleProperty: string, value: string) => void` | プライマリバー上のインラインスタイルを設定する。 |

### MDCLinearProgressFoundation API

MDC リニアプログレスファンデーションは以下のメソッドを公開しています。

| メソッド | 説明 |
| --- | --- |
| `setDeterminate(value: boolean) => void` | コンポーネントを確定状態と不定状態を切り替える。 |
| `setProgress(value: number) => void` | ブログレスバーに値を設定する。値は [0, 1] の間でなくてはならない。 |
| `setBuffer(value: number) => void` | バッファーバーに値を設定する。値は [0, 1] の間でなくてはならない。 |
| `setReverse(value: boolean) => void` | リニアプログレスのインジケーターの方向を反転させる。 |
| `open() => void` | コンポーネントを開いた状態にする。 |
| `close() => void` | コンポーネントを閉じた状態にする。 |

### MDCLinearProgress API

MDC リニアプログレスは以下のメソッドを公開しています。

| メソッド | 説明 |
| --- | --- |
| `set determinate(value: boolean) => void` | コンポーネントを確定状態と不定状態を切り替える。 |
| `set progress(value: number) => void` | ブログレスバーに値を設定する。値は [0, 1] の間でなくてはならない。 |
| `set buffer(value: number) => void` | バッファーバーに値を設定する。値は [0, 1] の間でなくてはならない。 |
| `set reverse(value: boolean) => void` | リニアプログレスのインジケーターの方向を反転させる。 |
| `open() => void` | コンポーネントを開いた状態にする。 |
| `close() => void` | コンポーネントを閉じた状態にする。 |
