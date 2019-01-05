
# Báo cáo ngày 5/1

## Bài toán tiền thật tiền giả:

### Các phần việc đã hoàn thành:
- Đọc dữ liệu bin -> ảnh.
- Fake 1 số tiền giả.
- Tạo dữ liệu features từ dữ liệu ảnh tiền thật, tiền giả dựa trên các thuật toán `MCIR_IR_MINUS_R_UP ,MCIR_IR_MINUS_R_DOWN,MCIR_IR_MINUS_G_UP, MCIR_IR_MINUS_G_DOWN,`
`CIR_3COLOR_IR_UP, 'CIR_3COLOR_IR_DOWN, CIR_4COLOR_IR1_UP', CIR_4COLOR_IR1_DOWN',` `CIR_4COLOR_IR2_UP, CIR_4COLOR_IR2_DOWN`
- Tạo dữ liệu features từ dữ liệu ảnh tiền thật, tiền giả, và tiền giả được tạo ra dựa trên các thuật toán `MCIR_IR_MINUS_R_UP ,MCIR_IR_MINUS_R_DOWN,MCIR_IR_MINUS_G_UP, MCIR_IR_MINUS_G_DOWN,``CIR_3COLOR_IR_UP, CIR_3COLOR_IR_DOWN,`
- Feed dữ liệu vào classifier SVM

### Thuật toán fake tiền giả từ tiền thật:
- Do so sánh tiền thật tiền giả dựa trên kênh IR, nên ý tưởng là điều chỉnh giá trị kênh màu IR. 
- Sau khi giá trị kênh màu IR trên 2 mẫu tiền thật và tiền giả thì thấy giá trị kênh màu IR trên tiền giả có giá trị nhỏ hơn so với tiền thật. Nên ý tưởng là giảm giá trị kênh IR của tiền thật để tạo ra 1 tờ tiền giả tương ứng bằng cách trừ giá trị cho 1 số random trong khoảng [0, 160] và có minmax normalize.

### SVM:
- Số lượng dữ liệu:
	- Tiền thật: 395 mẫu
	- Tiền giả (real-counterfeit money): 155 mẫu
	- Tiền giả được tạo ra từ tiền thật (fake-counterfeit money): 395 mẫu
	- Bộ dự liệu train-test được chia theo 3 cases:
	- Case 1:
		- Data train: 440 mẫu gồm tiền thật và tiền giả
		- Data test: 110 mẫu gồm tiền thật và tiền giả
		- phân phối của mẫu tiền thật/tiền giả: 2.55
	- Case 2:
		- Data train: 635 mẫu gồm 395 mẫu tiền giả được tạo ra và 240 mẫu tiền thật
		- Data test: 310 mẫu gồm tiền thật và tiền giả với tỉ lệ 50/50
	- Case 3:
		- Data train: 790 mẫu gồm 395 mẫu tiền giả được tạo ra, 317 mẫu tiền thật và 78 mẫu tiền giả.
		- Data test: 155 mẫu tiền thật và tiền giả với tỉ lệ 50/50
- file log: file csv có các trường: tên thuật toán, giá trị param cho kết quả tốt nhất, accuracy.

#### Params tunning cho SVM:
- Sử dụng thuật toán GridSearch của sk-learn để vét cạn các trường hợp để tìm trường hợp cho ra gía trị best accuracy.
- Param grid sử dụng khi classify: `{'C':[0.1, 0.01, 1], 'gamma':[1, 0.1, 0.001], 'kernel':['linear', 'rbf']}`

#### Kết quả:
- Case 1:

Column 1 | Column 2 | Column 3
--- | --- | ---
**Things** | _Don't_ | [Need](http://makeuseof.com)
To | *__Look__* | `Pretty`
