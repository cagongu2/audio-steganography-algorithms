# 📋 Checklist Tuần 4: Thuật Định Vị Pha (Phase Coding) Miền Tần Số

Mục tiêu tuần này là chuyển từ miền thời gian sang miền tần số, tìm hiểu cách thực hiện phép biến đổi Fourier (FFT), nguyên lý giấu tin vào phổ pha và tái hiện thuật toán Phase Coding sang Python.

---

## 🔬 1. Lý thuyết & Nguyên lý
- [ ] **Tìm hiểu phép biến đổi Fourier nhanh (FFT/IFFT)**:
  - [ ] Hiểu cách chuyển đổi tín hiệu từ miền thời gian sang miền tần số số phức.
  - [ ] Hiểu cấu trúc của số phức tần số: Biên độ (Magnitude) và Góc pha (Phase/Angle).
- [ ] **Tìm hiểu nguyên lý Phase Coding**:
  - [ ] Hiểu lý do tại sao tai người nhạy cảm với biên độ tần số nhưng ít nhạy cảm với pha tuyệt đối.
  - [ ] Cách mã hóa bit tin nhắn bằng cách áp góc pha cụ thể ($\pi/2$ hoặc $-\pi/2$) vào khung đầu tiên.
  - [ ] Cách điều chỉnh dịch pha tương đối của các khung tiếp theo để duy trì tính liên tục của sóng âm thanh.

---

## 🔎 2. Phân tích mã nguồn Matlab gốc
- [ ] **Đọc hiểu tệp mã nguồn Matlab [phase_enc.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/04-Phase-Coding/phase_enc.m)**:
  - [ ] Phân tích dòng code dùng `fft()` để lấy phổ tần số.
  - [ ] Xem cách tác giả lấy biên độ (`abs()`) và pha (`angle()`).
  - [ ] Nghiên cứu thuật toán tính pha lũy tiến để giữ tính liên tục của pha giữa các khung kề nhau.
  - [ ] Xem cách khôi phục tín hiệu số phức bằng công thức Euler rồi dùng `ifft()` và `real()` để trả về dạng sóng âm thanh.
- [ ] **Đọc hiểu tệp mã nguồn Matlab `phase_dec.m`**:
  - [ ] Phân tích cách trích xuất góc pha của khung đầu tiên bằng `angle(fft())` để giải mã ra bit thông tin.

---

## 💻 3. Tái hiện bằng Python
- [ ] **Triển khai FFT và IFFT trong Python**:
  - [ ] Sử dụng `numpy.fft.fft` và `numpy.fft.ifft` để biến đổi phổ tần số của các khung tín hiệu.
- [ ] **Triển khai bộ mã hóa Phase Coding (Encoder)**:
  - [ ] Tính toán mảng biên độ và mảng pha bằng `numpy.abs` và `numpy.angle`.
  - [ ] Thiết lập pha tham chiếu mới cho khung đầu tiên dựa trên bit thông tin.
  - [ ] Điều chỉnh tịnh tiến góc pha cho các khung tiếp theo.
  - [ ] Tái dựng số phức bằng công thức Euler: `amplitude * np.exp(1j * new_phase)` rồi thực hiện IFFT để thu hồi stego signal.
- [ ] **Triển khai bộ giải mã Phase Coding (Decoder)**:
  - [ ] Thực hiện FFT khung đầu tiên của file stego, trích xuất pha của các tần số cụ thể để khôi phục lại bit tin nhắn.

---

## 📊 4. Đánh giá kiểm chứng
- [ ] **Đo đạc chất lượng**: Tính toán chỉ số SNR giữa file gốc và file stego.
- [ ] **Vẽ phổ tần số**: Sử dụng `matplotlib` để vẽ dạng đồ thị pha của tín hiệu trước và sau khi nhúng để kiểm chứng mặt lý thuyết.
