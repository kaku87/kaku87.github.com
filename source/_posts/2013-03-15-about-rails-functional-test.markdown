---
layout: post
title: "关于rails控制器的功能测试"
date: 2013-03-15 15:16
comments: true
categories: 
---

# 控制器的功能测试

     require File.dirname(__FILE__) + '/../test_helper'

关键在于setup方法，有三个东西
	1.controller
	2.request
	3.response

get()方法时由测试辅助类提供的，它会模拟controller的web请求，并获取控制器的响应，
然后用assert_response来检查是否应答正确

-n可以指定运行某一个特定的测试方法

     ruby test/functional/logni_controller_test.rb -n test_index

assert_redirected_to :action=>"login"

# Dynamic Fixtures

在夹具中也可以使用ruby代码动态加入

assert_template "index" 对模版进行断言

# 测试登录

	def test_login
	  dave = users(:dave)
	  post :login, :nmae=>dave.name, :password=>'secret'
	  assert_redirected_to :action=>"index"
	  assert_equal dave.id, session[:user_id]
	end

# HTTP请求方法

get()  对指定的action执行一次HTTP GET请求，并将结果放入HTTP RESPONSE

	例: get(action,parameteres=nil,session=nil,flash=nil)

post() 提交表单

	例: post :edit, :user => {:name => "dave", :age => "24"}

     模拟XMLHttp请求
     xhr(method,action,parameters,session,flash)

put(),delete(),head()

# 功能测试的断言

     assert_dom_equal(expected_html,actual_html,message)
     例:assert_dom_equal(expected,@response.body)
     
     assert_response(type,message)
     type的种类
     1.:success
     2.:redirect
     3.:missing
     4.:error
     例:assert_response :success
     
# 变量

     assigns(key=nil)
          assert_not_nil assigns["items"]
     session
          assert_equal 2, session[:cart].items.size
     flash
          assert_equal "Danger!", flash[:notice]
     cookies
          assert_equal "Danger!", cookies[:name]
     redirect_to_url
          assert_equal "http://test.host/login", redirect_to_url

# 辅助方法

     find_tag(conditions)
     find_all_tag(conditions)
     follow_redirect
     fixture_file_upload(path,mime_type)

# 测试response的content

   使用强大的assert_select

     assert_select "title",  "TEST"

     

     
