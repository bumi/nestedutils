NESTED UTILS
===============

Easy handling of nested resources with support for custom domains. 

requires find_by_param plugin: http://github.com/bumi/find_by_param
[insert README here] ;)

If you have questions: michael@railslove.com

EXAMPLE:
===============

class ApplicationController < ActionController::Base
  include Railslove::Routes::NestedUtils
	helper_method :polymorphic_object_url,:polymorphic_object, :endmost_index_url, :current_url, :new_current_url, :edit_current_url, :scoped_url_for, :normalized_request_uri,
	before_filter :get_request_uri
end



URL: /posts/bumi/comments
> polymorphic_object # => Post.find_by_param("bumi")
> polymorphic_object! # => Post.find_by_param!("bumi") (raises an error if not found)


URL: /posts/bumi/comments/1/pictures/3
> polymorphic_object # => Picture.find_by_param(3)
> polymorphic_object(2) # => Comment.find_by_param(1)
> polymorphic_object(3) # => Post.find_by_param("bumi")

> current_url # => generated with post_comment_picture_url(...) -  /posts/bumi/comments/1/pictures/3

> init_polymorphic_variables # => sets @post, @comment and @picture - you can call this in a before_filter to set all instance variables of nested objects

> endmost_index_url# => /posts/bumi/comments/1/pictures


URL: /posts/bumi

> scoped_url_for(@comment) # => /posts/bumi/comments/25



NOTE if you use custom verbs on your resources add something like this to your application.rb

def verbs_to_ignore 
  %w{new edit activate}
end



Michael Bumann - Railslove.com