Bài tập 1:
- Đầu tiên sẽ cho code đọc ảnh và đọc màu của ảnh ở chế độ là RGB với biến khởi đầu là data.
- Tách kênh màu của ảnh lần lượt là ( R,G,B) và nhập cú pháp data[:, :, (số)] để xác định màu của ảnh.
- Sử dụng " zeros_like() " của numpy để khởi tạo mảng toàn về về tương ứng với việc tạo ra 3 ảnh có 3 màu khác nhau.
- Cuối cùng nhập iio.imwrite('redbird.png', r_image) để ra kết quả là tạo file ảnh, đặt tên và lưu ảnh vào file.
- Kết quả màu nền ảnh 1,2,3 có màu lần lượt là đỏ, xanh lá, xanh dương. 

Bài tập 2:
- Đầu tiên sẽ cho code đọc ảnh và đọc màu của ảnh ở chế độ là RGB với biến khởi đầu là data.
- Tạo các kênh màu ( b,g,r) sau đó tách và hoán đổi các kênh màu với cú pháp [ bgr_image =np.stack([b, g, r], axis=-1), brg_image = np.stack([b, r, g], axis=-1), gbr_image = np.stack([g, b, r], axis=-1) ]
- Lưu ảnh thành file với đoạn code iio.imwrite()
- Kết quả cả mỗi hình ảnh đều có nhiều màu khác nhau.

Bài tập 3:
- Nhập thư viện, cho code đọc ảnh và đọc màu của ảnh ở chế độ là RGB với biến khởi đầu là data.
- Chuyển đổi ảnh RGB sang hệ màu HSV bằng cách sử dụng hàm " colorsys.rgb_to_hsv " và " data[:, :, 0] / 255.0 " để lấy màu tương ứng.
- Điều chỉnh màu hình ảnh bằng biến h,s,v lần lượt là h là độ góc màu, s là độ đậm nhạt của màu, v là giá trị sáng - tối của màu.
- Tạo 3 ảnh HSV riêng biệt có sự điều chỉnh về độ góc màu, độ đậm nhạt, độ sáng màu.
- Lưu ảnh và tạo ảnh sang dạng file hiện ở cùng folder với đoạn code ( iio.imwrite())
- Kết quả là hiển thị bảng chứa 3 ảnh và kiểm tra xem bằng đoạn mã ( plt.figure() , plt.subplot() , plt.show() ) 

Bài tập 4:
- Nhập thư viện, cho code đọc ảnh và đọc màu của ảnh ở chế độ là RGB với biến khởi đầu là tên biến rgb để đọc file ảnh và sử dụng ( rgb_norm = rgb / 255.) để chuẩn hóa.
- Tách 3 (RGV) sang hệ màu HSV bằng mã ( h, s, v = rgb2hsv(rgb_norm[:, :, 0], rgb_norm[:, :, 1], rgb_norm[:, :, 2]) )
- Biến đổi (h1= (1/3) * h , v1 = (3/4) * v) như đề bài và không vượt quá giới hạn [0,1] 
- Chuyển ngược lại từ HSV sang RGB ( hsv2rgb = np.vectorize(colorsys.hsv_to_rgb) / r1, g1, b1 = hsv2rgb(h1, s, v1) ) và gộp về [0,255] => ( rgb1 = np.stack((r1, g1, b1), axis=-1) / rgb1 = (rgb1 * 255).astype(np.uint8)) và sau đó [ iio.imsave() ] để lưu ảnh và hiển thị hình ảnh.
- Kết quả 

Bài tập 5:
Ảnh Balloons_noisy.png
- Nhập các thư viện cần thiết.
- Nhập biến a để đọc file ảnh dưới dạng mode đen trắng.
- Tạo biến K ( Kernel) bao gồm 5x5 chứa giá trị là 1 để tính trung bình các pixel.
- Sử dụng phép tính chập {sn.convolve(a, k).astype(np.uint8) } giữa a và k.
- Sau đó lưu dưới dạng ảnh mới đã được chuyển đổi {iio.imsave()}.
- Hiển thị kết quả ra là ảnh đã được đổi màu.

Ảnh baby.png
- Nhập các thư viện cần thiết.
- Nhập biến a để đọc file ảnh dưới dạng mode đen trắng.
- Tạo biến K ( Kernel) bao gồm 5x5 chứa giá trị là 1 để tính trung bình các pixel.
- Sử dụng phép tính chập {sn.convolve(a, k).astype(np.uint8) } giữa a và k.
- Sau đó lưu dưới dạng ảnh mới đã được chuyển đổi {iio.imsave()}.
- Hiển thị kết quả ra là ảnh đã được đổi màu.
  
Ảnhflower.png
- Nhập các thư viện cần thiết.
- Nhập biến a để đọc file ảnh dưới dạng mode đen trắng.
- Tạo biến K ( Kernel) bao gồm 5x5 chứa giá trị là 1 để tính trung bình các pixel.
- Sử dụng phép tính chập {sn.convolve(a, k).astype(np.uint8) } giữa a và k.
- Sau đó lưu dưới dạng ảnh mới đã được chuyển đổi {iio.imsave()}.
- Hiển thị kết quả ra là ảnh đã được đổi màu.
