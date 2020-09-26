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
# パスと整合性取れるmodule名にしなければならない
module Api::ExceptionHandler
  # モジュールを読み込んだ時にインスタンスメソッドもクラスメソッドも両方読み込める
  extend ActiveSupport::Concern

  # モジュールがincludeされた後にこのメソッドが動作する
  included do
    rescue_from StandardError, with: :render_500
    rescue_from ActiveRecord::RecordNotFound, with: :render_404
  end

  private

  def render_404
    render_error('Record Not Found', 404)
  end

  def render_500
    render_error('Internal Server Error', 500)
  end

  def render_error(error_message, code)
    render json: error_message, status: code
  end
end
```

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
