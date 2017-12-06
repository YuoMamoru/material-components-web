[![Build Status](https://img.shields.io/travis/material-components/material-components-web/master.svg)](https://travis-ci.org/material-components/material-components-web/)
[![codecov](https://codecov.io/gh/material-components/material-components-web/branch/master/graph/badge.svg)](https://codecov.io/gh/material-components/material-components-web)
[![Chat](https://img.shields.io/discord/259087343246508035.svg)](https://discord.gg/material-components)

# Material Components for the web

Material Components for the web (MDC-Web) は開発者が [マテリアルデザイン](https://www.material.io) を実践する際の手助けになります。エンジニアのコアチームと Google の UX デザイナーによって開発され、このコンポーネントは美しくかつ機能的な Web プロジェクトを構築するための確かな開発ワークフローを可能にします。

Material Components for the web は [Material Design Lite](https://getmdl.io/) の後継であり、3つのハイレベルな目的を持っています。

- アラカルト方式で製品対応した利用可能なコンポーネント
- 最もパフォーマンスに優れ、[マテリアルデザインガイドライン](https://material.io/guidelines)に準拠
- 他の JS フレームワークおよびライブラリとのシームレスな統合
  - [Preact Material Components](https://github.com/prateekbh/preact-material-components)
  - [RMWC: React Material Web Components](https://github.com/jamesmfriedman/rmwc)
  - [Angular MDC](https://github.com/trimox/angular-mdc-web)
  - [Blox Material](https://blox.src.zone/material): Angular 統合ライブラリ.
  - [Vue MDC Adapter](https://github.com/stasson/vue-mdc-adapter): Vue.js ( [foundation/adapters](./docs/integrating-into-frameworks.md#the-advanced-approach-using-foundations-and-adapters) を使用) による MDC-Web との統合
  - [Material Components Vue](https://github.com/matsp/material-components-vue): Vue.js ([vanilla components](./docs/integrating-into-frameworks.md#the-simple-approach-wrapping-mdc-web-vanilla-components) を使用) による MDC-Web との統合
  - まだまだ増えます！[基準](docs/integrating-into-frameworks.md) をみたしているならあなたのライブラリをこのリストに加えるよう、遠慮なくプルリクエストを送ってください。

MDC-Web は単純な静的ウェブサイト、JavaScript を多用したアプリケーションやクライアント・サーバーのハイブリッドなレンダリングシステムまで、利用状況の広範にあたってシームレスに連携できるよう努めています。端的に言うと、あなたが他のフレームワークに既に多くの投資しているかどうかにかかわらず、あなたのサイトに Material Components を組み込むことは手間なくイディオム風にでき、容易です。

**[デモ](https://material-components-web.appspot.com/)**（リリースの都度、更新されます）

## クイックスタート

ライブラリをインストールします。

```
npm install --save material-components-web
```

次に適切なファイルを取り込み、HTML を作り、`<script>` タグで `mdc.autoInit()` を呼んでください。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Material Components for the web</title>
    <link rel="stylesheet"
          href="node_modules/material-components-web/dist/material-components-web.css">
  </head>
  <body class="mdc-typography">
    <h2 class="mdc-typography--display2">Hello, Material Components!</h2>
    <div class="mdc-text-field" data-mdc-auto-init="MDCTextField">
      <input type="text" class="mdc-text-field__input" id="demo-input">
      <label for="demo-input" class="mdc-text-field__label">Tell us how you feel!</label>
    </div>
    <script src="node_modules/material-components-web/dist/material-components-web.js"></script>
    <script>mdc.autoInit()</script>
  </body>
</html>
```

これで完了です！これが Material Components for web を立ち上げ、実行する最も簡単な方法です。ライブラリのより深い紹介は [入門ガイド](./docs/getting-started.md) を参照してください。

## 個別コンポーネントのインストール

MDC-Web は設計によりモジュール化されています。各コンポーネントは [@material npm org](https://www.npmjs.com/org/material) の下にあるそれぞれのパッケージに存在します。

```
npm install --save @material/button @material/card @material/textfield @material/typography
```

すべてのコンポーネントは [packages](./packages) ディレクトリにあります。各コンポーネントにはインストール方法と使用方法を記載した README があります。

## 含まれているコンポーネント

### JavaScript

JS モジュールの読み込みに Webpack や SystemJS のようなモジュールローダを使用するなら、`material-components-web` から必要なあらゆるコンポーネントを単に `import` でき、次のように使用できます。

```js
import {checkbox as mdcCheckbox} from 'material-components-web';

const {MDCCheckbox, MDCCheckboxFoundation} = mdcCheckbox;
// MDCCheckbox と MDCCheckboxFoundation を使う
```

次のようにしても同じです。

```js
import {MDCCheckbox, MDCCheckboxFoundation} from '@material/checkbox';
// MDCCheckbox と MDCCheckboxFoundation を使う
```

`material-components-web` とすべての個別コンポーネントに対して [UMD](http://bob.yexley.net/umd-javascript-that-runs-anywhere/) も提供しています。

```js
const {checkbox: mdcCheckbox} = require('material-components-web/dist/material-components-web');
// mdcCheckbox を使う

const {MDCCheckbox, MDCCheckboxFoundation} = require('@material/checkbox/dist/mdc.checkbox');
// MDCCheckbox と MDCCheckboxFoundation を使う
```

モジュールシステムを使用しない場合、すべてのコンポーネントはグローバル名前空間 `mdc` の下に加えられます。これはライブラリ全体が使われているか、個別コンポーネントが使われているかに関係ありません。

すべてのコンポーネントは UMD バンドルの圧縮バージョンがあり、`dist/mdc.COMPONENT.min.js` で探せます。

### CSS

スタイルを含んでいるすべてのコンポーネントは `dist/mdc.COMPONENT.css` でスタイルを提供しており、加えて圧縮バージョンとして `dist/mdc.COMPONENT.min.css` もあります。<em>コンポーネントが依存しているファイルはそのコンポーネントの CSS ファイルには含まれていない</em> ので注意していください。すなわち、個別コンポーネントを使うなら、個別に依存ファイルを含めなくてはいけません。

各コンポーネントにはあなたのアプリケーションの Sass からインクルードすることのできる Sass ソースファイルもあります。

```scss
// すべてのライブラリを使用
@import "material-components-web/material-components-web";

// 個別のライブラリ/ミキシンを利用
@import '@material/checkbox';
@import '@material/typography';
@import '@material/elevation/mixins'; // エレベーションのためのミキシン
```

> 注意: コンポーネントの Sass ファイルは `@material` スコープのフォルダを含む `node_modules` ディレクトリが Sass の参照パスにあることを想定しています。

## デモの実行

リポジトリを作成します。

```
git clone https://github.com/material-components/material-components-web.git && cd material-components-web
npm i
```

開発サーバを起動します（`demos/` で提供されます）。

```
cd /path/to/material-components-web
npm run dev
open http://localhost:8080
```

## リンク集

- [入門ガイド](docs/getting-started.md)
- [すべてのコンポーネント](packages/)
- [デモ](demos/)
- [寄付](CONTRIBUTING.md)
- [Material.io](https://www.material.io) （外部サイト）
- [マテリアルデザインガイドライン](https://material.io/guidelines) （外部サイト）

## ブラウザポート

私たちはすべての主要なブラウザの最新2つのバージョンを正式にサポートします。具体的には以下のブラウザでテストをしています。

- Chrome
- Safari
- Firefox
- IE 11/Edge
- Opera
- Mobile Safari
- Chrome on Android
