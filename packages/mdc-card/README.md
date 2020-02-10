<!--docs:
title: "Cards"
layout: detail
section: components
excerpt: "Cards contain content and actions about a single subject."
iconId: card
path: /catalog/cards/
-->

# Cards

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/card">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/cards.png" width="328" alt="Cards screenshot">
  </a>
</div>-->

カードは単一の課題に対してのコンテンツとアクションを含んでいます。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-cards">マテリアルデザインガイドライン: カード</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/card">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/card
```

## 基本的な使用法

### HTML 構造

```html
<div class="mdc-card">
  <!-- ... コンテンツ ... -->
</div>
```

> <em>注意</em>: MDC Card は様々なユースケースに対応できるよう設計されています。カード内の特定のタイプのヘルパーの情報については [Card Contents](#card-contents) の節を参照してください。

### スタイル

```css
@use "@material/card/mdc-card";
```

汎用性とカードの幅いっぱいの画像などに対応するために、MDC Card はルート要素にパディングがありません。カードに自由な形式のテキストコンテンツを追加する際には、パディングを `16px` に設定する必要があります。

```css
.my-card-content {
  padding: 16px;
}
```

> <em>注意</em>: コンテンツ領域用の MDC Card の適宜済みクラス（例えば `mdc-card__actions`）は独自のパディングを設定します。

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

> <em>注意</em>: カードに [アイコン切り替えボタン](../mdc-icon-button#icon-button-toggle) があるなら、`MDCRipple` ではなく `MDCIconButtonToggle` をインスタンス化します。

## バリエーション

### 縁ありのカード

デフォルトでは、カードは縁はなく、浮き上がっている表示がなされます。`mdc-card--outlined` 修飾クラスを加えると浮き上がっていない縁ありのカードが表示されます。

```html
<div class="mdc-card mdc-card--outlined">
  <!-- ... コンテンツ ... -->
</div>
```

### <a name="card-contents"></a>カードのコンテンツ

MDC Card は様々なユースケースで使用できますが、いくつか一般的なスタイルも含んでいます。

#### 主要な操作領域

カードの大部分（もしくはカード全体）が操作可能であるなら、その部分に MDC Ripple のスタイルを適用するために `mdc-card__primary-action` クラスを追加することができます。キーボードを通じて操作できるようにするために `tabindex="0"` も追加するべきです。

```html
<div class="mdc-card">
  <div class="mdc-card__primary-action" tabindex="0">
    <!-- 操作可能な領域内のコンテンツ -->
  </div>
  <!-- ... コンテンツ ... -->
</div>
```

> <em>注意</em>: `mdc-card__primary-action` の内部にほかの操作可能な要素を追加しないようにすることをお勧めします。これはリップルや一度適用した状態を入れ子になった要素が重複して持ってしまことを避けるためです。

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

## スタイルのカスタマイズ

### <a name="css-classes"></a>CSS クラス

CSS クラス | 説明
--- | ---
`mdc-card` | 必須。メインのカード要素。
`mdc-card--outlined` | オプション。影を消し、代わりに細い枠を表示する。
`mdc-card__primary-action` | オプション。カードの主たるタップ可能な領域。一般的には `mdc-card__actions` を除く大半（もしくはすべて）のカードコンテンツを含む。主たる表示をきっかけとした主要なアクションのあるカードに対してのみ適用する。
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

### Sass ミキシン

ミキシン | 説明
--- | ---
`fill-color($color)` | カードの塗りの色を設定する。
`outline($color, $thickness)` | カードの枠の色と太さを設定する（ただし、影は <em>消さない</em>）。
`shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にカードを設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`media-aspect-ratio($x, $y)` | 幅に合わせて動的に高さを変えることにより、`mdc-card__media` サブ要素を与えられたアスペクト比に保つ。
