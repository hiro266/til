# 課題7 アイキャッチの表示サイズ / 位置指定

## 実装

- 表示されるアイキャッチ画像の横幅を指定した大きさで表示
→ アイキャッチ横幅用カラムを作成し、width = 横幅データ + "px"で結合でいけそう  
→ 横幅指定時と未指定時で条件分岐させる必要がありそう。  
→ データはintegerからstringにして結合 to_s  

- サイズのピクセル許容範囲の指定
→ validation?  
→ numericalityが使えそう  
→ [リファレンス](https://railsguides.jp/active_record_validations.html#numericality)

- 表示されるアイキャッチ画像の位置を左寄せ、中央、右寄せの中から選べるようにする

→ アイキャッチ位置用カラムを作成し、ラジオボタンで0(left),1(center),2(right)の数値をデータに保存  
→ emunで数値 → 文字列で扱いやすいように設定  
article.eyecatch_position.0? → article.left?  
→ 送られてきたデータを使用してtext-alignのプロパティを指定

## RSpec

- クリックして特定の編集画面へいきたい時はhrefで明示的に記述
```
click_link '編集', href: edit_admin_article_path(article.uuid)
```

- attach_file

ファイルアップロード。  
テスト用のデータは`fixtures`配下に置くのが通例？
```
attach_file 'article[eye_catch]', "#{Rails.root}/spec/fixtures/images/super_saiyan2.jpg"
```

- rand

テキストフィールドに指定の数値を入れる時などに使用
```
rand(100..700)
```

- choose
ラジオボタンのクリック

```
choose '右寄せ'
```

- have_selector
sectionタグのクラスにeye_catchとtext-rightがあることを期待する
```
expect(page).to have_selector('section.eye_catch.text-right')
```

## その他
