
1.	Dataset: Tập data đã được chia sẵn Train - Test Set. Mỗi folder bao gồm các file ảnh và một file CSV chứa tên ảnh, kích cỡ và Label của ảnh đó (bao gồm 2 label “Motor" và “Bycycle")
2.	Preprocess Data:
-	Lấy từ file csv và các link ảnh, chia ra các tập X_train, X_test, y_train, y_test
+	X_train có shape (625, 416, 416, 3) (chế độ màu RGB)
-	Biểu diễn một số dữ liệu mẫu
-	Áp dụng Label Encoder và One-hot Encoding cho y_train và y_test để có thể chuyển sang vector, áp dụng được cho quá trình Training (khi predict sẽ ra một vector 2 phần tử là float, sau đó chúng ta sẽ chọn argmax và đảo ngược LabelEncoder để ra kết quả dự đoán gốc)
3.	Training Process:
-	Tạo model với Neural Networks và CNNs với Keras bao gồm các lớp:
+	Đầu vào input là khối (None, None, 3): kích thước không cố định
+	Lớp đầu tiên là lớp tích chập 2 chiều Conv2D với filter = 16 (16 lần chuyển toàn bộ hình ảnh), kích thước hạt nhân kenel_size = 3x3.
+	Sau đó, sử dụng Maxpool2D để giảm kích thước ảnh xuống một nửa.
+	Tương tự ta lại sử dụng Conv2D với filter = 32 và Maxpool2D để có được 32 tính năng, kích thước tiếp tục giảm một nửa.
+	Tiếp theo sử dụng GlobalAveragePooling2D để tính toán trung bình trên 2 chiều để đưa ra duy nhất 32 tính năng cuối cùng.
+	Cuối cùng là tạo ra mạng lưới thần kinh 2 lớp với 64 tế bào.
+	Đầu ra chỉ xuất ra 1 giá trị với activation= ‘sigmoid’ 
+	Sử dụng hàm loss là BinaryCrossentropy vì đây chỉ cần phân loại 2 object
+	Hàm Optimizers sử dụng Adam và số epoch là 100


