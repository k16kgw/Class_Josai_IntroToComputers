# 主加法標準形，主乗法標準形，論理ゲート

到達目標
- 論理式の標準形である主加法標準形と主乗法標準形，及び論理ゲートについて理解する．

今日の問い
1. 主加法標準形とは何か
2. 主乗法標準形とは何か
3. 論理ゲートにはどのような種類があるか

キーワード
- 主加法標準形
- 主乗法標準形
- 論理ゲート

## 復習

1. 基本的な演算（論理否定・論理和・論理積）の定義（真理値表）

| A | B | $\overline{A}$ | $A \cdot B$ | $A + B$   |
|:-:|:-:| :---------:    | :--------:  | :-------: |
| 0 | 0 |    1           |     0       |    0      |
| 0 | 1 |    1           |     0       |    1      |
| 1 | 0 |    0           |     0       |    1      |
| 1 | 1 |    0           |     1       |    1      |

2. 否定論理和 (NOR) と否定論理積 (NAND) の真理値表は上を元に次のように書ける．

| A | B | $\overline{A+B}$ | $\overline{A \cdot B}$ |
|:-:|:-:| :---------:      | :--------:             |
| 0 | 0 |     1            |    1                   |
| 0 | 1 |     0            |    1                   |
| 1 | 0 |     0            |    1                   |
| 1 | 1 |     0            |    0                   |

3. $\overline{A+B+C}$ をド・モルガンの法則に基づいて展開する．

## 論理関数

論理関数：論理変数を論理演算で結びつけたもの．

### 論理関数の表現

| 用語 | 意味 |
| --- | --- |
| 加法標準形 | 論理変数の論理積の論理和 |
| 乗法標準形 | 論理変数の論理和の論理積 |
| 最小項 (min term) | 使用する全ての論理変数またはその否定の<span style="color:red">論理積</span> |
| 最大項 (max term) | 使用する全ての論理変数またはその否定の<span style="color:red">論理和</span> |

| 用語 | 意味 | 例 |
| --- | --- | --- |
| 主加法標準形<br>(sum of products) | 最小項の論理和 | $\mathrm{A\cdot B \cdot C + A \cdot \overline{B} \cdot C + A \cdot \overline{B} \cdot \overline{C}}$ |
| 主乗法標準形<br>(product of sums) | 最大項の論理積 | $\mathrm{(A+B+C)\cdot(A+B+\overline{C})\cdot(\overline{A}+B+C)\cdot(\overline{A}+\overline{B}+C)}$ |

### 構成方法

- **主加法標準形** ← 出力が1となる行の**最小項**の和
- **主乗法標準形** ← 出力が0となる行の**最大項**の積

```{tip}
論理変数 $F=F(A,B,C)$ の真理値表が下表のようになっており，$F(A,B,C)=1$ となる行が (001, 010, 110, 111)のとき，$F$ の主加法標準形と主乗法標準形は次のように表される．
また，0となる行は (000, 011, 100, 101) である．

| A | B | C | $F(A,B,C)$ |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

- 主加法標準形：$F = \overline{A} \cdot \overline{B} \cdot C + \overline{A} \cdot B \cdot \overline{C} + A \cdot B \cdot \overline{C} + A \cdot B \cdot C$
- 主乗法標準形：$F = (A+B+C) \cdot (A+\overline{B}+\overline{C}) \cdot (\overline{A}+B+C) \cdot (\overline{A}+B+\overline{C})$
```

```{note}
**演習1**

1. 次の真理値表を満たす論理変数 $F=F(A,B)$ の主加法標準形と主乗法標準形を求めよ．

| A | B | $F(A,B)$ |
|:-:|:-:|:-:|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

2. 次の真理値表を満たす論理変数 $G=G(A,B)$ の主加法標準形と主乗法標準形を求めよ．

| A | B | C | $G(A,B)$ |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 0 |
```

## 完備性

ある論理関数の組み合わせ$X$が<span style="color:red">完備性</span>を有す：任意の論理関数を$X$の論理関数の組み合わせで表現可能であること

```{tip}
**例**

基本論理関数の組み $\{\text{AND, OR, NOT}\}$ は完備性を有す．

ド・モルガンの法則より $A+B = \overline{\overline{A}\cdot\overline{B}}$ であるから $\{\text{OR}\}$ は $\{\text{AND, NOT}\}$ の組みに置き換えることができる．
従って論理関数の組み $\{\text{AND, NOT}\}$ は完備性を有す．

一方で $A \cdot B = \overline{\overline{A}+\overline{B}}$ であるから $\{\text{AND}\}$ は $\{\text{OR, NOT}\}$ の組みに置き換えることができ，論理関数の組み $\{\text{OR, NOT}\}$ は完備性を有す．
```

- 否定論理積 (NAND) は完備性を有す．つまり<span style="color:red">否定論理積のみの組み合わせで全ての論理関数を表現することができる</span>．
- 否定論理和 (NOR) は完備性を有す．つまり<span style="color:red">否定論理和のみの組み合わせで全ての論理関数を表現することができる</span>．

論理積・論理和・論理否定 (AND・OR・NOT) は，次のように否定論理積 (NAND) のみの組み合わせで表現できる．

- $A \cdot B = \overline{(\overline{A \cdot B})\cdot(\overline{A \cdot B})}$
- $A + B = \overline{(\overline{A \cdot A})\cdot(\overline{B \cdot B})}$
- $\overline{A} = \overline{A \cdot A}$

```{note}
**演習2**

論理積・論理和・論理否定を否定論理積の組みで表現した次式において，右辺を式変形あるいは右辺の真理値表を作成して，左辺に一致することを確かめよ．

- $A \cdot B = \overline{(\overline{A \cdot B})\cdot(\overline{A \cdot B})}$
- $A + B = \overline{(\overline{A \cdot A})\cdot(\overline{B \cdot B})}$
- $\overline{A} = \overline{A \cdot A}$
```

論理積・論理和・論理否定 (AND・OR・NOT) は，次のように否定論理和 (NOR) のみの組み合わせで表現できる．

- $A \cdot B = \overline{(\overline{A + A})+(\overline{B + B})}$
- $A + B = \overline{(\overline{A + B})+(\overline{A + B})}$
- $\overline{A} = \overline{A + A}$

## 論理ゲート

- **論理ゲート** (logic gate)：基本的な論理演算機能を持つ論理回路
- MIL規格に基づくMIL記法では論理関数の論理ゲートは次のように図示される．

![論理ゲート一覧](/contents/figs/3/logic.png)

### 論理回路の構成

```{tip}
**例**

論理式$X = A + (B \cdot C) + C$を実現する論理回路は次のように構成される．

![例](/contents/figs/3/eg1.png)
```

```{tip}
**例**

論理式$X = A + (A \cdot B)$を実現する論理回路をNANDゲートのみを用いて構成する．

$$
\begin{align}
X &= A + (A \cdot B)\\
&= \overline{(\overline{A \cdot A})\cdot(\overline{(A \cdot B) \cdot (A \cdot B)})}\\
&= \overline{(\overline{A \cdot A})\cdot(\overline{(\overline{(\overline{A \cdot B})\cdot(\overline{A \cdot B})}) \cdot (\overline{(\overline{A \cdot B})\cdot(\overline{A \cdot B})})})}
\end{align}
$$

であるから

![論理式$X$を実現する論理回路の構成](/contents/figs/3/eg2.png)
```

```{note}
**演習3**

次の論理式を実現する論理回路について

$$
X = (A \cdot B) + (B \cdot C)
$$

1. ANDゲートとORゲートを用いて構成せよ．
2. NANDゲートのみを用いて構成せよ．
```

<!-- - 加法標準形はNANDゲートのみで表現することが可能である． -->
<!-- - 乗法標準形はNORゲートのみで表現することが可能である． -->

### 加法標準形と乗法標準形との変換

次の分配則に基づいて展開すれば良い．

- $A \cdot (B+C) = A \cdot B + A \cdot C$
- $A+B \cdot C = (A+B) \cdot (A+C)$

```{tip}
**例**

加法標準形 $(A \cdot B) + (A \cdot \overline{B})$ を分配則 $A+B \cdot C = (A+B) \cdot (A+C)$ に従って展開すると

$$
\begin{align}
(A \cdot B) + (A \cdot \overline{B})
&= ((A \cdot B) + A) \cdot ((A \cdot B) + \overline{B})\\
&= ((A + A) \cdot (A + B)) \cdot ((A + \overline{B}) \cdot (B + \overline{B}))\\
&= (A \cdot (A+B)) \cdot (A + \overline{B})\\
&= A \cdot (A+B) \cdot (A + \overline{B})
%&= A \cdot (A + \overline{B})\\
%&= A
\end{align}
$$

乗法標準形 $(A + B) \cdot (A + \overline{B})$ を分配則 $A \cdot (B + C) = (A \cdot B) + (A \cdot C)$ に従って展開すると

$$
\begin{align}
(A + B) \cdot (A + \overline{B})
&= ((A+B) \cdot A) + ((A+B) \cdot \overline{B})\\
&= ((A \cdot A) + (A \cdot B)) + ((A \cdot \overline{B}) + (B \cdot \overline{B}))\\
&= A + (A \cdot B) + (A \cdot \overline{B})
%&= A + (A \cdot \overline{B})
\end{align}
$$
```

## まとめ

### 復習

1. 「主加法標準形」と「主乗法標準形」との違いを説明してください．
2. AND・OR・NANDを表す論理ゲートの記号を書いてください．



