# Tìm hiểu về http
---
Thực hiện: **Phạm Văn Đạt**

## Mục lục   
[1. HTTP là gì?](#1)         
[2. HTTP - Các tham số](#2)          
[3. HTTP - Thông báo(Message)](#3)             
[4. HTTP - Yêu cầu(Request)](#4)            
[5. HTTP - Phản hồi(Response)](#5)                
[6. HTTP - Phương thức(Method)](#6)           
[7. HTTP - Mã hóa trạng thái](#7)            
[8. HTTP - Các trường Header](#8)             
[9. HTTP - Caching](#9)            
[10. Mã hóa URL](#10)             
[11. Bảo mật](#11)            
[12. Ví dụ về Massage](#12)  
           
---
# Nội dung

<a name="1"></a>
## 1. HTTP là gì?
 - HTTP là một giao thức cấp độ ứng dụng cho các hệ thống thông tin phân phối, cộng tác, đa phương tiện. Đây là nền tảng cho giao tiếp dữ liệu cho WWW (ví dụ: Internet) từ 1990.
 - HTTP là giao thức chung và stateless mà có thể được sử dụng cho các mục đích khác cũng như các sự co dãn của các phương thức được yêu cầu, các code lỗi và Hesder của nó.
 - HTTP là một giao thức giao tiếp trên cơ sở TCP/IP, mà được sử dụng phân phối dữ liệu(các tệp HTML, các file ảnh,..) trên www, Cổng mặng định là TCP 80. 
 - Chi tiết kỹ thuật HTTP xác định cách mà dữ liệu yêu cầu của Client sẽ được xây dựng và được gửi tới Server, và cách để server phản hồi các yêu cầu này.
**Các đặc trưng cơ bản**
 - Có 3 đặc trưng cơ bản:
     - **HTTP là giao thức connectionless(kết nối không liên tục)**: Client của HTTP. Là Client tạo 1 yêu cầu HTTP gửi tới Server và ngắt kết nối từ Client tới Server và đợi cho 1 phản hồi, sau đó Server sử lý yeu caaif và gưi lại phản hồi cho Client.
     - **HTTP là một phuong tiện đọc lập**: Bất kỳ dữ liệu nào cũng có thẻ gửi được bởi HTTP miễn alf Server và Client biết cách kiểm soát được nội dung dữ liệu. Yêu cầu Server và Client sử dụng kiểu MIME thích hợp để xác dịnhđược kiểu nội dung.
     - **HTTP là stateless**: HTTP là connectionless nên kết quả là HTTP trở thành một giao thức Stateless. Server và Client chỉ biết nhau tại thời điểm có yêu cầu hiện tại, sau đó cả hai sẽ quên nau luôn. Do bản chất của giao thức, cả Client và các trình duyệt có thể giữ lại thông tin giữa các yêu cầu khác nhau giữa các trang web.
 **- Cấu trúc cơ bản**
     - Sơ đồ biểu hiện cấu trúc đơn giản của một ứng dụng Web và miêu tả vị trí của HTTP:
<img src="">
     - Giao thức HTTP là gioa thức yêu cầu/phản hồi dự trên cấu trúc server/client, nơi mà các trình duyệt Web, các thiết bị tìm kiếm,... hoạt động như các client, và các server web hoạt động như server.
     - **Client**: Gửi yêu cầu tới Server theo mẫu cảu một phương thức yêu cầu, ỦI, và phiên bản giao thức, được theo bởi một thông báo MIME chứa các bộ chỉnh sửa yêu cầu, thông tin Client và nội dung có thể qua một kết nối TCP/IP.
     - **Server**: Phản hồi vói một dòng trạng thái, bao gồm phiên bản giao thức của thông báo và môt code thành công hoặc lỗi, theo sau bởi mỗi thông báo MIME chứa thông tin server, thông tin thực thể đa phuong tiện và nội dung đối tượng có thể.

<a name="2"></a>
## 2. HTTP - Các tham số
 -**Phiên bản HTTP**
     - HTTP sử dụng một sơ đồ đánh số ***<major>.<minor>*** để chỉ phiên bản của giao thức. Phiên bản của một thông báo HTTP được chỉ bởi một trường HTTP-Version trong dòng đầu tiên. Tại đây là cú pháp chung của việc xác định số phiên bản HTTP:

     `HTTP-Version ="HTTP" "/" 1*DIGIT "." 1*DIGIT`

      ví dụ:
     ```
     HTTP/1.0
     or
     HTTP/1.1
     ```

<a name="3"></a>
## 3. HTTP - Thông báo(Message)

<a name="4"></a>
## 4. HTTP - Yêu cầu(Request)

<a name="5"></a>
## 5. HTTP - Phản hồi(Response)

<a name="6"></a>
## 6. HTTP - Phương thức(Method)

<a name="7"></a>
## 7. HTTP - Mã hóa trạng thái

<a name="8"></a>
## 8. HTTP - Các trường Header

<a name="9"></a>
## 9. HTTP - Caching

<a name="10"></a>
## 10. Mã hóa URL

<a name="11"></a>
## 11. Bảo mật

<a name="12">## 12. Ví dụ về Massage</a>









