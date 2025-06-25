1.1
- Nhập các thư viện cần thiết cho bài tập.
- data = iio.imread('fruit.jpg'): Tìm và đọc ảnh có trong yêu cầu đoạn code.
- bmg= data[800:1200, 570:980] : Nhập tọa độ trong ảnh Fruit ở vị trí được người dùng chỉ định để cắt ảnh
- print(data.shape) : In ra kết quả kích thước của ảnh gốc
- iio.imsave('orange.jpg', bmg) : Sau khi thực hiện cắt ảnh thì từ ảnh được cắt sẽ được lưu dưới dạng là ảnh mới theo tọa đồ mà người dùng chỉ định.
- plt.imshow(bmg): Xuất ảnh sau khi cắt ra từ ảnh gốc
- plt.show() : Hiển thị ảnh sau khi xuất ảnh đã được cắt từ ảnh gốc.
=> Kết quả: ảnh hiện trái cam múp rụp có trong ảnh. 

1.2
- Nhập các thư viện cần thiết cho bài tập.
- img = Image.open('fruit.jpg').convert('L') : Đọc ảnh và chuyển sang ảnh xám.
- data = np.array(img) : Chuyển ảnh sang cho numpy xử lý ảnh.
- bdata = nd.shift(data, (100, 25)) : Tịnh tiến ảnh xám với giá trị được chỉ định.
- plt.imshow(bdata) : Xuất ảnh sau khi đã được tịnh tiến ảnh 
- plt.show() : hiển thị ảnh tịnh tiến.
=> Kết quả: Hiện ảnh đã đổi màu và có điều chỉnh giá trị.

1.3
- Nhập các thư viện cần thiết cho bài học.
- data = iio.imread('fruit.jpg') : Đọc ảnh theo yêu cầu và xuất ảnh gốc = print(data.shape)
- bdata = nd.zoom(data,2) : Phóng to hình ảnh gốc lên 2 lần và xuất ảnh đã zoom = print(bdata.shape)
- data2 = nd.zoom (data,(2,2,1)) :  Phóng to ảnh lên với chiều cao = 2, chiều rộng = 2, và kênh màu = 1 và cập nhật xuất ảnh = print(data2.shape).
- data3 = nd.zoom(data,(0.5,0.9,1)) : Giảm hình ảnh sau khi phóng to với chiều cao = 0.5, chiều rộng = 0.9, và kênh màu = 1 và cập nhật xuất ảnh = print(data3.shape).
- plt.imshow(data3) : Xuất kết quả ảnh mới nhất sau khi điều chỉnh kích cỡ.
- plt.show() : Hiển thị ảnh.
=> Kết quả: Hiển thị hình ảnh mới từ ảnh gốc đã được cắt ảnh theo tọa độ [(1427, 2100, 3),(2854, 4200, 6), (2854, 4200, 3)]

1.4 
- Nhập các thư viện cần thiết cho bài tập.
- data = iio.imread('fruit.jpg') : Đọc ảnh theo yêu cầu và xuất ảnh gốc = print(data.shape)
- d1 = nd.rotate(data,20) : Xoay ảnh ở góc 20 độ.
- plt.imshow(d1) : Xuất ảnh sau khi đã được nghiêng 
- plt.show() : hiển thị ảnh tịnh nghiêng.
- d2 = nd.rotate(data,20,reshape=False): Xoay ảnh ở góc 20 độ và các vị trí mà ảnh xoay sẽ bị cắt đi.
- plt.imshow(d2) : Xuất ảnh sau khi đã được làm nghiêng 
- plt.show() : hiển thị hiển nghiêng
=> Kết Quả: Hình ảnh bị nghiêng

1.5
- Nhập các thư viện cần thiết cho bài tập.
- data = iio.imread('world_cup.jpg', mode='L') : Đọc ảnh theo yêu cầu với ảnh màu xám và xuất bằng = print(data.shape)
- d1 = nd.binary_dilation(data) : Thực hiện nhị phân giãn nở ảnh.
- plt.imshow(d1) : Xuất kết quả ảnh mới nhất sau khi thực hiện giãn nở ảnh.
- plt.show() : Hiển thị ảnh.
- d2 = nd.binary_dilation(data,interations=3) : Thực hiện nhị phân giãn nở ảnh mạnh hơn 3 lần.
- plt.imshow(d2) : Xuất kết quả ảnh mới nhất sau khi thực hiện giãn nở ảnh.
- plt.show() : Hiển thị ảnh.
=> Kết quả: ![ảnh](https://github.com/user-attachments/assets/0d4f7169-01ae-4309-8658-6dfb35e7e6a9)

1.6
- Nhập các thư viện cần thiết cho bài tập.
- data = iio.imread('world_cup.jpg', mode='L') : Đọc ảnh theo yêu cầu với ảnh màu xám và xuất bằng = print(data.shape)
- V,H = data.shape : Đặt biến V,H lần lượt là chiều cao và chiều rộng cho ảnh
- M = np.indices ((V, H)) : Tạo bản đồ chỉ số pixel có kích thước ( V,H)
- d = 5 / q = 2 * d * np.random.ranf(M.shape) - d : Đặt d = 5 và tạo q làm thay đổi vị trí với ma trận np.random.ranf(M.shape)
- mp = (M + q).astype(int) : M + q với tạo tọa độ mới và ép về số nguyên.
- d1 = nd.map_coordinates(data,mp) : Sử dụng hàm này để lấy giá trị pixel tại vị trí mới.
- plt.imshow(d1) : Xuất kết quả ảnh mới
- plt.show() : Hiển thị ảnh.
=> Kết quả: ![ảnh](https://github.com/user-attachments/assets/01523bf8-4b99-41e6-a3f5-bc5f99bb89f7)

1.7
- Nhập các thư viện cần thiết cho bài tập.
- Sử dụng hàm GeoFun(outcoord) để xác định tọa độ đầu ra và tìm giá trị ảnh đầu ra trong ảnh gốc và trả về ảnh mới ở a,b.
- data = iio.imread('world_cup.jpg', mode='L') : Đọc ảnh theo yêu cầu với ảnh màu xám.  
- d1 = nd.geometric_transform(data, GeoFun) : Biến đổi hình học cho ảnh 
- plt.imshow(d1) : Xuất kết quả ảnh mới
- plt.show() : Hiển thị ảnh.
=> Kết quả: ![ảnh](https://github.com/user-attachments/assets/61f011b3-c2e9-446e-af97-a98fc54cd93a)

*Làm thêm
1.
- Nhập các thư viện cần thiết cho bài tập.
- data = iio.imread('fruit.jpg'): Tìm và đọc ảnh có trong yêu cầu đoạn code.
- bmg= data[810:1300, 1480:1850] : Nhập tọa độ trong ảnh Fruit ở vị trí được người dùng chỉ định để cắt ảnh
- print(data.shape) : In ra kết quả kích thước của ảnh gốc
- iio.imsave('apple.jpg', bmg) : Sau khi thực hiện cắt ảnh thì từ ảnh được cắt sẽ được lưu dưới dạng là ảnh mới theo tọa đồ mà người dùng chỉ định.
- plt.imshow(bmg): Xuất ảnh sau khi cắt ra từ ảnh gốc
- plt.show() : Hiển thị ảnh sau khi xuất ảnh đã được cắt từ ảnh gốc.
=> Kết quả: ảnh hiện trái táo size D có trong ảnh. ![ảnh](https://github.com/user-attachments/assets/0ffcfd66-3f1b-4e37-af6b-7e9021e03247)

2
- Nhập các thư viện cần thiết cho bài tập.
- img = Image.open('fruit.jpg').convert('L') : Đọc ảnh và chuyển sang ảnh xám.
- data = np.array(img) : Chuyển ảnh sang cho numpy xử lý ảnh.
- bdata = nd.shift(data, (50, -30)) : Tịnh tiến ảnh xám với giá trị được chỉ định.
- plt.imshow(bdata) : Xuất ảnh sau khi đã được tịnh tiến ảnh 
- plt.show() : hiển thị ảnh tịnh tiến.
=> Kết quả: Hiện ảnh đã đổi màu và có điều chỉnh giá trị khung ảnh có 1 vùng đệm ở trên và bên phải ảnh. ![ảnh](https://github.com/user-attachments/assets/7c26e009-f165-4156-aac6-5843011815f0)

3
- Nhập các thư viện cần thiết cho bài học.
- data = iio.imread('fruit.jpg') : Đọc ảnh theo yêu cầu và xuất ảnh gốc = print(data.shape)
- bdata = nd.zoom(data,3) : Phóng to hình ảnh gốc lên 2 lần và xuất ảnh đã zoom = print(bdata.shape)
- data2 = nd.zoom (data,(3,3,1)) :  Phóng to ảnh lên với chiều cao = 2, chiều rộng = 2, và kênh màu = 1 và cập nhật xuất ảnh = print(data2.shape).
- data3 = nd.zoom(data,(0.3,0.3,1)) : Giảm hình ảnh sau khi phóng to với chiều cao = 0.5, chiều rộng = 0.9, và kênh màu = 1 và cập nhật xuất ảnh = print(data3.shape).
- plt.imshow(data3) : Xuất kết quả ảnh mới nhất sau khi điều chỉnh kích cỡ.
- plt.show() : Hiển thị ảnh.
=> Kết quả: Hiển thị hình ảnh mới với ảnh phóng to lớn gấp 3 lần.

4
- Nhập các thư viện cần thiết cho bài tập.
- data = iio.imread('fruit.jpg') : Đọc ảnh theo yêu cầu và xuất ảnh gốc = print(data.shape)
- d1 = nd.rotate(data,20) : Xoay ảnh ở góc 20 độ.
- plt.imshow(d1) : Xuất ảnh sau khi đã được nghiêng 
- plt.show() : hiển thị ảnh tịnh nghiêng.
- d2 = nd.rotate(data,40,reshape=False): Xoay ảnh ở góc 40 độ và các vị trí mà ảnh xoay sẽ bị cắt đi.
- plt.imshow(d2) : Xuất ảnh sau khi đã được làm nghiêng 
- plt.show() : hiển thị hiển nghiêng 
- d3 = nd.rotate(data,40,reshape=True): Xoay ảnh ở góc 40 độ và các vị trí mà ảnh xoay sẽ bị cắt đi.
- plt.imshow(d3) : Xuất ảnh sau khi đã được làm nghiêng 
- plt.show() : hiển thị hiển nghiêng
=> Kết Quả: Hình ảnh d2 nghiêng 40 độ theo chiều nằm ngang và hình ảnh d3 bị nghiêng theo chiều thẳng đứng

5
- Nhập các thư viện cần thiết cho bài tập.
- data = iio.imread('world_cup.jpg', mode='L') : Đọc ảnh theo yêu cầu với ảnh màu xám và xuất bằng = print(data.shape)
- d1 = nd.binary_dilation(data) : Thực hiện nhị phân giãn nở ảnh.
- plt.imshow(d1) : Xuất kết quả ảnh mới nhất sau khi thực hiện giãn nở ảnh.
- plt.show() : Hiển thị ảnh.
- d2 = nd.binary_dilation(data, size=(5, 5)) : Thực hiện nhị phân giãn nở ảnh bằng Kernel.
- plt.imshow(d2) : Xuất kết quả ảnh mới nhất sau khi thực hiện giãn nở ảnh.
- plt.show() : Hiển thị ảnh.
=> kết Quả: ảnh xuất ra khó nhận xét :<

6
- Nhập các thư viện cần thiết cho bài tập.
- Sử dụng hàm GeoFun(outcoord) để xác định tọa độ đầu ra và tìm giá trị ảnh đầu ra trong ảnh gốc và trả về ảnh mới ở a,b.
- data = iio.imread('world_cup.jpg', mode='L') : Đọc ảnh theo yêu cầu với ảnh màu xám.  
- d1 = nd.geometric_transform(data, GeoFun) : Biến đổi hình học cho ảnh 
- plt.imshow(d1) : Xuất kết quả ảnh mới
- plt.show() : Hiển thị ảnh.
=> Kết Quả: Ảnh xuất ra hình trông như bị nhiễu


