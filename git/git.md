# 知識

### .git/objects

- ローカルリポジトリ本体

### .git/config

- 設定ファイル

### origin

- リモートリポジトリ本体(origin = リモートリポジトリのURL)

### .gitignore

```
/ からスタート
ルートディレクトリを指定

/ で終了
以下を除外

* 任意のファイル全てを指定
/*/*.css
→ ルートディレクトリから一つ階層を潜ったcssファイル全てを除外
```

### HEAD

- 自分のいるブランチの最新のコミット

### ブランチ

- 並行して複数機能を開発するために必要

### コンフリクト

- 複数人が同じ箇所(同ファイル、同行)で別々の編集をした時にどちらを優先すべきかわからない状態

# コマンド

```
差分の確認

ワークツリー〜ステージ差分を確認する
git diff
git diff <ファイル名>

ステージ〜リポジトリ差分を確認する
git diff --staged
```

```
変更履歴を確認する

一行で表示
git log --oneline

ファイルの変更差分を表示(diff)
git log -p index.html

表示するコミット数を制限
git log -n <コミット数>
```

```
ファイルの削除

リポジトリからもワークツリーからも削除
git rm <ファイル名>
git rm -r <ディレクトリ名>
git rm -rf <ディレクトリ名(中身のファイルに記載があっても削除)>

リポジトリから削除、ワークツリーには残したい
git rm --cached <ファイル名>
```

```
ファイル削除 → 復元

git reset HEAD <ファイル名>
git checkout <ファイル名>

リポジトリから削除 → 復元
git reset HEAD <ファイル名>
```

```
ファイルの移動(ファイル名の変更)

git mv <旧ファイル> <新ファイル>
```

```
ファイル(ワークツリー)の変更を取り消す

ワークツリーをステージの状態と同じにする
→ addしてたら無理よ
git checkout -- <ファイル名>
git checkout -- <ディレクトリ名>

全変更の取り消し
git checkout -- .
```

```
ステージ(add)した変更を取り消す
(ワークツリーに変更はない)

ステージをリポジトリの最新コミット(HEAD)のファイル or ディレクトリに上書き
git reset HEAD <ファイル名>
git reset HEAD <ディレクトリ名>

全変更の取り消し
git reset HEAD .
```

```
ステージした変更を取り消してワークツリーからも変更を取り消す

git reset HEAD <ファイル名 or ディレクトリ名>
git checkout -- <ファイル名 or ディレクトリ名>
```

```
リモートを変更

git remote rename <旧リモート名> <新リモート名>
```

```
変更履歴をマージする

git merge <ブランチ名>
git merge <リモート名/ブランチ名>
```

```
コンフリクトがおきたら

コンフリクトの確認
git status
→ both modified: のファイルがコンフリクトしたファイル

最終的に望むファイルにしてコミットすればOK
```

