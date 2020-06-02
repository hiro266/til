## 3. GitHub Flow
GitHub Flowで開発を進めていただきます。

### 1.作業ディレクトリへ移動して、下記コマンドでtopicブランチを作成

`git checkout -b xxx`

（xxxには各課題で指定されるブランチ名を入力してください）

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/6f30337a6e6cf20e5b9d00c5999edf5b.png)](https://startup-technology.gyazo.com/6f30337a6e6cf20e5b9d00c5999edf5b)

### 2. 課題の要件に合わせて実装する

### 3. リモートリポジトリへpushする

例）

`git add [ファイル名]`

`git status`
(ステージングにファイルが存在しているか確認)

`git commit -m 'Add: ジェネレータに関する設定を追加'`

`git status`(適切にコミットされて変更差分がないことを確認)

`git push`(指定されたコマンドを確認)

`git push --set-upstream origin xxx(ブランチ名)`(指定されたコマンドを入力)

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/a6e21d594fb918ce69b91912a05cadcb.png)](https://startup-technology.gyazo.com/a6e21d594fb918ce69b91912a05cadcb)

### 4. RUNTEQの課題画面にてプルリクエストを作成

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/9955006167b54a4fc39764c4fe87ce45.png)](https://startup-technology.gyazo.com/9955006167b54a4fc39764c4fe87ce45)

### 5. 自動コードレビューを確認する
自動コードレビューが通るまで2-3を繰り返しましょう。

レビューにパスすると出てくるmergeボタンが出てきます

クリックして課題完了となります。

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/dd83ca2f01e0f86a68b159ca1fd46075.png)](https://startup-technology.gyazo.com/dd83ca2f01e0f86a68b159ca1fd46075)

### 6. 自己採点
課題の提出後に確認ポイントと解答例が出てきます。必ず学習するようにしましょう。

解答例を見て修正したい点があれば、次の課題の作業ブランチで修正してください。

### 7. 次の課題に進み1-6を繰り返す

### 8. 全ての課題が完了したらカリキュラム終了
