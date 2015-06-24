---
layout: default
title: Continuous Deployment với Codeship
permalink: continuous
---

# Continuous Deployment với Codeship

*Viết bởi Floor Drees, [@floordrees](https://twitter.com/floordrees)*

## Continuous Deployment là gì?

Continuous Deployment là một phần của "phong trào" chuyển phát liên tục (continuous delivery). Ý tưởng của chuyển phát liên tục là tự động hóa càng nhiều càng tốt quá trình chuyển phát phần mềm.

Với một dây chuyền continuous deployment đang hoạt động, bạn sẽ thi hành Git deployment (triển khai ứng dụng với Git) (mọi thứ phải được commit để được test, và mọi thứ phải được test trước khi được deploy). Điều này sẽ làm cho việc phối hợp trở lên dễ dàng hơn và triển khai (deploy) ứng dụng nhanh hơn. Bạn sẽ có nhiều thời gian hơn tập trung cho phát triển ứng dụng, làm nó trở lên ngày càng tốt hơn.

Một vài công ty tuyệt vời đang mở đường cho làn sóng continuous deployment, và trong hướng dẫn này chúng ta sẽ cùng thiết lập qui trình continuous deployment cho ứng dụng Ruby on Rails của mình từ Github tới Heroku thông qua [Codeship](http://www.codeship.io).

**Huấn luyện viên**: Nói về các lợi ích của continuous deployment.

## Đăng kí tài khoản Codeship

Đầu tiên bạn cần [một tài khoản Codeship](https://www.codeship.io/). Đăng nhập Codeship thông qua tài khoản Github. Codeship cần truy cập vào các repositories trong tài khoản Github của bạn để thiết lập continuous deployment, vì thế hãy chắc chắn rằng bạn cấp quyền truy cập cho Codeship.

Trở lại với Codeship, hãy cùng khởi tạo dự án đầu tiên. Bước thứ nhất là lựa chọn GitHub làm nhà cung cấp repository. Trong danh sách các GitHub repositories, tìm repository bạn muốn cài đặt và chọn nó. Vì chúng ta đang làm ứng dụng `railsgirls` nên bạn có thể sẽ muốn chọn repository `railsgirls`.

Bây giờ, repository của bạn đã được kết nối (với Codeship), bạn có thể thiết lập các lệnh test. Bởi vì chúng ta đang làm việc với ứng dụng Ruby on Rails nên bạn hãy chọn "Ruby on Rails" là framework đang sử dụng. Codeship sẽ dựa trên lựa chọn này tạo ra những lệnh cài đặt và test phù hợp cho ứng dụng của bạn. Các lệnh test được tạo sẵn nhưng nằm ở trạng thái comment (dòng lệnh bắt đầu với kí tự `#`), bạn có thể uncomment các lệnh muốn sử dụng. Hiện tại có thể ứng dụng của bạn chưa cài đặt test nên bạn có thể bỏ qua phần này và quay lại cài đặt sau.

Hoàn tất quá trình thiết lập và đi tới bảng điều khiển (dashboard). Bạn có thể kích hoạt một "bản build mới" cho ứng dụng bằng việc thay đổi cái gì đó trong ứng dụng và push các thay đổi lên repository:

```sh
git add .  
git commit -m "test Codeship integration"  
git push origin master
```

Bạn có thể xem thông tin chi tiết về bản build bằng cách nhấn vào mũi tên phía bên phải. Bạn có thể quan sát trong khi bản build này đang chạy. Bảo đảm hay hơn chương tình truyền hình thực tế.

... và vài giây sau, bản build chạy thành công! Bạn có thể thấy tất cả các lệnh đã được chạy: sau vài lệnh chuẩn bị ban đầu, Codeship sẽ chạy các lệnh bạn chỉ định lúc trước. Bạn có thể xem các output của một lệnh cụ thể bằng cách nhấn vào lệnh đó.

Như vậy bạn đã vừa push code lên repository, xem log của bản build và có được một green build (bản build thành công). Chúc mừng bạn và hãy cùng sang bước tiếp theo.

## Cài đặt Continuous Deployment

Bây giờ, hãy cùng triển khai (deploy) ứng dụng của bạn lên Heroku. Nhấn vào thiết lập dự án (project settings) ở góc trên bên phải, chọn "Deployment" từ danh sách. Bạn sẽ được chuyển tới trang thiết lập "Deployment". Vì chúng ta dự định triển khai dự án lên Heroku nên bạn hãy nhấn vào logo của "Heroku".

Bạn sẽ được đề nghị nhập tên ứng dụng của mình trên Heroku cũng như API key. Để có API key, bạn có thể vào trang [tài khoản của mình trên Heroku](https://dashboard.heroku.com/account) và nhấn vào nút có nội dung "Show API key". Nhập tên ứng dụng và API key của bạn và lưu thiết lập này lại.

Vậy là từ bây giờ Codeship sẽ triển khai ứng dụng của bạn lên Heroku tự động mỗi khi bạn push code lên GitHub repository của mình. Tuyệt vời!

## Cùng thử nghiệm

Bây giờ hãy cùng push một thay đổi và xem thay đổi đó có được deploy hay không. Thay đổi một chút cho ứng dụng của bạn (tiêu đề ứng dụng chẳng hạn), rồi commit và push thay đổi đó lên Github.

```sh
git add .  
git commit -m "this changes everything"  
git push
```

Và ngay sau đó, một bản build mới sẽ bắt đầu chạy trên Codeship. Ứng dụng của bạn sẽ được triển khai tự động lên Heroku và bạn có thể thấy những thay đổi bạn vừa thực hiện trên ứng dụng của mình trên Internet chỉ sau 1 - 2 phút.
