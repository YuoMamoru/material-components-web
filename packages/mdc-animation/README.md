<!--docs:
title: "Animation"
layout: detail
section: components
excerpt: "Animation timing curves and utilities for smooth and consistent motion."
iconId: animation
path: /catalog/animation/
-->

# Animation

動作をともなうマテリアルは反応があり自然なものです。スムーズで一貫性のある動きを作るにはイージングカーブとデュレーションパターンを使ってください。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-motion">マテリアルデザインガイドライン: 継続時間とイージング</a>
  </li>
</ul>

## インストール

```
npm install @material/animation
```

## 使用法

### Sass 変数

`animation` や `transition` CSS プロパティで使用できるタイミング関数を提供しています。

```scss
@use "@material/animation";

.my-element--animating {
  animation: foo-keyframe 175ms animation.$standard-curve-timing-function;
}
```

変数 | 説明
--- | ---
`deceleration-curve-timing-function` | 減速していくタイミング関数
`standard-curve-timing-function` | 素早く加速し、ゆっくり減速していくタイミング関数
`acceleration-curve-timing-function` | 加速していくタイミング関数
`sharp-curve-timing-function` | 素早く加速、減速をしていくタイミング関数

以下の関数は `$name` と `$duration` を与えるトランジッションを生成します。`$delay`を指定することもできますが、初期値は 0 ミリ秒です。`$name` はキーフレームを参照することも `transition` で使っている CSS プロパティを参照することもできます。

```scss
@use "@material/animation";

.my-element {
  transition: animation.exit-permanent(/* $name: */ opacity, /* $duration: */ 175ms, /* $delay: */ 150ms);
  opacity: 0;
  will-change: opacity;

  &--animating {
    transition: animation.enter(/* $name: */ opacity, /* $duration: */ 175ms);
    opacity: 1;
  }
}
```


```scss
@use "@material/animation";

@keyframes fade-in {
  from {
    transform: translateY(-80px);
    opacity: 0;
  }

  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.my-element {
  animation: animation.enter(/* $name: */ fade-in, /* $duration: */ 350ms);
}
```

関数 | 説明
--- | ---
`enter($name, $duration, $delay)` | フレームに入るためのトランジッションを定義する
`exit-permanent($name, $duration, $delay)` | 恒久的にフレームに入るためのトランジッションを定義する
`exit-temporary($name, $duration, $delay)` | 一時的にフレームに入るためのトランジッションを定義する

### JavaScript

これらの関数は様々なブラウザのプレリックスを処理します。

```js
import {getCorrectEventName} from '@material/animation';

const eventToListenFor = getCorrectEventName(window, 'animationstart');
```

メソッド | 説明
--- | ---
`getCorrectEventName(windowObj: Window, eventType: StandardJsEventType) => StandardJsEventType \| PrefixedJsEventType` | JavaScript のイベント名と、必要であればプレフィックスを返す。サポートする値については [`types.ts`](types.ts) を参照のこと。
`getCorrectPropertyName(windowObj: Window, cssProperty: StandardCssPropertyName) => StandardCssPropertyName \| PrefixedCssPropertyName` | CSS のプロパティ名と、必要であればプレフィックスを返す。サポートする値については [`types.ts`](types.ts) を参照のこと。
