#2.1.1
- Nhập các thư viện cần thiết cho xử lý ảnh và hiển thị ảnh.
- data = Image.open('fruit.jpg').convert('L') : Mở ảnh 'fruit.jpg' và chuyển sang ảnh xám (grayscale) với giá trị pixel từ 0 đến 255.
- a = np.asarray(data) : Chuyển ảnh xám thành mảng 2D để tiện xử lý bằng các thư viện số học như NumPy.
- thres = threshold_otsu(a) : Tính ngưỡng phân tách nhị phân tự động bằng thuật toán Otsu.
- b = a > thres : Tạo ảnh nhị phân bằng cách so sánh mỗi pixel với ngưỡng vừa tìm được — pixel nào lớn hơn sẽ là True (trắng), còn lại là False (đen).
- b = Image.fromarray(b) : Chuyển ảnh nhị phân từ mảng NumPy sang ảnh kiểu PIL.
- plt.imshow(b) : Hiển thị ảnh nhị phân bằng thư viện matplotlib.
- plt.show() : Thực hiện việc hiển thị cửa sổ chứa ảnh đã được xử lý.

#2.1.2
- Nhập các thư viện cần thiết để xử lý ảnh và hiển thị ảnh.
- data = Image.open('fruit.jpg').convert('L'): Mở ảnh 'fruit.jpg' và chuyển sang ảnh xám với mức xám từ 0 đến 255.
- a = np.asarray(data): Chuyển ảnh thành mảng NumPy 2D để dễ dàng xử lý bằng toán học.
- b = threshold_local(a, 39, offset=10): Áp dụng ngưỡng cục bộ (local thresholding) với cửa sổ kích thước 39x39 và độ lệch ngưỡng là 10 để xử lý ảnh. Mỗi vùng nhỏ trong ảnh sẽ có ngưỡng khác nhau, giúp xử lý tốt hơn khi ánh sáng không đều.
- b = Image.fromarray(b): Chuyển mảng kết quả từ NumPy trở lại ảnh dạng PIL.
- plt.imshow(b): Hiển thị ảnh kết quả bằng thư viện matplotlib.
- plt.show(): Hiển thị cửa sổ chứa ảnh đã xử lý.

#2.2
Nhập các thư viện cần thiết để xử lý ảnh, phân đoạn và hiển thị kết quả.
data = cv2.imread('fruit.jpg'): Mở ảnh màu 'fruit.jpg' bằng OpenCV.
a = cv2.cvtColor(data, cv2.COLOR_BGR2GRAY): Chuyển ảnh từ màu sang ảnh xám để dễ xử lý.
thresh, bl = cv2.threshold(...): Áp dụng phương pháp Otsu để nhị phân hóa ảnh — tách foreground (vật thể) khỏi background. Sử dụng cv2.THRESH_BINARY_INV để đảo màu (vật thể màu trắng).
b2 = cv2.erode(bl, None, iterations = 2): Thực hiện phép co (erosion) để loại bỏ các chi tiết nhỏ và tách các vùng gần nhau.
dist = cv2.distanceTransform(b2, 2, 3): Tính toán khoảng cách từ mỗi pixel vật thể đến pixel nền gần nhất. Dùng để xác định vùng "lõi" của vật thể.
thresh, dt = cv2.threshold(dist, 1, 255, cv2.THRESH_BINARY): Áp ngưỡng lên ảnh khoảng cách để xác định vùng foreground chắc chắn.
labelled, ncc = label(dt): Gán nhãn cho các vùng foreground riêng biệt để phân biệt chúng.
labelled = labelled.astype(np.int32): Chuyển định dạng dữ liệu sang số nguyên 32-bit để phục vụ thuật toán Watershed.
cv2.watershed(data, labelled): Áp dụng thuật toán tách vùng Watershed để phân vùng các vật thể chạm nhau.
b = Image.fromarray(labelled): Chuyển ảnh sau phân đoạn thành định dạng ảnh để hiển thị.
plt.imshow(b): Hiển thị ảnh đã gán nhãn phân vùng bằng thư viện matplotlib.
plt.show(): Mở cửa sổ hiển thị ảnh.

#2.3.1
Nhập các thư viện cần thiết cho xử lý ảnh nhị phân và hiển thị ảnh.
data = Image.open('dil_img.gif').convert('L'): Mở ảnh 'dil_img.gif' và chuyển ảnh sang dạng ảnh xám (grayscale).
b = nd.binary_dilation(data, iterations=50): Thực hiện phép dãn ảnh nhị phân (binary dilation) lặp lại 50 lần nhằm mở rộng các vùng trắng trong ảnh — thường dùng để nối các điểm gần nhau hoặc làm đầy vùng rỗng nhỏ.
c = Image.fromarray(b): Chuyển mảng kết quả sau khi dãn về dạng ảnh PIL.
c.show(): Hiển thị ảnh sau khi thực hiện phép dãn bằng công cụ mặc định của hệ điều hành.
plt.imshow(c): Hiển thị ảnh với thư viện matplotlib.
plt.show(): Mở cửa sổ matplotlib để xem ảnh đã xử lý.

#2.3.2
Nhập các thư viện cần thiết để xử lý ảnh nhị phân và hiển thị kết quả.
data = Image.open('dil_img.gif').convert('L'): Mở ảnh 'dil_img.gif' và chuyển sang ảnh xám (grayscale) với giá trị pixel từ 0 đến 255.
s = [[0, 1, 0], [1, 1, 1], [0, 1, 0]]: Xác định phần tử cấu trúc (structuring element) hình chữ thập 3x3 dùng trong phép toán hình thái học.
b = nd.binary_opening(data, structure=s, iterations=25): Thực hiện phép mở nhị phân lặp lại 25 lần trên ảnh đầu vào với phần tử cấu trúc s. Phép mở giúp loại bỏ nhiễu nhỏ và làm trơn viền đối tượng. Tuy nhiên, ảnh đầu vào cần là nhị phân (dtype=bool), nên đoạn này có thể sai kiểu dữ liệu.
c = Image.fromarray(b): Chuyển ảnh kết quả từ NumPy sang ảnh PIL để hiển thị.
c.show(): Hiển thị ảnh kết quả bằng trình xem ảnh mặc định của hệ điều hành.
plt.imshow(c): Hiển thị ảnh bằng matplotlib.
plt.show(): Hiển thị cửa sổ matplotlib chứa ảnh đã xử lý.

#2.3.3
Nhập các thư viện cần thiết để xử lý ảnh nhị phân và hiển thị kết quả.
data = Image.open('dil_img.gif').convert('L'): Mở ảnh 'dil_img.gif' và chuyển sang ảnh xám với giá trị pixel từ 0–255.
s = [[0, 1, 0], [1, 1, 1], [0, 1, 0]]: Xác định phần tử cấu trúc dạng chữ thập 3x3 dùng cho phép toán hình thái.
b = nd.binary_erosion(data, structure=s, iterations=50): Thực hiện phép co (erosion) lặp lại 50 lần, làm thu hẹp vùng sáng (foreground), loại bỏ nhiễu nhỏ hoặc chi tiết dư thừa.
c = Image.fromarray(b): Chuyển ảnh kết quả từ dạng NumPy sang ảnh PIL để hiển thị.
c.show(): Hiển thị ảnh sau khi thực hiện erosion bằng trình xem ảnh mặc định.
plt.imshow(c), plt.show(): Hiển thị ảnh sau xử lý bằng matplotlib.

#2.3.4
Nhập các thư viện cần thiết để xử lý ảnh nhị phân và hiển thị kết quả.
data = Image.open('dil_img.gif').convert('L'): Mở ảnh 'dil_img.gif' và chuyển sang ảnh xám (grayscale).
s = [[0, 1, 0], [1, 1, 1], [0, 1, 0]]: Xác định phần tử cấu trúc hình chữ thập để áp dụng phép toán hình thái.
b = nd.binary_closing(data, structure=s, iterations=50): Thực hiện phép đóng (closing) lặp lại 50 lần, nhằm làm đầy các lỗ nhỏ và nối các vùng sáng gần nhau, giúp loại bỏ vùng đen nhỏ trong foreground.
c = Image.fromarray(b): Chuyển ảnh kết quả từ mảng NumPy về ảnh PIL để hiển thị.
c.show(): Hiển thị ảnh đã xử lý bằng trình xem ảnh mặc định.
plt.imshow(c), plt.show(): Hiển thị ảnh bằng matplotlib.

##Bài tập
#1
Nhập các thư viện cần thiết để xử lý ảnh nhị phân và hiển thị kết quả.
Image.open(...).convert('L'): Mở ảnh dalat.jpg và chuyển sang ảnh xám.
np.array(...)[0:350, 0:500]: Cắt vùng phía trên bên trái của ảnh, được giả định là vùng LangBiang cần xử lý.
shifted[:, 100:] = bmg[:, :-100]: Dịch vùng ảnh đã chọn sang phải 100 pixel.
threshold_otsu(...): Tính ngưỡng Otsu để phân biệt nền và đối tượng.
b = shifted > (ngưỡng * 0.3): Phân ngưỡng ảnh, dùng ngưỡng nhỏ hơn để tăng độ nhạy phát hiện.
Image.fromarray(...): Chuyển ảnh nhị phân về dạng ảnh PIL để lưu và hiển thị.
plt.imshow(...), plt.show(): Hiển thị ảnh kết quả sau khi phân vùng vùng LangBiang.

#2
Nhập các thư viện cần thiết để xử lý ảnh nhị phân và hiển thị kết quả.
Image.open('exercise/dalat.jpg').convert('L'): Mở ảnh dalat.jpg từ thư mục exercise và chuyển sang ảnh xám.
data[0:2000, 0:2000]: Cắt vùng ảnh 2000x2000 pixel từ góc trên bên trái – giả định đây là khu vực chứa hồ Xuân Hương.
nd.rotate(..., 45, reshape=True): Xoay ảnh 45 độ, giữ lại toàn bộ vùng xoay bằng cách mở rộng kích thước ảnh.
threshold_local(..., block_size=39, offset=60): Tính ngưỡng cục bộ cho mỗi vùng nhỏ trong ảnh với cửa sổ 39x39 và độ lệch ngưỡng là 60, giúp xử lý tốt ảnh có ánh sáng không đồng đều.
rotated > thresh: Tạo ảnh nhị phân bằng cách so sánh giá trị pixel với ngưỡng tương ứng từng vùng.
Image.fromarray(...): Chuyển kết quả thành ảnh PIL để lưu và hiển thị.
c.save(...): Lưu ảnh kết quả sau xử lý với tên ho_xuan_huong.jpg.
plt.imshow(c), plt.show(): Hiển thị ảnh nhị phân đã xoay và phân ngưỡng bằng thư viện matplotlib.

#3
Nhập các thư viện cần thiết để xử lý ảnh nhị phân và hiển thị kết quả.
Image.open('exercise/dalat.jpg').convert('L'): Mở ảnh dalat.jpg và chuyển sang ảnh xám.
data[0:350, 1000:1500]: Cắt vùng chứa quảng trường Lâm Viên từ ảnh gốc (giả định theo tọa độ dòng và cột).
nd.zoom(bmg, zoom=(0.8, 0.8)): Thực hiện co ảnh lại 80% theo cả chiều cao và chiều rộng (scale down).
mapped[:sx, 50:50 + sy] = scaled: Dán ảnh sau khi co vào ảnh mới, dịch sang phải 50 pixel.
binary = mapped > 128: Tạo ảnh nhị phân bằng cách áp ngưỡng cố định 128 (pixel sáng hơn sẽ thành trắng).
s = [[0,1,0], [1,1,1], [0,1,0]]: Định nghĩa phần tử cấu trúc hình chữ thập để áp dụng phép toán hình thái.
nd.binary_closing(..., iterations=20): Áp dụng phép đóng (closing) lặp lại 20 lần, giúp lấp lỗ nhỏ và nối các vùng trắng gần nhau.
Image.fromarray(...): Chuyển ảnh nhị phân từ NumPy về ảnh PIL để hiển thị và lưu.
c.save(...): Lưu ảnh kết quả với tên quan_truong_lam_vien.jpg.
plt.imshow(...), plt.show(): Hiển thị ảnh kết quả sau khi xử lý bằng matplotlib.

#4
Nhập các thư viện cần thiết để xử lý ảnh, xử lý hình thái và hiển thị kết quả.
Định nghĩa 3 hàm riêng biệt, mỗi hàm tương ứng với một chức năng đã làm ở các câu trước:
xu_ly_langbiang(): Cắt vùng ảnh LangBiang, dịch sang phải 100 pixel, phân ngưỡng Otsu (0.3), lưu và hiển thị ảnh nhị phân.
xu_ly_ho_xuan_huong(): Cắt ảnh lớn, xoay ảnh 45 độ, áp dụng ngưỡng cục bộ (adaptive thresholding), lưu và hiển thị ảnh nhị phân.
xu_ly_quangtruong(): Cắt ảnh vùng Quảng trường Lâm Viên, co ảnh (zoom 80%), chèn vào khung mới, phân ngưỡng và áp dụng phép đóng (closing), lưu và hiển thị ảnh.
Dùng vòng lặp while để tạo menu lặp lại cho người dùng chọn:
Nếu chọn 1: gọi hàm xử lý ảnh LangBiang.
Nếu chọn 2: gọi hàm xử lý ảnh Hồ Xuân Hương.
Nếu chọn 3: gọi hàm xử lý ảnh Quảng trường Lâm Viên.
Nếu chọn 0: kết thúc chương trình.
Nếu nhập sai: thông báo lỗi và cho chọn lại.
