# 📋 Checklist Tuần 2: Thuật Toán Echo Hiding (Giấu Tin Bằng Tiếng Vọng)

Mục tiêu tuần này là hiểu lý thuyết che khuất thời gian của tai người, phân tích cách Matlab thực hiện tạo tiếng vọng trễ thông qua bộ lọc, và tái hiện thuật toán Echo Hiding sang Python.

---

## 🔬 1. Lý thuyết & Nguyên lý
- [ ] **Tìm hiểu hiện tượng che khuất thời gian (Temporal Masking)**: 
  - [ ] Hiểu lý do tại sao tai người không phân biệt được âm vọng (echo) biên độ nhỏ khi nó cực kỳ gần tín hiệu gốc (độ trễ < 2-5 ms).
- [ ] **Tìm hiểu nguyên lý mã hóa Echo**:
  - [ ] Cách biểu diễn bit 0 bằng độ trễ $d_0$ (ví dụ: 150 mẫu ~ 3.4ms).
  - [ ] Cách biểu diễn bit 1 bằng độ trễ $d_1$ (ví dụ: 200 mẫu ~ 4.5ms).
  - [ ] Hiểu vai trò của biên độ vọng $\alpha$ đối với tính ẩn (imperceptibility) và độ bền vững (robustness).
- [ ] **Tìm hiểu cơ chế bộ trộn Cross-fading (Mixer)**:
  - [ ] Hiểu tại sao sự chuyển tiếp đột ngột giữa các khung bit 0 và 1 gây tiếng lách tách (click noise).
  - [ ] Hiểu cơ chế làm mượt đường ranh giới chuyển tiếp bằng cách tích chập chuỗi bit mở rộng với cửa sổ Hanning.

---

## 🔎 2. Phân tích mã nguồn Matlab gốc
- [ ] **Đọc hiểu tệp mã nguồn Matlab [echo_enc_single.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/02-Echo-Hiding/01-Echo-Hiding-Single-Kernel/echo_enc_single.m)**:
  - [ ] Xem cách tác giả định nghĩa nhân tiếng vọng `k0` và `k1`.
  - [ ] Tìm hiểu cơ chế lọc tín hiệu gốc bằng hàm `filter()` của Matlab để tạo tiếng vọng.
  - [ ] Xem cơ chế trộn tín hiệu stego bằng công thức: `out = signal + echo_zro * (1-mix) + echo_one * mix`.
- [ ] **Đọc hiểu tệp mã nguồn Matlab [mixer.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/02-Echo-Hiding/01-Echo-Hiding-Single-Kernel/mixer.m)**:
  - [ ] Tìm hiểu hàm tự viết `hanning()` và hàm tích chập `conv()`.
  - [ ] Xem cách chuẩn hóa năng lượng sau khi tích chập.

---

## 💻 3. Tái hiện bằng Python
- [ ] **Triển khai bộ lọc tiếng vọng trong Python**:
  - [ ] Sử dụng `scipy.signal.lfilter` để lọc tín hiệu qua nhân tiếng vọng, hoặc tự viết dịch mảng số học bằng NumPy.
- [ ] **Triển khai hàm bộ trộn (Mixer) trong Python**:
  - [ ] Sử dụng hàm tích chập `numpy.convolve` kết hợp cửa sổ Hanning `numpy.hanning` để tạo chuỗi trọng số chuyển tiếp mịn.
- [ ] **Triển khai bộ mã hóa Echo Hiding (Encoder)**:
  - [ ] Chia tín hiệu âm thanh đầu vào thành các khung kích thước $L$ (ví dụ: 8192).
  - [ ] Tạo tín hiệu stego bằng cách cộng trộn mềm tín hiệu trễ $d_0$ và $d_1$ dựa trên chuỗi bit tin nhắn.
- [ ] **Triển khai bộ giải mã Echo Hiding (Decoder)**:
  - [ ] Nghiên cứu thuật toán giải mã tiếng vọng (dựa trên phép tính tự tương quan Cepstrum - Cepstral Analysis).
  - [ ] Trích xuất các bit cực trị từ phổ Cepstrum của từng khung để khôi phục tin nhắn gốc.

---

## 📊 4. Đánh giá kiểm chứng
- [ ] **Nghe thử cảm quan**: Kiểm tra xem âm thanh stego có bị lách tách ở các đoạn chuyển tiếp bit hay không.
- [ ] **Đo đạc chất lượng**: Tính toán chỉ số SNR giữa file gốc và file stego.
