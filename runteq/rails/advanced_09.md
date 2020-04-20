# 課題9 トップ画像をスライダー形式に変更

## 実装

### セットアップ〜動作確認

**ruby:application.html**
```
# .minファイルはソースコードを必要最小限の記述にしてファイルサイズを小さくしたもの

<link rel="stylesheet" href="https://unpkg.com/swiper/css/swiper.css">
<link rel="stylesheet" href="https://unpkg.com/swiper/css/swiper.min.css">

<script src="https://unpkg.com/swiper/js/swiper.js"></script>
<script src="https://unpkg.com/swiper/js/swiper.min.js"></script>
```

**js:application.js**
```
var mySwiper = new Swiper('.swiper-container', {
});
```

**任意のファイル**
```
.swiper-container
  .swiper-wrapper
    .swiper-slide
      = image_tag 'imageのpath'
    .swiper-slide
      = image_tag 'imageのpath'
    .swiper-slide
      = image_tag 'imageのpath'
    .swiper-slide
      = image_tag 'imageのpath'
```


## RSpec

## その他

### .minファイル

- 通常ファイルよりもサイズの軽いファイル

> ファイルのサイズが小さいのは、ソースコードを必要最小限の記述にしているからで
> スクリプトの機能自体は変わらない。
> 変数名がたったの1文字で表されていたり、コメントでの説明が全て削除され、改行も全くない、グシャッと、ギュッとした形式で書かれている。

### 2つ以上ネストしたルーティング

```
Rails.application.routes.draw do
  namespace :admin do
    resource :site, only: %i[edit update destroy] do
      resources :attachments, controller: 'site/attachments', only: %i[destroy]
    end
  end
end
```

`resources :attachments, controller: 'site/attachments', only: %i[destroy]`  
明示的に記載する必要がある。
