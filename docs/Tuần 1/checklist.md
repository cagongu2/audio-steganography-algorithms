# 📋 Checklist Tuần 1: Nhập Môn & Triển Khai LSB Coding

Mục tiêu tuần này là thiết lập môi trường lập trình, hiểu các khái niệm cơ bản về âm thanh số và triển khai thành công thuật toán giấu tin LSB trên Python.

---

## 🛠️ 1. Môi trường & Lý thuyết nền tảng
- [ ] **Cài đặt Python và các thư viện cần thiết**: Chạy lệnh `pip install numpy scipy matplotlib soundfile` trong terminal.
- [ ] **Tìm hiểu lý thuyết âm thanh số**:
  - [ ] Hiểu khái niệm Tần số lấy mẫu (Sampling Rate, ví dụ: 44.1 kHz).
  - [ ] Hiểu khái niệm Độ phân giải bit (Bit Depth, ví dụ: 16-bit PCM).
  - [ ] Hiểu cấu trúc tệp âm thanh không nén `.wav`.
- [ ] **Tìm hiểu thuật toán LSB (Least Significant Bit)**:
  - [ ] Nắm được nguyên lý thay đổi bit cuối cùng của mẫu âm thanh để giấu bit dữ liệu.
  - [ ] Hiểu tại sao sự thay đổi này tai người không thể cảm nhận được (tính ẩn tín hiệu).
  - [ ] Nắm được cơ chế bảo mật bổ sung: Mã hóa XOR bằng chuỗi giả ngẫu nhiên sinh từ password.

---

## 🔎 2. Phân tích mã nguồn Matlab gốc
- [ ] **Đọc hiểu tệp mã nguồn Matlab [lsb_enc.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/03-LSB-Coding/lsb_enc.m)**:
  - [ ] Chỉ ra khối lệnh đọc dữ liệu thô (raw data) của tệp WAV.
  - [ ] Tìm hiểu cách mã hóa XOR thông tin bằng chuỗi giả ngẫu nhiên (`prng`).
  - [ ] Xem cách nhúng thông tin cấu trúc (8 bits checksum mật khẩu, 40 bits độ dài tin nhắn, và payload từ mẫu thứ 49).
- [ ] **Đọc hiểu tệp mã nguồn Matlab [lsb_dec.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/03-LSB-Coding/lsb_dec.m)**:
  - [ ] Xem cách trích xuất bits từ LSB của các mẫu âm thanh.
  - [ ] Xem cách kiểm tra checksum mật khẩu và cách chuyển đổi bits ngược lại thành chuỗi văn bản.

---

## 💻 3. Tái hiện bằng Python
- [ ] **Viết code đọc/ghi tệp WAV**: Sử dụng thư viện `soundfile` hoặc `wave` để đọc dữ liệu âm thanh dưới dạng mảng số thực hoặc số nguyên NumPy.
- [ ] **Viết hàm chuyển đổi dữ liệu**:
  - [ ] Viết hàm chuyển chuỗi văn bản ký tự (String) sang danh sách bits (`0` và `1`).
  - [ ] Viết hàm chuyển danh sách bits ngược lại thành chuỗi văn bản.
- [ ] **Triển khai bộ mã hóa LSB (Encoder)**:
  - [ ] Nhúng danh sách bits vào LSB của các mẫu âm thanh bằng toán tử bitwise `&` và `|`.
  - [ ] Lưu dữ liệu đã sửa đổi ra tệp WAV mới (`stego.wav`).
- [ ] **Triển khai bộ giải mã LSB (Decoder)**:
  - [ ] Đọc LSB từ các mẫu âm thanh của tệp `stego.wav`.
  - [ ] Trích xuất đủ số bit cần thiết để tái tạo lại tin nhắn văn bản gốc.

---

## 📊 4. Đánh giá kiểm chứng
- [ ] **Nghe thử cảm quan**: Nghe lại hai file âm thanh gốc và file stego để kiểm chứng tai người có phân biệt được không.
- [ ] **Tính toán định lượng**: Viết hàm tính chỉ số **SNR (Signal-to-Noise Ratio)** giữa tín hiệu gốc và tín hiệu stego để đánh giá độ trung thực của âm thanh sau khi giấu tin.
