# Lời giải Câu 49

**Đề bài:** Xét hàm số bậc bốn y = f(x) có f(-1) = -5. Hàm số y = f'(x) đồng biến trên khoảng (-vô cùng; +vô cùng), f'(4) = 0 và f'(-1) = a. Có bao nhiêu số nguyên a thuộc (-100; 0) sao cho ứng với mỗi a, hàm số y = |f(x) + 5/x^2| có đúng 3 điểm cực trị thuộc khoảng (-1; +vô cùng)?

A. 9.
B. 10.
C. 90.
D. 89.

---

**Lời giải chi tiết:**

**Bước 1: Phân tích các tính chất của f(x)**
Theo giả thiết, f(x) là hàm số bậc bốn nên f'(x) là hàm số bậc ba và f''(x) là hàm số bậc hai.
Vì f'(x) đồng biến trên khoảng (-vô cùng; +vô cùng) nên đạo hàm của nó f''(x) >= 0 với mọi x thuộc R (và f''(x) = 0 tại hữu hạn điểm).
Điều này có nghĩa là f(x) là một hàm số lồi trên toàn trục số thực R.
Ta có f'(4) = 0. Do f'(x) đồng biến trên R, nên:
- Khi x < 4, f'(x) < 0 => f(x) nghịch biến.
- Khi x > 4, f'(x) > 0 => f(x) đồng biến.
Từ đó suy ra x = 4 là điểm cực tiểu duy nhất và cũng là giá trị nhỏ nhất của f(x) trên R.
Đồng thời, với mọi x thuộc (-1; 4), ta luôn có f(x) < f(-1) = -5. (Đặc biệt là trên khoảng (-1; 0) và (0; 4)).

**Bước 2: Phân tích hàm số g(x) = f(x) + 5/x^2**
Hàm số g(x) xác định trên (-1; +vô cùng) \ {0}, tức là trên hai khoảng (-1; 0) và (0; +vô cùng).
Đạo hàm cấp một của g(x):
g'(x) = f'(x) - 10/x^3
Đạo hàm cấp hai của g(x):
g''(x) = f''(x) + 30/x^4
Do f''(x) >= 0 và 30/x^4 > 0 với mọi x khác 0, nên g''(x) > 0 trên (-1; 0) và trên (0; +vô cùng).
Suy ra g'(x) đồng biến trên từng khoảng (-1; 0) và (0; +vô cùng).
Và g(x) là hàm lồi trên từng khoảng (-1; 0) và (0; +vô cùng).

**Bước 3: Xét số điểm cực trị của |g(x)| trên (0; +vô cùng)**
Trên khoảng (0; +vô cùng):
- Khi x tiến tới 0+, 5/x^2 tiến tới +vô cùng, f(x) có giới hạn hữu hạn nên g(x) tiến tới +vô cùng.
- Khi x tiến tới +vô cùng, f(x) tiến tới +vô cùng (do hàm bậc bốn có a > 0), nên g(x) tiến tới +vô cùng.
Tại x = 4, ta có:
g(4) = f(4) + 5/4^2 = f(4) + 5/16.
Vì f(4) < f(-1) = -5 nên g(4) < -5 + 5/16 < 0.
Vì g(x) lồi, có giới hạn tiến tới +vô cùng ở hai đầu mút và có một điểm mang giá trị âm, nên đồ thị g(x) sẽ cắt trục hoành tại đúng 2 điểm phân biệt và có đúng 1 điểm cực tiểu (nằm dưới trục hoành) trên (0; +vô cùng).
Khi lấy trị tuyệt đối, y = |g(x)| trên khoảng (0; +vô cùng) sẽ có:
Số điểm cực trị của |g(x)| = (Số điểm cực trị của g(x)) + (Số giao điểm của g(x) với trục hoành).
Số điểm cực trị của |g(x)| = 1 + 2 = 3 (điểm).

**Bước 4: Xét số điểm cực trị của |g(x)| trên (-1; 0)**
Yêu cầu bài toán là hàm số y = |g(x)| có ĐÚNG 3 điểm cực trị trên khoảng (-1; +vô cùng).
Vì trên khoảng (0; +vô cùng) hàm số đã có sẵn 3 điểm cực trị, nên trên khoảng (-1; 0) hàm số |g(x)| KHÔNG ĐƯỢC CÓ điểm cực trị nào.
Ta phân tích g(x) trên khoảng (-1; 0):
- Tại x = -1, ta có:
g(-1) = f(-1) + 5/(-1)^2 = -5 + 5 = 0.
- Khi x tiến tới 0-, g(x) tiến tới +vô cùng.
Để |g(x)| không có điểm cực trị trên khoảng (-1; 0), thì g(x) không được đổi chiều biến thiên và cũng không được đổi dấu trên khoảng này (vì nếu g(x) vòng xuống tạo cực trị, hoặc cắt qua 0, khi lấy trị tuyệt đối sẽ sinh ra điểm cực trị).
Do g(-1) = 0 và g(0-) = +vô cùng, điều kiện cần và đủ để |g(x)| không có cực trị là g(x) phải đồng biến và lớn hơn 0 trên toàn bộ khoảng (-1; 0).
Điều này tương đương với g'(x) >= 0 với mọi x thuộc (-1; 0).
Vì g'(x) đồng biến trên khoảng (-1; 0) (do g''(x) > 0), nên giá trị nhỏ nhất của g'(x) trên nửa khoảng [-1; 0) đạt tại x = -1.
Vậy điều kiện là:
g'(-1) >= 0

Ta tính g'(-1):
g'(-1) = f'(-1) - 10/(-1)^3 = a - (-10) = a + 10.
Do đó:
a + 10 >= 0
=> a >= -10.

**Bước 5: Tìm số các giá trị nguyên của a**
Theo giả thiết, a là số nguyên thuộc khoảng (-100; 0).
Kết hợp với điều kiện a >= -10, ta có các giá trị:
a thuộc {-10, -9, -8, -7, -6, -5, -4, -3, -2, -1}.
Tổng cộng có 10 giá trị của a thỏa mãn bài toán.

**Kết luận:**
Có 10 số nguyên a thỏa mãn.
Đáp án đúng là B.
