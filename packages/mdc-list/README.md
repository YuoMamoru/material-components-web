<!--docs:
title: "Lists"
layout: detail
section: components
excerpt: "Lists present multiple line items vertically as a single continuous element."
iconId: list
path: /catalog/lists/
-->

# Lists

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/list">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/lists.png" width="365" alt="Lists screenshot">
  </a>
</div>-->

リストはテキストまたはイメージの連続した垂直方向に並んだ表示項目です。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/design/components/lists.html">マテリアルデザインガイドライン: リスト</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/list">デモ</a>
  </li>
</ul>

## インストール
```
npm install @material/list
```

## 基本的な使用法

### HTML 構造

```html
<ul class="mdc-list">
  <li class="mdc-list-item" tabindex="0">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
</ul>
```

### スタイル

```scss
@import "@material/list/mdc-list";
```

### JavaScript

MDC List はキーボードによる対話や操作を使用できるようにするオプションの JavaScript コンポーネントが含まれています。

```js
import {MDCList} from '@material/list';

const list = new MDCList(document.querySelector('.mdc-list'));
```

> JavaScript をインポートする方法についてのより詳細な情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

JS コンポーネントは自動的にリスト項目のリップルをインスタンス化する<em>わけではない</em>ことに注意してください。リスト項目上に完全にアップグレードされたリップル効果を含めたい場合、各項目に対して `MDCRipple` をインスタンス化しなくてはなりません。

```js
import {MDCRipple} from '@material/ripple';

const listItemRipples = list.listElements.map((listItemEl) => new MDCRipple(listItemEl));
```

## バリエーション

### 2行リスト

`mdc-list--two-line` をテキストの周囲のいくつかの追加マークアップと組み合わせて使うことにより、[仕様](https://material.io/design/components/lists.html#specs)（"Double line" 参照）に定義された2行で表示されるリストをスタイルすることができます。
（訳注: 原文は "Double line" となっていため、そのまま表記したが、現在の仕様では "Two-line list" となっている。）

```html
<ul class="mdc-list mdc-list--two-line">
  <li class="mdc-list-item" tabindex="0">
    <span class="mdc-list-item__text">
      <span class="mdc-list-item__primary-text">First-line text</span>
      <span class="mdc-list-item__secondary-text">Second-line text</span>
    </span>
  </li>
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">
      <span class="mdc-list-item__primary-text">First-line text</span>
      <span class="mdc-list-item__secondary-text">Second-line text</span>
    </span>
  </li>
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">
      <span class="mdc-list-item__primary-text">First-line text</span>
      <span class="mdc-list-item__secondary-text">Second-line text</span>
    </span>
  </li>
</ul>
```

> 注意: 主たるもの（primary）と副次的なもの（secondary）のテキストコンテンツの前にスペースを入れないようにしてください。

### リストグループ

複数の関連するリストで含まれる要素に `mdc-list-group` クラスと一緒に使うことにより、グループ化することができます。

```html
<div class="mdc-list-group">
  <h3 class="mdc-list-group__subheader">List 1</h3>
  <ul class="mdc-list">
    <li class="mdc-list-item" tabindex="0">
      <span class="mdc-list-item__text">line item</span>
    </li>
    <li class="mdc-list-item">
      <span class="mdc-list-item__text">line item</span>
    </li>
    <li class="mdc-list-item">
      <span class="mdc-list-item__text">line item</span>
    </li>
  </ul>
  <h3 class="mdc-list-group__subheader">List 2</h3>
  <ul class="mdc-list">
    <li class="mdc-list-item">
      <span class="mdc-list-item__text">line item</span>
    </li>
    <li class="mdc-list-item">
      <span class="mdc-list-item__text">line item</span>
    </li>
    <li class="mdc-list-item">
      <span class="mdc-list-item__text">line item</span>
    </li>
  </ul>
</div>
```

### <a name="list-dividers"></a>リストの区切線

フル幅で、またはリスト自身を細分化したり、コンテンツの関連するグループ間を独立させたりすることができる `mdc-list-divider` クラスを MDC List は含んでいます。

```html
<ul class="mdc-list">
  <li class="mdc-list-item" tabindex="0">
    <span class="mdc-list-item__text">Item 1 - Division 1</span>
  </li>
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">Item 2 - Division 1</span>
  </li>
  <li role="separator" class="mdc-list-divider"></li>
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">Item 1 - Division 2</span>
  </li>
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">Item 2 - Division 2</span>
  </li>
</ul>
```

> 注意: リスト区切線上の role="separator" 属性に注目してください。この要素が表現上の要素でありリスト内の要素に含まれるという意味ではないことを支援技術が認識するために、これは重要です。この区切線は li 要素にとって非常に有効な役目であることに注意してください。

または

```html
<ul class="mdc-list">
  <li class="mdc-list-item" tabindex="0">
    <span class="mdc-list-item__text">Item 1 - List 1</span>
  </li>
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">Item 2 - List 1</span>
  </li>
</ul>
<hr class="mdc-list-divider">
<ul class="mdc-list">
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">Item 1 - List 2</span>
  </li>
  <li class="mdc-list-item">
    <span class="mdc-list-item__text">Item 2 - List 2</span>
  </li>
</ul>
```

### 単一選択リスト

MDC List はクリックまたはキーボード操作に基づきリスト項目の選択/非選択を処理することができます。有効にすると、 `space` キーと `enter` キー（または `click` イベント）が一つのリスト項目を選択され、ほかの選択されていた要素が非選択になります。

```html
<ul id="my-list" class="mdc-list" role="listbox">
  <li class="mdc-list-item" role="option" tabindex="0">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
  <li class="mdc-list-item" role="option">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
  <li class="mdc-list-item" role="option">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
</ul>
```

```js
const list = new MDCList(document.getElementById('my-list'));
list.singleSelection = true;
```

#### 選択済リスト項目

選択済リスト項目を描画する際には、リストが生成される前に選択済にする必要のあるリスト項目に `mdc-list-item--selected` クラスか `mdc-list-item--activated` クラスを含めなくてはなりません。適切な aria 属性については[アクセシビリティ](#Accessibility) セクションを参照してください。

```html
<ul id="my-list" class="mdc-list" role="listbox">
  <li class="mdc-list-item" role="option" aria-selected="false">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
  <li class="mdc-list-item mdc-list-item--selected" role="option" aria-selected="true" tabindex="0">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
  <li class="mdc-list-item" role="option" aria-selected="false">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
</ul>
```

```js
const list = new MDCList(document.getElementById('my-list'));
list.singleSelection = true;
```

### ラジオグループを伴うリスト

選択済ラジオボタンを伴うラジオグループを描画するには、選択されたリスト項目は `aria-checked` を `true` に設定し、ネイティブな radio input 要素には `checked` 属性を含めます。その他のすべてのリスト項目は `aria-checked` を `false` に設定しなくてはなりません。リストのルートには `role="radiogroup"` を含め、ラジオボタンを内包するそれぞれのリスト項目には `role="radio"` を含めます。

```html
<ul class="mdc-list" role="radiogroup">
  <li class="mdc-list-item" role="radio" aria-checked="false">
    <span class="mdc-list-item__graphic">
      <div class="mdc-radio">
        <input class="mdc-radio__native-control"
              type="radio"
              id="demo-list-radio-item-1"
              name="demo-list-radio-item-group"
              value="1">
        <div class="mdc-radio__background">
          <div class="mdc-radio__outer-circle"></div>
          <div class="mdc-radio__inner-circle"></div>
        </div>
      </div>
    </span>
    <label class="mdc-list-item__text" for="demo-list-radio-item-1">Option 1</label>
  </li>
  <li class="mdc-list-item" role="radio" aria-checked="true" tabindex="0">
    <span class="mdc-list-item__graphic">
      <div class="mdc-radio">
        <input class="mdc-radio__native-control"
              type="radio"
              id="demo-list-radio-item-2"
              name="demo-list-radio-item-group"
              value="2"
              checked>
        <div class="mdc-radio__background">
          <div class="mdc-radio__outer-circle"></div>
          <div class="mdc-radio__inner-circle"></div>
        </div>
      </div>
    </span>
    <label class="mdc-list-item__text" for="demo-list-radio-item-2">Option 2</label>
  </li>
  <li class="mdc-list-item" role="radio" aria-checked="false">
    <span class="mdc-list-item__graphic">
      <div class="mdc-radio">
        <input class="mdc-radio__native-control"
              type="radio"
              id="demo-list-radio-item-3"
              name="demo-list-radio-item-group"
              value="3">
        <div class="mdc-radio__background">
          <div class="mdc-radio__outer-circle"></div>
          <div class="mdc-radio__inner-circle"></div>
        </div>
      </div>
    </span>
    <label class="mdc-list-item__text" for="demo-list-radio-item-3">Option 3</label>
  </li>
</ul>
```

### チェックボックス項目を伴うリスト

チェックボックス項目を伴うリストを描画するには、すべての選択済リスト項目は `aria-checked` を `true` に設定し、ネイティブな checkbox input 要素には `checked` 属性を含めます。その他のすべてのリスト項目は `aria-checked` を `false` に設定しなくてはなりません。チェックボックスリスト内のすべてのリスト項目には `role="checkbox"` 属性を含め、リストのルートは `role="group"` 属性と `aria-label` 属性を含めなくてはなりません。

```html
<ul class="mdc-list" role="group" aria-label="List with checkbox items">
  <li class="mdc-list-item" role="checkbox" aria-checked="false">
    <span class="mdc-list-item__graphic">
      <div class="mdc-checkbox">
        <input type="checkbox"
                class="mdc-checkbox__native-control"
                id="demo-list-checkbox-item-1"  />
        <div class="mdc-checkbox__background">
          <svg class="mdc-checkbox__checkmark"
                viewBox="0 0 24 24">
            <path class="mdc-checkbox__checkmark-path"
                  fill="none"
                  d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
          </svg>
          <div class="mdc-checkbox__mixedmark"></div>
        </div>
      </div>
    </span>
    <label class="mdc-list-item__text" for="demo-list-checkbox-item-1">Option 1</label>
  </li>
  <li class="mdc-list-item" role="checkbox" aria-checked="true" tabindex="0">
    <span class="mdc-list-item__graphic">
        <div class="mdc-checkbox">
            <input type="checkbox"
                    class="mdc-checkbox__native-control"
                    id="demo-list-checkbox-item-2"
                    checked />
            <div class="mdc-checkbox__background">
              <svg class="mdc-checkbox__checkmark"
                    viewBox="0 0 24 24">
                <path class="mdc-checkbox__checkmark-path"
                      fill="none"
                      d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
              </svg>
              <div class="mdc-checkbox__mixedmark"></div>
            </div>
          </div>
    </span>
    <label class="mdc-list-item__text" for="demo-list-checkbox-item-2">Option 2</label>
  </li>
  <li class="mdc-list-item" role="checkbox" aria-checked="false">
    <span class="mdc-list-item__graphic">
        <div class="mdc-checkbox">
            <input type="checkbox"
                    class="mdc-checkbox__native-control"
                    id="demo-list-checkbox-item-3" />
            <div class="mdc-checkbox__background">
              <svg class="mdc-checkbox__checkmark"
                    viewBox="0 0 24 24">
                <path class="mdc-checkbox__checkmark-path"
                      fill="none"
                      d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
              </svg>
              <div class="mdc-checkbox__mixedmark"></div>
            </div>
          </div>
    </span>
    <label class="mdc-list-item__text" for="demo-list-checkbox-item-3">Option 3</label>
  </li>
</ul>
```

`selectedIndex`（ファンデーションの `setSelectedState()` の代替）は選択状態を設定されたチェックボックス要素をもっているリストの配列形式のインデックスのリストを受け付けます。これは現在の選択状態を新たな選択状態で上書きします。

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-list` | リスト要素で必須。
`mdc-list--non-interactive` | オプション。対話型アフォーダンスを無効にする。
`mdc-list--dense` | オプション。リストを密集型にスタイルし、よりコンパクトにする。
`mdc-list--avatar-list` | オプション。各行にアイコンの代わりの画像を表示するための先頭タイルを設定する。リスト項目の画像をより大きくする。
`mdc-list--two-line` | オプション。2行（主たる行と副次的な行）を伴うリストにスタイルを変更する。
`mdc-list-item` | リスト項目で必須。
`mdc-list-item__text` |	必須。リスト項目テキストコンテンツのラッパー（リスト項目の中央に表示させる）。
`mdc-list-item__primary-text` | オプション。リスト項目の主たるテキスト。`mdc-list-item__text` の子要素にする必要がある。
`mdc-list-item__secondary-text` | オプション。リスト項目の副次的テキスト。`mdc-list-item__text` の子要素にする必要がある。
`mdc-list-item--disabled` | オプション。行を利用不可の状態にスタイルする。
`mdc-list-item--selected` | オプション。行を選択状態* にスタイルする。
`mdc-list-item--activated` | オプション。行を活性化状態* にスタイルする。
`mdc-list-item__graphic` | オプション。行の最初の領域（LTR 言語においてはリスト項目の最初の列）。一般的にはアイコンかイメージ。
`mdc-list-item__meta`	| オプション。行の最後の領域（LTR 減とに置いてはリスト項目の最後の列）。一般的には小さなテキスト、アイコンまたはイメージ。
`mdc-list-group` | オプション。一緒にグループ化する2つ以上の mdc-list 要素をラップする。
`mdc-list-group__subheader` |	オプション。グループの各リストの上に表示するヘッダーテキスト。
`mdc-list-divider` | オプション。リストの区切線要素。
`mdc-list-divider--padded` | オプション。`list-item__meta` のパディングと一致するように区切線の両脇の空白を残す。
`mdc-list-divider--inset` | オプション。アバター列と交差しないように区切線の先頭マージンを増やす。

> 注意: `mdc-list-divider` クラスはアイテム間、*もしくは*、2つのリスト間で使用できる（それぞれの例は [リスト区切線](#list-dividers) 以下を参照）。

> 注意: マテリアルデザインでは、選択状態と活性化状態は異なった廃板的な状況で適用されます。
> * *選択状態* は `.mdc-list-item` ではユーザーの選択によって頻繁に変更されうるときに適用します。例えば、Google Photos で一つ以上の写真をシェアするために選択するときです。
> * *活性化状態* は選択状態と比べ、より永続的であり、ページの存続時間に対してすぐに変更されることは **ありません**。一般的な例としてはナビゲーションドロワー内のリストのようなナビゲーションコンポーネントがあります。

### Sass ミキシン

ミキシン | 説明
--- | ---
`mdc-list-item-primary-text-ink-color($color)` | リスト項目のプライマリテキストのインク色を設定する。
`mdc-list-item-secondary-text-ink-color($color)` |  リスト項目のセカンダリテキストのインク色を設定する。
`mdc-list-item-graphic-fill-color($color)` | リスト項目内のグラフィック要素の背景インク色を設定する。
`mdc-list-item-graphic-ink-color($color)` | リスト項目内のグラフィック要素のインク色を設定する。
`mdc-list-item-meta-ink-color($color)` | リスト項目内のメタ要素のインク色を設定する。
`mdc-list-item-shape-radius($radius, $rtl-reflexive)` | リスト項目の角の丸みを与えられた繁栄の大きさに設定する。RTL コンテンツ内で半径を反転させるには `$rtl-reflexive` が true に設定する。デフォルトは false。
`mdc-list-divider-color($color)` | 区切線のインク色を設定する。
`mdc-list-group-subheader-ink-color($color)` | リストグループ内のサブヘッダーのインク色を設定する。

### <a name="Accessibility"></a>アクセシビリティ

MDCList JavaScript コンポーネントは [Listbox](https://www.w3.org/TR/wai-aria-practices-1.1/#Listbox) のための WAI-ARIA ベストプラクティスを実装しています。これにはリストコンポーネント内のデフォルトのタブの動作を上書きすることが含まれています。

最初のリスト項目要素や選択されたリスト項目要素では `tabindex` に `0` を設定しなくてはならず、残りのリスト項目要素には `tabindex` を設定してはいけません。

単一選択リストでは `role="listbox"` のみを使用し、このロールがないと `ul` 要素は暗黙のうちに `role="list"` となります。標準的なリスト（つまり、 `role="list"`）では `aria-orientation` 属性は使わす、コンポーネントの `vertical` プロパティを使って垂直方向に設定してください。

単一選択リストは `aria-selected` 属性と `aria-current` 属性をサポートします。リストは自動的にこれらの属性の存在を認識し、使用した ARIA 属性（つまり、`aria-selected` か `aria-current`）に基づいて次の選択されたリスト項目を設定します。推奨される使用法と利用可能な属性値については WAI-ARIA [aria-current](https://www.w3.org/TR/wai-aria-1.1/#aria-current) の記事を参照してください。

ユーザーがリストを通じて操作する際に、リスト項目がフォーカスされていないならリスト内のどの `button` 要素や `a` 要素も `tabindex="-1"` とします。リスト項目がフォーカスされているなら。前述の要素は `tabIndex="0"` とします。これにより、ユーザーはリスト項目要素をタブにより移動し、さらにリストの後にある最初の要素にタブで移動できます。リスト要素内の操作は `Arrow` キー、`Home` キー そして `End` キーを使うべきです。`singleSelection=true` となっているなら、ユーザーがリスト項目を選択もしくは非選択とするのに `Space` キーか `Enter` キーを使えるようにリストが設定されます。MDCList はそれそれキーが押されるたびに以下のアクションをおこします。リストの操作ではリスト項目内のラジオボタンやチェックボックスを切り替えるので、リストはそれらの要素の `tabindex` を切り替えることはありません。

無効なリスト項目はキーボード操作に含まれています。ARIA での慣習の記事の [Focusability of disabled controls](https://www.w3.org/TR/wai-aria-practices-1.1/#kbd_disabled_controls) セクションを参照してください。

キー | 操作
--- | ---
`ArrowUp` | リストが垂直方向のとき、フォーカスされている項目の前のリスト項目に移動する。
`ArrowDown` | リストが垂直方向のとき、フォーカスされている項目の次のリスト項目に移動する。
`ArrowLeft` | リストが水平方向（デフォルト）のとき、フォーカスされている項目の前のリスト項目に移動する。
`ArrowRight` | リストが水平方向（デフォルト）のとき、フォーカスされている項目の次のリスト項目に移動する。
`Home` | フォーカスされているリストの最初のリスト項目に移動する。
`End` | フォーカスされているリストの最後のリスト項目に移動する。
`Space` | `singleSelection=true` であるなら、現在フォーカスされているリスト項目を選択/非選択にする。
`Enter` | `singleSelection=true` であるなら、現在フォーカスされているリスト項目を選択/非選択にする。


## `MDCList` プロパティとメソッド

プロパティ | 値の型 | 説明
--- | --- | ---
`vertical` | `boolean` (書込専用) | ファンデーションの `setVerticalOrientation()` メソッドの代替。
`listElements` | `Array<Element>` (読込専用) | 無効なリスト項目を含めたすべてのリスト項目を返す。
`wrapFocus` | `boolean` (書込専用) | ファンデーションの `setWrapFocus()` メソッドの代替。
`singleSelection` | `boolean` (書込専用) | ファンデーションの `setSingleSelection()` メソッドの代替。
`selectedIndex` | `boolean` | ファンデーションの `getSelectedIndex()` メソッドと `setSelectedIndex()` メソッドの代替。

メソッド | 説明
--- | ---
`layout() => void` | レイアウトの方向を再計算する。
`initializeListType() => void` | 選択済みチェックボックス、単一選択、またはラジオボタンに基づいて `selectedIndex` の値を初期化する。
`setEnabled(itemIndex: number, isEnabled: boolean) => void` | `itemIndex` のリスト項目を希望する `isEnabled` の状態に更新する。 

### イベント

イベント | `event.detail` | 説明
--- | --- | ---
`MDCList:action` | `{index: number}` | 指定された院でkk数のリスト項目が有効になったことを示す。

## Web フレームワークでの使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のリストを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### 高度な方法での検討事項

`MDCListFoundation` は使用する前に一定の方法で HTML がセットアップされることを期待しています。このセットアップは `index.js` 内の `layout()` 関数と `singleSelection()` 関数の一部となっています。

#### `layout()` のステップイン

デフォルトのコンポーネントではフォーカスを受け取れるようにするため、すべてのリスト要素が `tabindex` の値を受け取ることを求めています（`li` 要素は `tabindex` の値がないときフォーカスを全く受けることができません）。`tabindex` 属性を含んでいないすべての属性は `tabindex=-1` となります。最初のリスト項目には `tab` を使って最初の要素を探せるようにするために `tabindex="0"` とすべきですが、そうすると次の `tab` キーの押下でリスト全体にフォーカスが来ます。リスト項目にフォーカスを受け取れる子要素（`button` 要素と `a` 要素）が含まれているなら、これらは `tabIndex="-1"` とすべきです。

```html
<ul id="my-list" class="mdc-list">
  <li class="mdc-list-item" tabindex="0">
    <span class="mdc-list-item__text">Single-line item</span>
    <button tabindex="-1"></button>
  </li>
  <li class="mdc-list-item" tabindex="-1">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
  <li class="mdc-list-item" tabindex="-1">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
</ul>
```

#### `singleSelection()` のステップイン

単一選択型を使用しているコンポーネントを実装するとき、HTML は `mdc-list-item--selected` クラスか `mdc-list-item--activated` クラスを含むように変更し、選択された要素の `tabindex` は `0` にしなくてはなりません。最初のリスト項目は `tabindex` を `-1` にします。ファンデーションがインスタンス化された後、ファンデーションメソッド `setSelectedIndex()` は初期化時に選択状態の要素を伴って直ちに呼び出されます。適切な aria 属性については [アクセシビリティ](#Accessibility) のセクションを参照してください。

```html
<ul id="my-list" class="mdc-list">
  <li class="mdc-list-item" tabindex="-1">
    <span class="mdc-list-item__text">Single-line item</span>
    <button tabindex="-1"></button>
    </li>
  <li class="mdc-list-item mdc-list-item--selected" aria-selected="true" tabindex="0">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
  <li class="mdc-list-item" tabindex="-1">
    <span class="mdc-list-item__text">Single-line item</span>
  </li>
</ul>
```

### `MDCListAdapter`

メソッド | 説明
--- | ---
`getListItemCount() => Number` | `root_` 要素の直接の子要素となっているリスト項目（`mdc-list-item` クラスを伴う要素）の総数を返す。
`getFocusedElementIndex() => Number` | 現在フォーカスされている要素の `index` の値を返す。
`getListItemIndex(ele: Element) => Number` | 与えられた `ele` 要素の `index` の値を返す。
`getAttributeForElementIndex(index: number, attribute: string) => string | null` | 与えられた `index` の位置のリスト項目の属性値を返す。
`setAttributeForElementIndex(index: Number, attr: String, value: String) => void` | `index` の位置のリスト項目の `attr` 属性を `value` にする。
`addClassForElementIndex(index: Number, className: String) => void` | `index` の位置のリスト項目に `className` クラスを追加する。
`removeClassForElementIndex(index: Number, className: String) => void` | `index` の位置のリスト項目から `className` クラスを削除する。
`focusItemAtIndex(index: Number) => void` | 指定した`index` の位置のリスト項目をフォーカスする。
`setTabIndexForListItemChildren(index: Number, value: Number) => void` | 指定した`index` の位置のリスト項目にあるボタンとアンカーの子要素の `tabindex` 属性を `value` にする。
`hasRadioAtIndex(index: number) => boolean` | 与えられたインデックスのリスト項目にラジオボタンがあれば true を返す。
`hasCheckboxAtIndex(index: number) => boolean` | 与えられたインデックスのリスト項目にチェックボックスがあれば true を返す。
`isCheckboxCheckedAtIndex(index: number) => boolean` | リスト項目内のチェックボックスがチェックされていれば true を返す。
`setCheckedCheckboxOrRadioAtIndex(index: number, isChecked: boolean) => void` | 与えられたインデックスのリスト項目にあるチェックボックスかラジオボタンのチェック状態を設定する。
`notifyAction(index: number) => void` | リスト項目上のキーボード操作やマウス操作を含むユーザー操作を通知する。
`isFocusInsideList() => boolean` | 現在フォーカスされている要素がリストのリートの内部にあれば true を返す。
`isRootFocused() => boolean` | ルート要素がフォーカスされていれば true を返す。

### `MDCListFoundation`

メソッド | 説明
--- | ---
`setWrapFocus(value: Boolean) => void` | リストの最後の要素にフォーカスするための最初の要素上で上矢印を許可するように設定する。逆も同様。
`setVerticalOrientation(value: Boolean) => void` | リストの方向を設定し、操作に利用するキーを変更する。`true` では上下の矢印キーを使用する。`false` では左右の矢印キーを使用する。
`setSingleSelection(value: Boolean) => void` | リストを選択リストにする。リスト項目の選択/非選択を設定するのに `enter` キーと `space` キーを使えるようにする。
`getSelectedIndex() => MDCListIndex` | 選択されたインデックスもしくはリストに基づくチェックボックスによるインデックスのリストを返すことにより、現在の選択状態を取得する。`MDCListIndex` 型定義については [types.ts](./types.ts) を参照のこと。
`setSelectedIndex(index: MDCListIndex) => void` | 選択されたインデックスもしくはリストに基づくチェックボックスによるインデックスのリストを与えることにより、選択状態を設定する。`MDCListIndex` 型定義については [types.ts](./types.ts) を参照のこと。
`setUseActivatedClass(useActivated: boolean) => void` | `mdc-list-item--activated` クラスを適用/削除するための選択ロジックを設定する。
`handleFocusIn(evt: Event) => void` | リスト項目がフォーカスを受けた際、すべてのボタン要素とアンカー要素のために `tabindex` の `0` への変更を処理する。
`handleFocusOut(evt: Event) => void` | リスト項目がフォーカスを失った際、すべてのボタン要素とアンカー要素のために `tabindex` の `-1` への変更を処理する。
`handleKeydown(evt: Event) => void` | キーイベントがトリガーになった際、フォーカス操作を起こすべきかどうかの決定を処理する。
`handleClick(evt: Event) => void` | リスト項目がクリックされた際、リスト項目の選択/非選択の状態の切り替えを処理する。このメソッドは単一選択リストでのみ使用される。
`focusNextElement(index: number) => number` | 現在の `index` を利用して次の要素へのフォーカスを処理する。フォーカスされた要素のインデックスを返す。
`focusPrevElement(index: number) => number` | 現在の `index` を利用して前の要素へのフォーカスを処理する。フォーカスされた要素のインデックスを返す。
`focusFirstElement() => number` | リストの最初の要素へのフォーカスを処理する。フォーカスされた要素のインデックスを返す。
`focusLastElement() => number` | リストの最後の要素へのフォーカスを処理する。フォーカスされた要素のインデックスを返す。
`setEnabled(itemIndex: number, isEnabled: Boolean) => void` | リスト項目の無効状態を更新する。
