---
layout: post
title: "rails gem系列之settingslogic"
date: 2015-02-04 21:37
comments: true
categories: rails gem
---
##概要

可以从配置文件简单读取配置的gem

github地址：https://github.com/binarylogic/settingslogic

安装

```ruby
gem install settingslogic
```

定义class   app/models/settings.rb

```ruby
class Settings < Settingslogic
  source "#{Rails.root}/config/application.yml"
  namespace Rails.env
end
```

创建配置文件  config/application.yml

```ruby
defaults: &defaults
  cool:
    saweet: nested settings
  neat_setting: 24
  awesome_setting: <%= "Did you know 5 + 5 = #{5 + 5}?" %>

development:
  <<: *defaults
  neat_setting: 800

test:
  <<: *defaults

production:
  <<: *defaults
```

之后在rails console里面测试一下，就可以拿到配置文件里的值了

```ruby
>> Rails.env
=> "development"

>> Settings.cool
=> "#<Settingslogic::Settings ... >"

>> Settings.cool.saweet
=> "nested settings"

>> Settings.neat_setting
=> 800

>> Settings.awesome_setting
=> "Did you know 5 + 5 = 10?"
```