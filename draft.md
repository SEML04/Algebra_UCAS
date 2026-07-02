# Q1

设 `f: A -> B` 是 flat homomorphism，那么下行定理是否成立？

## 判定

成立。

## 解答

这正是 flat ring homomorphism 的基本性质之一：

> 若 `A -> B` 是平坦环同态，则诱导谱映射
> `Spec(B) -> Spec(A)`
> 满足 going-down。

也就是说，若

```math
\mathfrak p_1 \subseteq \mathfrak p_2 \in \operatorname{Spec} A,
\qquad
\mathfrak q_2 \in \operatorname{Spec} B,
\qquad
\mathfrak q_2 \cap A = \mathfrak p_2,
```

则存在

```math
\mathfrak q_1 \subseteq \mathfrak q_2
```

使得

```math
\mathfrak q_1 \cap A = \mathfrak p_1.
```

在 `Algebra III` 第 3 章 flatness 部分，这就是一个标准定理。  
因此这道题的答案是：**对，flat 推出 going-down**。

---

# Q2

设 `\hat A` 是 `A` 的 `I`-completion，记

```math
f: A \to \hat A
```

为典范映射。那么

```math
\operatorname{Spec}\hat A \to \operatorname{Spec}A
```

总是满射吗？

## 判定

不总是。

## 解答

若 `A` 是 Noether 环，则 `A -> \hat A` 是 flat；但谱映射满射对应的是更强的 **faithfully flat**，而 completion 一般未必 faithfully flat。

一个标准反例是：

```math
A=\mathbb Z,\qquad I=(2),\qquad \hat A=\mathbb Z_2.
```

此时

```math
\operatorname{Spec}(\mathbb Z_2)=\{(0),(2)\},
```

而

```math
\operatorname{Spec}(\mathbb Z)
```

里还有 `(3),(5),...` 等素理想。典范映射

```math
\operatorname{Spec}(\mathbb Z_2)\to \operatorname{Spec}(\mathbb Z)
```

的像只有

```math
\{(0),(2)\},
```

显然不是满射。

所以：**`Spec(\hat A) -> Spec(A)` 不总满射。**

补充一句：若 `I \subseteq Jac(A)` 且在 Noether 情形下，则 completion 常常是 faithfully flat，这时谱映射才会满射。

---

# Q3

设 `A` 是一个环，`f: A^m -> A^n`。

- 若 `f` 是满射，`m,n` 之间有什么关系？
- 若 `f` 是单射呢？

Idea3: 是否都应有 `m=n`？因为自由模都是投射模和内射模？

## 判定

`Idea3` 不对。

- 对一般环，若不加条件，未必能推出简单的 `m,n` 关系。
- 对交换环（或更一般有 `IBN` 的环），有：
  - 满射 `A^m -> A^n` 必有 `m >= n`；
  - 单射 `A^m -> A^n` 必有 `m <= n`。

## 解答

### 1. 为什么 “投射/内射” 这个想法不对

`A^m` 是自由模，因此确实是投射模；但**自由模一般不是内射模**。  
所以不能从“投射 + 内射”推出 `m=n`。

而且即使有满射或单射，也通常只能推出“不等式”，不能直接推出相等。

### 2. 在交换环情形下，满射推出 `m >= n`

设

```math
f:A^m\to A^n
```

是满射。对任意极大理想 `\mathfrak m` 局部化，得到满射

```math
f_{\mathfrak m}: A_{\mathfrak m}^m \to A_{\mathfrak m}^n.
```

再模去极大理想，得到剩余域 `k(\mathfrak m)` 上的满射

```math
k(\mathfrak m)^m \to k(\mathfrak m)^n.
```

这是有限维向量空间之间的满射，因此必有

```math
m \ge n.
```

### 3. 在交换环情形下，单射推出 `m <= n`

若

```math
f:A^m\to A^n
```

单射，则局部化后仍单射：

```math
f_{\mathfrak m}: A_{\mathfrak m}^m \hookrightarrow A_{\mathfrak m}^n.
```

设 `C = coker(f)`，则有短正合列

```math
0 \to A^m \to A^n \to C \to 0.
```

局部化后仍正合：

```math
0 \to A_{\mathfrak m}^m \to A_{\mathfrak m}^n \to C_{\mathfrak m} \to 0.
```

再张量剩余域 `k(\mathfrak m)`，得到右正合列

```math
k(\mathfrak m)^m \to k(\mathfrak m)^n \to C_{\mathfrak m}/\mathfrak m C_{\mathfrak m} \to 0.
```

因为最后一项是某个向量空间，所以

```math
\dim k(\mathfrak m)^n
=
\dim \operatorname{Im}(f_{\mathfrak m}\otimes k(\mathfrak m))
 + \dim (C_{\mathfrak m}/\mathfrak m C_{\mathfrak m})
\ge m.
```

故 `n >= m`，即

```math
m \le n.
```

### 4. 为什么对一般环不能随便说

一般环未必满足 `IBN`（Invariant Basis Number）。存在某些环使得

```math
A \cong A^2
```

作为左 `A`-模同构。那时就会出现 `m != n` 但 `A^m \cong A^n` 的现象，于是单射、满射都可能在不同秩之间发生。

所以这题若放在交换代数语境，答案是：

- 满射 `=> m >= n`
- 单射 `=> m <= n`

但若问任意环，则必须额外假设 `A` 满足 `IBN` 一类条件。

---

# Q4

设 `A` 是一个环，而 `M,N` 不全是 `A` 上的有限生成模。能否由

```math
M \otimes_A N = 0
```

推出 `M = 0` 或 `N = 0`？

Idea4:

- `\mathbb Q \otimes_A \mathbb Z/2\mathbb Z` 是否为零？
- `\mathbb Z/2\mathbb Z \otimes_A \mathbb Z/3\mathbb Z = 0` 吗？

## 判定

不能推出。

而且即使 `M,N` 都是有限生成模，也仍然不能推出。

## 解答

### 1. 反例一：`Z/2 ⊗ Z/3 = 0`

在 `A=\mathbb Z` 上，有一般公式

```math
\mathbb Z/m\mathbb Z \otimes_{\mathbb Z} \mathbb Z/n\mathbb Z
\cong
\mathbb Z/\gcd(m,n)\mathbb Z.
```

因此

```math
\mathbb Z/2\mathbb Z \otimes_{\mathbb Z} \mathbb Z/3\mathbb Z
\cong
\mathbb Z/\gcd(2,3)\mathbb Z

=
0.
```

但两边都不是零模。

所以已经得到反例：

```math
M\otimes_A N=0
\centernot\Longrightarrow
M=0 \text{ or } N=0.
```

### 2. 反例二：`\mathbb Q \otimes \mathbb Z/2 = 0`

仍取 `A=\mathbb Z`。由于 `\mathbb Q` 是把所有非零整数都变成单位得到的局部化，而 `\mathbb Z/2\mathbb Z` 是 `2`-torsion，所以张量后被消掉：

```math
\mathbb Q \otimes_{\mathbb Z} \mathbb Z/2\mathbb Z = 0.
```

也可直接算：在张量积里

```math
1\otimes \bar 1

=
\frac12 \otimes 2\bar 1

=
\frac12 \otimes 0

=
0,
```

于是所有元素都为零。

### 3. 为什么会这样

张量积并不会“忠实地检测非零性”。  
只有在很特殊的情形，例如一边是 **faithfully flat** 模时，才可以从

```math
M\otimes_A N=0
```

反推另一边的某种消失结论。

例如若 `N` 是 faithfully flat 的 `A`-模，则

```math
M\otimes_A N=0 \Longrightarrow M=0.
```

但对一般模，这个结论完全不成立。

### 4. 本题结论

因此这题的最终答案是：

- 一般不能推出 `M=0` 或 `N=0`；
- 甚至在有限生成模里也不能推出；
- 反例可取
  - `\mathbb Z/2\mathbb Z \otimes_{\mathbb Z} \mathbb Z/3\mathbb Z = 0`
  - `\mathbb Q \otimes_{\mathbb Z} \mathbb Z/2\mathbb Z = 0`.
