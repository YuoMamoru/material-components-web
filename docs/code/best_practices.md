# ベストプラクティス

コードの一貫性を保ち、API をユーザーフレンドリーに保つために MDC Web は命名方法やドキュメントのペストプラクティスにしたがっています。結合を疎にするために分離のためのベストプラクティスにしたがっています。そしてコンポーネントの速さを維持するためにパフォーマンスのベストプラクティスにもしたがっています。

### 命名規則

* できる限り [仕様](https://material.io/guidelines) に沿うこと。仕様で使われている命名法がネイティブに実装された要素やパターンと矛盾するときはガイダンスのために手を挙げる。
* CSS クラスについては [BEM 命名規則](http://getbem.com/naming/) を使用する。

### ドキュメント

* ドキュメントは短く保ち、一つのことをするのに10の単語を使わない。
* マテリアルデザインのガイドラインは、いつ、どうしてコンポーネントを使わなくてはいけないのかを網羅している。

### 分離

* 決してファンデーション内で [要素](https://developer.mozilla.org/en-US/docs/Web/API/Element) を直接参照しない。

TODO: コンポーネントの仕様からサブシステムを分離する方法についての注意を記載する

### パフォーマンス

* アニメーションするプロパティは GPU 上で実行されるものだけにする。
* `requestAnimationFrame` を使用する。
* 不変で同期している DOM の読み書きを避ける。
* 合成されたレイヤの数を減らす。

### Typescript

#### 限定代入演算子
* MDC Web has other lifecycle methods (`initialize()` and `initSyncWithDom()`) that are not contained within the `constructor`.
* Typescript compiler cannot infer that the other methods are run in conjunction, and will throw an error on properties not defined.
* Feel free to use the `!` when you run into the error `<PROPERTY_NAME> has no initializer and is not definitely assigned in the constructor.`. ie.
* MDC Web には `constructor` に含まれない異なるライフサイクルのメソッド（`initialize()` と `initSyncWithDom()`）がある。
* Typescript コンパイラーはほかのメソッドが一緒に実行されていることを推論できず、定義されていないプロパティに対してエラーを発生させる。
* `<PROPERTY_NAME> has no initializer and is not definitely assigned in the constructor.` というエラーが発生した際には自由に `!` を使用する。つまり、

```
private progress_!: number; // Assigned in init

init() {
  this.progress_ = 0;
}
```

#### type vs. interface
* 型定義においては可能な限り `type` より `interface` を使う。

#### any vs. unknown vs. {}
* `any` 型と `{}` 型より `unknown` を使う。

* `any` と `{}` で選ばなくてはいけない場合は `{}` にする。

#### イベント
* `@material/base` ではイベントやイベントリスナーを扱うための便利な型（`EventType` と `SpecificEventListener`）を定義する。
* 標準的なイベント名（例えば `click` や `keydown`）であることを想定している場合は `string` 型よりも `EventType` 型を使う。
* どんな種類のイベントかがわかっている場合は `EventListener` 型より `SpecificEventListener` を使う。（例えば `SpecificEventHandler<'click'>`）

#### Node/Element/HTMLElement の使い分け
* `Node` は `Element` より一般的で、`Element` は `HTMLElement` より一般的。
* `Node` は、主に文書全体かコンテンツ/文言に対して使われる。
* `Element` は、対象の型が `HTMLElement`、`SVGElement` などをとりえるときに使うべき。
* `HTMLElement` DOM 要素、いくつか例を挙げると `<a>`、`<li>`、`<div>` といったものに対してのみ使用する。
* 実行時に可能な限り考えうる最も一般的な型を使う。
