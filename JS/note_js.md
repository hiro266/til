# 作りながら学ぶVue!Slack風クローンApp

## 用語

### node.js

- JavaScriptをサーバーサイド側で使えるようにするプラットフォーム

### npm

- node.jsのパッケージを管理するツール

`npm install`で`package.json`に記載されているパッケージをインストールできる

### パッケージ

- 世界中の誰かが作ったプログラム

### コンポーネント

- 一つのファイルに HTML、JavaScript、CSSがごっちゃになっているのを単一ファイルコンポーネント（Single File Component）。  
一般的には、コンポーネントと呼ばれる。

## 知識

- pages フォルダ配下に .vue ファイルを作ることでルーティングができる。  
→ pages/articles.vue http://localhost:3000/articles が生成

## コード

```
{ components: {　Logo　} }
{ components: {　Logo: Logo　} }

これらは同義でkey,valueが同じ時、短縮して記述することができる
```

### firestore(データベース)から情報を取得

#### plugins/firebase.js

```
import firebase from 'firebase/app'  // firebase 全般の機能を利用するために必要
import 'firebase/auth'  // ログイン機能を使うために読み込み
import 'firebase/firestore'  // データベース機能を使うために読み込み
// このようにfirebaseの機能を使う際は読み込む必要がある

// firebase の準備が出来ている場合のみに設定する
// 自身の環境を使用するために読み込み
if (!firebase.apps.length) {
  const config = {
    apiKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    authDomain: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    databaseURL: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    projectId: "xxxxxxxxxxxxxxxxxxxxxxxxxx",
    storageBucket: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    messagingSenderId: "xxxxxxxxxxxxxxxx",
    appId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    measurementId: "xxxxxxxxxxxxxxxxxxxxx"
  }
  firebase.initializeApp(config)  // config によって firebase の設定を行う
}

const db = firebase.firestore()  // データベースを定義
export {  // 別ファイルから firebase と db を利用できるように export 
  firebase,
  db
}
```

#### index.vue
```
<script>
import { db } from "~/plugins/firebase";

export default {
  components: {
    Messages,
    ChatForm
  },
  mounted() {
    // vue のコンポーネントが描画されたときに実行されるメソッド。index.vue が画面に表示されるたびにこの mounted という function が実行
    db.collection("channels") // firestore からデータを取得する場合は、channel id を指定して、doc id を指定
      .doc("XdBzGewmBetJF8P9y4NG")
      .get() // チャンネルidとドキュメントidに対してget()を実行すると doc という値が返ってくる
      .then(doc => {
        // thenはgetが成功した時に実行される
        console.log("doc.id: ", doc.id);
        console.log("doc.data(): ", doc.data());
      });
  }
};
</script>
  }
```

