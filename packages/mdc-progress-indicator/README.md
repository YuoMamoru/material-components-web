<!--docs:
title: "Progress Indicator"
layout: detail
section: components
excerpt: "Material Design-styled progress indicators."
iconId: progress_linear
path: /catalog/progress-indicator/
-->

# Progress Indicators
MDC Progress Indicator コンポーネントはプログレスインジケーターに共通する基盤とコンポーネントインターフェースを提供します。これらのインターフェースを実装するコンポーネントには [linear progress](https://github.com/material-components/material-components-web/tree/master/packages/mdc-linear-progress) と [circular progress](https://github.com/material-components/material-components-web/tree/master/packages/mdc-circular-progress) が含まれています。[マテリアルデザインプログレスと動作要件](https://material.io/go/design-progress-indicators).

## インストール

```
npm install @material/progress-indicator
```

## 基本的な使用法

### MDCProgressIndicatorFoundation API

MDC Progress Indicator ファンデーションは以下のメソッドを提供します。

| メソッド | 説明 |
| --- | --- |
| `setDeterminate(value: boolean) => void` | コンポーネントに対して確定状態と未確定状態とを切り替える。 |
| `setProgress(value: number) => void` | プログレスに値を設定する。値は [0, 1] の範囲で指定する。 |
| `open() => void` | コンポーネントを開いた状態にする。 |
| `close() => void` | コンポーネントを閉じた状態にする。 |

### MDCProgressIndicator Component API

MDC Progress Indicator は以下のメソッドを提供します。

| メソッド | 説明 |
| --- | --- |
| `determinate: boolean` | インジケーターが確定状態か未確定状態か。 |
| `progress: number` | 現在の進行状況。値は [0, 1] の間。 |
| `open() => void` | コンポーネントを開いた状態にする。 |
| `close() => void` | コンポーネントを閉じた状態にする。 |
