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

- **Các đặc trưng cơ bản**
 * Có 3 đặc trưng cơ bản:
      * **HTTP là giao thức connectionless(kết nối không liên tục)**: Client của HTTP. Là Client tạo 1 yêu cầu HTTP gửi tới Server và ngắt kết nối từ Client tới Server và đợi cho 1 phản hồi, sau đó Server sử lý yeu caaif và gưi lại phản hồi cho Client.
      * **HTTP là một phuong tiện đọc lập**: Bất kỳ dữ liệu nào cũng có thẻ gửi được bởi HTTP miễn alf Server và Client biết cách kiểm soát được nội dung dữ liệu. Yêu cầu Server và Client sử dụng kiểu MIME thích hợp để xác dịnhđược kiểu nội dung.
      * **HTTP là stateless**: HTTP là connectionless nên kết quả là HTTP trở thành một giao thức Stateless. Server và Client chỉ biết nhau tại thời điểm có yêu cầu hiện tại, sau đó cả hai sẽ quên nau luôn. Do bản chất của giao thức, cả Client và các trình duyệt có thể giữ lại thông tin giữa các yêu cầu khác nhau giữa các trang web.

- **Cấu trúc cơ bản**
 * Sơ đồ biểu hiện cấu trúc đơn giản của một ứng dụng Web và miêu tả vị trí của HTTP:
 <img src="http://imageshack.com/a/img923/5160/VC8oSU.png"/>   

 * Giao thức HTTP là giao thức yêu cầu/phản hồi dự trên cấu trúc server/client, nơi mà các trình duyệt Web, các thiết bị tìm kiếm,... hoạt động như các client, và các server web hoạt động như server.
 * **Client**: Gửi yêu cầu tới Server theo mẫu cảu một phương thức yêu cầu, ỦI, và phiên bản giao thức, được theo bởi một thông báo MIME chứa các bộ chỉnh sửa yêu cầu, thông tin Client và nội dung có thể qua một kết nối TCP/IP.
 * **Server**: Phản hồi vói một dòng trạng thái, bao gồm phiên bản giao thức của thông báo và môt code thành công hoặc lỗi, theo sau bởi mỗi thông báo MIME chứa thông tin server, thông tin thực thể đa phuong tiện và nội dung đối tượng có thể.

<a name="2"></a>
## 2. HTTP - Các tham số

**- Phiên bản HTTP** 

 * HTTP sử dụng một sơ đồ đánh số `<major>.<minor>` để chỉ phiên bản của giao thức. Phiên bản của một thông báo HTTP được chỉ bởi một trường HTTP-Version trong dòng đầu tiên. Tại đây là cú pháp chung của việc xác định số phiên bản HTTP:  
`HTTP-Version ="HTTP" "/" 1*DIGIT "." 1*DIGIT`

ví dụ:
```
      HTTP/1.0
      or
      HTTP/1.1
```

**- Uniform Resource Identifiers - Bộ nhận diện nguồn tài nguyên đồng nhất**   
 * URI là một định dạng tài nguyên thống nhất (URI, viết tắt từ Uniform Resource Identifier) là một chuỗi ký tự được sử dụng để xác định, nhận dạng một tên hoặc một tài nguyên. Việc xác định như vậy cho phép tương tác với các thể hiện tài nguyên trên mạng (thường là World Wide Web) sử dụng các giao thức cụ thể.
 * Ví dụ:   
` URI="http:" "//" host [ ":" port ] [abs_path ["?" query]] `
 * Với: * **port** để trống thì tự hiểu là port 80
        * **abs_path** tương đương vs 1 "/".
        * **reserved** và **unsafe** tương đương với mã hóa "%" "HEX HEX" tương ứng.
 * Ví dụ các URI tương ứng
```
  http://abc.com:80/~smith/home.html
  http://ABC.com/%7Esmith/home.html
  http://ABC.com:/%7esmith/home.html
```

**- Các định dạng Ngày/Thời gian**  
 * Tất cả các nhãn Ngày/Thời gian HTTP Phải được biểu diễn trong Greenwich Mean Time (GMT), không có sự ngoại trừ. Các ứng dụng HTTP được cho phép để sử dụng 3 nhãn đại diện Ngày/Thời gian sau:
```
 Sun, 06 Nov 1994 08:49:37 GMT  ; RFC 822, updated by RFC 1123
 Sunday, 06-Nov-94 08:49:37 GMT ; RFC 850, obsoleted by RFC 1036
 Sun Nov  6 08:49:37 1994       ; ANSI C's asctime() format
```

**- Các bộ ký tự**   
 * Chúng ta sử dụng các bộ ký tự để xác định các thiết lập ký tự mà Client ưa thích. Nhiều bộ thiết lập ký tự có thể được liệt kê riêng biệt bởi các dấu phảy. Nếu một giá trị là không được xác định, mặc định là US-ASII.
 * Ví dụ:
```
 US-ASCII

 or

 ISO-8859-1

 or 

 ISO-8859-7
```

**- Mã hóa nội dung**   
 * Là một thuật toán mã hóa đã được sử dụng để mã hóa nooin dung trước khi nó được truyền đi. Mã háo nội dung được dùng để nén dữ liệu để cho thông tin được nhẹ hơn và chuyền tải giễ dàng hơn hoặc làm cho thông tin hoàn thiện và đảm bảo hơn trước khi truyền đi mà không bị thất lạc nhận diện.
 * Tất cả các giá trị mã hóa nội dung là không phân biệt kiểu chữ (case-insensitive). HTTP/1.1 sử dụng các giá trị mã hóa nội dung trong các trường Accept-Encoding và Content-Encoding Header mà chúng ta sẽ quan sát trong các chương kế tiếp.
 * Ví dụ: sơ đồ mã hóa hợp lệ
```
 Accept-encoding: gzip

 or

 Accept-encoding: compress

 or 

 Accept-encoding: deflate
```

**- Các kiểu đa phương tiện (media types)**   
 * HTTP sử dụng các Kiểu phương tiện Internet trong các trường **Content-Type** và **Accept** để cung cấp dữ liệu mở và có thể mở rộng. Tất cả các giá trị kiểu phương tiện được đăng ký với IANA (Internet Assigned Number Authority). Cú pháp chung để xác định kiểu phương tiện như sau:
```
 media-type     = type "/" subtype *( ";" parameter )
```
 Các thuộc tính type, subtype và parameter là case-insentive 
 * Ví dụ:
`Accept: image/gif`

**- Các thẻ ngôn ngữ**   
 * HTTP sử dụng các thẻ ngôn ngữ trong các trường Accept-Language và Content-Language. Một thẻ ngôn ngữ bao gồm một hoặc nhiều phần: Một thẻ ngôn ngữ sơ cấp và một dãy các thẻ phụ:
`language-tag  = primary-tag *( "-" subtag )` 
 Các khoảng trắng không được cho phép trong thẻ và tất cả các thẻ là case-insentive.
 * Ví dụ: Các thẻ ví dụ bao gồm:
```
 en, en-US, en-cockney, i-cherokee, x-pig-latin
```
 * Hai chữ primary-tag là một chữ viết tắt cho ngôn ngữ trong ISO-639 và hai ký tự đầu tiên trong thẻ phụ subtag là mã quốc gia.


<a name="3"></a>
## 3. HTTP - Thông báo(Message)
* HTTP được xây dựng trên cơ sở mô hình Client-Server và giao thức Stateless các yêu cầu/phản hồi được trao đổi các thông báo(Message) dọc theo một lết nối TCP/IP
* Một Client là một chương trình mà thiết lập một kết nối tới một Server cho mục đích gửi một hoặc nhiều thông báo yêu cầu HTTP. Một HTTP Server là một chương trình mà chấp nhận các kết nối để phụ vụ các yêu cầu HTTP bởi việc gửi các thông báo phản hồi HTTP.
* HTTP sử dụng URI để nhận diện một nguồn đã cho và để thiết lập một kết nối. Một khi một kết nối được thiết lập, các thông báo HTTP được truyền trong một định dạng.ác thông báo này bao gồm các Yêu cầu từ Client tới Server và các Phản hồi từ Server tới Client  mà sẽ theo định dạng sau:
```
 HTTP-message   = <Request> | <Response> ; HTTP/1.1 messages
```
* Các yêu cầu và phản hồi HTTP sử dụng 1 định dạng thông báo chung của RFC 822 cho chuyền tải dữ liệu đưuọc yêu cầu. Định bạng thông báo chung này gốm 4 phần:
```
 Một dòng đầu tiên

 Không hoặc nhiều trường Header theo sau bởi CRLF.

 Một dòng trống (ví dụ: một dòng mà không có gì trước CRLF), chỉ phần cuối của trường Header. 

 Một thân thông báo tùy ý

 ```
 * Dòng đầu thông báo(Start-line)
      * Một dòng đầu sẽ có cú pháp chung như sau:
     ```
      start-line = Request-Line | Status-Line
     ```
      * 
      * Trong đó **Request-Line** là yêu cầu của client còn **Status-Line** là phản hồi của server. Ví dụ:
     ```
      GET /hello.jsp HTTP/1.1     (This is Request-Line sent by the client)

      HTTP/1.1 200 OK             (This is Status-Line sent by the server)
     ```
 * Các trường Header
      * Các trường Header cung cấp thông tin được yêu cầu về yêu cầu hoặc phản hồi, hoặc về đối tượng được gửi trong thân thông báo.
      * Có 4 kiểu của Header trong các thông báo HTTP:  
           * Kiểu chung (General-Header): Các trường Header này có khả năng ứng dụng chung cho cả các thông báo yêu cầu và phản hồi.
           * Kiểu yêu cầu (Request-Header): Các trường Header này chỉ có khả năng áp dụng cho các thông báo yêu cầu.
           * Kiểu phản hồi (Response-Header): Các trường Header này chỉ có khả năng áp dụng cho các thông báo phản hồi.
           * Kiểu thực thể (Entity-Header): Các trường này xác định thông tin về thân-thực thể hoặc, nếu không có phần thân nào hiển thị, về nguồn được nhận diện bởi yêu cầu.
      * Tất cả các header ở trên đều được định dạng chung theo một định dạng chung là tên được theo bởi một dấu ":". Ví dụ:
     ```
      message-header = field-name ":" [ field-value ]
     ```
      * Một số Header đa dạng:
     ```
      User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
      Host: www.example.com
      Accept-Language: en, mi
      Date: Mon, 27 Jul 2009 12:28:53 GMT
      Server: Apache
      Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
      ETag: "34aa387-d-1568eb00"
      Accept-Ranges: bytes
      Content-Length: 51
      Vary: Accept-Encoding
      Content-Type: text/plain
     ```
 * Phần thân thông báo
      * Phần thân thông báo là tùy ý cho một thông báo HTTP nhưng nếu nó là có sẵn, thì khi đó nó được sử dụng để mang phần thân được liên kết với yêu cầu hoặc phản hồi. Nếu phần thân thực thể được liên kết, thì sau đó thường các dòng Content-Type và Content-Length xác định bản chất của phần thân được liên kết.
      * Một phần thân thông báo là phần mà mang dữ liệu yêu cầu HTTP thực sự (bao gồm dữ liệu mẫu và được tải lên,…) và dữ liệu phản hồi HTTP từ Server (bao gồm các file, ảnh, …). Dưới đây là nội dung đơn giản của một phần thân thông báo:
     ```
      <html>
           <body>
   
                <h1>Hello, World!</h1>
   
           </body>
      </html>
     ```    

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









