# 記事詳細API作成

relationshipsとしてUserのデータも追加。

# 実装

### app/serializers/user_serializer.rb

```
class UserSerializer
  include FastJsonapi::ObjectSerializer

  has_many :articles
  attributes :name, :email
end
```

### articles_controller.rb

```
module Api
  module V1
    class ArticlesController < BaseController
.
.
.
      def show
        article = Article.find(params[:id])
        options = { include: [:user, :'user.name', :'user.email'] }
        json_string = ArticleSerializer.new(article, options).serialized_json
        render json: json_string
      end
    end
  end
end
```

#### Userデータなし

`http://localhost:3000/api/v1/articles/1`

```
{"data":{"id":"1","type":"article","attributes":{"title":"MyString1","contents":"MyText1","status":"draft"},"relationships":{"user":{"data":{"id":"1","type":"user"}}}}}
```

#### Userデータあり

```
{"data":{"id":"1","type":"article","attributes":{"title":"MyString1","contents":"MyText1","status":"draft"},"relationships":{"user":{"data":{"id":"1","type":"user"}}}},"included":[{"id":"1","type":"user","attributes":{"name":"MyString1","email":"user+1@example.com"},"relationships":{"articles":{"data":[{"id":"1","type":"article"}]}}}]}
```

