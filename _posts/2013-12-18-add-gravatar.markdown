---
layout: default
title: Thêm Gravatar vào ứng dụng
permalink: gravatar
---

# Thêm Gravatar vào ứng dụng

*Viết bởi Catherine Jones*

Hướng dẫn này giả định rằng bạn đã tạo một ứng dụng Rails Girls tại [hướng dẫn xây dựng ứng dụng](http://guides.railsgirls.com/app/) và thêm tính năng xác thực (authentication) sử dụng [Devise](http://guides.railsgirls.com/devise/).

### Chú ý

Bạn cần có một địa chỉ email đã đăng kí với Gravatar để thực hiện theo hướng dẫn này. Nếu chưa có, bạn có thể đăng kí một tài khoản mới tại [gravatar.com](http://en.gravatar.com/).

## *1.* Thêm Gravtastic gem

Mở `Gemfile` và dưới `devise` gem, thêm vào

{% highlight ruby %}
gem 'gravtastic'
{% endhighlight %}

Trong terminal chạy

{% highlight sh %}
bundle install
{% endhighlight %}

Gravtastic gem sẽ được cài đặt. Hãy nhớ khởi động lại server.

## *2.* Thiết lập Gravatar cho ứng dụng

Mở `app/models/user.rb` và thêm đoạn code sau

{% highlight ruby %}
include Gravtastic
gravtastic
{% endhighlight %}

vào ngay sau dòng đầu tiên.

## *3.* Cấu hình Gravatar

Mở `app/views/layouts/application.html.erb` và giữa

{% highlight erb %}
<% if user_signed_in? %>
{% endhighlight %}

và

{% highlight erb %}
<% else %>
{% endhighlight %}

thêm

{% highlight erb %}
<%= image_tag current_user.gravatar_url %>
{% endhighlight %}

Bây giờ bạn có thể mở ứng dụng bằng trình duyệt và đăng nhập với email (đã được liên kết với 1 Gravatar). Bạn sẽ thấy Gravatar của bạn hiển thị trong ứng dụng.
