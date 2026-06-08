# HƯỚNG DẪN TÍNH NHANH X^N MOD B (Thiết kế cho Thi tự luận & Trắc nghiệm)

Trong các đề thi Mật mã học và An toàn thông tin, việc tính số dư của luỹ thừa lớn `x^n mod b` xuất hiện liên tục (đặc biệt là trong hệ mật mã RSA, trao đổi khóa Diffie-Hellman). Dưới đây là các phương pháp tối ưu nhất để **giải tay nhanh** viết vào bài thi và **bấm máy tính Casio** cực tốc độ mà không lo bị tràn màn hình (Math Error).

---

> [!IMPORTANT]
> **QUY TRÌNH HỌC VÀ KIỂM CHỨNG BẮT BUỘC BẰNG PYTHON:**
> Khi giải bài tập ở nhà, để đảm bảo hiểu sâu bản chất thuật toán và không bị sai sót, bạn **bắt buộc** phải thực hiện quy trình sau:
> 1. **Tự viết Python kiểm chứng từng bước (Custom Script):** Với mỗi bước tính toán trung gian (ví dụ: in từng dòng của bảng Bình phương và Nhân, hoặc từng dòng của bảng Euclid mở rộng), bạn phải **tự viết mã Python** để mô phỏng và in ra kết quả từng bước. Việc này giúp đối chiếu chính xác xem mình tính toán nháp sai ở bước nào.
> 2. **Dùng thư viện chuẩn kiểm tra đáp số:** Sau khi tự code kiểm chứng từng bước, hãy dùng các hàm tối ưu hoặc thư viện chuẩn của Python (ví dụ: hàm built-in `pow(base, exp, mod)`, thư viện `sympy`) để kiểm tra lại xem kết quả cuối cùng có hoàn toàn chính xác hay không.

---

## 1. Phương pháp Giải Tay trong Bài thi Tự luận

Khi làm tự luận, bạn phải trình bày từng bước. Cách tốt nhất và chuyên nghiệp nhất là sử dụng **Thuật toán Bình phương và Nhân (Square-and-Multiply)** kết hợp với các định lý tối giản.

### Bước 1: Giảm số mũ n bằng các định lý toán học (Nếu có thể)
*   **Nếu b là số nguyên tố p** và `UCLN(x, p) == 1`: Áp dụng **Định lý Fermat nhỏ**:
    `x^(p-1) mod p == 1`
    Suy ra: `x^n mod p == x^(n mod (p-1)) mod p`
    
    *Ví dụ:* Tính `7^222 mod 11`. 
    Vì 11 là số nguyên tố nên `7^10 mod 11 == 1`.
    Ta có `222 mod 10 == 2`.
    Vậy `7^222 mod 11 == 7^2 mod 11 == 49 mod 11 == 5`. (Chỉ mất 5 giây!)

*   **Nếu b là hợp số (như n = p * q trong RSA)** và `UCLN(x, b) == 1`: Áp dụng **Định lý Euler**:
    `x^(phi(b)) mod b == 1`
    Suy ra: `x^n mod b == x^(n mod phi(b)) mod b`
    *(Trong đó phi(b) = (p-1) * (q-1) nếu b = p * q)*

### Bước 2: Trình bày thuật toán Bình phương và Nhân (Bình phương liên tiếp)
Nếu số mũ sau khi rút gọn vẫn lớn, ta phân tích số mũ `n` dưới dạng tổng các lũy thừa của 2 (hệ nhị phân).

**Ví dụ:** Tính `7^13 mod 15`.
1.  Phân tích số mũ: `13 = 8 + 4 + 1 = 2^3 + 2^2 + 2^0` (nhị phân là `1101`).
    Do đó: `7^13 = (7^8 * 7^4 * 7^1) mod 15`.
2.  Tính bình phương liên tiếp:
    *   `7^1 mod 15 == 7`
    *   `7^2 mod 15 == 49 mod 15 == 4` (vì 15 * 3 = 45, dư 4)
    *   `7^4 mod 15 == (7^2)^2 mod 15 == 4^2 mod 15 == 16 mod 15 == 1`
    *   `7^8 mod 15 == (7^4)^2 mod 15 == 1^2 mod 15 == 1`
3.  Nhân các kết quả tương ứng với số mũ phân tích được:
    `7^13 mod 15 == (7^8 * 7^4 * 7^1) mod 15 == (1 * 1 * 7) mod 15 == 7 mod 15 == 7`.

Trình bày bảng này vào bài thi sẽ được điểm tối đa:
| Số mũ lũy thừa 2 | Phép tính trung gian | Kết quả mod 15 | Có nhân vào kết quả không? |
| :--- | :--- | :--- | :--- |
| 2^0 = 1 | 7^1 | **7** | Có (vì số mũ 13 có thành phần 2^0) |
| 2^1 = 2 | 7^2 = 49 | 4 | Không |
| 2^2 = 4 | 4^2 = 16 | **1** | Có (vì số mũ 13 có thành phần 2^2) |
| 2^3 = 8 | 1^2 = 1 | **1** | Có (vì số mũ 13 có thành phần 2^3) |

Kết quả phép nhân cuối: `7 * 1 * 1 = 7 mod 15`.

---

## 2. Thủ thuật Bấm Máy tính Casio fx-580VN X (Không lo tràn bộ nhớ)

Dòng máy **Casio fx-580VN X** tích hợp sẵn chức năng chia lấy dư **`÷R`** rất mạnh mẽ. Dưới đây là các kỹ thuật thực tế bạn cần áp dụng.

### Cách A: Cách gõ ký hiệu `÷R` và tính trực tiếp (Cho số mũ nhỏ/vừa)
Ký hiệu `÷R` màu đỏ nằm ngay phía trên **phím phân số** (phím có biểu tượng hình vuông trên hình vuông nằm dưới phím SHIFT).

*   **Cách gõ phép toán A mod B:**
    1. Nhập số bị chia `A`.
    2. Nhấn nút **`ALPHA`** rồi nhấn **`Phím phân số`** (màn hình hiện ký hiệu **`÷R`**).
    3. Nhập số chia `B`.
    4. Nhấn nút **` = `**.
    *   *Màn hình hiển thị:* Dạng **`Q=... , R=...`**. Trong đó **`R`** chính là số dư (kết quả phép mod).

*   **Ví dụ:** Tính `13^5 mod 17`.
    *   Tính giá trị trước: `13^5 = 371293` (chưa vượt quá 10^15, máy tính xử lý được).
    *   Nhập vào máy: `371293` -> `ALPHA` -> `Phím phân số` -> `17` -> `=`.
    *   Kết quả trả về: `Q=21840, R=13`. Vậy `13^5 mod 17 == 13`.

---

### Cách B: Thuật toán Lặp Bình phương bằng phím `Ans` (Cho số mũ rất lớn)
Khi bạn cần tính `x^n mod b` với số mũ `n` lớn (ví dụ `n = 99, 100`), việc tính trực tiếp sẽ gây lỗi **`MATH ERROR`** (tràn màn hình). Hãy dùng thuật toán lặp bình phương để tính chuỗi: `x^1, x^2, x^4, x^8, x^16, x^32, x^64, ... mod b`.

*   **Quy trình bấm nút trên fx-580VN X:**
    1.  **Tính số dư đầu tiên `x mod b`:**
        *   Nhập: `x` -> `ALPHA` -> `Phím phân số` -> `b` -> `=`.
        *   Ví dụ tính `7^99 mod 15`: Nhập `7` -> `ALPHA` -> `Phím phân số` -> `15` -> `=`. Kết quả dư **`7`** (kết quả này tự động được lưu vào biến bộ nhớ tạm `Ans`).
    2.  **Thiết lập công thức lặp bình phương:**
        *   Nhấn nút xóa màn hình `AC`.
        *   Nhập phép toán: `Ans^2` -> `ALPHA` -> `Phím phân số` -> `b` (tức là `Ans^2 ÷R b`).
    3.  **Bấm nút `=` liên tiếp để lấy các kết quả lũy thừa 2:**
        *   Bấm **` = ` lần 1**: Kết quả là `7^2 mod 15 == 4`. (Lưu nháp: `7^2 == 4`)
        *   Bấm **` = ` lần 2**: Kết quả là `7^4 mod 15 == 1`. (Lưu nháp: `7^4 == 1`)
        *   Bấm **` = ` lần 3**: Kết quả là `7^8 mod 15 == 1`. (Lưu nháp: `7^8 == 1`)
        *   Bấm **` = ` lần 4**: Kết quả là `7^16 mod 15 == 1`. (Lưu nháp: `7^16 == 1`)
        *   Bấm **` = ` lần 5**: Kết quả là `7^32 mod 15 == 1`. (Lưu nháp: `7^32 == 1`)
        *   Bấm **` = ` lần 6**: Kết quả là `7^64 mod 15 == 1`. (Lưu nháp: `7^64 == 1`)
    4.  **Tổng hợp kết quả:**
        *   Tách số mũ: `99 = 64 + 32 + 2 + 1`.
        *   Nhân các số dư tương ứng lại:
            `7^99 mod 15 == (7^64 * 7^32 * 7^2 * 7^1) mod 15 == (1 * 1 * 4 * 7) mod 15 == 28 mod 15`
        *   Bấm tiếp phép dư cuối cùng: `28 ÷R 15` -> kết quả cuối cùng là **`13`**.

---

### Cách C: Phương pháp phân tích nhân tử số mũ (Tách lũy thừa tầng)
Nếu số mũ là một tích: `n = p1 * p2`. Ta dùng công thức `(x^p1)^p2 mod b`.

*   **Ví dụ:** Tính `3^50 mod 19`.
    *   Ta tách số mũ: `50 = 5 * 10`.
    *   Bước 1: Tính `3^5 mod 19`.
        *   Bấm: `3^5` -> `ALPHA` -> `Phím phân số` -> `19` -> `=`. Kết quả dư `15`.
    *   Bước 2: Thế kết quả `15` vào và tính `15^10 mod 19`.
        *   Tách tiếp `15^10 = (15^2)^5 mod 19`.
        *   Tính `15^2 mod 19`: Bấm `15^2` -> `ALPHA` -> `Phím phân số` -> `19` -> `=`. Kết quả dư `16`.
        *   Tính tiếp `16^5 mod 19`: Bấm `16^5` -> `ALPHA` -> `Phím phân số` -> `19` -> `=`. Kết quả dư `17`.
    *   **Kết luận:** `3^50 mod 19 == 17`.

---

## 3. Giải pháp cho số mũ cực kỳ lớn (Ví dụ: n = 65537 hoặc n lên tới hàng triệu)

Khi gặp các số mũ khổng lồ (thường gặp trong bài toán giải mã RSA hoặc chữ ký số), việc tính từng bước bình thường sẽ rất lâu. Ta áp dụng 2 bước chiến lược sau:

### Bước 1: Rút gọn số mũ bằng Định lý Euler/Fermat
Nếu đề bài cho số mũ `n` cực lớn, bạn **bắt buộc** phải rút gọn số mũ trước khi bấm máy:
1. Xác định mod `b`. Nếu `b` là tích hai số nguyên tố `p * q` (trong RSA), hãy tính `phi(b) = (p-1) * (q-1)`.
2. Nếu `UCLN(x, b) == 1`, ta luôn có: `x^n mod b == x^(n mod phi(b)) mod b`.
3. Bấm máy tính tìm số dư số mũ mới: `n ÷R phi(b)`. Lấy số dư này làm số mũ mới `n_moi`.

*   **Ví dụ thực tế:** Tính `123^987654321 mod 3233` (với `3233 = 61 * 53`).
    *   Tính `phi(3233) = (61-1) * (53-1) = 60 * 52 = 3120`.
    *   Rút gọn số mũ: Bấm `987654321 ÷R 3120` -> dư **`1521`**.
    *   Vậy bài toán quy về tính: `123^1521 mod 3233`. (Số mũ đã giảm từ gần 1 tỷ xuống còn 1521).

---

### Bước 2: Bấm máy tính nhanh cho số mũ sau rút gọn (ví dụ 1521)
Để tính `123^1521 mod 3233`:
1.  **Phân tích 1521 sang mã nhị phân:**
    *   Lũy thừa 2 gần nhất: `1521 = 1024 + 256 + 128 + 64 + 32 + 16 + 1`.
2.  **Bấm máy tính chuỗi bình phương liên tiếp bằng `Ans`:**
    *   Nhập: `123 ÷R 3233` -> `=` (Lưu `Ans = 123` ứng với `123^1`).
    *   Nhập tiếp công thức: `Ans^2 ÷R 3233`.
    *   Bấm phím **` = ` liên tiếp** để lấy các kết quả lũy thừa 2 tương ứng:
        *   **Lần 1 (123^2):** Dư `2197`
        *   **Lần 2 (123^4):** Dư `1222`
        *   **Lần 3 (123^8):** Dư `2482`
        *   **Lần 4 (123^16):** Dư **`1380`** (Cần lấy)
        *   **Lần 5 (123^32):** Dư **`2874`** (Cần lấy)
        *   **Lần 6 (123^64):** Dư **`3108`** (Cần lấy)
        *   **Lần 7 (123^128):** Dư **`256`** (Cần lấy)
        *   **Lần 8 (123^256):** Dư **`862`** (Cần lấy)
        *   **Lần 9 (123^512):** Dư `3108`
        *   **Lần 10 (123^1024):** Dư **`256`** (Cần lấy)
3.  **Nhân các số dư cần lấy lại với nhau (Nhân từng cặp một để tránh bị tràn màn hình):**
    *   Tính tích cặp 1: `123^1024 * 123^256 == 256 * 862 = 220672`. Bấm `220672 ÷R 3233` -> dư `834`.
    *   Nhân tiếp số dư này với `123^128`: `834 * 256 = 213504`. Bấm `213504 ÷R 3233` -> dư `126`.
    *   Nhân tiếp với `123^64`: `126 * 3108 = 391608`. Bấm `391608 ÷R 3233` -> dư `388`.
    *   Nhân tiếp với `123^32`: `388 * 2874 = 1115112`. Bấm `1115112 ÷R 3233` -> dư `2991`.
    *   Nhân tiếp với `123^16`: `2991 * 1380 = 4127580`. Bấm `4127580 ÷R 3233` -> dư `1968`.
    *   Nhân tiếp với số dư ban đầu `123^1`: `1968 * 123 = 242064`. Bấm `242064 ÷R 3233` -> dư **`2788`**.
    *   **Kết quả cuối cùng:** `123^987654321 mod 3233 == 2788`.

---

> [!TIP]
> **Mẹo phòng thi:**
> 1. Luôn ưu tiên dùng **Định lý Fermat nhỏ** hoặc **Euler** trước tiên để hạ số mũ xuống mức nhỏ nhất trước khi dùng Casio bấm máy.
> 2. Nếu tính tích cuối cùng của thuật toán bình phương và nhân mà số lớn, hãy nhân từng số rồi mod ngay tại chỗ để giữ cho các con số luôn nhỏ hơn `b`.
