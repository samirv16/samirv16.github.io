---
layout: post
title:      "Rails API - handling errors"
date:       2020-08-15 03:35:41 +0000
permalink:  rails_api_-_handling_errors
---


Since most of the endpoints will need some kind of error handling, our goal should be to reduce boilerplate when adding new features. Even more importantly, this will reduce the risk that someone forgets to handle validation errors. The pattern that I want to have is handling errors behind the scenes:

```
def update
    @article = Article.find(params[:id])
    @article.update!(article_attributes)
  end
```

Moreover, I want to be able to define more error responses easily. There are not too many apps with only 404 and 422 responses.

How to achieve this? I will go through the development process step by step and you can stop as early as you want, even after first step. Every step will work just fine, but the further you go, the more control over error responses and exceptions handling you get.

The first step is using Rails’ rescue_from method. While you should be careful using this method, I think it is fairly safe to say that it can make your life much easier as long as it is properly used (and documented…) and as long as your application’s logic fits its usage pattern.

Using exceptions for flow control is sometimes considered as an anti-pattern, but I think that in this case it is really reasonable. The code executed in the rescue_from doesn’t have any side effects and its only result is an immediate error response.

In the Rails documentation you can see that rescue_from lets you define code which will be called when an exception of a given type is raised. Applying this to our example:

```
class ApplicationController < ActionController::API

  rescue_from ActiveRecord::RecordInvalid, with: :render_unprocessable_entity_response
  rescue_from ActiveRecord::RecordNotFound, with: :render_not_found_response

  def render_unprocessable_entity_response(exception)
    render json: exception.record.errors, status: :unprocessable_entity
  end

  def render_not_found_response(exception)
    render json: { error: exception.message }, status: :not_found
  end
end
```

```
class ArticlesController < ApplicationController
  def update
    @article = Article.find(params[:id])
    @article.update!(article_attributes)
  end
end
```

For very simple applications this might be enough. In the coming weeks I will discuss more about about what it actually returns and how to dive deeper into it.
