---
layout: post
title: "rails gem系列之CarrierWave"
date: 2015-02-11 22:50
comments: true
categories: rails gem ruby
---
##概要
CarrierWave是rails中用来上传文件的gem。类似的gem还有PaperClip。

##和PaperClip的区别
1.PaperClip简单易用

2.CarrierWave的功能较多，应用广泛


##用法

先来做一个测试用的project吧

```ruby
rails new test
cd test
rails g scaffold Product name:string 
rake db:migrate
rails s
```

加入CarrierWave的gem

```ruby Gemfile
gem 'carrierwave'
```

安装

```ruby
bundle install
```

生成carrierwave的配置文件

```ruby
rails g uploader Image
      create  app/uploaders/image_uploader.rb
```

加入image列

```ruby
rails g migration add_image_to_product image:string
rake  db:migrate
```

向model中加入mount_uploader方法

```ruby
# app/models/product.rb
class Product < ActiveRecord::Base
  mount_uploader :image, ImageUploader
end
```

向form中加入上传组件，其中指定hidden属性image_cache的作用就是当提交form时发生error上传的文件或者图片可以保存起来，不用再上传一次。

```erb _form.html.erb
<!-- 开始 -->
  <div class="field">
    <% if @product.image? %>
      <div class="thumbnail">
        <%= image_tag @product.image.url %>
      </div>
    <% end %><br>
    <%= f.label :image %><br>
    <%= f.file_field :image %>
    <%= f.hidden_field :image_cache %>
  </div>
  <div class="field">
    <!-- 既存product且存在图片-->
    <% if @product.persisted? && @product.image? %>
      <label>
        <%= f.check_box :remove_image %>
        删除
      </label>
    <% end %>
  </div>
  <!-- 结束 -->
```

别忘了要在controller中加一下StrongParameter

```ruby products_controller.rb
def product_params
  params.require(:product).permit(:name, :price, :image, :image_cache, :remove_image)
end
```

添加显示部分的image_tag代码

```erb show.html.erb
<p>
  <strong>Image:</strong>
  <% if @product.image? %>
    <div class="thumbnail">
      <%= image_tag @product.image.url %>
    </div>
  <% end %>
</p>
```

就这些，大功告成，很简单。