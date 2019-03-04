<!--docs:
title: "Base"
layout: detail
section: components
excerpt: "Base foundation and component classes."
path: /catalog/base/
-->

# Base

MDC Base には MDC Web のファンデーションクラスとコンポーネントクラスのすべての基底クラスとして役に立つ中核となるファンデーションクラスとコンポーネントクラスが（それぞれ）含まれています。

多くの場合、 `mdc-base` に直接的に依存する必要はないでしょう。しかし、MDC Web のパターンにしたがい、MDC Web のエコシステムにきちんと統合するカスタムコンポーネントを作る必要があるなら、このパッケージが役立ちます。

## インストール

まず、モジュールをインストールします。

```
npm install @material/base
```

次に以下の方法のいずれかでコードにモジュールをインクルードします。

#### ES モジュール構文

```javascript
import {MDCComponent, MDCFoundation} from '@material/base';
```
#### CommonJS

```javascript
const MDCComponent = require('mdc-base').MDCComponent;
const MDCFoundation = require('mdc-base').MDCFoundation;
```

#### AMD

```javascript
require(['path/to/mdc-base'], function(mdcBase) {
  const MDCComponent = mdcBase.MDCComponent;
  const MDCFoundation = mdcBase.MDCFoundation;
});
```

#### Vanilla

```javascript
const MDCComponent = mdc.base.MDCComponent;
const MDCFoundation = mdc.base.MDCFoundation;
```

## 使用法

mdc-base は2つのクラス、すなわちすべてのコンポーネントを拡張する `MDCComponent` （デフォルトのエクスポート）とすべてのファンデーションクラスを拡張する `MDCFoundation` を公開しています。ファンデーションクラスとコンポーネントクラスについてより学ぶには [アーキテクチャーとベストプラクティス](../../docs/code) にある概要を参照してください。

### MDCFoundation

MDCFoundation はファンデーションクラスを実装するための基本的な仕組みを提供します。サブクラスは次のことをします。

- 必要なところに適切な静的ゲッタの実装を提供する。
- ライスサイクルメソッドとして `init()` と `destroy()` を提供する。

```javascript
import {MDCFoundation} from '@material/base/foundation';

export default class MyFoundation extends MDCFoundation {
  static get cssClasses() {
    return {
      ROOT: 'my-component',
      MESSAGE: 'my-component__message',
      BUTTON: 'my-component__button',
      TOGGLED: 'my-component--toggled'
    };
  }

  static get defaultAdapter() {
    return {
      toggleClass: (/* className: string */) => {},
      registerBtnClickHandler: (/* handler: Function */) => {},
      deregisterBtnClickHandler: (/* handler: Function */) => {}
    };
  }

  constructor(adapter) {
    super({...MyFoundation.defaultAdapter, ...adapter});
    const {TOGGLED} = MyFoundation.cssClasses;
    this.clickHandler_ = () => this.adapter_.toggleClass(TOGGLED);
  }

  init() {
    this.adapter_.registerBtnClickHandler(this.clickHandler_);
  }

  destroy() {
    this.adapter_.deregisterBtnClickHandler(this.clickHandler_);
  }
}
```

#### 静的ゲッタ

静的ゲッタはファンデーションクラスとコンポーネントの内部そしてサードパーティのコードのよって使用される定数を提示するものです。<em>これらのゲッタの中に常に定数を入れているということを覚えておくことは重要です</em>。これはコンポーネントができる限り多くの環境と相互利用できることを保証するものです。多くの環境というのにはホストライブラリ（例えば Closure Stylesheets）によって CSS クラスが上書きされる場合や文字列を変更する必要がある（例えば i18n のように）場合があります。

コンポーネントに何も指定されていないときは定数ゲッタを明示的に提供する必要がないことも気に留めておいてください。
提供されるゲッタは次のように指定します。

| ゲッタ | 説明 |
| --- | --- |
| `cssClasses` | コードの依存している CSS クラスをキーとするオブジェクトを返す。 |
| `strings` | 識別するための文字列定数、例えば `ARIA_ROLE` の値、をキーとするオブジェクトを返す。 |
| `numbers` | 各キーが見分けるための数値定数、例えば `TRANSITION_DELAY_MS` の値、のオブジェクトを返す。 |
| `defaultAdapter` | アダプターの形状（訳注: アダプターのインターフェースのこと）を指定するオブジェクトを返す。アダプターにとって機能的なデフォルトとしてだけでなく、アダプターの「スキーマ」を指定する方法をして利用できる。 |

#### ライフサイクルメソッド

各ファンデーションクラスは2つのライフサイクルメソッド、`init()` と `destroy()`、を持ちます。そのメソッドを以下に説明します。

| メソッド | 呼び出しタイミング | ユースケース |
| --- | --- | --- |
| `init()` | コンポーネントの初期がの準備が整ったとき、ホストクラスによって呼び出される | イベントリスナーの追加、アダプターによる情報の問い合わせなど |
| `destroy()` | コンポーネントが使用されなくなったとき、ホストクラスによって呼び出される | イベントリスナーの削除、一時的な状態のリセットなど |

### MDCComponent

MDCComponent はコンポーネントクラスの実装のための基本的な仕組みを提供します。

```javascript
import MyComponentFoundation from './foundation';

export class MyComponent extends MDCComponent {
  static attachTo(root) {
    return new MyComponent(root);
  }

  getDefaultFoundation() {
    const btn = this.root.querySelector(`.${MyComponentFoundation.cssClasses.BUTTON}`);
    return new MyComponentFoundation({
      toggleClass: className => {
        if (this.root.classList.contains(className)) {
          this.root.classList.remove(className);
          return;
        }
        this.root.classList.add(className);
      },
      registerBtnClickHandler: handler => btn.addEventListener('click', handler),
      deregisterBtnClickHandler: handler => btn.removeEventListener('click', handler)
    });
  }
}
```

#### プロパティ

`MDCComponent` は以下の「プライベート」なプロパティをサブクラスに提供します。

| プロパティ | 説明 |
| --- | --- |
| `root_` | 最初の引数としてコンストラクターに渡されるルート要素。 |
| `foundation_` | そのコンポーネントのファンデーションクラス。これはコンストラクターにオプションの第2引数としてわたされるか、 `getDefaultFoundation()` が呼び出された結果が設定される。 |

#### メソッド

`MDCComponent` はサブクラスに以下のメソッドを提供します。

| メソッド | 説明 |
| --- | --- |
| `initialize(...args)` | ルート要素がコンポーネントにアタッチされた後に呼び出さるが、ファンデーションがインスタンス化される <em>前に</em> 呼び出される。コンポーネントに渡されたルート要素より後ろのすべての位置引数はオプションの第2引数であるファンデーションも含めてこのメソッドに渡される。これは通常コンストラクター内で行う初期化をするにはちょうどいい場所である。 |
| `getDefaultFoundation()` | コンポーネントにとって適切に設定されたファンデーションクラスのインスタンスを返す。コンストラクター内でファンデーションクラスが与えられなかった場合に呼び出される。サブクラスでは **必ず** このメソッドを実装しなくてはならない。 |
| `initialSyncWithDOM()` | コンストラクター内で呼び出される。サブクラスがホストの DOM 要素と状態の最初の同期を取りたい場合、このメソッドを上書きする。例えばスライダーで、ホストとなる要素に値があらかじめ設定されているかどうかを確認して、それに応じてスライダーの初期状態を設定したいときなどである。ファンデーションクラスのライフサイクルメソッドと同様の注意点がこのメソッドにも適用されることに注意。デフォルトでは何もしない。 |
| `destroy()` | コンポーネントが破棄される際に追加でクリーンアップをしたいならサブクラスでこのメソッドを上書きする。例えばコンポーネントがウィンドウリサイズのリスナーを削除したいときに使用する。 |
| `listen(type: string, handler: EventListener)` | コンポーネントのルートノードに `type` で指定したイベントのリスナーを追加する。`this.root_.addEventListener` の単なる代替であることに注意。 |
| `unlisten(type: string, handler: EventListener)` | コンポーネントのルートノードからイベントリスナーを削除する。`this.root_.removeEventListener` の単なる代替であることに注意。 |
| `emit(type: string, data: Object, shouldBubble: boolean = false)` | コンポーネントのルートノードから詳細な `data` とともに `type` のカスタムイベントを送る。オプション引数としてイベントがバブリングするかどうかを指定する `shouldBubble` をとる。これは素のコンポーネント内でイベントを発生させる好ましい方法である。 |

#### 静的メソッド

継承されるメソッドメソッドに加えてサブクラスは以下の2つの（訳注: 当初は2つあったのもが1つ削除されたが、そのことがこの原文に反映されていないため「2つの」としている。正しくは「1つの」）静的メソッドがコードに実装しなくてはならない。

| メソッド | 説明 |
| --- | --- |
| `attachTo(root) => <ComponentClass>` | 与えられたルート要素を使ってインスタンスを生成し、返す便利なメソッドとしてサブクラスでこのメソッドを実装しなくてはならない。このメソッドは `mdc-auto-init` 内で使用され、将来的にはカスタムリントルールとして存在を強制されるようなる。 |

#### ファンデーションのライフサイクル操作

`MDCComponent` は <em>コンストラクター</em> 内でファンデーションの `init()` 関数を呼び、コンポーネント自身の _destroy()_ 関数内でファンデーションの `destroy()` 関数を呼びます。したがって、<em>destory() を上書きしたときは常に super() を呼ぶ</em> ことを忘れないことが重要です。

#### 初期化とコンストラクターのパラメーター

コンポーネントのコンストラクターに追加のパラメーターが必要なときは上に書いたように `initialize` メソッドを使うことができます。この一例は依存関係そして子コンポーネントを渡す時です。

```js
class MyComponent extends MDCComponent {
  initialize(childComponent = null) {
    this.child_ = childComponent ?
      childComponent : new ChildComponent(this.root_.querySelector('.child'));
  }

  getDefaultFoundation() {
    return new MyComponentFoundation({
      doSomethingWithChildComponent: () => this.child_.doSomething(),
      // ...
    });
  }
}
```

このコードは次のように呼び出せます。

```js
const childComponent = new ChildComponent(document.querySelector('.some-child'));
const myComponent = new MyComponent(
  document.querySelector('.my-component'), /* foundation */ undefined, childComponent
);
// myComponent を使う
```

> 注意: 望むのなら初期化されたファンデーションを渡すこともできます。上の例ではファンデーションを初期化せずに初期化の引数を渡す方法を簡単に示しています。

#### ベストプラクティス: アダプターを単純なままに保つ

アダプターが複雑になってきたと感じたら、複雑な部分を固有の実装にリファクタリングすることを考えるべきです。

```javascript
import MyComponentFoundation from './foundation';
import {toggleClass} from './util';

class MyComponent {
  // ...
  getDefaultFoundation() {
    return new MyComponentFoundation({
      toggleClass: className => util.toggleClass(this.root_, className),
      // ...
    });
  }
}
```

`./util` は次のようになっています。

```javascript
export function toggleClass(element, className) {
  if (root.classList.contains(className)) {
    root.classList.remove(className);
    return;
  }
  root.classList.add(className);
}
```

これは単にコンポーネントクラスの複雑さを軽減するばかりでなく、複雑なアダプターの機能が適切にテストされるようになります。

```javascript
test('toggleClass() removes a class when present on an element', t => {
  const root = document.createElement('div');
  root.classList.add('foo');

  util.toggleClass(root, 'foo');

  t.false(root.classList.contains('foo'));
  t.end();
});
```
