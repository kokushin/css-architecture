# CSS architecture

CSS設計におけるベストプラクティスを求めて

## SCSSファイルの構成

構成は `imports`, `bases`, `modules`, `components`, `pages` に別けられる

```
├── components
│   ├── content.scss
│   ├── footer.scss
│   ├── header.scss
│   └── sidebar.scss
├── imports.scss
├── modules
│   ├── button.scss
│   ├── input.scss
│   └── typography.scss
├── pages
│   ├── index.scss
│   └── path
│       └── index.scss
├── reset.scss
└── variable.scss
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
- ボタンやタイポグラフィといった単体で機能する最小限のスタイルを `@mixin` として用意する
- 大きさやカラーバリエーションなど細かく分解できるものも用意しておく
- 全ての箇所で使いまわされることを想定して設計する必要がある

### components

- `components` ディレクトリ内のファイルが該当する
- ヘッダーやフッターなど、大きなコンポーネント単位で機能するスタイルを `@mixin` として用意し、コンポーネントクラスにスタイルを `@include` して適用させる
- 必要に応じて `modules` からスタイルを `@include` して適用させる

### pages

- `pages` ディレクトリ内のファイルが該当する
- Webサイトの各ページのディレクトリ構造に合わせてファイルを作成し、そのページごとのユニークな要素に対してスタイルを適用させる
- このファイルに限り、スタイルを上書きしても良い