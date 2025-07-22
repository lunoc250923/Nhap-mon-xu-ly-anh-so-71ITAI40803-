Câu 1:
Nhập các thư viện cần thiết cho bài tập.
import numpy as np: Thư viện NumPy hỗ trợ xử lý mảng số học và các phép tính ma trận nhanh.
import imageio.v2 as iio: Thư viện dùng để đọc và lưu ảnh với nhiều định dạng.
import scipy.ndimage as sn: Thư viện dùng cho xử lý ảnh như lọc, biến đổi và phân tích ảnh.
from skimage import feature: Sử dụng để khai thác các chức năng phát hiện đặc trưng, ví dụ như bộ lọc Canny.
import matplotlib.pylab as plt: Thư viện vẽ đồ thị và hiển thị ảnh.
import colorsys: Thư viện xử lý chuyển đổi màu sắc giữa RGB và HSV.

a = iio.imread('a.jpg', mode='L').astype(np.uint8): Đọc ảnh đầu vào a.jpg ở chế độ xám (grayscale), chuyển đổi thành kiểu dữ liệu 8-bit để dễ xử lý, mỗi pixel có giá trị từ 0 đến 255.

k = np.ones((5, 5)) / 25: Tạo một kernel (ma trận) 5x5 có tất cả giá trị bằng 1, chia cho 25 để tạo bộ lọc trung bình (mean filter).
b = sn.convolve(a, k).astype(np.uint8): Thực hiện phép chập (convolution) giữa ảnh gốc và kernel để làm mờ ảnh, kết quả chuyển sang kiểu dữ liệu 8-bit.
iio.imsave('a_mean.jpg', b): Lưu ảnh sau khi áp dụng bộ lọc trung bình thành tệp a_mean.jpg.

c = feature.canny(a, sigma=3).astype(np.uint8) * 255: Sử dụng bộ lọc Canny để phát hiện biên ảnh, sigma=3 điều chỉnh độ nhạy với nhiễu, nhân với 255 để các đường biên rõ nét.
iio.imsave('a_Canny.jpg', c): Lưu ảnh kết quả phát hiện biên dưới dạng tệp a_Canny.jpg.

img_rgb = iio.imread('a.jpg').astype(np.float32): Đọc ảnh gốc a.jpg ở dạng màu RGB và chuyển dữ liệu thành số thực 32-bit để dễ xử lý.
if len(img_rgb.shape) == 2: img_rgb = np.stack((img_rgb, img_rgb, img_rgb), axis=-1): Nếu ảnh là ảnh xám, sao chép thành ba kênh (RGB) để tạo ảnh màu giả lập.

r = np.clip(img_rgb[:, :, 0] * np.random.uniform(0.5, 1.5), 0, 255): Tạo kênh màu đỏ mới bằng cách nhân giá trị pixel kênh R với một hệ số ngẫu nhiên (0.5 đến 1.5), giới hạn giá trị từ 0 đến 255.
g = np.clip(img_rgb[:, :, 1] * np.random.uniform(0.5, 1.5), 0, 255): Tạo kênh màu xanh lá mới theo cách tương tự với kênh G.
b = np.clip(img_rgb[:, :, 2] * np.random.uniform(0.5, 1.5), 0, 255): Tạo kênh màu xanh dương mới theo cách tương tự với kênh B.
random_rgb = np.stack((r, g, b), axis=-1).astype(np.uint8): Ghép các kênh màu R, G, B đã chỉnh sửa để tạo thành ảnh màu mới và chuyển về kiểu dữ liệu 8-bit.
iio.imsave('a_rgb.jpg', random_rgb): Lưu ảnh với màu RGB ngẫu nhiên thành a_rgb.jpg.

rgb_norm = img_rgb / 255.0: Chuẩn hóa các giá trị pixel RGB về khoảng [0,1] để dễ chuyển đổi sang không gian màu khác.
rgb2hsv = np.vectorize(colorsys.rgb_to_hsv): Chuyển đổi từng pixel từ hệ màu RGB sang HSV bằng cách vector hóa hàm rgb_to_hsv.
h, s, v = rgb2hsv(rgb_norm[:, :, 0], rgb_norm[:, :, 1], rgb_norm[:, :, 2]): Tách các kênh Hue (màu sắc), Saturation (độ bão hòa), Value (độ sáng) từ ảnh RGB đã chuẩn hóa.

h_img = (h * 255).astype(np.uint8): Chuyển kênh Hue từ dạng chuẩn hóa về ảnh xám với giá trị 0-255.
s_img = (s * 255).astype(np.uint8): Chuyển kênh Saturation về ảnh xám với giá trị 0-255.
v_img = (v * 255).astype(np.uint8): Chuyển kênh Value về ảnh xám với giá trị 0-255.

iio.imsave('a_hue.jpg', h_img): Lưu kênh Hue thành ảnh xám.
iio.imsave('a_saturation.jpg', s_img): Lưu kênh Saturation thành ảnh xám.
iio.imsave('a_value.jpg', v_img): Lưu kênh Value thành ảnh xám.

plt.figure(figsize=(12, 6)): Tạo một cửa sổ hiển thị với kích thước 12x6 inch.
plt.subplot(231), plt.imshow(b, cmap='gray'), plt.title("Mean Filter"): Hiển thị ảnh sau khi lọc trung bình trên vị trí đầu tiên, đặt tiêu đề.
plt.subplot(232), plt.imshow(c, cmap='gray'), plt.title("Canny Edges"): Hiển thị ảnh biên Canny.
plt.subplot(233), plt.imshow(random_rgb), plt.title("Random RGB Colors"): Hiển thị ảnh màu RGB ngẫu nhiên.
plt.subplot(234), plt.imshow(h_img, cmap='gray'), plt.title("Hue Channel"): Hiển thị kênh Hue.
plt.subplot(235), plt.imshow(s_img, cmap='gray'), plt.title("Saturation Channel"): Hiển thị kênh Saturation.
plt.subplot(236), plt.imshow(v_img, cmap='gray'), plt.title("Value Channel"): Hiển thị kênh Value.
plt.tight_layout(): Tự động điều chỉnh bố cục để các hình không bị đè.
plt.show(): Hiển thị toàn bộ các ảnh đã xử lý trên cửa sổ.

Câu 2:
import cv2: Thư viện OpenCV dùng để xử lý ảnh và video.
import numpy as np: Thư viện NumPy hỗ trợ mảng và các phép toán số học.
import matplotlib.pyplot as plt: Thư viện vẽ và hiển thị ảnh.
import random: Thư viện sinh số ngẫu nhiên cho các tham số biến đổi.
import os: Thư viện quản lý tệp và thư mục.

image_files = ['image1.jpg', 'image2.jpg', 'image3.jpg']: Danh sách chứa tên các ảnh đầu vào.

images = []: Tạo danh sách trống để lưu ảnh đọc được.
for f in image_files: Duyệt qua từng tên ảnh.
img = cv2.imread(f, cv2.IMREAD_GRAYSCALE): Đọc ảnh ở dạng grayscale (xám).
if img is None: raise FileNotFoundError(...): Báo lỗi nếu ảnh không tồn tại.
images.append(img): Thêm ảnh đã đọc vào danh sách images.

if not os.path.exists('outputs'): os.makedirs('outputs'): Kiểm tra thư mục outputs, nếu chưa có thì tạo mới để lưu ảnh kết quả.

Khai báo các hàm xử lý:
inverse_transformation(img): Đảo ngược màu sắc của ảnh, chuyển vùng sáng thành tối.
gamma_correction(img, gamma): Thay đổi độ sáng/độ tương phản bằng công thức Gamma, hệ số gamma chọn ngẫu nhiên từ 0.5 đến 2.0.
log_transformation(img, c): Dùng phép log để làm nổi bật chi tiết vùng tối, hệ số c chọn ngẫu nhiên từ 1.0 đến 5.0.
histogram_equalization(img): Cân bằng histogram làm tăng độ tương phản ảnh.
contrast_stretching(img, min_val, max_val): Dãn độ tương phản, chuẩn hóa giá trị pixel trong khoảng [min_val, max_val] ngẫu nhiên.
adaptive_histogram_equalization(img): Cân bằng histogram cục bộ (CLAHE) để cải thiện độ sáng vùng nhỏ.

methods = {...}: Tạo từ điển liên kết phím bấm (I, G, L, H, C, A) với từng hàm và tên phương pháp tương ứng.

In menu hướng dẫn lựa chọn biến đổi ảnh.
while True: Vòng lặp chính cho phép chọn phím và thực hiện nhiều lần.
key = input(...).upper(): Lấy ký tự nhập từ người dùng và chuyển thành chữ hoa.
if key == 'Q': break: Thoát chương trình nếu bấm Q.
if key not in methods: continue: Bỏ qua nếu nhập sai phím.

func, name = methods[key]: Lấy hàm xử lý và tên từ methods.
results = []: Danh sách chứa ảnh kết quả sau khi biến đổi.
for i, img in enumerate(images, start=1):: Lặp qua 3 ảnh.
result = func(img): Áp dụng phương pháp xử lý lên ảnh.
cv2.imwrite(output_file, result): Lưu ảnh kết quả vào thư mục outputs.

Hiển thị 3 ảnh kết quả bằng matplotlib:
plt.figure(figsize=(15,5)): Tạo cửa sổ hiển thị lớn.
plt.subplot(1,3,idx): Chia cửa sổ thành 1 hàng 3 cột để hiển thị.
plt.imshow(result, cmap='gray'): Hiển thị từng ảnh kết quả dạng grayscale.
plt.title(...): Đặt tiêu đề cho từng ảnh.
plt.axis('off'): Ẩn trục tọa độ.
plt.show(): Hiển thị toàn bộ kết quả.

Câu 3:
import numpy as np: Thư viện NumPy hỗ trợ mảng số học.
import imageio.v2 as iio: Dùng để đọc và ghi ảnh.
import scipy.ndimage as sn: Thư viện xử lý ảnh (zoom, rotate, filter).
import matplotlib.pylab as plt: Hiển thị ảnh bằng matplotlib.
from skimage import feature: Thư viện trích xuất đặc trưng (ở đây chưa dùng).
import colorsys: Dùng cho chuyển đổi không gian màu (ở đây chưa dùng).

img = iio.imread('colorful-ripe-tropical-fruits.jpg'): Đọc ảnh gốc hoa quả.
h1, w1 = img.shape[:2]: Lấy chiều cao và chiều rộng ảnh.
new_h1 = h1 + 30, new_w1 = w1 + 30: Tính kích thước mới, tăng 30 pixel theo cả 2 chiều.
fruits_resized = sn.zoom(img, (new_h1 / h1, new_w1 / w1, 1)): Phóng to ảnh theo tỉ lệ mới.
fruits_resized = np.clip(...).astype(np.uint8): Giới hạn giá trị pixel trong [0,255] và chuyển về kiểu dữ liệu 8-bit.
iio.imwrite('resized_fruits.jpg', fruits_resized): Lưu ảnh phóng to.

quangninh = iio.imread('quang-ninh.jpg'): Đọc ảnh Quảng Ninh.
h2, w2 = quangninh.shape[:2]: Lấy kích thước.
rotated_qn = sn.rotate(quangninh, -45, reshape=True): Xoay ảnh 45 độ theo chiều kim đồng hồ.
flipped_qn = rotated_qn[:, ::-1]: Lật ngang ảnh sau khi xoay.
flipped_qn = np.clip(...).astype(np.uint8): Giới hạn giá trị pixel về 8-bit.
iio.imwrite('rotated_flipped_quangninh.jpg', flipped_qn): Lưu ảnh xoay và lật.

pagoda = iio.imread('pagoda.jpg'): Đọc ảnh ngôi chùa.
h3, w3 = pagoda.shape[:2]: Lấy kích thước.
pagoda_resized = sn.zoom(pagoda, (5, 5, 1)): Phóng to ảnh gấp 5 lần.
pagoda_blur = sn.gaussian_filter(pagoda_resized, sigma=(2.5,2.5,0)): Làm mờ ảnh bằng bộ lọc Gaussian.
pagoda_blur = np.clip(...).astype(np.uint8): Giới hạn giá trị pixel.
iio.imwrite('resized_blurred_pagoda.jpg', pagoda_blur): Lưu ảnh sau khi phóng to và làm mờ.

pagoda_float = pagoda_blur.astype(np.float32): Chuyển ảnh sang dạng float để thực hiện biến đổi log.
c = 255 / np.log(1 + np.max(pagoda_float)): Hệ số chuẩn hóa cho biến đổi log.
pagoda_log = c * np.log(1 + pagoda_float): Tính ảnh sau biến đổi log.
pagoda_log = np.clip(...).astype(np.uint8): Giới hạn giá trị và chuyển về dạng 8-bit.
iio.imwrite('log_pagoda.jpg', pagoda_log): Lưu ảnh sau khi biến đổi log.

Hiển thị kết quả bằng matplotlib:
plt.figure(figsize=(15,10)): Tạo khung hình lớn.
plt.subplot(2,2,1)... plt.subplot(2,2,4): Hiển thị lần lượt 4 ảnh (phóng to hoa quả, xoay+lật Quảng Ninh, chùa làm mờ, chùa log).
plt.imshow(...): Hiển thị từng ảnh.
plt.title(...): Đặt tiêu đề cho mỗi ảnh.
plt.tight_layout(): Điều chỉnh bố cục tự động.
plt.show(): Hiển thị toàn bộ ảnh kết quả.
