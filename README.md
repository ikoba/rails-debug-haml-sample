# 準備

```sh
bundle install

bundle exec rails s
```

http://localhost:3000
にアクセスします。

# Hamlに binding.xxx を仕込んだ結果
## binding.b

app/views/hello/index.html.haml
```
- binding.b
%span Hello
```

コンソール
```
Started GET "/" for ::1 at 2022-11-30 10:02:57 +0900
Processing by HelloController#index as HTML
  Rendering layout layouts/application.html.erb
  Rendering hello/index.html.haml within layouts/application
[1, 4] in ~/dev/src/github.com/ikoba/rails-debug-haml-sample/app/views/hello/index.html.haml
=>   1|           def _app_views_hello_index_html_haml___4460360376425139889_21340(local_assigns, output_buffer)
     2|             @virtual_path = "hello/index";;@output_buffer = output_buffer || ActionView::OutputBuffer.new;  binding.b;
     3| ; @output_buffer.safe_concat(("<span>Hello</span>\n".freeze)); @output_buffer
     4|           end
=>#0	#<Class:0x00000001062020b8>#_app_views_hello_index_html_haml___4460360376425139889_21340(local_assigns={}, output_buffer="") at ~/dev/src/github.com/ikoba/rails-debug-haml-sample/app/views/hello/index.html.haml:1
  #1	[C] Kernel#public_send at ~/.rbenv/versions/3.1.2/lib/ruby/gems/3.1.0/gems/actionview-7.0.4/lib/action_view/base.rb:244
  # and 114 frames (use `bt' command for all frames)
```

### debugの最新masterを使用した場合のコンソール

```
Started GET "/" for ::1 at 2022-11-30 10:28:18 +0900
Processing by HelloController#index as HTML
  Rendering layout layouts/application.html.erb
  Rendering hello/index.html.haml within layouts/application
[1, 2] in ~/dev/src/github.com/ikoba/rails-debug-haml-sample/app/views/hello/index.html.haml
=>   1| - binding.b
     2| %span Hello
=>#0	#<Class:0x000000010621ad20>#_app_views_hello_index_html_haml___3425911851805557894_21340(local_assigns={}, output_buffer="") at ~/dev/src/github.com/ikoba/rails-debug-haml-sample/app/views/hello/index.html.haml:1
  #1	[C] Kernel#public_send at ~/.rbenv/versions/3.1.2/lib/ruby/gems/3.1.0/gems/actionview-7.0.4/lib/action_view/base.rb:244
  # and 114 frames (use `bt' command for all frames)
(ruby) q!
Exiting
  Rendered hello/index.html.haml within layouts/application (Duration: 46473.6ms | Allocations: 154833)
  Rendered layout layouts/application.html.erb (Duration: 46474.1ms | Allocations: 154947)
Completed   in 46478ms (ActiveRecord: 0.0ms | Allocations: 157888)
```

## binding.pry

app/views/hello/index.html.haml
```
- binding.pry
%span Hello
```

コンソール
```
Started GET "/" for ::1 at 2022-11-30 09:56:30 +0900
Processing by HelloController#index as HTML
  Rendering layout layouts/application.html.erb
  Rendering hello/index.html.haml within layouts/application

From: /Users/idai/dev/src/github.com/ikoba/rails-debug-haml-sample/app/views/hello/index.html.haml:2 #<Class:0x00000001093e6d18>#_app_views_hello_index_html_haml___2228876407865889475_23060:

    1: - binding.pry
 => 2: %span Hello
```