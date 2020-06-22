<!--docs:
title: "Switches"
layout: detail
section: components
iconId: switch
path: /catalog/input-controls/switches/
-->

# 選択コントロール: スイッチ

[選択コントロール](https://material.io/components/selection-controls#usage) はユーザーにオプションを選択させるものです。

スイッチはオンまたはオフの単一の状態を切り替えるものです。モバイル上で設定を変えるにあたって優れた方法です。

![メニューオプションのためのスイッチの例](images/switch-hero.png)

## コンテンツ

* [スイッチの使用法](#using-switches)
* [スイッチ](#switches)
* [その他のバリエーション](#other-variants)
* [API](#api)
* [Web フレームワークでの使用](#usage-within-web-frameworks)

## <a name="using-switches"></a>スイッチの使用法

スイッチは次のような場所で使います。

* モバイルやタブレット上での単一項目のオンかオフの切り替え
* 直ちに何かを有効または無効にする

### スイッチのインストール

```
npm install @material/switch
```

### スタイル

```scss
@use "@material/switch";

@include switch.core-styles;
```

### JavaScript のインスタンス化

スイッチは機能するうえで JavaScript が必須で、そのため、`mdc-switch` 要素上に `MDCSwitch` をインスタンス化する必要があります。

```js
import {MDCSwitch} from '@material/switch';

const switchControl = new MDCSwitch(document.querySelector('.mdc-switch'));
```

**注意: See JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。**

## <a name="switches"></a>スイッチ

### スイッチの例

```html
<div class="mdc-switch">
  <div class="mdc-switch__track"></div>
  <div class="mdc-switch__thumb-underlay">
    <div class="mdc-switch__thumb"></div>
    <input type="checkbox" id="basic-switch" class="mdc-switch__native-control" role="switch" aria-checked="false">
  </div>
</div>
<label for="basic-switch">off/on</label>
```

### スイッチの状態

スイッチはオンかオフにすることができます。スイッチは利用可能、ホバー、フォーカス、押下の状態をとります。

![スイッチの状態の表。列は利用可能、利用不可、ホバー、フォーカス、押下を表す。行はオン・オフ。](images/switch-states.png)

## <a name="other-variants"></a>その他のバリエーション

### 初期状態が利用不可のスイッチ

`mdc-switch` 要素に `mdc-switch--disabled` クラスを追加し、スイッチを利用不可にするために `mdc-switch__native-control` 要素に `disabled` 属性を追加します。このロジックは `MDCSwitchFoundation.setDisabled` メソッドにより行われますが、初期化の際にクラスと属性を追加することにより FOUC を避けることができます。

```html
<div class="mdc-switch mdc-switch--disabled">
  <div class="mdc-switch__track"></div>
  <div class="mdc-switch__thumb-underlay">
    <div class="mdc-switch__thumb"></div>
    <input type="checkbox" id="another-basic-switch" class="mdc-switch__native-control" role="switch" aria-checked="false" disabled>
  </div>
</div>
<label for="another-basic-switch">off/on</label>
```

### 初期状態が "on" のスイッチ

`mdc-switch` 要素に `mdc-switch--checked` クラスを追加し、スイッチを "on" に切り替えるために `mdc-switch__native-control` 要素に `checked` 属性を追加します。このロジックは `MDCSwitchFoundation.setChecked` メソッドにより行われますが、初期化の際にクラスと属性を追加することにより FOUC を避けることができます。


```html
<div class="mdc-switch mdc-switch--checked">
  <div class="mdc-switch__track"></div>
  <div class="mdc-switch__thumb-underlay">
    <div class="mdc-switch__thumb"></div>
    <input type="checkbox" id="another-basic-switch" class="mdc-switch__native-control" role="switch" aria-checked="true" checked>
  </div>
</div>
<label for="another-basic-switch">off/on</label>
```

## API

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-switch` | 必須。親要素につける。
`mdc-switch--disabled` | オプション。スイッチを無効にする。
`mdc-switch--checked` | オプション。スイッチをチェック状態（"on"）にする。
`mdc-switch__track` | 必須。トラック要素につける。
`mdc-switch__thumb-underlay` | 必須。リップル効果に必要。
`mdc-switch__thumb` | 必須。つまみ要素につける。
`mdc-switch__native-control` | 必須。隠された input チェックボックスにつける。

### Sass ミキシン

MDC Switch はデフォルトでチェックさえた状態（トグルが ON）に [MDC Theme](../mdc-theme) の `secondary` カラーを使用します。<em>利用可能</em>なスイッチをカスタマイズするには以下のミキシンを使います。現時点では<em>利用不可</em>のスイッチの色をカスタマイズすることはできません。利用不可のスイッチは利用可能なスイッチと同じ色を使用しますが、透明度の値が異なります。

ミキシン | 説明
--- | ---
`toggled-on-color($color)` | スイッチがオンの時のトラック、つまみとリップルの色を設定する。
`toggled-off-color($color)` | スイッチがオフの時のトラック、つまみとリップルの色を設定する。
`toggled-on-track-color($color)` | スイッチがオンの時のトラックの色を設定する。
`toggled-off-track-color($color)` | スイッチがオフの時のトラックの色を設定する。
`toggled-on-thumb-color($color)` | スイッチがオンの時のつまみの色を設定する。
`toggled-off-thumb-color($color)` | スイッチがオフの時のつまみの色を設定する。
`toggled-on-ripple-color($color)` | スイッチがオンの時のつまみを囲むリップルの色を設定する。
`toggled-off-ripple-color($color)` | スイッチがオフの時のつまみを囲むリップルの色を設定する。
`ripple-size($ripple-size)` | スイッチのリップルサイズを設定する。
`density($density-scale)` | スイッチの密度スケールを設定する。サポートしている密度スケールは `-5`、`-4`、`-3`、`-2`、`-1` そして `0`（デフォルト）。
`ripple-states-opacity($opacity-map)` | `hover`、`focus`、`press` いずれかの状態のつまみを囲むリップルの不透明度を設定する。`opacity-map` にはこれらの状態をキーとして指定できる。マップに指定していない状態はデフォルトの不透明度が使われる。

### `MDCSwitch` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`checked` | Boolean | スイッチのチェック状態のセッタ/ゲッタ
`disabled` | Boolean | スイッチの利用不可かどうかの状態のセッタ/ゲッタ

## <a name="usage-within-web-frameworks"></a>Web フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のスイッチを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCSwitchAdapter`

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `setNativeControlChecked(checked: boolean)` | ネイティブコントロールのチェック状態を設定する。 |
| `setNativeControlDisabled(disabled: boolean)` | ネイティブコントロールの利用不可の状態を設定する。 |
| `setNativeControlAttr(attr: string, value: string)` | ネイティブコントロールの HTML 属性を与えられた値に設定する。 |

### `MDCSwitchFoundation`

| メソッド | 説明 |
| --- | --- |
| `setChecked(checked: boolean) => void` | ネイティブコントロールのチェック状態を設定し、チェック状態を反映したスタイルに更新する。 |
| `setDisabled(disabled: boolean) => void` | ネイティブコントロールの利用不可かどうかの値を設定し、利用不可かどうかの状態を反映したスタイルに更新する。 |
| `handleChange(evt: Event) => void` | ネイティブコントロールからの change イベントをハンドリングする。 |

### `MDCSwitchFoundation` イベントハンドラー

スイッチコンポーネントをラプスるときには `handleChange` ファンデーションメソッドを呼び出すネイティブコントロールの change イベントのイベントハンドラーを追加する必要があります。この例としては、[`MDCSwitch`](component.ts) コンポーネントの `initialSyncWithDOM` メソッドを参照してください。

| イベント | 要素セレクター | ファンデーションハンドラー |
| --- | --- | --- |
| `change` | `.mdc-switch__native-control` | `handleChange()` |
