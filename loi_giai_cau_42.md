# Lời giải Câu 42

**Đề bài:** Xét hàm số f(x) = ax^3 + bx^2 + cx + d (a, b, c, d thuộc R, a > 0) có hai điểm cực trị x1, x2 (với x1 < x2) thỏa mãn x1 + x2 = 0. Hình phẳng giới hạn bởi đường y = f'(x)f''(x) và trục hoành có diện tích bằng 9/16. Biết tích phân từ x1 đến x2 của f'(x)/(2^x + 1) dx = -5/2, giá trị của tích phân từ 0 đến x2 của (x + 2)f''(x) dx thuộc khoảng nào dưới đây?

A. (-9/2; -7/2)
B. (-3/2; -1/2)
C. (7/2; 9/2)
D. (1/2; 3/2)

---

**Lời giải chi tiết:**

Theo giả thiết, hàm số có hai điểm cực trị x1, x2 thỏa mãn x1 + x2 = 0.
Ta có đạo hàm:
f'(x) = 3ax^2 + 2bx + c
Đạo hàm bậc hai:
f''(x) = 6ax + 2b

Tổng hai nghiệm của phương trình f'(x) = 0 là:
x1 + x2 = -2b / (3a)
Vì x1 + x2 = 0 nên ta suy ra:
-2b / (3a) = 0  =>  b = 0

Khi đó:
f'(x) = 3ax^2 + c
f''(x) = 6ax

Đặt x2 = m (với m > 0), thì x1 = -m.
Vì x2 là cực trị nên f'(x2) = 0:
3a(m)^2 + c = 0  =>  c = -3am^2
(Vì a > 0 và m > 0 nên c < 0).

**Bước 1: Khai thác giả thiết diện tích hình phẳng**
Hàm số dưới dấu tích phân là:
y = f'(x)f''(x) = (3ax^2 + c)(6ax) = 18a^2x^3 + 6acx
Các giao điểm của y với trục hoành là nghiệm của y = 0:
x = 0, x = -m, x = m.
Vì y là hàm lẻ, đồ thị nhận gốc tọa độ O làm tâm đối xứng, nên diện tích hình phẳng trên đoạn [-m; 0] bằng diện tích trên đoạn [0; m].
Diện tích S giới hạn bởi y và trục hoành trên đoạn [-m; m] là:
S = 2 * tích phân từ 0 đến m của (-y) dx
(Ta lấy -y vì trên (0; m), 3ax^2 + c < 0 và 6ax > 0 nên y < 0).

Tính nguyên hàm:
Nguyên hàm của -y = -(18a^2x^3 + 6acx) là - (9/2)a^2x^4 - 3acx^2.
Tính tích phân từ 0 đến m:
S = 2 * [ - (9/2)a^2m^4 - 3acm^2 ]
Thay thế c = -3am^2, tức là am^2 = -c/3, ta có a^2m^4 = c^2 / 9:
S = 2 * [ - (9/2)(c^2 / 9) - 3c(-c/3) ]
S = 2 * [ - c^2 / 2 + c^2 ] = 2 * (c^2 / 2) = c^2.

Theo đề bài S = 9/16, suy ra:
c^2 = 9/16
Do c < 0 nên:
c = -3/4.

**Bước 2: Khai thác giả thiết tích phân của f'(x)/(2^x + 1)**
Gọi I = tích phân từ -m đến m của f'(x)/(2^x + 1) dx.
Do f'(x) = 3ax^2 + c là hàm số chẵn, ta áp dụng tính chất của tích phân:
tích phân từ -A đến A của g(x)/(k^x + 1) dx = tích phân từ 0 đến A của g(x) dx (với g(x) là hàm chẵn).
Do đó:
I = tích phân từ 0 đến m của f'(x) dx = tích phân từ 0 đến m của (3ax^2 + c) dx
I = [ ax^3 + cx ] từ 0 đến m = am^3 + cm = m(am^2 + c).

Từ c = -3am^2, suy ra am^2 = -c / 3. Thay vào I:
I = m( -c/3 + c ) = (2/3)cm.

Theo đề bài I = -5/2. Thay c = -3/4 vào:
(2/3) * (-3/4) * m = -5/2
- (1/2) * m = -5/2
=> m = 5.

Vậy x2 = 5.

**Bước 3: Tìm hệ số a và tính tích phân yêu cầu**
Từ am^2 = -c/3, ta có:
a * 5^2 = -(-3/4) / 3
25a = 1/4
=> a = 1/100.

Hàm f''(x) trở thành:
f''(x) = 6ax = 6(1/100)x = (3/50)x.

Giá trị của tích phân J = tích phân từ 0 đến x2 của (x + 2)f''(x) dx:
J = tích phân từ 0 đến 5 của (x + 2)(3/50)x dx
J = (3/50) * tích phân từ 0 đến 5 của (x^2 + 2x) dx
J = (3/50) * [ x^3 / 3 + x^2 ] từ 0 đến 5
J = (3/50) * ( 125/3 + 25 )
J = (3/50) * ( 125/3 + 75/3 )
J = (3/50) * ( 200/3 )
J = 200 / 50 = 4.

**Kết luận:**
Giá trị J = 4.
Ta thấy 4 thuộc khoảng (7/2; 9/2) tương ứng với đáp án C.

**Đáp án đúng là C.**
