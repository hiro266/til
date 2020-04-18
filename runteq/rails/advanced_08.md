# 課題8 埋め込みメディアタイプにTwitterの追加

## 実装

## RSpec

### system_specで、同一バリューを持っているボタンを区別

htmlの方でbuttonに name attributeを付与。  
<button name="aaaa">Submit</button> みたいなイメージ。  
そうすれば click_button 'aaaa' でクリックできる。  

## その他

### アイコン埋め込み方

```
'<i class="fa fa-youtube-play"></i>'.html_safe
```

### split

```
[1] pry(main)> article = 'hoge/192837483711'
=> "hoge/192837483711"
[2] pry(main)> article
=> "hoge/192837483711"
[3] pry(main)> article.split('/').last
=> "192837483711"
[4] pry(main)> article.split('/').first
=> "hoge"
```

