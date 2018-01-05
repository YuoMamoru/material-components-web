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
     href="https://material-components-web.appspot.com/switch.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/switches.png" width="37" alt="Switches screenshot">
  </a>
</div>-->

MDC Switch コンポーネントは [マテリアルデザインスイッチ要件](https://material.io/guidelines/components/selection-controls.html#selection-controls-switch) に準拠したスイッチコンポーネントです。JavaScript を使わなくても動作します。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/selection-controls.html#selection-controls-switch">マテリアルデザインガイドライン: スイッチ</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/switch.html">デモ</a>
  </li>
</ul>

## インストール

```
npm install --save @material/switch
```

## 使用法

```html
<div class="mdc-switch">
  <input type="checkbox" id="basic-switch" class="mdc-switch__native-control" />
  <div class="mdc-switch__background">
    <div class="mdc-switch__knob"></div>
  </div>
</div>
<label for="basic-switch" class="mdc-switch-label">off/on</label>
```

### 無効なスイッチ
```html
<div class="mdc-switch">
  <input type="checkbox" id="another-basic-switch" class="mdc-switch__native-control" disabled />
  <div class="mdc-switch__background">
    <div class="mdc-switch__knob"></div>
  </div>
</div>
<label for="another-basic-switch" class="mdc-switch-label">off/on</label>
```

### クラス

#### ブロック

ブロッククラスは `mdc-switch` です。これはトップレベルのスイッチ要素で定義されます。

### Sass ミキシン

以下のミキシンは <em>有効な</em>  _on_ （チェック）状態のスイッチにのみ適用されます。現在、<em>無効</em> もしくは _off_ （チェックなし）の状態のスイッチの色をカスタマイズすることはできません。

ミキシン | 説明
--- | ---
`mdc-switch-track-color($color)` | トラックの色を設定する。
`mdc-switch-knob-color($color)` | つまみの色を設定する。
`mdc-switch-focus-indicator-color($color)` | フォーカス時のインジケータの色を設定する。
