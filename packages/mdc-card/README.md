<!--docs:
title: "Cards"
layout: detail
section: components
excerpt: "Cards contain content and actions about a single subject."
iconId: card
path: /catalog/cards/
-->

# Cards

[Cards](https://material.io/components/cards/) は単一の課題に対してのコンテンツとアクションを含んでいます。

追加の情報は [API](#api) を参照してください。

![サブタイトルと2つのアクション（紫の Action 1 と Action 2）のある浮き上がったカード](images/card-elevated.png)

## カードを使う

### インストール

```
npm install @material/card
```

### スタイル

```css
@use "@material/card";

@include card.core-styles;
```

汎用性とカードの幅いっぱいの画像などに対応するために、MDC Card はルート要素にパディングがありません。カードに自由な形式のテキストコンテンツを追加する際には、パディングを `16px` に設定する必要があります。

```css
.my-card-content {
  padding: 16px;
}
```

**注意: コンテンツ領域用の MDC Card の適宜済みクラス（例えば `mdc-card__actions`）は独自のパディングを設定します。**

デフォルトでは、カードは利用できる場所いっぱいに水平方向に拡張され、垂直方向はコンテンツが収まる高さになります。
カードの幅と高さを一貫性のあるものにしたいのなら、スタイルを設定する必要があります。

```css
.my-card {
  height: 350px;
  width: 350px;
}
```

[MDC Layout Grid](../mdc-layout-grid) や CSS フレックスボックス、グリッドのようにカードはレイアウトコンテナ内に配置することができます。

### JavaScript

MDC Card 自身は JavaScript を必要としません。しかし、カード内にインタラクティブなコンポーネントを配置するなら、リップルやその他のコンポーネントをインスタンス化することができます。例えば次のようにします。

```js
import {MDCRipple} from '@material/ripple';

const selector = '.mdc-button, .mdc-icon-button, .mdc-card__primary-action';
const ripples = [].map.call(document.querySelectorAll(selector), function(el) {
  return new MDCRipple(el);
});
```

**注意: カードに [アイコントグルボタン](../mdc-icon-button#icon-button-toggle) があるなら、`MDCRipple` ではなく `MDCIconButtonToggle` をインスタンス化します。**

## カード

### カードの例

```html
<div class="mdc-card">
  <!-- ... コンテンツ ... -->
</div>
```

**注意: MDC Card は様々な使用例に対応するよう、設計されています。カード内のコンテンツの特定のタイプについてのヘルパーの情報は [カードのコンテンツ](#card-contents) の節を参照してください。**

## その他のバリエーション

### 枠付きカード

![サブタイトルと2つのアクション（紫の Action 1 と Action 2）のある枠付きカード](images/card-outlined.png)

デフォルトでは、カードは枠がなく、浮き上がっています。`mdc-card--outlined` 修飾クラスを追加することにより、浮き上がらずに枠のあるカードを表示できます。

```html
<div class="mdc-card mdc-card--outlined">
  <!-- ... コンテンツ ... -->
</div>
```

### <a name="card-contents"></a>カードのコンテンツ

MDC Card は様々な使用例で使用できますが、いくつか一般的なスタイルも含んでいます。

#### 主要な操作領域

カードの大部分（もしくはカード全体）が操作可能であるなら、その部分に MDC Ripple のスタイルを適用するために `mdc-card__primary-action` クラスを追加することができます。キーボードを通じて操作できるようにするために `tabindex="0"` も追加するべきです。

```html
<div class="mdc-card">
  <div class="mdc-card__primary-action" tabindex="0">
    <!-- 操作可能な領域内のコンテンツ -->
    <div class="mdc-card__ripple"></div>
  </div>
  <!-- ... コンテンツ ... -->
</div>
```

**注意: `mdc-card__primary-action` の内部にほかの操作可能な要素を追加しないようにすることをお勧めします。これはリップルや一度適用した状態を入れ子になった要素が重複して持ってしまことを避けるためです。**

#### リッチメディア領域

この領域はカード内のリッチメディアを表示するために使用され、オプションでコンテナとして使用することもできます。`mdc-card__media` CSS クラスと [オプションの CSS クラス](#css-classes) を使用してください。

```html
<div class="my-card__media mdc-card__media mdc-card__media--16-9">
  <div class="mdc-card__media-content">Title</div>
</div>
```

```css
.my-card__media {
  background-image: url("pretty.jpg");
}
```

#### 操作領域

この領域はユーザーがとりうる様々な操作を表示するために使用し、通常はカードの下部にあります。しばしば [ボタン](../mdc-button) が使われます。

```html
<div class="mdc-card__actions">
  <button class="mdc-button mdc-card__action mdc-card__action--button">
    <div class="mdc-button__ripple"></div>
    <span class="mdc-button__label">Action 1</span>
  </button>
  <button class="mdc-button mdc-card__action mdc-card__action--button">
    <div class="mdc-button__ripple"></div>
    <span class="mdc-button__label">Action 2</span>
  </button>
</div>
```

[アイコンボタン](../mdc-icon-button) を使うこともできます。

```html
<div class="mdc-card__actions">
  <button class="mdc-icon-button mdc-card__action mdc-card__action--icon"
     aria-pressed="false"
     aria-label="Add to favorites"
     title="Add to favorites">
   <i class="material-icons mdc-icon-button__icon mdc-icon-button__icon--on">favorite</i>
   <i class="material-icons mdc-icon-button__icon">favorite_border</i>
  </button>
  <button class="material-icons mdc-icon-button mdc-card__action mdc-card__action--icon" title="Share">share</button>
  <button class="material-icons mdc-icon-button mdc-card__action mdc-card__action--icon" title="More options">more_vert</button>
</div>
```

正確な位置決めのためにすべてのアクションには `mdc-card__action` クラスを含めてください。加えて、<em>ボタン</em> アイコンには `mdc-card__action--button` クラスを、<em>アイコン</em> アクションには `mdc-card__action--icon` クラスを使わなくてはいけません。

アクション領域の幅いっぱいを占める単一のアクションボタンを使うには `--full-bleed` 修飾子を領域に使います。


```html
<div class="mdc-card__actions mdc-card__actions--full-bleed">
  <a class="mdc-button mdc-card__action mdc-card__action--button" href="#">
    <div class="mdc-button__ripple"></div>
    <span class="mdc-button__label">All Business Headlines</span>
    <i class="material-icons mdc-button__icon" aria-hidden="true">arrow_forward</i>
  </a>
</div>
```

ボタン <em>と</em> アイコンを同じ行に表示するには、それらを `mdc-card__action-buttons` 要素と `mdc-card__action-icons` 要素で囲います。

```html
<div class="mdc-card__actions">
  <div class="mdc-card__action-buttons">
    <button class="mdc-button mdc-card__action mdc-card__action--button">
      <div class="mdc-button__ripple"></div>
      <span class="mdc-button__label">Read</span>
    </button>
    <button class="mdc-button mdc-card__action mdc-card__action--button">
      <div class="mdc-button__ripple"></div>
      <span class="mdc-button__label">Bookmark</span>
    </button>
  </div>
  <div class="mdc-card__action-icons">
   <button class="material-icons mdc-icon-button mdc-card__action mdc-card__action--icon" title="Share">share</button>
    <button class="material-icons mdc-icon-button mdc-card__action mdc-card__action--icon" title="More options">more_vert</button>
  </div>
</div>
```

##### アイコン

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

#### 組み合わせた例

以下はこれまでの要素をすべて組み込んだ例です。

```html
<div class="mdc-card">
  <div class="mdc-card__primary-action">
    <div class="mdc-card__media mdc-card__media--square">
      <div class="mdc-card__media-content">Title</div>
    </div>
    <!-- ... 主要な操作領域のコンテンツを追加 ... -->
    <div class="mdc-card__ripple"></div>
  </div>
  <div class="mdc-card__actions">
    <div class="mdc-card__action-buttons">
      <button class="mdc-button mdc-card__action mdc-card__action--button">
        <div class="mdc-button__ripple"></div>
        <span class="mdc-button__label">Action 1</span>
      </button>
      <button class="mdc-button mdc-card__action mdc-card__action--button">
        <div class="mdc-button__ripple"></div>
        <span class="mdc-button__label">Action 2</span>
      </button>
    </div>
    <div class="mdc-card__action-icons">
      <button class="material-icons mdc-icon-button mdc-card__action mdc-card__action--icon" title="Share">share</button>
      <button class="material-icons mdc-icon-button mdc-card__action mdc-card__action--icon" title="More options">more_vert</button>
    </div>
  </div>
</div>
```

#### 非セマンティックコンテンツ

ときにはカードに非セマンティック要素を追加することが便利なことがあります。例えば、ある実装ではオーバーレイレイヤーを追加するためこれをやっていることがあります。

この場合、実装により追加されたセマンティックな（実際の）コンテンツと非セマンティックコンテンツを区別することが重要です。これを達成するために単純に `mdc-card__content` 要素内のセマンティックなコンテンツ単純にラップします。非セマンティックコンテンツはカードのトップレベルのままにすることが可能になります。

```html
<div class="mdc-card">
  <div class="mdc-card__content">
    <!-- ... セマンティックコンテンツ ... -->
  </div>
  <!-- ... 非セマンティックコンテンツ ... -->
</div>
```

## API

### <a name="css-classes"></a>CSS クラス

CSS クラス | 説明
--- | ---
`mdc-card` | 必須。メインのカード要素。
`mdc-card--outlined` | オプション。影を消し、代わりに細い枠を表示する。
`mdc-card__primary-action` | オプション。カードの主たるタップ可能な領域。一般的には `mdc-card__actions` を除く大半（もしくはすべて）のカードコンテンツを含む。主たる表示をきっかけとした主要なアクションのあるカードに対してのみ適用する。
`mdc-card__ripple` | オプション。要素をリップルスタイルで表示する。`mdc-card__primary-action` が使われているときは必須。主たる表示のトリガーとなる主要なアクションを持つカードにのみ適用する。
`mdc-card__media` | オプション。`background-size: cover` のあるカスタム `background-image` を表示するメディア領域。
`mdc-card__media--square` | オプション。自動的にメディア領域の高さを幅と同じにする。
`mdc-card__media--16-9` | オプション。自動的にメディア領域の高さを幅に基づいて 16:9 のアスペクト比になるようにする。
`mdc-card__media-content` | オプション。タイトルもしくはアイコンを `background-image` の上に表示するために、メディア領域と同じ大きさの絶対座標にボックスを配置する。
`mdc-card__actions` | オプション。アクションボタン・アイコンを含む行。
`mdc-card__actions--full-bleed` | オプション。アクション領域のパディングを削除し、その唯一の子（`mdc-card__action` 要素）がアクション領域の幅の 100% を使えるようにする。
`mdc-card__action-buttons` | オプション。アクションボタンのグループ。（LTR のときは）カードの左側から表示し、`mdc-card__action-icons` に隣接させる。
`mdc-card__action-icons` | オプション。追加のアクションボタンのグループ。（LTR のときは）カードの左側から表示し、`mdc-card__action-buttons` に隣接させる。
`mdc-card__action` | オプション。個々のアクションボタンもしくはアイコン。
`mdc-card__action--button` | オプション。テキストのあるアクションボタン。
`mdc-card__action--icon` | オプション。テキストのないアクションボタン。Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨。
`mdc-card__content` | オプション。セマンティックコンテンツを非セマンティックコンテンツ（例えば、オーバーレイの実装に使われる要素など）と区別するために使う。

### Sass ミキシン

ミキシン | 説明
--- | ---
`fill-color($color)` | カードの塗りの色を設定する。
`outline($color, $thickness)` | カードの枠の色と太さを設定する（ただし、影は <em>消さない</em>）。
`shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にカードを設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`media-aspect-ratio($x, $y)` | 幅に合わせて動的に高さを変えることにより、`mdc-card__media` サブ要素を与えられたアスペクト比に保つ。
