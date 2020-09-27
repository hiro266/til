# HTTPステータスコードを理解する

404, 500のレスポンスを用意。

# 実装

エラーハンドリングは`base_controller.rb(もしくはapplicagion_controller.rb)`に記述して検知させたいが直接書くとFatになるため、moduleに切り出す。

複数コントローラーやモデルから利用する処理は`controllers/concerns`配下にモジュールとして切り出して記述することが多い。

`app/controllers/concerns/api/exception_handler.rb`

```
# extend ActiveSupport::Concern を有効にするための読み込み
require 'active_support'
# 名前空間のためApi::を挟む
module Api::ExceptionHandler
  # モジュールを読み込んだ時にインスタンスメソッドもクラスメソッドも両方読み込める
  extend ActiveSupport::Concern

  # モジュールがincludeされた後にこのメソッドが動作する
  included do
    rescue_from StandardError, with: :render_500
    rescue_from ActiveRecord::RecordNotFound, with: :render_404
  end

  private
  
  # 
  def render_404(exception)
    render_error(404, 'Record Not Found', exception.message)
  end

  def render_500(exception)
    render_error(500, 'Internal Server Error', exception.message)
  end
  
  # *で配列(インデックス一つしかないのに配列にしてある理由は不明)にしているのはRUNTEQのRspec対策。なくても動作上は問題なし。
  def render_error(code, message, *error_messages)
    response = {
        message: message,
        errors: error_messages
    }

    render json: response, status: code
  end
end

```

### pryで止めてパラメータ確認

```
[1] pry(#<Api::V1::ArticlesController>)> exception
=> #<ActiveRecord::RecordNotFound: Couldn't find Article with 'id'=hoge>
[2] pry(#<Api::V1::ArticlesController>)> exception.message
=> "Couldn't find Article with 'id'=hoge"

[1] pry(#<Api::V1::ArticlesController>)> response
=> {:message=>"Record Not Found", :errors=>["Couldn't find Article with 'id'=hoge"]}
```

exceptionには例外の内容、exception.messageでエラーメッセージにアクセスできる。

render_404(exception)とすることで使用可能。




`base_controller.rb`

includeで切り出したmodule呼び出したら完了。

```
module Api
  module V1
    class BaseController < ApplicationController
      include Api::ExceptionHandler
    end
  end
end
```
