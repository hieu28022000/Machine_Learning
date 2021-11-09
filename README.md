# Machine_Learning

## Mô tả chung  
Đây là dự án api nhằm thực hiện phát hiện con vật có trong ảnh và trả về kết quả là vị trí và tên con vật. Dự án được xây dựng dựa trên api-flask, pretrain Yolov4 và sử dụng cơ sở dữ liệu mysql. 

## Cấu trúc của dự án  
Cấu trúc của dự án được phân chia như sau:  
- api-production   
  |-- docs: thông tin về 2 API   
  |-- src   
  |   |-- api_detection: chứa mã nguồn của API-detection và module phát hiện con vật.   
  |   |-- api_query: chứa mã nguồn của API-query.   
  |   |-- mysql_database: chứa cơ sở dữ liệu của dự án.   
  |-- test   
  |   |-- detection_api: chứa unit test của API-detection (1 request/sec, 5 request/sec, 1 request/min, 5request/min)   
  |   |-- query_api: chứa unit test của API-query (1 request/sec, 5 request/sec, 1 request/min, 5request/min)   
  |-- README.md   

## Chức năng và hướng dẫn  
### Chức năng của dự án  
Chức năng của dự án bao gồm nhận ảnh, phát hiện con vật và trả về kết quả. Dự án được chia thành 2 api để thực hiện chức năng:  
- API-detection: api này thực hiện nhiệm vụ nhận ảnh vào thông báo nhận thành công, đồng thời thực hiện phát hiện con vật trong ảnh và lưu kết quả vào cơ sở dữ liệu.
- API-query: api này thực hiện nhiệm vụ truy vấn cơ sở dữ liệu khi nhận vào một id. Nếu ảnh của id đó đã thực hiện phát hiện con vật thành công thì trả về kết quả phát hiện, ngược lại thì thông báo đang xử lý.  

### Hướng dẫn 
#### Chuẩn bị cơ sở dữ liệu  
Đầu tiên bạn clone dự án về, nhập mật tài khoản và mật khẩu khi được yêu cầu:  
'''
$git clone http://devops.runsystem.info/researchproject/api-production.git
$cd api-production/
'''  
Tiếp theo bạn cần chuẩn bị '''src/api_detection/api/authorization/db/1/private_key.pem'''. [Download](https://we.runsystem.info/download/attachments/26545544/private_key.pem?version=1&modificationDate=1624413302138&api=v2&download=true)   
Vì dự án được xây dựng và thực hiện trên nền tảng Docker nên bạn cần có Docker trên thiết bị của mình.   
Sau đó bạn cần di chuyển đến '''src/mysql_database/''' và thực hiện xây dựng container chứa cơ sở dữ liệu.  
'''
$cd src/mysql_database/  
$docker compose up
'''  
Giờ đây bạn có thể thực hiện kết nối tới cơ sở dữ liệu và tạo bảng dữ liệu.  
'''
$docker exec -it container_mysql_id bash  
mysql>USE detect_db;  
mysql>CREATE TABLE result_detect (image_id VARCHAR(5), bboxes VARCHAR(200))  
'''  
Ở đây chúng tôi tạo một bảng dữ liệu result_detect với 2 cột dữ liệu là image_id và bboxes.  

#### Khởi chạy api  
Để khởi chạy api, chúng tôi đã cung cấp cho bạn một Dockerfile ở mỗi api để bạn có thể nhanh chóng xây dựng các container. Ngoài ra bạn cũng cần cài đặt thư viện '''opencv-python version 4.4.0.42'''  
'''
pip install opencv-python==4.4.0.42
'''  
Bây giờ bạn đã đã có thể thử nghiệm api với url sau:
- API-detection: http://host:80/ocr/v1/recognition
- API-querry: http://host:80//detection/query
