# CSS architecture

自分なりのCSS設計におけるベストプラクティスを求めて

## SCSSファイルの構成

構成は `imports`, `cores`, `modules`, `components`, `pages` に別けられる

- `modules` は「部品」、`components` は「部品を組み合わせた製品」と捉えるとよい

```
├── _imports.scss
├── components
│   ├── _import.scss
│   ├── content.scss
│   ├── footer.scss
│   ├── header.scss
│   └── sidebar.scss
├── cores
│   ├── _import.scss
│   ├── reset.scss
│   ├── mixins.scss
│   └── variables.scss
├── modules
│   ├── _import.scss
│   ├── button.scss
│   ├── input.scss
│   └── typography.scss
└── pages
    ├── index.scss
    └── single
        └── index.scss
```

### imports

- `imports.scss` が該当する
- 各scssファイルを `@import` するためのファイルで、プリプロセッサのエントリーポイントとして機能する最重要ファイル

### cores

- `variables.scss` や `mixins.scss`、`reset.scss` などが該当する
- 全体に影響するようなスタイルや設定ファイルを配置する
- `imports.scss` 内では最初に読み込ませなければならない

### modules

- `modules` ディレクトリ内のファイルが該当する
- ボタンやタイポグラフィといった「部品」単位で機能する最小限のスタイルを専用のモジュールクラスに適用させる
- 大きさやカラーバリエーションなど細かく分解できるものも用意しておく

### components

- `components` ディレクトリ内のファイルが該当する
- ヘッダーやフッターなど、「製品」単位で機能するスタイルを専用のコンポーネントクラスに適用させる
- コンポーネントごとの細かいスタイル調整が必要な場合は、各モジュールのスタイルを上書きしてもよい

### pages

- `pages` ディレクトリ内のファイルが該当する
- Webサイトの各ページのディレクトリ構造に合わせてファイルを作成し、そのページごとのユニークな要素に対してスタイルを適用させる
- ページごとの細かいスタイル調整が必要な場合は、各モジュール・コンポーネントのスタイルを上書きしてもよい

## クラスの命名規則

思想としてはOOCSSとSMACSSを組み合わせたものが望ましい

- 接頭辞の付与はどちらでもよい。クラス名の競合が懸念される場合は付与する
- ネストが深くならない場合に限り `p` や `li` などはクラス名の付与を省略してもよい
- 詳細度はなるべく低く保てるように最小限のHTML構成が求められる
- クラス名を考えるときは英単語のシソーラス検索などを利用し、なるべく理解しやすいものを採用する
- 単語はキャメルケースで繋ぐ
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
.m-className

/* components */
.c-className

/* state */
.is-className

/* JavaScript */
.js-className
```
