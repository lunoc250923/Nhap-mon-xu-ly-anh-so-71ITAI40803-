Cau 1:
- Nhập thư viên cần thiết cho bài tập
- data = iio.imread('exercise/colorful-ripe-tropical-fruits.jpg') : Đọc ảnh theo yêu cầu
- bng = data[650:900, 1380:1630]: Cắt ảnh Kiwi
- bdata = nd.shift(bng, (100, 30, 0)) : Điều chỉnh ảnh sang phải 30 độ
- iio.imwrite('kiwiex.jpg', bdata): Đọc và lưu ảnh
- plt.imshow(bdata) / plt.show() : Hiển thị ảnh
=> Kết quả: ![ảnh](https://github.com/user-attachments/assets/c6249e8d-3dbe-455f-9b92-225db7c60e15)
Cau 2: 
- Nhập thư viên cần thiết cho bài tập
- data = iio.imread('exercise/colorful-ripe-tropical-fruits.jpg') : Đọc ảnh theo yêu cầu
- duahau = data[300:1150, 1600:] : Cắt ảnh dưa hấu
- duahau[:, :, 1] = np.clip(duahau[:, :, 1] + 60, 0, 255)  # xanh lá / duahau[:, :, 0] = np.clip(duahau[:, :, 0] - 40, 0, 255) #Đỏ : Chỉnh màu ảnh
- iio.imwrite('kiwiex.jpg', duahau) : Lưu và tạo ảnh mới đã được đổi màu
- plt.imshow(duahau) / plt.show() : Hiển thị ảnh.
- dudu = data[300:800, 100:700] : cắt ảnh đu đủ
- dudu[:, :, 0] = np.clip(dudu[:, :, 0] + 80, 0, 255) #Xanh / dudu[:, :, 1] = np.clip(dudu[:, :, 1] - 30, 0, 255) # Đỏ : Chỉnh màu ảnh mới
- iio.imwrite('kiwiex1.jpg', dudu) : Lưu và tạo ảnh mới đã được đổi màu
- plt.imshow(dudu) / plt.show(): Hiển thị ảnh
  => kết quả: 
dưa hấu: ![ảnh](https://github.com/user-attachments/assets/a7816c15-2a73-4153-8627-ae8e4d0ae647)
đu đủ: ![ảnh](https://github.com/user-attachments/assets/2b202544-cdf4-4abc-9f49-583557588daf)

Câu 3:
- Nhập thư viên cần thiết cho bài tập
- data = iio.imread('exercise/quang_ninh.jpg') : Đọc ảnh theo yêu cầu
- cut = data[:300, 400:650] : Cắt ảnh núi
- nui = nd.rotate(cut, 45, reshape=False) : Xoay ảnh 45 độ không thay đổi kích cỡ 
- plt.imshow(nui) / plt.show() : Hiển thị ảnh
- cut1 = data[350:550, 450:650] : Cắt ảnh thuyền
- thuyen = nd.rotate(cut1, 45, reshape=False) : Xoay ảnh 45 độ không thay đổi kích cỡ
- plt.imshow(thuyen) / plt.show() : Hiển thị ảnh
=> Kết quả:
Núi: ![ảnh](https://github.com/user-attachments/assets/44970146-3ecc-4ec4-8f98-b91cb6c60b34)
Thuyền:  ![ảnh](https://github.com/user-attachments/assets/50aec9ac-9b5c-455e-a047-13d9692e133f)

Câu 4: 
- Nhập thư viên cần thiết cho bài tập
- data = iio.imread('exercise/pagoda.jpg') : Đọc ảnh theo yêu cầu
- bdata = nd.zoom(data, (5, 5, 1)) : Phóng to ảnh lên gấp 5 lần
- plt.imshow(bdata) / plt.show() : Hiển thị ảnh
=> Kết quả: ![ảnh](https://github.com/user-attachments/assets/b65d010d-427c-497f-8e29-ae1174d7892b)

