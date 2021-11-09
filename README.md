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
### Bắt đầu  
