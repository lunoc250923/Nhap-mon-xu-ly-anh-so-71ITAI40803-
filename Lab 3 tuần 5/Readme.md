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




