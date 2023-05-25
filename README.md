# Build and Deploy CRA and NextJs

```bash

1. Build CRA khác gì so với Build Next
2. Làm sao để chạy được CRA, Next ở production (nên kèm theo giải thích)
3. Nginx là gì?, nginx đóng vai trò gì trong việc deploy?.


```

## Nginx

1. Tổng quan
   Với kiến trúc bất đồng bộ và khả năng mở rộng tốt, NGINX là lựa chọn hàng đầu cho việc xử lý lưu lượng truy cập web cao và đảm bảo hiệu suất cao cho các ứng dụng web phức tạp. NGINX cũng được sử dụng làm load balancer, HTTP cache, và cung cấp nhiều tính năng bảo mật như bảo vệ chống DDoS và SSL/TLS. Với sự phát triển nhanh chóng và sự hỗ trợ tuyệt vời từ cộng đồng, NGINX đã trở thành một công cụ quan trọng cho việc triển khai và quản lý các ứng dụng web trên Internet.

2. Khái niệm

- NGINX là phần mềm mã nguồn mở để phân phối web, reverse proxy, lưu vào bộ nhớ đệm, cân bằng tải, phát trực tuyến đa phương tiện, v.v. Nó bắt đầu như một máy chủ web được thiết kế để có hiệu suất tối đa và ổn định. Ngoài khả năng máy chủ HTTP, NGINX cũng có thể hoạt động như một máy chủ proxy cho email (IMAP, POP3 và SMTP) và reverse proxy và cân bằng tải cho các máy chủ HTTP, TCP và UDP.

- NGINX sở hữu kiến trúc bất đồng bộ, đó là một trong những đặc điểm làm nên sự phổ biến của nó. Cụ thể, kiến trúc bất đồng bộ của NGINX bao gồm một master process chịu trách nhiệm quản lý các worker process. Master process khởi tạo và quản lý các worker process, trong khi các worker process chịu trách nhiệm xử lý các yêu cầu của client. Với kiến trúc này, NGINX có thể xử lý đồng thời nhiều yêu cầu của client mà không gây tốn nhiều tài nguyên hệ thống.

- Ngoài ra, NGINX còn hỗ trợ nhiều tính năng quan trọng như load balancing, caching, SSL/TLS, compression, và chống DDoS. Load balancing cho phép phân phối lưu lượng truy cập đến các server ứng dụng khác nhau, giúp tăng hiệu suất và độ tin cậy của hệ thống. Caching giúp tăng tốc độ truy cập bằng cách lưu trữ các phiên bản tài nguyên trên server, tránh phải tải lại từ client mỗi lần truy cập. SSL/TLS cung cấp tính năng bảo mật cho các truy cập web, còn compression giúp giảm kích thước của các tài nguyên truyền tải. Cuối cùng, chống DDoS giúp đảm bảo an toàn và tránh những cuộc tấn công từ các kẻ tấn công.

![alt](https://cloud.z.com/vn/wp-content/uploads/2023/03/Screenshot_1.jpg)

3. NGINX hoạt động

- NGINX được xây dựng để cung cấp mức sử dụng bộ nhớ thấp và tính đồng thời cao. Thay vì tạo các quy trình mới cho mỗi yêu cầu web, NGINX sử dụng cách tiếp cận không đồng bộ, theo hướng sự kiện, trong đó các yêu cầu được xử lý trong một luồng duy nhất.

4. 1 số đặc điểm

- Reverse proxy với bộ nhớ đệm
- IPv6
- Cân bằng tải
- WebSockets
- Xử lý các tệp tĩnh, tệp chỉ mục và tự động lập chỉ mục
- TLS / SSL với SNI

## Cách build CRA trên production

- Tạo ứng dụng CRA bằng

```bash

npx create-react-app my-app

```

I. Buid ứng dụng

```bash

    npm run build

    -> Tạo ra 1 thư mục build. Đây chính là thư mục dùng để triển khai.

```

II. Triển khai ứng dụng (server phải được cài nodejs và npm)

1. Static Server

- Sử dụng 1 dịch vụ dựa trên môi trường Node là Serve:

```bash

npm install -g serve

serve -s build (build: đường dẫn tới forder build vừa chạy câu lệnh "npm run build")

```

- cũng có thể chọn cổng được bind cho ứng dụng:

```bash

serve -s build -l 5000

```

2. Cách khác

- Có thể sử dụng Node và Express(cái này cũng tương tự như Serve nhưng cần tạo 1 dịch vụ, còn bên trên đã dựng sẵn )

```bash

const express = require("express");

const path = require("path");

const app = express();

app.use(express.static(path.join(__dirname + "/public")));

const PORT = process.env.PORT || 5000;

app.listen(PORT);


```

- dirname là đường dẫn tới thư mục build

- run lệnh

```bash

    nodemon index.js

```

## Cách build NextJs trên production

- Tạo ứng dụng NextJs bằng

```bash

npx create-react-app my-app

```
