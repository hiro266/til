# 最新の記事一覧APIを作成する

jsonのserializerはfast_jsonapiを使用。

# 実装
[参考](https://tech.dely.jp/entry/2019/12/02/193000)

### Gemfile

```
gem 'fast_jsonapi'
```

### app/serializers/article_serializer.rb

```
$ rails g serializer Article title contents status
```

```
class ArticleSerializer
  include FastJsonapi::ObjectSerializer

  belongs_to :user
  attributes :title, :contents, :status
end
```
リレーション先の情報が欲しければそれを記述。

今回はArticleに紐づいたUser情報もjsonで返す課題だったため`belongs_to :user`を記述。

comment情報が欲しければ`has_many :comments`を追記

### articles_controller.rb

```
module Api
  module V1
    class ArticlesController < BaseController
      def index
        article = Article.all
        json_string = ArticleSerializer.new(article).serialized_json
        render json: json_string
      end
    end
  end
end
```

`json_string = ArticleSerializer.new(article).serialized_json`と`render json: json_string`がなくてもレスポンスのjsonは変わらなかった。

apiモードなので`render json`がなくてもjsonが返るのはデフォルトで決まっていて省略されていてもおかしくなさそう。

#### 実験
binding.pryで止めて実験

`ArticleSerializer.new(article)`

@resourceの中でインスタンスが格納されてる。

```
[4] pry(#<Api::V1::ArticlesController>)> ArticleSerializer.new(article)
=> #<ArticleSerializer:0x00007fc451053bc0
 @fieldsets={},
 @params={},
 @resource=
  [#<Article:0x00007fc44f3523c8
    id: 1,
    user_id: 1,
    title: "MyString1",
    contents: "MyText1",
    status: "draft",
    created_at: Sat, 27 Jun 2020 13:32:04 UTC +00:00,
    updated_at: Sat, 27 Jun 2020 13:32:04 UTC +00:00>,
   #<Article:0x00007fc44bbf7c98
    id: 2,
    user_id: 2,
    title: "MyString2",
    contents: "MyText2",
    status: "draft",
    created_at: Sat, 27 Jun 2020 13:32:04 UTC +00:00,
    updated_at: Sat, 27 Jun 2020 13:32:04 UTC +00:00>,
   #<Article:0x00007fc44bbf7bd0
```

`ArticleSerializer.new(article).serialized_json`

```
[5] pry(#<Api::V1::ArticlesController>)> ArticleSerializer.new(article).serialized_json
=> "{\"data\":[{\"id\":\"1\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString1\",\"contents\":\"MyText1\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"1\",\"type\":\"user\"}}}},{\"id\":\"2\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString2\",\"contents\":\"MyText2\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"2\",\"type\":\"user\"}}}},{\"id\":\"3\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString3\",\"contents\":\"MyText3\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"3\",\"type\":\"user\"}}}},{\"id\":\"4\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString4\",\"contents\":\"MyText4\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"4\",\"type\":\"user\"}}}},{\"id\":\"5\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString5\",\"contents\":\"MyText5\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"5\",\"type\":\"user\"}}}},{\"id\":\"6\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString6\",\"contents\":\"MyText6\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"6\",\"type\":\"user\"}}}},{\"id\":\"7\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString7\",\"contents\":\"MyText7\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"7\",\"type\":\"user\"}}}},{\"id\":\"8\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString8\",\"contents\":\"MyText8\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"8\",\"type\":\"user\"}}}},{\"id\":\"9\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString9\",\"contents\":\"MyText9\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"9\",\"type\":\"user\"}}}},{\"id\":\"10\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString10\",\"contents\":\"MyText10\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"10\",\"type\":\"user\"}}}}]}"
```

`ArticleSerializer.new(article).serializable_hash.to_json`

上記と変わらん

```
[6] pry(#<Api::V1::ArticlesController>)> ArticleSerializer.new(article).serializable_hash.to_json
=> "{\"data\":[{\"id\":\"1\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString1\",\"contents\":\"MyText1\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"1\",\"type\":\"user\"}}}},{\"id\":\"2\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString2\",\"contents\":\"MyText2\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"2\",\"type\":\"user\"}}}},{\"id\":\"3\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString3\",\"contents\":\"MyText3\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"3\",\"type\":\"user\"}}}},{\"id\":\"4\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString4\",\"contents\":\"MyText4\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"4\",\"type\":\"user\"}}}},{\"id\":\"5\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString5\",\"contents\":\"MyText5\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"5\",\"type\":\"user\"}}}},{\"id\":\"6\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString6\",\"contents\":\"MyText6\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"6\",\"type\":\"user\"}}}},{\"id\":\"7\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString7\",\"contents\":\"MyText7\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"7\",\"type\":\"user\"}}}},{\"id\":\"8\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString8\",\"contents\":\"MyText8\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"8\",\"type\":\"user\"}}}},{\"id\":\"9\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString9\",\"contents\":\"MyText9\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"9\",\"type\":\"user\"}}}},{\"id\":\"10\",\"type\":\"article\",\"attributes\":{\"title\":\"MyString10\",\"contents\":\"MyText10\",\"status\":\"draft\"},\"relationships\":{\"user\":{\"data\":{\"id\":\"10\",\"type\":\"user\"}}}}]}"
```
