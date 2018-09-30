[![Version](https://img.shields.io/npm/v/material-components-web.svg)](https://www.npmjs.com/package/material-components-web)
[![Build Status](https://travis-ci.com/material-components/material-components-web.svg?branch=master)](https://travis-ci.com/material-components/material-components-web/)
[![codecov](https://codecov.io/gh/material-components/material-components-web/branch/master/graph/badge.svg)](https://codecov.io/gh/material-components/material-components-web)
[![Chat](https://img.shields.io/discord/259087343246508035.svg)](https://discord.gg/material-components)

# Material Components for the web

Material Components for the web (MDC Web) は開発者が [マテリアルデザイン](https://www.material.io) を実践する際の手助けになります。エンジニアのコアチームと Google の UX デザイナーによって開発され、このコンポーネントは美しくかつ機能的な Web プロジェクトを構築するための確かな開発ワークフローを可能にします。

Material Components for the web は [Material Design Lite](https://getmdl.io/) の後継であり、3つのハイレベルな目的を持っています。

- アラカルト方式で製品対応した利用可能なコンポーネント
- 最もパフォーマンスに優れ、[マテリアルデザインガイドライン](https://material.io/guidelines)に準拠
- 他の JS フレームワークおよびライブラリとのシームレスな統合
  - [Material Components for React](https://github.com/material-components/material-components-web-react): React と MDC Web の統合 ( [foundations/adapters](./docs/integrating-into-frameworks.md#the-advanced-approach-using-foundations-and-adapters) を使用)
  - [Material Web Components](https://github.com/material-components/material-components-web-components): Web Components と MDC Web の統合 ( [vanilla components](./docs/integrating-into-frameworks.md#the-simple-approach-wrapping-mdc-web-vanilla-components) を使用)
  - 追加されたサードパーティ製の統合
    - [Preact Material Components](https://github.com/prateekbh/preact-material-components)
    - [RMWC: React Material Web Components](https://github.com/jamesmfriedman/rmwc)
    - [Angular MDC](https://github.com/trimox/angular-mdc-web)
    - [Blox Material](https://blox.src.zone/material): Angular 統合ライブラリ.
    - [Vue MDC Adapter](https://github.com/stasson/vue-mdc-adapter): Vue.js と MDC Web の統合 ( [foundation/adapters](./docs/integrating-into-frameworks.md#the-advanced-approach-using-foundations-and-adapters) を使用)
    - [Material Components Vue](https://github.com/matsp/material-components-vue): Vue.js と MDC Web の統合 ( [vanilla components](./docs/integrating-into-frameworks.md#the-simple-approach-wrapping-mdc-web-vanilla-components) を使用)
    - [BalmUI](https://material.balmjs.com/): Vue.js 用の次世代マテリアル UI
  - まだまだ増えます！[基準](docs/integrating-into-frameworks.md) をみたしているならあなたのライブラリをこのリストに加えるよう、遠慮なくプルリクエストを送ってください。

MDC Web は単純な静的ウェブサイト、JavaScript を多用したアプリケーションやクライアント・サーバーのハイブリッドなレンダリングシステムまで、利用状況の広範にあたってシームレスに連携できるよう努めています。端的に言うと、あなたが他のフレームワークに既に多くの投資しているかどうかにかかわらず、あなたのサイトに Material Components を組み込むことは手間なくイディオム風にでき、容易です。

**[デモ](https://material-components.github.io/material-components-web-catalog/)**（リリースの都度、更新されます）

> 注意: Material Components Web はセマンティックバージョニングに基づいてまだバージョン 0.x としています。これは破壊的な変更が定期的に起こることを前提としていることを意味しています。月に1回の破壊的な変更を含むマイナーリリースとバグ修正を含む中間パッチリリースを含む2週間のリリーススケジュールに私たちは通常したがっています。
> 変更のリストは常に [CHANGELOG](./CHANGELOG.md) で確認でき、次回の作業の内容の暫定スケジュールは [ROADMAP](./ROADMAP.md) で確認できます。

## クイックスタート

> 注意: このガイドは Node.js と npm がローカルにインストールされていることを前提にしています。

### コンポーネントに CSS を追加する

> 注意: このガイドは Sass を CSS にコンパイルするように webpack を設定していることを前提としています。webpack の設定方法については [入門ガイド](./docs/getting-started.md) を参照してください。

マテリアルデザインボタンの Sass ファイルを含めるには、Node の依存関係をインストールします。

```
npm install @material/button
```

次にアプリケーションに `@material/button` の Sass ファイルをインポートします。これでボタンのカスタマイズに Sass ミキシンを使うことができます。

```scss
@import "@material/button/mdc-button";

.foo-button {
  @include mdc-button-ink-color(teal);
  @include mdc-states(teal);
}
```

MDC Web を使うには `@material` のインポートを解釈できるようにするために Sass ローダを設定する必要があります。`webpack.config.js` の `{ loader: 'sass-loader' }` を次のように修正してください。

```js
{
  loader: 'sass-loader',
  options: {
    includePaths: ['./node_modules']
  }
}
```

`@material/button` にはボタンに必要な HTML についての [ドキュメント](packages/mdc-button/README.md) があります。アプリケーションの HTML に MDC Button のマークアップを入れ、要素に `foo-button` クラスを追加しましょう。

```html
<button class="foo-button mdc-button">
  Button
</button>
```

これでカスタマイズされたマテリアルデザインボタンが完成しました！

<img src="docs/button.png" alt="Button" width="90" height="36">

### コンポーネントに JavaScript を追加する

> 注意: このガイドは JavaScript を ES2015 形式でコンパイルするように webpack を設定していることを前提にしています。webpack の設定方法については [入門ガイド](./docs/getting-started.md) を参照してください。

マテリアルデザインのリップル用に ES2015 ファイルを含めるために依存関係をインストールします。

```
npm install @material/ripple
```

次にアプリケーションに @material/ripple 用の ES2015 ファイルをインポートし、DOM 要素を使って MDCRipple を初期化してください。

```js
import {MDCRipple} from '@material/ripple/index';
const ripple = new MDCRipple(document.querySelector('.foo-button'));
```

> 注意: ビルドプロセスで MDC web の ES2015 ソースをトランスパイルしたいのであれば `@material/ripple/index` をインポートしてください。ビルドのツールチェーンがあなたのソースだけをトランスパいるするように設定されているなら、代わりに `@material/ripple` をインポートします。これは代わりに分散 UMD モジュールを参照しています。

これでボタンにマテリアルデザインリップルが追加されました！

<img src="docs/button_with_ripple.png" alt="Button with Ripple" width="90" height="36">

## リンク集

- [入門ガイド](docs/getting-started.md)
- [すべてのコンポーネント](packages/)
- [デモ](demos/)
- [プロジェクトへの貢献](CONTRIBUTING.md)
- [Material.io](https://www.material.io) （外部サイト）
- [マテリアルデザインガイドライン](https://material.io/guidelines) （外部サイト）

## 助けが必要ですか？

私たちは絶えずコンポーネントの改善を試みています。もし Github の Issues がニーズに合わないなら、[Discord Channel](https://discord.gg/material-components) に来てください。

## ブラウザポート

私たちはすべての主要なブラウザの最新2つのバージョンを正式にサポートします。具体的には以下のブラウザでテストをしています。

- **Chrome** on Android, Windows, macOS, and Linux
- **Firefox** on Windows, macOS, and Linux
- **Safari** on iOS and macOS
- **Edge** on Windows
- **IE 11** on Windows

## 謝辞

速く、信頼性の高い [自動スクリーンショットテスト](test/screenshot/) は以下の人たちが気前よく提供してくれました。

[![CrossBrowserTesting logo](test/screenshot/static/images/cbt-logo.png)](https://crossbrowsertesting.com/)

オープンソースプロジェクトはフリーなのです！

追加の継続的インテグレーションサービスは以下のご好意によるものです。

- [Travis CI](https://travis-ci.com/)
- [Sauce Labs](https://saucelabs.com/)
