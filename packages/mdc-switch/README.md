<!--docs:
title: "Switches"
layout: detail
section: components
iconId: switch
path: /catalog/input-controls/switches/
-->

# Switches

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/switch">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/switches.png" width="37" alt="Switches screenshot">
  </a>
</div>-->

スイッチはオンまたはオフの単一の状態を切り替えるものです。モバイル上で設定を変えるにあたって優れた方法です。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-switches">マテリアルデザインガイドライン: スイッチ</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/switch">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/switch
```

## 基本的な使用法

### HTML 構造

```html
<div class="mdc-switch">
  <div class="mdc-switch__track"></div>
  <div class="mdc-switch__thumb-underlay">
    <div class="mdc-switch__thumb">
        <input type="checkbox" id="basic-switch" class="mdc-switch__native-control" role="switch">
    </div>
  </div>
</div>
<label for="basic-switch">off/on</label>
```

### スタイル

```scss
@import "@material/switch/mdc-switch";
```

### JavaScript のインストール

スイッチを機能させるは JavaScript が必須で、そのため HTML 上で MDCSwitch をインスタンス化することが必要です。

```js
import {MDCSwitch} from '@material/switch';

const switchControl = new MDCSwitch(document.querySelector('.mdc-switch'));
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## 様々な使用法

### 無効なスイッチの初期化

`mdc-switch` 要素に `mdc-switch--disabled` クラスを追加し、スイッチを無効にするために `mdc-switch__native-control` 要素に `disabled` 属性を追加します。このロジックは `MDCSwitchFoundation.setDisabled` メソッドにより行われますが、初期化の際にクラスと属性を追加することにより FOUC を避けることができます。

```html
<div class="mdc-switch mdc-switch--disabled">
  <div class="mdc-switch__track"></div>
  <div class="mdc-switch__thumb-underlay">
    <div class="mdc-switch__thumb">
      <input type="checkbox" id="another-basic-switch" class="mdc-switch__native-control" role="switch" disabled>
    </div>
  </div>
</div>
<label for="another-basic-switch">off/on</label>
```

### "On" のスイッチの初期化

`mdc-switch` 要素に `mdc-switch--checked` クラスを追加し、スイッチを "on" に切り替えるために `mdc-switch__native-control` 要素に `checked` 属性を追加します。このロジックは `MDCSwitchFoundation.setChecked` メソッドにより行われますが、初期化の際にクラスと属性を追加することにより FOUC を避けることができます。


```html
<div class="mdc-switch mdc-switch--checked">
  <div class="mdc-switch__track"></div>
  <div class="mdc-switch__thumb-underlay">
    <div class="mdc-switch__thumb">
      <input type="checkbox" id="another-basic-switch" class="mdc-switch__native-control" role="switch" checked>
    </div>
  </div>
</div>
<label for="another-basic-switch">off/on</label>
```

## スタイルのカスタマイズ

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
`mdc-switch-toggled-on-color($color)` | スイッチがオンの時のトラック、つまみとリップルの色を設定する。
`mdc-switch-toggled-off-color($color)` | スイッチがオフの時のトラック、つまみとリップルの色を設定する。
`mdc-switch-toggled-on-track-color($color)` | スイッチがオンの時のトラックの色を設定する。
`mdc-switch-toggled-off-track-color($color)` | スイッチがオフの時のトラックの色を設定する。
`mdc-switch-toggled-on-thumb-color($color)` | スイッチがオンの時のつまみの色を設定する。
`mdc-switch-toggled-off-thumb-color($color)` | スイッチがオフの時のつまみの色を設定する。
`mdc-switch-toggled-on-ripple-color($color)` | スイッチがオンの時のつまみを囲むリップルの色を設定する。
`mdc-switch-toggled-off-ripple-color($color)` | スイッチがオフの時のつまみを囲むリップルの色を設定する。

## `MDCSwitch` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`checked` | Boolean | スイッチのチェック状態のセッタ/ゲッタ
`disabled` | Boolean | スイッチの利用不可かどうかの状態のセッタ/ゲッタ

## Web フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のスイッチを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCSwitchAdapter`

| メソッド | 説明 |
| --- | --- |
| `addClass(className: string) => void` | ルート要素にクラスを追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラスを削除する。 |
| `setNativeControlChecked(checked: boolean)` | ネイティブコントロールのチェック状態を設定する。 |
| `setNativeControlDisabled(disabled: boolean)` | ネイティブコントロールの利用不可の状態を設定する。 |

### `MDCSwitchFoundation`

| メソッド | 説明 |
| --- | --- |
| `setChecked(checked: boolean) => void` | ネイティブコントロールのチェック状態を設定し、チェック状態を反映したスタイルに更新する。 |
| `setDisabled(disabled: boolean) => void` | ネイティブコントロールの利用不可かどうかの値を設定し、利用不可かどうかの状態を反映したスタイルに更新する。 |
| `handleChange(evt: Event) => void` | ネイティブコントロールからの change イベントをハンドリングする。 |

### `MDCSwitchFoundation` イベントハンドラー
スイッチコンポーネントをラプスるときには `handleChange` ファンデーションメソッドを呼び出すネイティブコントロールの change イベントのイベントハンドラーを追加する必要があります。この例としては、[`MDCSwitch`](component.ts) コンポーネントの `initialSyncWithDOM` メソッドを参照してください。

| イベント | 要素セレクタ | ファンデーションハンドラー |
| --- | --- | --- |
| `change` | `.mdc-switch__native-control` | `handleChange()` |
