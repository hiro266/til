# 課題6 アクション権限の調整

## 実装

### authorize

アクション毎に権限の付与を行う。

**articles_controller.rb**
```
def destroy
  authorize(@article)
end
```

**article_policy.rb**
```
def destroy?
  user.admin? || user.editor?
end

private

def set_article
  @article = Article.find_by!(uuid: params[:uuid])
end
```

上記の場合、  
@articleがadmin or editorであれば  
destroyアクションを実行する権限がある。  
この権限判断を`authorize`でしている。


## RSpec

## その他
