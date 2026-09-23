# 線性代數筆記：向量空間至基底與維度

> 範圍：Vector Spaces → Subspaces → Linear Combinations / Span → Linear Independence → Bases → Dimension。最後以課堂照片中的矩陣空間與多項式空間為例。本文為獨立撰寫的複習筆記；證明使用簡明英文，說明使用繁體中文。

[TOC]

### 如何閱讀這份筆記

定義是約定，不需要證明；定理、推論與「某集合是基底」才需要證明。下面每個證明都用同一個順序：**已知什麼 → 要證明什麼 → 寫出任意元素或線性關係 → 說明使用了哪個定義 → 得到結論**。英文句子供你練習數學書寫，旁邊的繁中註解指出關鍵一步。建議先遮住證明，自己試寫開頭與關鍵等式，再對照。

## 0. 記號與前提

- $F$ 是一個**體**（field），例如 $\mathbb R$ 或 $\mathbb C$；$V$ 是 $F$ 上的向量空間。
- $0_F$ 是純量的零，$0_V$ 是向量的零。下文不致混淆時都記成 $0$。
- $M_{m\times n}(F)$ 是所有 $m\times n$、元素屬於 $F$ 的矩陣所成的集合。
- $P(F)$ 是係數屬於 $F$ 的**形式多項式**空間；$P_n(F)=\{0\}\cup\{f\in P(F):\deg f\le n\}$，其中 $n\ge0$。零多項式的次數不必定義。
- $\mathrm{span}(\varnothing)=\{0\}$；空集合線性獨立。這兩項約定使後續命題也適用於零維空間。

## 1. Vector Spaces（向量空間）

### Definition 1.1　向量空間

集合 $V$ 配備向量加法及純量乘法；對任意 $u,v,w\in V$、$a,b\in F$，滿足：

1. $u+v\in V$；
2. $u+v=v+u$；
3. $(u+v)+w=u+(v+w)$；
4. 存在 $0_V\in V$，使 $v+0_V=v$；
5. 每個 $v$ 都有 $-v\in V$，使 $v+(-v)=0_V$；
6. $av\in V$，且 $a(u+v)=au+av$；
7. $(a+b)v=av+bv$；
8. $a(bv)=(ab)v$ 且 $1_Fv=v$。

上面為方便閱讀合併列出部分性質；不同教材拆分公理的方式不同，重點是逐一檢查列出的**每一項性質**。

**例子**：$F^n$、$M_{m\times n}(F)$、$P(F)$、$P_n(F)$ 都用通常的逐項加法與純量乘法。$P_n(F)$ 的封閉性也可由後面的 subspace test 得出。

**基礎檢查 — 為何矩陣與多項式也是向量空間？** 對 $A=(a_{ij}),B=(b_{ij}),C=(c_{ij})$，矩陣運算逐項定義為 $(A+B)_{ij}=a_{ij}+b_{ij}$、$(tA)_{ij}=ta_{ij}$。例如

$$
((A+B)+C)_{ij}=(a_{ij}+b_{ij})+c_{ij}
=a_{ij}+(b_{ij}+c_{ij})=(A+(B+C))_{ij}.
$$

因此矩陣的加法結合律來自 $F$ 的結合律；交換律、分配律等也可**逐項**用 $F$ 的對應性質證明。零矩陣的每個元素是 $0_F$，$-A$ 的每個元素是 $-a_{ij}$。形式多項式則把 $x^j$ 的係數當成第 $j$ 個位置：逐係數檢查得到相同結論。此處是驗證公理的證明方法；初學時可以自己挑分配律再寫一次。

### Theorem 1.2　零與負向量的基本性質

對任意 $a\in F$、$v\in V$：

$$
0_Fv=0_V,\qquad a0_V=0_V,\qquad (-1_F)v=-v,\qquad (-a)v=-(av).
$$

**Proof — step 1: $0_Fv=0_V$.** Let $x=0_Fv$. Since $0_F+0_F=0_F$, distributivity gives

$$
x=(0_F+0_F)v=0_Fv+0_Fv=x+x.
$$

Add $-x$ to both sides. Hence $0_V=x=0_Fv$.

> **中文註解**：單純寫「$0v=0$ 很明顯」不算證明。上式先得到 $x=x+x$，再使用加法反元素消去 $x$。

**Proof — step 2: $a0_V=0_V$.** Let $y=a0_V$. Since $0_V+0_V=0_V$, we have $y=a(0_V+0_V)=a0_V+a0_V=y+y$. Add $-y$ to both sides to obtain $y=0_V$.

**Proof — step 3: $(-1_F)v=-v$.** By step 1,

$$
v+(-1_F)v=(1_F+(-1_F))v=0_Fv=0_V.
$$

Thus $(-1_F)v$ satisfies the definition of the additive inverse of $v$. By uniqueness of the additive inverse, $(-1_F)v=-v$.

**Proof — step 4: $(-a)v=-(av)$.** Since $av+(-a)v=(a-a)v=0_Fv=0_V$, the vector $(-a)v$ is the additive inverse of $av$. Hence $(-a)v=-(av)$. $\square$

> **為何用得上**：在 subspace test 中，$0_Fw=0_V$ 與 $(-1_F)w=-w$ 分別幫你取得零向量和負向量。

**補充證明 — 零向量唯一。** Suppose both $z,z'$ are additive identities. Since $z'$ is an identity, $z=z+z'$. Since $z$ is an identity, $z+z'=z'$. Therefore $z=z'$.

**補充證明 — 加法反元素唯一。** Suppose both $w$ and $w'$ are additive inverses of $v$. By associativity and the identity laws,

$$
w=w+0_V=w+(v+w')=(w+v)+w'=0_V+w'=w'.
$$

Thus the inverse is unique. $\square$

> **中文註解**：寫「唯一」通常要假設有兩個候選者，再證它們其實相同；這個套路會在基底表示唯一時再次出現。

## 2. Subspaces（子空間）

### Definition 2.1　子空間

$W\subseteq V$ 若沿用 $V$ 的運算後本身也是 $F$ 上的向量空間，就稱 $W$ 是 $V$ 的子空間（subspace）。

### Theorem 2.2　Subspace test

$W\subseteq V$ 是子空間，若且唯若 $W\ne\varnothing$，且對任意 $u,v\in W$、$a\in F$，有 $u+v\in W$ 與 $au\in W$。等價地，直接驗證 $0_V\in W$，且 $au+bv\in W$ 對所有 $u,v\in W$、$a,b\in F$ 成立。

**Proof — only if.** Suppose $W$ is a subspace. Then $W$ is a vector space under the inherited operations. Hence it is nonempty and closed under vector addition and scalar multiplication.

**Proof — if.** Suppose $W\ne\varnothing$ and both closure properties hold. Choose $w\in W$. Since $W$ is closed under scalar multiplication,

$$
0_V=0_Fw\in W,\qquad -w=(-1_F)w\in W.
$$

Thus $W$ contains the zero vector and the additive inverse of each of its vectors. Associativity, commutativity, distributivity, and $1_Fw=w$ are already true in $V$; they remain true when the inputs lie in $W$. Therefore $W$ is a vector space and hence a subspace. $\square$

> **中文註解**：「沿用原本運算」是重點。我們只需查新集合有沒有缺少運算結果、零向量和負向量，原空間已成立的等式不必逐條重證。驗證 $au+bv$ 封閉時，令 $a=b=0$ 並不能獨自保證 $W$ 非空；仍要先知道 $0\in W$ 或 $W\ne\varnothing$。

**例 2.3**：$W=\{(x,y,z)\in\mathbb R^3:x+y+z=0\}$。若 $u,v\in W$，則其座標和皆為 $0$；$au+bv$ 的座標和仍為 $0$。故 $W$ 是子空間。

**反例**：$A=\{(x,y)\in\mathbb R^2:x+y=1\}$ 不含 $(0,0)$，故不是子空間。判定前先查零向量通常最快。

**補充證明 — $P_n(F)$ 是 $P(F)$ 的子空間。** The zero polynomial belongs to $P_n(F)$ by definition. Let

$$
f=\sum_{j=0}^n a_jx^j,\qquad g=\sum_{j=0}^n b_jx^j
$$

belong to $P_n(F)$, padding missing coefficients with zeros if necessary. For $\alpha,\beta\in F$,

$$
\alpha f+\beta g=\sum_{j=0}^n(\alpha a_j+\beta b_j)x^j.
$$

No term of degree above $n$ appears. Therefore $\alpha f+\beta g\in P_n(F)$, even if it becomes the zero polynomial. The subspace test completes the proof. $\square$

> **中文註解**：這樣寫避開「零多項式的 degree 是多少」的爭議，也清楚處理可能的最高次項相消。
### Theorem 2.4　子空間的交集

若 $\{W_i\}_{i\in I}$ 是 $V$ 的一族子空間，則 $\bigcap_{i\in I}W_i$ 也是子空間（空指標集時交集約定為 $V$）。

**Proof.** Let $W=\bigcap_{i\in I}W_i$. For every $i\in I$, $0_V\in W_i$. Hence $0_V\in W$. Now let $u,v\in W$ and $a,b\in F$. By the definition of intersection, $u,v\in W_i$ for **every** $i$. Since each $W_i$ is a subspace, $au+bv\in W_i$ for every $i$. Thus $au+bv\in W$, and the subspace test proves the claim. If $I=\varnothing$, then $W=V$ by convention, so the claim also holds. $\square$

> **中文註解**：交集中的元素必須「同時屬於每一個」子空間，證明也要對任意 $i$ 完成。

### Definition 2.5　和與直和

$$
U+W=\{u+w:u\in U,\ w\in W\}.
$$

若 $U,W$ 是子空間且 $U\cap W=\{0\}$，記 $U+W=U\oplus W$。此時其中每個向量都有唯一的 $u+w$ 表示。

### Theorem 2.6　子空間和、表示唯一性

$U+W$ 是子空間；且 $U+W$ 中的每個向量都能**唯一**表示成 $u+w$，若且唯若 $U\cap W=\{0\}$。

**Proof — $U+W$ is a subspace.** Since $0_V\in U$ and $0_V\in W$, $0_V=0_V+0_V\in U+W$. Let $x=u_1+w_1$ and $y=u_2+w_2$ belong to $U+W$. For any $a,b\in F$,

$$
ax+by=(au_1+bu_2)+(aw_1+bw_2).
$$

The first parenthesis lies in $U$ and the second in $W$, so $ax+by\in U+W$ by its definition.

**Proof — intersection implies uniqueness.** Suppose $U\cap W=\{0_V\}$ and $u_1+w_1=u_2+w_2$. Rearranging gives

$$
u_1-u_2=w_2-w_1.
$$

The left side belongs to $U$ and the right side belongs to $W$. Their common value therefore lies in $U\cap W=\{0_V\}$. Hence $u_1=u_2$ and $w_1=w_2$.

**Proof — uniqueness implies intersection.** Let $x\in U\cap W$. Then $x=x+0_V=0_V+x$ are two valid $U+W$ decompositions. By uniqueness their $U$ components agree, so $x=0_V$. Thus $U\cap W=\{0_V\}$. $\square$

> **中文註解**：證唯一性常用技巧是「假設有兩種表示，兩邊相減」，再把差放進交集。

**提醒與反例證明**：$U\cup W$ 一般不是子空間。取 $U=\{(x,0):x\in\mathbb R\}$、$W=\{(0,y):y\in\mathbb R\}$。Then $(1,0)\in U\cup W$ and $(0,1)\in U\cup W$, but their sum $(1,1)$ lies in neither $U$ nor $W$. Hence the union is not closed under addition.

## 3. Linear Combinations and Span（線性組合與生成）

### Definition 3.1　線性組合與 span

有限多個 $v_1,\ldots,v_k\in V$ 的線性組合是 $a_1v_1+\cdots+a_kv_k$，其中 $a_i\in F$。對任意集合 $S\subseteq V$，

$$
\mathrm{span}(S)=\left\{\sum_{i=1}^k a_iv_i:k\ge0,\ a_i\in F,\ v_i\in S\right\}.
$$

允許 $k=0$，空和就是 $0_V$。即使 $S$ 是無限集合，每個線性組合也**只用有限多項**。若 $\mathrm{span}(S)=V$，稱 $S$ 生成（spans）$V$。

### Theorem 3.2　span 是最小子空間

$\mathrm{span}(S)$ 是包含 $S$ 的子空間；任何包含 $S$ 的子空間 $W$ 都包含 $\mathrm{span}(S)$。

**Proof — subspace.** The empty linear combination equals $0_V$, so $0_V\in\mathrm{span}(S)$. Let

$$
x=\sum_{i=1}^r a_is_i,\qquad y=\sum_{j=1}^t b_jt_j,
$$

where all $s_i,t_j$ lie in $S$. For any $\alpha,\beta\in F$,

$$
\alpha x+\beta y
=\sum_{i=1}^r(\alpha a_i)s_i+\sum_{j=1}^t(\beta b_j)t_j.
$$

This is still a **finite** linear combination of members of $S$, hence belongs to $\mathrm{span}(S)$. The subspace test applies.

**Proof — contains $S$.** For each $s\in S$, $s=1_Fs$, so $s\in\mathrm{span}(S)$.

**Proof — smallest.** Let $W$ be any subspace with $S\subseteq W$. For every finite combination $\sum_{i=1}^r a_is_i$, scalar closure gives $a_is_i\in W$ and additive closure gives $\sum_{i=1}^r a_is_i\in W$. Thus $\mathrm{span}(S)\subseteq W$. $\square$

> **中文註解**：要證「最小」不是比數量，而是證它包含在**每一個**含 $S$ 的子空間裡。

### Theorem 3.3　加入已在 span 中的向量不改變 span

若 $w\in\mathrm{span}(S)$，則 $\mathrm{span}(S\cup\{w\})=\mathrm{span}(S)$。

**Proof.** Since $S\subseteq S\cup\{w\}$, every linear combination of members of $S$ is also a linear combination of members of $S\cup\{w\}$. Hence

$$
\mathrm{span}(S)\subseteq\mathrm{span}(S\cup\{w\}).
$$

Conversely, write $w=\sum_{i=1}^r c_is_i$ with $s_i\in S$. Any member of the larger span has the form $x=aw+\sum_{j=1}^t b_jt_j$, where $t_j\in S$. Substitute the expression for $w$:

$$
x=\sum_{i=1}^r(ac_i)s_i+\sum_{j=1}^t b_jt_j\in\mathrm{span}(S).
$$

Thus the reverse inclusion also holds and the two spans are equal. $\square$

> **中文註解**：集合相等要證兩邊包含；「代入 $w$ 的表示」就是刪除多餘向量的實際操作。

**例 3.4**：$(1,1)=(1,0)+(0,1)$，所以 $\mathrm{span}\{(1,0),(0,1),(1,1)\}=\mathbb R^2$；第三個向量在生成方面是多餘的。

## 4. Linear Independence（線性獨立）

### Definition 4.1　線性獨立／相依

$S\subseteq V$ **線性獨立**（linearly independent, LI），指 $S$ 中任意有限且互異的 $v_1,\ldots,v_k$，

$$
a_1v_1+\cdots+a_kv_k=0\quad\Longrightarrow\quad a_1=\cdots=a_k=0.
$$

否則稱 **線性相依**（linearly dependent, LD）；也就是存在有限個互異向量及**至少一個非零**係數，組合後等於零向量。

### Theorem 4.2　常用相依判準

1. 含有 $0_V$ 的集合線性相依。
2. 非空集合 $S$ 線性相依，若且唯若其中某個向量可由 $S$ 中**其他有限多個**向量線性組合而成。
3. 線性獨立集合的任意子集合仍線性獨立；相依集合的任意超集合仍相依。

**Proof — (1).** If $0_V\in S$, the equation $1_F0_V=0_V$ uses a nonzero coefficient $1_F$. Thus it is a nontrivial relation and $S$ is dependent.

**Proof — (2), forward.** Suppose $S$ is dependent. There are distinct $v_1,\ldots,v_k\in S$ and coefficients, not all zero, such that $\sum_{i=1}^k a_iv_i=0_V$. Choose $j$ for which $a_j\ne0_F$. Since every nonzero element of a field has an inverse,

$$
v_j=-a_j^{-1}\sum_{i\ne j}a_iv_i
=-\sum_{i\ne j}\frac{a_i}{a_j}v_i.
$$

Hence $v_j$ is a combination of the other vectors. If $k=1$, this is the empty combination $0_V$.

**Proof — (2), backward.** If $v_j=\sum_{i\ne j}c_iv_i$, rearrange to obtain $1_Fv_j-\sum_{i\ne j}c_iv_i=0_V$. The coefficient of $v_j$ is nonzero, so $S$ is dependent.

**Proof — (3).** If a subset of an independent set had a nontrivial relation, the same relation would also exist in the larger set, a contradiction. If a set is dependent, its finite nontrivial relation remains valid in every superset. $\square$

> **中文註解**：除以 $a_j$ 之前，務必寫「選 $a_j\ne0$」。這也是為何純量必須來自體 $F$。

### Theorem 4.3　獨立組的表示唯一

若 $S=\{v_1,\ldots,v_k\}$ 線性獨立，則 $\mathrm{span}(S)$ 中每個向量相對於這組向量的係數唯一。

**Proof.** Let $x\in\mathrm{span}(S)$, and suppose it has two representations

$$
x=a_1v_1+\cdots+a_kv_k=b_1v_1+\cdots+b_kv_k.
$$

Subtract the two equations:

$$
0_V=(a_1-b_1)v_1+\cdots+(a_k-b_k)v_k.
$$

Since $S$ is linearly independent, **every** coefficient in a zero relation must vanish. Thus $a_i-b_i=0_F$, i.e. $a_i=b_i$, for all $i$. $\square$

> **中文註解**：span 保證「存在表示」；線性獨立保證「表示唯一」。兩個角色在下一章合成基底。

**提醒**：要檢查「是否獨立」，必須從**等於零的線性組合**開始；只找到某個向量可表示為線性組合，是用來證明「相依」。

**空集合的細節**：$\varnothing$ 線性獨立，因為不存在能挑出的有限非平凡相依關係；$\mathrm{span}(\varnothing)=\{0_V\}$，因為唯一允許的和是空和 $0_V$。故 $\varnothing$ 同時獨立且生成零空間，是 $\{0_V\}$ 的基底。這也是 $\dim\{0_V\}=0$ 的原因。

## 5. Bases（基底）

### Definition 5.1　基底

$B\subseteq V$ 是 $V$ 的基底（basis），若 $B$ 同時線性獨立且 $\mathrm{span}(B)=V$。零空間 $\{0\}$ 的基底是空集合。

### Theorem 5.2　基底與唯一座標

$B=\{v_1,\ldots,v_n\}$ 是 $V$ 的基底，若且唯若每個 $v\in V$ 都能**唯一**寫成 $v=a_1v_1+\cdots+a_nv_n$。此時 $[v]_B=(a_1,\ldots,a_n)^T$ 稱為座標向量；座標需先指定基底的**順序**。

**Proof — basis implies unique representation.** Suppose $B$ is a basis. For every $v\in V$, spanning supplies $a_1,\ldots,a_n$ with $v=\sum_i a_iv_i$. If also $v=\sum_i b_iv_i$, subtracting gives $\sum_i(a_i-b_i)v_i=0_V$. Independence forces $a_i=b_i$ for every $i$. Hence the representation exists and is unique.

**Proof — unique representation implies basis.** Suppose every $v\in V$ has exactly one representation using $B$. Existence gives $\mathrm{span}(B)=V$. To check independence, suppose $\sum_i c_iv_i=0_V$. But $0_V=\sum_i0_Fv_i$ is another representation of the same vector. Uniqueness gives $c_i=0_F$ for every $i$. Thus $B$ is independent and spanning, hence a basis. $\square$

> **中文註解**：證「若且唯若」要完成兩個方向。逆向巧妙使用零向量的兩種可能表示，迫使所有係數歸零。

### Theorem 5.3　基底的極小／極大特徵

基底既是**極小生成集**（移除任何一個向量就不再生成），也是**極大線性獨立集**（加入任何一個基底外的向量就相依）。反過來，在 $V$ 中，極小生成集或極大線性獨立集也都是基底。

**Proof — a basis is a minimal spanning set.** Let $B$ be a basis and $b\in B$. If $B\setminus\{b\}$ still spanned $V$, then $b\in\mathrm{span}(B\setminus\{b\})$. By Theorem 4.2, $B$ would be dependent, a contradiction. Thus removing any $b$ destroys spanning.

**Proof — a basis is a maximal independent set.** If $v\in V\setminus B$, then $v\in\mathrm{span}(B)$ because $B$ spans $V$. By Theorem 4.2, $B\cup\{v\}$ is dependent.

**Proof — minimal spanning implies basis.** Let $S$ be a minimal spanning set. Suppose it is dependent. By Theorem 4.2, there is $s\in S$ with $s\in\mathrm{span}(S\setminus\{s\})$. Theorem 3.3 gives $\mathrm{span}(S\setminus\{s\})=\mathrm{span}(S)=V$, contradicting minimality. Hence $S$ is independent and therefore a basis.

**Proof — maximal independent implies basis.** Let $S$ be a maximal independent set. If $\mathrm{span}(S)\ne V$, choose $v\in V\setminus\mathrm{span}(S)$. Suppose $S\cup\{v\}$ were dependent. Since $S$ is independent, the coefficient of $v$ in a nontrivial relation must be nonzero, so we could solve for $v\in\mathrm{span}(S)$, a contradiction. Thus $S\cup\{v\}$ is independent, contradicting maximality. Therefore $\mathrm{span}(S)=V$ and $S$ is a basis. $\square$

> **中文註解**：這裡的「極小／極大」是指**不能再刪／不能再加**，不是說與別組基底比較數量。

### Example 5.4　矩陣空間的標準基底（課堂照片）

對 $1\le i\le m$、$1\le j\le n$，定義 $E^{ij}\in M_{m\times n}(F)$：

$$
(E^{ij})_{k\ell}=\begin{cases}1_F,&(k,\ell)=(i,j),\\0_F,&\text{otherwise}.\end{cases}
$$

**Theorem.** $\mathcal E=\{E^{ij}:1\le i\le m,\ 1\le j\le n\}$ 是 $M_{m\times n}(F)$ 的基底。

**Proof — spanning.** Let $A=(a_{ij})\in M_{m\times n}(F)$ be arbitrary and set $B=\sum_{i=1}^m\sum_{j=1}^n a_{ij}E^{ij}$. Fix a position $(k,\ell)$. At this position, all $E^{ij}$ are zero except $E^{k\ell}$, whose entry is $1_F$. Hence $B_{k\ell}=a_{k\ell}$. Since **every** entry of $B$ equals the corresponding entry of $A$, $B=A$. Therefore every $A$ lies in $\mathrm{span}(\mathcal E)$.

> **中文註解**：證矩陣相等，要逐一比較位置；「任取 $(k,\ell)$」讓這一步對所有格子都有效。

**Proof — independence.** Suppose $\sum_{i=1}^m\sum_{j=1}^n c_{ij}E^{ij}=0_{m\times n}$. Fix any position $(k,\ell)$. The entry on the left is $c_{k\ell}$; the entry on the right is $0_F$. Thus $c_{k\ell}=0_F$. Since $(k,\ell)$ was arbitrary, **all** coefficients vanish. Therefore $\mathcal E$ is linearly independent. Together with spanning, $\mathcal E$ is a basis. $\square$

**繁中理解**：每個 $E^{ij}$ 只管一個位置；要拼出 $A$，就把第 $(i,j)$ 個位置的數字 $a_{ij}$ 乘上對應的 $E^{ij}$ 再相加。

### Example 5.5　多項式空間的標準基底（課堂照片）

**Theorem.** 對 $n\ge0$，$\mathcal P_n=\{1,x,x^2,\ldots,x^n\}$ 是 $P_n(F)$ 的基底。

**Proof — spanning.** Let $f\in P_n(F)$. By the definition of $P_n(F)$, either $f=0$ or $f$ has degree at most $n$. In both cases we can choose $a_0,\ldots,a_n\in F$ such that

$$
f=a_0(1)+a_1x+\cdots+a_nx^n;
$$

when $f=0$, choose every $a_i=0_F$. Hence every $f$ is a combination of $\mathcal P_n$ and $\mathrm{span}(\mathcal P_n)=P_n(F)$.

**Proof — independence.** Suppose $c_0(1)+c_1x+\cdots+c_nx^n$ is the **zero formal polynomial**. The coefficients of the zero polynomial at degrees $0,1,\ldots,n$ are all $0_F$. Equality of formal polynomials is defined coefficient by coefficient, so $c_0=c_1=\cdots=c_n=0_F$. Thus $\mathcal P_n$ is independent. Together with spanning, it is a basis. $\square$

> **中文註解**：矩陣是「逐格比較」，多項式是「逐次方比較」。兩個證明的結構完全相同。

**重要細節**：此處比較的是**形式多項式的係數**，不能把「在有限體 $F$ 的每個點代入都得到 $0$」直接當成同一件事。例如在 $F_2$ 上，$x^2-x$ 是非零形式多項式，卻在 $F_2$ 的兩個點都取值 $0$。

## 6. Dimension（維度）與有限維定理

### Definition 6.1　有限維與維度

若 $V$ 有一個有限基底，則稱 $V$ 為有限維；任一有限基底中的向量個數稱為 $\dim V$。以下定理保證此數字不依基底的選擇而改變。$\dim\{0\}=0$。

### Lemma 6.2　Replacement / exchange lemma（替換引理）

若 $V$ 由 $n$ 個向量 $w_1,\ldots,w_n$ 生成，而 $v_1,\ldots,v_k$ 線性獨立，則 $k\le n$；並且可依序把 $k$ 個 $w_i$ 換成 $v_1,\ldots,v_k$，仍保持生成 $V$。

**Proof — induction on the number of replacements.** We show that, for each $r$ up to $k$, after replacing $r$ old vectors there is still a generating list of exactly $n$ vectors containing $v_1,\ldots,v_r$.

**Base case $r=0$.** No vector has been replaced. The list $(w_1,\ldots,w_n)$ generates $V$ by assumption.

**Induction hypothesis.** Suppose $0\le r<n$ and, after relabeling the old vectors that remain, the list

$$
(v_1,\ldots,v_r,w_{r+1},\ldots,w_n)
$$

generates $V$. The list may contain repeated vectors; the argument only needs it to generate.

**Induction step.** Since this list generates $V$, there are $a_1,\ldots,a_r,b_{r+1},\ldots,b_n\in F$ with

$$
v_{r+1}=\sum_{i=1}^{r}a_iv_i+\sum_{j=r+1}^{n}b_jw_j. \tag{1}
$$

At least one $b_j$ is nonzero. Otherwise equation (1) would put $v_{r+1}$ in $\mathrm{span}\{v_1,\ldots,v_r\}$, contradicting the linear independence of $v_1,\ldots,v_k$. Relabel the remaining old vectors so that $b_{r+1}\ne0$. We can divide by this coefficient in the field $F$ and solve (1) for the vector being removed:

$$
w_{r+1}=b_{r+1}^{-1}
\left(v_{r+1}-\sum_{i=1}^{r}a_iv_i
-\sum_{j=r+2}^{n}b_jw_j\right). \tag{2}
$$

Equation (2) says that $w_{r+1}$ is in the span of the new list

$$
(v_1,\ldots,v_r,v_{r+1},w_{r+2},\ldots,w_n).
$$

Every other vector of the previous generating list already appears in the new list. Thus every old generator, and hence every vector of $V$, is a combination of the new list. This completes the induction step.

**Why $k\le n$.** If we had $k>n$, the first $n$ steps would produce the generating list $(v_1,\ldots,v_n)$. Then $v_{n+1}\in\mathrm{span}\{v_1,\ldots,v_n\}$ because that list generates $V$, contradicting the independence of $v_1,\ldots,v_k$. Therefore $k\le n$. $\square$

> **中文註解**：這正是黑板上的歸納法。起點是「換 0 個也能生成」；歸納假設是「換了 $r$ 個仍生成」；關鍵有兩步：先證某個舊向量的係數 $b_j\ne0$，再**把那個舊向量解出來**。式 (2) 解釋了為什麼替換後沒有失去生成能力。寫「可替換」而不寫式 (2)，會省略證明核心。

### Theorem 6.3　所有有限基底等長

若 $B$、$C$ 是 $V$ 的兩個有限基底，則 $|B|=|C|$。

**Proof.** Let $|B|=p$ and $|C|=q$. Since a basis is independent, $B$ is an independent set of $p$ vectors. Since a basis also spans, $C$ is a generating set of $q$ vectors. Apply Lemma 6.2 with independent set $B$ and generating set $C$ to get $p\le q$. Now interchange their roles: $C$ is independent and $B$ spans, so the same lemma gives $q\le p$. Together $p\le q\le p$; hence $p=q$. $\square$

> **中文註解**：不能只證 $p\le q$ 就說相等；把兩組基底角色交換一次，才會得到反方向的不等式。這一定理讓「維度」定義得有意義。

### Theorem 6.4　基底延伸與生成集縮減

若 $\dim V=n$：

1. 每個線性獨立的有限集合都可延伸為 $V$ 的基底。
2. 每個有限生成集都可刪去多餘向量，縮減為 $V$ 的基底。
3. 若恰有 $n$ 個向量，則**線性獨立**與**生成 $V$** 任一條件成立，就足以保證它們是基底。

**Proof — (1), extend an independent set.** Let $S$ be independent. If $\mathrm{span}(S)=V$, it is already a basis. Otherwise choose $v\in V\setminus\mathrm{span}(S)$. To verify that $S\cup\{v\}$ is independent, suppose a finite relation has the form

$$
a v+\sum_{i=1}^r a_is_i=0_V,\qquad s_i\in S.
$$

If $a\ne0_F$, solving for $v$ would give $v=-a^{-1}\sum_i a_is_i\in\mathrm{span}(S)$, a contradiction. Hence $a=0_F$; independence of $S$ then gives every $a_i=0_F$. Thus the larger set is still independent. Repeat while it does not span $V$. By Lemma 6.2 it cannot have more than $n$ members, so the process stops; at the stopping point it spans and is a basis.

> **中文註解**：黑板「從獨立集合選向量」的停止條件是 span 已經等於 $V$。用替換引理限制獨立向量數量，保證不會無止境地加入。

**Proof — (2), reduce a generating set.** Let $T$ be a finite generating set. If it is independent, it is already a basis. Otherwise Theorem 4.2 gives $t\in T$ with $t\in\mathrm{span}(T\setminus\{t\})$. Theorem 3.3 then gives

$$
\mathrm{span}(T\setminus\{t\})=\mathrm{span}(T)=V.
$$

Delete $t$ and repeat while the remaining set is dependent. Each deletion reduces the finite number of members by one, so this process stops. The remaining set still spans $V$ and is independent; hence it is a basis. This also works for $V=\{0\}$, leaving the empty set.

> **中文註解**：黑板另一個停止條件是「每個尚未選入的向量，加入後都相依」。這保證已選向量生成原集合；要因此得到 **$V$ 的基底**，還須知道原集合生成 $V$。

**Proof — (3), exactly $n$ vectors.** First suppose a set of $n$ vectors is independent. By (1) it extends to a basis, but every basis has exactly $n$ vectors by Theorem 6.3. Thus no new vector is needed, and the given set already spans. Next suppose a set of $n$ vectors spans $V$. By (2) it reduces to a basis. Every basis has $n$ vectors, so none can be removed; the given set was independent already. $\square$

> **中文註解**：第 (3) 點的「只驗一項」必須先知道 $\dim V=n$，而且手上剛好有 $n$ 個向量。

### Corollary 6.5　常見空間的維度

$$
\dim F^n=n,\qquad \dim M_{m\times n}(F)=mn,\qquad \dim P_n(F)=n+1.
$$

**Proof — $F^n$.** For $1\le j\le n$ let $e_j$ have $1_F$ in the $j$th position and $0_F$ elsewhere. Every $(a_1,\ldots,a_n)\in F^n$ equals $\sum_{j=1}^n a_je_j$, so these vectors span. If $\sum_j c_je_j=0$, comparison of the $j$th coordinate gives $c_j=0_F$ for every $j$. Hence they are independent and form a basis of $n$ vectors.

**Proof — matrices.** Example 5.4 proved that $\{E^{ij}\}$ is a basis. There are $m$ choices for $i$ and $n$ choices for $j$, hence $mn$ basis vectors.

**Proof — polynomials.** Example 5.5 proved that $\{1,x,\ldots,x^n\}$ is a basis. The exponents $0,1,\ldots,n$ give $n+1$ vectors. By the definition of dimension, the three formulas follow. $\square$

> **中文註解**：維度不是「變數最多的次方」，而是**基底元素的個數**；$P_n(F)$ 的常數 $1=x^0$ 也要算。

### Theorem 6.6　子空間和的維度公式

對有限維空間 $V$ 的子空間 $U,W$：

$$
\dim(U+W)=\dim U+\dim W-\dim(U\cap W).
$$

特別地，若 $U\cap W=\{0\}$，則 $\dim(U\oplus W)=\dim U+\dim W$。

**Proof — choose compatible bases.** Let $B_0=(b_1,\ldots,b_r)$ be a basis of $U\cap W$. By Theorem 6.4, extend it separately to

$$
B_U=(b_1,\ldots,b_r,u_1,\ldots,u_p)\quad\text{for }U,
\qquad
B_W=(b_1,\ldots,b_r,w_1,\ldots,w_q)\quad\text{for }W.
$$

We claim that $B=(b_1,\ldots,b_r,u_1,\ldots,u_p,w_1,\ldots,w_q)$ is a basis of $U+W$.

**Proof — spanning.** Let $x\in U+W$. Write $x=u+w$ with $u\in U$ and $w\in W$. Expand $u$ using $B_U$ and $w$ using $B_W$. Adding the two expressions writes $x$ as a combination of $B$. Therefore $B$ spans $U+W$.

**Proof — independence.** Suppose

$$
\sum_{i=1}^r\alpha_i b_i+\sum_{j=1}^p\beta_j u_j
+\sum_{k=1}^q\gamma_k w_k=0_V. \tag{3}
$$

Rearrange equation (3):

$$
\sum_{k=1}^q\gamma_k w_k
=-\left(\sum_{i=1}^r\alpha_i b_i+\sum_{j=1}^p\beta_j u_j\right). \tag{4}
$$

The left side lies in $W$, and the right side lies in $U$. Thus their common vector $z$ lies in $U\cap W=\mathrm{span}(B_0)$; write $z=\sum_{i=1}^r\delta_i b_i$. Compare this with the left side of equation (4):

$$
\sum_{k=1}^q\gamma_k w_k-\sum_{i=1}^r\delta_i b_i=0_V.
$$

Since $B_W$ is independent, every $\gamma_k=0_F$ (and every $\delta_i=0_F$). Equation (3) becomes $\sum_i\alpha_i b_i+\sum_j\beta_j u_j=0_V$. Independence of $B_U$ gives all remaining coefficients zero. Therefore $B$ is independent.

**Proof — count.** As $B$ is a basis, $\dim(U+W)=r+p+q$. Meanwhile $\dim U=r+p$, $\dim W=r+q$, and $\dim(U\cap W)=r$. Hence

$$
\dim(U+W)=(r+p)+(r+q)-r
=\dim U+\dim W-\dim(U\cap W).
$$

If $U\cap W=\{0_V\}$, then $r=0$, giving the direct-sum formula. $\square$

> **中文註解**：交集的 $r$ 個基底向量在 $U$ 和 $W$ 各算過一次，所以最後減掉 $r$。證聯集獨立時，關鍵不是直接說「兩組基底合起來獨立」，而是先把等式兩側共同的向量放進交集，再用各自的獨立性消去係數。

## 7. 用處與例題

這一節把定義與定理放進實際題目。每題先說明**何時使用**，再展示可直接仿寫的解法。

### 例題 7.1　向量空間：辨認運算的零向量

**用處**：題目若重新定義加法，不能直接把平常的數字 $0$ 當成零向量；先找出此運算的零元，才能繼續檢查向量空間公理。

令 $V=\mathbb R_{>0}$，定義「加法」$u\oplus v=uv$，以及「純量乘法」$a\odot u=u^a$（$a\in\mathbb R$）。找出 $V$ 的零向量與 $u$ 的加法反元素。

**解**：零向量 $e$ 必須滿足 $u\oplus e=u$，即 $ue=u$，所以 $e=1$。反元素 $w$ 滿足 $u\oplus w=e=1$，所以 $w=1/u$。在這個運算下，$0_{\mathbb R}\odot u=u^0=1=e$，正好符合定理 1.2。

**檢查**：$\mathbb R_{>0}$ 在這兩個運算下確實是 $\mathbb R$ 上的向量空間；例如 $(a+b)\odot u=u^{a+b}=u^au^b=(a\odot u)\oplus(b\odot u)$，其餘公理也由正數乘法與次方性質得到。

### 例題 7.2　子空間：齊次條件

**用處**：由線性齊次方程定義的集合，通常用 subspace test 一次證明封閉性；若右側是非零常數，先檢查零向量。

判斷 $W=\{(x,y,z)\in\mathbb R^3:x-2y+z=0\}$ 與 $A=\{(x,y,z)\in\mathbb R^3:x-2y+z=1\}$ 是否為子空間。

**解**：令 $L(x,y,z)=x-2y+z$。若 $u,v\in W$ 且 $a,b\in\mathbb R$，則 $L(au+bv)=aL(u)+bL(v)=0$；且 $0\in W$，故 $W$ 是子空間。因 $L(0)=0\ne1$，$A$ 不含零向量，故不是子空間。

### 例題 7.3　Span：判斷能否表示目標向量

**用處**：求某個向量是否落在 span 中，就是解「係數能否存在」的問題。

設 $v_1=(1,1,0)$、$v_2=(0,1,1)$。判斷 $w=(2,3,1)$ 是否屬於 $\mathrm{span}\{v_1,v_2\}$。

**解**：令 $av_1+bv_2=w$，比較三個座標得 $a=2$、$a+b=3$、$b=1$，三式相容。因此 $w=2v_1+v_2$，故 $w\in\mathrm{span}\{v_1,v_2\}$。若改成 $(2,3,2)$，前兩式要求 $b=1$，第三式卻要求 $b=2$，因此它不在此 span 中。

### 例題 7.4　線性獨立：找出多餘向量

**用處**：檢查一組向量能否擔任基底，以及從生成集刪除多餘的向量。

設 $S=\{(1,0,1),(0,1,1),(1,1,2)\}$。判斷 $S$ 是否線性獨立。

**解**：第三個向量等於前兩個之和，因此

$$
(1,0,1)+(0,1,1)-(1,1,2)=(0,0,0).
$$

係數 $(1,1,-1)$ 不全為零，所以 $S$ 線性相依。刪去第三個向量後，前兩個向量線性獨立，仍生成與原集合相同的子空間。

### 例題 7.5　基底與座標：同一向量的不同表示

**用處**：選定基底後，可以用一串係數記錄向量；轉換基底時，向量本身不變，座標會改變。

在 $\mathbb R^2$ 中，令 $B=((1,1),(1,-1))$。證明 $B$ 是基底，並求 $[(3,1)]_B$。

**解**：若 $a(1,1)+b(1,-1)=(0,0)$，則 $a+b=0$、$a-b=0$，因此 $a=b=0$。兩個線性獨立向量位於二維空間，故構成基底。再解 $a+b=3$、$a-b=1$，得 $a=2$、$b=1$，所以

$$
(3,1)=2(1,1)+(1,-1),\qquad [(3,1)]_B=\begin{pmatrix}2\\1\end{pmatrix}.
$$

### 例題 7.6　黑板上的方法（一）：從獨立集合延伸基底

**用處**：題目先指定一些「一定要留在基底裡」的獨立向量時，加入 span 之外的新向量，直到整個空間被生成。

在 $\mathbb R^3$ 中，從 $S=\{(1,1,0),(0,1,1)\}$ 出發，找一組包含 $S$ 的基底。

**解**：令 $u_1=(1,1,0)$、$u_2=(0,1,1)$。它們線性獨立，因 $au_1+bu_2=0$ 的第一、第三座標分別給出 $a=b=0$。取 $e_1=(1,0,0)$。若 $e_1=au_1+bu_2=(a,a+b,b)$，第一、第三座標要求 $a=1,b=0$，第二座標卻變成 $1\ne0$，所以 $e_1\notin\mathrm{span}(S)$。因此加入 $e_1$ 後仍獨立；三個獨立向量位於三維空間，得到基底

$$
B=\{(1,1,0),(0,1,1),(1,0,0)\}.
$$

**對照黑板的停止條件**：此時 $\mathrm{span}(B)=\mathbb R^3$，停止。有限維保證持續加入獨立向量的過程最多進行 $\dim V$ 次。

### 例題 7.7　黑板上的方法（二）：從生成集縮減基底

**用處**：題目給了很多生成向量、其中有重複資訊時，逐一刪掉可由其他向量表示的向量。

設 $S=\{(1,0),(0,1),(1,1),(2,1)\}\subseteq\mathbb R^2$。從 $S$ 選出一組基底。

**解**：$(1,1)=(1,0)+(0,1)$，$(2,1)=2(1,0)+(0,1)$，故刪除這兩個向量不改變 span。留下的 $\beta=\{(1,0),(0,1)\}$ 線性獨立且生成 $\mathbb R^2$，所以是基底。

**對照黑板的停止條件**：對每個 $u\in S\setminus\beta$，$\beta\cup\{u\}$ 都線性相依，表示 $u\in\mathrm{span}(\beta)$。既然原本 $\mathrm{span}(S)=V$，便有 $\mathrm{span}(\beta)=V$。這項推論需要「原本 $S$ 生成 $V$」這個前提；如果不知道 $S$ 是否生成 $V$，只能保證 $\beta$ 是 $\mathrm{span}(S)$ 的基底。

### 例題 7.8　維度公式：兩個平面的和

**用處**：兩個子空間有重疊時，計算 $U+W$ 的維度要把重複算到的交集扣回來。

令 $U=\mathrm{span}\{e_1,e_2\}$、$W=\mathrm{span}\{e_2,e_3\}\subseteq\mathbb R^3$，求 $\dim(U+W)$。

**解**：$\dim U=\dim W=2$，交集為 $\mathrm{span}\{e_2\}$，維度是 $1$。所以 $\dim(U+W)=2+2-1=3$；也可直接看出 $U+W=\mathbb R^3$。

## 8. 考前速查與易錯處

| 想證明的事 | 直接使用的做法 |
| --- | --- |
| $W$ 是子空間 | 證明含 $0$，且對 $au+bv$ 封閉 |
| $S$ 生成 $V$ | 取任意 $v\in V$，實際寫出有限線性組合 |
| $S$ 線性獨立 | 設線性組合為 $0$，推得所有係數為 $0$ |
| $S$ 是基底 | 分別證明生成與獨立 |
| $V$ 中恰有 $\dim V$ 個向量 | 只需再證明生成或獨立其中一項 |

1. $\{0\}$ 是子空間，但 $\{0\}$ **不是**線性獨立集合；它的基底是 $\varnothing$。
2. $\mathrm{span}(S)$ 的元素是有限線性組合；不要把它和任意無限級數混在一起。
3. 基底給的是**唯一表示**；只會生成並不足以保證係數唯一。
4. 矩陣基底數量 $mn$ 由位置 $(i,j)$ 計算；$P_n(F)$ 包含常數項，共有 $n+1$ 個單項式。
5. 說多項式基底獨立時，比的是**係數**，不是只代入若干個數值。
