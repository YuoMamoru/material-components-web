<!--docs:
title: "Sliders"
layout: detail
section: components
excerpt: "A select over a range of values by moving the slider thumb."
iconId: slider
path: /catalog/input-controls/sliders/
-->

# Slider

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/slider">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/slider.png" width="400" alt="Select screenshot">
  </a>
</div>-->

MDC Slider はマテリアルデザインのスライダーコンポーネントの実装を提供します。これはブラウザの `<input type="range">` 要素にならって作られています。Slider は完全に RTL 対応しており、WAI-ARIA の [スライダー作成手法](https://www.w3.org/TR/wai-aria-practices-1.1/#slider) に従っています。

**鉛直スライダーとレンジスライダー（複数つまみ）は、マテリアルデザイン仕様に存在しないため、サポートしていません**。

また、仕様内において UX からある程度逸脱していることも気に留めておいてください。例えば、トラック上のスライダーの動作のニュアンスや目盛の色がそれにあたります。したがって、モックから逸脱した使い方があるでしょう。これらの逸脱は web 上で使用されているスライダーを確認することによる設計のフィードバックから生じたものであり、マテリアルデザインチームから支持されています。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-sliders">マテリアルデザインガイドライン: スライダー</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/slider">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/slider
```

## 使用法

### 連続スライダー

```html
<div class="mdc-slider" tabindex="0" role="slider"
     aria-valuemin="0" aria-valuemax="100" aria-valuenow="0"
     aria-label="Select Value">
  <div class="mdc-slider__track-container">
    <div class="mdc-slider__track"></div>
  </div>
  <div class="mdc-slider__thumb-container">
    <svg class="mdc-slider__thumb" width="21" height="21">
      <circle cx="10.5" cy="10.5" r="7.875"></circle>
    </svg>
    <div class="mdc-slider__focus-ring"></div>
  </div>
</div>
```

### 非連続スライダー

```html
<div class="mdc-slider mdc-slider--discrete" tabindex="0" role="slider"
     aria-valuemin="0" aria-valuemax="100" aria-valuenow="0"
     aria-label="Select Value">
  <div class="mdc-slider__track-container">
    <div class="mdc-slider__track"></div>
  </div>
  <div class="mdc-slider__thumb-container">
    <div class="mdc-slider__pin">
      <span class="mdc-slider__pin-value-marker"></span>
    </div>
    <svg class="mdc-slider__thumb" width="21" height="21">
      <circle cx="10.5" cy="10.5" r="7.875"></circle>
    </svg>
    <div class="mdc-slider__focus-ring"></div>
  </div>
</div>
```

JS は以下のようにします。

```js
import {MDCSlider} from '@material/slider';

const slider = new MDCSlider(document.querySelector('.mdc-slider'));
slider.listen('MDCSlider:change', () => console.log(`Value changed to ${slider.value}`));
```

`dist/mdc.slider[.min].js` にある UMD バージョンを通じて MDCSlider をインクルードすることもできます。

```js
// CommonJS
const {MDCSlider} = require('@material/slider/dist/mdc.slider');

// AMD
require(['/path/to/@material/slider/dist/mdc.slider'], ({MDCSlider}) => {
  // MDCSlider を使う
});

// Global
const {MDCSlider} = mdc.slider;
```

### 指定した範囲/値を持つスライダーの初期化

`MDCSlider` が初期化される際に、要素の `aria-valuemin` と `aria-valuemax` と `aria-valuenow` の値があるなら読み込み、コンポーネントの `min`、 `max`、 `value` の各プロパティの設定に使用します。スライダーにこれらの値を設定すのに DOM 内のこれらの属性を使うことができるということをこれは意味しています。

```html
<div class="mdc-slider" tabindex="0" role="slider"
     aria-valuemin="-5" aria-valuemax="50" aria-valuenow="10"
     aria-label="Select Value">
  <!-- ... -->
</div>
```

### 刻み幅の指定

> **注意**: スライダーに刻み幅があるということは「非連続」スライダーであるということを意味するものでは <em>ありません</em>。「非連続スライダー」は UX の議論であり、刻み幅は振舞いの話です。

`MDCSlider` は `data-step` 属性を使って不動小数点の `step` の値をユーザーに提供することにより離散的な値を取ることができます。

```html
<div class="mdc-slider" tabindex="0" role="slider"
     aria-valuemin="0" aria-valuemax="100" aria-valuenow="0"
     data-step="2" aria-label="Select Value">
  <!-- ... -->
</div>
```

刻み幅が与えられると、スライダーは最大値と最小値を <em>除く</em> すべての値を刻み幅に合うように設定し、最大値と最小値も設定できるようにします。これにより一貫した挙動が保証されます。

刻み幅は正の浮動小数点の数値か `0` でなくてはなりません。刻み幅を `0` にするとスライダーは刻み幅を持たないとみなします。刻み幅に負の数を設定するとエラーが投げられます。

非連続スライダーは 0 以外の正の刻み幅が必要です。刻み幅に 0 を指定するか値を設定しないときは、刻み幅はデフォルトで 1 になります。

### トラックマーカーの表示（非連続スライダーのみ）

非連続スライダーは、`mdc-slider` に `mdc-slider--display-markers` 修飾クラスを追加し、トラックのコンテナに `<div class="mdc-slider__track-marker-container"></div>` を追加することにより、トラック上にマーカーを表示することができます。

```html
<div class="mdc-slider mdc-slider--discrete mdc-slider--display-markers" tabindex="0" role="slider"
     aria-valuemin="0" aria-valuemax="100" aria-valuenow="0"
     data-step="2" aria-label="Select Value">
     <div class="mdc-slider__track-container">
      <div class="mdc-slider__track"></div>
      <div class="mdc-slider__track-marker-container"></div>
    </div>
    <!-- ... -->
</div>
```

> **注意**: 最大値と最小値の間隔が与えられた目盛の間隔で割り切れないとき、最後から 2 番目のマーカーを目盛の間隔に比例させたことろに配置し、最後のマーカーは最大値のところに配置します。

### 無効なスライダー

スライダーを最初から無効にするには `aria-disabled` 属性を追加します。

```html
<div class="mdc-slider" tabindex="0" role="slider"
     aria-valuemin="0" aria-valuemax="100" aria-valuenow="0"
     aria-label="Select Value" aria-disabled="true">
  <!-- ... -->
</div>
```

### MDC Slider コンポーネント API

`MDCSlider` API は `<input type="range">` 要素に倣って作られており、この要素がサポートしているプロパティの一部をサポートしています。また、`<input type="range">` の `input` および `change` イベントと同様のイベントも提供しています。

#### プロパティ

| プロパティ | 型 | 説明 |
| --- | --- | --- |
| `value` | `number` | スライダーの現在の値。これを変更するとスライダーの値も更新される。 |
| `min` | `number` | スライダーが取れる値の最小値。プログラムから設定された値は最小値として固定される。このプロパティを変更した際にスライダーの値が新しい最小値より小さいときはスライダーの値も更新される。 |
| `max` | `number` | スライダーが取れる値の最大値。プログラムから設定された値は最大値として固定される。このプロパティを変更した際にスライダーの値が新しい最大値より大きいときはスライダーの値も更新される。 |
| `step` | `number` | スライダーに設定できる値の増分を指定する。正の数か、刻み幅がないなら `0` をとることができる。このプロパティを変更すると新しい刻み幅に応じた値にスライダーの値が更新される。 |
| `disabled` | `boolean` | スライダーが無効かそうでないか。 |

#### メソッド

| メソッド | 説明 |
| --- | --- |
| `layout() => void` | 大きさを再計算し、コンポーネントを再配置する。このメソッドはスライダー自身か親要素のいずれかの大きさが変わったときに呼び出される（これを自動リサイズという）。 |
| `stepUp(amount = 1) => void` | スライダーの値を与えられた `amount` の分だけ増やす。引数を与えないときは `1` 増やす。 |
| `stepDown(amount = 1) => void` | スライダーの値を与えられた `amount` の分だけ減らす。引数を与えないときは `1` 減らす。 |

#### イベント

ユーザーのイベントによりスライダーの値が変更されたときに、`MDCSlider` はルート要素から `MDCSlider:input` カスタムイベントを送出します。例えば、ユーザーがスライダーをドラッグしたり、方向キーで値を変更したりしたときに発生します。イベントの `detail` プロパティには対象となったスライダーのインスタンスが設定されます。

ユーザーのイベントによりスライダーの値の変更が <em>確定</em> したときに、`MDCSlider` はルート要素から `MDCSlider:change` カスタムイベントを送出します。例えば、ユーザーがスライダーをドラッグし終えたり、方向キーで値を変更したりしたときに発生します。イベントの `detail` プロパティには対象となったスライダーのインスタンスが設定されます。

### ファンデーションクラスの使用

フレームワーク制作者が自身のフレームワークにおいてカスタム MDCSlicer コンポーネントを構築するために使用できる `MDCSliderFoundation` クラスが `@material/slider` パッケージには付属しています。

#### アダプター API

| メソッド | 説明 |
| --- | --- |
| `hasClass(className: string) => boolean` | ルート要素に `className` が存在するか確認する。 |
| `addClass(className: string) => void` | ルート要素にクラス `className` を追加する。 |
| `removeClass(className: string) => void` | ルート要素からクラス `className` を削除する。 |
| `getAttribute(name: string) => string?` | ルート要素の属性 `name` の値を返す。ルート要素にその属性がないときは `null` を返す。 |
| `setAttribute(name: string, value: string) => void` | ルート要素の属性 `name` に値 `value` を設定する。 |
| `removeAttribute(name: string) => void` | ルート要素から属性 `name` を削除する。 |
| `computeBoundingRect() => ClientRect` | ルート要素に結びついている client rect を計算して返す。私たちの実装では `getBoundingClientRect()` を呼んでいる。 |
| `getTabIndex() => number` | ルート要素の `tabIndex` プロパティの値を返す。 |
| `registerInteractionHandler(type: string, handler: EventListener) => void` | スライダーのルート要素にイベント `type` のイベントリスナー `handler` を追加する。 |
| `deregisterInteractionHandler(type: string, handler: EventListener) => void` | スライダーのルート要素からイベント `type` のイベントリスナー `handler` を削除する。 |
| `registerThumbContainerInteractionHandler(type: string, handler: EventListener) => void` | スライダーのつまみのコンテナ要素にイベント `type` のイベントリスナー `handler` を追加する。 |
| `deregisterThumbContainerInteractionHandler(type: string, handler: EventListener) => void` | スライダーのつまみのコンテナ要素からイベント `type` のイベントリスナー `handler` を削除する。 |
| `registerBodyInteractionHandler(type: string, handler: EventListener) => void` | スライダーのドキュメントの `<body>` 要素にイベント `type` のイベントリスナー `handler` を追加する。 |
| `deregisterBodyInteractionHandler(type: string, handler: EventListener) => void` | スライダーのドキュメントの `<body>` 要素からイベント `type` のイベントリスナー `handler` を削除する。 |
| `registerResizeHandler(handler: EventListener) => void` | コンポーネントのビューポートがリサイズされたとき（例えば `window.onresize`）に呼び出されるイベントリスナー `handler` を追加する。 |
| `deregisterResizeHandler(handler: EventListener) => void` | `registerResizeHandler` を使ってアタッチしたイベントリスナー `handler` を削除する。 |
| `notifyInput() => void` | スライダーの値が現在変わっている最中であることをクライアントに通知する "input" イベントを発生させる。実装ではこのイベントに関連する適切な情報を渡さなくてはならない。私たちのケースではイベントのトリガーとなったコンポーネントのインスタンスを渡している。 |
| `notifyChange() => void` | ユーザーによってスライダーの値の変更が確定したことをクライアントに通知する "change" イベントを発生させる。`notifyInput()` と同じことがここでもいえる。 |
| `setThumbContainerStyleProperty(propertyName: string, value: string) => void` | つまみのコンテナ要素のダッシュの付いたスタイルのプロパティ `propertyName` に与えた `value` を設定する。 |
| `setTrackStyleProperty(propertyName: string, value: string) => void` | トラック要素のダッシュの付いたスタイルのプロパティ `propertyName` に与えた `value` を設定する。 |
| `setMarkerValue(value: number) => void` | 非連続スライダーのつまみが動かす際にピンの値にマーカーの値を設定する。 |
| `appendTrackMarkers(numMarkers: number) => void` | トラックのコンテナにトラックマーカー要素を追加する。 |
| `removeTrackMarkers() => void` | トラックコンテナに既存のマーカー要素を動かす。 |
| `setLastTrackMarkersStyleProperty(propertyName: string, value: string) => void` | トラックマーカーの最後の要素のダッシュの付いたスタイルのプロパティ `propertyName` に与えた `value` を設定する。 |
| `isRTL() => boolean` | スライダーが RTL コンテキスト内にあるなら true を返し、そうでなければ False を返す。 |

#### MDCSliderFoundation API

| メソッド | 説明 |
| --- | --- |
| `layout() => void` | コンポーネントメソッドの表の中で説明した layout() に同じ。作業の大半を行い、コンポーネントの layout メソッドは単なるこのメソッドのプロキシ。 |
| `getValue() => number` | 現在のスライダーの値を返す。 |
| `setValue(value: number) => void` | 現在のスライダーの値を設定する。 |
| `getMax() => number` | スライダーがとりうる最大値を返す。 |
| `setMax(max: number) => void` | スライダーがとりうる最大値を設定する。 |
| `getMin() => number` | スライダーがとりうる最小値を返す。 |
| `setMin(min: number) => number` | スライダーがとりうる最小値を設定する。 |
| `getStep() => number` | スライダーの刻み幅を返す。 |
| `setStep(step: number) => void` | スライダーの刻み幅を設定する。 |
| `isDisabled() => boolean` | スライダーが無効かそうでないかを返す。 |
| `setDisabled(disabled: boolean) => void` | true を与えるとスライダーを無効にし、そうでないときは有効にする。 |
| `setupTrackMarker() => void` | トラックマーカーを表示している非連続スライダーのトラック上のマーカーの正確な数を設定する。それらの条件を満たしていないときは何もしない。 |

### テーマ

デフォルトでスライダーのすべてのテーマを持つ要素は **セカンダリテーマカラー** を使用します。

#### Sass ミキシン

以下のミキシンは <em>有効な</em> スライダーでのみ適用されています。<em>無効な</em> スライダーの色を設定することは現在できません。

ミキシン | 説明
--- | ---
`mdc-slider-color-accessible($color)` | スライダーのすべての要素の色を設定し、値表示ピンのインク色を高いコントラストの識別しやすい色に自動的に設定する。
`mdc-slider-highlight-color($color)` | スライダーのハイライトされた（別名「オン」）部分の色を設定する。
`mdc-slider-rail-color($color, $opacity)` | レールの色（オプションで不透明度も）を設定する。
`mdc-slider-rail-tick-mark-color($color)` | レール上の目盛の色を設定する。
`mdc-slider-thumb-color($color)` | つまみ（つかむ部分）の色を設定する。
`mdc-slider-focus-halo-color($color)` | フォーカス時の背景の光輪の色を設定する。
`mdc-slider-value-pin-fill-color-accessible($color)` | 値表示ピンの塗りの色を設定し、インク色を高いコントラストの識別しやすい色に自動的に設定する。
`mdc-slider-value-pin-fill-color($color)` | 値表示ピンの塗りの色を設定する。
`mdc-slider-value-pin-ink-color($color)` | 値表示ピンのインク色を設定する。

#### 無効なスライダーつまみに対する適切な色の設定

スライダーの難しい問題の一つに、無効な状態のときつまみをどのように見せるかというものがあります。この場合、スライダーのつまみとトラックの確かな部分は「透明」になり、背後にある背景色で表示することになります。しかしながら、この方法は、スライダーの背後にくる背景色を何にすべきかというエレガントな解決策のない問題を発生させてしまいます。論理的には背景色を持つ祖先が見つかるまで DOM をさかのぼることはできますが、これはコンポーネントのカプセル化に反することになります。

この問題を解決するために、CSS カスタムプロパティ `--mdc-slider-bg-color-behind-component` を適用することができます。これを使うと、無効のスライダーのつまみが使用しているデフォルト色を上書きされ、してした色にすることができます。

```css
.container {
  background: #fafafa;
}

.container > .mdc-slider {
  --mdc-slider-bg-color-behind-component: #fafafa;
}
```

### ヒント/小技

#### [FOUC](https://en.wikipedia.org/wiki/Flash_of_unstyled_content) の防止

`MDCSlider` はインスタンス化されたときに読み込んだ値をもとに UI を構築するので、`MDCSlider` インスタンスロジックの含まれるスクリプトが実行される前の最初の描画が不適切である可能性があります。これを避けるために、やれることがいくつかあります。

インスタンス化されるときにスライダーの幅がわかっているなら、私たちのコードの中でやっているのと同じ方法で `mdc-slider__thumb-container`/`mdc-slider__track` 要素にインラインスタイルを追加することができます。

1. `(value - min) / (max - min)` を計算することにより、つまみがトラック上を動く長さの割合を求めます。これを `pctComplete` とします。
1. スライダー要素の幅に `pctComplete` をかけてスライダーつまみのコンテナの大きさを計算します。これを `translatePx` とします。RTL コンテンツでスライダーを使っているときは、`translatePx` は `translatePx = <width of the slider element> - translatePx` に変えてください。
1. `mdc-slider__thumb-container` の `transform` スタイルを `translateX(${translatePx}px) translateX(-50%)` に設定します。
1. `mdc-slider__track` の `transform` スタイルを `scale(pctComplete)` に設定します。
