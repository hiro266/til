# 画像挿入時のバグ修正

## 実装編
- image_tagの引数にnilが入るとエラーを吐く  
if(unless)でnil以外の時だけ画像を表示させてやれば良い

### 解答例
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

- `trait`同じFactoryBot内で別のデータを持ったインスタンスを生成したい時に使用
- spec/support以下にモジュールを作成するのが一般的
- seedとseed-fu  
seedは実行するたびに同じデータが登録されていく  
seed-fuは既にデータが存在している場合でも、レコードだけ更新したり、ファイル単位で実行できたり、簡単に書けるようなシンタックスシュガーがあったりと便利  
何度`rails db:seed_fu`を実行してもデータが積み重なることはない。  


## その他

module/concerns/以下に、railsの共通部分をまとめるファイルを用意しメソッドやスコープを記述する。
例えばuserモデルでもpostモデルでも使うスコープなりメソッドがあった場合にまとめることができます。
