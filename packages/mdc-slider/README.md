<!--docs:
title: "Sliders"
layout: detail
section: components
excerpt: "Sliders allow users to make selections from a range of values."
iconId: slider
path: /catalog/input-controls/sliders/
-->

# Slider

[Sliders](https://material.io/components/sliders/) はユーザーに値の範囲から選択させるようにするものです。

MDC Slider の実装は1点スライダー（1つのつまみ）と範囲スライダー（2つのつまみ）の両方をサポートします。これはブラウザの `<input type="range">` 要素にならって作られています。

スライダーは [WAI-ARIA 仕様](https://www.w3.org/TR/wai-aria-practices/#slider) に沿ったアクセシビリティのベストプラクティスに沿っており、完全に RTL 対応しています。

## コンテンツ

*   [スライダーの使用法](#using-sliders)
*   [スライダー](#sliders)
*   [その他のバリエーション](#other-variants)
*   [追加の情報](#additional-information)
*   [API](#api)

## <a name="using-sliders"></a>スライダーの使用

### スライダーのインストール

```
npm install @material/slider
```

### スタイル

```scss
@use "@material/slider";

@include slider.core-styles;
```

### JavaScript のインスタンス化

```js
import {MDCSlider} from '@material/slider';

const slider = new MDCSlider(document.querySelector('.mdc-slider'));
```

**注意**: JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## <a name="sliders"></a>スライダー

スライダーには2つのタイプがあります。

1.  [連続スライダー](#continuous-slider)
1.  [離散スライダー](#discrete-slider)

### <a name="continuous-slider"></a>連続スライダー

連続スライダーはユーザーに特定の値を必要としな意味のある選択をさせるようにするものです。

<img src="images/continuous-slider.png" alt="Continuous slider with a value of 50">

```html
<div class="mdc-slider">
  <div class="mdc-slider__track">
    <div class="mdc-slider__track--active">
      <div class="mdc-slider__track--active_fill"></div>
    </div>
    <div class="mdc-slider__track--inactive"></div>
  </div>
  <div class="mdc-slider__thumb" role="slider" tabindex="0" aria-valuemin="0"
       aria-valuemax="100" aria-valuenow="50">
    <div class="mdc-slider__thumb-knob"></div>
  </div>
</div>
```

#### 連続範囲スライダー

<img src="images/continuous-range-slider.png" alt="Continuous range slider with values of 30 and 70">

```html
<div class="mdc-slider mdc-slider--range">
  <div class="mdc-slider__track">
    <div class="mdc-slider__track--active">
      <div class="mdc-slider__track--active_fill"></div>
    </div>
    <div class="mdc-slider__track--inactive"></div>
  </div>
  <div class="mdc-slider__thumb" role="slider" tabindex="0" aria-valuemin="0" aria-valuemax="100" aria-valuenow="30">
    <div class="mdc-slider__thumb-knob"></div>
  </div>
  <div class="mdc-slider__thumb" role="slider" tabindex="0" aria-valuemin="0" aria-valuemax="100" aria-valuenow="70">
    <div class="mdc-slider__thumb-knob"></div>
  </div>
</div>
```

### <a name="discrete-slider"></a>離散スライダー

離散スライダーはつまみを押さえると数値ラベルを表示し、ユーザーに正確な値を選ばせるようにするものです。

<img src="images/discrete-slider.png" alt="Discrete slider with a value of 50">

離散スライダーを作るには以下のものを追加します。

*   ルート要素の `mdc-slider--discrete` クラス
*   ルート要素の `data-step` 属性。これは値の刻み幅を表します。設定しなければデフォルトで 1 になります。
*   以下に示すような値インジケーター要素（`mdc-slider__value-indicator-container`）。

```html
<div class="mdc-slider mdc-slider--discrete" data-step="10">
  <div class="mdc-slider__track">
    <div class="mdc-slider__track--active">
      <div class="mdc-slider__track--active_fill"></div>
    </div>
    <div class="mdc-slider__track--inactive"></div>
  </div>
  <div class="mdc-slider__thumb" role="slider" tabindex="0" aria-valuemin="0" aria-valuemax="100" aria-valuenow="50">
    <div class="mdc-slider__value-indicator-container">
      <div class="mdc-slider__value-indicator">
        <span class="mdc-slider__value-indicator-text">
          50
        </span>
      </div>
    </div>
    <div class="mdc-slider__thumb-knob"></div>
  </div>
</div>
```

#### 目盛付き離散スライダー

離散スライダーはオプションで目盛を表示することができます。目盛はユーザーがスライダーを動かくすことのできるあらかじめ決められた値を表します。

<img src="images/discrete-slider-tick-marks.png" alt="Discrete slider (with tick marks), with a value of 50">

離散スライダーにメモリを追加するには、以下のものを追加します。

*   ルート要素の `mdc-slider--tick-marks` クラス

```html
<div class="mdc-slider mdc-slider--discrete mdc-slider--tick-marks" data-step="10">
  <div class="mdc-slider__track">
    <div class="mdc-slider__track--active">
      <div class="mdc-slider__track--active_fill"></div>
    </div>
    <div class="mdc-slider__track--inactive"></div>
  </div>
  <div class="mdc-slider__thumb" role="slider" tabindex="0" aria-valuemin="0" aria-valuemax="100" aria-valuenow="50">
    <div class="mdc-slider__value-indicator-container">
      <div class="mdc-slider__value-indicator">
        <span class="mdc-slider__value-indicator-text">
          50
        </span>
      </div>
    </div>
    <div class="mdc-slider__thumb-knob"></div>
  </div>
</div>
```

#### 離散範囲スライダー

```html
<div class="mdc-slider mdc-slider--range mdc-slider--discrete" data-step="10">
  <div class="mdc-slider__track">
    <div class="mdc-slider__track--active">
      <div class="mdc-slider__track--active_fill"></div>
    </div>
    <div class="mdc-slider__track--inactive"></div>
  </div>
  <div class="mdc-slider__thumb" role="slider" tabindex="0" aria-valuemin="0" aria-valuemax="100" aria-valuenow="20">
    <div class="mdc-slider__value-indicator-container">
      <div class="mdc-slider__value-indicator">
        <span class="mdc-slider__value-indicator-text">
          20
        </span>
      </div>
    </div>
    <div class="mdc-slider__thumb-knob"></div>
  </div>
  <div class="mdc-slider__thumb" role="slider" tabindex="0" aria-valuemin="0" aria-valuemax="100" aria-valuenow="50">
    <div class="mdc-slider__value-indicator-container">
      <div class="mdc-slider__value-indicator">
        <span class="mdc-slider__value-indicator-text">
          50
        </span>
      </div>
    </div>
    <div class="mdc-slider__thumb-knob"></div>
  </div>
</div>name
```

## <a name="other-variants"></a>その他のバリエーション

### 無効なスライダー

スライダーを無効にするには、以下のものを追加します。

*   ルート要素の `mdc-slider--disabled` クラス
*   つまみの `tabindex="-1"` 属性
*   つまみの `aria-disabled="true"`

```html
<div class="mdc-slider mdc-slider--disabled">
  <div class="mdc-slider__track">
    <div class="mdc-slider__track--active">
      <div class="mdc-slider__track--active_fill"></div>
    </div>
    <div class="mdc-slider__track--inactive"></div>
  </div>
  <div class="mdc-slider__thumb" role="slider" tabindex="-1" aria-valuemin="0" aria-valuemax="100" aria-valuenow="50" aria-disabled="true">
    <div class="mdc-slider__thumb-knob"></div>
  </div>
</div>
```

## <a name="additional-information"></a>追加の情報

### 指定した範囲と値を持つスライダーの初期化

`MDCSlider` が初期化される際に、要素の `aria-valuemin` と `aria-valuemax` と `aria-valuenow` の値があるなら読み込み、コンポーネント内部の `min`、 `max`、 `value` の各プロパティに設定します。

これらの属性を指定した範囲と値のスライダーの初期化に使うには以下のようにします。

```html
<div class="mdc-slider">
  <!-- ... -->
  <div class="mdc-slider__thumb" role="slider" tabindex="0" aria-valuemin="0" aria-valuemax="100" aria-valuenow="75">
    <div class="mdc-slider__thumb-knob"></div>
  </div>
</div>
```

## API

### Sass ミキシン

ミキシン | 説明
--- | ---
`track-active-color($color)` | 有効なトラックの色を設定する。
`track-inactive-color($color, $opacity)` | 有効でないトラックの色と不透明度を設定する。
`thumb-color($color)` | つまみの色を設定する。
`thumb-ripple-color($color)` | つまみのリップルの色を設定する。
`tick-mark-active-color($color)` | 有効なトラック上の目盛の色を設定する。
`tick-mark-inactive-color($color)` | 有効でないトラック上の目盛の色を設定する。
`value-indicator-color($color, $opaicty)` | 値インジケーターの色と不透明度を設定する。
`value-indicator-text-color($color, $opaicty)` | 値インジケーターのテキストの色を設定する。

### `MDCSlider` イベント

イベント名 | `event.detail` | 説明
--- | --- | ---
`MDCSlider:change` | `MDCSliderChangeEventDetail` | 値が変わり、ユーザーイベントが完了したときに発生する。ネイティブな `change` イベント (https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event) の鏡
`MDCSlider:input` | `MDCSliderChangeEventDetail` | ユーザーイベントにより値が変わったときに発生する。ネイティブな `input` イベント (https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/input_event) の鏡

### `MDCSlider` メソッド

メソッド | 説明
--- | ---
`getValueStart() => number` | 開始つまみの値を取得する（範囲スライダーのみに適用）。
`setValueStart(valueStart: number) => void` | 開始つまみの値を設定する（範囲スライダーのみに適用）。
`getValue() => number` | つまみ（1点スライダーのとき）、または、終了つまみ（範囲スライダーのとき）の値を取得する。
`setValue(value: number) => void` | つまみ（1点スライダーのとき）、または、終了つまみ（範囲スライダーのとき）の値を設定する。
`getDisabled() => boolean` | スライダーの無効状態を取得する。
`setDisabled(disabled: boolean) => void` |スライダーの無効状態を設定する。

### フレームワーク内での使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のスライダーを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

スライダーのファンデーション API の 最新コードのドキュメントに関しては [MDCSliderAdapter](./adapter.ts) と [MDCSliderFoundation](./foundation.ts) を参照してください。
