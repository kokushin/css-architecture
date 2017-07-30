# CSS architecture

自分なりのCSS設計におけるベストプラクティスを求めて

## SCSSファイルの構成

構成は `imports`, `bases`, `modules`, `components`, `pages` に別けられる

```
├── modules
│   ├── button.scss
│   ├── input.scss
│   └── typography.scss
├── components
│   ├── content.scss
│   ├── footer.scss
│   ├── header.scss
│   └── sidebar.scss
├── pages
│   ├── index.scss
│   └── path
│       └── index.scss
├── variable.scss
├── reset.scss
└── imports.scss
```

### imports

- `imports.scss` が該当する
- 各scssファイルを `@import` するためのファイルで、プリプロセッサのエントリーポイントとして機能する最重要ファイル

### bases

- `variable.scss` や `reset.scss` などが該当する
- 全体に影響するような記述が含まれる場合に指定される
- `imports.scss` 内では最初に読み込ませなければならない

### modules

- `modules` ディレクトリ内のファイルが該当する
- ボタンやタイポグラフィといった単体で機能する最小限のスタイルを `@mixin` として用意し、各モジュールクラスにスタイルを `@include` して適用させる
- 大きさやカラーバリエーションなど細かく分解できるものも用意しておく
- 全ての箇所で使いまわされることを想定して設計する必要がある

### components

- `components` ディレクトリ内のファイルが該当する
- ヘッダーやフッターなど、大きなコンポーネント単位で機能するスタイルを `@mixin` として用意し、各コンポーネントクラスにスタイルを `@include` して適用させる
- 必要に応じて `modules` からスタイルを `@include` して適用させる

### pages

- `pages` ディレクトリ内のファイルが該当する
- Webサイトの各ページのディレクトリ構造に合わせてファイルを作成し、そのページごとのユニークな要素に対してスタイルを適用させる
- このファイルに限り、各モジュール・コンポーネントのスタイルを上書きしてもよい

## クラスの命名規則

設計思想としてはOOCSSとSMACSSを組み合わせたものが望ましい

- 接頭辞の付与はどちらでもよい。クラス名の競合が懸念される場合は付与する
- ネストが深くならない場合に限り `p` や `li` などはクラス名の付与を省略してもよい
- 詳細度はなるべく低く保てるように最小限のHTML構成が求められる
- クラス名を考えるときは英単語のシソーラス検索などを利用し、なるべく理解しやすいものを採用する
- Modifierはハイフン一つで繋ぐ
- あまり冗長的にしない

### 基本

```css
.header
.header.is-fixed
.header .logo
.header .description

.menu
.menu.is-active
.menu .item
.menu .item.item-1
```

### 略語

```css
.btn
.txt
.pic
.img
.nav
.typo
```

### 接頭辞

```css
/* modules */
.m-***

/* components */
.c-***

/* state */
.is-***
```
