# CẨM NANG TRÌNH BÀY BÀI THI MẬT MÃ HỌC & AN TOÀN THÔNG TIN

Tài liệu này hướng dẫn cách tư duy, giải quyết và trình bày tự luận chuẩn mực khi gặp các dạng bài toán số lớn, số nguyên tố, căn nguyên thủy, hệ mật ElGamal và chữ ký số.

---

> [!IMPORTANT]
> **QUY TRÌNH HỌC VÀ KIỂM CHỨNG BẮT BUỘC BẰNG PYTHON:**
> Khi giải bài tập ở nhà, để đảm bảo hiểu sâu bản chất thuật toán và không bị sai sót, bạn **bắt buộc** phải thực hiện quy trình sau:
> 1. **Tự viết Python kiểm chứng từng bước (Custom Script):** Với mỗi bước tính toán trung gian (ví dụ: in từng dòng của bảng Bình phương và Nhân, hoặc từng dòng của bảng Euclid mở rộng), bạn phải **tự viết mã Python** để mô phỏng và in ra kết quả từng bước. Việc này giúp đối chiếu chính xác xem mình tính toán nháp sai ở bước nào.
> 2. **Dùng thư viện chuẩn kiểm tra đáp số:** Sau khi tự code kiểm chứng từng bước, hãy dùng các hàm tối ưu hoặc thư viện chuẩn của Python (ví dụ: hàm built-in `pow(base, exp, mod)`, thư viện `sympy`) để kiểm tra lại xem kết quả cuối cùng có hoàn toàn chính xác hay không.
> 3 sau khi xong cũng phải chạy python kiểm tra kết quả
---

> [!IMPORTANT]
> **LƯU Ý ĐẶC BIỆT QUAN TRỌNG VỀ CÁCH VIẾT CÔNG THỨC TOÁN HỌC:**
> 1. **Viết công thức chữ tổng quát trước, thay số sau:** Khi làm bài thi tự luận, ở mọi bước tính toán, bạn **bắt buộc** phải ghi công thức tổng quát bằng ký tự chữ trước (ví dụ: viết `S = m^d mod n` hoặc `S2 = ((m - d * S1) * k^(-1)) mod (p-1)`), sau đó mới xuống dòng thay số vào để tính. 
> 2. **Giải thích các ký hiệu:** Đảm bảo ghi rõ các biến phụ nếu tự chọn (ví dụ: "Chọn số ngẫu nhiên k sao cho...").
> 3. **Tránh mất điểm oan:** Nếu bạn chỉ thay số và tính ra kết quả ngay mà không ghi công thức chữ, giảng viên chấm thi có thể nghi ngờ sao chép bài hoặc trừ 50% đến 100% số điểm của bước đó, ngay cả khi kết quả số của bạn hoàn toàn đúng!

---

## MỤC LỤC
1. [Xử lý Modulo Lớn & Rút gọn số mũ](#1-xử-lý-modulo-lớn--rút-gọn-số-mũ)
2. [Số Nguyên Tố & Căn Nguyên Thủy (Primitive Root)](#2-số-nguyên-tố--căn-nguyên-thủy-primitive-root)
3. [Quy trình giải & Trình bày Hệ mật ElGamal](#3-quy-trình-giải--trình-bày-hệ-mật-elgamal)
4. [Quy trình giải & Trình bày Chữ ký số (RSA & ElGamal)](#4-quy-trình-giải--trình-bày-chữ-ký-số-rsa--elgamal)
5. [Cạm bẫy phòng thi cần tránh](#5-cạm-bẫy-phòng-thi-cần-tránh)
6. [Phương pháp học & Kiểm tra bài tập bằng Python](#6-phương-pháp-học--kiểm-tra-bài-tập-bằng-python)

---

## 1. XỬ LÝ MODULO LỚN & RÚT GỌN SỐ MŨ

Khi gặp biểu thức `A^B mod M` với số mũ `B` rất lớn, tuyệt đối KHÔNG tính trực tiếp. Trình bày tự luận theo các bước sau:

### Bước 1: Kiểm tra tính nguyên tố của Modulo M
*   **Trường hợp 1: M là số nguyên tố p**
    *   Áp dụng Định lý Fermat nhỏ: Nếu `UCLN(A, p) == 1` thì `A^(p-1) mod p == 1`.
    *   Công thức rút gọn số mũ: 
        *   `B_moi = B mod (p-1)`
        *   `A^B mod p == A^(B_moi) mod p`
*   **Trường hợp 2: M là hợp số (Ví dụ: M = p * q trong RSA)**
    *   Áp dụng Định lý Euler: Nếu `UCLN(A, M) == 1` thì `A^(phi(M)) mod M == 1`.
    *   Tính phi hàm Euler: `phi(M) = (p-1) * (q-1)`.
    *   Công thức rút gọn số mũ:
        *   `B_moi = B mod phi(M)`
        *   `A^B mod M == A^(B_moi) mod M`

### Mẫu trình bày trong bài thi:
> **Đề bài:** Tính `7^2026 mod 11`.
>
> **Lời giải:**
> Vì 11 là số nguyên tố và `UCLN(7, 11) == 1`, áp dụng Định lý Fermat nhỏ ta có:
> `7^(11-1) mod 11 == 7^10 mod 11 == 1`
> Ta rút gọn số mũ: `2026 mod 10 == 6`.
> Do đó:
> `7^2026 mod 11 == 7^6 mod 11`
> Tiếp tục tính `7^6 mod 11` (Sử dụng bảng Bình phương và Nhân hoặc tính tách lũy thừa):
> *   `7^2 = 49 == 5 (mod 11)`
> *   `7^4 = (7^2)^2 == 5^2 = 25 == 3 (mod 11)`
> *   `7^6 = 7^4 * 7^2 == 3 * 5 = 15 == 4 (mod 11)`
>
> **Kết luận:** `7^2026 mod 11 == 4`.

---

## 2. SỐ NGUYÊN TỐ & CĂN NGUYÊN THỦY (PRIMITIVE ROOT)

Trong hệ mật ElGamal và trao đổi khóa Diffie-Hellman, đề bài luôn yêu cầu chọn hoặc chứng minh `alpha` là căn nguyên thủy của số nguyên tố `p`.

### Định nghĩa & Điều kiện cần và đủ:
Số `alpha` là căn nguyên thủy của `p` nếu và chỉ nếu bậc của `alpha` modulo `p` bằng `p-1`.
*   **Cách kiểm tra nhanh đi thi:**
    1. Tìm tất cả các ước nguyên tố của `p-1`. Gọi các ước đó là `q1, q2, ..., qk`.
    2. Tính các lũy thừa: `A_i = alpha^((p-1) / q_i) mod p` với mọi ước `q_i`.
    3. **Kết luận:** Nếu tất cả các kết quả `A_i` đều KHÁC `1 (mod p)`, thì `alpha` là căn nguyên thủy của `p`.

### Mẫu trình bày trong bài thi:
> **Đề bài:** Chứng minh `alpha = 2` là căn nguyên thủy của `p = 11`.
>
> **Lời giải:**
> Ta có `p - 1 = 10`. Các ước nguyên tố của 10 là `q1 = 2` và `q2 = 5`.
> Ta tính các lũy thừa tương ứng modulo 11:
> *   Với `q1 = 2`: Lũy thừa cần tính là `2^((11-1) / 2) mod 11 == 2^5 mod 11 == 32 mod 11 == 10` (Khác 1).
> *   Với `q2 = 5`: Lũy thừa cần tính là `2^((11-1) / 5) mod 11 == 2^2 mod 11 == 4` (Khác 1).
>
> Vì cả hai kết quả đều khác 1 (mod 11), ta kết luận `alpha = 2` là căn nguyên thủy của `p = 11`.

---

## 3. QUY TRÌNH GIẢI & TRÌNH BÀY HỆ MẬT ELGAMAL

Khi giải bài toán ElGamal tự luận, bạn cần chia rõ thành 3 giai đoạn lớn và viết đầy đủ các công thức tổng quát trước khi thay số.

### Bước 1: Giai đoạn Tạo khóa (Key Generation)
*   **Công thức:** Chọn khóa bí mật `d`, tính khóa công khai `beta = alpha^d mod p`.
*   **Trình bày:** Ghi rõ bộ khóa:
    *   Khóa công khai: `PU = {p, alpha, beta}`
    *   Khóa bí mật: `PR = {d}`

### Bước 2: Giai đoạn Mã hóa (Encryption)
*   **Công thức:** Bản mã `C = (y1, y2)` của thông điệp `m` với số ngẫu nhiên `k` là:
    *   `y1 = alpha^k mod p`
    *   `y2 = (m * beta^k) mod p`
*   **Trình bày:** Lập bảng Bình phương và Nhân tính riêng từng lũy thừa `alpha^k mod p` và `beta^k mod p` nếu số mũ lớn.

### Bước 3: Giai đoạn Giải mã (Decryption)
*   **Công thức:**
    *   `m = (y2 * (y1^d)^(-1)) mod p`
*   **Trình bày:**
    1. Tính giá trị trung gian: `A = y1^d mod p` (dùng bảng Bình phương và Nhân).
    2. Tìm nghịch đảo modulo: `A^(-1) mod p` (lập bảng Euclid mở rộng).
    3. Thực hiện phép nhân cuối cùng: `m = (y2 * A^(-1)) mod p`.

---

## 4. QUY TRÌNH GIẢI & TRÌNH BÀY CHỮ KÝ SỐ (RSA & ELGAMAL)

### A. Chữ ký số RSA
*   **Ký thông điệp m:**
    *   Công thức: `S = m^d mod n`.
    *   Trình bày: Lập bảng tính nghịch đảo tìm `d = e^(-1) mod phi(n)` (nếu đề bài chưa cho `d`). Kẻ bảng Bình phương và Nhân tính `S`.
*   **Xác thực chữ ký S:**
    *   Công thức: Tính `V = S^e mod n`.
    *   So sánh: Đối chiếu `V` với `m`. Nếu `V == m`, kết luận chữ ký hợp lệ.

### B. Chữ ký số ElGamal (Trọng tâm thi)
Hệ chữ ký số ElGamal yêu cầu sự chính xác cao độ về mặt modulo.

*   **Quy trình Ký (Signing):**
    1.  Chọn khóa tạm thời ngẫu nhiên `k` thỏa mãn: `UCLN(k, p-1) == 1`.
    2.  Tính thành phần chữ ký thứ nhất:
        `S1 = alpha^k mod p`
    3.  Tính thành phần chữ ký thứ hai:
        `S2 = ((m - d * S1) * k^(-1)) mod (p-1)`
        *(Lưu ý: Modulo p-1 chứ không phải p)*
        *Trình bày tự luận:*
        *   Tìm `k^(-1) mod (p-1)` bằng cách lập bảng Euclid mở rộng.
        *   Nếu tử số `(m - d * S1)` âm, ta biến đổi bằng cách cộng thêm bội của `(p-1)` cho đến khi ra số dương:
            `Tu_so_duong = (m - d * S1) + (p-1) * h` (với h là số nguyên phù hợp).
    4.  Kết luận: Chữ ký là cặp `(S1, S2)`.

*   **Quy trình Xác thực (Verification):**
    1.  Kiểm tra điều kiện biên: `0 < S1 < p` và `0 < S2 < (p-1)`. (Bắt buộc phải viết dòng này vào bài thi).
    2.  Tính vế trái:
        `V1 = (beta^S1 * S1^S2) mod p`
    3.  Tính vế phải:
        `V2 = alpha^m mod p`
    4.  So sánh: Nếu `V1 == V2 (mod p)`, chữ ký được chấp nhận.

---

## 5. CẠM BẪY PHÒNG THI CẦN TRÁNH

> [!CAUTION]
> **1. Nhầm lẫn Modulo p và Modulo (p-1) trong ElGamal**
> *   Mọi phép tính liên quan đến **số mũ** hoặc **chữ ký S2** đều thực hiện trên **modulo p-1** (hoặc phi(n) trong RSA).
> *   Mọi phép tính liên quan đến **cơ số** (phép nhân bản rõ, bản mã, tính toán khóa công khai beta, vế xác thực V1, V2) đều thực hiện trên **modulo p** (hoặc n).
> *   *Nhớ quy tắc:* **Dưới đất dùng p (cơ số), trên trời dùng p-1 (số mũ)**.

> [!WARNING]
> **2. Tìm nghịch đảo modulo của số âm**
> *   Trong bảng Euclid mở rộng, kết quả cuối cùng ở cột y có thể bị âm (Ví dụ: `y = -367`).
> *   Lỗi thường gặp là lấy luôn số âm đó làm kết quả. Bạn phải cộng thêm số modulo m:
>   `y_duong = y_am + m`

> [!IMPORTANT]
> **3. Thiếu điều kiện nguyên tố cùng nhau**
> *   Khi chọn khóa tạm thời `k` trong mã hóa ElGamal hoặc chữ ký số, bạn bắt buộc phải ghi câu lập luận: **"Chọn số ngẫu nhiên k sao cho UCLN(k, p-1) == 1"**. Nếu chọn `k` không thỏa mãn điều kiện này, bạn sẽ không thể tìm được `k^(-1)` để ký.

---

## 6. PHƯƠNG PHÁP HỌC & KIỂM TRA BÀI TẬP BẰNG PYTHON

Để đảm bảo kết quả làm bài tập tự luận của bạn chính xác 100%, tôi đã viết sẵn công cụ bằng Python tại tập tin [kiem_tra_ket_qua.py](file:///C:/Users/trung/Desktop/aigiaibaithi/kiem_tra_ket_qua.py).

Quy trình tự động hóa kiểm chứng gồm 2 bước:
1. **Bước 1: Giả lập thuật toán tự luận (Custom Solver)**: In ra từng bước lập bảng nháp của bạn (bảng Bình phương & Nhân, bảng Euclid mở rộng). Bạn chỉ cần đối chiếu xem mình tính nháp sai ở hàng nào.
2. **Bước 2: Sử dụng thư viện chuẩn (Library Check)**: Chương trình tự động gọi các hàm tính toán tối ưu built-in của Python để đưa ra đáp án chính xác nhất và xác minh xem giải thuật từng bước của bạn có khớp với kết quả chính xác không.

### Cách sử dụng để tự ôn tập:
1. Mở tập tin [kiem_tra_ket_qua.py](file:///C:/Users/trung/Desktop/aigiaibaithi/kiem_tra_ket_qua.py).
2. Kéo xuống phần `if __name__ == "__main__":` ở cuối file.
3. Thay đổi các tham số đầu vào (cơ số, số mũ, modulo, v.v.) bằng đề bài tập bạn cần giải.
4. Chạy file bằng cách mở terminal trong thư mục và gõ:
   `python kiem_tra_ket_qua.py`
5. Chương trình sẽ in ra bảng nháp chi tiết để bạn chép vào vở thi và thông báo `[ĐÚNG ✔]` hoặc `[SAI ❌]` tương ứng.

