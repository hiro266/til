# ID/PWを使って新規登録機能を作る

### registrations_controller.rb

```
# frozen_string_literal: true

module Api
  module V1
    class RegistrationsController < BaseController
      def create
        user = User.new(user_params)
        if user.save
          json_string = UserSerializer.new(user).serialized_json
          render json: json_string
        else
          raise ActionController::BadRequest
        end
      end

      private

      def user_params
        params.require(:user)
              .permit(:name, :email, :password)
      end
    end
  end
end
```

`raise ActionController::BadRequest`は`exception_handler.rb`に書き足さないとキャッチされない。

### exception_handler.rb

```
included do
  rescue_from StandardError, with: :render_500
  rescue_from ActionController::BadRequest, with: :render_400
  rescue_from ActiveRecord::RecordNotFound, with: :render_404
end

def render_400(exception)
  render_error(400, 'Bad Request', exception.message)
end
```

注意は、`rescue_form`は下から読み込まれるため、`StandardError`より上に書くと上書きされてしまうため注意が必要。
