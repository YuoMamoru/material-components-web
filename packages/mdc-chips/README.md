<!--docs:
title: "Chips"
layout: detail
section: components
excerpt: "Chips are compact elements that represent an attribute, text, entity, or action."
iconId: chip
path: /catalog/chips/
-->

# Chips

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components.github.io/material-components-web-catalog/#/component/chips">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/chips.png" width="363" alt="Chips screenshot">
  </a>
</div>-->

チップはユーザーに情報を入力させたり、選択したり、コンテンツを絞ったりするなどの操作のトリガーとなるコンパクトな要素です。

## デザインと API ドキュメント

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/go/design-chips">マテリアルデザインガイドライン: チップ</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components.github.io/material-components-web-catalog/#/component/chips">デモ</a>
  </li>
</ul>

## インストール

```
npm install @material/chips
```

## 基本的な使用法

### HTML 構造

>**Note**: Due to IE11 and Edge's lack of support for the `:focus-within` selector, keyboard navigation of the chip set will not be visually obvious.

```html
<div class="mdc-chip-set" role="grid">
  <div class="mdc-chip" role="row">
    <div class="mdc-chip__ripple"></div>
    <span role="gridcell">
      <span role="button" tabindex="0" class="mdc-chip__primary-action">
        <span class="mdc-chip__text">Chip One</span>
      </span>
    </span>
  </div>
  <div class="mdc-chip" role="row">
    <div class="mdc-chip__ripple"></div>
    <span role="gridcell">
      <span role="button" tabindex="-1" class="mdc-chip__primary-action">
        <span class="mdc-chip__text">Chip Two</span>
      </span>
    </span>
  </div>
  ...
</div>
```

### スタイル

```scss
@use "@material/chips/mdc-chips";
```

### JavaScript のインスタンス化

```js
import {MDCChipSet} from '@material/chips';
const chipSetEl = document.querySelector('.mdc-chip-set');
const chipSet = new MDCChipSet(chipSetEl);
```

> JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

## バリエーション

### 先頭と末尾のアイコン

先頭アイコン（つまり、サムネイル）や末尾の「削除」アイコンをチップにオプションで追加できます。アイコンを加えるには、好みのアイコンを入れた `i` 要素を追加し、`mdc-c hip__icon` クラスと `mdc-chip__icon--leading` か `mdc-chip__icon--trailing` かのどちらかのクラスを追加します。

Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨します。

```html
<head>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>
```

また、SVG や [Font Awesome](https://fontawesome.com/) 、そのほかの利用したいアイコンライブラリを使うこともできます。

#### 先頭アイコン

```html
<div class="mdc-chip" role="row">
  <div class="mdc-chip__ripple"></div>
  <i class="material-icons mdc-chip__icon mdc-chip__icon--leading">event</i>
  <span role="gridcell">
    <span role="button" tabindex="0" class="mdc-chip__primary-action">
      <span class="mdc-chip__text">Add to calendar</span>
    </span>
  </span>
</div>
```

#### 末尾アイコン

末尾アイコンはチップを集合から削除する機能が備えられています。末尾アイコンを追加するなら、キーボードやスクリーンリーダーからアクセスできるように `tabindex="0"` と `role="button"` も設定します。末尾アイコンは [入力チップ](#input-chips) にのみ追加できます。

```html
<div class="mdc-chip" role="row">
  <div class="mdc-chip__ripple"></div>
  <span role="gridcell">
    <span role="button" tabindex="0" class="mdc-chip__primary-action">
      <span class="mdc-chip__text">Jane Smith</span>
    </span>
  </span>
  <span role="gridcell">
    <i class="material-icons mdc-chip__icon mdc-chip__icon--trailing" tabindex="-1" role="button">cancel</i>
  </span>
</div>
```

### 選択チップ

選択チップは選択肢の集合から一つ選択させるためのチップのバリエーションです。選択チップとしてチップの集合を定義するには、チップセットの要素にクラス `mdc-chip-set--choice` を追加します。

```html
<div class="mdc-chip-set mdc-chip-set--choice" role="grid">
  ...
</div>
```

### フィルターチップ

フィルターチップは選択肢の集合から複数の選択をさせるためのチップのバリエーションです。フィルターチップとしてチップの集合を定義するには、チップセットの要素にクラス `mdc-chip-set--filter` を追加します。フィルターチップが選択されると、先頭アイコンとしてチェック印が表示されます。チップに既に先頭アイコンがあるなら、そのアイコンはチェック印に置き換えられます。そのため、フィルターチップはほかのチップと HTML 構造が異なっています。

```html
<div class="mdc-chip-set mdc-chip-set--filter" role="grid">
  <div class="mdc-chip" role="row">
    <div class="mdc-chip__ripple"></div>
    <span class="mdc-chip__checkmark" >
      <svg class="mdc-chip__checkmark-svg" viewBox="-2 -3 30 30">
        <path class="mdc-chip__checkmark-path" fill="none" stroke="black"
              d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
      </svg>
    </span>
    <span role="gridcell">
      <span role="checkbox" tabindex="0" aria-checked="false" class="mdc-chip__primary-action">
        <span class="mdc-chip__text">Filterable content</span>
      </span>
    </span>
  </div>
  ...
</div>
```

フィルターチップに先頭アイコンを使うのであれば、`mdc-chip__checkmark` 要素の <em>前に</em>  `mdc-chip__icon--leading` 要素を配置します。

```html
<div class="mdc-chip-set mdc-chip-set--filter" role="grid">
  <div class="mdc-chip" role="row">
    <div class="mdc-chip__ripple"></div>
    <i class="material-icons mdc-chip__icon mdc-chip__icon--leading">face</i>
    <span class="mdc-chip__checkmark" >
      <svg class="mdc-chip__checkmark-svg" viewBox="-2 -3 30 30">
        <path class="mdc-chip__checkmark-path" fill="none" stroke="black"
              d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
      </svg>
    </span>
    <span role="gridcell">
      <span role="checkbox" tabindex="0" aria-checked="false" class="mdc-chip__primary-action">
        <span class="mdc-chip__text">Filterable content</span>
      </span>
    </span>
  </div>
  ...
</div>
```

### <a name="input-chips"></a>入力チップ

入力チップはテキストをチップにすることによりユーザーが入力できるようにしたチップのバリエーションです。入力チップとしてチップの集合を定義するには、チップセットの要素にクラス `mdc-chip-set--input` を追加します。

```html
<div class="mdc-chip-set mdc-chip-set--input" role="grid">
  ...
</div>
```

#### DOM へのチップの追加

フレームワークに依存させないために、MDC Chips パッケージにはテキストをチップにする過程はハンドリングされていません。`MDCChipSet` コンポーネントは `addChip` メソッドを公開しており、このメソッドはチップセットの要素内の既存のチップの後ろに既に挿入されていることを前提にして要素を受け入れます。`MDCChipSet` コンポーネントは `MDCChip` コンポーネントのインスタンスの作成と追跡を処理します。

例を挙げると

```js
input.addEventListener('keydown', function(event) {
  if (event.key === 'Enter' || event.keyCode === 13) {
    const chipEl = document.createElement('div');
    // ... チップ要素を適切に配置/装飾する操作を実行 ...
    chipSetEl.appendChild(chipEl);
    chipSet.addChip(chipEl);
  }
});
```

> <em>注意</em>: `MDCChipSet` は、チップ要素が `addChip` に渡される際にまだ ID がないな各チップ要素に適用するための一意の ID を生成します。これはユーザー対話中にチップを区別するために使用されます。

#### DOM からのチップの削除

デフォルトでは、入力チップはチップ内の末尾削除アイコンをクリックに反応して削除されます。削除は `MDCChip` の `beginExit()` メソッドの呼び出しをトリガーにすることもできます。

個々の `MDCChip` インスタンスは削除アニメーションが終了すると `MDCChip:removal` イベントを発行します。`MDCChipSet` は  `MDCChip:removal` に応答して、`MDCChip` インスタンスを破棄しますが、DOM からは手動で削除する必要があります。イベントバブルによってチップセットもしくはその祖先から `MDCChip:removal` を取得することができます。

```js
chipSet.listen('MDCChip:removal', function(event) {
  chipSetEl.removeChild(event.detail.root);
});
```

### 選択済

選択済のフィルターチップや選択チップを表示するには、ルートチップ要素にクラス `mdc-chip--selected` を追加します。

```html
<div class="mdc-chip-set mdc-chip-set--choice" role="grid">
  <div class="mdc-chip mdc-chip--selected" role="row">
    <div class="mdc-chip__ripple"></div>
    <span role="gridcell">
      <span role="radio" tabindex="0" aria-checked="true" class="mdc-chip__primary-action">
        <span class="mdc-chip__text">Add to calendar</span>
      </span>
    </span>
  </div>
</div>
```

先頭アイコンのある選択済フィルターチップでは、`mdc-chip__icon--leading` 要素にクラス `mdc-chip__icon--leading-hidden` も追加します。これによって先頭アイコンはチェック印に置き換えられます。

```html
<div class="mdc-chip-set mdc-chip-set--filter" role="grid">
  <div class="mdc-chip mdc-chip--selected" role="row">
    <div class="mdc-chip__ripple"></div>
    <i class="material-icons mdc-chip__icon mdc-chip__icon--leading mdc-chip__icon--leading-hidden">face</i>
    <span class="mdc-chip__checkmark">
      <svg class="mdc-chip__checkmark-svg" viewBox="-2 -3 30 30">
        <path class="mdc-chip__checkmark-path" fill="none" stroke="black"
              d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
      </svg>
    </span>
    <span role="gridcell">
      <span role="checkbox" tabindex="0" aria-checked="true" class="mdc-chip__primary-action">
        <span class="mdc-chip__text">Filterable content</span>
      </span>
    </span>
  </div>
</div>
```

## 追加情報

### アクセシビリティ

マテリアルデザイン仕様ではタッチの対象は少なくとも  48 x 48 px にすることを勧めています。この要件を満たすためにチップに以下のものを追加してください。

```html
<div class="mdc-touch-target-wrapper">
  <div class="mdc-chip mdc-chip--touch">
    <div class="mdc-chip__ripple"></div>
    <span role="gridcell">
      <span role="button" tabindex="0" class="mdc-chip__primary-action">
        <div class="mdc-chip__touch"></div>
        <span class="mdc-chip__text">Chip One</span>
      </span>
    </span>
  </div>
</div>
```

隣接している要素において、潜在的に（マージンを縮小するために）タッチ対象が重なってしまうのを避けたい場合は、外側に `mdc-touch-target-wrapper` 要素だけが必要なことに注意してください。

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-chip-set` | 必須。チップの属する集合であることを表す。
`mdc-chip-set--input` | オプション。集合内のチップが入力チップであることを表す。入力チップはテキストをチップにすることによりユーザーが入力できるようにする。
`mdc-chip-set--choice` | オプション。集合内のチップが選択チップであることを表す。選択チップは選択肢の集合から一つ選択できるようにする。
`mdc-chip-set--filter` | オプション。集合内のチップがフィルターチップであることを表す。フィルターチップは選択肢の集合から複数の選択できるようにする。
`mdc-chip` | 必須。
`mdc-chip__ripple` | 必須。リップルスタイルで表示される要素であることを示す。
`mdc-chip--selected` | オプション。チップが選択されていることを表す。
`mdc-chip__text` | 必須。チップのテキストコンテンツを表す。
`mdc-chip__icon` | オプション。チップ内のアイコンを表す。Google フォントにある [Material Icons](https://material.io/tools/icons/) を使うことを推奨。
`mdc-chip__icon--leading` | オプション。チップの先頭アイコンを表す。
`mdc-chip__icon--leading-hidden` | オプション。チップが選択された際にフィルターチップの先頭アイコンを隠す。
`mdc-chip__icon--trailing` | オプション。DOM からチップを削除する末尾アイコンを表す。入力チップでのみ使用する。
`mdc-chip__checkmark` | オプション。フィルターチップのチェック印を表す。
`mdc-chip__checkmark-svg` | `mdc-chip__checkmark` を使用する場合は必須。フィルターチップの SVG 要素を表す。
`mdc-chip__checkmark-path` | `mdc-chip__checkmark` を使用する場合は必須。フィルターチップの SVG パスを表す。
`mdc-chip__action--primary` | 必須。`mdc-chip__text` 要素に配置する。
`mdc-chip__action--trailing` | オプション。キーボード操作を通じたアクセスをさせたいときに `mdc-chip__icon--trailing` に配置する。
`mdc-chip--deletable` | オプション。削除キーもしくはバックスペースキーでチップが削除できることを示す。

> <em>注意</em>: `mdc-chip__icon` クラスを持つすべての要素には `mdc-chip__icon--leading` クラスか `mdc-chip__icon--trailing` クラスがある必要があります。

### Sass ミキシン

ミキシン | 説明
--- | ---
`set-spacing($gap-size)` | 集合内の各チップの間隔の大きさを設定する。
`shape-radius($radius, $rtl-reflexive)` | 与えられた半径の大きさにチップ輪郭の丸みを設定する。RTL コンテキスト内で半径の値を設定するには `$rtl-reflexive` を true にする。デフォルトは false。
`fill-color-accessible($color)` | チップの背景の塗りの色を設定し、チップのインクとリップルの色はアクセシビリティ標準に対応したものにする。
`fill-color($color)` | チップの背景の塗りの色を設定する。
`ink-color($color)` | チップのテキストインクの色を設定し、それに合うようにリップルの色を設定する。
`selected-ink-color($color)` | <em>選択された</em> 状態のチップのテキストインクとリップルの色を設定する。
`outline($width, $style, $color)` | チップの輪郭のプロパティを設定する。
`outline-width($width, $horizontal-padding)` | チップの輪郭の太さを設定する。`horizontal-padding` にもカスタム値が設定されているときに限り `$horizontal-padding` は必須。
`outline-style($style)` | チップの輪郭のスタイルを設定する。
`outline-color($color)` | チップの輪郭の色を設定する。
`height($height)` | チップの高さを設定する。
`horizontal-padding($padding)` | チップの水平パディングの値を設定する。
`leading-icon-color($color, $opacity)` | チップの先頭アイコンの色を設定する。オプションで不透明度も設定できる。
`trailing-icon-color($color, $opacity, $hover-opacity, $focus-opacity)` | チップの末尾アイコンの色を設定する。オプションで通常時/ホバー時/フォーカス時の不透明度も設定できる。
`leading-icon-size($size)` | チップの先頭アイコンの大きさを設定する。
`trailing-icon-size($size)` | チップの末尾アイコンの大きさを設定する。
`leading-icon-margin($left-margin, $right-margin)` | チップの先頭アイコンのマージンを設定する。
`trailing-icon-margin($left-margin, $right-margin)` | チップの末尾アイコンのマージンを設定する。
`elevation-transition()` | チップに MDC 持ち上がりトランジッションを追加する。チップにボックスシャドウトランジッションが必要な際には `mdc-elevation-transition-value()` を使ってトランジッションを直接指定する代わりにこれを使ってください。
`density($density-scale)` | チップの密度スケールを設定する。サポートしている密度スケールは `-2`、`-1` そして `0`（デフォルト）

> <em>注意</em>: `mdc-chip-set-spacing` ではチップとチップが含まれている集合の端との間隔の大きさも設定されます。

## `MDCChip` および `MDCChipSet` のプロパティとメソッド

MDC Chips パッケージには2つの JavaScript クラスが同梱されています。
* `MDCChip` は単独のチップの動作を定義しています。
* `MDCChipSet` は指定した集合内のチップの動作を定義しています。例えば、入力チップセット内のチップはフィルターチップセット内のチップとは異なる動作をします。

`MDCChip` クラスと `MDCChipSet` クラスを使うには、`@material/chips` から両方のクラスを [import](../../docs/importing-js.md) します。

#### `MDCChip`

メソッド | 説明
--- | ---
`beginExit() => void` | ファンデーションの `beginExit` メソッドの代替
`focusPrimaryAction() => void` | ファンデーションの `focusPrimaryAction` メソッドの代替
`focusTrailingAction() => void` | ファンデーションの `focusTrailingAction` メソッドの代替
`removeFocus() => void` | ファンデーションの `removeFocus` メソッドの代替
`setSelectedFromChipSet(selected: boolean) => void` | ファンデーションの `setSelectedFromChipset` メソッドの代替（チップセットからのみ呼び出される）

プロパティ | 値の型 | 説明
--- | --- | ---
`id` | `string` (読取専用) | チップの一意な識別子\*
`selected` | `boolean` | ファンデーションの `isSelected`/`setSelected` メソッドの代替
`shouldRemoveOnTrailingIconClick` | `boolean` | ファンデーションの `getShouldRemoveOnTrailingIconClick`/`setShouldRemoveOnTrailingIconClick` メソッドの代替\*\*
`ripple` | `MDCRipple` (読取専用) | `MDCChip` がインスタンス化したルート要素の `MDCRipple` インスタンス

> \*<em>注意</em>: これはルート要素の `id` 属性と同じものです。`id` が提供されないなら、`MDCChipSet.addChip()` によって一意なものが生成されます。

> \*\*<em>注意</em>: `shouldRemoveOnTrailingIconClick` が false に設定されているときは、チップを削除するのに `beginExit()` を手動で呼ぶ必要があります。

##### イベント

イベント | `event.detail` | 説明
--- | --- | ---
`MDCChip:interaction` | `{chipId: string}` | チップが対話（クリック/タップもしくはエンターキーを通じて）したことを示す
`MDCChip:selection` | `{chipId: string, selected: boolean}` | チップが選択状態に変わった（選択チップ/フィルターチップで）ことを示す
`MDCChip:removal` | `{chipId: string, removedAnnouncement: string|null}` | チップが DOM から削除される準備ができたことを示す
`MDCChip:trailingIconInteraction` | `{chipId: string}` | チップの末尾アイコンが対話（クリック/タップもしくはエンターキーを通じて）したことを示す
`MDCChip:navigation` | `{chipId: string, key: string, source: FocusSource}` | チップ上でナビケーションイベントが発生したことを示す

> <em>注意</em>: `MDCChip` のすべてが DOM を通じてイベントバブルを生じます。

#### `MDCChipSet`

メソッド | 説明
--- | ---
`addChip(chipEl: Element) => void` | 与えられた `mdc-chip` 要素をもとにしてチップセットに新しい `MDCChip` インスタンスを追加する

プロパティ | 値の型 | 説明
--- | --- | ---
`chips` | `ReadonlyArray<MDCChip>` | 集合内のチップを表す `MDCChip` オブジェクトの配列
`selectedChipIds` | `ReadonlyArray<string>` | すべての選択されたチップの ID の配列

## Web フレームワークでの使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のチップを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### アダプター: `MDCChipAdapter` と `MDCChipSetAdapter`

これらのアダプター API の素の実装は [`chip/component.ts`](chip/component.ts) and [`chip-set/component.ts`](chip-set/component.ts) を参照してください。

#### `MDCChipAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素にクラスを追加する
`removeClass(className: string) => void` | ルート要素からクラスを削除する
`hasClass(className: string) => boolean` | ルート要素が与えられたクラスを含んでいるなら true を返す
`addClassToLeadingIcon(className: string) => void` | 先頭アイコン要素にクラスを追加する
`removeClassFromLeadingIcon(className: string) => void` | 先頭アイコン要素からクラスを削除する
`eventTargetHasClass(target: EventTarget, className: string) => boolean` | 対象が className を持っていれば true を返し、そうでないなら false を返す
`notifyInteraction() => void` | チップがチップセットと対話したことをチップセットに通知する\*
`notifySelection(selected: boolean, chipSetShouldIgnore: boolean) => void` | チップが選択された、もしくは選択が解除されたことをチップセットに通知する\*\*。`chipSetShouldIgnore` が `true` のとき、チップセットはイベントを処理しない。
`notifyTrailingIconInteraction() => void` | チップの末尾アイコンがチップセットと対話したことをチップセットに通知する\*
`notifyRemoval() => void` | チップが削除されることをチップセットに通知する\*\*\*
`getComputedStyleValue(propertyName: string) => string` | ルート要素の与えられたスタイルプロパティの計算されたプロパティ値を返す
`setStyleProperty(propertyName: string, value: string) => void` | ルート要素の与えられたスタイルプロパティのプロパティ値を設定する
`hasLeadingIcon() => boolean` | チップに先頭アイコンがあるかどうかを返す
`getRootBoundingClientRect() => ClientRect` | ルート要素に結びついている client rect を返す
`getCheckmarkBoundingClientRect() => ClientRect \| null` | チェック印要素に結びついている client rect を返し、チェック印要素がないなら null を返す
`notifyNavigation(key: string, source: EventSource) => void` | ナビゲーションイベントが発生したことをチップセットに通知する
`setPrimaryActionAttr(attr: string, value: string) => void` | プライマリアクション要素の属性を与えられた値に設定する
`focusPrimaryAction() => void` | プライマリアクション要素にフォーカスを与える
`hasTrailingAction() => boolean` | チップが末尾アクション要素を持っていれば `true` を返す
`setTrailingActionAttr(attr: string, value: string) => void` | 末尾アクション要素があれば属性を与えられた値に設定する
`focusTrailingAction() => void` | 存在すれば末尾アクション要素にフォーカスを与える
`getAttribute(attr: string) => string|null` | 存在すれば促成の文字列の値を返し、そうでないなら `null` を返す

> \*<em>注意</em>: `notifyInteraction` と `notifyTrailingIconInteraction` は対象となるチップの ID を伝たえる必要があり、親の `mdc-chip-set` 要素から識別できる必要があります（例えば、DOM イベントバブルを通じて）。

> \*\*<em>注意</em>: `notifySelection` は対象のチップの ID と選択状態を伝える必要がり、親の `mdc-chip-set` 要素から識別できる必要があります（例えば、DOM イベントバブルを通じて）。

> \*\*\*<em>注意</em>: `notifyRemoval` は対象チップの ID とそのルート要素を伝える必要がり、親の `mdc-chip-set` 要素から識別できる必要があります（例えば、DOM イベントバブルを通じて）。

#### `MDCChipSetAdapter`

メソッド | 説明
--- | ---
`hasClass(className: string) => boolean` | チップセットが与えられたクラスを含んでいるかどうかを返す
`removeChipAtIndex(index: number) => void` | チップセットから与えられた `index` のチップを削除する
`selectChipAtIndex(index: string, selected: boolean, shouldNotifyClients: boolean) => void` | 与えられた `index` のチップに対して `MDCChip#setSelectedFromChipSet(selected)` を呼び出す。`shouldNotifyClients` を `true` にして呼ばれたときは選択イベントが発生する。発生した選択イベントは `MDCChipSetFoundation` によって無視される
`getIndexOfChipById(id: string) => number` | `id` に合致したチップのインデックス、もしくは、-1 を返す
`focusChipPrimaryActionAtIndex(index: number) => void` | 与えられた `index` のチップに対して `MDCChip#focusPrimaryAction()` を呼び出す
`focusChipTrailingActionAtIndex(index: number) => void` | 与えられた `index` のチップに対して `MDCChip#focusTrailingAction()` を呼び出す
`isRTL() => boolean` | テキストの方向が RTL なら `true` を返す
`getChipListCount() => number` | チップセット内のチップの数を返す
`removeFocusFromChipAtIndex(index: number) => void` | 与えられた `index` のチップに対して `MDCChip#removeFocus()` を呼び出す
`announceMessage(message: string) => void` | [`aria-live` リージョン](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions) を通じてメッセージを通知する

### ファンデーション: `MDCChipFoundation` と `MDCChipSetFoundation`

#### `MDCChipFoundation`

メソッド | 説明
--- | ---
`isSelected() => boolean` | チップが選択されていれば true を返す
`setSelected(selected: boolean) => void` | チップの選択状態を設定する
`setSelectedFromChipSet(selected: boolean, shouldNotifyClients: boolean) => void` | チップの（チップセットから呼ばれた）選択状態を `selected` パラメータで更新する。`shouldNotifyClients` を `true` にして呼ばれたときは選択イベントが発生する。発生した選択イベントは `MDCChipSetFoundation` によって無視される
`getShouldRemoveOnTrailingIconClick() => boolean` | 末尾アイコンのクリックがチップの終了/削除のトリガーとなっているかどうかを返す
`setShouldRemoveOnTrailingIconClick(shouldRemove: boolean) => void` | 末尾アイコンのクリックをチップの終了/削除のトリガーとするかどうかを設定する
`getDimensions() => ClientRect` | チップの大きさを返す。チップにリップルを提供するのに使用される。
`beginExit() => void` | チップの削除に先駆けて終了アニメーションを開始する
`handleInteraction(evt: Event) => void` | ルート要素の対話イベントをハンドリングする
`handleTransitionEnd(evt: Event) => void` | ルート要素のトランジッション終了イベントをハンドリングする
`handleTrailingIconInteraction(evt: Event) => void` | 末尾アイコン要素の対話イベントをハンドリングする
`handleKeydown(evt: Event) => void` | ルート要素のキーダウンイベントをハンドリングする
`removeFocus() => void` | チップからフォーカスを削除する

#### `MDCChipFoundation` イベントハンドラー

チップファンデーションをラップする際には、以下のイベントを指定されたファンデーションメソッドにバインドしなくてはなりません。

イベント | 要素セレクター | ファンデーションハンドラー
--- | --- | ---
`click`, `keydown` | `.mdc-chip` (ルート) | `handleInteraction()`
`click`, `keydown` | `.mdc-chip__icon--trailing` (存在すれば) | `handleTrailingIconInteraction()`
`transitionend` | `.mdc-chip` (ルート) | `handleTransitionEnd()`
`keydown` | `.mdc-chip` (ルート) | `handleKeydown()`

#### `MDCChipSetFoundation`

メソッド | 説明
--- | ---
`getSelectedChipIds() => ReadonlyArray<string>` | すべての選択されたチップの ID の配列を返す
`select(chipId: string) => void` | 与えられた id を持つチップを選択する
`handleChipInteraction(detail: MDCChipInteractionEventDetail) => void` | ルート要素のカスタム `MDCChip:interaction` イベントをハンドリングする
`handleChipSelection(detail: MDCChipSelectionEventDetail) => void` | ルート要素のカスタム `MDCChip:selection` イベントをハンドリングする。`chipSetShouldIgnore` が true なら、チップセットはイベントを処理しない
`handleChipRemoval(detail: MDCChipRemovalEventDetail) => void` | ルート要素のカスタム `MDCChip:removal` イベントをハンドリングする
`handleChipNavigation(detail: MDCChipNavigationEventDetail) => void` | ルート要素のカスタム `MDCChip:navigation` イベントをハンドリングする

#### `MDCChipSetFoundation` イベントハンドラー

チップセットファンデーションをラップする際には、以下のイベントを指定されたファンデーションメソッドにバインドしなくてはなりません。

イベント | 要素セレクター | ファンデーションハンドラー
--- | --- | ---
`MDCChip:interaction` | `.mdc-chip-set` (ルート) | `handleChipInteraction`
`MDCChip:selection` | `.mdc-chip-set` (ルート) | `handleChipSelection`
`MDCChip:removal` | `.mdc-chip-set` (ルート) | `handleChipRemoval`
`MDCChip:navigation` | `.mdc-chip-set` (ルート) | `handleChipNavigation`
