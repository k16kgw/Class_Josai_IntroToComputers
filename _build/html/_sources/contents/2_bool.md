# ブール代数，論理演算，真理値表

到達目標
- 論理演算の基本となるブール代数および真理値表について理解する．

- **ブール代数の公理・基本定理**を用いて論理式を変形できる。
- **双対性（duality）**の概念を説明し、双対式を導出できる。
- 基本的な**論理式の簡略化**（代数的手法、吸収・冗長項の削除、合意（コンセンサス）など）ができる。

## 復習と準備














## ブール代数

ブール代数：`0`と`1`（または偽と真）の2つの値だけを使って論理を扱う数学的な枠組み．

### 基本記号と演算

- 変数を $A,B,C$ とし，これらは`0`か`1`の値しか取らない．
- 基本的な演算は次の3つ
  - 否定（NOT）：$\lnot A$, $\overline{A}$
  - 論理積（AND）：$A \land B$, $A\cdot B$, $AB$
  - 論理和（OR）：$A \lor B$, $A + B$
- これらを組み合わせて，他に次の演算を定義できる．
  - 排他的論理和（XOR）：$A \oplus B$
  - 否定論理和（NOR）：$\overline{A+B}$
  - 否定論理積（NAND）：$\overline{A\cdot B}$, $\overline{AB}$

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
| 単位元  | $A+0=A$，$A \cdot 1=A$ |
| 交換則  | $A+B=B+A$，$A \cdot B = B \cdot A$ |
| 結合則  | $(A+B)+C=A+(B+C)$，$(A \cdot B) \cdot C=A \cdot (B \cdot C)$ |
| 分配則  | $A \cdot (B+C) = A \cdot B + A \cdot C$，$A+B \cdot C = (A+B) \cdot (A+C)$ |
| 補元    | $A+\overline{A}=1$，$A\cdot\overline{A}=0$ |

### 基本定理（よく使う等式）

* べき等律：$$A+A=A,,\ AA=A$$
* 吸収律：$$A+AB=A,,\ A(A+B)=A$$
* 反転同値：$$\overline{\overline{A}}=A$$
* ド・モルガン：$$\overline{A+B}=\overline{A},\overline{B},,\quad \overline{AB}=\overline{A}+\overline{B}$$
* コンセンサス（合意）定理：$$AB + \overline{A}C + BC = AB + \overline{A}C$$

> **使いどころ**：冗長項（例えば $$BC$$）を削ってゲート数・段数を減らす。

### 2.3 双対性の原理（Principle of Duality）

* 規則：「$$0\leftrightarrow 1$$ と $$+\leftrightarrow \cdot$$ を同時に入れ替える」と**常に真**の等式は**双対**も真。
* 例：$$A+0=A$$ の双対は $$A\cdot 1=A$$。
* 例：分配 $$A+BC=(A+B)(A+C)$$ の双対は $$A(B+C)=AB+AC$$。

**演習（その場で口頭）**：

1. $$A+\overline{A}B = A+B$$ を示せ（吸収＋分配）。
2. 上式の双対を求めよ。

## 3. 論理式の簡略化（後半その1）

> 第4回のカルノー図，第5回のQ-M法に先立ち，**代数的**にシンプルにするコツを学ぶ。

### 3.1 代数的簡略化の手順例

1. **共通因子**で括る／分配する。
2. **吸収律**で項を削る。
3. **ド・モルガン**で否定を外へ寄せる。
4. **コンセンサス**で冗長項を落とす。

### 3.2 例題A（2変数）

与式：$$F(A,B)= A\overline{B} + AB$$

* 因数分解：$$F=A(\overline{B}+B)=A\cdot 1= A$$
  → **最小**：NOT/AND/OR不要（バッファ1つ）。

### 3.3 例題B（3変数：吸収）

与式：$$F= AB + A\overline{B}C + AB\overline{C}$$

* まず $$AB$$ が他項を**吸収**：$$F=AB + A\overline{B}C$$
* さらに因数分解：$$F=A(B+\overline{B}C)=A(B+C)$$
  → ゲート段数・配線削減。

### 3.4 例題C（コンセンサス）

与式：$$F= AB + \overline{A}C + BC$$

* 合意定理より：$$F=AB + \overline{A}C$$（$$BC$$ は冗長）

### 3.5 例題D（SOP→簡約）

与式（SOP）：$$F= \overline{A}BC + A\overline{B}C + ABC$$

* 2項をまとめ：$$F=C(\overline{A}B + A\overline{B} + AB)=C(B\oplus A + AB)$$
* さらに：$$B\oplus A + AB = A+B$$（よく出る恒等式）
* よって：$$F=C(A+B)$$

> 補足：$$A\oplus B = A\overline{B}+\overline{A}B$$ を起点に示せる。

---

## 4. 例題演習（後半その2）

### 4.1 例題1：真理値表→SOP/POS

**仕様**：2入力の**少なくとも1つが1**なら1。

* 真理値表から：$$F(A,B)=A+B$$
* SOP：$$A\overline{B}+\overline{A}B+AB = A+B$$（吸収）
* POS：$$(A+B)$$（最小形）

### 4.2 例題2：多数決（majority）

**仕様**：3入力中**2つ以上が1**で1。

* SOP（機械的導出）：$$F=AB+BC+CA$$（最小）
* 証明スケッチ：真理値表で1となる行を和で表し、吸収で簡約。

### 4.3 例題3：ハザードに注意した冗長項

**仕様**：$$F=\overline{A}B + A\overline{B}$$（XOR）

* タイミングを考慮しない論理最小化ではOKだが、物理回路では**静的ハザード**回避のため $$AB$$ または $$\overline{A},\overline{B}$$ を**意図的に追加**することがある（第9回で詳述）。

---

## 5. ミニ確認テスト（5問・その場採点）

1. $$A+\overline{A}B$$ を簡略化せよ。
2. 双対性の原理に従い、$$A(B+C)=AB+AC$$ の双対を答えよ。
3. $$\overline{A+B+C}$$ をド・モルガンで展開せよ。
4. $$AB+\overline{A}C+BC$$ を簡略化せよ。
5. 真理値表で1となる行が 3変数で (1,3,5,7) のときのSOPを答えよ。

**解答例（配布・板書）**：

1. $$A+\overline{A}B = (A+\overline{A})(A+B)=1\cdot(A+B)=A+B$$
2. $$A+BC=(A+B)(A+C)$$
3. $$\overline{A},\overline{B},\overline{C}$$
4. $$AB+\overline{A}C$$（合意定理）
5. $$\overline{A},\overline{B}C + \overline{A}BC + A\overline{B}C + ABC = C(A+B)$$

---

## 6. まとめ・次回予告

* **キー等式**：吸収、ド・モルガン、合意定理、双対。
* **実務観点**：ゲート数と段数の削減＝面積・遅延・消費電力の削減に直結。
* **次回（第3回）**：主加法標準形・主乗法標準形の体系化と**論理ゲート実装**（NAND-NAND, NOR-NOR）。

## 論理関数

---

## 付録：等式 “チートシート”

* $$A+\overline{A}B=A+B$$
* $$AB+\overline{A}C+BC=AB+\overline{A}C$$（合意）
* $$A+AB=A,,\ A(A+B)=A$$（吸収）
* $$\overline{AB}=\overline{A}+\overline{B}$$, $$\overline{A+B}=\overline{A},\overline{B}$$（ド・モルガン）
* $$A\oplus B = A\overline{B}+\overline{A}B$$, $$A\oplus B = (A+B)(\overline{A}+\overline{B})$$

## 宿題

* ワークシート（10問）：等式変形とSOP/POS導出。うち2問は自由記述で**どの法則を使ったか**明記。次回冒頭で回収。
