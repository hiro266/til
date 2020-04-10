# 課題3 テキスト挿入時のバグ修正

## 実装

```
hoge = ''
hoge << if fuga.sentence?
        geho = fuga
        geho.age
```

上記のような場合、`hoge`に代入されるのは返り値である`geho.age`のみで`geho`は関係ない

- binding.pryをする時の注意  
返り値の位置(ブロックの最終行)に配置するとbinding.pryもメソッドのため  
自身が返り値となり、デバッグ中でも思わぬエラーがおこる  

- TypeError: no implicit conversion of nil into String  
文字列にnilは入れることはできない  
1. 条件分岐で`presence`と`nil`で処理を分ける  
2. nilガードでnilが入ったら、空文字列を代入  

```
# geho.ageがnilじゃなければ自身が、nilなら''が代入
geho.age ||= ''
```

## RSpec

新しい記述は特になし
