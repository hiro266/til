# 作りながら学ぶVue!Slack風クローンApp

## 用語

### node.js

- JavaScriptをサーバーサイド側で使えるようにするプラットフォーム

### npm

- node.jsのパッケージを管理するツール

`npm install`で`package.json`に記載されているパッケージをインストールできる

### パッケージ

- 世界中の誰かが作ったプログラム

### コンポーネント

- 一つのファイルに HTML、JavaScript、CSSがごっちゃになっているのを単一ファイルコンポーネント（Single File Component）。  
一般的には、コンポーネントと呼ばれる。

## 知識

- pages フォルダ配下に .vue ファイルを作ることでルーティングができる。  
→ pages/articles.vue http://localhost:3000/articles が生成

## コード

```
{ components: {　Logo　} }
{ components: {　Logo: Logo　} }

これらは同義でkey,valueが同じ時、短縮して記述することができる
```


