1.1
- Nhập các thư viện cần thiết cho bài tập.
- img = Image.open('bird.png').convert('L') : Sử dụng hàm này với mục đích mở tệp ảnh để thực hiện việc chuyển màu sang chế độ xám với các giá trị pixel [0 , 255].
- im_1 = np.asarray(img) : thực hiện việc chuyển ảnh để xử lý số thành mảng 2D với mỗi phần tử có giá trị cường độ pixel [0,255].
- im_2 = 255 - im_1 : Biến đổi các vùng sáng thành vùng tối .
- new_img = Image.fromarray(im_2) : Tạo ảnh PIL mới sau khi biến đổi
- img.show() : Hiển thị ảnh gốc
- plt.imshow(new_img) : Hiển thị ảnh nghịch đảo.
- plt.show() : Hiển thị ảnh plt chứa ảnh nghịch đảo

1.2
- Nhập các thư viện cần thiết cho bài tập.
- img = Image.open('bird.png').convert('L') : Sử dụng hàm này với mục đích mở tệp ảnh để thực hiện việc chuyển màu sang chế độ xám với các giá trị pixel [0 , 255].
- im_1 = np.asarray(img) : thực hiện việc chuyển ảnh để xử lý số thành mảng 2D với mỗi phần tử có giá trị cường độ pixel [0,255].
- gamma = 0.5 : Định nghĩa giá trị gamma = 0.5 điều khiển mức độ sáng - tối của ảnh.
- b1 = im_1.astype(float) : Chuyển mảng sang kiểu float để thực hiện phép toán và không gây mất dữ liệu.
- b2 = np.max(b1) : Tìm cường độ pixel lớn nhất có trong ảnh.
- b3 = b1 / b2 : Chuẩn hóa giá trị pixel về [0,1].
- b2 = np.log(b3 + 1e-8) * gamma : Dùng để biến đổi logarit với gamma bằng tính logarit = các giá trị xác định chuyển hóa và nhân với gamma để kiểm soát mức độ biến đổi kiểm soát mức độ sáng và tối.
- c = np.exp(b2) * 255.0 : Sau khi tính, bắt đầu chuyển đổi ngược lại và mở rộng về phạm vi [0,255].
-  c1 = np.clip(c, 0, 255).astype(np.uint8) : Giới hạn cho các giá trị pixel [0,255] và chuyển sang kiểu uint8 để phù hợp với ảnh PIL.
-  d = Image.fromarray(c1) : Xử lý thành ảnh PIL.
- img.show() : Hiển thị ảnh gốc
- plt.imshow(d) : Hiển thị ảnh nghịch đảo.
- plt.show() : Hiển thị ảnh plt chứa ảnh nghịch đảo

1.3
- Nhập các thư viện cần thiết cho bài tập.
- img = Image.open('bird.png').convert('L') : Sử dụng hàm này với mục đích mở tệp ảnh để thực hiện việc chuyển màu sang chế độ xám với các giá trị pixel [0 , 255].
- im_1 = np.asarray(img) : thực hiện việc chuyển ảnh để xử lý số thành mảng 2D với mỗi phần tử có giá trị cường độ pixel [0,255].
- b1 = im_1.astype(float) : Chuyển mảng sang kiểu float để thực hiện phép toán và không gây mất dữ liệu.
- b2 = np.max(b1) : Tìm cường độ pixel lớn nhất có trong ảnh.
- c = (128.0 * np.log(1 + b1)) / np.log(1 + b2) : Biến đổi logarit để tăng cường độ tương phản ở các vùng tối. ( np.log(1 + b1)) là logarit của các giá trị pixel được tăng lên 1 rồi nhân với 128.0 và chia cho np.log(1 + b2) là phần logarit có giá trị tối đa để chuẩn hóa kết quả logarit.
-  c1 = np.clip(c, 0, 255).astype(np.uint8) : Giới hạn cho các giá trị pixel [0,255] và chuyển sang kiểu uint8 để phù hợp với ảnh PIL.
-  d = Image.fromarray(c1) : Xử lý thành ảnh PIL.
- img.show() : Hiển thị ảnh gốc
- d.show() : Hiển thị ảnh nghịch đảo.
- plt.show(d) : Hiển thị ảnh đã áp dụng biến đổi logarit.
- plt.show(): Hiển thị ảnh qua cửa sổ. 

1.4
- Nhập các thư viện cần thiết cho bài tập.
- img = Image.open('bird.png').convert('L') : Sử dụng hàm này với mục đích mở tệp ảnh để thực hiện việc chuyển màu sang chế độ xám với các giá trị pixel [0 , 255].
- im1 = np.asarray(img) : thực hiện việc chuyển ảnh để xử lý số thành mảng 2D với mỗi phần tử có giá trị cường độ pixel [0,255].
- b1 = im1.flatten() : Hàm im1.flatten() giúp chuyển mảng 2D thành mảng 1D để tính toán histogram. 
- hist, bins = np.histogram(im1, 256, [0,255]): Hàm np.histogram(im1, 256, [0,255]) tạo histogramt với 256 bin từ 0 đến 255 và trả về hist và bins.
-  cdf = hist.cumsum()  : Hàm hist.cumsum() là hàm tính tổng tích lũy của histogram .
-  cdf_m = np.ma.masked_equal(cdf, 0) : Loại bỏ các giá trị CDF = 0.
-  num_cdf_m = (cdf_m - cdf_m.min()) * 255
-  den_cdf_m = (cdf.max() - cdf_m.min()) : Tính mẫu số để chuẩn hóa CDF.
-  cdf_m = num_cdf_m / den_cdf_m : Dùng num_cdf_m chia cho den_cdf_m để tạo ra mảng CDF chuẩn hóa với các ánh xạ giá trị pixel ban đầu sang giá trị mới.
-  cdf = np.ma.filled(cdf_m, 0).astype('uint8') : Hàm np.ma.filled(cdf_m, 0) để thay các giá trị bị che trong cdf_m = 0 và chuyển sang kiểu uint8 để phù hợp với ảnh 8-bit.
-  im2 = cdf[b1] : Dùng mảng b1 là các giá trị pixel gốc dạng 1D để tra cứu giá trị mới từ cdf và tạo ra mảng im2 chứa các giá trị pixel đã cân bằng.
-  im3 = np.reshape(im2, im1.shape) : Sử dụng hàm np.reshape(im2, im1.shape) để định dạng lại mảng ở im2 về ban đầu của im1 và tạo mảng 2D cho im3.
-  im4 = Image.fromarray(im3) : Xử lý ảnh thành ảnh PIL.
- img.show() : Hiển thị ảnh gốc
- im4.show() : Hiển thị ảnh đã cân bằng histogram.
- plt.imshow(im4) : Hiển thị ảnh đã được cân bằng Histogram với Matplotlib.
- plt.show(): Hiển thị ảnh đã xử lý.

1.5
- Nhập các thư viện cần thiết cho bài tập.
- img = Image.open('bird.png').convert('L') : Sử dụng hàm này với mục đích mở tệp ảnh để thực hiện việc chuyển màu sang chế độ xám với các giá trị pixel [0 , 255].
- im1 = np.asarray(img) : thực hiện việc chuyển ảnh để xử lý số thành mảng 2D với mỗi phần tử có giá trị cường độ pixel [0,255].
- b = im1.max() : Tìm cường độ pixel lớn nhất có trong ảnh.
- a = im1.min() : Tìm cường độ pixel nhỏ nhất có trong ảnh.
- c = im_1.astype(float) : Chuyển mảng sang kiểu float để thực hiện phép toán và không gây mất dữ liệu.
- im2 = 255 * (c - a) / (b - a) : Dùng để kéo giãn độ tương phản.
- im3 = Image.fromarray(im2) : Xử lý thành ảnh .
- img.show() : Hiển thị ảnh gốc
- im3.show() : Hiển thị ảnh đã kéo giãn tương phản.
- plt.imshow(im3): Hiển thị ảnh đã kéo giãn độ tương phản.
- plt.show() : Hiển thị ảnh đã xử lý.

1.6.1
- Nhập các thư viện cần thiết cho bài tập.
- img = Image.open('bird.png').convert('L') : Sử dụng hàm này với mục đích mở tệp ảnh để thực hiện việc chuyển màu sang chế độ xám với các giá trị pixel [0 , 255].
- im1 = np.asarray(img) : thực hiện việc chuyển ảnh để xử lý số thành mảng 2D với mỗi phần tử có giá trị cường độ pixel [0,255].
- c = abs(scipy.fftpack.fft2(im1)) : Thực hiện để biến đổi Fourier nhanh 2D và lấy biên độ ảnh.
- d = d.astype(float) : Chuyển mảng d sang kiểu float.
- im3 = Image.fromarray(d) : Chuyển mảng d thành mảng PIL
- img.show() : Hiển thị ảnh gốc
- im3.show() : Hiển thị ảnh phổ tần số.
- plt.imshow(im3): Hiển thị ảnh phổ tần số bằng Matplotlib.
- plt.show() : Hiển thị ảnh đã xử lý.

1.6.2
- Sử dụng các thư viện cần thiết.
- img = Image.open('bird.png').convert('L') : Sử dụng hàm này với mục đích mở tệp ảnh để thực hiện việc chuyển màu sang chế độ xám với các giá trị pixel [0 , 255].
- im1 = np.asarray(img) : thực hiện việc chuyển ảnh để xử lý số thành mảng 2D với mỗi phần tử có giá trị cường độ pixel [0,255].
- c = abs(scipy.fftpack.fft2(im1)) : Thực hiện để biến đổi Fourier nhanh 2D và lấy biên độ ảnh.
- d = scipy.fftpack.fftshift(c) : Hàm scipy.fftpack.fftshift() dùng để dịch chuyển phổ tần số đưa tần số 0 vào trung tâm mảng.
- M = d.shape[0] / N = d.shape[1] : Lấy kích thước của mảng phổ tần số.
- H = np.zeros((M, N)) : Tạo mảng mặt nạ lọc Butterworth với kích thước của M và N.
- center1 = M / 2. / center2 = N / 2. : Xác định trung tâm của phổ tần số.
- d_0 = 30.0. / t1 = 1. /t2 = 2 * t1. : Định nghĩa các tham số cho bộ lọc Butterworth.
- for i in range(1, M):
    for j in range(1, N):
        r1 = (i - center1) ** 2 + (j - center2) ** 2
        r = math.sqrt(r1)
        if r > d_0:
            H[i, j] = 1 / (1 + (r / d_0) ** t1)
  => Sử dụng vòng lặp for để tạo mặt nạ bộ lọc thông thấp Butterworth.
- H = H.astype(float) : Chuyển mảng mặt nạ sang kiểu float.
- H = Image.fromarray(H) : Chuyển mảng mặt nạ sang mảng PIL.
- con = d * H : Nhân với mảng phổ tần số d và H .
- e = abs(scipy.fftpack.ifft2(con)) : Thực hiện biến đổi Fourier ngược để trở về miền không gian.
- e = e.astype(float) : Chuyển mảng sang kiểu float.
- im3 = Image.fromarray(e) : Chuyển mảng thành ảnh PIL.
- img.show() : Hiển thị ảnh gốc
- im3.show() : Hiển thị ảnh đã lọc. 
- plt.imshow(im3): Hiển thị ảnh phổ tần số bằng Matplotlib.
- plt.show() : Hiển thị ảnh đã xử lý.

1.6.3
- Sử dụng các thư viện cần thiết cho bài tập.
- img = Image.open('bird.png').convert('L') : Sử dụng hàm này với mục đích mở tệp ảnh để thực hiện việc chuyển màu sang chế độ xám với các giá trị pixel [0 , 255].
- im1 = np.asarray(img) : thực hiện việc chuyển ảnh để xử lý số thành mảng 2D với mỗi phần tử có giá trị cường độ pixel [0,255].
- c = abs(scipy.fftpack.fft2(im1)) : Thực hiện để biến đổi Fourier nhanh 2D và lấy biên độ ảnh.
- d = scipy.fftpack.fftshift(c) : Hàm scipy.fftpack.fftshift() dùng để dịch chuyển phổ tần số đưa tần số 0 vào trung tâm mảng.
- M = d.shape[0] / N = d.shape[1] : Lấy kích thước của mảng phổ tần số.
- H = np.zeros((M, N)) : Tạo mảng mặt nạ lọc Butterworth với kích thước của M và N.
- center1 = M / 2. / center2 = N / 2. : Xác định trung tâm của phổ tần số.
- d_0 = 30.0. / t1 = 1. /t2 = 2 * t1. : Định nghĩa các tham số cho bộ lọc Butterworth.
- for i in range(1, M):
    for j in range(1, N):
        r1 = (i - center1) ** 2 + (j - center2) ** 2
        r = math.sqrt(r1)
        if r > d_0:
            H[i, j] = 1 / (1 + (r / d_0) ** t2)
  => Sử dụng vòng lặp for để tạo mặt nạ bộ lọc thông cao Butterworth.
- H = H.astype(float) : Chuyển mảng mặt nạ sang kiểu float.
- H = Image.fromarray(H) : Chuyển mảng mặt nạ sang mảng PIL.
- con = d * H : Nhân với mảng phổ tần số d và H .
- e = abs(scipy.fftpack.ifft2(con)) : Thực hiện biến đổi Fourier ngược để trở về miền không gian.
- e = e.astype(float) : Chuyển mảng sang kiểu float.
- im3 = Image.fromarray(e) : Chuyển mảng thành ảnh PIL.
- img.show() : Hiển thị ảnh gốc
- im3.show() : Hiển thị ảnh đã lọc. 
- plt.imshow(im3): Hiển thị ảnh phổ tần số bằng Matplotlib.
- plt.show() : Hiển thị ảnh đã xử lý.
