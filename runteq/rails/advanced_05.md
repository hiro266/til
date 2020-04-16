# 課題5 検索機能の追加

## 実装

- ActiveModel関連 [リファレンス](https://railsguides.jp/active_model_basics.html)

> ActiveModelとはActiveRecordを継承しないクラスでもActiveRecordと同じような便利メソッドが使えるようになる優れものです。validatesメソッドなどがその一例

search_articles_form.rb
```
class SearchArticlesForm
  # 検索フォーム等、モデルに紐付かないパラメータを処理する時などに使用(gem)
  include Virtus.model

  # 命名やルーティングの管理を支援するクラスメソッドを多数追加
  # form_withの裏でmodel_nameが使用されているため必要な記述
  # コメントアウトするとsearch_articles_form/indexでform_withが使用できなくなる
  extend ActiveModel::Naming

  # railsの変換メソッド(new,present?など)をSearchArticlesFormに対して使用可能
  include ActiveModel::Conversion

  # SearchArticlesFormクラスが抱える属性(include Virtus.modelによって使用可能)
  attribute :category_id, Integer
  attribute :tag_id, Integer
  attribute :author_id, Integer
  attribute :body, String
  attribute :title, String
end
```

- form_withのscope(その他にも例を記載)

`scope: :q`の指定はなぜ必要?  
→ 慣習的に検索はクエリ(q)の中にデータを入れるから

admin/articles/index.html.slim
```
= form_with model: @search_articles_form, scope: :q, url: admin_articles_path, method: :get, html: { class: 'form-inline' } do |f|
```


- [単一テーブル継承について(Qiita)](https://qiita.com/hiro266/items/218713c076fb0075712f)

## RSpec

- transientとafter(:build)のイメージ

spec/factories/articles.rb
```
   trait :with_author do
      # transient = articlesに属するデータ以外のattributeを定義
      transient do
        sequence(:author_name) { |n| "test_author_name_#{n}" }
        sequence(:tag_slug) { |n| "test_author_slug_#{n}" }
      end

      # インスタンスを生成し、transientで定義されたデータを:authorやslugに代入する
      after(:build) do |article, evaluator|
        article.author = build(:author, name: evaluator.author_name, slug: evaluator.tag_slug)
      end
    end
```

## 用語

## その他

### form_with(model、scope、urlについて)

- modelあり、scope・urlなし

```
= form_with model: @search_articles_form, method: :get, html: { class: 'form-inline' } do |f|
```

scope → params[:search_articles_form]  
url → search_articles_forms_path そんなpathはないと怒られる

- model・urlあり、scopeなし

```
= form_with model: @search_articles_form, url: admin_articles_path, method: :get, html: { class: 'form-inline' } do |f|
```

scope → params[:search_articles_form]  
url → admin_articles_pathへ

- model・url・scopeあり

```
= form_with model: @search_articles_form, scope: :q, url: admin_articles_path, method: :get, html: { class: 'form-inline' } do |f|
```

scope → q[:search_articles_form]  
url → admin_articles_pathへ

#### 補足

- form_withのmodelオプションにActive Record以外のオブジェクト(Active Recordを継承していない)を渡すデザインパターンを**Form Object**と呼ぶ
