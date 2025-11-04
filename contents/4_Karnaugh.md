# カルノー図による組合せ回路の設計法

到達目標
- 組合せ回路の設計法としてカルノー図を用いる手法を理解する．

今日の問い
- 与えられた論理式を簡略化して論理回路に実装する手続きはどのようなものか

キーワード
- カルノー図（Karnaugh map）
- グレイコード
- 論理式の簡略化

## 復習（第3回）

| 用語 | 意味 | 例 |
| --- | --- | --- |
| 最小項 (min term) | 使用する全ての論理変数またはその否定の<span style="color:red">論理積</span> |
| 最大項 (max term) | 使用する全ての論理変数またはその否定の<span style="color:red">論理和</span> |
| 主加法標準形 (sum of products) | 最小項の論理和 |
| 主乗法標準形 (product of sums) | 最大項の論理積 |

- **主加法標準形** ← 出力が1となる行の**最小項**の和
- **主乗法標準形** ← 出力が0となる行の**最大項**の積

```{tip}
**例**

次の真理値表で与えられる論理変数$F$を主加法標準形・主乗法標準形で表すと，

| A | B | C | $F(A,B,C)$ |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 |

$$
F = (\overline{A} \cdot \overline{B} \cdot \overline{C})
 + (\overline{A} \cdot \overline{B} \cdot C)
 + (\overline{A} \cdot B \cdot C)
 + (A \cdot \overline{B} \cdot C)
 + (A \cdot B \cdot C)
$$

$$
F = (A+\overline{B}+C)
 \cdot(\overline{A}+B+C)
 \cdot(\overline{A}+\overline{B}+\overline{C})
$$
```

```{note}
**第3回演習3 - 解答例**

次の論理式を実現する論理回路について

$$
X = (A \cdot B) + (B \cdot C)
$$

1. ANDゲートとORゲートを用いて構成せよ．

![1の解答例](/contents/figs/4/old3-1.png)

2. NANDゲートのみを用いて構成せよ．

$$
X &= (A \cdot B) + (B \cdot C) = \overline{\overline{(A \cdot B) + (B \cdot C)}}
\\
&= \overline{\overline{(A \cdot B)} \cdot \overline{(B \cdot C)}}
$$

![2の解答例](/contents/figs/4/old3-2.png)
```

- 標準形は**正しいが冗長**になりがち → 簡略化する方法の一つが<span style="color:red">カルノー図</span>

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

## カルノー図 (Karnaugh map)

- **カルノー図**：論理回路を簡単化するための図表

### グレイコード配置

カルノー図では<span style="color:red">グレイコード配置</span>に従って表を作成する．

- **ハミング距離**：同じ長さのビット列について，同じ位置の符号が異なってる箇所の数．
  - 例：`01`と`00`のハミング距離は1
  - 例：`010101`と`001001`のハミング距離は2

- **グレイコード配置**：前後に隣接する符号間のハミング距離が必ず1となるような，数値の符号化法．
  - 2変数：行を$A=0,1$，列を$B=0,1$とする．
    <!-- ![2変数の場合のKarnaugh図の描き方](/contents/figs/4/Karnaugh_AB.png) -->
    <img src="./figs/Karnaugh_AB.png" width="50%">
  - 3変数：行を$A=0,1$，列を$BC=00,01,11,10$とする．$BC$の**隣接は1ビット差**が原則．
    ![3変数の場合のKarnaugh図の描き方](/contents/figs/4/Karnaugh_ABC.png)
  - 4変数：行を$AB=00,01,11,10$，列を$CD=00,01,11,10$とする．
    ![4変数の場合のKarnaugh図の描き方](/contents/figs/4/Karnaugh_ABCD.png)
  - 四辺は**周期的に隣接**している（上下・左右・四隅も隣接）．

### カルノー図の描き方

- 与えられた論理式が**加法標準形**か**乗法標準形**かで分類する．

加法標準形の場合
1. 主加法標準形に変換する．
2. 各最小項に対応する区画に1を入れる．

乗法標準形の場合
1. 加法標準形に変換する．（分配則）
2. 以下，加法標準形の場合と同様．

```{tip}
**例**

次の論理式$F$のカルノー図を作成する．

$$
F = \overline{A} \cdot B \cdot C
 + A \cdot B \cdot \overline{C}
 + \overline{A} \cdot B \cdot \overline{C}
 + A \cdot C
$$

1. 加法標準形なので主加法標準形に変換する．
$A \cdot C = A \cdot (B+\overline{B}) \cdot C = A \cdot B \cdot C + A \cdot \overline{B} \cdot C$であるから，

$$
F = \overline{A} \cdot B \cdot C
 + A \cdot B \cdot \overline{C}
 + \overline{A} \cdot B \cdot \overline{C}
 + A \cdot B \cdot C 
 + A \cdot \overline{B} \cdot C
$$

2. カルノー図は

![例1](/contents/figs/4/eg1.png)
```

```{note}
**演習1**

次の論理式$G$のカルノー図を作成せよ．

$$
G = \overline{A} \cdot B \cdot \overline{C} \cdot D
 + \overline{A} \cdot B \cdot C
 + A \cdot B \cdot C \cdot \overline{D}
 + A \cdot B \cdot D
$$
<!-- 
1. 加法標準形なので主加法標準形に変換する．

    $$
    \begin{align}
    G &= \overline{A} \cdot B \cdot \overline{C} \cdot D
    + \overline{A} \cdot B \cdot C
    + A \cdot B \cdot C \cdot \overline{D}
    + A \cdot B \cdot D
    \\
    &= \overline{A} \cdot B \cdot \overline{C} \cdot D
    + \overline{A} \cdot B \cdot C \cdot D
    + \overline{A} \cdot B \cdot C \cdot \overline{D}
    + A \cdot B \cdot C \cdot \overline{D}
    \\
    &\quad + A \cdot B \cdot C \cdot D
    + A \cdot B \cdot \overline{C} \cdot D
    \end{align}
    $$

2. カルノー図は

![演習1](/contents/figs/4/exc1.png)
-->
```

### カルノー図を用いた論理式の簡略化

1. 与えられた論理式のカルノー図を作成する．（前節）
2. 1の区画をなるべく大きいグループで区分けする．
   - グループは含む区画の数が **2の冪（1,2,4,8,16）** となるような，長方形または正方形をした区画のまとまり
3. グループの大きさを順に小さくし，区分けされなかった区画を含むようにグループによる区分けを行う．ただし，区画は複数のグループに属しても良い．
4. 得られたグループを表す論理式の和として元の論理式の簡略化が得られる．

```{warning}
グループによる区分けは一意ではなく，複数の区分けの仕方が存在する．
```

```{tip}
1以外の区画（0の区画）をグループで区分けすると，乗法標準形としての表現を得る．
```

```{tip}
**例**

論理式
$F = \overline{A} \cdot B \cdot C + A \cdot B \cdot \overline{C} + \overline{A} \cdot B \cdot \overline{C} + A \cdot C$
のカルノー図は次のように描ける．

![例1](/contents/figs/4/eg1.png)

このとき論理式$F$の簡略化を試みる．
このカルノー図は例えば次のように区分けでき，対応する論理式の和として簡略化できる．

![例2](/contents/figs/4/eg2.png)

従って，$F = A \cdot C + B$となる．
```

```{note}
**演習2**

演習1で作成した，論理式
$G = \overline{A} \cdot B \cdot \overline{C} \cdot D + \overline{A} \cdot B \cdot C + A \cdot B \cdot C \cdot \overline{D} + A \cdot B \cdot D$
のカルノー図を元に，この論理式$G$の簡略化を試みよ．
<!-- 
カルノー図は次のように区分けできる．

![演習2](/contents/figs/4/exc2.png)

従って，$G = B \cdot C + B \cdot D = B \cdot (C + D)$となる．
 -->
```

### 簡略化した論理式を用いたNAND回路の構成

1. 簡略化した論理式に2重否定を施し，内側の否定についてド・モルガンの法則を適用する．

```{tip}
**例**

論理式
$F = \overline{A} \cdot B \cdot C + A \cdot B \cdot \overline{C} + \overline{A} \cdot B \cdot \overline{C} + A \cdot C$
は
$F = A \cdot C + B$
と簡略化できたが，これをNAND回路として実装する．

右辺の二重否定を取り，ド・モルガンの法則に従って展開すれば

$$
F &= A \cdot C + B
\\
&= \overline{\overline{A \cdot C + B}}
\\
&= \overline{\overline{A \cdot C} \cdot \overline{B}}
$$

これを論理回路に実装すれば次のようになる．

![例3](/contents/figs/4/eg3.png)
```

```{note}
**演習3**

論理式
$G = \overline{A} \cdot B \cdot \overline{C} \cdot D + \overline{A} \cdot B \cdot C + A \cdot B \cdot C \cdot \overline{D} + A \cdot B \cdot D$
は
$G = B \cdot C + B \cdot D = B \cdot (C + D)$
と簡略化できたが，これをNAND回路として実装せよ．
<!-- 
$G = B \cdot C + B \cdot D$の二重否定を取り，ド・モルガンの法則に従って展開すれば

$$
G &= B \cdot C + B \cdot D
\\
&= \overline{\overline{B \cdot C + B \cdot D}}
\\
&= \overline{\overline{B \cdot C} \cdot \overline{B \cdot D}}
$$

これを論理回路に実装すれば次のようになる．

![演習3](/contents/figs/4/exc3.png)
 -->
```

<!-- 
## 5. K-map → ゲート実装（後半その2）

- SOP 最小形 → **NAND–NAND** 実装が直結。
- POS 最小形 → **NOR–NOR** 実装が直結。
- 実装時の注意：ファンイン制約、配線のうねり、等長化の必要性。

```{tip}
**手を動かす⑥（10分）**
- 手を動かす③で得た最小形 \(F=C(A+B)\) を  
  1) NAND–NAND、2) NOR–NOR でブロック図化し、段数と推定遅延を比較せよ。
```
-->

## まとめ

### 復習

1. 加法標準形の論理式が与えられたときに，これを簡略化してNAND回路を構成するまでの一連の手続きを箇条書きしてください．
2. グレイコードを使う理由を考えてみてください．例えばグレイコードではない例として，行を$A=0,1$，列を$BC=00,01,10,11$としたときの図表ではどのような不便が生じるでしょうか．

