# notes

* 一遍略读
* 反复精读，草稿纸上抄写证明过程，整理成笔记
* 含证明，不必写进slides，作为补充材料

## 4.1 Concentration in metric spaces

### 度量空间和Lipschitz函数

### 例子：Gaussian concentration

**Gaussian concentration**

* 引理4.3：设 $f: \mathbb{R}^n \to \mathbb{R}$ 一阶导数连续，则 $L$-Lipschitz 等价于 $\|\|\nabla f\|^2\|_{\infty} \le L^2$
  * 这里无穷范数应该是关于（连续的）自变量求上确界
  * Lipschitz $\iff$ 导数有上界
* $L$-Lipschitz $\iff$ $\|\|\nabla f\|^2\|_{\infty} \le L^2$ $\implies$ $L^2$-subgaussian
* 令 $L=1$

### 例子：McDiarmid's inequality

**Def. "discrete derivative"**

$$
D_i f(x) := \sup_{z} f(x_1,\cdots,x_{i-1},z,x_{i+1},\cdots,x_n) - \inf_{z} f(x_1,\cdots,x_{i-1},z,x_{i+1},\cdots,x_n)
$$

* 理解为 $f(x)$ 对 $x_i$ 的“离散导数”
* 是因 $x_i$ 变化而导致函数 $f(x)$ 值变化量的上确界

**Def. weighted Hamming distance**

$$
d_c(x, y) := \sum_{i=1}^{n} c_i \mathbf{1}_{x_i\neq y_i}
$$

* 定义在 $\mathbb{X}_1\times\cdots\times\mathbb{X}_n$ 上，$\mathbb{X}_i$ 可测 $(i=1,\cdots,n)$
* 从零开始，第 $i$ 坐标不同则加 $c_i$

**Lemma 4.5** 设 $f: \mathbb{X}_1\times\cdots\times\mathbb{X}_n \to \mathbb{R}$，则 $d_c$ 距离意义下 $1$-Lipschitz 充要条件是 $\forall i, ||D_i f||_{\infty} \le c_i$

证明：（1） 各坐标依次从 $x$ 移向 $y$，第 $i$ 步 $f$ 变化量 $\delta_i\le D_i \le c_i$，则
$$
f(y) - f(x)
= \sum_{i: x_i\neq y_i} \delta_i \le \sum_{i: x_i\neq y_i} c_i
= d_c(x, y)
$$

所以是Lipschitz函数

调换 $x, y$ 仍成立；或者说加上绝对值符号，就是绝对值不等式

（2）设 $x, y$ 有且仅有第 $i$ 元素不同 $\exists ! i, x_i \neq y_i$，则 由Lipschitz得
$$
|f(y) - f(x)| \le d_c(x, y) = c_i
$$

由 $x_i, y_i$ 任意性得

$$
D_i f = \sup |f(y) - f(x)| \le c_i
$$

对 $\forall i$ 成立

### Bobkov-G{\"o}tze

问题：在度量空间 $(\mathbb{X}, d)$ 中，怎样的概率测度 $\mu$ 能够使得所有 $f\in{\rm Lip}(\mathbb{X})$ 都是 $\sigma^{2}$-subgaussian？

**Def 4.6 Wasserstein distance**

$$
\begin{aligned}
W_1(\mu, \nu)
&:= \sup_{f\in{\rm Lip}(\mathbb{X})} \left|\int fd\mu - \int fd\nu\right| \\
&= \sup_{f\in{\rm Lip}(\mathbb{X})} \left|\mathbb{E}_{\mu} f - \mathbb{E}_{\nu} f\right| \\
& = \inf_{\mathbf{M} \in \mathcal{C}(\mu,\nu)} \mathbb{E}_{\mathbf{M}} [d(X, Y)]
\end{aligned}
$$

* $\mu, \nu \in \mathcal{P}_{1}(\mathbb{X})$ 意味着距离 $d$ 期望有限，这等价于所有 $f\in{\rm Lip}(\mathbb{X})$ 期望有限
* Lipschitz函数 $f$ 在2个概率测度 $\mu, \nu$ 下的期望之差的上确界
* 是两个概率测度 $\mu, \nu$ 之间的一种距离
* 另一种看法是 earth moving 推土机距离，但下一节才提到

**Def 4.7 Relative entropy**

$$
D(\nu\|\mu) = -\mathbb{E}_{\nu} \left[\ln \cfrac{d\mu}{d\nu}\right]
$$

* 就是KL散度，是两个概率测度 $\mu, \nu$ 之间的一种不对称的“距离”
* 不知道 $\nu << \mu$ 什么意思，不知道为什么 ${\rm Ent}_{\mu}$，不知道为什么 $\infty$

**Thm 4.8 Bobkov-Götze**

**Lemma. Gibbs variational principle**

证明：

* 定义 $\tilde{\mu}$
* 相对熵定义
* 对数内乘一项 $d\mu$ 除一项 $d\mu$
* 第2项相对熵定义；第3项代入 $\tilde{\mu}$ 定义，第1项与 $\nu$ 无关，对 $\nu$ 求期望不变，加起来
* 关于 $\nu$ 最优化，结果似乎就是 $\nu=\tilde{\mu}$，使得 $D(\nu\|\tilde{\mu}) = 0$

证明 **Thm 4.8 Bobkov-Götze**

* 从条件1出发，subgaussian定义
* 右边移到左边，使用上面的lemma，把 $\lambda(f-\mathbb{E}_{\mu}f)$ 代入lemma中的 $f$，对 $\nu$ 求期望，$f$ 为 $\mathbb{E}_{\nu}f$，$\mathbb{E}_{\mu}f$ 为常数不变，这样就凑出了Wasserstein距离定义式中的 $\mathbb{E}_{\nu}f - \mathbb{E}_{\mu}f$
* $\lambda, f, \nu$ 三重上确界，其实可以看做 $\forall \lambda, \forall f, \forall \nu$，可以调换顺序
* 作为 $\lambda$ 的一元二次函数不大于零，对应根的判别式 $b^2-4ac$ 不大于零
* $\forall \nu \forall f: (\mathbb{E}_{\nu}f - \mathbb{E}_{\mu}f)^2 \le D(\nu\|\mu)$
* 左边对 $f$ 上确界得Wasserstein距离
* 每一步都等价

### Pinsker's inequality

* trivial metric 意义下的Lip等价于 $|\sup f - \inf f| \le 1$
* Wasserstein distance = total variation distance
* 使用Bobkov-Götze定理 2->1
$$
\sigma^{2} = \cfrac{1}{4}(\sup f - \inf f) \le \cfrac{1}{4}\\
W_1 = TV \le \sqrt{2\sigma^{2}D(\nu\|\mu)} \le \sqrt{\cfrac{1}{2}D(\nu\|\mu)}
$$

证明

**引理3.6 (Hoeffding引理)** 有界 $f(X)$ 是 $\cfrac{1}{4}(\sup f - \inf f)$-subgaussian

* 使用Bobkov-Götze定理 2->1
$$
\sigma^{2} = \cfrac{1}{4}(\sup f - \inf f) \le \cfrac{1}{4}\\
W_1(\mu, \nu) = \|\mu-\nu\|_{\rm TV} \le \sqrt{2\sigma^{2}D(\nu\|\mu)} \le \sqrt{\cfrac{1}{2}D(\nu\|\mu)}
$$

## 4.2 Transportation inequalities and tensorization

### 推土机

**Def 4.12 Coupling** $\mathcal{C}(\mu, \nu)$

* 联合分布组成的集合

**Thm 4.13 Monge-Kantorvich duality**

$$
\begin{aligned}
W_1(\mu, \nu)
&= \sup_{f\in{\rm Lip}(\mathbb{X})} \left|\mathbb{E}_{\mu} f - \mathbb{E}_{\nu} f\right| \\
& = \inf_{\mathbf{M} \in \mathcal{C}(\mu,\nu)} \mathbb{E}_{\mathbf{M}} [d(X, Y)]
\end{aligned}
$$

* optimal transport，推土机距离，把两个分布看成两个沙堆，从其中一个搬成另一个所需的最小成本

证明：

线性规划，Lagrange
$$
L(M, f, g, h) = \sum_{i,j} d_{ij} M_{ij} - \sum_{i, j} h_{ij} M_{ij} - \sum_i f_i (\sum_j M_{ij} - \mu_i) - \sum_j g_j (\sum_i M_{ij} - \nu_i)
$$

Lagrange dual
$$
\max_{f, g} \sum_i f_i \mu_i + \sum_j g_j \nu_i = \mathbb{E}_{\mu} f + \mathbb{E}_{\nu} g
$$
s.t. $\forall i \forall j$
$$
h_{ij} \ge 0 \\
d_{ij} - h_{ij} - f_i - g_j = 0\
$$

所以
$$
\inf_{\mathbf{M} \in \mathcal{C}(\mu,\nu)} \mathbb{E}_{\mathbf{M}} [d(X, Y)] = \sup\left\{\mathbb{E}_{\mu} f + \mathbb{E}_{\nu} g: \forall x\forall y\ f(x) + g(y) \le d(x, y) \right\}
$$

往证右边上确界就是Wasserstein distance。一方面取 $g=-f$ 缩小得 $W_1$
$$
\sup\{\cdots\} \ge W_1
$$

另一方面 $f, g$ 可能都不是Lipschitz，构造 $\tilde{f}$

$$
\sup\{\cdots\} \le W_1
$$

### 例子：total variation

* 构造 $\mathbf{M}$，填表
* 图片

### transportation inequality

### tensorize

**Thm 4.15 Marton**

证明：

* Lemma 4.18
* induction

推论

## 4.3 Talagrand's concentration inequality

### 单侧Lip

### Talagrand

### 例子

前几章算过

### 推论

### Talagrand证明

略

## 4.4 Dimension-free concentration and the T2-inequality

### $T_2$ 不等式

把Bobkov-G{"o}tze定理的第2个条件，也就是运输不等式中的 $W_1$ 换成 $W_2$

从Marton定理得到推论

### 对比

### Gozlan定理

条件限制更为苛刻，$n$ 个随机变量服从相同分布 $\mu$
