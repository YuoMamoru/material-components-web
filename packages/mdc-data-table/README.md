<!--docs:
title: "Data Tables"
layout: detail
section: components
excerpt: "Data tables display information in a grid-like format of rows and columns."
iconId: data_table
path: /catalog/data-tables/
-->

# Data tables

[Data tables](https://material.io/components/data-tables/#) は列と行を通じてデータの集合を表示します。

![5つの行（1つのヘッダ行と4つの行、1つのチェックボックス列）を持つデータテーブル](images/data-table-hero.png)

## データテーブルを使う

データテーブルはグリッド風の行と列の形式で情報を表示します。ユーザーがパターンや洞察を見つけやすいように、スキャンしやすい方法で情報を整理します。

データテーブルには以下のものを含められます。

* 双方向コンポーネント（チップやボタン、メニューなど）
* 双方向でない要素（バッジなど）
* データの問い合わせと操作を行うツール


### インストール

```
npm install @material/data-table
```

### スタイル

```scss
@use "@material/checkbox"; // Required only for data table with row selection.
@use "@material/data-table";

@include checkbox.core-styles;
@include data-table.core-styles;
```

**注意: データテーブルに含めるつもりのコンポーネント（例えばチェックボックスやボタン等）のスタイルもロードしなくてはなりません。**

### JavaScript のインスタンス化

```js
import {MDCDataTable} from '@material/data-table';
const dataTable = new MDCDataTable(document.querySelector('.mdc-data-table'));
```

> JavaScript をインポートする方法についてのさらなる情報は [JS コンポーネントのインポート](../../docs/importing-js.md) を参照してください。

> `MDCDataTable` コンポーネントのインスタンス化は双方向の操作、例えば行選択、を追加したいときのみ必要です。

MDC Data Table コンポーネントはヘッダー行のチェックボックスとすべてのチェックボックスの `MDCCheckbox` を自動的にインスタンス化します。チェックボックスコンポーネントをインスタンス化するのに必要なクラス名を設定してください。行を追加したりデータテーブルから行を削除するときには新しいチェックボックスコンポーネントを登録するために `layout` API を使うことをお勧めします。

### データテーブルを操作しやすくする

テーブル要素に必要な ARIA 推奨のロール、状態、プロパティについては [テーブルについての WAI-ARIA オーサリングプラクティス](https://www.w3.org/TR/wai-aria-practices-1.1/#table) を参照してください。

## データテーブル

```html
<div class="mdc-data-table">
  <table class="mdc-data-table__table" aria-label="Dessert calories">
    <thead>
      <tr class="mdc-data-table__header-row">
        <th class="mdc-data-table__header-cell" role="columnheader" scope="col">Dessert</th>
        <th class="mdc-data-table__header-cell mdc-data-table__header-cell--numeric" role="columnheader" scope="col">Carbs (g)</th>
        <th class="mdc-data-table__header-cell mdc-data-table__header-cell--numeric" role="columnheader" scope="col">Protein (g)</th>
        <th class="mdc-data-table__header-cell" role="columnheader" scope="col">Comments</th>
      </tr>
    </thead>
    <tbody class="mdc-data-table__content">
      <tr class="mdc-data-table__row">
        <td class="mdc-data-table__cell">Frozen yogurt</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">24</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">4.0</td>
        <td class="mdc-data-table__cell">Super tasty</td>
      </tr>
      <tr class="mdc-data-table__row">
        <td class="mdc-data-table__cell">Ice cream sandwich</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">37</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">4.33333333333</td>
        <td class="mdc-data-table__cell">I like ice cream more</td>
      </tr>
      <tr class="mdc-data-table__row">
        <td class="mdc-data-table__cell">Eclair</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">24</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">6.0</td>
        <td class="mdc-data-table__cell">New filing flavor</td>
      </tr>
    </tbody>
  </table>
</div>
```

## その他のバリエーション

### 行選択を伴うデータテーブル

```html
<div class="mdc-data-table">
  <table class="mdc-data-table__table" aria-label="Dessert calories">
    <thead>
      <tr class="mdc-data-table__header-row">
        <th class="mdc-data-table__header-cell mdc-data-table__header-cell--checkbox" role="columnheader" scope="col">
          <div class="mdc-checkbox mdc-data-table__header-row-checkbox mdc-checkbox--selected">
            <input type="checkbox" class="mdc-checkbox__native-control" aria-label="Checkbox for header row selection"/>
            <div class="mdc-checkbox__background">
              <svg class="mdc-checkbox__checkmark" viewBox="0 0 24 24">
                <path class="mdc-checkbox__checkmark-path" fill="none" d="M1.73,12.91 8.1,19.28 22.79,4.59" />
              </svg>
              <div class="mdc-checkbox__mixedmark"></div>
            </div>
          </div>
        </th>
        <th class="mdc-data-table__header-cell" role="columnheader" scope="col">Status</th>
        <th class="mdc-data-table__header-cell" role="columnheader" scope="col">Signal name</th>
        <th class="mdc-data-table__header-cell" role="columnheader" scope="col">Severity</th>
        <th class="mdc-data-table__header-cell" role="columnheader" scope="col">Stage</th>
        <th class="mdc-data-table__header-cell mdc-data-table__header-cell--numeric" role="columnheader" scope="col">Time</th>
        <th class="mdc-data-table__header-cell" role="columnheader" scope="col">Roles</th>
      </tr>
    </thead>
    <tbody class="mdc-data-table__content">
      <tr data-row-id="u0" class="mdc-data-table__row">
        <td class="mdc-data-table__cell mdc-data-table__cell--checkbox">
          <div class="mdc-checkbox mdc-data-table__row-checkbox">
            <input type="checkbox" class="mdc-checkbox__native-control" aria-labelledby="u0"/>
            <div class="mdc-checkbox__background">
              <svg class="mdc-checkbox__checkmark" viewBox="0 0 24 24">
                <path class="mdc-checkbox__checkmark-path" fill="none" d="M1.73,12.91 8.1,19.28 22.79,4.59" />
              </svg>
              <div class="mdc-checkbox__mixedmark"></div>
            </div>
          </div>
        </td>
        <td class="mdc-data-table__cell">Online</td>
        <td class="mdc-data-table__cell" id="u0">Arcus watch slowdown</td>
        <td class="mdc-data-table__cell">Medium</td>
        <td class="mdc-data-table__cell">Triaged</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">0:33</td>
        <td class="mdc-data-table__cell">Allison Brie</td>
      </tr>
      <tr data-row-id="u1" class="mdc-data-table__row mdc-data-table__row--selected" aria-selected="true">
        <td class="mdc-data-table__cell mdc-data-table__cell--checkbox">
          <div class="mdc-checkbox mdc-data-table__row-checkbox mdc-checkbox--selected">
            <input type="checkbox" class="mdc-checkbox__native-control" checked aria-labelledby="u1"/>
            <div class="mdc-checkbox__background">
              <svg class="mdc-checkbox__checkmark" viewBox="0 0 24 24">
                <path class="mdc-checkbox__checkmark-path" fill="none" d="M1.73,12.91 8.1,19.28 22.79,4.59" />
              </svg>
              <div class="mdc-checkbox__mixedmark"></div>
            </div>
          </div>
        </td>
        <td class="mdc-data-table__cell">Offline</td>
        <td class="mdc-data-table__cell" id="u1">monarch: prod shared ares-managed-features-provider-heavy</td>
        <td class="mdc-data-table__cell">Huge</td>
        <td class="mdc-data-table__cell">Triaged</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">0:33</td>
        <td class="mdc-data-table__cell">Brie Larson</td>
      </tr>
      <tr data-row-id="u2" class="mdc-data-table__row mdc-data-table__row--selected" aria-selected="true">
        <td class="mdc-data-table__cell mdc-data-table__cell--checkbox">
          <div class="mdc-checkbox mdc-data-table__row-checkbox mdc-checkbox--selected">
            <input type="checkbox" class="mdc-checkbox__native-control" checked aria-labelledby="u2"/>
            <div class="mdc-checkbox__background">
              <svg class="mdc-checkbox__checkmark" viewBox="0 0 24 24">
                <path class="mdc-checkbox__checkmark-path" fill="none" d="M1.73,12.91 8.1,19.28 22.79,4.59" />
              </svg>
              <div class="mdc-checkbox__mixedmark"></div>
            </div>
          </div>
        </td>
        <td class="mdc-data-table__cell">Online</td>
        <td class="mdc-data-table__cell" id="u2">monarch: prod shared ares-managed-features-provider-heavy</td>
        <td class="mdc-data-table__cell">Minor</td>
        <td class="mdc-data-table__cell">Not triaged</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">0:33</td>
        <td class="mdc-data-table__cell">Jeremy Lake</td>
      </tr>
      <tr data-row-id="u3" class="mdc-data-table__row">
        <td class="mdc-data-table__cell mdc-data-table__cell--checkbox">
          <div class="mdc-checkbox mdc-data-table__row-checkbox">
            <input type="checkbox" class="mdc-checkbox__native-control" aria-labelledby="u3"/>
            <div class="mdc-checkbox__background">
              <svg class="mdc-checkbox__checkmark" viewBox="0 0 24 24">
                <path class="mdc-checkbox__checkmark-path" fill="none" d="M1.73,12.91 8.1,19.28 22.79,4.59" />
              </svg>
              <div class="mdc-checkbox__mixedmark"></div>
            </div>
          </div>
        </td>
        <td class="mdc-data-table__cell">Online</td>
        <td class="mdc-data-table__cell" id="u3">Arcus watch slowdown</td>
        <td class="mdc-data-table__cell">Negligible</td>
        <td class="mdc-data-table__cell">Triaged</td>
        <td class="mdc-data-table__cell mdc-data-table__cell--numeric">0:33</td>
        <td class="mdc-data-table__cell">Angelina Cheng</td>
      </tr>
    </tbody>
  </table>
</div>
```

## スタイルのカスタマイズ

### CSS クラス

CSS クラス | 説明
--- | ---
`mdc-data-table` | 必須。`table` とその他の補助的な要素を含んだルート DOM 要素。
`mdc-data-table__table` | 必須。テーブル要素。`table` HTML タグに追加する。
`mdc-data-table__header-row` | 必須。テーブルヘッダー行要素。`thead > tr` HTML タグに追加する。
`mdc-data-table__header-cell` | 必須。テーブルヘッダーセル要素。`thead > tr > th` HTML タグに追加する。
`mdc-data-table__header-cell--checkbox` | オプション。`mdc-checkbox` を含むテーブルヘッダーセル要素。`thead> tr > th` HTML タグに追加する。
`mdc-data-table__header-cell--numeric` | オプション。数値セルに対応するテーブルヘッダーセル要素。`thead > tr > th` HTML タグに追加する。
`mdc-data-table__content` | 必須。テーブルボディ要素。`tbody` HTML タグに追加する。
`mdc-data-table__row` | 必須。テーブル行要素。`tbody > tr` HTML タグに追加する。
`mdc-data-table__cell` | 必須。テーブルセル要素。`tbody > tr > td` HTML タグに追加する。
`mdc-data-table__cell--numeric` | オプション。数値データを含むテーブルセル要素。`tbody > tr > td` HTML タグに追加する。
`mdc-data-table__cell--checkbox` | オプション。`mdc-checkbox` を含むテーブルセル要素。`tbody > th > td:first-child` HTML タグに追加する。（訳注: 原文は `thead> th > td:first-child` となっているが、`tbody > th > td:first-child` の誤り）
`mdc-data-table__header-row-checkbox` | オプション。テーブルヘッダー行要素に描画されるチェックボックス要素。データテーブルに必須なスタイルに上書きするためにこのクラス名を `mdc-checkbox` 要素に追加する。
`mdc-data-table__row-checkbox` | オプション。テーブル行要素に描画されるチェックボックス要素。データテーブルに必須なスタイルに上書きするためにこのクラス名を `mdc-checkbox` 要素に追加する。
`mdc-data-table__row--selected` | オプション。テーブル行が選択されたときに `mdc-data-table__row` に追加する修飾クラス。

### Sass ミキシン

ミキシン | 説明
--- | ---
`fill-color($color)` | データテーブル面の背景色を設定する。
`row-fill-color($color)` | テーブル行のコンテナの背景色を設定する。
`header-row-fill-color($color)` | テーブルヘッダー行のコンテナの背景色を設定する。
`selected-row-fill-color($color)` | 選択行のコンテナの背景色を設定する。
`checked-icon-color($color)` | チェック時のアイコン色を設定する。
`divider-color($color)` | テーブル行の境界の色を設定する。
`divider-size($size)` | テーブル行の境界の大きさを設定する。
`row-hover-fill-color($color)` | テーブル行のホバー時の背景色を設定する。
`header-row-text-color($color)` | ヘッダー行の文字色を設定する。
`row-text-color($color)` | 行の文字色を設定する。
`shape-radius($radius)` | 与えられた半径の大きさに角の丸めの大きさを設定する。`$radius` は一つの半径、もしくは最大4つの値のリスト使う。
`stroke-size($size)` | データテーブルの境界の大きさを設定する。
`stroke-color($color)` | データテーブルの境界色を設定する。
`header-cell-height($height)` | テーブルヘッダーセルの高さを設定する。
`cell-height($height)` | テーブルセルの高さを設定する。
`cell-padding($leading-padding, $trailing-padding)` | すべてのセルの先頭と末尾のパディングを設定する。
`column-widths($width-list)` | テーブル各行の幅を個別に設定する。
`density($density-scale)` | データテーブルの密度スケールを設定する。サポートしている密度スケールは `-4`、`-3`、`-2`、`-1`、`0`。コンテンツとしてデータテーブル内に描画される密度スケールを適用するために、子コンポーネント（Checkbox など）の対応する密度ミキシンを使用する。

## イベント

イベント定数にアクセスするには MDCDataTable の定数ファイルを使ってください。

```ts
const {events} from '@material/data-table/constants';
// `events.ROW_SELECTION_CHANGED` イベント定数にアクセスに必要
```

イベント定数 | イベント名 | 説明
-- | -- | --
`ROW_SELECTION_CHANGED` | `MDCDataTable:rowSelectionChanged` | 行のチェックボックスがチェックされた、もしくはチェックが外されたときに発生するイベント。
`SELECTED_ALL` | `MDCDataTable:selectedAll` | ヘッダー行のチェックボックスがチェックされたときに発生するイベント。
`UNSELECTED_ALL` | `MDCDataTable:unselectedAll` | ヘッダー行のチェックボックスのチェックが外されたときに発生するイベント。

## `MDCDataTable` プロパティとメソッド

メソッド | 説明
--- | ---
`layout() => void` | 新たな行とヘッダー行のチェックボックスを登録し、ヘッダー行のチェックボックスの状態を更新する。行をデータテーブルから登録/削除した際にはこれを使用する。
`getRows() => HTMLElement[]` | 行要素の配列を返す。
`getSelectedRowIds() => Array<string \| null>` | 選択されている行の id の配列を返す。
`setSelectedRowIds(rowIds: string[])` | 選択された行の id を設定する。直前の選択状態を上書きする。

## Web フレームワークでの使用

React や Angular のような JavaScript フレームワークを使っているなら、そのフレームワーク用のデータテーブルを作ることができます。ニーズに合わせて、<em>単純な手法: MDC Web の素のコンポーネントをラップする</em> や <em>高度な方法: ファンデーションアダプターを使用する</em> を使うことができます。[ここ](../../docs/integrating-into-frameworks.md) にある説明にしたがってください。

### `MDCDataTableAdapter`

メソッド | 説明
--- | ---
`addClass(className: string) => void` | ルート要素に CSS クラス名を追加する。
`removeClass(className: string) => void` | ルート要素から CSS クラス名を削除する。
`addClassAtRowIndex(rowIndex: number, cssClasses: string) => void` | ヘッダー行を除いて、与えられた行のインデックスにある行要素にクラス名を追加する。
`getRowCount() => number` | ヘッダー行を除いた行数を返す。
`getRowElements() => HTMLElement[]` | ヘッダー行を除いた行要素の配列を返す。
`getRowIdAtIndex(rowIndex: number) => string \| null` | 与えられた行インデックスの行要素 `tr` 上の `data-row-id` 属性に基づく行要素の id を返す。
`getRowIndexByChildElement(el: Element) => number` | 与えられた子要素を含んでいる行要素のインデックスを返す。
`getSelectedRowCount() => number` | 選択されている行数を返す。
`isCheckboxAtRowIndexChecked(rowIndex: number) => boolean;` | 与えられた行インデックスの行のチェックボックスがチェックされていれば true を返す。
`isHeaderRowCheckboxChecked() => boolean` | ヘッダー行のチェックボックスがチェックされていれば true を返す。
`isRowsSelectable() => boolean` | テーブル行が選択可能であれば true を返す。
`notifyRowSelectionChanged(data: MDCDataTableRowSelectionChangedEventDetail) => void` | 行の選択状態が変更されたことを通知する。
`notifySelectedAll() => void` | ヘッダー行がチェックされたことを通知する。
`notifyUnselectedAll() => void` | ヘッダー行のチェックが外されたことを通知する。
`registerHeaderRowCheckbox() => Promise<void> \| void` | ヘッダー行のチェックボックスを初期化する。直前の状態でヘッダー行のチェックボックスのインスタンスが存在するなら破棄する。登録されているチェックボックスが非同期の場合にのみ Promise を返すことができる。
`registerRowCheckboxes() => Promise<void> \| void` | すべての行のチェックボックスを初期化する。直前の状態で行のチェックボックスのインスタンスが存在するなら破棄する。これは通常、テーブルにチェックボックスが追加または削除されたときに呼ばれる。登録されているチェックボックスが非同期の場合にのみ Promise を返すことができる。
`removeClassAtRowIndex(rowIndex: number, cssClasses: string) => void` | 与えられた行インデックスの行要素からクラス名を削除する。
`setAttributeAtRowIndex(rowIndex: number, attr: string, value: string) => void` | 与えられた行インデックスの行要素の属性を設定する。
`setHeaderRowCheckboxChecked(checked: boolean) => void` | ヘッダー行のチェックボックスをチェックまたはチェックの解除をする。
`setHeaderRowCheckboxIndeterminate(indeterminate: boolean) => void` | ヘッダー行のチェックボックスを未定状態にする。
`setRowCheckboxCheckedAtIndex(rowIndex: number, checked: boolean) => void` | 与えられた行インデックスの行のチェックボックスをチェックまたはチェックの解除をする。
`getHeaderCellCount(): number;` | ヘッダーセルの総数を返す。
`getHeaderCellElements(): Element[];` | ヘッダーセル要素の配列を返す
`getAttributeByHeaderCellIndex(columnIndex: number, attribute: string) => string` | 与えられたインデックスのヘッダーセルの属性値を返す。
`setAttributeByHeaderCellIndex(columnIndex: number, attribute: string, value: string) => void` | インデックスのヘッダーセルの属性を設定する。
`setClassNameByHeaderCellIndex(columnIndex: number, className: string) => void` | インデックスのヘッダーセルのクラス名を設定する。
`removeClassNameByHeaderCellIndex(columnIndex: number, className: string) => void` | インデックスのヘッダーセルクラス名を削除する。

### `MDCDataTableFoundation`

メソッド | 説明
--- | ---
`layout() => void` | 選択可能な行がテーブルに追加/削除された際にヘッダー行のチェックボックスと行のチェックボックスを再初期化する。チェックボックスの登録が同期しているときに使用する。
`layoutAsync() => Promise<void> \| void` | 選択可能な行がテーブルに追加/削除された際にヘッダー行のチェックボックスと行のチェックボックスを再初期化する。`registerRowCheckboxes` と `registerHeaderRowCheckbox` が同期しているときのみ使用する。
`getRows() => HTMLElement[]` | 行要素の配列を返す。
`setSelectedRowIds(rowIds: string[]) => void` | 選択された行の id を設定する。直前の選択状態を上書きする。
`getSelectedRowIds() => Array<string \| null>` | 選択されている行の id の配列を返す。
`handleHeaderRowCheckboxChange() => void` | ヘッダー行のチェックボックスの変更イベントをハンドリングする。
`handleRowCheckboxChange(event: Event) => void` | 行チェックボックスから発生した変更イベントをハンドリングする。
`getHeaderCells() => Elements[]` | ヘッダーセル要素の配列を返す。
