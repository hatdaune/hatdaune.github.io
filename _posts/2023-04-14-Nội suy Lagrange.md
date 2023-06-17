---
layout: post
title:  "Nội suy Lagrange"
---

## 0x00 Giới thiệu 

Lần đầu tiên tôi quan tâm đến nội suy Lagrange là khi đọc bài viết của Trần Xuân Bách (fextivity) trên tạp chí VNOI 2023. Dạo gần đây, khi tình yêu dành cho toán sơ cấp trỗi dậy, tôi lại đi tìm tòi, khám phá những bài toán sơ cấp mà thuở cấp 3 tôi chưa được học nhiều hay chưa hề biết đến. 

## 0x01 Nội suy Lagrange 

Với mọi số tự nhiên $n \geq 0$ và tập $n + 1$ điểm $(x_1,y_1), (x_2,y_2), ..., (x_{n+1}, y_{n+1})$ với các điểm $x_i$ đôi một phân biệt. Tồn tại duy nhất đa thức $P(x)$ bậc $n$ thỏa mãn: $P(x_i) = y_i$ $\forall i, i = \overline{1,{n+1}}$ 

Đa thức $P$ sẽ được tách thành $n + 1$ đa thức con: 

$$ P = P_1 + P_2 + ... + P_{n+1} $$

Trong đó, các đa thức $P_i$ thỏa mãn: 
- $P_i(x_i) = y_i$
- $P_i(x_j) = 0$ $\forall i \neq j$

Công thức tổng quát để tính $P_i$ là: 

$$ P_i(x) = y_i \frac{x - x_1}{x_i - x_1} \frac{x - x_2}{x_i - x_2} ... \frac{x - x_{i-1}}{x_i - x_{i-1}} \frac{x - x_{i+1}}{x_i - x_{i+1}} ... \frac{x - x_{n+1}}{x_i - x_{n+1}}$$

$$ = y_i \prod_{i \neq j} \frac{x - x_j}{x_i - x_j} $$

Công thức tổng quát để tính $P$ là: 

$$ P(x) = y_1 \prod_{j \neq 1} \frac{x - x_j}{x_1 - x_j} + y_2 \prod_{j \neq 2} \frac{x - x_j}{x_2 - x_j} + ... + y_{n+1} \prod_{j \neq {n+1}} \frac{x - x_j}{x_{n+1} - x_j}$$

$$ = \displaystyle \sum_{i=1}^{n+1} y_i \prod_{j \neq i} \frac{x - x_j}{x_i - x_j}$$

**Bài toán 1.** Cho đa thức $f(x) \in R[x]$ có bậc là $n$ thỏa mãn các điều kiện sau: 

$$ f(0) = 0, f(1) = \frac 1 2, f(2) = \frac 2 3, ..., f(n) = \frac{n}{n+1}$$

Tính giá trị của $f(n+1)$.

**Bài giải.** 

Áp dụng công thức nội suy Lagrange với $n+1$ mốc nội suy $x_i = i,$ $\forall i = \overline{1, {n+1}}$, ta có: 

$$ f(x) = \displaystyle \sum_{i=0}^{n} f(i) \prod_{j \neq i} \frac{x - j}{i - j} = \displaystyle \sum_{i=0}^{n} \frac{i}{i+1} \prod_{j \neq i} \frac{x - j}{i - j}$$

Với $x = n+1$ 

$$f(n+1) = \displaystyle \sum_{i=0}^{n} \frac{i}{i+1} \prod_{j \neq i} \frac{n+1-j}{i - j}$$

Dễ thấy:

$$\prod_{j \neq i} \frac{n+1-j}{i - j} = \frac{(n+1)!}{(n+1-i)i!(n-i)!} (-1)^{n-i}$$

Vì vậy, 

$$ f(n+1) = \displaystyle \sum_{i=0}^{n} \frac{i}{i+1} \frac{(n+1)!}{(n+1-i)i!(n-i)!} (-1)^{n-i} = \displaystyle \sum_{i=0}^{n} (-1)^{n-i} i \frac{(n+1)!}{(n+1-i)!(i+1)!} = \frac{1}{n+2} \displaystyle \sum_{i=0}^{n} (-1)^{n-i} i C_{n+2}^{i+1} $$

**Bài toán 2. (IMO Shortlist 1981)** Cho đa thức $P(x) \in R[x]$ có $degP(x) = n$ thỏa mãn điều kiện:

$$ P(k) = \frac{1}{C_{n+1}^k}, \forall k = \overline{0, n}$$

Tính $P(n+1)$. 

**Bài giải.** 

Áp dụng công thức nội suy Lagrange với $n+1$ mốc nội suy $x_i = i,$ $\forall i = \overline{0,n}$, ta có: 

$$ P(x) = \displaystyle \sum_{i=0}^{n} \Bigg[ P(i) \prod_{j = 0\\j \neq i}^{n} \frac{x - x_j}{x_i - x_j}\Bigg] = \displaystyle \sum_{i=0}^{n} \Bigg[ \frac{1}{C_{n+1}^i} \prod_{j = 0\\j \neq i}^{n} \frac{x - j}{i - j}\Bigg]$$

Với $x=n+1$: 

$$ P(n+1) = \displaystyle \sum_{i=0}^{n} \Bigg[ \frac{1}{C_{n+1}^i} \prod_{j = 0\\j \neq i}^{n} \frac{n+1-j}{i - j} \Bigg]$$

$$ = \displaystyle \sum_{i=0}^{n} \Bigg[ \frac{1}{C_{n+1}^i i! (n-i)! (-1)^{n-i}} \prod_{j = 0\\j \neq i}^{n} \frac{n+1-j}{i - j} \Bigg]$$

$$ = \displaystyle \sum_{i=0}^{n} \Bigg[ \frac{n+1-i}{(n+1)! (-1)^{n-i}} \prod_{j = 0\\j \neq i}^{n} \frac{n+1-j}{i - j} \Bigg]$$

$$ = \displaystyle \sum_{i=0}^{n} \Bigg[ \frac{n+1-i}{(n+1)! (-1)^{n-i}} \frac{(n+1)!}{n+1-i} \Bigg] = \displaystyle \sum_{i=0}^{n} \frac{1}{(-1)^{n-i}}$$

Vậy với $n$ chẵn thì $P(n+1) = 1$ còn $n$ lẻ thì $P(n+1) = 0$. 