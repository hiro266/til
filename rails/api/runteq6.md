# ID/PWを使ってログイン機能を作る

### api/v1/authenticationsでPOST形式のリクエストを受け取る
authentications_controller.rbのcreateメソッドで受け取れる。

(POSTだからcreateメソッドね)

# 実装

`app/controllers/api/v1/authentications_controller.rb`

```
module Api
  module V1
    class AuthenticationsController < BaseController
      def create
        authentication = login(params[:email], params[:password])
        if authentication
          json_string = UserSerializer.new(current_user).serialized_json
          render json: json_string
        else
          render_404
        end
      end

      private

      def form_authenticity_token; end
    end
  end
end
```

ログイン成功：ログインユーザーのデータをjson形式で返す

ログイン失敗：render_404メソッド呼び出し

render404はbase_controller.rbで`include Api::ExceptionHandler`してるから使用可能。

`app/controllers/concerns/api/exception_handler_controller.rb`

**変更前**

```
def render_404(exception)
  render_error(404, 'Record Not Found', exception.message)
end
```

**変更後**

```
def render_404(exception = nil)
  render_error(404, 'Record Not Found', exception&.message)
end
```

exception = nil にしておかないと引数なしでrender_404を呼び出せない。

exception&.message ぼっち演算子にして、exceptionがnilだった時はメソッド呼び出さないようにする。
