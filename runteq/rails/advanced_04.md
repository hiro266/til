# 課題4 記事ステータスの追加

## 実装

### やりたいこと

1. rakeタスクに`公開待ちの中で、公開日時が過去になっているものがあれば、ステータスを「公開」に変更されるようにする`タスクを作成
2. 上記のrakeタスクを`schedule.rb(whenever)`に1時間毎に定期実行させる(バッチ処理)設定を記述して、1時間毎に定期的にcronを編集する
3. cronをcronコマンドでアップデート

## RSpec

## 用語

### rake

- rubyのソースコードで処理内容を定義できるビルドツール

### rakeタスク

- rakeが実行する処理内容

>rakeタスクを使用する場面の例  
>>1. 何かしらのデータの連携  
>>2. データベースのバックアップ  
>>3. 定期的にデータを更新、削除する  

### ビルド

- ソースコード(人間用)から実際のプログラム(機械用)に変換する作業

### whenever

- cronの設定をrubyの文法で扱えるようにするライブラリ

[CapistranoでWhenever](https://qiita.com/yumiyon/items/388fbb84450f49a6ab0d)

### バッチ処理

- あらかじめ登録した一連の処理を自動的に実行する処理方式

### cron

- メモリ場で常に命令を待機しているデーモンプロセスの1つ

### デーモンプロセス

- UNIX系OSでメインメモリ上に常駐して特定の機能を提供するプログラム

## その他

### N+1問題

#### 概要

N+1:SQLの実行回数+全てのレコードの取得  
1. postをallで取得(全てのレコードの取得)
2. postに紐づくuserをpostの数だけ(n回)取得(postの数だけ(n回)SQLが実行される)

大量のSQL実行処理により動作が重くなる

#### 解決法

includesメソッドで関連するモデルのデータを先に取得  
includes(:取得したいモデル)

### find find_by where

find、find_byは検索結果のインスタンス(データが返ってくるため)カラムの取得も可能。  
whereは検索結果の表示をしているだけなのでカラムの取得はできない。

#### find

- idを検索対象としてデータを取得&カラムの取得可能

```
[3] pry(main)> article = Article.find(1)
  Article Load (0.4ms)  SELECT  `articles`.* FROM `articles` WHERE `articles`.`id` = 1 LIMIT 1
=> #<Article:0x00007f9e5aa4b960
 id: 1,
 category_id: nil,
 author_id: nil,
 uuid: "547c8942-edad-4c2a-a962-27198fef75ed",
 slug: "slag",
 title: "初投稿",
 description: "テスト投稿",
 body: nil,
 state: "draft",
 published_at: Wed, 08 Apr 2020 17:40:00 JST +09:00,
 created_at: Wed, 08 Apr 2020 17:38:57 JST +09:00,
 updated_at: Wed, 08 Apr 2020 17:40:49 JST +09:00,
 deleted_at: nil>
[4] pry(main)> article.title
=> "初投稿"
```

#### find_by

- id以外を検索対象としてhitした**最初のデータ**のみ取得&カラム取得可能

```
[5] pry(main)> article = Article.find_by(state: 'draft')
  Article Load (0.3ms)  SELECT  `articles`.* FROM `articles` WHERE `articles`.`state` = 0 LIMIT 1
=> #<Article:0x00007f9e5a659f28
 id: 1,
 category_id: nil,
 author_id: nil,
 uuid: "547c8942-edad-4c2a-a962-27198fef75ed",
 slug: "slag",
 title: "初投稿",
 description: "テスト投稿",
 body: nil,
 state: "draft",
 published_at: Wed, 08 Apr 2020 17:40:00 JST +09:00,
 created_at: Wed, 08 Apr 2020 17:38:57 JST +09:00,
 updated_at: Wed, 08 Apr 2020 17:40:49 JST +09:00,
 deleted_at: nil>
[6] pry(main)> article.title
=> "初投稿"
```

#### where

- id以外を検索対象として検索した場合、該当する全てのデータが返ってくる&カラムの取得不可(返ってきたデータが1件だろうと)

```
[35] pry(main)> article = Article.where(state: 'published')
  Article Load (0.6ms)  SELECT `articles`.* FROM `articles` WHERE `articles`.`state` = 1
=> [#<Article:0x00007f9e5a8a8ab8
  id: 2,
  category_id: 1,
  author_id: nil,
  uuid: "12d9214c-bbb6-4743-92cc-e7e1711d43af",
  slug: "image",
  title: "エラー確認投稿",
  description: "エラー確認",
  body: "",
  state: "published",
  published_at: Sun, 12 Apr 2020 03:57:00 JST +09:00,
  created_at: Wed, 08 Apr 2020 17:54:59 JST +09:00,
  updated_at: Sun, 12 Apr 2020 03:57:18 JST +09:00,
  deleted_at: nil>,
[36] pry(main)> article.title
NoMethodError: undefined method `title' for #<Article::ActiveRecord_Relation:0x00007f9e5a8abf60>
from /Users/niwayamahiroki/runteq-curriculum/266_hiro266_runteq_learning_advanced/vendor/bundle/ruby/2.6.0/gems/activerecord-5.2.3/lib/active_record/relation/delegation.rb:125:in `method_missing'
```
