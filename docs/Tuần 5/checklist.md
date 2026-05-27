# 📋 Checklist Tuần 5: Đánh Giá Thực Nghiệm & Hoàn Thiện Báo Cáo

Mục tiêu tuần này tập trung vào khía cạnh khoa học của môn học: đánh giá định lượng các thuật toán đã triển khai dưới các đòn tấn công thực tế và tổng hợp số liệu để viết báo cáo khoa học.

---

## 🛠️ 1. Xây dựng Pipeline Đo Đạc Tự Động
- [ ] **Viết script tự động hóa (Batch testing)**:
  - [ ] Đọc một danh sách các tệp âm thanh WAV làm mẫu thử đầu vào (Dataset).
  - [ ] Tự động chạy tuần tự các thuật toán: LSB, Echo Hiding, DSSS, Phase Coding.
- [ ] **Triển khai các bộ chỉ số đo đạc**:
  - [ ] **SNR (Signal-to-Noise Ratio)**: Đánh giá chất lượng âm thanh stego.
  - [ ] **BER (Bit Error Rate)**: Đánh giá tỉ lệ lỗi bit khi khôi phục thông tin.
  - [ ] **Capacity (Dung lượng)**: Đo đạc số lượng bit giấu được trên một giây âm thanh (bps).

---

## ☣️ 2. Giả Lập Tấn Công (Robustness Attacks)
- [ ] **Triển khai đòn tấn công Thêm nhiễu**:
  - [ ] Viết hàm Python thêm nhiễu trắng Gauss (AWGN) với các mức cường độ khác nhau ($\sigma$) vào tệp stego.
- [ ] **Triển khai đòn tấn công Lọc tần số**:
  - [ ] Sử dụng bộ lọc Butterworth Low-pass trong thư viện `scipy.signal` để lọc bỏ các thành phần tần số cao của tệp stego.
- [ ] **Triển khai đòn tấn công Nén âm thanh**:
  - [ ] Sử dụng thư viện `pydub` (hoặc gọi lệnh `ffmpeg` thông qua module `subprocess`) để nén tệp stego sang định dạng MP3 với các bitrate khác nhau (128kbps, 192kbps, 320kbps), sau đó giải nén ngược lại WAV để trích xuất tin.

---

## 📈 3. Tổng Hợp Số Liệu & Vẽ Đồ Thị
- [ ] **Đo đạc và so sánh**:
  - [ ] Đo chỉ số SNR của cả 4 thuật toán trên cùng một file âm thanh và lưu kết quả vào bảng so sánh.
  - [ ] Đo tỉ lệ BER của các thuật toán tương ứng dưới các mức độ tấn công khác nhau.
- [ ] **Vẽ biểu đồ phân tích**:
  - [ ] Vẽ đồ thị dạng cột so sánh SNR của các thuật toán.
  - [ ] Vẽ biểu đồ đường biểu diễn sự thay đổi của BER khi cường độ nhiễu tăng dần (BER vs. Noise Level).
  - [ ] Vẽ biểu đồ đường biểu diễn sự thay đổi của BER đối với các bitrate nén MP3 khác nhau.

---

## 📝 4. Hoàn Thiện Báo Cáo Khoa Học
- [ ] **Cấu trúc lại báo cáo theo chuẩn khoa học**:
  - [ ] **Đặt vấn đề (Introduction)**: Lý do nghiên cứu giấu tin âm thanh, thách thức của thính giác người.
  - [ ] **Cơ sở lý thuyết (Background)**: Nguyên lý của các thuật toán LSB, Echo Hiding, DSSS, Phase Coding.
  - [ ] **Triển khai (Implementation)**: Kiến trúc hệ thống bằng Python, cách sử dụng các thư viện SciPy/NumPy.
  - [ ] **Thực nghiệm & Thảo luận (Experiments & Discussion)**: Trưng bày bảng so sánh SNR, BER, các biểu đồ phân tích dưới tác động của tấn công nén/nhiễu. Rút ra kết luận thuật toán nào có độ bền vững cao nhất, thuật toán nào có chất lượng âm thanh tốt nhất.
  - [ ] **Kết luận & Hướng phát triển (Conclusion & Future work)**.
