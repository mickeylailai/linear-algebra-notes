# 線性代數筆記：向量空間至基底與維度

> 範圍：Vector Spaces → Subspaces → Linear Combinations / Span → Linear Independence → Bases → Dimension。最後以課堂照片中的矩陣空間與多項式空間為例。本文為獨立撰寫的複習筆記；證明使用簡明英文，說明使用繁體中文。

[TOC]

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

### Theorem 1.2　零與負向量的基本性質

對任意 $a\in F$、$v\in V$：

$$
0_Fv=0_V,\qquad a0_V=0_V,\qquad (-1_F)v=-v,\qquad (-a)v=-(av).
$$

**Proof.** Since $(0_F+0_F)v=0_Fv+0_Fv$ and $(0_F+0_F)v=0_Fv$, cancellation gives $0_Fv=0_V$. Likewise, $a(0_V+0_V)=a0_V+a0_V=a0_V$, so $a0_V=0_V$. Now $v+(-1_F)v=(1_F-1_F)v=0_Fv=0_V$; hence $(-1_F)v=-v$. Finally, $av+(-a)v=(a-a)v=0_V$, so $(-a)v=-(av)$. $\square$

**重點提醒**：同一空間的零向量與加法反元素皆唯一。證明可分別假設有兩個零元 $z,z'$，寫出 $z=z+z'=z'$；反元素則對 $v+w=v+w'=0$ 兩側加上 $-v$。

## 2. Subspaces（子空間）

### Definition 2.1　子空間

$W\subseteq V$ 若沿用 $V$ 的運算後本身也是 $F$ 上的向量空間，就稱 $W$ 是 $V$ 的子空間（subspace）。

### Theorem 2.2　Subspace test

$W\subseteq V$ 是子空間，若且唯若 $W\ne\varnothing$，且對任意 $u,v\in W$、$a\in F$，有 $u+v\in W$ 與 $au\in W$。等價地，直接驗證 $0_V\in W$，且 $au+bv\in W$ 對所有 $u,v\in W$、$a,b\in F$ 成立。

**Proof.** If $W$ is a subspace, closure and nonemptiness follow from its vector-space axioms. Conversely, take $w\in W$. By scalar closure, $0_Fw=0_V\in W$ and $(-1_F)w=-w\in W$. All other axioms are inherited from $V$, so $W$ is a vector space. $\square$

**例 2.3**：$W=\{(x,y,z)\in\mathbb R^3:x+y+z=0\}$。若 $u,v\in W$，則其座標和皆為 $0$；$au+bv$ 的座標和仍為 $0$。故 $W$ 是子空間。

**反例**：$A=\{(x,y)\in\mathbb R^2:x+y=1\}$ 不含 $(0,0)$，故不是子空間。判定前先查零向量通常最快。

### Theorem 2.4　子空間的交集

若 $\{W_i\}_{i\in I}$ 是 $V$ 的一族子空間，則 $\bigcap_{i\in I}W_i$ 也是子空間（空指標集時交集約定為 $V$）。

**Proof.** Every $W_i$ contains $0_V$, so their intersection contains $0_V$. If $u,v$ belong to every $W_i$, then $au+bv$ belongs to every $W_i$. Apply the subspace test. $\square$

### Definition 2.5　和與直和

$$
U+W=\{u+w:u\in U,\ w\in W\}.
$$

若 $U,W$ 是子空間且 $U\cap W=\{0\}$，記 $U+W=U\oplus W$。此時其中每個向量都有唯一的 $u+w$ 表示。

### Theorem 2.6　子空間和、表示唯一性

$U+W$ 是子空間；且 $U+W$ 中的每個向量都能**唯一**表示成 $u+w$，若且唯若 $U\cap W=\{0\}$。

**Proof.** Since $0=0+0\in U+W$, the sum is nonempty. For $u_i\in U,w_i\in W$, we have $a(u_1+w_1)+b(u_2+w_2)=(au_1+bu_2)+(aw_1+bw_2)\in U+W$. Thus it is a subspace. If $u_1+w_1=u_2+w_2$, then $u_1-u_2=w_2-w_1\in U\cap W$. When this intersection is $\{0\}$, both differences vanish, giving uniqueness. Conversely, if $x\in U\cap W$, then $x=x+0=0+x$; uniqueness gives $x=0$. $\square$

**提醒**：$U\cup W$ 一般不是子空間。例如 $x$ 軸與 $y$ 軸的聯集，不含 $(1,1)=(1,0)+(0,1)$。

## 3. Linear Combinations and Span（線性組合與生成）

### Definition 3.1　線性組合與 span

有限多個 $v_1,\ldots,v_k\in V$ 的線性組合是 $a_1v_1+\cdots+a_kv_k$，其中 $a_i\in F$。對任意集合 $S\subseteq V$，

$$
\mathrm{span}(S)=\left\{\sum_{i=1}^k a_iv_i:k\ge0,\ a_i\in F,\ v_i\in S\right\}.
$$

允許 $k=0$，空和就是 $0_V$。即使 $S$ 是無限集合，每個線性組合也**只用有限多項**。若 $\mathrm{span}(S)=V$，稱 $S$ 生成（spans）$V$。

### Theorem 3.2　span 是最小子空間

$\mathrm{span}(S)$ 是包含 $S$ 的子空間；任何包含 $S$ 的子空間 $W$ 都包含 $\mathrm{span}(S)$。

**Proof.** The empty sum belongs to $\mathrm{span}(S)$. Sums and scalar multiples of finite linear combinations are still finite linear combinations; hence it is a subspace. Each $s\in S$ equals $1s$, so $S\subseteq\mathrm{span}(S)$. If $W$ is a subspace containing $S$, its closure under addition and scalar multiplication puts every finite linear combination of elements of $S$ in $W$. Thus $\mathrm{span}(S)\subseteq W$. $\square$

### Theorem 3.3　加入已在 span 中的向量不改變 span

若 $w\in\mathrm{span}(S)$，則 $\mathrm{span}(S\cup\{w\})=\mathrm{span}(S)$。

**Proof.** Since $S\subseteq S\cup\{w\}$, we have $\mathrm{span}(S)\subseteq\mathrm{span}(S\cup\{w\})$. Since $\mathrm{span}(S)$ is a subspace containing $S\cup\{w\}$, minimality gives the reverse inclusion. $\square$

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

**Proof.** (1) The equation $1\cdot0_V=0_V$ is a nontrivial dependence relation. (2) If $\sum_{i=1}^k a_iv_i=0$ is nontrivial, choose $j$ with $a_j\ne0$. Since $F$ is a field, $a_j^{-1}$ exists and $v_j=-\sum_{i\ne j}(a_i/a_j)v_i$. Conversely, move such a representation to one side to obtain a nontrivial relation. (3) A nontrivial relation among vectors in a subset would also be a relation in the original set; the dependent case follows by retaining its finite relation in the larger set. $\square$

### Theorem 4.3　獨立組的表示唯一

若 $S=\{v_1,\ldots,v_k\}$ 線性獨立，則 $\mathrm{span}(S)$ 中每個向量相對於這組向量的係數唯一。

**Proof.** Suppose $\sum_i a_iv_i=\sum_i b_iv_i$. Then $\sum_i(a_i-b_i)v_i=0$. Linear independence gives $a_i-b_i=0$ for each $i$. $\square$

**提醒**：要檢查「是否獨立」，必須從**等於零的線性組合**開始；只找到某個向量可表示為線性組合，是用來證明「相依」。

## 5. Bases（基底）

### Definition 5.1　基底

$B\subseteq V$ 是 $V$ 的基底（basis），若 $B$ 同時線性獨立且 $\mathrm{span}(B)=V$。零空間 $\{0\}$ 的基底是空集合。

### Theorem 5.2　基底與唯一座標

$B=\{v_1,\ldots,v_n\}$ 是 $V$ 的基底，若且唯若每個 $v\in V$ 都能**唯一**寫成 $v=a_1v_1+\cdots+a_nv_n$。此時 $[v]_B=(a_1,\ldots,a_n)^T$ 稱為座標向量；座標需先指定基底的**順序**。

**Proof.** If $B$ is a basis, spanning gives existence and Theorem 4.3 gives uniqueness. Conversely, existence implies spanning. If $\sum_i c_iv_i=0$ and some $c_i\ne0$, the zero vector has both the all-zero representation and a distinct representation, contradicting uniqueness. Thus $B$ is linearly independent. $\square$

### Theorem 5.3　基底的極小／極大特徵

基底既是**極小生成集**（移除任何一個向量就不再生成），也是**極大線性獨立集**（加入任何一個基底外的向量就相依）。反過來，在 $V$ 中，極小生成集或極大線性獨立集也都是基底。

**Proof.** Let $B$ be a basis. If $B\setminus\{b\}$ still spanned $V$, then $b$ would be a linear combination of other elements of $B$, contradicting independence. If $v\notin B$, spanning expresses $v$ as a finite linear combination of elements of $B$, so $B\cup\{v\}$ is dependent. Conversely, a minimal spanning set cannot be dependent: a nontrivial dependence lets us remove one member without changing its span. A maximal independent set must span: otherwise choose $v\notin\mathrm{span}(B)$; a dependence in $B\cup\{v\}$ would force $v\in\mathrm{span}(B)$, a contradiction. $\square$

### Example 5.4　矩陣空間的標準基底（課堂照片）

對 $1\le i\le m$、$1\le j\le n$，定義 $E^{ij}\in M_{m\times n}(F)$：

$$
(E^{ij})_{k\ell}=\begin{cases}1_F,&(k,\ell)=(i,j),\\0_F,&\text{otherwise}.\end{cases}
$$

**Theorem.** $\mathcal E=\{E^{ij}:1\le i\le m,\ 1\le j\le n\}$ 是 $M_{m\times n}(F)$ 的基底。

**Proof — spanning.** Let $A=(a_{ij})\in M_{m\times n}(F)$. By comparing entries, $A=\sum_{i=1}^m\sum_{j=1}^n a_{ij}E^{ij}$. Thus $\mathcal E$ spans the matrix space.

**Proof — independence.** Suppose $\sum_{i=1}^m\sum_{j=1}^n c_{ij}E^{ij}=0$. The $(k,\ell)$ entry on the left equals $c_{k\ell}$, while the corresponding entry on the right is $0_F$. Hence $c_{k\ell}=0_F$ for every $(k,\ell)$. Therefore $\mathcal E$ is linearly independent, so it is a basis. $\square$

**繁中理解**：每個 $E^{ij}$ 只管一個位置；要拼出 $A$，就把第 $(i,j)$ 個位置的數字 $a_{ij}$ 乘上對應的 $E^{ij}$ 再相加。

### Example 5.5　多項式空間的標準基底（課堂照片）

**Theorem.** 對 $n\ge0$，$\mathcal P_n=\{1,x,x^2,\ldots,x^n\}$ 是 $P_n(F)$ 的基底。

**Proof — spanning.** Let $f\in P_n(F)$. By definition, there are $a_0,\ldots,a_n\in F$ such that $f=a_0+a_1x+\cdots+a_nx^n$; for the zero polynomial, take all $a_i=0$. Hence $f\in\mathrm{span}(\mathcal P_n)$.

**Proof — independence.** Suppose $c_0+c_1x+\cdots+c_nx^n=0$ as a **polynomial identity**. Equality of formal polynomials means equality of corresponding coefficients. Thus $c_0=c_1=\cdots=c_n=0$, so $\mathcal P_n$ is linearly independent. Therefore it is a basis. $\square$

**重要細節**：此處比較的是**形式多項式的係數**，不能把「在有限體 $F$ 的每個點代入都得到 $0$」直接當成同一件事。例如在 $F_2$ 上，$x^2-x$ 是非零形式多項式，卻在 $F_2$ 的兩個點都取值 $0$。

## 6. Dimension（維度）與有限維定理

### Definition 6.1　有限維與維度

若 $V$ 有一個有限基底，則稱 $V$ 為有限維；任一有限基底中的向量個數稱為 $\dim V$。以下定理保證此數字不依基底的選擇而改變。$\dim\{0\}=0$。

### Lemma 6.2　Replacement / exchange lemma（替換引理）

若 $V$ 由 $n$ 個向量 $w_1,\ldots,w_n$ 生成，而 $v_1,\ldots,v_k$ 線性獨立，則 $k\le n$；並且可依序把 $k$ 個 $w_i$ 換成 $v_1,\ldots,v_k$，仍保持生成 $V$。

**Proof.** Initially the $w_i$ span $V$. Suppose after $r-1$ replacements the list $v_1,\ldots,v_{r-1},w_r,\ldots,w_n$ still spans $V$. Express $v_r$ using this list. At least one coefficient of $w_r,\ldots,w_n$ is nonzero; otherwise $v_r\in\mathrm{span}\{v_1,\ldots,v_{r-1}\}$, contrary to independence. Solve for that $w_i$ and replace it with $v_r$. The new list still spans $V$. This requires an unremoved $w_i$ at every step; hence $k\le n$. $\square$

### Theorem 6.3　所有有限基底等長

若 $B$、$C$ 是 $V$ 的兩個有限基底，則 $|B|=|C|$。

**Proof.** Since $B$ is independent and $C$ spans, Lemma 6.2 gives $|B|\le|C|$. Interchanging their roles gives $|C|\le|B|$. Hence they have the same size. $\square$

### Theorem 6.4　基底延伸與生成集縮減

若 $\dim V=n$：

1. 每個線性獨立的有限集合都可延伸為 $V$ 的基底。
2. 每個有限生成集都可刪去多餘向量，縮減為 $V$ 的基底。
3. 若恰有 $n$ 個向量，則**線性獨立**與**生成 $V$** 任一條件成立，就足以保證它們是基底。

**Proof.** Start with an independent set $S$. If it does not span $V$, choose $v\notin\mathrm{span}(S)$. Then $S\cup\{v\}$ stays independent: a dependence with a nonzero coefficient of $v$ would put $v$ in $\mathrm{span}(S)$. Lemma 6.2 bounds the size by $n$, so this process ends with a basis. For a finite spanning set, whenever it is dependent, remove a vector expressible by the others; Theorem 3.3 preserves its span. The process ends with an independent spanning set. Finally, an independent set of size $n$ can be extended to a basis but no extra vector can be added, since all bases have size $n$. A spanning set of size $n$ can be reduced to a basis but no vector can be removed. $\square$

### Corollary 6.5　常見空間的維度

$$
\dim F^n=n,\qquad \dim M_{m\times n}(F)=mn,\qquad \dim P_n(F)=n+1.
$$

**Proof.** The standard coordinate vectors form a basis of $F^n$; Example 5.4 supplies $mn$ basis matrices; Example 5.5 supplies $n+1$ monomials. $\square$

### Theorem 6.6　子空間和的維度公式

對有限維空間 $V$ 的子空間 $U,W$：

$$
\dim(U+W)=\dim U+\dim W-\dim(U\cap W).
$$

特別地，若 $U\cap W=\{0\}$，則 $\dim(U\oplus W)=\dim U+\dim W$。

**Proof.** Choose a basis $b_1,\ldots,b_r$ of $U\cap W$. Extend it to a basis $b_1,\ldots,b_r,u_1,\ldots,u_p$ of $U$ and to a basis $b_1,\ldots,b_r,w_1,\ldots,w_q$ of $W$. Their union spans $U+W$. For independence, suppose $\sum_i\alpha_i b_i+\sum_j\beta_j u_j+\sum_k\gamma_k w_k=0$. Then $\sum_k\gamma_k w_k=-\sum_i\alpha_i b_i-\sum_j\beta_j u_j\in U\cap W$. Independence of the basis of $W$ forces every $\gamma_k=0$. Independence of the basis of $U$ then forces all $\alpha_i,\beta_j=0$. Thus the union is a basis with $r+p+q=(r+p)+(r+q)-r$ vectors. $\square$

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
