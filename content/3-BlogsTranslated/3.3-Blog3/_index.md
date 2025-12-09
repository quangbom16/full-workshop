---
title: "AWS Lambda chuẩn hóa việc tính phí cho giai đoạn INIT"
date: "2025-10-10"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

*Bởi Shubham Gupta và Jeff Gebhart*

- Bài viết gốc: <a href="https://aws.amazon.com/vi/blogs/compute/aws-lambda-standardizes-billing-for-init-phase/"
   target="_blank" 
   rel="noopener noreferrer">
   AWS Lambda standardizes billing for INIT Phase - AWS Compute Blog
</a>

- doc: <a href="https://docs.google.com/document/d/1C4o30LDk20ZZrDsVgy-GWLDbFVYOdajqTDpOZmo0XW8/edit?usp=sharing"
   target="_blank" 
   rel="noopener noreferrer">
   GG docs
</a>

Có hiệu lực từ ngày **1 tháng 8 năm 2025**, AWS sẽ chuẩn hóa việc tính phí cho giai đoạn khởi tạo (INIT) trên tất cả các cấu hình hàm AWS Lambda. Thay đổi này đặc biệt ảnh hưởng đến các lệnh gọi theo yêu cầu của các hàm Lambda được đóng gói dưới dạng tệp ZIP sử dụng các runtime được quản lý, mà trước đây thời lượng giai đoạn INIT không được tính phí.

Bản cập nhật này chuẩn hóa việc tính phí giai đoạn INIT trên tất cả các loại runtime, gói triển khai và chế độ gọi. Hầu hết người dùng sẽ thấy tác động tối thiểu đến tổng hóa đơn Lambda của họ từ thay đổi này, vì giai đoạn INIT thường chỉ xảy ra trong một phần rất nhỏ các lệnh gọi hàm.

Trong bài đăng này, chúng tôi thảo luận về Vòng đời hàm Lambda và những thay đổi sắp tới đối với việc tính phí giai đoạn INIT. Bạn sẽ tìm hiểu điều gì xảy ra trong giai đoạn INIT và khi nào nó xảy ra, cách giám sát thời lượng giai đoạn INIT của bạn và các chiến lược để tối ưu hóa giai đoạn này và giảm thiểu chi phí.

### Tìm hiểu vòng đời thực thi hàm Lambda

Vòng đời thực thi hàm Lambda bao gồm ba giai đoạn riêng biệt: **INIT**, **INVOKE** và **SHUTDOWN**.
*   Giai đoạn **INIT** được kích hoạt trong quá trình "khởi động lạnh" khi Lambda tạo một môi trường thực thi mới cho một hàm để phản hồi một lệnh gọi.
*   Tiếp theo là giai đoạn **INVOKE** nơi yêu cầu được xử lý.
*   Cuối cùng là giai đoạn **SHUTDOWN** nơi môi trường thực thi bị chấm dứt.

Trong giai đoạn INIT, Lambda thực hiện một loạt các bước chuẩn bị trong thời gian tối đa 10 giây. Dịch vụ truy xuất mã hàm từ một S3 bucket nội bộ của Amazon, hoặc từ Amazon Elastic Container Registry (Amazon ECR) đối với các hàm sử dụng đóng gói container. Sau đó, nó cấu hình một môi trường với bộ nhớ, runtime và các cài đặt khác được chỉ định.

Khi môi trường thực thi được chuẩn bị, Lambda thực hiện bốn tác vụ chính theo trình tự:
1.  Khởi tạo bất kỳ tiện ích mở rộng nào được cấu hình (Extension INIT)
2.  Khởi động runtime (Runtime INIT)
3.  Thực thi mã tĩnh của hàm (Function INIT)
4.  Chạy bất kỳ hook runtime trước checkpoint nào (chỉ áp dụng cho Lambda SnapStart)

![Vòng đời thực thi hàm Lambda](/images/T1.png)
*Hình 1: Vòng đời thực thi hàm Lambda*

### Tìm hiểu những thay đổi về tính phí

Phí Lambda được tính dựa trên số lượng yêu cầu và thời lượng cần thiết để mã chạy. Thời lượng được tính từ thời điểm mã hàm bắt đầu chạy cho đến khi hoàn thành hoặc chấm dứt, được làm tròn lên đến mili giây gần nhất. Chi phí thời lượng phụ thuộc vào lượng bộ nhớ bạn cấp phát cho hàm của mình.

Trước đây, thời lượng giai đoạn INIT không được bao gồm trong Billed Duration đối với các hàm sử dụng runtime được quản lý với đóng gói lưu trữ ZIP, như được chứng minh trong nhật ký Amazon CloudWatch:

```
REPORT RequestId: xxxxx   Duration: 250.06 ms  Billed Duration: 251 ms  Memory Size: 1024 MB
Max Memory Used: 350 MB   Init Duration: 100.77 ms
```

Tuy nhiên, các hàm được cấu hình với runtime tùy chỉnh, Provisioned Concurrency (PC) hoặc đóng gói OCI đã bao gồm thời lượng giai đoạn INIT trong Billed Duration của chúng.

Có hiệu lực từ ngày **1 tháng 8 năm 2025**, giai đoạn INIT sẽ được tính phí trên tất cả các loại cấu hình và thời lượng giai đoạn INIT cũng sẽ được bao gồm trong Billed Duration đối với các lệnh gọi theo yêu cầu của các hàm sử dụng runtime được quản lý với đóng gói lưu trữ ZIP. Sau thay đổi này, dòng nhật ký `REPORT Request ID` sẽ hiển thị như sau:

```
REPORT RequestId: xxxxx   Duration: 250.06 ms  Billed Duration: 351 ms  Memory Size: 1024 MB
Max Memory Used: 350 MB   Init Duration: 100.77 ms
```

Các khoản phí thời lượng giai đoạn INIT tiếp theo sẽ tuân theo giá thời lượng theo yêu cầu tiêu chuẩn dành riêng cho từng Vùng AWS, có thể tìm thấy trên trang giá Lambda. Đối với các hàm AWS Lambda@Edge, thời lượng giai đoạn INIT sẽ được tính phí theo tỷ lệ thời lượng Lambda@Edge.

### Tìm thời lượng giai đoạn INIT và tác động đến việc tính phí Lambda

Bạn đã có thể giám sát thời gian dành cho giai đoạn INIT của các lệnh gọi hàm của mình thông qua dòng nhật ký "REPORT RequestId" trong CloudWatch Logs, bao gồm giá trị "Init Duration". Ngoài ra, nếu Lambda Insights được bật, bạn có thể sử dụng chỉ số CloudWatch "init_duration".

Để phân tích toàn diện hơn, bạn có thể sử dụng truy vấn **CloudWatch Log Insights** sau để tạo báo cáo chi tiết ước tính thời lượng giai đoạn INIT trước đây không được tính phí:

```sql
filter @type = "REPORT"
| stats
    sum((@memorySize/1000000/1024) * (@billedDuration/1000)) as BilledGBs,
    sum((@memorySize/1000000/1024) * ((@duration + @initDuration - @billedDuration)/1000)) as UnbilledInitGBs,
    UnbilledInitGBs / (UnbilledInitGBs + BilledGBs) as UnbilledInitRatio
```

Truy vấn CloudWatch Log Insights cung cấp ba chỉ số thiết yếu:
1.  **BilledGBs:** Đại diện cho tổng GB-s (gigabyte-giây) hiện đang được tính phí cho các nhóm nhật ký đã chọn.
2.  **UnbilledInitGBs:** Hiển thị tổng GB-s tiêu thụ trong giai đoạn INIT mà trước đây không được bao gồm trong tính phí.
3.  **Ratio:** Cho biết tỷ lệ phần trăm tổng GB-s được gán cho thời lượng giai đoạn INIT trước đây không được tính phí.

![Báo cáo CloudWatch Log Insights](/images/T2.png)
*Hình 2: Báo cáo CloudWatch Log Insights*

Sử dụng các khả năng giám sát hiện có này cho phép bạn chủ động đánh giá và tối ưu hóa thời gian INIT của hàm Lambda, có khả năng giảm thiểu tác động của cấu trúc thanh toán mới đến tổng chi phí của bạn.

### Tìm hiểu và tối ưu hóa giai đoạn INIT của Lambda

Giai đoạn INIT của Lambda được kích hoạt trong hai trường hợp cụ thể: trong quá trình tạo môi trường thực thi mới và khi một hàm mở rộng quy mô để đáp ứng nhu cầu. Mã INIT này chỉ chạy trong các "khởi động lạnh" này và bị bỏ qua trong các lệnh gọi tiếp theo sử dụng các môi trường ấm hiện có.

Các nhà phát triển có thể sử dụng giai đoạn INIT để tạo, khởi tạo và cấu hình các đối tượng dự kiến được sử dụng lại trên nhiều lệnh gọi trong quá trình INIT hàm thay vì thực hiện nó trong trình xử lý. Khởi tạo các phụ thuộc/đối tượng được chia sẻ trước sẽ giảm độ trễ của các lệnh gọi tiếp theo. Ví dụ:
*   Tải xuống thêm thư viện hoặc phụ thuộc.
*   Thiết lập kết nối máy khách với các dịch vụ AWS khác như Amazon S3 hoặc Amazon DynamoDB.
*   Tạo kết nối cơ sở dữ liệu để chia sẻ trên các lệnh gọi.
*   Truy xuất các tham số ứng dụng hoặc bí mật từ Amazon Systems Manager Parameter Store hoặc AWS Secrets Manager.

Khi phát triển các hàm Lambda, điều quan trọng là phải quyết định một cách chiến lược mã nào chạy trong giai đoạn INIT so với giai đoạn xử lý, vì nó ảnh hưởng đến cả hiệu suất và chi phí.

#### Tối ưu hóa kích thước gói/thư viện

Ba yếu tố chính ảnh hưởng đến hiệu suất của giai đoạn INIT:
1.  Kích thước của gói hàm, về các thư viện và phụ thuộc được nhập, và các lớp Lambda.
2.  Lượng mã và công việc INIT.
3.  Hiệu suất của các thư viện và các dịch vụ khác trong việc thiết lập kết nối và các tài nguyên khác.

Các gói hàm lớn hơn làm tăng thời gian tải xuống mã. Bạn có thể giảm thời lượng giai đoạn INIT bằng cách giảm kích thước gói, dẫn đến khởi động lạnh nhanh hơn và chi phí INIT thấp hơn. Các công cụ như **esbuild** có thể tối ưu hóa hiệu suất hơn nữa bằng cách thu nhỏ và đóng gói các gói.

#### Tối ưu hóa việc thực thi giai đoạn INIT và hiệu quả chi phí

Tần suất thực thi giai đoạn INIT (hoặc khởi động lạnh) tác động trực tiếp đến cả hiệu suất và hiệu quả chi phí. Theo phân tích các khối lượng công việc Lambda trong sản xuất, INIT (khởi động lạnh) thường xảy ra dưới 1% các lệnh gọi.

Bạn có thể sử dụng giai đoạn INIT để thực hiện các thao tác một lần có lợi cho các lệnh gọi tiếp theo, ví dụ như tải dữ liệu tĩnh từ Amazon S3 hoặc DynamoDB trong quá trình INIT.

#### Lambda SnapStart

Lambda SnapStart cung cấp một giải pháp hiệu quả để giảm độ trễ khởi động lạnh và chi phí giai đoạn INIT. Khi được bật, SnapStart tạo một ảnh chụp nhanh trong quá trình INIT hàm đầu tiên và sử dụng lại nó cho các khởi động lạnh tiếp theo, loại bỏ nhu cầu thực thi giai đoạn INIT lặp lại. SnapStart được hỗ trợ cho các runtime Java, .NET và Python.

#### Provisioned Concurrency

Provisioned Concurrency là một tính năng của Lambda giúp khởi tạo trước môi trường thực thi trước khi bất kỳ lệnh gọi nào xảy ra. Phương pháp chủ động này loại bỏ hiệu quả tác động hiệu suất của giai đoạn INIT đối với các lệnh gọi hàm riêng lẻ. Từ góc độ tối ưu hóa chi phí, Provisioned Concurrency phù hợp nhất cho các khối lượng công việc có mẫu sử dụng bền vững trên 60%.

### Kết luận

Có hiệu lực từ ngày **1 tháng 8 năm 2025**, AWS đang chuẩn hóa việc tính phí giai đoạn INIT cho AWS Lambda. AWS cung cấp nhiều cách để bạn tối ưu hóa cả hiệu suất và chi phí của các hàm Lambda của mình. Cho dù bạn đang sử dụng SnapStart, triển khai Provisioned Concurrency hay tối ưu hóa mã INIT, chúng tôi khuyên bạn nên làm việc chặt chẽ với các nhóm hỗ trợ của AWS để xác định phương pháp tối ưu hóa phù hợp nhất cho các yêu cầu khối lượng công việc cụ thể của bạn.