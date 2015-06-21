---
layout: default
title: Hiển thị thumbnail trong danh sách ý tưởng
permalink: thumbnails
---

# Tạo thumbnail với Carrierwave

*Viết bởi Miha Filej, [@mfilej](https://twitter.com/mfilej)*

**Huấn luyện viên**: Giải thích việc chỉ định chiều dài của ảnh trong HTML ở bước 4 có ý nghĩa gì và nó khác với việc thay đổi kích thước ảnh trên server thế nào.

## *1.* Cài đặt ImageMagick

- **OS X**: chạy `brew install imagemagick`. Nếu chưa có brew, bạn có thể [cài đặt Homebrew tại đây]( http://mxcl.github.io/homebrew/).
- **Windows**: tải về và chạy  [ImageMagick installer](http://www.imagemagick.org/script/binary-releases.php?ImageMagick=vkv0r0at8sjl5qo91788rtuvs3#windows) (sử dụng link *download* đầu tiên).
- **Linux**: Trên Ubuntu và Debian, chạy `sudo apt-get install imagemagick`. Sử dụng package manager phù hợp thay cho `apt-get` ở các bản Linux khác.

**Huấn luyện viên**: Giải thích ImageMagick là gì và nó khác các thư viện / gem chúng ta sử dụng trước đây như thế nào.

Mở `Gemfile` của dự án và thêm vào:

```ruby
gem 'mini_magick', '3.8.0'
```

dưới dòng

```ruby
gem 'carrierwave'
```

Trong terminal chạy:

```sh
bundle
```

## *2.* Thiết lập để ứng dụng tạo thumbnail khi có ảnh được tải lên

Mở `app/uploaders/picture_uploader.rb` và tìm tới dòng giống như sau:

```ruby
  # include CarrierWave::MiniMagick
```

và bỏ kí tự `#` đi.

**Huấn luyện viên**: Giải thích khái niệm comment (chú thích) trong code.

Dưới dòng bạn vừa sửa bên trên, thêm vào:

```ruby
version :thumb do
  process :resize_to_fill => [50, 50]
end
```

The images uploaded from now on should be resized, but the ones we already
have weren't affected. So edit one of the existing ideas and re-add a picture.

Như vậy những ảnh tải lên sau này sẽ được tạo thumbnail, nhưng những ảnh chúng ta đã tải lên trước đây vẫn không có. Chúng ta có thể sửa các idea và thêm lại ảnh để có thumbnail.

## *3.* Hiển thị các thumbnail

To see if the uploaded picture was resized ope

Để xem ảnh tải lên có được thay đổi kích thước hay chưa, hãy vào `app/views/ideas/index.html.erb`và sửa dòng:

```erb
<td><%= idea.picture %></td>
```

thành

```erb
<td><%= image_tag idea.picture_url(:thumb) if idea.picture? %></td>
```

Bây giờ, bạn hãy vào trình duyệt xem trang danh mục các ý tưởng (idea) và xem các thumbnail đã được hiển thị ở đó chưa.
