# Lời giải Câu 47

**Đề bài:** Cho hàm số f(x) = 2/x^3 + ln((x+3)/(x-3)). Có bao nhiêu số nguyên a thuộc (-vô cùng; 2100) thỏa mãn f(a - 2024) + f(6a - 27) >= 0?

A. 1807.
B. 288.
C. 2096.
D. 360.

---

**Lời giải chi tiết:**

**Bước 1: Tìm tập xác định và tính chẵn lẻ của hàm số**
Hàm số f(x) = 2/x^3 + ln((x+3)/(x-3)) xác định khi:
(x+3)/(x-3) > 0  <=>  x > 3 hoặc x < -3.
Tập xác định D = (-vô cùng; -3) hợp (3; +vô cùng).

Kiểm tra tính chẵn lẻ của hàm số f(x):
Với mọi x thuộc D, ta có -x cũng thuộc D.
f(-x) = 2/(-x)^3 + ln((-x+3)/(-x-3))
f(-x) = -2/x^3 + ln((-(x-3)) / (-(x+3)))
f(-x) = -2/x^3 + ln((x-3)/(x+3))
f(-x) = -2/x^3 - ln((x+3)/(x-3))
f(-x) = - (2/x^3 + ln((x+3)/(x-3))) = -f(x).
Vậy f(x) là hàm số lẻ.

**Bước 2: Xét chiều biến thiên của hàm số**
Tính đạo hàm f'(x):
f'(x) = -6/x^4 + ( (x-3) - (x+3) ) / (x-3)^2 * (x-3)/(x+3)
f'(x) = -6/x^4 - 6 / (x^2 - 9).

Với mọi x thuộc D, ta có x^2 > 9 nên x^2 - 9 > 0.
Do đó: 1/x^4 > 0 và 1/(x^2 - 9) > 0.
Suy ra f'(x) = -6 * (1/x^4 + 1/(x^2 - 9)) < 0 với mọi x thuộc D.
Hàm số f(x) nghịch biến trên từng khoảng xác định (-vô cùng; -3) và (3; +vô cùng).

Đồng thời, ta nhận xét về dấu của f(x):
- Trên khoảng (3; +vô cùng): x > 3 nên 2/x^3 > 0 và (x+3)/(x-3) > 1 => ln((x+3)/(x-3)) > 0. Do đó f(x) > 0.
- Trên khoảng (-vô cùng; -3): Do f(x) là hàm lẻ nên f(x) < 0.

**Bước 3: Giải bất phương trình f(u) + f(v) >= 0**
Đặt u = a - 2024 và v = 6a - 27.
Điều kiện: |u| > 3 và |v| > 3.
Bất phương trình đã cho trở thành:
f(u) + f(v) >= 0

Do tính chất dấu của hàm số đã phân tích ở trên, ta xét các trường hợp:

*Trường hợp 1:* Cả u và v cùng thuộc (-vô cùng; -3).
Khi đó f(u) < 0 và f(v) < 0, suy ra f(u) + f(v) < 0. (Không thỏa mãn)

*Trường hợp 2:* Cả u và v cùng thuộc (3; +vô cùng).
Khi đó f(u) > 0 và f(v) > 0, suy ra f(u) + f(v) > 0. (Luôn thỏa mãn)
Điều kiện là:
u > 3 => a - 2024 > 3 => a > 2027.
v > 3 => 6a - 27 > 3 => 6a > 30 => a > 5.
Kết hợp lại ta được a >= 2028.
Vì a thuộc khoảng (-vô cùng; 2100) nên 2028 <= a <= 2099.
Số giá trị nguyên của a trong trường hợp này là: 2099 - 2028 + 1 = 72.

*Trường hợp 3:* u thuộc (-vô cùng; -3) và v thuộc (3; +vô cùng).
Vì f(x) là hàm lẻ nên f(u) + f(v) >= 0 <=> f(v) >= -f(u) <=> f(v) >= f(-u).
Do u < -3 nên -u > 3. Như vậy cả v và -u đều thuộc khoảng (3; +vô cùng).
Trên khoảng này f(x) nghịch biến, nên:
f(v) >= f(-u) <=> v <= -u <=> u + v <= 0.
Điều kiện của trường hợp này là:
u < -3 => a - 2024 < -3 => a < 2021.
v > 3 => 6a - 27 > 3 => a > 5.
=> 6 <= a <= 2020.
Bất phương trình u + v <= 0 trở thành:
(a - 2024) + (6a - 27) <= 0
7a - 2051 <= 0
7a <= 2051
a <= 293.
Kết hợp điều kiện, ta có 6 <= a <= 293.
Số giá trị nguyên của a trong trường hợp này là: 293 - 6 + 1 = 288.

*Trường hợp 4:* u thuộc (3; +vô cùng) và v thuộc (-vô cùng; -3).
Điều kiện là:
u > 3 => a > 2027.
v < -3 => 6a < 24 => a < 4.
Hai điều kiện này mâu thuẫn nên trường hợp này không có giá trị nào của a thỏa mãn.

**Bước 4: Tổng hợp kết quả**
Tổng số giá trị nguyên của a thỏa mãn yêu cầu đề bài là:
72 + 288 = 360 (giá trị).

**Kết luận:**
Có 360 số nguyên a thỏa mãn.

**Đáp án đúng là D.**
