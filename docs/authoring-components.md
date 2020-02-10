<!--docs:
title: "Authoring Components"
layout: landing
section: docs
path: /docs/authoring-components/
-->

# コンポーネントの構成

このドキュメントは MDC Web を直接利用する場合や MDC Web とのインターフェースを持つ外部コンポーネントを開発する場合のどちらの場合でもリファレンスとして役立ちます。

> このプロジェクトはまだ開発の初期段階で、これらの実践はまた変わりうることに注意してください。これらは完全なリリースに近づくにつれ安定していきます。

- [コンポーネントの構成](#authoring-components)
  - [誰のためのドキュメントか](#who-this-document-is-for)
  - [コンポーネント構築の方法](#how-to-build-a-component)
    - [単純なコンポーネントのプロトタイプ](#start-with-a-simple-component-prototype)
    - [ホスト環境とのやりとりの確認](#identify-host-environment-interactions)
    - [アダプターインターフェースの作成](#create-the-adapter-interface)
    - [既存のコードをファンデーションに再構築](#refactor-your-existing-code-into-a-foundation)
    - [ファンデーション上のコンポーネントの構築とアダプターの提供](#build-a-component-on-top-of-that-foundation-providing-an-adapter)
  - [よいコンポーネント作るには](#what-makes-a-good-component)
    - [完全にテストされたコード](#fully-tested-code)
    - [徹底的な文書化と厳密にバージョン管理されたアダプターインターフェース](#thoroughly-documented-and-strictly-versioned-adapter-interface)
    - [アクセシビリティ](#accessibility)
    - [RTL への意識](#rtl-awareness)
    - [テーマのサポート](#support-for-theming)
  - [ベストプラクティス](#general-best-practices)
    - [ユーザーの期待していることを実行する](#do-what-the-user-expects)
    - [アダプターインターフェースは単純かつ直感的なものにする](#design-adapter-interfaces-to-be-simple-and-intuitive)
    - [ファンデーションコード内でホストオブジェクトを参照しない](#do-not-reference-host-objects-within-foundation-code)
    - [デストラクターですべての参照を削除する](#clean-up-all-references-on-destruction)
  - [MDC Web のコンポーネントの作成](#authoring-components-for-mdc-web)
    - [ファイル構成](#file-structure)
    - [ライセンスの記載](#license-stanzas)
    - [Scss](#scss)
      - [再利用可能な変数とミキシンをメインの scss から分離する](#separate-reusable-variables-and-mixins-from-main-scss)
      - [BEM の様式にしたがう](#follow-the-bem-pattern)
      - [テーマの設定には mdc-theme を使う](#use-mdc-theme-for-theming)
      - [RTL のサポートには mdc-rtl を使う](#use-mdc-rtl-for-rtl-support)
    - [Javascript](#javascript)
      - [すべてのコンポーネントに静的メソッド attachTo(root) を定義する](#define-a-static-attachtoroot-method-for-every-component)
      - [すべてのファンデーションにゲッタ defaultAdapter を定義する](#define-a-defaultadapter-getter-for-every-foundation)
      - [外部参照されるすべての CSS クラス、文字列、数値をファンデーションの定数として定義する](#define-all-exported-css-classes-strings-and-numbers-as-foundation-constants)
      - [コンポーネントとファンデーションは mdc-base のクラスを継承して作成する](#extend-components-and-foundations-from-mdc-base-classes)
      - [パッケージをビルドインフラおよび material-components-web パッケージに登録しなくてはいけない](#packages-must-be-registered-with-our-build-infrastructure-and-with-material-components-web-pkg)
      - [TypeScript との互換性](#typescript-compatibility)
    - [テスト](#testing)
      - [ファンデーションのアダプターを検証する](#verify-foundations-adapters)
      - [ヘルパーメソッドを使う](#use-helper-methods)
      - [DOM フィクスチャーに bel を使う](#use-bel-for-dom-fixture)
      - [あらゆるテストの後は常に DOM をきれいにする](#always-clean-up-the-dom-after-every-test)
      - [testdouble を通じてアダプターの検証をする](#verify-adapters-via-testdouble)

## <a name="who-this-document-is-for"></a>誰のためのドキュメントか

このドキュメントの最初の2つのセクションにはコンポーネント構築の考え方や良いコンポーネントの基準についての一般的なガイドラインを記載します。直接 MDC Web を構築する場合にも MDC Web と連携する外部コンポーネントを作成する場合にもコンポーネントの構築に関心のある人にはこれが役立つでしょう。3つ目のセクションでは特に MDC Web のコンポーネント制作について説明します。このセクションはプロジェクトに直接貢献したい人に最適です。

このドキュメントはあなたがこのライブラリとそのアーキテクチャーに精通していることを前提としています。もしそうでない場合はまず [アーキテクチャー](code/architecture.md) を読むことをお勧めします。もしこのプロジェクトに初めて触れるのであれば [入門ガイド](./getting-started.md) から始めるのが良いでしょう。

## <a name="how-to-build-a-component"></a>コンポーネント構築の方法

このセクションでは MDC Web のための新しいコンポーネントの作成の背景にある考え方のアウトラインを示します。これは React の [Thinking in React](https://facebook.github.io/react/docs/thinking-in-react.html) という記事に触発されました。

何もない状態から取りかかり、コンポーネント/アダプター/ファンデーション の実装にまっすぐ進むことは非常に困難であり、最悪の場合、生産性と実験性の観点から完全に不可能になってしまいます。そこで、しばしば<em>可能な限りもっとも簡単な方法でプロトタイプのコンポーネントを構築し、それからファンデーションとアダプターに向かって作業を進めます</em>。私たちはよくこの方法でステップを進めます。

このアプローチを実証するために私たちは **red-blue toggle** を構築します。これは赤い背景と青いテキストが入れ替わる非常に単純なトグルボタンです。マテリアルデザインのコンポーネントではありませんが、これを使って MDC Web の構成がどのように考えられているかというコンセプトを説明します。

### <a name="start-with-a-simple-component-prototype"></a>単純なコンポーネントのプロトタイプ

最初にコンポーネントに取り掛かるにあたり、ファンデーションやアダプターを気にせずに素の HTML/CSS/JavaScript を使ってプロトタイプを構築することから始めます。次のコードが redblue-toggle のプロトタイプのコードです。[CodePen](http://codepen.io/traviskaufman/pen/jVxdNo) でコードを見ることもできます。

> **ヒント**: コメントを試すときは [この CodePen テンプレート](http://codepen.io/traviskaufman/pen/pNQmRp) を出発点とすることもできます。

最初に DOM を使って試しすことから始め、動的な機能を試すために単純なコンポーネントを書いてみましょう。

```html
<div class="redblue-toggle" role="button" aria-pressed="false">
  Toggle <span class="redblue-toggle__color">Blue</span>
</div>
```

```ts
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

この JS コンポーネントは MDC Web を少しも参照しておらず、ファンデーションやアダプターの概念を持っていないことに注意してください。こういったことをしないことにより、素早くコンポーネントを試してみることができ、早く簡単に変更を行うことができます。それにもかかわらずこのプロトタイプのコンポーネントのやり方は MDC Web コンポーネントの構築によるやり方に結局のところとても似ています。

### <a name="identify-host-environment-interactions"></a>ホスト環境とのやりとりの確認

一旦プロトタイプができれば、次のステップはアダプターを通して機能させることが必要であるということを理解することです。ホスト環境との直接的なやりとりは代わりにやってくれるものを必要としています。機能は Web プラットフォーム上のすべてのフレームワークに統合できるできるようするべきだからです（訳注: ホスト環境と直接的なやりとりを行う API を使うとホスト環境を提供するフレームワークとの統合ができてもそれ以外のフレームワークでの適用が難しくなるのでホスト環境の API をラップするものを用意したほうが良いということ）。

> 私たちのアーキテクチャードキュメントについて簡単に説明すると、**ホスト環境** という用語はコンポーネントを使用している環境という意味で使っています。[React-Native](https://facebook.github.io/react-native/) のような技術の場合はブラウザであったりコンポーネントを描画するサーバー、仮想DOM環境、はたまたモバイルアプリケーションといったものを指します。

redblue-toggle ではホスト環境とのやりに関するすべてのインスタンスをとても簡単に見ることができます。`root` ノードに対する読み書きしているところを確認すればよいのです。

- 切り替える際に `setAttribute` で `aria-pressed` を更新
- 切り替える際に `classList.{add,remove}` で root ノードのクラスを更新
- 切り替える際に色名を表示している子要素をの `textContent` を設定
- `initialize()`/`destroy()` を使って root ノードのイベントリスナーをそれぞれ追加または削除

それ以外のケースではホスト環境とのやりとりは `window.addEventListener('resize', ...)` のように単純ではない場合があります。これらもホスト環境のやりとりの例であり、気に留めておく必要があります。

### <a name="create-the-adapter-interface"></a>アダプターインターフェースの作成

ホスト環境とのやりとりが明らかになったので、アダプターインターフェースをこのコンポーネントに構築していきます。

```ts
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
    this.root.addEventListener('click', this.clickHandler_);
  }

  destroy() {
    this.root.removeEventListener('click', this.clickHandler_);
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

| フェイクメソッド | アダプターメソッド |
| --- | --- |
| SOMEHOW_GET_ATTRIBUTE(attr: string) => string | getAttr(attr: string) => string |
| SOMEHOW_SET_ATTRIBUTE(attr: string, value: string) | setAttr(attr: string, value: string) |
| SOMEHOW_ADD_CLASS(className: string) | addClass(className: string) |
| SOMEHOW_REMOVE_CLASS(className: string) | removeClass(className: string) |
| SOMEHOW_UPDATE_TOGGLE_COLOR_TEXT_CONTENT(textContent: string) | setToggleColorTextContent(textContent: string) |

> 注意: 私たちは、イベントリスナーを追加/削除をおこなうのアダプターメソッドとして `registerInteractionHandler` と `deregisterInteractionHandler` を使うことをもはや推奨していません。イベント処理はフレームワークによって大きく異なるので（例えば、[React Synthetic Events](https://reactjs.org/docs/events.html)）、コンポーネント層でイベントを管理することを推奨します。

### <a name="refactor-your-existing-code-into-a-foundation"></a>既存のコードをファンデーションに再構築

アダプター API を定義しましたが、このコードをファンデーションクラスに書き直すことができます。慣習として、なにもしない各関数をもつアダプターを返す静的な `defaultAdapter` ゲッタを定義します。このメソッドは私たちがアダプターの形式を確認するのに役立ち、メソッドの実装を忘れた際にアダプターがエラーを返すことを防ぎ、将来リントツールがアダプターの形式が適切であること強制するため使うことができます（使うべきです）。その例を示しますが、これは `MDCFoundation` クラスの使用例でもあります。このクラスはすべてのファンデーションクラスの基底クラスです。

```ts
class RedblueToggleFoundation extends MDCFoundation {
  static get defaultAdapter() {
    return {
      getAttr: (attr: string) => '',
      setAttr: (attr: string, value: string) => undefined,
      addClass: (className: string) => undefined,
      removeClass: (className: string) => undefined,
      setToggleColorTextContent: (textContent: string) => undefined,
      registerInteractionHandler: (type: string, handler: EventListener) => undefined,
      deregisterInteractionHandler: (type: string, handler: EventListener) => undefined,
    };
  }

  private toggled_ = false;

  constructor(adapter) {
    super({...RedblueToggleFoundation.defaultAdapter, ...adapter});
  }

  handleClick() {
    this.toggle_();
  }

  isToggled() {
    return this.adapter_.getAttr('aria-pressed') === 'true';
  }

  private toggle_(isToggled = undefined) {
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

### <a name="build-a-component-on-top-of-that-foundation-providing-an-adapter"></a>ファンデーション上のコンポーネントの構築とアダプターの提供

最後のステップは上記のファンデーションを使い、コンポーネントを構築することです。コンポーネントは2つの主な役割を持っています。

* ホスト環境内にファンデーションのもつ機能へのイディオム的なインターフェースを提供する
* ホスト環境内で動作するファンデーションへのアダプターを提供する

このコンポーネントは素のコンポーネントなので、素の DOM API をならって作ることになります。素の DOM API はこれらの機能を実装することになるセッタやゲッタにとって好都合です（`checked`, `disabled` などを考えてみてください）。ここで実装するメソッドは簡単に再利用可能なのでアダプターは極めて簡単なものになります。

```ts
class RedblueToggle extends MDCComponent {
  initialize() {
    this.listen('click', this.foundation_.handleClick);
  }

  destroy() {
    this.unlisten('click', this.foundation_.handleClick);
  }

  get toggled() {
    return this.foundation_.isToggled();
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
    });
  }
}
```

このコードは [CodePen 上の最終的なサンプル](http://codepen.io/traviskaufman/pen/gLExme?editors=0010) で見ることができます。

## <a name="what-makes-a-good-component"></a>よいコンポーネント作るには

これらの追加のガイドラインはあなた自身のコンポーネントを作る際に「チェックリスト」を提供します。私たちはコードを書く上でおいてこれらを厳格に守っており、厳格に守ることであなたのコンポーネントの利用者にとって素晴らしい経験を確実なものにするでしょう。

### <a name="fully-tested-code"></a>完全にテストされたコード

ECMAScript は設計上、動的かつ柔軟な言語です。動的で柔軟であることの利点はプログラムの正しさを検証するコストにもなります。コードが期待通りに動作していることを検証する唯一の方法はコードを実行し結果が期待したものであるかを検証することです。ファンデーション、アダプター、コンポーネントのテストカバレッジが100%になるよう努力してください。

### <a name="thoroughly-documented-and-strictly-versioned-adapter-interface"></a>徹底的な文書化と厳密にバージョン管理されたアダプターインターフェース

フレームワークの開発者はあなたのアダプターインターフェース周りコードを設計しいくので、あなたが開発者に設計のために必要な情報をすべて提供することは重要ことです。私たちの推奨する方法はコンポーネントの README にアダプターのインターフェースを文書化し、メソッドの期待された振る舞いはもちろんのこと、メソッドの使い方も文書に提供することです。

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

### <a name="do-what-the-user-expects"></a>ユーザーの期待していることを実行する

これは私たちの「黄金の掟 (golden rule)」です。<em>コンポーネントの API は直感的でわかりやすいものになるよう設計してください。コンポーネントはユーザーの予想通りのふるまいをするようにしてください。</em>例えば `MDCCheckbox` の `checked` ゲッタはチェックボックスの内部状態がチェックされているかどうかを表す真偽値を返してください。副作用ががなく、`type` が `"checkbox"` であるときは `HTMLInputElement.prototype.checked` とまったく同じ方法で動作するようにします。コンポーネントを設計する際には、ユーザーがどのように使うのかを想像したことをもとに作ってください。私たちのケースでは素のコンポーネント（訳注: 手を入れていない MDC Web の素のコンポーネントのこと）は DOM API をもとに作っています。

### <a name="design-adapter-interfaces-to-be-simple-and-ntuitive"></a>アダプターインターフェースは単純かつ直感的なものにする

このルールは先に述べたユーザーの期待しているものを作るというプラクティスに則ったものです。ライブラリの利用者はアダプターメソッドを実装することになるので、アダプターメソッドは実装することが簡単であるだけでなく、本質的に簡素で直感的でなくてはなりません。大半のアダプターメソッドは「クラスを加える」や「プロパティのスタイルを更新する」といったように一言で記述できるべきです。アダプターメソッドの目的は何かとかインプットとアウトプットが何かとかをユーザーが推測するようではいけません。

例えば良いアダプターインターフェースは次のようになっています。

| メソッド | 説明 |
| --- | --- |
| `setStyle(styleProperty: string, value: string) => void` | ダッシュで連結された `styleProperty` とそのプロパティの `value` を指定してルート要素のスタイルを設定する。 |

対して悪いアダプターインターフェースは次のようになっています。

| メソッド | 説明 |
| --- | --- |
| `applyComponentStyles() => void` | コンポーネントのルート要素に適切なスタイルを設定する。詳細はドキュメントを参照のこと。 |

上記のアダプターインターフェースはファンデーションメソッドのほうがふさわしいです。アダプターの唯一の責務はスタイルを更新することであるべきで、スタイルを決定することではありません。

### <a name="do-not-reference-host-objects-within-foundation-code"></a>ファンデーションコード内でホストオブジェクトを参照しない

ファンデーションに可能な限り多くのフレームワークと互換性を持たせるために、ファンデーション内でホストオブジェクトを直接参照することを避けてください。ホストオブジェクトには `window`、 `document`、 `console` などを含みます。<em>ファンデーション内では ECMAScript 仕様で定義されたグローバルオブジェクトのみを参照するようにします。</em>

`requestAnimationFrame` はこのルールの例外ですが、私たちは将来リファクタリングするでしょう。加えて、ファンデーション内でホストオブジェクトを使用することの回避策はアダプターを介してホストオブジェクトを使用することです。

### <a name="clean-up-all-references-on-destruction"></a>デストラクターですべての参照を削除する

このプラクティスはイベントハンドラー、タイマー ID、アニメーションフレーム ID、保持される可能性のあるその他の外部参照を含みます。このプラクティスが実施されているかを確認するために2つの正確なリトマステストがあります。

1. `init()` （もしくは素のコンポーネントにおける  `initialize()`）と `destroy()` が対称的になっている。例えば `init()` でアタッチされたすべてのイベントリスナーは `destroy()` で削除されている。
2. 外部参照を作成するすべての呼び出し（例: `setTimeout()`、`requestAnimationFrame()`）は追跡され、破棄する際にクリーンアップされる。例えばすべての `setTimeout()` 呼び出しはファンデーションやコンポーネントによって ID が保持され、破棄される際には `clearTimeout()` が破棄する処理の中で呼ばれる。

## <a name="authoring-components-for-mdc-web"></a>MDC Web のコンポーネントの作成

以下のガイドラインは直接 MDC Web に貢献したい人向けのものです。上に記載したすべてのプラクティスを守ることに加え、コントリビューターに守ってほしい追加の慣習があります。それらの慣習 - コーディングスタイルやコミットメッセージの書式、テストカバレッジが含まれます - の多くは注目に値するものです。コントリビューターが素早く自信をもって行動できるようになり、コアチームメンバはプルリクエストに時間の浪費や労力の消費をする必要がなくなるからです。

### <a name="file-structure"></a>ファイルの構成

コンポーネントのすべてのソースファイルは `packages/` の下に置きます。すべてのテストファイルは `test/unit` の下に置き、`packages/` ディレクトリの構成を反映させます。パッケージのスクリーンショットテストは `test/screenshot/spec` の下にあります。

典型的なコンポーネントの構成は以下の通りです。

```
packages
  ├── mdc-component
      ├── README.md # 使い方の説明と API ドキュメント
      ├── adapter.ts # フレームワークラッパと素のコンポーネントにより実装されたアダプターインターフェース
      ├── foundation.ts # ラッパライブラリと素のコンポーネントにより使用されるフレームワークにとらわれないビジネスロジック
      ├── component.ts # フレームワークを使用しないときのための素のコンポーネントとアダプターの実装
      ├── constants.ts # パッケージ内のファイルにより利用される定数値（例えば、cssClasses、strings、numbers）
      ├── index.ts # パッケージ内の他のファイル（adapter、foundation、component、util など）を export したもの
      ├── types.ts # （オプション）素のコンポーネントとは関係のないパブリックで公開されている型とインターフェースが含まれる
      ├── util.ts # （オプション）フィレー無ワークにとらわれないヘルパー関数（例えば特徴検出）
      ├── mdc-component.scss # コンポーネントの CSS の主要なソースファイル
      └── package.json # コンポーネントのパッケージファイル
test/unit
  ├── mdc-component
      ├── foundation.test.js # コンポーネントのファンデーションのユニットテスト
      ├── mdc-component.test.js # コンポーネントのユニットテスト
test/screenshot
  ├── spec
      ├── mdc-component
          ├── classes
              ├── baseline.html # 正常ケースでのコンポーネントの使用。そのほかの変種は ./classes の下に置く。
          ├── mixins
              ├── ink-color.html # カスタマイズのための sass ミキシンを使用したコンポーネント。
```

**私たちがプルリクエストを受け入れる前にすべてのコンポーネントにはこれらのファイルが <em>なくてはいけません</em>。**

新しいコンポーネントを提供する際には、私たちの慣習の感覚をよりつかむために既存のコンポーネントを見てみることをお勧めします。あなたの新しいコンポーネントは既存のコンポーネントと「混ざりあって」いるはずです。

加えて、すべての新しいコンポーネントは `package.json` 内に以下の記載が必要です。

```
"publishConfig": {
  "access": "public"
}
```

これは lerna が自動的に新たなスコープ付きパッケージを公開できるようにするために必要です。

各パッケージごとにキーワードのリストも必要です。このリストには常に `material components` と `material design` を入れなくてはならず、それに続けてコンポーネント名を入れます。

```
"keywords": [
  "material components",
  "material design",
  <COMPONENT_NAME>
]
```

例えばチェックボックスコンポーネントを作るのなら、`keywords` には `material components` と `material design`、`checkbox` を入れなくてはいけません。

**以下は新しいコンポーネントの `package.json` の全体の例です。**

```json
{
  "name": "@material/example",
  "version": "0.0.0",
  "description": "The Material Components for the web example component",
  "license": "MIT",
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

### <a name="license-stanzas"></a>ライセンスの記載

テストやデモ、そしてデモの HTML を含む <em>すべてのソースコードファイル</em> の <em>冒頭</em> に以下の記載が必要です。内容は以下の通りです。

```
Copyright <YEAR> Google Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```

すべてのソースファイルの冒頭のコメントにこれを記載し、<YEAR> をファイルを作成した年に置き換えてください。

### Scss

#### <a name="separate-reusable-variables-and-mixins-from-main-scss"></a>再利用可能な変数とミキシンをメインの scss から分離する

変数やミキシンを単一のスタイルシートの外で使用するつもりであるなら、[パーシャル sass](http://sass-lang.com/guide#topic-4) 内にそれらを移してください。これらのファイルは余計な CSS を消さずにほかのスタイルシートにインクルードできます。大雑把に言うと重複した出力になる可能性が高いので CSS を出力する sass ファイルは <em>決して</em> `@import` しないでください。

#### <a name="follow-the-bem-pattern"></a>BEM の様式にしたがう

私たちは [BEM](http://getbem.com/) の様式の修正したバージョンにしたがっており、それは [stylelint ルール](../.stylelintrc.yaml#L252-L255) に定義されています。基本的には以下のようなものです。

```scss
.mdc-block {

}

.mdc-block__element {

}

.mdc-block--modifier {

}
```

通常、コードは次のようになっています。

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

ときより、 `.some-context .mdc-block {/* ... */}` のようにセレクターを修飾する必要がでてきます。Stylelint はこれに対して警告を出すでしょうが、以下の内容を追加することにより、無効にできます。

```scss
// stylelint-disable plugin/selector-bem-pattern

// styles select-bem-pattern complains about...

// stylelint-enable plugin/selector-bem-pattern
```

#### <a name="use-mdc-theme-for-theming"></a>テーマの設定には mdc-theme を使う

コンポーネントのすべてのテーマ要素は [mdc-theme](../packages/mdc-theme) を通じて指定してしなくてはなりません。これにより、コンポーネントが円滑にテーマシステムと統合されることが保証されます。

#### <a name="use-mdc-rtl-for-rtl-support"></a>RTL のサポートには mdc-rtl を使う

コンポーネントのスタイル内の RTL の扱いは、すべて [mdc-rtl](../packages/mdc-rtl) を通じて指定しなくてはなりません。これにより、すべてのコンポーネントが同じ方法で RTL コンテンツを扱え、矛盾なくふるまうことが保証されます。

### Javascript

#### <a name="define-a-static-attachtoroot-method-for-every-component"></a>すべてのコンポーネントに静的メソッド attachTo(root) を定義する

すべてのコンポーネントに以下のシグネチャを持つ静的メソッド `attachTo` を定義 <em>しなくてはいけません</em>。

`static attachTo(element: HTMLElement) => Constructor`

例えば以下のようなコードです。

```js
class MDCNewComponent extends MDCComponent {
  static attachTo(root) {
    return new MDCNewComponent(root);
  }
}
```

`mdc-auto-init` はこのメソッドの存在を必要としており、私たちはユーザーの利便性のためにこのメソッドが提供されることを保証しています。将来的にはこのためのリントルールを書こうと話しています。

#### <a name="define-a-defaultadapter-getter-for-every-foundation"></a>すべてのファンデーションにゲッタ defaultAdapter を定義する

すべてのファンデーションには定義されている関数すべてを持つアダプターを返す静的メソッド `defaultAdapter` を定義 <em>しなくてはいけません</em>。関数は本質的には何もしないのものになるでしょう。引数は取らず、正しい型（例えば、真偽値なら `false`、数値なら `0`、オブジェクトなら `{}` など）を返すようにします。[Typescript の型注釈](https://basarat.gitbooks.io/typescript/content/docs/types/type-system.html) の書式のインラインコメントで型の注釈を付けるのが私たちの慣習です。

デフォルトのアダプターオブジェクトを `adapter` 引数を通じてファンデーションのコンストラクターに渡すようにオーバーライドすることも慣習となっています。これによりアダプターが正しいインターフェースを持つことが保証されます。

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
    super(...MDCNewComponentFoundation.defaultAdapter, ...adapter});
  }
}
```

これにはもちろん、潜在的に誤ったアダプターを渡すことに気づかないことがあるという問題があります。しかし、将来的にはこの問題を緩和するためにアダプターの型定義を提供することを予定しています。前述のルールと同様に、これらの慣習を守ってもらうためのリントルールを提供することも考えています。

#### <a name="define-all-exported-css-classes-strings-and-numbers-as-foundation-constants"></a>外部参照されるすべての CSS クラス、文字列、数値をファンデーションの定数として定義する

- コンポーネントのファンデーションから参照されるすべての CSS クラスは `cssClasses` 静的ゲッタを通じて参照しなくてはいけない。
- ファンデーションクラスのコンテキスト外から使用されるすべての文字列（CSS セレクター、カスタムイベント名、潜在的にローカライズ可能な文字列など）は `strings` 静的ゲッタを通じて参照しなくてはいけない。
- ファンデーションが影響を与えるセマンティックなすべての数値（タイムアウトの長さ、アニメーションの継続時間など）は `numbers` 静的ゲッタを通じて参照しなくてはいけない。
- これらの定数は `constants.ts` ファイルに定義し、ファンデーションを通じてアクセスできるようにしなくてはならない。

```ts
// constants.ts

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

// foundation.ts

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

これの主たる目的は、コンポーネントが Closure Stylesheets の [CSS Class Renaming](https://github.com/google/closure-stylesheets#renaming) メカニズムのような Google のフロントエンドインフラと相互運用できるようにすることです。加えて、コードの理解するうえで良い影響を与え、マジックナンバーやマジックストリングを減らす利点もあります。

#### <a name="extend-components-and-foundations-from-mdc-base-classes"></a>コンポーネントとファンデーションは mdc-base のクラスを継承して作成する

すべてのパッケージに一貫性のある振る舞いをさせるために、すべてのコンポーネントは `MDCComponent` を継承し、すべてのファンデーションは `MDCFoundation` を継承していなくてはいけません。これらのクラスのさらなる情報は [mdc-base README](../packages/mdc-base) にあります。

#### <a name="packages-must-be-registered-with-our-build-infrastructure-and-with-material-components-web-pkg"></a>パッケージをビルドインフラおよび material-components-web パッケージに登録しなくてはいけない

コンポーネントを作る際に、適切なツールとパッケージに登録することは重要です。具体的には以下のことをやってください。

- コンポーネントの登録が `webpack.config.js` 上に `js-components` と `css` のモジュールに対して存在していることを確認すること。
- `material-components-web` の依存関係にそのコンポーネントが追加されていることを確認すること。コンポーネントが JavaScript を含んでいるなら、`material-components-web` 内でそのコンポーネントの名前空間がエクスポートされ、`mdc-auto-init` に登録されていることを確認すること。最後に `material-components-web` の `package.json` にコンポーネントを追加することを忘れないこと。
- レポジトリのルートにあるトップレベル `package.json` の `config.validate-commit-msg.scope.allowed` にパッケージの正確な **コミットサブジェクト** が追加されていることを確認すること。コミットサブジェクトとは <em>コンポーネント名から `mdc-`/`@material/` を除いたもの</em> をいう。例えば `mdc-icon-button` であれば `icon-button` である。

#### <a name="typescript-compatibility"></a>TypeScript との互換性

すべてのコア MDC Web コンポーネントは strict-mode [TypeScript](https://www.typescriptlang.org/) と完全な互換性がなくてはなりません。TypeScript 互換に必要な要件のリストや詳細な説明、慣習、例、やってはいけない一般的な TypeScript のパターンについては [Coding Best Practices](./code/best_practices.md) に記載しています。

### <a name="testing"></a>テスト

MDC Web のコードのテストを書く際に以下のガイドラインにしたがってください。私たちはテストを [Jasmine](https://jasmine.github.io) テストフレームワークで書いており、[karma](https://karma-runner.github.io/1.0/index.html) で実行しています。

#### <a name="verify-foundations-adapters"></a>ファンデーションのアダプターを検証する

ファンデーションをテストする際、少なくともテストケースのうち一つは [foundation helpers](../testing/helpers/foundation.ts) で定義している `verifyDefaultAdapter` メソッドを使うようにしてください。アダプターのインターフェースが予期せず変更されていないことを確認するためです。

#### <a name="use-helper-methods"></a>ヘルパーメソッドを使う
ファンデーション起動テストやイベントによるアダプターメソッドの起動、`requestAnimationFrame` の処理といったことのために [testing/helpers](../testing/helpers) の中にヘルパーモジュールがあります。テストができる限り簡単にかけるようにコードを書く上でこれらを使うことをお勧めしています！

#### <a name="use-bel-for-dom-fixture"></a>DOM フィクスチャーに `getFixture` を使う
コンポーネントやアダプターのテストのフィクスチャーを生成するために [#getFixture](../testing/dom/index.ts) ヘルパーを使います。

#### <a name="always-clean-up-the-dom-after-every-test"></a>あらゆるテストの後は常に DOM をきれいにする
これは重要なことです。<em>テストが終わる前に、DOM にアタッチしたすべての要素が削除されていることを確認してください。</em>。
