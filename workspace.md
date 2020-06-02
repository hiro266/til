## 3. GitHub Flow
GitHub Flowで開発を進めていただきます。

### 1.作業ディレクトリへ移動して、下記コマンドでtopicブランチを作成

`git checkout -b xxx`

（xxxには各課題で指定されるブランチ名を入力してください）

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/63f3e605248a7fe49a22346ae35748be.png)](https://startup-technology.gyazo.com/63f3e605248a7fe49a22346ae35748be)

### 2. 課題の要件に合わせて実装する

### 3. リモートリポジトリへpushする

例）

`git add [ファイル名]`

`git status`(ステージングにファイルが存在しているか確認)

`git commit -m '(適切な内容のコミットメッセージ)`

`git status`(適切にコミットされて変更差分がないことを確認)

`git push`(指定されたコマンドを確認)

`git push --set-upstream origin xxx(ブランチ名)`(指定されたコマンドを入力)

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/5c4ea7083ce69b7c1ebd255635472425.png)](https://startup-technology.gyazo.com/5c4ea7083ce69b7c1ebd255635472425)

### 4. RUNTEQの課題画面にてプルリクエストを作成

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/35619eb70ed0af25c9231b0a60d497a2.png)](https://startup-technology.gyazo.com/35619eb70ed0af25c9231b0a60d497a2)

### 5. 自動コードレビューを確認する
自動コードレビューが通るまで2-3を繰り返しましょう。

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/165d3ca5cdcf32ba9a5bb7e329b5f279.png)](https://startup-technology.gyazo.com/165d3ca5cdcf32ba9a5bb7e329b5f279)

レビューに合格（LGTM）するとmergeボタンが出てきます。
このボタンをクリックすると課題完了となり、RUNTEQ側のリモートリポジトリでマージ作業が行われます。

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/b3824350cc75e242421dfb3e40879987.png)](https://startup-technology.gyazo.com/b3824350cc75e242421dfb3e40879987)

### 6. 自己採点
課題の提出後に確認ポイントと解答例が出てきます。

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/5cce54462d547165de546252dcc1a6f3.png)](https://startup-technology.gyazo.com/5cce54462d547165de546252dcc1a6f3)

必ず確認してポイントの内容を学習するようにしましょう。

解答例を見て修正したい点があれば、次の課題の作業ブランチで修正してください。

### 7. 次の課題に進み1-6を繰り返す

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/5d5ece0cc9a992cfad3e3abeb2560953.png)](https://startup-technology.gyazo.com/5d5ece0cc9a992cfad3e3abeb2560953)

ローカルの作業ブランチをmasterに切り替えて、リモートリポジトリでマージされて更新されたmasterの情報を`git pull`コマンドで取り込みましょう。

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/ef4508f7f93e9e6c080a1cbb87de332c.png)](https://startup-technology.gyazo.com/ef4508f7f93e9e6c080a1cbb87de332c)

`git log`コマンドで ローカルとリモートのコミット履歴が同じことが確認できたら、`git checkout -b` コマンドで新しい作業ブランチを作成します。

[![Image from Gyazo](https://t.gyazo.com/teams/startup-technology/72d5b29f1f334c6060e80da72361a7cd.png)](https://startup-technology.gyazo.com/72d5b29f1f334c6060e80da72361a7cd)

### 8. 全ての課題が完了したらカリキュラム終了
