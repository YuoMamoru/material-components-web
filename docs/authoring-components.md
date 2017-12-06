<!--docs:
title: "Authoring Components"
layout: landing
section: docs
path: /docs/authoring-components/
-->

# コンポーネントの構成

このドキュメントは MDC-Web を直接利用する場合や MDC-Web とのインターフェースを持つ外部コンポーネントを開発する場合のどちらの場合でもリファレンスとして役立ちます。

> このプロジェクトはまだ開発の初期段階で、これらの実践はまた変わりうることに注意してください。これらは完全なリリースに近づくにつれ安定していきます。

* [誰のためのドキュメントか](#who-this-document-is-for)
* [コンポーネント構築の方法](#how-to-build-a-component)
  * [単純なコンポーネントのプロトタイプ](#start-with-a-simple-component-prototype)
  * [ホスト環境とのやりとりの確認](#identify-host-environment-interactions)
  * [アダプタインターフェースの作成](#create-the-adapter-interface)
  * [既存のコードをファンデーションに再構築](#refactor-your-existing-code-into-a-foundation)
  * [ファンデーション上のコンポーネントの構築とアダプタの提供](#build-a-component-on-top-of-that-foundation-providing-an-adapter)
* [よいコンポーネント作るには](#what-makes-a-good-component)
  * [完全にテストされたコード](#fully-tested-code)
  * [徹底的な文書化と厳密にバージョン管理されたアダプタインターフェース](#thoroughly-documented-and-strictly-versioned-adapter-interface)
  * [アクセシビリティ](#accessibility)
  * [RTL への意識](#rtl-awareness)
  * [テーマのサポート](#support-for-theming)
* [ベストプラクティス](#general-best-practices)
  * [ユーザの期待していることを実行する](#do-what-the-user-expects)
  * [アダプタインターフェースは単純かつ直感的なものにする](#design-adapter-interfaces-to-be-simple-and-intuitive)
  * [ファンデーションコード内でホストオブジェクトを参照しない](#do-not-reference-host-objects-within-foundation-code)
  * [デストラクタですべての参照を削除する](#clean-up-all-references-on-destruction)
* [Authoring components for MDC-Web](#authoring-components-for-mdc-web)
  * [File Structure](#file-structure)
  * [License Stanzas](#license-stanzas)
  * [Scss](#scss)
     * [Separate reusable variables and mixins from main scss](#separate-reusable-variables-and-mixins-from-main-scss)
     * [Follow the BEM Pattern](#follow-the-bem-pattern)
     * [Use mdc-theme for theming](#use-mdc-theme-for-theming)
     * [Use mdc-rtl for RTL support](#use-mdc-rtl-for-rtl-support)
  * [Javascript](#javascript)
     * [Define a static attachTo(root) method for every component](#define-a-static-attachtoroot-method-for-every-component)
     * [Define a defaultAdapter getter for every foundation](#define-a-defaultadapter-getter-for-every-foundation)
     * [Define all exported CSS classes, strings, and numbers as foundation constants.](#define-all-exported-css-classes-strings-and-numbers-as-foundation-constants)
     * [Extend components and foundations from mdc-base classes.](#extend-components-and-foundations-from-mdc-base-classes)
     * [Packages must be registered with our build infrastructure, and with material-components-web pkg](#packages-must-be-registered-with-our-build-infrastructure-and-with-material-components-web-pkg)
     * [Closure Compatibility](#closure-compatibility)
  * [Testing](#testing)
     * [Verify foundation's adapters](#verify-foundations-adapters)
     * [Use helper methods](#use-helper-methods)
     * [Use bel for DOM fixture](#use-bel-for-dom-fixture)
     * [Always clean up the DOM after every test](#always-clean-up-the-dom-after-every-test)
     * [Verify adapters via testdouble.](#verify-adapters-via-testdouble)

## <a name="who-this-document-is-for"></a>誰のためのドキュメントか

このドキュメントの最初の2つのセクションにはコンポーネント構築の考え方や良いコンポーネントの基準についての一般的なガイドラインを記載します。直接 MDC-Web を構築する場合にも MDC-Web と連携する外部コンポーネントを作成する場合にもコンポーネントの構築に関心のある人にはこれが役立つでしょう。3つ目のセクションでは特に MDC-Web のコンポーネント制作について説明します。このセクションはプロジェクトに直接貢献したい人に最適です。

このドキュメントはあなたがこのライブラリとそのアーキテクチャに精通していることを前提としています。もしそうでない場合はまず [アーキテクチャ](code/architecture.md) を読むことをお勧めします。もしこのプロジェクトに初めて触れるのであれば [入門ガイド](./getting-started.md) から始めるのが良いでしょう。

## <a name="how-to-build-a-component"></a>コンポーネント構築の方法

このセクションでは MDC-Web のための新しいコンポーネントの作成の背景にある考え方のアウトラインを示します。これは React の [Thinking in React](https://facebook.github.io/react/docs/thinking-in-react.html) という記事に触発されました。

何もない状態から取りかかり、コンポーネント/アダプタ/ファンデーション の実装にまっすぐ進むことは非常に困難であり、最悪の場合、生産性と実験性の観点から完全に不可能になってしまいます。そこで、しばしば<em>可能な限りもっとも簡単な方法でプロトタイプのコンポーネントを構築し、それからファンデーションとアダプタに向かって作業を進めます</em>。私たちはよくこの方法でステップを進めます。

このアプローチを実証するために私たちは **red-blue toggle** を構築します。これは赤い背景と青いテキストが入れ替わる非常に単純なトグルボタンです。マテリアルデザインのコンポーネントではありませんが、これを使って MDC-Web の構成がどのように考えられているかというコンセプトを説明します。

### <a name="start-with-a-simple-component-prototype"></a>単純なコンポーネントのプロトタイプ

最初にコンポーネントに取り掛かるにあたり、ファンデーションやアダプタを気にせずに素の HTML/CSS/JavaScript を使ってプロトタイプを構築することから始めます。次のコードが redblue-toggle のプロトタイプのコードです。[CodePen](http://codepen.io/traviskaufman/pen/jVxdNo) でコードを見ることもできます。

> **ヒント**: コメントを試すときは [この CodePen テンプレート](http://codepen.io/traviskaufman/pen/pNQmRp) を出発点とすることもできます。

最初に DOM を使って試しすことから始め、動的な機能を試すために単純なコンポーネントを書いてみましょう。

```html
<div class="redblue-toggle" role="button" aria-pressed="false">
  Toggle <span class="redblue-toggle__color">Blue</span>
</div>
```

```js
class RedblueTogglePrototype {
  get toggled() {
    return this.root.getAttribute('aria-pressed') === 'true';
  }

  set toggled(toggled) {
    this.toggle(toggled);
  }

  constructor(root) {
    this.root = root;
    this.clickHandler_ = () => this.toggle();
    this.initialize();
  }

  initialize() {
    this.root.addEventListener('click', this.clickHandler_);
  }

  destroy() {
    this.root.removeEventListener('click', this.clickHandler_);
  }

  toggle(isToggled = undefined) {
    const wasToggledExplicitlySet = isToggled === Boolean(isToggled);
    const toggled = wasToggledExplicitlySet ? isToggled : !this.toggled;
    const toggleColorEl = this.root.querySelector('.redblue-toggle__color');
    let toggleColor;

    this.root.setAttribute('aria-pressed', String(toggled));
    if (toggled) {
      toggleColor = 'Red';
      this.root.classList.add('redblue-toggle--toggled');
    } else {
      toggleColor = 'Blue';
      this.root.classList.remove('redblue-toggle--toggled');
    }
    toggleColorEl.textContent = toggleColor;
  }
}

new RedblueTogglePrototype(document.querySelector('.redblue-toggle'));
```

この JS コンポーネントは MDC-Web を少しも参照しておらず、ファンデーションやアダプタの概念を持っていないことに注意してください。こういったことをしないことにより、素早くコンポーネントを試してみることができ、早く簡単に変更を行うことができます。それにもかかわらずこのプロトタイプのコンポーネントのやり方は MDC-Web コンポーネントの構築によるやり方に結局のところとても似ています。

### <a name="identify-host-environment-interactions"></a>ホスト環境とのやりとりの確認

一旦プロトタイプができれば、次のステップはアダプタを通して機能させることが必要であるということを理解することです。ホスト環境との直接的なやりとりは代わりにやってくれるものを必要としています。機能は Web プラットフォーム上のすべてのフレームワークに統合できるできるようするべきだからです（訳注: ホスト環境と直接的なやりとりを行う API を使うとホスト環境を提供するフレームワークとの統合ができてもそれ以外のフレームワークでの適用が難しくなるのでホスト環境の API をラップするものを用意したほうが良いということ）。

> 私たちのアーキテクチャドキュメントについて簡単に説明すると、**ホスト環境** という用語はコンポーネントを使用している環境という意味で使っています。[React-Native](https://facebook.github.io/react-native/) のような技術の場合はブラウザであったりコンポーネントを描画するサーバー、仮想DOM環境、はたまたモバイルアプリケーションといったものを指します。

redblue-toggle ではホスト環境とのやりに関するすべてのインスタンスをとても簡単に見ることができます。`root` ノードに対する読み書きしているところを確認すればよいのです。

- 切り替える際に `setAttribute` で `aria-pressed` を更新
- 切り替える際に `classList.{add,remove}` で root ノードのクラスを更新
- 切り替える際に色名を表示している子要素をの `textContent` を設定
- `initialize()`/`destroy()` を使って root ノードのイベントリスナーをそれぞれ追加または削除

それ以外のケースではホスト環境とのやりとりは `window.addEventListener('resize', ...)` のように単純ではない場合があります。これらもホスト環境のやりとりの例であり、気に留めておく必要があります。

### <a name="create-the-adapter-interface"></a>アダプタインターフェースの作成

ホスト環境とのやりとりが明らかになったので、アダプターインターフェースをこのコンポーネントに構築していきます。

```js
class RedblueTogglePrototype {
  get toggled() {
    return SOMEHOW_GET_ATTRIBUTE('aria-pressed') === 'true';
  }

  set toggled(toggled) {
    this.toggle(toggled);
  }

  constructor(root) {
    this.root = root;
    this.clickHandler_ = () => this.toggle();
    this.initialize();
  }

  initialize() {
    SOMEHOW_REGISTER_INTERACTION_HANDLER('click', this.clickHandler_);
  }

  destroy() {
    SOMEHOW_UNREGISTER_INTERACTION_HANDLER('click', this.clickHandler_);
  }

  toggle(isToggled = undefined) {
    const wasToggledExplicitlySet = isToggled === Boolean(isToggled);
    const toggled = wasToggledExplicitlySet ? isToggled : !this.toggled;

    let toggleColor;

    SOMEHOW_SET_ATTRIBUTE('aria-pressed', String(toggled));
    if (toggled) {
      toggleColor = 'Red';
      SOMEHOW_ADD_CLASS('redblue-toggle--toggled');
    } else {
      toggleColor = 'Blue';
      SOMEHOW_REMOVE_CLASS('redblue-toggle--toggled');
    }
    SOMEHOW_UPDATE_TOGGLE_COLOR_TEXT_CONTENT(toggleColor);
  }
}
```

上記のコードではホスト環境とのやりとりがすべてフェイクの `SOMEHOW_*` メソッドに置き換えられています。私たちはこのフェイクのメソッドを取り出し、アダプターインターフェースに変換することができます。

| フェイクメソッド | アダプタメソッド |
| --- | --- |
| SOMEHOW_GET_ATTRIBUTE(attr: string) => string | getAttr(attr: string) => string |
| SOMEHOW_SET_ATTRIBUTE(attr: string, value: string) | setAttr(attr: string, value: string) |
| SOMEHOW_ADD_CLASS(className: string) | addClass(className: string) |
| SOMEHOW_REMOVE_CLASS(className: string) | removeClass(className: string) |
| SOMEHOW_UPDATE_TOGGLE_COLOR_TEXT_CONTENT(textContent: string) | setToggleColorTextContent(textContent: string) |
| SOMEHOW_REGISTER_INTERACTION_HANDLER(type: string, handler: EventListener) | registerInteractionHandler(type: string, handler: EventListener) |
| SOMEHOW_DEREGISTER_INTERACTION_HANDLER(type: string, handler: EventListener) | deregisterInteractionHandler(type: string, handler: EventListener) |

> 注意: 私たちはコードにおいて、イベントリスナを追加/削除をおこなうのアダプタメソッドとして `registerInteractionHandler` と `deregisterInteractionHandler` という用語を使うことを使うことを慣習としています。私たちがそのような用語を使うのは大半のコンポーネントはやりとりに対してのみ関心を持っているというように感じているからです。しかし、これらのメソッドを `{add,remove}EventListener` やそれ以外の好きな名前をつけても構いません。

### <a name="refactor-your-existing-code-into-a-foundation"></a>既存のコードをファンデーションに再構築

アダプタAPIを定義しましたが、このコードをファンデーションクラスに書き直すことができます。慣習として、なにもしない各関数をもつアダプタを返す静的な `defaultAdapter` ゲッタを定義します。このメソッドは私たちがアダプタの形式を確認するのに役立ち、メソッドの実装を忘れた際にアダプタがエラーを返すことを防ぎ、将来リントツールがアダプタの形式が適切であること強制するため使うことができます（使うべきです）。その例を示しますが、これは `MDCFoundation` クラスの使用例でもあります。このクラスはすべてのファンデーションクラスの基底クラスです。

```js
class RedblueToggleFoundation extends MDCFoundation {
  static get defaultAdapter() {
    return {
      getAttr: (/* attr: string */) => /* string */ '',
      setAttr: (/* attr: string, value: string */) => {},
      addClass: (/* className: string */) => {},
      removeClass: (/* className: string */) => {},
      setToggleColorTextContent: (/* textContent: string */) => {},
      registerInteractionHandler: (/* type: string, handler: EventListener */) => {},
      deregisterInteractionHandler: (/* type: string, handler: EventListener */) => {}
    };
  }

  constructor(adapter) {
    super(Object.assign(RedblueToggleFoundation.defaultAdapter, adapter));
    this.toggled_ = false;
    this.clickHandler_ = () => this.toggle();
  }

  init() {
    this.adapter_.registerInteractionHandler('click', this.clickHandler_);
  }

  destroy() {
    this.adapter_.deregisterInteractionHandler('click', this.clickHandler_);
  }

  isToggled() {
    return this.adapter_.getAttr('aria-pressed') === 'true';
  }

  toggle(isToggled = undefined) {
    const wasToggledExplicitlySet = isToggled === Boolean(isToggled);
    this.toggled_ = wasToggledExplicitlySet ? isToggled : !this.toggled_;

    let toggleColor;

    this.adapter_.setAttr('aria-pressed', String(this.toggled_));
    if (this.toggled_) {
      toggleColor = 'Red';
      this.adapter_.addClass('redblue-toggle--toggled');
    } else {
      toggleColor = 'Blue';
      this.adapter_.removeClass('redblue-toggle--toggled');
    }
    this.adapter_.setToggleColorTextContent(toggleColor);
  }
}
```

セッタとゲッタの代わりに `isToggled()` と `toggle()` が使われていることに注意してください。このファンデーションは低レベルな API であることを考えると、この慣習が適切であると思われます。

### <a name="build-a-component-on-top-of-that-foundation-providing-an-adapter"></a>ファンデーション上のコンポーネントの構築とアダプタの提供

最後のステップは上記のファンデーションを使い、コンポーネントを構築することです。コンポーネントは2つの主な役割を持っています。

* ホスト環境内にファンデーションのもつ機能へのイディオム的なインターフェースを提供する
* ホスト環境内で動作するファンデーションへのアダプタを提供する

このコンポーネントは素のコンポーネントなので、素の DOM API をならって作ることになります。素の DOM API はこれらの機能を実装することになるセッタやゲッタにとって好都合です（`checked`, `disabled` などを考えてみてください）。ここで実装するメソッドは簡単に再利用可能なのでアダプタは極めて簡単なものになります。

```js
class RedblueToggle extends MDCComponent {
  get toggled() {
    return this.foundations_.isToggled();
  }

  set toggled(toggled) {
    this.foundation_.toggle(toggled);
  }

  getDefaultFoundation() {
    return new RedblueToggleFoundation({
      getAttr: attr => this.root_.getAttribute(attr),
      setAttr: (attr, value) => this.root_.setAttribute(attr, value),
      addClass: className => this.root_.classList.add(className),
      removeClass: className => this.root_.classList.remove(className),
      setToggleColorTextContent: textContent => {
        this.root_.querySelector('.redblue-toggle__color').textContent = textContent;
      },
      registerInteractionHandler: (type, handler) => this.root_.addEventListener(type, handler),
      deregisterInteractionHandler: (type, handler) => this.root_.removeEventListener(type, handler)
    });
  }
}
```

このコードは [CodePen 上の最終的なサンプル](http://codepen.io/traviskaufman/pen/gLExme?editors=0010) で見ることができます。

## <a name="what-makes-a-good-component"></a>よいコンポーネント作るには

これらの追加のガイドラインはあなた自身のコンポーネントを作る際に「チェックリスト」を提供します。私たちはコードを書く上でおいてこれらを厳格に守っており、厳格に守ることであなたのコンポーネントの利用者にとって素晴らしい経験を確実なものにするでしょう。

### <a name="fully-tested-code"></a>完全にテストされたコード

ECMAScript は設計上、動的かつ柔軟な言語です。動的で柔軟であることの利点はプログラムの正しさを検証するコストにもなります。コードが期待通りに動作していることを検証する唯一の方法はコードを実行し結果が期待したものであるかを検証することです。ファンデーション、アダプタ、コンポーネントのテストカバレッジが100%になるよう努力してください。

### <a name="thoroughly-documented-and-strictly-versioned-adapter-interface"></a>徹底的な文書化と厳密にバージョン管理されたアダプタインターフェース

フレームワークの開発者はあなたのアダプタインターフェース周りコードを設計しいくので、あなたが開発者に設計のために必要な情報をすべて提供することは重要ことです。私たちの推奨する方法はコンポーネントの README にアダプターのインターフェースを文書化し、メソッドの期待された振る舞いはもちろんのこと、メソッドの使い方も文書に提供することです。

同様に重要なことは <em>アダプターインターフェースを厳格にバージョン管理すること</em> です。アダプターインターフェースが変わると既存の実装部分が壊れたり、新しいアダプターメソッドの実装とつながらなくなることによりコンポーネントの重要な部分が失われているにもかかわらず実装者は正しく期待通りにコードが動いているように思ったりする可能性があります。私たちは <em>それぞれの変更はアダプターインターフェースの破壊的な変更</em> であると考え、このやり方を推奨します。

### <a name="accessibility"></a>アクセシビリティ

すべての主要なコンポーネントが完全にアクセス可能であることが必要です。私たちは [ARIA 仕様書](https://www.w3.org/WAI/intro/aria) を実装することが理にかなっており、コンポーネントの動作に関しては可能な限り意味を持つことを保証するようにしています。[Accessibility Developer Tools](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en) はコンポーネントがどの程度アクセシビリティを待つのかを分析する優れた方法です。

### <a name="rtl-awareness"></a>RTL への意識

コンポーネントは RTL 対応にすべきです。すなわち、RTL コンテキストかどうかを検出するための何らかの戦略がコンポーネントになくてはならず、そうれに応じて適切に調整しなくてはなりません。私たちはこれを支援するために [@material/rtl](../packages/mdc-rtl) ライブラリを使用します。

### <a name="support-for-theming"></a>テーマのサポート

コンポーネントは **テーマ** に応じて変更できなくてはなりません。テーマは様々な方法で定義できます。_primary_ と _secondary_ の色を指定する方法や、公開された scss 変数や CSS カスタムプロパティをコンポーネントで選ぶこともできます。どの方法をえらんでも <em>クライアントが全体的なデザインに合わせて容易にコンポーネントの共通な美的要素を変更できます</em>。この目的で私たちは [@material/theme](../packages/mdc-theme) を使います。

## <a name="general-best-practices"></a>ベストプラクティス

コンポーネントが上記の要件を満たしている場合でも落とし穴にはまるかもしれません。落とし穴や予期せぬ状況を可能な限り回避するために以下の推奨事項に従ってください。

> すべてのベストプラクティスがそうであるように、このベストプラクティスは厳格で揺るがないルールではなく <em>ガイドライン</em> であることを気に留めておくことは重要です。[もしベストプラクティスがコンポーネントの改善や維持を妨げるようであれば無視してください](https://en.wikipedia.org/wiki/Wikipedia:Ignore_all_rules)。しかし、なるべくドキュメントやコメントとして軽視したことの理由を示してください。

### <a name="do-what-the-user-expects"></a>ユーザの期待していることを実行する

これは私たちの「黄金の掟 (golden rule)」です。<em>コンポーネントの API は直感的でわかりやすいものになるよう設計してください。コンポーネントはユーザの予想通りのふるまいをするようにしてください。</em>例えば `MDCCheckbox` の `checked` ゲッタはチェックボックスの内部状態がチェックされているかどうかを表す真偽値を返してください。副作用ががなく、`type` が `"checkbox"` であるときは `HTMLInputElement.prototype.checked` とまったく同じ方法で動作するようにします。コンポーネントを設計する際には、ユーザがどのように使うのかを想像したことをもとに作ってください。私たちのケースでは素のコンポーネント（訳注: 手を入れていない MDC-Web の素のコンポーネントのこと）は DOM API をもとに作っています。

### <a name="design-adapter-interfaces-to-be-simple-and-ntuitive"></a>アダプタインターフェースは単純かつ直感的なものにする

このルールは先に述べたユーザの期待しているものを作るというプラクティスに則ったものです。ライブラリの利用者はアダプタメソッドを実装することになるので、アダプタメソッドは実装することが簡単であるだけでなく、本質的に簡素で直感的でなくてはなりません。大半のアダプタメソッドは「クラスを加える」や「プロパティのスタイルを更新する」といったように一言で記述できるべきです。アダプタメソッドの目的は何かとかインプットとアウトプットが何かとかをユーザが推測するようではいけません。

例えば良いアダプタインターフェースは次のようになっています。

| メソッド | 説明 |
| --- | --- |
| `setStyle(styleProperty: string, value: string) => void` | ダッシュで連結された `styleProperty` とそのプロパティの `value` を指定してルート要素のスタイルを設定する。 |

対して悪いアダプタインターフェースは次のようになっています。

| メソッド | 説明 |
| --- | --- |
| `applyComponentStyles() => void` | コンポーネントのルート要素に適切なスタイルを設定する。詳細はドキュメントを参照のこと。 |

上記のアダプタインターフェースはファンデーションメソッドのほうがふさわしいです。アダプタの唯一の責務はスタイルを更新することであるべきで、スタイルを決定することではありません。

### <a name="do-not-reference-host-objects-within-foundation-code"></a>ファンデーションコード内でホストオブジェクトを参照しない

ファンデーションに可能な限り多くのフレームワークと互換性を持たせるために、ファンデーション内でホストオブジェクトを直接参照することを避けてください。ホストオブジェクトには `window`、 `document`、 `console` などを含みます。<em>ファンデーション内では ECMAScript 仕様で定義されたグローバルオブジェクトのみを参照するようにします。</em>

`requestAnimationFrame` はこのルールの例外ですが、私たちは将来リファクタリングするでしょう。加えて、ファンデーション内でホストオブジェクトを使用することの回避策はアダプタを介してホストオブジェクトを使用することです。しかし、ホストオブジェクト自身の [名目型]() よりもむしろホストオブジェクトの代理となる [構造型]() を返すようなアダプタ API を設計すべきです。例えば、タイプが `"checkbox"` の `HTMLInputElement` を使う代わりに `checked`、 `indeterminate`、 `disabled` という真偽値プロパティを持つオブジェクトを使ってください。

### <a name="clean-up-all-references-on-destruction"></a>デストラクタですべての参照を削除する

このプラクティスはイベントハンドラ、タイマー ID、アニメーションフレーム ID、保持される可能性のあるその他の外部参照を含みます。このプラクティスが実施されているかを確認するために2つの正確なリトマステストがあります。

1. `init()` （もしくは素のコンポーネントにおける  `initialize()`）と `destroy()` が対称的になっている。例えば `init()` でアタッチされたすべてのイベントリスナーは `destroy()` で削除されている。
2. 外部参照を作成するすべての呼び出し（例: `setTimeout()`、`requestAnimationFrame()`）は追跡され、破棄する際にクリーンアップされる。例えばすべての `setTimeout()` 呼び出しはファンデーションやコンポーネントによって ID が保持され、破棄される際には `clearTimeout()` が破棄する処理の中で呼ばれる。

## Authoring components for MDC-Web

The following guidelines are for those who wish to contribute directly to MDC-web. In addition to
adhering to all of the practices above, we have additional conventions we expect contributors to
adhere to. It's worth noting that most of these conventions - including our coding style, commit
message format, and test coverage - are _automatically enforced via linters_, both so that
contributors can move quickly and confidently, and core team members do not have to waste time and
energy nitpicking on pull requests.

### File Structure

All source files for a component reside under `packages/`. All test files reside under `test/unit`,
which mirrors the `packages/` directory. Demos for each component are located under `demos/`.

A typical component within our codebase looks like so:

```
packages
  ├── mdc-component
      ├── README.md # The component's README
      ├── constants.js # The component's cssClasses/strings/numbers constants
      ├── foundation.js # The component's foundation class
      ├── index.js # The file that contains the vanilla component class, as well as exports the foundation
      ├── mdc-component.scss # The main source file for the component's CSS
      └── package.json # The components package file
test/unit
  ├── mdc-component
      ├── foundation.test.js # Unit tests for the component's foundation
      ├── mdc-component.test.js # Unit tests for the component's
demos
  ├── component.html
```

**Every component _must_ have these files before we will accept a PR for them.**

When contributing a new component, we encourage you to look at existing components to get a better
sense of our conventions. Your new component should "blend in" with all existing components.

Additionally, all new components require the following within their `package.json`:

```
"publishConfig": {
  "access": "public"
}
```

This is needed so that lerna will be able to automatically publish new scoped packages.

We also require a list of keywords for each package. This list should always include `material components` and `material design`, followed by the component name:

```
"keywords": [
  "material components",
  "material design",
  <COMPONENT_NAME>
]
```

For example, if you are building a checkbox component, `keywords` would include `material components`, `material design`, and `checkbox`

**Below is an example of what a full `package.json` should look like for a new component:**

```json
{
  "name": "@material/example",
  "version": "0.0.0",
  "description": "The Material Components for the web example component",
  "license": "Apache-2.0",
  "repository": {
    "type": "git",
    "url": "https://github.com/material-components/material-components-web.git"
  },
  "keywords": [
    "material components",
    "material design",
    "example"
  ],
  "publishConfig": {
    "access": "public"
  }
}
```

### License Stanzas

We are required to put the following at the _top_ of _every source code file_, including tests,
demos, and demo html. The stanza is as follows:

```
Copyright 2016 Google Inc. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

Please put this in a comment at the top of every source file.

### Scss

#### Separate reusable variables and mixins from main scss

If variables and mixins are intended to be used outside of a single stylesheet, refactor them out
into [sass partials](http://sass-lang.com/guide#topic-4). These files can then be included in other
stylesheets without having extra CSS omitted both times. As a rule of thumb, _never `@import` sass
files which output CSS`, as it will most likely be duplicate output.

#### Follow the BEM Pattern
We follow a modified version of the [BEM](http://getbem.com/) pattern, which is defined within our
[stylelint rules](../.stylelintrc.yaml#L252-L255). It's basically:

```scss
.mdc-block {

}

.mdc-block__element {

}

.mdc-block--modifier {

}
```

Usually, we structure it within our code as such:

```scss
.mdc-block {
  // ...

  &__element {
    // ...
  }
}

.mdc-block--modifier {
  // ...

  .mdc-block__element {
    // ...
  }
}
```

Sometimes, you'll need to qualify selectors, which such as `.some-context .mdc-block {/* ... */}`.
Stylelint will complain about this, which you can disable by inserting the following:

```scss
// stylelint-disable plugin/selector-bem-pattern

// styles select-bem-pattern complains about...

// stylelint-enable plugin/selector-bem-pattern
```

#### Use mdc-theme for theming
All thematic elements of a component should be specified via [mdc-theme](../packages/mdc-theme).
This will ensure that the component integrates harmoniously into our theming system.

#### Use mdc-rtl for RTL support
All RTL treatments within a component's style should be specified via [mdc-rtl](../packages/mdc-rtl).
This will ensure that all components treat RTL contexts the same way, and will behave consistently.

### Javascript

#### Define a static attachTo(root) method for every component

All components _must_ define a static `attachTo` method with the following signature:

`static attachTo(element: HTMLElement) => Constructor`

e.g.

```js
class MDCNewComponent extends MDCComponent {
  static attachTo(root) {
    return new MDCNewComponent(root);
  }
}
```

`mdc-auto-init` requires this method to be present, and we guarantee its provision as a convenience
to our users. We have spoken about writing a lint rule for this in the future.

#### Define a defaultAdapter getter for every foundation
All foundations _must_ define a static `defaultAdapter` method which returns an adapter with all
functions defined. The functions should essentially be NOPs; taking no parameters and returning the
correct type (e.g. `false` for boolean, `0` for number, `{}` for object, etc.). Our convention is
to annotate the function via inline comments using [Typescript's type annotations](https://basarat.gitbooks.io/typescript/content/docs/types/type-system.html).

It is also a convention to override a foundation's constructor to mix in the passed `adapter` param
to a default adapter object. This ensures that the adapter is guaranteed to have the correct shape.

```js
class MDCNewComponentFoundation extends MDCFoundation {
  static get defaultAdapter() {
    return {
      addClass: (/* className: string */) => {},
      getAttr: (/* attr: string */) => /* string */ '',
      // ...
    }
  }

  constructor(adapter) {
    super(Object.assign(MDCNewComponentFoundation.defaultAdapter, adapter));
  }
}
```

This of course comes at the cost of potentially obscuring erroneous passed in adapters. However,
we plan on providing type definitions for adapters in the future to help assuage this. Similar to
the aforementioned rule, we would also like to provide lint rules to enforce these conventions.

#### Define all exported CSS classes, strings, and numbers as foundation constants.
- All CSS Classes referenced by a component's foundation must be referenced by a `cssClasses` static
  getter.
- All strings that are used outside the context of the foundation class (CSS selectors, custom event names,
  text that could potentially be localized, etc.) must be referenced by a `strings` static getter.
- All semantic numbers leveraged by the foundation (timeout lengths, transition durations, etc.) must
  be referenced by a `numbers` static getter.
- These constants should be defined within a `constants.js` file, and then proxied through the
  foundation.

```js
// constants.js

export const cssClasses = {
  ROOT: 'mdc-new-component',
  ACTIVE: 'mdc-new-component--active',
  DISABLED: 'mdc-new-component--disabled',
};

export const strings = {
  CHILD_SELECTOR: '.mdc-new-component__child',
  CUSTOM_EVENT: 'MDCNewComponent:event',
};

export const numbers = {
  DEFAULT_THROTTLE_DELAY_MS: 300,
};

// foundation.js

import {cssClasses, strings, numbers} from './constants';

class MDCNewComponentFoundation extends MDCFoundation {
  static get defaultAdapter() {
    // ...
  }

  static get cssClasses() {
    return cssClasses;
  }

  static get strings() {
    return strings;
  }

  static get numbers() {
    return numbers;
  }
}
```

The primary purpose of this is so that our components can interoperate with aspects of Google's
front-end infrastructure, such as Closure Stylesheets' [CSS Class Renaming](https://github.com/google/closure-stylesheets#renaming) mechanism. In addition, it
provides the added benefit of semantic code, and less magic strings/numbers.

#### Extend components and foundations from mdc-base classes.
To ensure that all packages behave consistently, all components must extend `MDCComponent` and all
foundations must extend `MDCFoundation`. More information for both of these classes can be found in
the [mdc-base README](../packages/mdc-base).

#### Packages must be registered with our build infrastructure, and with material-components-web pkg
Whenever you create a new component, it's important to notify the proper tools and packages of it.
Concretely:

- Ensure that an entry for it exists in `webpack.config.js` for the `js-components` and `css` module
- Ensure that it is added as a dependency of `material-components-web`. If the component contains
  styles, ensure that they are `@import`ed within `material-components-web.scss`. If the component
  contains javascript, ensure that its component namespace is exported within
  `material-components-web`, and it is registered with `mdc-auto-init`. Lastly, remember to add it
  to `package.json` of `material-components-web`.
- Ensure that the correct **commit subject** for the package is added to the
  `config.validate-commit-msg.scope.allowed` array within the top-level `package.json` at the root
  of the repo. The commit subject is the _name the component, without the `mdc-`/`@material/`_.
  E.g., for `mdc-icon-toggle`, the correct subject is `icon-toggle`.
- Ensure that the package name is added to the `closureWhitelist` array within the top-level
  `package.json`.

#### Closure Compatibility

> NOTE: This section was introduced as part of our [closure compatibility milestone](https://github.com/material-components/material-components-web/milestone/4). Our
currently existing components are in the process of being made compatible with closure.

All core MDC-Web components must be fully compatible with the Google Closure Compiler using its
advanced compilation mechanisms. We've provided a thorough explanation of this, as well as
conventions, examples, and common closure patterns you may not be used to, in our [closure compiler documentation](./closure-compiler.md).

### Testing

The following guidelines should be used to help write tests for MDC-Web code. Our tests are written
using [mocha](https://mochajs.org/) with the [qunit UI](https://mochajs.org/#qunit), and are driven by [karma](https://karma-runner.github.io/1.0/index.html). We use the [chai assert API](http://chaijs.com/api/assert/)
for assertions, and [testdouble](https://github.com/testdouble/testdouble.js/) for mocking and stubbing.

#### Verify foundation's adapters
When testing foundations, ensure that at least one of your test cases uses the
`verifyDefaultAdapter` method defined with our [foundation helpers](../test/unit/helpers/foundation.js). This is done to ensure that adapter interfaces do not
change unexpectedly.

#### Use helper methods
We have helper modules within [test/unit/helpers](../test/unit/helpers) for things like
bootstrapping foundation tests, intercepting adapter methods used for listening to events, and
dealing with `requestAnimationFrame`. We encourage you to make use of them in your code to make it
as easy as possible to write tests!

#### Use bel for DOM fixture
We use the [bel](https://www.npmjs.com/package/bel) library to generate fixtures for our component/adapter tests. We've found it to
be an easy and successful way to bootstrap fixtures without having to worry about maintaining HTML
files or write unwieldy DOM API code.

#### Always clean up the DOM after every test
This is important. _Before a test ends, ensure that any elements attached to the DOM have been
removed_.

#### Verify adapters via testdouble.
We use [testdouble.js](https://github.com/testdouble/testdouble.js) as our de-facto mocking
framework. A huge benefit to the component/foundation/adapter pattern is it makes testing the
functionality of our components extremely easy. We encourage you to make use of testdouble stubs for
adapters and use them to verify your foundation's behavior (note that this is what [our foundation setup code](../test/unit/helpers/setup.js#L21) does by default).
