# Machine_Learning
# Test OCR   

# Cấu trúc dự án  
- text_detection/  
   - evaluate.py  
- text_recognition/  
   - .gitkeep  
   - evaluate.py  
   - model_predict.py  
- .gitignore  
- README.md  

# Hướng dẫn đánh giá text detection  
## Tải bộ dữ liệu dùng để đánh giá  

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
Ta cập nhật đường dẫn đến bộ dữ liệu trong file evaluate_text_recognition.py tại dataset_path.  
Sau đó chúng ta thực hiện đánh giá mô hình text recognition:  
```$python3 evaluate_text_recognition.py```  

Kết quả đánh giá sẽ được lưu thành file result_evaluate_reg.csv bao gồm average distance và accuracy score.
