# アーキテクチャー

MDC Web はパッケージに分かれています。各パッケージはサブシステムもしくはコンポーネントのいずれかです。一般的にそれらはスタイル（色など）と動作（アニメーションなど）とみなせます。コンポーネントパッケージは多くのサブシステムパッケージに依存する傾向にあります。一方、コンポーネントパッケージは他のコンポーネントパッケージにはめったに依存しません。コンポーネントは HTML の構造を必要としています。いくつかのコンポーネントは静的ですが、大半は動的で JavaScript を含んでいます。

> 各コンポーネントは他のコンポーネントとは別個に使用できます。

## Sass

すべての MDC Web の CSS は [Sass](http://sass-lang.com/) を使って生成されます。Sass のミキシンでは複数のコンポーネントで再利用したい CSS 宣言 のグループを作ることができます。サブシステムは Sass ミキシンを提供し、コンポーネントでは Sass ファイル内でミキシンをインポートします。各パッケージはパッケージ内の Sass ファイルを一つの CSS ファイルにコンパイルします。

## HTML

MDC Web は HTML テンプレートを提供しません。単に必要な HTML の構造のドキュメントを提供するだけです。

## JavaScript

MDC Web はそれぞれの動的なコンポーネントの JavaScript をファンデーションとアダプターの2つに分けています。これにより、アダプターのみを再実装すれば React や Angular のような複数の Web プラットフォーム上でファンデーションのコードを再利用できます。今のところ、アダプターの素の JavaScript のバージョンだけが実装されています。

### TypeScript

MDC Web のコンポーネントは開発者の作業速度を上げ、エラーを減らすために [TypeScript](https://www.typescriptlang.org/) で書かれています。npm リリースには UMD JavaScript バンドル、ES5 を含む ES モジュール、そして TypeScript ユーザーのための `.d.ts` 型定義ファイルが含まれています。より詳しい情報は [Importing JS](../importing-js.md) を参照してください。

### ファンデーション

ファンデーションはマテリアルデザインを最もよく表しているビジネスロジックを含んでおり、DOM 要素を参照することはありません。ファンデーションは DOM の操作を必要とするすべてのロジックをアダプターメソッドに委譲します。

### アダプター

アダプターは、マテリアルデザインのビジネスロジックを実装するためにファンデーションが必要なメソッドをすべて持つインターフェースです。アダプターには多くことを実装でき、異なるフレームワークとの相互運用を可能にします。

### 素のコンポーネント

ルート [要素](https://developer.mozilla.org/en-US/docs/Web/API/Element) を使ってインスタンス化するには、`MDCComponent` の `getDefaultFoundation` メソッドをオーバーライドすることによって素のコンポーネントは素のアダプターをともなったファンデーションのインスタンスを生成します。素のアダプターはアダプター API を実装し、ルート要素を直接参照します。素のコンポーネントは開発者のアクセスしたいファンデーションメソッドの代理となるメソッドも公開します。

単に MDC Web を使うだけの（つまり、ラッパーライブラリを作成しない）開発者はコンポーネントだけが必要になります。ファンデーションやアダプターの API を直接操作する必要はありません。
