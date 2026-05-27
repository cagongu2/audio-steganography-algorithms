# 📋 Checklist Tuần 3: Thuật Toán DSSS (Direct Sequence Spread Spectrum)

Mục tiêu tuần này là hiểu nguyên lý trải phổ trực tiếp trong truyền thông, cách sử dụng chuỗi giả ngẫu nhiên trực giao để nhúng và trích xuất dữ liệu, và tái hiện thuật toán DSSS sang Python.

---

## 🔬 1. Lý thuyết & Nguyên lý
- [ ] **Tìm hiểu lý thuyết trải rộng phổ (Spread Spectrum)**:
  - [ ] Hiểu nguyên lý phân tán năng lượng của bit tin nhắn ra dải phổ rộng lớn bằng cách nhân nó với chuỗi tần số cao PN Sequence.
  - [ ] Nắm được nguyên nhân tại sao nhiễu phổ rộng có biên độ cực nhỏ lại khó bị phát hiện và có khả năng chống nhiễu cao.
- [ ] **Tìm hiểu cơ chế giải điều chế (Demodulation)**:
  - [ ] Hiểu tính chất trực giao của chuỗi ngẫu nhiên.
  - [ ] Hiểu phép nhân chéo và tích lũy tích vô hướng để lọc bỏ tín hiệu âm thanh gốc và phóng đại tín hiệu bit tin nhắn cần tìm.

---

## 🔎 2. Phân tích mã nguồn Matlab gốc
- [ ] **Đọc hiểu tệp mã nguồn Matlab [dsss_enc.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/01-Spread-Spectrum/01-DSSS-Conventional-Algorithm/dsss_enc.m)**:
  - [ ] Phân tích cách chuyển đổi bit sang dạng nhị phân lưỡng cực (bipolar) $\{-1, 1\}$.
  - [ ] Xem cơ chế phát sinh chuỗi giả ngẫu nhiên `prng` từ mật khẩu.
  - [ ] Xem công thức cộng tín hiệu phổ rộng điều chế vào tín hiệu gốc: `stego = signal + alpha * mix * pr`.
- [ ] **Đọc hiểu tệp mã nguồn Matlab `dsss_dec.m`**:
  - [ ] Phân tích cách bên nhận đồng bộ chuỗi giả ngẫu nhiên bằng cùng một password.
  - [ ] Xem thuật toán tích vô hướng để phục hồi bits.

---

## 💻 3. Tái hiện bằng Python
- [ ] **Triển khai bộ sinh số giả ngẫu nhiên tương thích**:
  - [ ] Sử dụng `numpy.random.default_rng` hoặc module `random` của Python để thiết lập hạt giống sinh chuỗi ngẫu nhiên gồm các giá trị $\{-1, 1\}$ đồng nhất giữa Encoder và Decoder.
- [ ] **Triển khai bộ mã hóa DSSS (Encoder)**:
  - [ ] Thực hiện phép nhân mảng (element-wise) giữa tín hiệu điều chế và chuỗi PN Sequence.
  - [ ] Cộng tín hiệu đã điều chế vào dữ liệu âm thanh gốc với hệ số biên độ nhúng $\alpha$.
- [ ] **Triển khai bộ giải mã DSSS (Decoder)**:
  - [ ] Thực hiện nhân chéo từng khung tín hiệu stego với chuỗi PN Sequence tương ứng.
  - [ ] Tính tổng tích lũy bằng `numpy.sum()` để quyết định dấu của bit giải mã được (dương là bit 1, âm là bit 0).

---

## 📊 4. Đánh giá kiểm chứng
- [ ] **Đo đạc chất lượng**: Tính toán chỉ số SNR giữa file gốc và file stego sau khi nhúng DSSS.
- [ ] **Đánh giá hiệu năng**: Đo lường tỷ lệ giải mã chính xác (BER) trên môi trường lý tưởng (không có nhiễu ngoài).
