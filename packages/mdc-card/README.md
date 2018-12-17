<!--docs:
title: "Cards"
layout: detail
section: components
excerpt: "Cards for displaying content composed of different elements."
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

MDC Card は [マテリアルデザインカードコンポーネント](https://material.io/go/design-cards) を実装したコンポーネントで、CSS クラスの集まりとして開発者が利用できます。

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

## 使用法

### HTML 構造

```html
<div class="mdc-card">
  Simple
</div>
```

完全な機能を使うと以下のようになります。

```html
<div class="mdc-card">
  <div class="mdc-card__media mdc-card__media--square">
    <div class="mdc-card__media-content">Title</div>
  </div>
  <!-- ... コンテンツ ... -->
  <div class="mdc-card__actions">
    <div class="mdc-card__action-buttons">
      <button class="mdc-button mdc-card__action mdc-card__action--button">
        <span class="mdc-button__label">Action 1</span>
      </button>
      <button class="mdc-button mdc-card__action mdc-card__action--button">
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

カードには事前に定義された幅、高さ、パディング、マージンはありません。もっとも単純な形式（`mdc-card` を持つ単一の要素のとき）では、カードは基本的に  `mdc-elevation` + `border-radius` だけになります。

カードは利用できる場所いっぱいに水平方向に拡張され、垂直方向はコンテンツが収まる高さになります。

カードの幅と高さを一貫性のあるものにしたいのなら、スタイルを設定する必要があります。

```css
.my-card {
  height: 350px;
  width: 350px;
}
```

#### アイコン

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

#### コンテンツブロック

カードは異なるコンテンツブロックで構成され、コンテンツブロックは通常垂直方向に配置されます。

アプリケーションによる違いがあるため、カードコンテンツには「標準的」なレイアウトはありません。それぞれのアプリは独自のものを定義する必要があります。

しかし、MDC Card は 2 つの共用のカード要素を提供しています。<em>リッチメディア</em>（画像もしくは映像）と <em>アクション</em> です。

##### リッチメディア

```css
.my-card__media {
  background-image: url("pretty.jpg");
}
```

```html
<div class="my-card__media mdc-card__media mdc-card__media--16-9">
  <div class="mdc-card__media-content">Title</div>
</div>
```

この領域はカード内のリッチメディアを表示するために使用され、オプションでコンテナとして使用することもできます。`mdc-card__media` CSS クラスと [オプションの CSS クラス](#css-classes) を使用してください。

##### アクション

```html
<div class="mdc-card__actions">
  <button class="mdc-button mdc-card__action mdc-card__action--button">
    <span class="mdc-button__label">Action 1</span>
  </button>
  <button class="mdc-button mdc-card__action mdc-card__action--button">
    <span class="mdc-button__label">Action 2</span>
  </button>
</div>
```

この領域はユーザーがとりうる様々なアクションを表示するために使用します。通常は上に示したようにボタンを使用し、以下のようにアイコンボタンを使うこともあります。

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
    <span class="mdc-button__label">All Business Headlines</span>
    <i class="material-icons" aria-hidden="true">arrow_forward</i>
  </a>
</div>
```

ボタン <em>と</em> アイコンを同じ行に表示するには、それらを `mdc-card__action-buttons` 要素と `mdc-card__action-icons` 要素で囲います。

```html
<div class="mdc-card__actions">
  <div class="mdc-card__action-buttons">
    <button class="mdc-button mdc-card__action mdc-card__action--button">
      <span class="mdc-button__label">Read</span>
    </button>
    <button class="mdc-button mdc-card__action mdc-card__action--button">
      <span class="mdc-button__label">Bookmark</span>
    </button>
  </div>
  <div class="mdc-card__action-icons">
   <button class="material-icons mdc-icon-button mdc-card__action mdc-card__action--icon" title="Share">share</button>
    <button class="material-icons mdc-icon-button mdc-card__action mdc-card__action--icon" title="More options">more_vert</button>
  </div>
</div>
```

### スタイル
```css
@import "@material/card/mdc-card";
```

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
`mdc-card-fill-color($color)` | カードの塗りの色を設定する。
`mdc-card-outline($color, $thickness)` | カードの枠の色と太さを設定する（ただし、影は <em>消さない</em>）。
`mdc-card-shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさの丸い形状にカードを設定する。`$rtl-reflexive` を true にする（デフォルトは false）と RTL コンテキスト において半径の値を反転する。
`mdc-card-media-aspect-ratio($x, $y)` | 幅に合わせて動的に高さを変えることにより、`mdc-card__media` サブ要素を与えられたアスペクト比に保つ。
