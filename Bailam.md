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
* HTTP là một giao thức cấp độ ứng dụng cho các hệ thống thông tin phân phối, cộng tác, đa phương tiện. Đây là nền tảng cho giao tiếp dữ liệu cho WWW (ví dụ: Internet) từ 1990.
* HTTP là giao thức chung và stateless mà có thể được sử dụng cho các mục đích khác cũng như các sự co dãn của các phương thức được yêu cầu, các code lỗi và Hesder của nó.
* HTTP là một giao thức giao tiếp trên cơ sở TCP/IP, mà được sử dụng phân phối dữ liệu(các tệp HTML, các file ảnh,..) trên www, Cổng mặng định là TCP 80. 
* Chi tiết kỹ thuật HTTP xác định cách mà dữ liệu yêu cầu của Client sẽ được xây dựng và được gửi tới Server, và cách để server phản hồi các yêu cầu này.

**Các đặc trưng cơ bản**
 * Có 3 đặc trưng cơ bản:
   * **HTTP là giao thức connectionless(kết nối không liên tục)**: Client của HTTP. Là Client tạo 1 yêu cầu HTTP gửi tới Server và ngắt kết nối từ Client tới Server và đợi cho 1 phản hồi, sau đó Server sử lý yeu caaif và gưi lại phản hồi cho Client.
   * **HTTP là một phuong tiện đọc lập**: Bất kỳ dữ liệu nào cũng có thẻ gửi được bởi HTTP miễn alf Server và Client biết cách kiểm soát được nội dung dữ liệu. Yêu cầu Server và Client sử dụng kiểu MIME thích hợp để xác dịnhđược kiểu nội dung.
   * **HTTP là stateless**: HTTP là connectionless nên kết quả là HTTP trở thành một giao thức Stateless. Server và Client chỉ biết nhau tại thời điểm có yêu cầu hiện tại, sau đó cả hai sẽ quên nau luôn. Do bản chất của giao thức, cả Client và các trình duyệt có thể giữ lại thông tin giữa các yêu cầu khác nhau giữa các trang web.

**- Cấu trúc cơ bản**
 * Sơ đồ biểu hiện cấu trúc đơn giản của một ứng dụng Web và miêu tả vị trí của HTTP:
<img src="">   

 * Giao thức HTTP là giao thức yêu cầu/phản hồi dự trên cấu trúc server/client, nơi mà các trình duyệt Web, các thiết bị tìm kiếm,... hoạt động như các client, và các server web hoạt động như server.
 * **Client**: Gửi yêu cầu tới Server theo mẫu cảu một phương thức yêu cầu, ỦI, và phiên bản giao thức, được theo bởi một thông báo MIME chứa các bộ chỉnh sửa yêu cầu, thông tin Client và nội dung có thể qua một kết nối TCP/IP.
 * **Server**: Phản hồi vói một dòng trạng thái, bao gồm phiên bản giao thức của thông báo và môt code thành công hoặc lỗi, theo sau bởi mỗi thông báo MIME chứa thông tin server, thông tin thực thể đa phuong tiện và nội dung đối tượng có thể.

<a name="2"></a>
## 2. HTTP - Các tham số

**- Phiên bản HTTP**  
+ HTTP sử dụng một sơ đồ đánh số **<major>.<minor>** để chỉ phiên bản của giao thức. Phiên bản của một thông báo HTTP được chỉ bởi một trường HTTP-Version trong dòng đầu tiên. Tại đây là cú pháp chung của việc xác định số phiên bản HTTP:  
`HTTP-Version ="HTTP" "/" 1*DIGIT "." 1*DIGIT`

ví dụ:
```
      HTTP/1.0
      or
      HTTP/1.1
```

 **- Uniform Resource Identifiers - Bộ nhận diện nguồn tài nguyên đồng nhất**   
      - URI là một định dạng tài nguyên thống nhất (URI, viết tắt từ Uniform Resource Identifier) là một chuỗi ký tự được sử dụng để xác định, nhận dạng một tên hoặc một tài nguyên. Việc xác định như vậy cho phép tương tác với các thể hiện tài nguyên trên mạng (thường là World Wide Web) sử dụng các giao thức cụ thể.
      - Ví dụ:  
     ` URI="http:" "//" host [ ":" port ] [abs_path ["?" query]] `
      - Với: + **port** để trống thì tự hiểu là port 80
             + **abs_path** tương đương vs 1 "/".
             + **reserved** và **unsafe** tương đương với mã hóa "%" "HEX HEX" tương ứng.
      - Ví dụ các URI tương ứng
      ```
      http://abc.com:80/~smith/home.html
      http://ABC.com/%7Esmith/home.html
      http://ABC.com:/%7esmith/home.html
      ```

 **- Các định dạng Ngày/Thời gian**  
      - Tất cả các nhãn Ngày/Thời gian HTTP Phải được biểu diễn trong Greenwich Mean Time (GMT), không có sự ngoại trừ. Các ứng dụng HTTP được cho phép để sử dụng 3 nhãn đại diện Ngày/Thời gian sau:
      ```
      Sun, 06 Nov 1994 08:49:37 GMT  ; RFC 822, updated by RFC 1123
      Sunday, 06-Nov-94 08:49:37 GMT ; RFC 850, obsoleted by RFC 1036
      Sun Nov  6 08:49:37 1994       ; ANSI C's asctime() format
      ```

 **- Các bộ ký tự**   
      - Chúng ta sử dụng các bộ ký tự để xác định các thiết lập ký tự mà Client ưa thích. Nhiều bộ thiết lập ký tự có thể được liệt kê riêng biệt bởi các dấu phảy. Nếu một giá trị là không được xác định, mặc định là US-ASII.
      - Ví dụ:
      ```
      US-ASCII

      or

      ISO-8859-1

      or 

      ISO-8859-7
      ```

 **- Mã hóa nội dung**   
      - Là một thuật toán mã hóa đã được sử dụng để mã hóa nooin dung trước khi nó được truyền đi. Mã háo nội dung được dùng để nén dữ liệu để cho thông tin được nhẹ hơn và chuyền tải giễ dàng hơn hoặc làm cho thông tin hoàn thiện và đảm bảo hơn trước khi truyền đi mà không bị thất lạc nhận diện.
      - Tất cả các giá trị mã hóa nội dung là không phân biệt kiểu chữ (case-insensitive). HTTP/1.1 sử dụng các giá trị mã hóa nội dung trong các trường Accept-Encoding và Content-Encoding Header mà chúng ta sẽ quan sát trong các chương kế tiếp.
      - Ví dụ: sơ đồ mã hóa hợp lệ
      ```
      Accept-encoding: gzip

      or

      Accept-encoding: compress

      or 

      Accept-encoding: deflate
      ```

 **- Các kiểu đa phương tiện (media types)**   
      - HTTP sử dụng các Kiểu phương tiện Internet trong các trường **Content-Type** và **Accept** để cung cấp dữ liệu mở và có thể mở rộng. Tất cả các giá trị kiểu phương tiện được đăng ký với IANA (Internet Assigned Number Authority). Cú pháp chung để xác định kiểu phương tiện như sau:
      ```
      media-type     = type "/" subtype *( ";" parameter )
      ```
      Các thuộc tính type, subtype và parameter là case-insentive 
      Ví dụ:
      `Accept: image/gif`
 **- Các thẻ ngôn ngữ**   
      - HTTP sử dụng các thẻ ngôn ngữ trong các trường Accept-Language và Content-Language. Một thẻ ngôn ngữ bao gồm một hoặc nhiều phần: Một thẻ ngôn ngữ sơ cấp và một dãy các thẻ phụ:
      `language-tag  = primary-tag *( "-" subtag )` Các khoảng trắng không được cho phép trong thẻ và tất cả các thẻ là case-insentive.
      - Ví dụ: Các thẻ ví dụ bao gồm:
      ```
      en, en-US, en-cockney, i-cherokee, x-pig-latin
      ```
      - Hai chữ primary-tag là một chữ viết tắt cho ngôn ngữ trong ISO-639 và hai ký tự đầu tiên trong thẻ phụ subtag là mã quốc gia.


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

<a name="12"></a>
## 12. Ví dụ về Massage









