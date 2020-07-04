# 函数的增长

> 讨论了渐近记号。

## 渐近记号（Asymptotic Notation）

> 渐进记号可以看成是一个函数，它把函数映射为函数的集合。可以形式化定义某个渐进记号 $\Sigma$：
>
> - 假设 $\mathbb{F}$ 是渐进记号接受函数的集合，
>
> - $\Sigma: \mathbb{F} \to P(\mathbb{F})$

规定我们使用的渐进记号接受的函数类型为 $\mathbb{N} \to \mathbb{R}$，也可将定义域、值域做适当的限制或扩展。

- $\Theta(g) = \{f  \mid \exist c_1>0, c_2 > 0, n_0 > 0, \forall n \ge n_0,0\le c_1g(n) \le f(n) \le c_2g(n)\}$
- $O(g) = \{f \mid \exist c > 0, n_0 > 0, \forall n \ge n_0,0\le f(n) \le cg(n)\}$
- $\Omega(g) = \{f \mid \exist c > 0, n_0 > 0, \forall n \ge n_0,0\le cg(n)\le f(n)\}$
- $o(g) = \{f \mid \forall c > 0, \exist n_0 > 0, \forall n \ge n_0,0\le f(n) < cg(n)\}$
- $\omega(g) = \{f \mid \forall c > 0, \exist n_0 > 0, \forall n \ge n_0,0\le cg(n) < f(n)\}$

### 严谨性

> 渐进记号返回的实际上是**函数**的集合，同时它接受的输入也是一个**函数**。在笔记里，会采用两种**匿名函数**表示方法（有时会穿插出现）：
>
> - $n \mapsto f(n),\quad (x, y) \mapsto f(x, y),\quad x \mapsto y \mapsto f(x, y)$
> - $\lambda n. f(n),\quad\lambda (x, y). f(x, y),\quad\lambda x.\lambda y.f(x, y)$
>
> 例如 $f(n) = 2n$ 可以匿名的表示为 $n \mapsto 2n$ 或者 $\lambda n. 2n$。

然而在很多情况下，我们会写成 $O(n),\ \Theta(n^2),\ O(1)$ 等形式。严格意义上来说，这些写法都不严谨，因为记号接受的输入均不是函数，而是（含有或没有自由变量的）表达式。严谨的写法应该是 $O(n \mapsto n)$，$\Theta(\lambda x. x^2)$，$O(f)\quad f(y) = 1$。（刻意采用了不同的自变量符号，这并不影响一个函数的表示）

### 基本的活用

> 绝大多数的资料中均会采取不严谨的表达方法。因此这里给出定义，在上下文清晰的情况下 $O(n)$ 等接受表达式而非函数的式子实际上表达了什么。

假设 $e$ 是一个非函数**表达式**（可以含有自由变量）。在上下文清晰的表明 $n$ 是一个自变量时：

- $e \doteq \lambda n. e$

因此，当我们在表达 $n \in O(n^2)$ 时实际上指的是 $\lambda n.n \in O(n \mapsto n^2)$。

下文将介绍其他的活用表达的含义。

## 渐近记号出现在式子中

### 匿名函数

> 当渐进记号出现在式子中时，可以将它解释为某个匿名函数。

$\Theta(g)$ 就代表了某个 $\in \Theta(g)$ 的匿名函数。因此也可以理解为某个满足相关性质，但不知道具体表示的函数。

从而 $\Theta(\lambda n. n^2)(3)$ 就带表给某个 $\in \Theta(\lambda n. n^2)$ 的匿名函数传入 $3$ 这个参数。

### 独立与等式右边

$f = \Theta(g)$ 解释为 $f \in \Theta(g)$。

> 或者也可以解释为，$\Theta(g)$ 中存在某个匿名函数与 $f$ 相等。

### 在公式中

如 $2n^2 + 3n + 1 = 2n^2 + \Theta(n)$，则解释为：存在某个匿名函数 $f \in \Theta(\lambda n. n)$，使 $2n^2 + 3n + 1 = 2n^2 + f(n)$。也可以翻译成 $2n^2 + 3n + 1 = 2n^2 + \Theta(\lambda n. n)(n)$。

### 出现在左边

如 $2n^2 + \Theta(n) = \Theta(n^2)$，解释为：**无论怎么选择左边的匿名函数，都能选择右边的匿名函数是等式成立**。

## 算法的运行时间分析

> 算法的运行时间分析运用到渐进记号。

### 算法运行时间的决定因素

> 算法的运行时间 $t \in \mathbb R$ 是一个**实数**。

一个算法某次执行的时间**唯一**取决于它的**输入**（包括随机算法的随机选择结果）。如果我们假设，算法的输入取自集合 $\mathbb I$，那么该算法就存在一个 $T_\bullet: \mathbb I \to \mathbb R$，它将算法的输入映射到该输入下的执行时间。

我们可以定义：

- $T_\bullet = \lambda i. \sum(\text{the number of steps each line of code takes } \cdot \text{ its time cost})$

### 算法在相应规模下可能执行时间

> 一般而言，算法的输入规模极大的影响了算法的运行时间。因此，在分析算法时，我们不是细化到计算每个输入下算法的执行时间，从而得到 $T_\bullet$，而是考察算法在某个规模 $s$ 下可能的运行时间，把它记为 $T_\star(s)$，对应的函数就是 $T_\star$。
>
> 一个算法的规模 $\mathbb S$ 是什么依赖具体问题，例如数组长度、二进制位数、$(x, y)$ 等，通常 $\mathbb {S = N}$。

假设输入集合为 $\mathbb I$，它的规模集合是 $\mathbb S$，则 $T_\star$ 的定义：

- $T_\star(s) = \{T_\bullet(i) \mid (i \in \mathbb I) \land (\mathrm{scale}(i) = s)\}$

所以 $T_\star$ 其实是一个将**输入规模**映射到可能的**运行时间的集合**的函数。

### 最坏情况与最好情况下的运行时间函数

>  最坏情况与最好情况下的运行时间函数 $T_\mathrm{worst}, T_\mathrm{best}: \mathbb S \to \mathbb R$。

- $T_\mathrm{worst}(s) = \max T_\star(s)$
- $T_\mathrm{best}(s) = \min T_\star(s)$

> 进而，在规模为 $k$ 时算法的最坏或最好情况运行时间就是 $T_\mathrm{worst}(k)$ 或 $T_\mathrm{best}(k)$。

### 算法的运行时间函数

对于一个算法，合法的运行时间函数共同组成一个集合 $\mathbb T$，它的定义：

- $\mathbb T = \{T: \mathbb S\to \mathbb R \mid \forall s \in \mathbb S (T(s) \in T_\star(s))\}$。

意思就是，对每个规模 $s$，取一个该规模下可能的运行时间，这样所组成的运行时间函数就是合法的。

> #### 区分运行时间和运行时间函数
>
> - 运行时间是一个 $\mathbb R$ 上的**数**，
>
> - 而运行时间函数是一个 $\mathbb {S \to R}$ 上的**函数**。
>
>   > 分析算法时，我们就会建立这样的函数。

### 算法的运行时间为 $O(n^2)$

> 这句话我们经常说，其中的 $n$ 代表了规模。这句话想要表达，运行时间函数是 $O(n^2)$ 的，但我们知道一个算法的运行时间函数不唯一（有最好情况的、最坏情况的等等），从而导致了这句话不严谨。

当我们说“最好（或最坏）情况的运行时间为 $O(n^2)$“时，我们在表达：

- $T_\mathrm{best} \in O(n^2)$
- $T_\mathrm{worst} \in O(n^2)$

而“算法的运行时间为 $O(n^2)$”表达的意思其实是：

- $\forall T \in \mathbb T(T \in O(n^2))$。

也就是，对任何合法的运行时间函数 $T$ 都有 $T \in O(n^2)$。

> 平均情况，期望时间的运行时间涉及到了概率，则会采用概率模型，表达的含义会与上述解释不同。

## $w$ 与 $o$

从极限的定义，可以得到直观的结论：

$$
f \in o(g) \Rightarrow \lim_{n \to +\infty} \frac{f(n)}{g(n)} = 0 \\
f \in \omega(g) \Rightarrow \lim_{n \to +\infty} \frac{f(n)}{g(n)} = +\infty
$$

## 基础性质

> 为了记住这些性质，可以对渐进记号进行类比。
>
> - $O$ 类比为 $\le$
> - $\Theta$ 类比为 $=$
> - $\Omega$ 类比为 $\ge$
> - $o$ 类比为 $<$
> - $\omega$ 类比为 $>$

### 传递性

- $f \in \Theta(g) \land g \in \Theta(h) \to f \in \Theta(h)$
- $f \in \Theta(g) \land g \in \Theta(h) \to f \in \Theta(h)$
- $f \in \Omega(g) \land g \in \Omega(h) \to f \in \Omega(h)$
- $f \in o(g) \land g \in o(h) \to f \in o(h)$
- $f \in \omega(g) \land g \in \omega(h) \to f \in \omega(h)$

### 自反性

- $f \in \Theta(f)$
- $f \in O(f)$
- $f \in \Omega(f)$

### 对称性

- $f \in \Theta(g) \leftrightarrow g \in \Theta(f)$

### 转置对称性

- $f = O(g) \leftrightarrow g = \Omega(f)$
- $f = o(g) \leftrightarrow g = \omega(f)$

### 三分性

$\lambda n. n$ 与 $\lambda n. n^{1+\sin n}$ 无法比较。

### 等价性质

$f \in \Theta(g) \leftrightarrow (f \in \Omega(g) \land f \in O(g))$

## Exercises

### 性质证明

> 假设 $f, g$ 是渐进非负函数，证明 $h \doteq \lambda n. \max (f(n), g(n)) = \Theta(\lambda n. f(n) + g(n))$。

当 $n$ 很大的时候，$h(n) = \max(f(n), g(n))$，由于渐进非负，得到：

- $h(n) \le f(n) + g(n)$
- $2h(n) \ge f(n) + g(n)$

因此 $\frac{1}{2}(f(n) + g(n)) \le h(n) \le f(n) + g(n)$。

所以证明成立。

### 性质证明

> 证明 $\forall a\forall b (a \in \mathbb R \land b \in \mathbb R) \to ((n + a)^b =\Theta(n^b))$。

蕴含符号之后表达的其实是 $n \mapsto (n + a)^b \in \Theta(n \mapsto n^b)$。

当 $n \ge 2|a| \ge |a|$ 时，

- $n + a \le n + |a| \le 2n$，$(n + a)^b \le 2^bn^b$
- $n + a \ge n - |a| \ge n/2$，$(n + a)^b \ge n^b/2^b$

所以证明成立。

### 解释无意义表述

> 说明“算法 $A$ 的运行时间至少是 $O(n^2)$”这句话没有意义。

这句话表达：$\forall T \in \mathbb T\ \ \exist f \in O(n^2)\ \ \forall n (T(n) \ge f(n))$。也就是：存在一个 $O(n^2)$ 的函数，使运行时间函数永远大于等于它。这个命题永真，我们只需要取 $f = n \mapsto 0$。

### $2^{n+1} \overset{?}{=} O(2^n),\ 2^{2n} \overset ? = O(2^n)$

- $2^{n+1} = 2 \cdot 2^n \le 2 \cdot 2^n$，所以 $2^{n+1} = O(2^n)$。
- $\lim_\limits{n \to \infty}\frac {2^{2n}} {2^n} = \lim_\limits{n \to \infty}2^n = \infty$，所以 $2^{2n} = \omega(2^n) \ne O(2^n)$。

### 算法运行时间与最好最坏情况运行时间

> 证明算法运行时间为 $\Theta(g)$ 等价于算法最好情况运行时间为 $\Omega(g)$ 且最坏情况运行时间为 $O(g)$。

#### 运行时间为 $\Theta(g)$ 时

这种情况下有 $\forall T \in \mathbb T(T \in \Theta(g))$，因此 $T_\mathrm{best}$、$T_\mathrm{worst}$ 都是 $\Theta(g)$，因此分别是 。

#### 最好为 $\Omega(g)$ 且最坏为 $O(g)$

- $T_\mathrm{worst}$ 满足 $\forall T\forall n(T_\mathrm{worst}(n) \ge T(n))$
- $T_\mathrm{best}$ 满足 $\forall T\forall n(T_\mathrm{best}(n) \le T(n))$

现在有 $T_\mathrm{worst} \in O(g)$ 且 $T_\mathrm{best} \in \Omega(g)$，因此当 $n$ 很大时：

- $T_\mathrm{worst}(n) \le c_1g(n)$
- $T_\mathrm{best}(n) \ge c_2g(n)$

因为任何的 $T$ 都介于最好最坏的二者之间，因此有 $c_2g(n) \le T(n) \le c_1g(n)$。即 $T \in \Theta(g)$。

### 证明 $o(g) \cap \omega(g) = \varnothing$

**反证法**

假设 $f \in o(g) \land f \in \omega(g)$：

- $\forall c > 0\ \  \exist n_0 > 0\ \ \forall n \ge n_0(0 \le f(n) < g(n))$
- $\forall c > 0\ \  \exist n_1 > 0\ \ \forall n \ge n_1(f(n) > g(n))$

那么就有，当 $n \ge \max (n_0, n_1)$，对于某个 $c$，有 $f(n) > g(n)$ 且 $f(n) < g(n)$，矛盾。

因此命题成立。

### 扩展渐进记号到向量 $\boldsymbol n \in \mathbb N^n,\ g: \mathbb{N^n \to R}$

- $O(g) = \{f \mid \exists c > 0\ \ \exists n_0 > 0\ \ \forall \boldsymbol n(|\boldsymbol n| \ge n_0 \to 0 \le f(\boldsymbol n) \le cg(\boldsymbol n))\}$。

> Might be wrong🙃.
>
> 书本中对于两个变量的扩展如下：
>
> $$
> O(g) = \{f \mid \exists c > 0\ \ \exists n_0 > 0\ \ \exists m_0 > 0\ \ \text{such that} \\
> \text{for all }n \ge n_0 \text{ or } m \ge m_0 \text{ it satisfies }0 \le f(n, m) \le cg(n, m)\}
> $$


