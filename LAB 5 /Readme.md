#cau 2.1 
Nhập các thư viện cần thiết để xử lý ảnh, tính ngưỡng, phân vùng và hiển thị.
data = Image.open('geometric.png').convert('L'): Mở ảnh 'geometric.png' và chuyển sang ảnh xám (grayscale) với các giá trị pixel từ 0 đến 255.
a = np.asarray(data): Chuyển ảnh PIL sang mảng NumPy 2D để xử lý số học.
thres = threshold_otsu(a): Áp dụng thuật toán Otsu để tìm ngưỡng phân chia ảnh nhị phân tự động.
b = a > thres: Tạo ảnh nhị phân, các pixel có giá trị lớn hơn ngưỡng sẽ được giữ lại.
c = label(b): Gán nhãn cho từng vùng liên thông trong ảnh nhị phân.
c_uint8 = (255 * (c / np.max(c))).astype(np.uint8): Chuẩn hóa ảnh đã gán nhãn về thang xám [0,255] và chuyển sang kiểu uint8.
cl = Image.fromarray(c_uint8): Tạo ảnh PIL từ mảng gán nhãn đã chuẩn hóa.
iio.imwrite('label_output.jpg', c_uint8): Lưu ảnh gán nhãn ra tệp 'label_output.jpg'.
d = regionprops(c): Tính các đặc trưng của từng vùng nhãn như diện tích, tâm, và bounding box.
fig, ax = plt.subplots(...): Tạo khung vẽ matplotlib để hiển thị ảnh đã gán nhãn.
ax.imshow(c, cmap='YlOrRd'): Hiển thị ảnh nhãn với bản đồ màu.
mpatches.Rectangle(...): Vẽ các hình chữ nhật bao quanh mỗi vùng được phát hiện dựa trên thông tin tọa độ.
plt.show(): Hiển thị toàn bộ ảnh có các vùng được phân vùng và khung bao.
=> kết quả: <img width="1631" height="854" alt="ảnh" src="https://github.com/user-attachments/assets/ea7bdeb6-b729-46ff-bfc6-d39195f579bc" />


#câu 2.2:
Nhập các thư viện cần thiết để xử lý ảnh, tính toán và hiển thị kết quả.
data = Image.open('geometric.png').convert('L') : Mở ảnh 'geometric.png' và chuyển ảnh sang dạng xám với giá trị pixel từ 0 đến 255.
bmg = abs(data - nd.shift(data, (0, 1), order=0)) : Tính toán ảnh biên bằng cách trừ ảnh gốc với chính nó sau khi dịch ngang 1 pixel bằng hàm shift, rồi lấy giá trị tuyệt đối để làm nổi bật sự thay đổi cường độ.
plt.imshow(bmg) : Hiển thị ảnh biên sau xử lý bằng thư viện matplotlib.
plt.show : Thực hiện hiển thị ảnh đã xử lý.
=> kết quả: <img width="1538" height="799" alt="ảnh" src="https://github.com/user-attachments/assets/f2b86095-88f8-4848-bf1c-f9776d46bedf" />

#cau 2.3:
Nhập các thư viện cần thiết để xử lý ảnh, phát hiện biên và hiển thị kết quả.
data = Image.open('geometric.png') : Mở ảnh 'geometric.png' gốc ở định dạng ảnh PIL RGB hoặc grayscale.
a = nd.sobel(data, axis=0) : Tính đạo hàm theo trục dọc (Ox) bằng toán tử Sobel để phát hiện biên theo chiều ngang.
b = nd.sobel(data, axis=1) : Tính đạo hàm theo trục ngang (Oy) để phát hiện biên theo chiều dọc.
bmg = abs(a) + abs(b) : Tính tổng giá trị tuyệt đối theo hai hướng để làm nổi bật toàn bộ biên ảnh.
plt.imshow(bmg) : Hiển thị ảnh biên bằng thư viện matplotlib.
plt.show : Thực hiện hiển thị ảnh biên đã tính toán.
=> ket quả: <img width="709" height="404" alt="ảnh" src="https://github.com/user-attachments/assets/452bbbab-6bf5-4ecd-873d-0801dfed51f2" />

#cau 2.4:
Nhập các thư viện cần thiết để xử lý ảnh, tính biên, lọc Gauss và hiển thị kết quả.
Định nghĩa hàm Harris dùng để phát hiện điểm góc trong ảnh dựa trên đạo hàm Sobel và công thức ma trận cấu trúc.
    x = nd.sobel(indata, 0) : Tính đạo hàm ảnh theo trục dọc (Ox)
    y = nd.sobel(indata, 1) : Tính đạo hàm ảnh theo trục ngang (Oy)
    xl = x ** 2, yl = y ** 2, xy = abs(x * y) : Tính các tích riêng phần cần cho ma trận cấu trúc
    nd.gaussian_filter(..., 3) : Làm mượt các ma trận trên bằng bộ lọc Gauss kích thước 3
    detC = xl * yl - 2 * xy : Tính định thức của ma trận cấu trúc
    trC = xl + yl : Tính trace của ma trận cấu trúc
    R = detC - alpha * trC**2 : Công thức tính giá trị phản hồi góc theo phương pháp Harris
    Trả về ma trận giá trị Harris để xác định điểm góc mạnh
data = Image.open('geometric.png') : Mở ảnh 'geometric.png' từ file
bmg = Harris(data) : Áp dụng hàm phát hiện góc lên ảnh
plt.imshow(bmg) : Hiển thị ảnh kết quả thể hiện các điểm có phản hồi góc cao
plt.show : Hiển thị ảnh góc đã phát hiện
=> ket quả: <img width="1511" height="795" alt="ảnh" src="https://github.com/user-attachments/assets/a317a49f-46dd-40cb-8d3c-b379ce6be76c" />

#cau 2.5.1:
Nhập các thư viện cần thiết để xử lý ảnh, tính toán và hiển thị kết quả.
Định nghĩa hàm LineHough để thực hiện phép biến đổi Hough phát hiện đường thẳng:
    V, H = data.shape : Lấy kích thước chiều ảnh đầu vào
    R = int(np.sqrt(V * V + H * H)) : Tính bán kính tối đa trong không gian Hough
    ho = np.zeros((R, 90), float) : Tạo không gian Hough với các giá trị theta từ 0 đến 89 độ
    w = data + 0 : Sao chép ảnh gốc sang biến tạm để xử lý
    theta = np.arange(90)/180 * pi : Tạo danh sách góc theta tính bằng radian
    Trong vòng lặp while:
        Tìm điểm ảnh có giá trị lớn nhất mx
        Nếu nhỏ hơn ngưỡng gamma, kết thúc
        Ngược lại, tính tọa độ điểm ảnh đó
        Áp dụng công thức rho = x * cos(theta) + y * sin(theta) để xác định vị trí trong không gian Hough
        Cập nhật điểm tương ứng trong mảng ho
        Xóa điểm đã xét khỏi w
data = np.zeros((256, 256)) : Tạo ảnh rỗng kích thước 256x256
data[128, 128] = 1 : Gán một điểm trắng tại trung tâm ảnh
bmg = LineHough(data, 0.5) : Thực hiện biến đổi Hough với ngưỡng gamma = 0.5
plt.imshow(bmg) : Hiển thị không gian Hough
plt.show : Hiển thị kết quả cuối cùng lên màn hình
=> ket qua: <img width="532" height="777" alt="ảnh" src="https://github.com/user-attachments/assets/c360e469-41a7-43f7-8582-23fc6e2ab3a7" />

# cau 2.5.2:
Nhập các thư viện cần thiết để xử lý ảnh, phát hiện góc và hiển thị kết quả.
data = iio.imread('bird.png') : Đọc ảnh 'bird.png' dưới dạng mảng RGB từ thư viện imageio.
image_gray = rgb2gray(data) : Chuyển ảnh màu sang ảnh xám để phục vụ phát hiện góc.
coordinate = corner_harris(image_gray, k = 0.001) : Áp dụng thuật toán Harris Corner Detection để phát hiện các điểm góc với tham số k điều chỉnh độ nhạy.
plt.figure(figsize=(20,10)) : Tạo khung ảnh lớn để hiển thị rõ góc.
plt.imshow(coordinate) : Hiển thị bản đồ phản hồi Harris – nơi nào giá trị cao là điểm góc mạnh.
plt.axis 'off' : Ẩn trục tọa độ để dễ quan sát.
plt.show : Hiển thị ảnh kết quả lên màn hình.

#cau 2.6
Nhập các thư viện cần thiết.
img1 = cv2.imread('bird.png'), img2 = cv2.imread('geometric.png'): Đọc hai ảnh cần so khớp.
cv2.resize(...): Thay đổi kích thước cả hai ảnh về 400x400 để đảm bảo khi ghép chúng lại không bị lỗi.
gray1 = rgb2gray(img1), gray2 = rgb2gray(img2): Chuyển hai ảnh sang ảnh xám để xử lý phát hiện đặc trưng dễ hơn.
corner_harris(...), corner_peaks(...): Dùng thuật toán Harris Corner Detector để tìm ra các điểm đặc trưng (góc) trong từng ảnh. Chỉ giữ những điểm cách nhau ít nhất 5 pixel.
get_descriptors(...): Hàm cắt các patch nhỏ 11x11 pixel xung quanh từng điểm đặc trưng để tạo vector mô tả đơn giản cho mỗi điểm.
cdist(...): Tính toán khoảng cách Euclidean giữa các vector mô tả của ảnh 1 và ảnh 2 → mục đích là tìm điểm giống nhất giữa hai ảnh.
np.argmin(dist, axis=1): Với mỗi điểm trong ảnh 1, tìm điểm tương ứng gần nhất trong ảnh 2 (dựa trên mô tả patch).
combined = np.hstack((img1, img2)): Nối hai ảnh lại cạnh nhau theo chiều ngang để hiển thị các cặp khớp.
plt.plot(...): Vẽ đường nối giữa các cặp điểm tương đồng từ ảnh 1 sang ảnh 2 để minh họa kết quả so khớp.
plt.show(): Hiển thị ảnh đã ghép cùng các đường nối thể hiện kết quả so khớp giữa hai ảnh.
=> kết quả: <img width="1541" height="816" alt="ảnh" src="https://github.com/user-attachments/assets/5ac84fde-b922-4167-bd3c-3ed9233c6c6f" />

