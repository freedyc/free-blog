---
title: ruby thin 服务器最大请求 URL 限制
date:  2020-11-10 10:08:59
tags: ruby
comments: true
---

# ruby thin 服务器最大请求 URL 限制

1. 请求头
当请求头超过112kb会抛出错误

2. 请求体
当请求体超过112kb会把请求移出内存，放入临时文件

## 上源码

```ruby
    # thin-1.7.2/lib/thin/request.rb限制
    
    # Maximum request body size before it is moved out of memory
    # and into a tempfile for reading.
    MAX_BODY          = 1024 * (80 + 32)
    BODY_TMPFILE      = 'thin-body'.freeze
    MAX_HEADER        = 1024 * (80 + 32)
    
    if @parser.finished?  # Header finished, can only be some more body
        @body << data
      else                  # Parse more header using the super parser
        @data << data
        raise InvalidRequest, 'Header longer than allowed' if @data.size > MAX_HEADER

        @nparsed = @parser.execute(@env, @data, @nparsed)

        # Transfer to a tempfile if body is very big
        move_body_to_tempfile if @parser.finished? && content_length > MAX_BODY
      end
```

```c
# thin-1.7.2/ext/thin_parser/thin.c
/* Defines the maximum allowed lengths for various input elements.*/
DEF_MAX_LENGTH(FIELD_NAME, 256);
DEF_MAX_LENGTH(FIELD_VALUE, 80 * 1024);
DEF_MAX_LENGTH(REQUEST_URI, 1024 * 12);
DEF_MAX_LENGTH(FRAGMENT, 1024); /* Don't know if this length is specified somewhere or not */
DEF_MAX_LENGTH(REQUEST_PATH, 2048);
DEF_MAX_LENGTH(QUERY_STRING, (1024 * 10));
DEF_MAX_LENGTH(HEADER, (1024 * (80 + 32)));
```

## 针对批量删除/编辑条数超过500条时会报bad Request分析和方案

问题分析：

查看thin源码thin-1.7.2/lib/thin/request.rb文件中定义

```ruby
MAX_HEADER = 1024 * (80 + 32)
```

代码中会判断

```ruby
raise InvalidRequest, 'Header longer than allowed' if @data.size > MAX_HEADER
```

操作日志信息会放在header中传输当删除条数过多时header长度会超过所定义长度，则报bad Request

## 解决方案

1. 长期考虑的话建议，停止使用data-description传操作日志信息，能使用提交参数记录尽量使用，不能则用_desc替代
2. 前台在生成data-description判断长度是否超过40kb，超过则放在body中传给后台
