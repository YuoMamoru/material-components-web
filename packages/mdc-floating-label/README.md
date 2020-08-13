<!--docs:
title: "Floating Label"
layout: detail
section: components
excerpt: "An animated text caption for a Text Field or Select."
path: /catalog/input-controls/floating-label/
-->

# Floating Label

フローティングラベルは入力欄に必要な入力のタイプを表示します。フル幅のテキスト欄を除くすべてのテキスト欄とセレクトにはラベルが必要で、フル幅のテキスト欄は代わりに `placeholder` 属性を使用します。ラベルは入力ラインにそろえられ、常に表示されています。ラベルは休んでいる（フィールドがアクティブでなく、空のとき）もしくは浮いています（訳注： アクティブでなく、空のときは入力欄に表示され、そうでないときは入力欄の上部に表示される、ということ）。ラベルはテキスト欄の見出しか説明となっています。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-text-fields#text-fields-layout">マテリアルデザインガイドライン: テキスト欄のレイアウト</a>
  </li>
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/text-field">テキスト欄のデモ</a>
  </li>
</ul>

## インストール

```
npm install @material/floating-label
```

## 基本的な使用法

### HTML 構造

```html
<span class="mdc-floating-label" id="my-label-id">Hint text</span>
```

### スタイル

```scss
@use "@material/floating-label/mdc-floating-label";
```

### JavaScript のインスタンス化

```js
import {MDCFloatingLabel} from '@material/floating-label';

const floatingLabel = new MDCFloatingLabel(document.querySelector('.mdc-floating-label'));
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-floating-label` | 必須。
`mdc-floating-label--float-above` | ラベルがフローティングポジションに浮いていることを示す。
`mdc-floating-label--shake` | ラベルを震えさせる。
`mdc-floating-label--required` | ラベルに必須であることを示し、アスタリスクを追加する。

### Sass ミキシン

ミキシン | 説明
--- | ---
`ink-color($color)` | ラベルのインク色を設定する。
`fill-color($color)` | ラベルの塗りの色を設定する。
`shake-keyframes($modifier, $positionY, $positionX, $scale)` | 無効なラベルの震えに対して CSS の `@keyframes` ルールを生成する。`shake-animation` ミキシンと組み合わせて使用する。
`shake-animation($modifier)` | ラベルに振動のキーフレームアニメーションを適用する。
`float-position($positionY, $positionX, $scale)` | 浮いているときのラベルの位置を設定する。
`max-width($max-width)` | ラベルの最大幅を設定する。
`float-transition($duration-ms, $timing-function)` | "float" への移動の期間とオプションでタイミング関数を設定する。

## `MDCFloatingLabel` プロパティとメソッド

メソッド | 説明
--- | ---
`shake(shouldShake: boolean) => void` | ファンデーションの `shake()` メソッドの代替。
`float(shouldFloat: boolean) => void` | ファンデーションの `float()` メソッドの代替。
`setRequired(isRequired: boolean) => void` | ファンデーションの `setRequired()` メソッドの代替。
`getWidth() => number` | ファンデーションの `getWidth()` メソッドの代替。

## フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のフローティングラベルを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCFloatingLabelAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ラベル要素にクラスを追加する。
`removeClass(className: string) => void` | ラベル要素からクラスを削除する。
`getWidth() => number` | ラベル要素の幅を返す。
`registerInteractionHandler(evtType: string, handler: EventListener) => void` | 与えられた要素にイベントリスナーを登録する。
`deregisterInteractionHandler(evtType: string, handler: EventListener) => void` | 与えられた要素からイベントリスナーを登録解除する。

### `MDCFloatingLabelFoundation`

メソッド | 説明
--- | ---
`shake(shouldShake: boolean)` | `shouldShake` の値に応じて、ラベルを震えさせる、もしくは震えを止める。
`float(shouldFloat: boolean)` | `shouldFloat` の値に応じて、ラベルを浮かせる、もしくはもとに元す。
`setRequired(isRequired: boolean)` | `isRequired` の値に応じて、ラベルを必須としてスタイルする
`getWidth() => number` | ラベル要素の幅を返す。
