# 課題5 検索機能の追加

## 実装

[単一テーブル継承について](https://qiita.com/hiro266/items/218713c076fb0075712f)

## RSpec

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


