# MATH1064 Practice Exam 1

This practice exam is based on the Tutorials and the 2019 sample exam. It focuses on sets, functions, logic, relations, combinatorics, graph theory, number theory and induction.

Try to complete it in approximately **2 hours**.

## Section A: Multiple Choice

Choose one answer for each question.

### 1.

Let

$$
A=\{a,\{b\},\{a,b\}\}.
$$

Which statement is true?

(a) $b\in A$

(b) $\{b\}\subseteq A$

(c) $\{a,b\}\subseteq A$

(d) $|A|=4$

(e) $|\mathcal P(A)|=3$

(f) $A\subseteq\{\{a,b\}\}$

---

### 2.

Let

$$
X=\{1,2,\ldots,3n\}.
$$

What is $|\mathcal P(X)|$?

(a) $2^n$

(b) $3^n$

(c) $6^n$

(d) $8^n$

---

### 3.

Suppose

$$
|A|=14,\qquad |B|=18,\qquad |C|=20,
$$

$$
|A\cap B|=5,\qquad |A\cap C|=6,\qquad |B\cap C|=7,
$$

and

$$
|A\cap B\cap C|=2.
$$

Find $|A\cup B\cup C|$.

(a) $32$

(b) $34$

(c) $36$

(d) $40$

(e) $42$

---

### 4.

Let

$$
f:\mathbb Q\to\mathbb Z,\qquad f(x)=\lfloor 2x\rfloor.
$$

Which description is correct?

(a) Injective but not surjective

(b) Surjective but not injective

(c) Bijective

(d) Neither injective nor surjective

---

### 5.

Let

$$
f:\mathbb Z\to\mathbb Z,\qquad f(n)=n^2.
$$

Which statement is correct?

(a) $f$ is injective

(b) $f$ is surjective

(c) $f$ is bijective

(d) $f$ is neither injective nor surjective

---

### 6.

What is the coefficient of $x^4$ in $(2x-3)^7$?

(a) $\binom74 2^4 3^3$

(b) $\binom74 2^4(-3)^3$

(c) $\binom73 2^4(-3)^3$

(d) $\binom74 2^3(-3)^4$

---

### 7.

Six identical doughnuts are placed into three distinct boxes. Each box may be empty. How many arrangements are possible?

(a) $\binom63$

(b) $\binom62$

(c) $\binom82$

(d) $3^6$

---

### 8.

How many distinct arrangements are there of the letters in `MISSISSIPPI`?

(a) $\dfrac{11!}{4!4!2!}$

(b) $\dfrac{11!}{4!2!}$

(c) $\dfrac{11!}{4!4!}$

(d) $11!$

---

### 9.

How many permutations of $\{1,2,3,4\}$ have at least one fixed point?

(a) $8$

(b) $12$

(c) $15$

(d) $18$

(e) $20$

---

### 10.

A relation $R$ on $\mathbb Z$ is defined by

$$
xRy\iff x-y\text{ is even}.
$$

Which statement is correct?

(a) $R$ is only reflexive

(b) $R$ is reflexive and symmetric, but not transitive

(c) $R$ is an equivalence relation

(d) $R$ is a partial order but not an equivalence relation

---

### 11.

Which congruence is correct?

(a) $1234\equiv 1\pmod 7$

(b) $1234\equiv 2\pmod 7$

(c) $1234\equiv 3\pmod 7$

(d) $1234\equiv 4\pmod 7$

---

### 12.

Using the Euclidean algorithm, find $\gcd(252,198)$.

(a) $6$

(b) $9$

(c) $18$

(d) $36$

---

### 13.

Which function $f:\mathbb Z\to\mathbb Z$ is injective?

(a) $f(n)=n^2$

(b) $f(n)=|n|$

(c) $f(n)=3n-5$

(d) $f(n)=\sin n$

---

### 14.

Which statement is false?

(a) $n^2+3n+1\in O(n^3)$

(b) $n^2+3n+1\in\Theta(n^2)$

(c) $n^2+3n+1\in\Omega(n)$

(d) $n^2+3n+1\in\Omega(n^3)$

---

### 15.

Which proposition is a contradiction?

(a) $p\vee q$

(b) $(p\wedge q)\wedge(\neg p\vee\neg q)$

(c) $p\to q$

(d) $p\vee\neg q$

---

### 16.

What is the negation of

$$
\forall x\in D,\; P(x)\wedge\neg Q(x)?
$$

(a) $\exists x\in D,\; \neg P(x)\vee Q(x)$

(b) $\forall x\in D,\; \neg P(x)\vee Q(x)$

(c) $\exists x\in D,\; P(x)\vee\neg Q(x)$

(d) $\forall x\in D,\; \neg P(x)\wedge Q(x)$

---

### 17.

A simple graph has vertex degrees

$$
1,2,3,3,3,4.
$$

How many edges does it have?

(a) $6$

(b) $7$

(c) $8$

(d) $9$

---

### 18.

Which complete graph has an Eulerian circuit?

(a) $K_3$

(b) $K_4$

(c) $K_5$

(d) $K_6$

---

### 19.

A fair die is rolled $18$ times. What is the expected number of times that a $4$ appears?

(a) $2$

(b) $3$

(c) $4$

(d) $6$

---

### 20.

Which statement is true?

(a) $(1011)_2=(10)_{10}$

(b) $(1011)_2=(11)_{10}$

(c) $(1011)_2=(12)_{10}$

(d) $(1011)_2=(13)_{10}$

---

# Section B: Extended Answer

Show all working and give reasons for your answers.

## Question 1: Sets and Functions

Let

$$
A=\{1,2,3\},\qquad B=\{x,y\}.
$$

### (a)

Write down $A\times B$ and $B\times A$.

### (b)

Let

$$
f:\mathbb Z\to\mathbb Z,\qquad f(n)=2n+1.
$$

Determine whether $f$ is injective and whether it is surjective. Prove your answers.

### (c)

Let

$$
g:\mathbb Z\to\mathbb Z,\qquad g(n)=n^2.
$$

Determine whether $g$ is injective and whether it is surjective. Give proofs or counterexamples.

### (d)

Find the composition $g\circ f$.

---

## Question 2: Combinatorics

### (a)

State the Binomial Theorem.

### (b)

Find the coefficient of $x^5$ in

$$
(3x-2)^8.
$$

Do not evaluate the final binomial coefficient.

### (c)

How many arrangements of the letters in `COMPUTATION` contain the consecutive word `PUT`?

### (d)

How many five-digit numbers can be formed using the digits

$$
0,1,2,3,4,5,6
$$

without repetition and without beginning with $0$?

---

## Question 3: Number Theory and Logic

### (a)

State the Quotient-Remainder Theorem.

### (b)

Use the Euclidean algorithm to find

$$
\gcd(391,299).
$$

### (c)

Prove that if $d\mid a$ and $d\mid b$, then

$$
d\mid(4a-7b).
$$

### (d)

Determine whether the following statement is true or false:

$$
d\mid ab\Longrightarrow d\mid a\text{ or }d\mid b.
$$

If it is false, give a counterexample.

### (e)

Let

$$
P(x): x>1,\qquad Q(x): x^2>1.
$$

Taking the domain to be $\mathbb R$, determine the truth value of

$$
\forall x\big(P(x)\to Q(x)\big).
$$

Then write its negation.

---

## Question 4: Relations and Graph Theory

Let

$$
S=\{1,2,3,4\}
$$

and define

$$
R=\{(1,1),(2,2),(3,3),(4,4),(1,2),(2,1),(2,3),(3,2)\}.
$$

For each property below, determine whether $R$ has that property. Give a reason or counterexample.

### (a)

Reflexive

### (b)

Symmetric

### (c)

Transitive

### (d)

Antisymmetric

### (e)

Let $G$ be a graph with seven vertices and degrees

$$
1,2,2,3,3,3,4.
$$

How many edges does $G$ have?

### (f)

Prove that every simple graph with five vertices and at least seven edges is connected.

---

## Question 5: Mathematical Induction

### (a)

Prove by mathematical induction that for every positive integer $n$,

$$
1+3+5+\cdots+(2n-1)=n^2.
$$

### (b)

Prove by mathematical induction that for every positive integer $n$,

$$
2+5+8+\cdots+(3n-1)=\frac{n(3n+1)}2.
$$

### (c)

Prove that $7$ divides

$$
8^n-1
$$

for every positive integer $n$.

### (d)

A sequence is defined by

$$
a_1=2,\qquad a_{n+1}=3a_n-2.
$$

Find a possible formula for $a_n$, and prove your formula by induction.




我会重新编一整套英文模拟卷，保持 2019 年的结构：20 道单选题加 5 道大题；出完后逐题检查计算、定义域、选项是否唯一正确，避免上一套的歧义。

 # MATH1064 Practice Examination 2

This practice paper follows the general style of the 2019 sample exam.

- **Section A:** 20 multiple-choice questions
- **Section B:** 5 extended-answer questions
- Choose exactly one answer for each multiple-choice question.
- Show all working in Section B.
- Suggested time: **2 hours**

---

# Section A: Multiple Choice

### 1.

Let

$$
A=\{a,\{b\},\{a,b\},a\}.
$$

Which statement is true?

(a) $|A|=4$

(b) $b\in A$

(c) $\{b\}\subseteq A$

(d) $|\mathcal P(A)|=8$

---

### 2.

Let

$$
X=\{1,2,\ldots,2n\}.
$$

What is $|\mathcal P(X)|$?

(a) $2^n$

(b) $3^n$

(c) $4^n$

(d) $8^n$

---

### 3.

Suppose

$$
|A|=12,\quad |B|=16,\quad |C|=21,
$$

$$
|A\cap B|=5,\quad |A\cap C|=7,\quad |B\cap C|=8,
$$

and

$$
|A\cap B\cap C|=3.
$$

Find $|A\cup B\cup C|$.

(a) $29$

(b) $32$

(c) $35$

(d) $38$

---

### 4.

Let

$$
f:\mathbb Q\to\mathbb Z,\qquad f(x)=\lfloor 2x\rfloor.
$$

Which statement is correct?

(a) $f$ is injective but not surjective.

(b) $f$ is surjective but not injective.

(c) $f$ is bijective.

(d) $f$ is neither injective nor surjective.

---

### 5.

Let

$$
f:\mathbb Z\to\mathbb Z,\qquad f(n)=n^3.
$$

Which statement is correct?

(a) $f$ is injective and surjective.

(b) $f$ is injective but not surjective.

(c) $f$ is surjective but not injective.

(d) $f$ is neither injective nor surjective.

---

### 6.

What is the coefficient of $x^3$ in $(x-2)^8$?

(a) $\binom83(-2)^3$

(b) $\binom85(-2)^3$

(c) $\binom83(-2)^5$

(d) $\binom85(-2)^5$

---

### 7.

Five identical objects are distributed among three distinct boxes. Empty boxes are allowed. How many distributions are possible?

(a) $\binom52$

(b) $\binom73$

(c) $\binom72$

(d) $3^5$

---

### 8.

How many distinct arrangements are there of the letters in `BANANA`?

(a) $60$

(b) $120$

(c) $180$

(d) $360$

---

### 9.

How many permutations of $\{1,2,3,4\}$ have at least one fixed point?

(a) $9$

(b) $12$

(c) $15$

(d) $18$

---

### 10.

Define a relation $R$ on $\mathbb Z$ by

$$
xRy\iff x-y\text{ is even}.
$$

Which statement is correct?

(a) $R$ is reflexive but not symmetric.

(b) $R$ is symmetric but not transitive.

(c) $R$ is an equivalence relation.

(d) $R$ is a partial order.

---

### 11.

Using the Euclidean algorithm, find $\gcd(391,299)$.

(a) $13$

(b) $23$

(c) $31$

(d) $46$

---

### 12.

What is the remainder when $34567$ is divided by $9$?

(a) $5$

(b) $6$

(c) $7$

(d) $8$

---

### 13.

Which proposition is a contradiction?

(a) $p\vee q$

(b) $p\wedge q$

(c) $(p\wedge q)\wedge(\neg p\vee\neg q)$

(d) $(p\vee q)\to p$

---

### 14.

What is the negation of

$$
\forall x\in D,\; P(x)\vee\neg Q(x)?
$$

(a) $\exists x\in D,\; \neg P(x)\wedge Q(x)$

(b) $\exists x\in D,\; P(x)\wedge\neg Q(x)$

(c) $\forall x\in D,\; \neg P(x)\wedge Q(x)$

(d) $\forall x\in D,\; P(x)\wedge\neg Q(x)$

---

### 15.

Which statement is false?

(a) $n\log n\in O(n^2)$

(b) $n^2+4n+1\in\Theta(n^2)$

(c) $n^2+4n+1\in\Omega(n)$

(d) $n\log n\in O(n)$

---

### 16.

A graph has six vertices with degrees

$$
1,2,3,3,4,5.
$$

How many edges does the graph have?

(a) $8$

(b) $9$

(c) $10$

(d) $18$

---

### 17.

Which graph has an Eulerian circuit?

(a) $K_3$

(b) $K_4$

(c) $K_6$

(d) $K_8$

---

### 18.

A fair die is rolled $24$ times. What is the expected number of times that a $6$ appears?

(a) $3$

(b) $4$

(c) $5$

(d) $6$

---

### 19.

What is the decimal representation of $(110101)_2$?

(a) $51$

(b) $52$

(c) $53$

(d) $54$

---

### 20.

A jar contains blue, red, green and yellow balls. Five balls are selected, and balls of the same colour are considered identical. How many possible colour combinations are there?

(a) $\binom53$

(b) $\binom73$

(c) $\binom84$

(d) $4^5$

---

# Section B: Extended Answer

Show all working and give reasons for your answers.

## Question 1: Sets and Functions

Let

$$
A=\{1,2,3\},\qquad B=\{x,y\}.
$$

### (a)

Write down $A\times B$ and $B\times A$.

### (b)

Let

$$
f:\mathbb Z\to\mathbb Z,\qquad f(n)=3n-2.
$$

Determine whether $f$ is injective and whether it is surjective. Prove your answers.

### (c)

Let

$$
g:\mathbb Z\to\mathbb Z,\qquad g(n)=n^2+1.
$$

Determine whether $g$ is injective and whether it is surjective. Give a proof or a counterexample for each claim.

### (d)

Find the composition $g\circ f$.

---

## Question 2: Counting and Combinatorics

### (a)

State the Binomial Theorem.

### (b)

Find the coefficient of $x^4$ in

$$
(2x-3)^7.
$$

Do not evaluate the final binomial coefficient.

### (c)

How many arrangements are there of the letters in `ALGEBRA` containing the consecutive word `BRA`?

### (d)

How many integers between $1000$ and $9999$ can be formed using the digits

$$
0,1,2,3,4,5,6
$$

without repetition?

---

## Question 3: Number Theory

### (a)

State the Quotient-Remainder Theorem.

### (b)

Use the Euclidean algorithm to find

$$
\gcd(527,391).
$$

### (c)

Prove that if $d\mid a$ and $d\mid b$, then

$$
d\mid(5a-2b).
$$

### (d)

Determine whether the following statement is true or false:

$$
d\mid ab\Longrightarrow d\mid a\text{ or }d\mid b.
$$

If it is false, give a counterexample.

### (e)

Prove that

$$
3\mid n^3-n
$$

for every integer $n$.

---

## Question 4: Logic, Relations and Graph Theory

Let

$$
S=\{1,2,3,4\}
$$

and define

$$
R=\{(1,1),(2,2),(3,3),(4,4),(1,2),(2,1),(2,3),(3,2)\}.
$$

For each property, determine whether $R$ has that property. Give a reason or a counterexample.

### (a)

Reflexive

### (b)

Symmetric

### (c)

Transitive

### (d)

Antisymmetric

### (e)

Let $G$ be a graph with seven vertices and degrees

$$
1,2,2,3,3,3,4.
$$

How many edges does $G$ have?

### (f)

Prove that every simple graph with exactly five vertices and at least seven edges is connected.

---

## Question 5: Mathematical Induction

### (a)

Prove by mathematical induction that, for every positive integer $n$,

$$
1+3+5+\cdots+(2n-1)=n^2.
$$

### (b)

Prove by mathematical induction that, for every positive integer $n$,

$$
2+5+8+\cdots+(3n-1)=\frac{n(3n+1)}2.
$$

### (c)

Prove by mathematical induction that

$$
5^n-1
$$

is divisible by $4$ for every positive integer $n$.

### (d)

A sequence is defined by

$$
a_1=1,\qquad a_{n+1}=2a_n+3.
$$

Find a formula for $a_n$, and prove your formula by mathematical induction.