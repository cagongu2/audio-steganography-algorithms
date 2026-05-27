# Lộ Trình Nghiên Cứu và Triển Khai Audio Steganography (Giấu Tin Trong Âm Thanh)

Tài liệu này là lộ trình học tập và nghiên cứu khoa học được thiết kế riêng theo phương pháp: **Hiểu lý thuyết thuật toán trước ➔ Phân tích cấu trúc code Matlab gốc ➔ Tái hiện từng phần sang Python ➔ Đánh giá thực nghiệm khoa học**.

---

## 🧭 Quy Trình Học Tập Cho Mỗi Thuật Toán
Để nắm vững bản chất khoa học và không bị ngợp bởi mã nguồn, đối với mỗi thuật toán bạn nên đi qua 4 bước sau:

```
┌────────────────────────┐     ┌────────────────────────┐
│  Bước 1: Hiểu Lý Thuyết │ ──> │ Bước 2: Đọc Code Matlab│
│   (Vật lý/Toán học)    │     │   (Phân tích luồng đi) │
└────────────────────────┘     └────────────────────────┘
                                            │
                                            ▼
┌────────────────────────┐     ┌────────────────────────┐
│   Bước 4: Kiểm Chứng   │ <── │ Bước 3: Code Python    │
│  (SNR, BER, Nghe thử)  │     │   (Tái hiện từng phần) │
└────────────────────────┘     └────────────────────────┘
```

---

## 🗺️ Lộ Trình Chi Tiết 5 Tuần

### 🗓️ Tuần 1: Nhập Môn & Triển Khai Thuật Toán LSB (Miền Thời Gian)
*   **Lý thuyết**:
    *   Tìm hiểu về âm thanh số: Tần số lấy mẫu (Sampling Rate), Độ phân giải (Bit Depth - 16-bit PCM), và cách lưu trữ dữ liệu dạng sóng (waveform) miền thời gian.
    *   Nguyên lý giấu tin LSB: Thay đổi bit ít quan trọng nhất để ẩn giấu dữ liệu mà không làm thay đổi cảm nhận âm thanh của tai người.
*   **Đọc cấu trúc code Matlab**:
    *   Phân tích cấu trúc tệp [lsb_enc.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/03-LSB-Coding/lsb_enc.m) và [lsb_dec.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/03-LSB-Coding/lsb_dec.m).
    *   Hiểu cách định vị các phân đoạn dữ liệu: 8 mẫu đầu làm Header kiểm tra, 40 mẫu tiếp theo lưu độ dài tin nhắn, các mẫu sau chứa dữ liệu mã hóa XOR.
*   **Tái hiện sang Python**:
    *   Triển khai đọc/ghi tệp WAV bằng thư viện `wave` hoặc `soundfile`.
    *   Tự code hàm chuyển đổi văn bản thành dãy bit và ngược lại.
    *   Triển khai toán tử bit (`&`, `|`, `~`) trong Python để thay đổi bit LSB.
*   **Kiểm chứng**:
    *   Nhúng thử một đoạn văn bản và trích xuất lại. Tính toán tỷ số tín hiệu trên nhiễu (**SNR**) để đo độ biến dạng tín hiệu.

### 🗓️ Tuần 2: Thuật Toán Echo Hiding (Giấu Tin Bằng Tiếng Vọng)
*   **Lý thuyết**:
    *   Hiện tượng che khuất thời gian (**Temporal Masking**): Tai người không phát hiện được tiếng vọng cực nhỏ nếu nó xuất hiện ngay sau âm thanh gốc một khoảng thời gian rất ngắn.
    *   Học cách mã hóa bit 0 bằng độ trễ $d_0$ (ví dụ: $150$ samples) và bit 1 bằng độ trễ $d_1$ (ví dụ: $200$ samples).
    *   Hiểu sự cần thiết của hàm trộn (Cross-fading Mixer) để làm mượt các điểm chuyển đổi giữa các khung chứa bit khác nhau.
*   **Đọc cấu trúc code Matlab**:
    *   Phân tích cấu trúc hàm [echo_enc_single.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/02-Echo-Hiding/01-Echo-Hiding-Single-Kernel/echo_enc_single.m) và hàm tạo bộ lọc trễ.
    *   Nghiên cứu cơ chế nội suy cửa sổ Hanning trong tệp [mixer.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/02-Echo-Hiding/01-Echo-Hiding-Single-Kernel/mixer.m).
*   **Tái hiện sang Python**:
    *   Triển khai bộ lọc trễ tạo tiếng vọng bằng `scipy.signal.lfilter` hoặc dịch chuyển mảng số trong NumPy.
    *   Tái hiện hàm `mixer` bằng tích chập `numpy.convolve` và cửa sổ Hanning `numpy.hanning`.
*   **Kiểm chứng**:
    *   Nghe thử âm thanh stego xem có nghe thấy tiếng vọng hoặc tiếng lách tách không.

### 🗓️ Tuần 3: Thuật Toán DSSS (Phổ Giãn Rộng Trực Tiếp)
*   **Lý thuyết**:
    *   Nguyên lý trải rộng phổ: Nhân bit thông tin $\{-1, 1\}$ với chuỗi nhiễu giả ngẫu nhiên (PN Sequence) tần số cao để biến thông tin thành một dạng "tiếng ồn nền" biên độ cực nhỏ phân bố đều trên dải tần.
    *   Nguyên lý giải mã thông qua tích vô hướng và tính chất trực giao của chuỗi ngẫu nhiên nhằm triệt tiêu tín hiệu nền của âm thanh gốc và khôi phục bit tin nhắn.
*   **Đọc cấu trúc code Matlab**:
    *   Nghiên cứu cách điều chế và nhúng tin trong [dsss_enc.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/01-Spread-Spectrum/01-DSSS-Conventional-Algorithm/dsss_enc.m) và giải mã trong `dsss_dec.m`.
    *   Hiểu cách tạo bộ sinh số giả ngẫu nhiên đồng bộ giữa bên gửi và nhận dựa trên khóa mật khẩu (seed).
*   **Tái hiện sang Python**:
    *   Sử dụng bộ sinh số ngẫu nhiên của NumPy (`numpy.random.default_rng`) có thiết lập seed tương thích.
    *   Triển khai phép toán nhân vector và tính tổng tích lũy bằng NumPy để tối ưu hóa hiệu năng giải mã.
*   **Kiểm chứng**:
    *   Đo đạc độ chính xác của việc phục hồi thông tin.

### 🗓️ Tuần 4: Thuật Toán Phase Coding (Mã Hóa Pha Miền Tần Số)
*   **Lý thuyết**:
    *   Biến đổi Fourier nhanh (FFT) để chuyển đổi tín hiệu từ miền thời gian sang miền tần số số phức.
    *   Sự kém nhạy cảm của tai người đối với sự thay đổi pha tuyệt đối.
    *   Cách mã hóa thông tin vào pha của khung âm thanh đầu tiên và điều chỉnh pha các khung sau để đảm bảo tính liên tục của dạng sóng.
*   **Đọc cấu trúc code Matlab**:
    *   Xem cách tác giả thực hiện biến đổi `fft()` trên từng khung tín hiệu trong [phase_enc.m](file:///e:/Cao%20h%E1%BB%8Dc/Ph%C6%B0%C6%A1ng%20ph%C3%A1p%20nghi%C3%AAn%20c%E1%BB%A9u%20khoa%20h%E1%BB%8Dc%20CNTT/code/audio-steganography-algorithms/04-Phase-Coding/phase_enc.m).
    *   Phân tích cách tái lập số phức từ biên độ và pha mới bằng toán học Euler.
*   **Tái hiện sang Python**:
    *   Sử dụng `numpy.fft.fft` và `numpy.fft.ifft`.
    *   Sử dụng `np.angle()` và `np.abs()` để xử lý pha và biên độ.
*   **Kiểm chứng**:
    *   Vẽ đồ thị phổ pha của âm thanh gốc và âm thanh stego để so sánh sự thay đổi pha.

### 🗓️ Tuần 5: Đánh Giá Thực Nghiệm Khoa Học & Viết Báo Cáo
*   **Xây dựng bộ kiểm thử tự động (Automation Test Pipeline)**:
    *   Viết mã Python tự động chạy cả 4 thuật toán trên một tập dữ liệu âm thanh mẫu (Dataset).
    *   Tính toán tự động: **SNR** (chất lượng âm thanh), **BER** (tỉ lệ lỗi bit), và **Capacity** (tốc độ nhúng tin - bps).
*   **Mô phỏng tấn công (Attacks)**:
    *   Viết code mô phỏng các kênh truyền lỗi: Thêm nhiễu trắng (AWGN), Bộ lọc thông thấp (Low-pass filter).
    *   Gọi công cụ ngoài (như `ffmpeg`) để nén file stego sang định dạng `.mp3` hoặc `.aac` với các mức bitrate khác nhau (128kbps, 192kbps).
    *   Chạy giải mã từ các file bị tấn công để vẽ biểu đồ so sánh độ bền vững (BER vs Attack Strength) của các thuật toán.
*   **Hoàn thiện báo cáo**:
    *   Tổng hợp các bảng biểu, đồ thị thực nghiệm để đưa vào báo cáo khoa học.

---

> [!NOTE]
> Lộ trình này sẽ giúp bạn tiếp cận từng bước một cách khoa học: đi từ cái dễ nhất (LSB) để quen cách xử lý file âm thanh trên Python, sau đó đi sâu vào xử lý tín hiệu nâng cao ở miền thời gian (Echo, DSSS), cuối cùng là miền tần số (Phase).
