# 画像挿入時のバグ修正

## 実装編
- image_tagの引数にnilが入るとエラーを吐く  
if(unless)でnil以外の時だけ画像を表示させてやれば良い

## 解答例
```ruby
ruby:
  medium = local_assigns[:medium]

- if medium.image_url
  .media-image
    = image_tag medium.image_url(:lg)
```

このように記載すると判定結果がelseの場合に空のmedia-imageタグが生成されてしまうので注意
```ruby
ruby:
  medium = local_assigns[:medium]

.media-image
  - if medium.image_url
    = image_tag medium.image_url(:lg)
```

## RSpec編
