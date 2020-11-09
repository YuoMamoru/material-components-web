[![Version](https://img.shields.io/npm/v/material-components-web.svg)](https://www.npmjs.com/package/material-components-web)
[![Chat](https://img.shields.io/discord/259087343246508035.svg)](https://discord.gg/material-components)

# Material Components for the web

Material Components for the web は開発者が [マテリアルデザイン](https://www.material.io) を実践する際の手助けになります。エンジニアのコアチームと Google の UX デザイナーによって開発され、このコンポーネントは美しくかつ機能的な Web プロジェクトを構築するための確かな開発ワークフローを可能にします。

Material Web は単純な静的ウェブサイト、JavaScript を多用したアプリケーションやクライアント・サーバーのハイブリッドなレンダリングシステムまで、利用状況の広範にあたってシームレスに連携できるよう努めています。端的に言うと、あなたが他のフレームワークに既に多くの投資しているかどうかにかかわらず、あなたのサイトに Material Components を組み込むことは手間なくイディオム風にでき、容易です。

Material Components for the web は [Material Design Lite](https://getmdl.io/) の後継です。[マテリアルデザインガイドライン](https://material.io/design) を実装することに加えて、より柔軟なテーマのカスタマイズ、これは色彩だけでなくタイポグラフィや形状、状態などまでも提供しています。様々な [主要 Web フレームワーク](docs/framework-wrappers.md) に適応できるように [設計](docs/code/architecture.md) もされています。 

> 注意: Material Components Web は月ごとに重大な変更をリリースすることにしていますが、[semver](https://semver.org/) にしたがっているのでリリースを取り込む際にコントロールすることができます。通常、月1回の重大な変更を含むメジャーリリスとバグ修正を含む中間リリースの2週間ごとのリリーススケジュールにしたがっています。

## 主要なリンク

- [入門ガイド](docs/getting-started.md)
- [デモ](https://material-components.github.io/material-components-web-catalog)
- [ほかのフレームワーク上での Material](docs/framework-wrappers.md)
- [Material Web の利用例](docs/examples.md)
- [Contributing](CONTRIBUTING.md)
- [マテリアルデザインガイドライン](https://material.io/design) (external site)
- [ブラウザポート](docs/supported-browsers.md)
- [すべてのパッケージ](packages/)
- [Changelog](./CHANGELOG.md)

## クイックスタート

### CDN を通じての利用

```html
<!-- Required styles for Material Web -->
<link rel="stylesheet" href="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.css">

<!-- Render textfield component -->
<label class="mdc-text-field mdc-text-field--filled">
  <span class="mdc-text-field__ripple"></span>
  <span class="mdc-floating-label" id="my-label">Label</span>
  <input type="text" class="mdc-text-field__input" aria-labelledby="my-label">
  <span class="mdc-line-ripple"></span>
</label>

<!-- Required Material Web JavaScript library -->
<script src="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.js"></script>
<!-- Instantiate single textfield component rendered in the document -->
<script>
  mdc.textField.MDCTextField.attachTo(document.querySelector('.mdc-text-field'));
</script>
```

> サンプルのすべてについては codepen 上の [クイックスタートデモ](https://codepen.io/abhiomkar/pen/gQWarJ) を参照してください。

### NPM を使用する

> このガイドでは Sass を CSS にコンパイルするように設定されている webpack が入っていることを想定しています。webpack の設定については [入門ガイド](docs/getting-started.md) の全文を参照してください。最終的なコードや結果は [Material Starter Kit](https://glitch.com/~material-starter-kit) でも見ることができます。

プロジェクトに textfield node モジュールをインストールしてください。

```
npm install @material/textfield
```

#### HTML

text field コンポーネントの使用例です。さらなるオプションに関しては [Textfield](packages/mdc-textfield) コンポーネントのページを参照してください。

```html
<label class="mdc-text-field mdc-text-field--filled">
  <span class="mdc-text-field__ripple"></span>
  <input type="text" class="mdc-text-field__input" aria-labelledby="my-label">
  <span class="mdc-floating-label" id="my-label">Label</span>
  <span class="mdc-line-ripple"></span>
</label>
```

#### CSS

必須である text field コンポーネントを読み込みます。

```scss
@use "@material/floating-label/mdc-floating-label";
@use "@material/line-ripple/mdc-line-ripple";
@use "@material/notched-outline/mdc-notched-outline";
@use "@material/textfield";

@include textfield.core-styles;

```

#### JavaScript

text field コンポーネントをインスタンス化するために `MDCTextField` モジュールをインポートします。

```js
import {MDCTextField} from '@material/textfield';
const textField = new MDCTextField(document.querySelector('.mdc-text-field'));
```

これで一つだけある `.mdc-text-field` 要素上に text field が初期化されました。

> すべてのサンプルについては glitch の [quick start demo](https://glitch.com/edit/#!/remix/new-web) を参照してください。

## 助けが必要ですか？

私たちは絶えずコンポーネントの改善を試みています。もし Github の Issues がニーズに合わないなら、[Discord Channel](https://discord.gg/material-components) に来てください。
