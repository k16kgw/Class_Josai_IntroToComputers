# ブール代数，論理演算，真理値表

到達目標
- 論理演算の基本となるブール代数および真理値表について理解する．

## 前回の復習

1. 次の計算結果を2進数で答えよ．
    - $(101)_2+(11)_2 = (1000)_2$
    - $(1.011)_2+(0.11)_2 = (10.001)_2$
    - $(\mathrm{A})_{16}+(\mathrm{C})_{16} = (16)_{16}$
2. 次の数を2進数に基数変換せよ．
   - $(9)_{10} = (1001)_{2}$
   - $(54)_{10} = (110110)_{2}$
   - $(\mathrm{F})_{16} = (1111)_{2}$
   - $(1\mathrm{A})_{16} = (11010)_{2}$
3. 次の数を10進数に基数変換せよ．
   - $(1111)_{2} = (15)_{10}$
   - $(2\mathrm{C})_{16} = (44)_{16}$
   - $(10)_{16} = (16)_{10}$
4. 2進数で4桁までしか表せないものとする．このとき $(101)_{2} - (11)_{2}$ を $(11)_{2}$ の補数を用いた足し算で計算せよ．

    $(11)_{2}$ の補数は $(1101)_{2}$ である．

    $$
    (101)_{2} + (1101)_{2} = (10010)_{2}
    $$

    であるから，繰り上がった項を無視して

    $$
    (101)_{2} - (11)_{2} = (10)_{2}
    $$


## ブール代数

ブール代数：`0`と`1`（または偽と真）の2つの値だけを使って論理を扱う数学的な枠組み．

### 基本記号と演算

- 変数を $A,B,C$ とし，これらは`0`か`1`の値しか取らない．
- 基本的な演算は次の3つ
  - 否定（NOT）：$\lnot A$，<span style="color:red">$\overline{A}$</span>
  - 論理積（AND）：$A \land B$，<span style="color:red">$A\cdot B$</span>，$AB$
  - 論理和（OR）：$A \lor B$，<span style="color:red">$A + B$</span>
  - 演算の順序は`()`，`・`，`+`の順．
- これらを組み合わせて，他に次の演算を定義できる．
  - 排他的論理和（XOR）：$A \oplus B$
  - 否定論理和（NOR）：$\overline{A+B}$
  - 否定論理積（NAND）：$\overline{A\cdot B}$

これらの演算がどのような論理を表しているかは**真理値表**で定義される．
幾何学的なイメージで理解するのであれば，**ベン図**を描くと良い．

- 真理値表：入力の全てのパターンとそれに対する結果の値を表にしたもの．全てのパターンを列挙しているため，これで関数を定義することができる．

| A | B | $\overline{A}$ | $A \cdot B$ | $A + B$   | $A\oplus B$ | $\overline{A+B}$ | $\overline{A \cdot B}$ |
| - | - | ---------      | ----------  | --------- | ----------- | -----------      | -----------            |
| 0 | 0 |    1           |     0       |    0      |     0       |     1            |    1                   |
| 0 | 1 |    1           |     0       |    1      |     1       |     0            |    1                   |
| 1 | 0 |    0           |     0       |    1      |     1       |     0            |    1                   |
| 1 | 1 |    0           |     1       |    1      |     0       |     0            |    0                   |

### 公理

| 名前    | 内容                   |
| ---    | ---                    |
| 単位元  | $A+0=A$ <br> $A \cdot 1=A$ |
| 交換則  | $A+B=B+A$ <br> $A \cdot B = B \cdot A$ |
| 結合則  | $(A+B)+C=A+(B+C)$ <br> $(A \cdot B) \cdot C=A \cdot (B \cdot C)$ |
| 分配則  | $A \cdot (B+C) = A \cdot B + A \cdot C$ <br> <span style="color:red">$A+B \cdot C = (A+B) \cdot (A+C)$</span> |
| 補元    | $A+\overline{A}=1$ <br> $A\cdot\overline{A}=0$ |

### 基本定理（よく使う等式）

| 名前    | 内容                   |
| ---    | ---                    |
| 冪等則（べきとうそく，巾等則） | $A+A=A$ <br> $A \cdot A=A$ |
| 帰無則 | $A + 1 = 1$ <br> $A \cdot 0 = 0$ |
| 復元則 | $\overline{\overline{A}}=A$ |
| 吸収則 | $A+A \cdot B=A$ <br> $A \cdot (A+B)=A$ <br> $A+\overline{A} \cdot B=A + B$ <br> $A \cdot (\overline{A}+B)=A \cdot B$ |
| ド・モルガンの法則（De Morgan's laws） | $\overline{A+B}=\overline{A} \cdot \overline{B}$ <br> $\overline{A \cdot B}=\overline{A}+\overline{B}$
| 合意定理（consensus theorem） | $A \cdot B + \overline{A} \cdot C + B \cdot C = A \cdot B + \overline{A} \cdot C$

- 論理式の簡略化に当たって，公理と基本定理を活用して式変形を行う．

```{tip}
**例**

合意定理 $A \cdot B + \overline{A} \cdot C + B \cdot C = A \cdot B + \overline{A} \cdot C$ を示す．

<u>証明</u>

取り得る値が`0`か`1`しかないため，真理値表を作成するだけでも証明になる．

**方法1（真理値表の作成）**

| A | B | C | 左辺（$A \cdot B + \overline{A} \cdot C + B \cdot C$） | 右辺（$A \cdot B + \overline{A} \cdot C$） |
| - | - | - | ----------  | --------- |
| 0 | 0 | 0 |     |     |
| 0 | 0 | 1 |     |     |
| 0 | 1 | 0 |     |     |
| 0 | 1 | 1 |     |     |
| 1 | 0 | 0 |     |     | 
| 1 | 0 | 1 |     |     | 
| 1 | 1 | 0 |     |     | 
| 1 | 1 | 1 |     |     | 

<br>

**方法2（式変形）**

$A+\overline{A} = 1$より

$$
B \cdot C = B \cdot C \cdot (A+\overline{A}) = A\cdot B \cdot C + \overline{A} \cdot B \cdot C.
$$

ここで吸収則より

$$
A \cdot B + A \cdot B \cdot C = A \cdot B,
\\
\overline{A} \cdot B + \overline{A} \cdot B \cdot C = \overline{A} \cdot B.
$$

従って右辺を変形すれば左辺を得る．
```

### 双対性の原理 （Principle of Duality）

- 双対：<span style="color:red">$0 \leftrightarrow 1$</span> と <span style="color:red">$+ \leftrightarrow \cdot$</span> を同時に入れ替える手続きによって得られる論理式．
- 例
  - $A+0=A$ の双対は $A\cdot 1=A$．
  - 分配則 $A+B \cdot C=(A+B)\cdot(A+C)$ の双対は，もう一方の分配則 $A\cdot(B+C)=A \cdot B+A \cdot C$．

```{note}
**演習1**

1. $A+\overline{A} \cdot B = A+B$ を示せ．
2. 上式の双対を求めよ。
```

## 論理式の簡略化

- 簡略化：少ない項数，少ない論理積，少ない論理和で等価な論理式を導くこと．
- 簡略化によって，実際に回路を実装する際の面積・遅延・消費電力の削減に直結する．
- 補元・吸収則・合意定理などで項を減らすことを目指す．

```{tip}
**例**：
$F(A,B)= A\overline{B} + A\cdot B$ を簡略化する．

次のように因数分解できる．

$$
F=A \cdot (\overline{B}+B)=A\cdot 1= A
$$
```

```{tip}
**例**：
$F= A \cdot B + A \cdot \overline{B} \cdot C + A \cdot B \cdot \overline{C}$を簡略化する．

吸収則より

$$
A \cdot B + A \cdot \overline{B} \cdot C + A \cdot B \cdot \overline{C}
= A \cdot B + A \cdot \overline{B} \cdot C
$$

因数分解して吸収則を適用すれば

$$
A \cdot B + A \cdot \overline{B} \cdot C
= A \cdot (B + \overline{B} \cdot C)
= A \cdot (B + C).
$$
```

```{note}
**演習2**

1. $\overline{A+B+C}$ をド・モルガンの法則に従い展開せよ。
2. $A \cdot B + \overline{A} \cdot C + B \cdot C$ を簡略化せよ。
```

## 復習

```{note}
**復習**

1. 否定論理積（NAND）の真理値表を作成すること．
2. 吸収則，ド・モルガンの法則，合意定理が主張する論理式を書き下すこと．
3. 本日学んだことを3つ箇条書きで挙げること．
```


