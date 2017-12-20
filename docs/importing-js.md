# JS コンポーネントのインポート

大半のコンポーネントは完全忠実なマテリアルデザインコンポーネントを提供するために使用される コンポーネント/ファンデーション クラスが付属しています。これまでどのようなテクノロジーを使ってきたかによって、JavaScript をインポートする方法はいくつかあります。

## ES2015

```javascript
import {MDCFoo, MDCFooFoundation} from '@material/foo';
```

## CommonJS

```javascript
const mdcFoo = require('mdc-foo');
const MDCFoo = mdcFoo.MDCFoo;
const MDCFooFoundation = mdcFoo.MDCFooFoundation;
```

## AMD

```javascript
require(['path/to/mdc-foo'], mdcFoo => {
  const MDCFoo = mdcFoo.MDCFoo;
  const MDCFooFoundation = mdcFoo.MDCFooFoundation;
});
```

## グローバル変数の使用

```javascript
const MDCFoo = mdc.foo.MDCFoo;
const MDCFooFoundation = mdc.foo.MDCFooFoundation;
```

## 自動インスタンス生成

```javascript
mdc.foo.MDCFoo.attachTo(document.querySelector('.mdc-foo'));
```

## 手動インスタンス生成

```javascript
import {MDCFoo} from '@material/foo';

const foo = new MDCFoo(document.querySelector('.mdc-foo'));
```
