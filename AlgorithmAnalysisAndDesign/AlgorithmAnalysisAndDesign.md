## Anali

## Class 1

### Big-O Notation - formal definition



![image-20230306131317227](C:\Users\96514\AppData\Roaming\Typora\typora-user-images\image-20230306131317227.png)

$g(n)$ is one of the functions: $1, \log{n}, n, n\log{n}, n^2 , n^3 , \cdots, 2^n , n! $

$O(\log{n}) < O(\log^2{n}) < O(\sqrt{n}) < O(n) < O(n\log{n}) < O(n^2) < O(2^n) < O(n!)$

$f(n) \in \Omega(g(n)) $



| Expression       | Definition                                                   | Relative  Growth |
| ---------------- | ------------------------------------------------------------ | ---------------- |
| $T(N)=O(F(N))$   | $\exist c > 0, \exist n_0 ≥ 0,\forall n ≥ n_0 : f(n) ≤ cg(n) $ | T(N)  ≤F(N)      |
| $T(N)=Ω(F(N))  $ | $\exist c > 0, \exist n_0 ≥ 0,\forall n ≥ n_0 : f(n) \geq cg(n) $ | T(N)  ≥ F(N)     |
| $T(N)=Θ(F(N))  $ | $\exist c_1 > 0, \exist c_2 > 0, \exist n_0 ≥ 0,\forall n ≥ n_0 :c_1 g(n) \geq f(n) \geq c_2 g(n) $ | T(N)  =  F(N)    |
| $T(N)=o(F(N))  $ | $\exist c > 0, \exist n_0 ≥ 0,\forall n ≥ n_0 : f(n) < cg(n) $ | T(N)  ＜F(N)     |





## Chapter 3

