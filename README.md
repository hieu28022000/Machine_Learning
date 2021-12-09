# Machine_Learning
# Test OCR   

# Docker
## Build image
```docker build -t [image's name] .```
## Run container 
```docker run -it --name [container's name] -v `pwd`/:/host [image's name] /bin/bash```

# Cấu trúc dự án  
- soc/core/  
   - text_detection
      - printed_vie_detection
      - printed_jp_detection
   - text_recognition
      - printed_vie_reconition
      - printed_jp_recognition
- text_detection/  
   - .gitkeep
   - evaluate.py  
- text_recognition/  
   - .gitkeep  
   - evaluate.py  
   - model_predict.py  
- .gitignore  
- README.md  

# Model soc  
Mô hình text detection và text recognition được lấy từ thư viện soc.  
Thông tin hiện tại:  
- Tên thư viện: soc
- Version: 0.9.11
- Ngày cập nhật: 19-11-2021
- Link: "/media/rshcm/1TB/data/soc-19112021-0.9.11.zip"
Trước khi thực hiện đánh giá mô hình cần tải mô hình từ thư viện soc và cấu trúc theo cấu trúc của dự án.

# Hướng dẫn đánh giá text detection  
## Chuẩn bị dữ liệu để đánh giá  
Bộ dữ liệu dùng để đánh giá mô hình text detection là các hình ảnh về báo chí, băng rôn, bảng quản cáo,... có chữ.   
Tạo một folder đặt tên là data và có cùng cấp với file test.py.  
Trong folder data tạo thêm hai folder nữa là images và labels. Folder images sẽ chứa ảnh để test và folder labels chứa các file ground truth của ảnh.  
Bộ dữ liệu có cấu trúc như sau: 
- data  
   - images  
      - image1.jpg  
      - image2.jpg  
      - . . .  
   - labels  
      - image1.txt  
      - image2.txt  
      - . . .  
Với mỗi ảnh sẽ có tên tương ứng với file txt có trong thư mục labels, ví dụ: ảnh image1.jpg sẽ có ground truth chứa trong file image1.txt.  
Trong các file txt sẽ có nội dung là các bounding box có trong ảnh, mỗi dòng trong file txt tương ứng với một bounding box.  
Các bounding box có format như sau: ```x1,y1,x2,y2,x3,y3,x4,y4```.  

# Hướng dẫn đánh giá text recognition  
## Chuẩn bị dữ liệu để đánh giá  
Bộ dữ liệu dùng để đánh giá mô hình text recognition là các hình ảnh của các từ, cụm từ, câu. Bộ dữ liệu có cấu trúc như sau:  
- recognize_data/  
  - im0001.jpg  
  - im0001.txt  
  - im0002.jpg  
  - im0002.txt  
  - . . .  

Nội dung của các file label (im0001.txt, im0002.txt,...) chứa nội dung text của các file hình ảnh (im0001.jpg, im0002.jpg,...)  
VD: ```Ngôi sao```  

Bạn có thể tự chuẩn bị dữ liệu theo cấu trúc ở trên. Tuy nhiên, chúng tôi đã chuẩn bị sẵn một số bộ dữ liệu:  
|Dataset|Description|Link|  
|-------|-----------|----|  
|vie_recognize|Bộ dữ liệu đánh giá nhận dạng chữ in Tiếng Việt|"/media/rshcm/1TB/data/printed_vie_data/vie_recognize_data.zip"|  
|jap_recognize|Bộ dữ liệu đánh giá nhận dạng chữ in Tiếng Nhật|def|  
## Đánh giá mô hình  
Ta cập nhật đường dẫn đến bộ dữ liệu trong file ```text_recognition/vie_reg_evaluate.py``` tại ```dataset_path```.  
Sau đó chúng ta thực hiện đánh giá mô hình text recognition:  
```
$cd text_recognition/   
$python3 vie_reg_evaluate.py
```  

Kết quả đánh giá sẽ được lưu thành file result_evaluate_reg.csv bao gồm ```average distance``` và ```accuracy score```.
