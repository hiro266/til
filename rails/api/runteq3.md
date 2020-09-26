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

