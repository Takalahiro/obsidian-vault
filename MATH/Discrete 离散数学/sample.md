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


我会先对照知识库里的两张样卷和 Tutorial，编一套新的英文模拟卷，并逐题校验，确保每道选择题只有一个正确选项。


两张样卷都包含概念判断和证明题，2025 年卷还加入了状态机、文法和归纳法纠错。我会把这些题型纳入新卷，并标明大题各小问的分值，方便之后准确批改。

**This paper draws on both the 2019 and 2025 sample exams and the Tutorials. Each multiple-choice question has exactly one correct answer. Answers are omitted so you can attempt it under exam conditions.**

# MATH1064 — Practice Examination 3

**Reading time:** 10 minutes  
**Writing time:** 2 hours  
**Total marks:** 100

- Section A: 20 multiple-choice questions, worth **50 marks**.
- Section B: 5 extended-answer questions, worth **50 marks**.
- All questions may be attempted.
- Show your working and give reasons in Section B.

**Notation:** $\mathbb N_0=\{0,1,2,\ldots\}$. The symbol $\subseteq$ allows equality; $\subsetneq$ denotes a proper subset. All graphs are finite and undirected unless stated otherwise.

---

**SECTION A — MULTIPLE CHOICE**

Each question is worth **2.5 marks**. Select **exactly one** option.

**1.** Let

$$
A=\{\varnothing,\{\varnothing\},\{1\}\}.
$$

Which statement is **false**?

(a) $\varnothing\in A$

(b) $\{\varnothing\}\subseteq A$

(c) $1\in A$

(d) $|\mathcal P(A)|=8$

---

**2.** Let

$$
S=\{a,b,c\}\times\{0,1\},
\qquad
T=\mathcal P(\{x,y,z\}).
$$

Which statement is correct?

(a) $|S|=6$ and $|T|=8$

(b) $|S|=8$ and $|T|=6$

(c) $|S|=6$ and $|T|=6$

(d) $|S|=9$ and $|T|=8$

---

**3.** Which identity holds for all sets $A,B,C$?

(a) $A\setminus(B\cup C)=(A\setminus B)\cup(A\setminus C)$

(b) $A\setminus(B\cup C)=(A\setminus B)\cap(A\setminus C)$

(c) $A\setminus(B\cup C)=(B\cup C)\setminus A$

(d) $A\setminus(B\cup C)=A\cap(B\cup C)$

---

**4.** Define

$$
f:\mathbb Z\to\mathbb Z,\qquad
f(n)=\left\lfloor\frac n2\right\rfloor.
$$

Then $f$ is:

(a) injective but not surjective.

(b) bijective.

(c) neither injective nor surjective.

(d) surjective but not injective.

---

**5.** Let

$$
E=\{2k:k\in\mathbb Z\},
$$

and define

$$
g:\mathbb Z\to E,\qquad g(n)=2n.
$$

Then $g$ is:

(a) injective but not surjective.

(b) surjective but not injective.

(c) bijective.

(d) neither injective nor surjective.

---

**6.** How many integers from $1$ to $60$, inclusive, are relatively prime to $10$?

(a) $18$

(b) $24$

(c) $30$

(d) $36$

---

**7.** A shop sells three flavours of cookies and two flavours of muffins. A customer chooses exactly four cookies and exactly three muffins.

Items of the same type and flavour are indistinguishable. Each flavour is available in unlimited quantities.

How many selections are possible?

(a) $\binom42\binom31$

(b) $3^4\,2^3$

(c) $\binom62+\binom41$

(d) $\binom62\binom41$

---

**8.** A committee consists of two people chosen from five students and one person chosen from six tutors.

One particular student and one particular tutor must **not both** be on the committee.

How many committees are possible?

(a) $\binom52\cdot6-4$

(b) $\binom52\cdot6-1$

(c) $\binom42\cdot5$

(d) $\binom52\cdot5$

---

**9.** How many permutations $f$ of $\{1,2,3,4,5\}$ have **exactly two fixed points**?

A fixed point is an element $i$ such that $f(i)=i$.

(a) $10$

(b) $15$

(c) $20$

(d) $60$

---

**10.** Write

$$
(1+x)^9=\sum_{k=0}^{9}a_kx^k.
$$

Which statement is correct?

(a) $a_0=9$

(b) $a_2=a_7$

(c) $a_1=a_2$

(d) $a_9=0$

---

**11.** Which proposition is a tautology?

(a) $(p\to q)\to(q\to p)$

(b) $(p\vee q)\to(p\wedge q)$

(c) $(p\to q)\wedge\neg q$

(d) $((p\to q)\wedge\neg q)\to\neg p$

---

**12.** What is the negation of

$$
\forall x\in D\;\exists y\in D\;
\bigl(P(x)\to Q(y)\bigr)?
$$

(a) $\exists x\in D\;\forall y\in D\;\bigl(P(x)\wedge\neg Q(y)\bigr)$

(b) $\forall x\in D\;\exists y\in D\;\bigl(P(x)\wedge\neg Q(y)\bigr)$

(c) $\exists x\in D\;\forall y\in D\;\bigl(\neg P(x)\vee Q(y)\bigr)$

(d) $\exists x\in D\;\exists y\in D\;\bigl(P(x)\wedge\neg Q(y)\bigr)$

---

**13.** Define a relation $R$ on $\mathbb Z$ by

$$
xRy\iff x\le y.
$$

Which description is correct?

(a) Reflexive, symmetric and transitive

(b) Symmetric and antisymmetric, but not reflexive

(c) Reflexive, antisymmetric and transitive

(d) Reflexive and symmetric, but not transitive

---

**14.** Which list **cannot** be the degrees of the vertices of a simple graph with five vertices?

(a) $2,2,2,2,2$

(b) $4,4,1,1,0$

(c) $4,1,1,1,1$

(d) $3,3,2,2,2$

---

**15.** Let $G$ have vertex set $\{1,2,3,4,5\}$ and edge set

$$
E=\bigl\{
\{1,2\},\{2,3\},\{3,1\},
\{3,4\},\{4,5\},\{5,3\}
\bigr\}.
$$

Which statement is correct?

(a) $G$ is disconnected.

(b) $G$ has exactly two vertices of odd degree.

(c) $G$ has an Eulerian circuit.

(d) $G$ has no Eulerian trail.

---

**16.** For positive integers $n$, let

$$
h(n)=\frac{n^3+2n}{n+1}.
$$

Which statement is **false**?

(a) $h(n)\in\Theta(n^2)$

(b) $h(n)\in O(n^3)$

(c) $h(n)\in\Omega(n)$

(d) $h(n)\in\Omega(n^3)$

---

**17.** A fair coin is tossed three times. Let $X$ be the number of heads.

What is $P(X\ge2)$?

(a) $\frac18$

(b) $\frac38$

(c) $\frac12$

(d) $\frac34$

---

**18.** A finite-state automaton has initial state $s_0$ and the following transition table.

| Current state | Input $0$ | Input $1$ |
|---|---|---|
| $s_0$ | $s_0$ | $s_1$ |
| $s_1$ | $s_1$ | $s_0$ |

What is its final state after reading the input string `1011010` from left to right?

(a) $s_0$

(b) $s_1$

(c) It has no final state because the string contains consecutive $1$s.

(d) The transition table does not determine the result.

---

**19.** A grammar has start symbol $S$, terminal alphabet $\{a,b\}$ and productions

$$
S\to aS\mid b.
$$

Which language does it generate?

(a) $\{a^nb:n\ge1\}$

(b) $\{a^nb:n\in\mathbb N_0\}$

(c) $\{a^nb^n:n\ge1\}$

(d) $\{ba^n:n\in\mathbb N_0\}$

---

**20.** A student wants to prove

$$
\sum_{i=1}^{n}i(i+1)=\frac{n(n+1)(n+2)}3
$$

by induction.

After assuming the formula for $n=k$, which expression correctly represents the sum for $n=k+1$?

(a) $\dfrac{k(k+1)(k+2)}3+(k+1)$

(b) $\dfrac{k(k+1)(k+2)}3+k(k+1)$

(c) $\dfrac{k(k+1)(k+2)}3+(k+1)(k+2)$

(d) $\dfrac{(k+1)(k+2)(k+3)}3+(k+1)(k+2)$

---

**SECTION B — EXTENDED ANSWER**

Each question is worth **10 marks**. Marks for individual parts are shown.

**Question 1 — Sets and Functions [10 marks]**

**(a) [2 marks]** Let

$$
A=\{\varnothing,1,\{1\}\}.
$$

Determine whether each statement is true or false.

(i) $\{1\}\in A$

(ii) $\{1\}\subseteq A$

(iii) $\{\{1\}\}\subseteq A$

(iv) $\varnothing\in\mathcal P(A)$

**(b) [3 marks]** Define

$$
f:\mathbb Z\to\mathbb Z,\qquad f(n)=4n+1.
$$

Determine whether $f$ is injective and whether it is surjective. Justify both answers.

**(c) [3 marks]** Define

$$
g:\mathbb Z\times\mathbb Z\to\mathbb Z,\qquad g(a,b)=a-b.
$$

Determine whether $g$ is injective and whether it is surjective. Justify both answers.

**(d) [2 marks]** Let $u:X\to Y$ and $v:Y\to Z$ be functions.

Prove that if $v\circ u$ is injective, then $u$ is injective.

---

**Question 2 — Counting and Probability [10 marks]**

**(a) [2 marks]** Find the coefficient of $x^5$ in

$$
(1+x)^4(1+2x)^3.
$$

You may leave your answer as a sum involving binomial coefficients.

**(b) [2 marks]** How many distinct arrangements of the letters in `BALLOON` have the two letters `L` **not adjacent**?

Give a brief explanation.

**(c) [3 marks]** How many permutations of $\{1,2,3,4,5\}$ have at least one fixed point?

Use the Inclusion–Exclusion Principle and show your calculation.

**(d) [3 marks]** Box $A$ contains two red balls and one blue ball. Box $B$ contains one red ball and three blue balls.

A box is selected with equal probability, and one ball is drawn uniformly at random from that box.

Given that the ball is red, find the probability that it came from Box $A$.

---

**Question 3 — Number Theory and Logic [10 marks]**

**(a) [2 marks]** Use the Euclidean algorithm to find

$$
\gcd(414,322).
$$

Show all divisions with remainders.

**(b) [2 marks]** Prove that, for every integer $n$,

$$
n^2\equiv0\text{ or }1\pmod4.
$$

**(c) [2 marks]** Hence prove that the equation

$$
x^2+y^2=4z+3
$$

has no solutions with $x,y,z\in\mathbb Z$.

**(d) [2 marks]** Write the negation of the following statement. Move the negation inside so that it applies only to $P$ and $Q$.

$$
\forall x\in D\;\exists y\in D\;
\bigl(P(x)\wedge Q(y)\bigr).
$$

**(e) [2 marks]** Determine whether the following argument is valid. Give a reason or a counterexample using truth values.

$$
p\to q,\qquad q,\qquad \therefore p.
$$

---

**Question 4 — Relations and Graph Theory [10 marks]**

**(a) [4 marks]** Define a relation $R$ on $\mathbb Z$ by

$$
xRy\iff |x|=|y|.
$$

Determine whether $R$ is:

(i) reflexive;

(ii) symmetric;

(iii) transitive;

(iv) antisymmetric.

Give a brief justification or counterexample for each answer.

**(b) [2 marks]** Let $G$ be the simple graph with adjacency matrix

$$
M=
\begin{pmatrix}
0&1&0&1\\
1&0&1&0\\
0&1&0&1\\
1&0&1&0
\end{pmatrix}.
$$

(i) How many edges does $G$ have?

(ii) Does $G$ have an Eulerian circuit? Justify your answer.

**(c) [2 marks]** Prove that every simple graph on six vertices with minimum degree at least $3$ is connected.

*Hint: If the graph were disconnected, how many vertices would each connected component need?*

**(d) [2 marks]** Is the union of two equivalence relations on the same set always an equivalence relation?

Give a proof or a specific counterexample.

---

**Question 5 — Induction, Recursion and Grammars [10 marks]**

**(a) [4 marks]** A sequence is defined by

$$
a_0=2,\qquad a_{n+1}=2a_n+1
\quad\text{for all }n\in\mathbb N_0.
$$

(i) Write down $a_1,a_2,a_3$.

(ii) Find a closed formula for $a_n$ and prove it by mathematical induction.

**(b) [3 marks]** Prove by mathematical induction that

$$
3\mid(4^n-1)
$$

for every $n\in\mathbb N_0$.

Clearly state your base case, induction hypothesis and induction step.

**(c) [3 marks]** Consider the grammar with start symbol $S$, terminal alphabet $\{a,b\}$ and productions

$$
S\to aSb\mid ab.
$$

(i) Give a derivation of the string `aaabbb`.

(ii) Describe the language generated by the grammar using set-builder notation, and briefly explain why your description is correct.

---

**End of Practice Examination**



我会按两张样卷和 Tutorial 出 20 道英文单选题，重点检查昨天复习的内容，并逐题核对答案是否唯一；先不附答案。

今天这套共 **20 道英文单选题**，建议限时 **45–50 分钟**，每题 5 分。已逐题核对，**每题只有一个正确答案**。

先不附答案。遇到不认识的单词，把它圈出来；不会的题也保留过程，批改时我们区分读题问题和知识点问题。

---

# MATH1064 — Multiple-Choice Practice 4

**Instructions:** Choose exactly one answer for each question.

**Notation:** $\mathbb N_0=\{0,1,2,\ldots\}$. The symbol $\subseteq$ allows equality. All graphs are finite, simple and undirected unless otherwise stated.

**1.** Let

$$
A=\{a,\{b\},\varnothing\},
$$

where $a$ and $b$ are distinct letters. Which statement is **false**?

(a) $\{a\}\subseteq A$

(b) $\{b\}\in A$

(c) $b\in A$

(d) $\varnothing\subseteq A$

---

**2.** A set $X$ has five elements, including a particular element $u$.

How many subsets of $X$ contain $u$?

(a) $8$

(b) $16$

(c) $31$

(d) $32$

---

**3.** Three sets satisfy

$$
|A\cap B|=5,\qquad |A\cap C|=6,\qquad |B\cap C|=7,
$$

and

$$
|A\cap B\cap C|=2.
$$

How many elements belong to **exactly two** of the sets $A,B,C$?

(a) $18$

(b) $16$

(c) $14$

(d) $12$

---

**4.** Define

$$
f:\mathbb R\to\mathbb R,\qquad f(x)=x^2.
$$

Then $f$ is:

(a) neither injective nor surjective.

(b) injective but not surjective.

(c) surjective but not injective.

(d) bijective.

---

**5.** Let

$$
O=\{2k+1:k\in\mathbb Z\},
$$

and define

$$
g:\mathbb Z\to O,\qquad g(n)=2n+1.
$$

Then $g$ is:

(a) surjective but not injective.

(b) neither injective nor surjective.

(c) bijective.

(d) injective but not surjective.

---

**6.** Use the Euclidean algorithm to find

$$
\gcd(286,198).
$$

(a) $11$

(b) $22$

(c) $44$

(d) $88$

---

**7.** How many integers from $1$ to $40$, inclusive, are relatively prime to $6$?

(a) $7$

(b) $13$

(c) $20$

(d) $14$

---

**8.** A shop sells four flavours of muffins, with an unlimited supply of each flavour. Muffins of the same flavour are indistinguishable.

How many selections of six muffins are possible if some flavours may be omitted?

(a) $\binom93$

(b) $\binom63$

(c) $\binom94$

(d) $4^6$

---

**9.** How many distinct arrangements of the letters in `LEVEL` have the two letters `L` adjacent?

(a) $6$

(b) $24$

(c) $12$

(d) $30$

---

**10.** How many permutations of $\{1,2,3,4,5\}$ have **exactly three fixed points**?

A fixed point is an element $i$ such that $f(i)=i$.

(a) $5$

(b) $10$

(c) $20$

(d) $60$

---

**11.** What is the coefficient of $x^2$ in

$$
(1+2x)^5?
$$

(a) $\binom52$

(b) $\binom52 2^3$

(c) $\binom53 2^3$

(d) $\binom52 2^2$

---

**12.** For which truth values is $p\to q$ **false**?

(a) $p=T,\ q=F$

(b) $p=T,\ q=T$

(c) $p=F,\ q=F$

(d) $p=F,\ q=T$

---

**13.** Which expression is the negation of

$$
\forall x\in D\;\bigl(P(x)\to Q(x)\bigr)?
$$

(a) $\exists x\in D\;\bigl(\neg P(x)\vee Q(x)\bigr)$

(b) $\forall x\in D\;\bigl(P(x)\wedge\neg Q(x)\bigr)$

(c) $\exists x\in D\;\bigl(P(x)\wedge\neg Q(x)\bigr)$

(d) $\exists x\in D\;\bigl(\neg P(x)\wedge Q(x)\bigr)$

---

**14.** Define a relation $R$ on $\mathbb Z$ by

$$
xRy\iff |x-y|\le1.
$$

Which description is correct?

(a) Reflexive, antisymmetric and transitive

(b) Reflexive and symmetric, but not transitive

(c) Symmetric and transitive, but not reflexive

(d) An equivalence relation

---

**15.** A connected graph has vertex degrees

$$
1,2,2,2,3.
$$

Which statement is correct?

(a) It has an Eulerian circuit.

(b) It has no Eulerian trail.

(c) It has exactly four edges.

(d) It has an Eulerian trail but no Eulerian circuit.

---

**16.** Which list **cannot** be the vertex degrees of a simple graph with six vertices?

(a) $5,2,2,2,1,0$

(b) $2,2,2,2,2,2$

(c) $5,1,1,1,1,1$

(d) $3,3,3,3,3,3$

---

**17.** For positive integers $n$, let

$$
h(n)=4n^2+7n+2.
$$

Which statement is **false**?

(a) $h(n)\in O(n^3)$

(b) $h(n)\in\Omega(n)$

(c) $h(n)\in\Theta(n)$

(d) $h(n)\in\Theta(n^2)$

---

**18.** A fair coin is tossed four times. What is the probability of obtaining **at least three heads**?

(a) $\frac14$

(b) $\frac5{16}$

(c) $\frac38$

(d) $\frac12$

---

**19.** A finite-state machine starts in state $s_0$. Each table entry gives:

$$
\text{next state / output}.
$$

| Current state | Input $0$ | Input $1$ |
|---|---|---|
| $s_0$ | $s_1/1$ | $s_0/0$ |
| $s_1$ | $s_0/0$ | $s_1/1$ |

What **output string** is produced by the input `0110`?

(a) `1000`

(b) `0110`

(c) `1100`

(d) `1110`

---

**20.** A grammar has start symbol $S$, terminal alphabet $\{a,b\}$, and productions

$$
S\to aS\mid b.
$$

Which string **cannot** be generated by this grammar?

(a) `aba`

(b) `b`

(c) `ab`

(d) `aaab`

---

**End of paper**

交答案时可以写成 `1c 2b …`；有疑问的题在旁边标一个 `?`。


我会按知识库里 2019、2025 两张样卷的题型和难度分布出一套完整英文卷，保持选择题、大题各占 50%，并校验单选答案和大题条件。你吃完饭可以直接限时做。


这套按 **2019、2025 样卷的题型分布**编排，包含基础题和综合题，不只是重复刚练过的题。**已逐题核对，每道选择题只有一个正确答案。**它用于检验当前水平，但不能保证与正式考试等难。

建议饭后完整限时做：**阅读 10 分钟，作答 2 小时**。不查资料；不认识的单词圈起来，不会的题保留过程。先不附答案。

# MATH1064 — Practice Examination 5

**Reading time:** 10 minutes  
**Writing time:** 2 hours  
**Total marks:** 100

- Section A: 20 multiple-choice questions, worth **50 marks**.
- Section B: 5 extended-answer questions, worth **50 marks**.
- Select exactly one option for each multiple-choice question.
- Show your working and justify your answers in Section B.

**Notation:** $\mathbb N_0=\{0,1,2,\ldots\}$. The symbol $\subseteq$ allows equality. All graphs are finite, simple and undirected unless otherwise stated.

---

## Section A — Multiple Choice

**Each question is worth 2.5 marks.**

**1.** Let

$$
A=\{1,\{1\},\varnothing\}.
$$

Which statement is **false**?

(a) $\{1\}\in A$

(b) $\{1\}\subseteq A$

(c) $\{\varnothing\}\subseteq A$

(d) $\{1,\varnothing\}\in A$

---

**2.** Let

$$
S=\{a,b\}\times\{0,1,2\},
\qquad
T=\mathcal P(\mathcal P(\{x,y\})).
$$

Which statement is correct?

(a) $|S|=6$ and $|T|=8$

(b) $|S|=6$ and $|T|=16$

(c) $|S|=8$ and $|T|=16$

(d) $|S|=6$ and $|T|=4$

---

**3.** In a group of $50$ students, $28$ study mathematics, $24$ study physics, and $10$ study both.

How many students study neither subject?

(a) $2$

(b) $8$

(c) $12$

(d) $18$

---

**4.** Let

$$
f:\mathbb Z\to\mathbb Z,\qquad f(n)=3n+1.
$$

Then $f$ is:

(a) injective but not surjective.

(b) surjective but not injective.

(c) bijective.

(d) neither injective nor surjective.

---

**5.** Which function $f:\mathbb Z\times\mathbb Z\to\mathbb Z$ is **not surjective**?

(a) $f(a,b)=a-b$

(b) $f(a,b)=a$

(c) $f(a,b)=2a+4b$

(d) $f(a,b)=a+2b$

---

**6.** How many integers from $1$ to $72$, inclusive, are relatively prime to $12$?

(a) $12$

(b) $18$

(c) $24$

(d) $36$

---

**7.** A café sells four flavours of tea and three flavours of coffee. A customer buys exactly five packets of tea and exactly four packets of coffee.

Packets of the same drink and flavour are indistinguishable. Each flavour is available in unlimited quantities.

How many selections are possible?

(a) $\binom83\binom62$

(b) $\binom54\binom43$

(c) $\binom84\binom63$

(d) $4^5\,3^4$

---

**8.** How many distinct arrangements of the letters in `PEPPER` are possible?

(a) $30$

(b) $60$

(c) $120$

(d) $180$

---

**9.** How many permutations of $\{1,2,3,4\}$ have **exactly one fixed point**?

A fixed point is an element $i$ such that $f(i)=i$.

(a) $4$

(b) $6$

(c) $8$

(d) $12$

---

**10.** Write

$$
(2+x)^6=\sum_{k=0}^{6}a_kx^k.
$$

What is $a_4$?

(a) $\binom64 2^4$

(b) $\binom64 2^2$

(c) $\binom62 2^4$

(d) $\binom64$

---

**11.** Which proposition is a tautology?

(a) $((p\to q)\wedge p)\to q$

(b) $((p\to q)\wedge q)\to p$

(c) $(p\vee q)\to p$

(d) $p\wedge\neg p$

---

**12.** What is the negation of

$$
\forall x\in D\;\exists y\in D\;
\bigl(P(x)\wedge Q(y)\bigr)?
$$

(a) $\exists x\in D\;\forall y\in D\;
\bigl(\neg P(x)\vee\neg Q(y)\bigr)$

(b) $\exists x\in D\;\forall y\in D\;
\bigl(\neg P(x)\wedge\neg Q(y)\bigr)$

(c) $\forall x\in D\;\exists y\in D\;
\bigl(\neg P(x)\vee\neg Q(y)\bigr)$

(d) $\exists x\in D\;\exists y\in D\;
\bigl(\neg P(x)\vee\neg Q(y)\bigr)$

---

**13.** Define a relation $R$ on $\mathbb Z$ by

$$
xRy\iff 3\mid(x-y).
$$

Which set is the equivalence class containing $1$?

(a) $\{3k:k\in\mathbb Z\}$

(b) $\{3k+1:k\in\mathbb Z\}$

(c) $\{3k+2:k\in\mathbb Z\}$

(d) $\{1,3,5,7,\ldots\}$

---

**14.** A graph has adjacency matrix

$$
M=
\begin{pmatrix}
0&1&1&0\\
1&0&1&0\\
1&1&0&1\\
0&0&1&0
\end{pmatrix}.
$$

How many edges does it have?

(a) $3$

(b) $4$

(c) $5$

(d) $8$

---

**15.** Which graph has an Eulerian circuit?

(a) The complete graph $K_4$

(b) The complete graph $K_6$

(c) The cycle graph $C_6$

(d) A connected graph with exactly two vertices of odd degree

---

**16.** Which list **cannot** be the vertex degrees of a simple graph with five vertices?

(a) $4,2,2,1,1$

(b) $3,3,2,2,2$

(c) $4,3,2,1,0$

(d) $2,2,2,1,1$

---

**17.** Which function belongs to $O(n^3)$ but **not** to $\Theta(n^3)$?

(a) $n^3+4n$

(b) $7n^3+1$

(c) $n^2+5n+2$

(d) $n^4+n$

---

**18.** A biased coin has probability $\frac23$ of landing heads. It is tossed three times independently.

What is the probability of obtaining **exactly two heads**?

(a) $\frac4{27}$

(b) $\frac8{27}$

(c) $\frac49$

(d) $\frac23$

---

**19.** A finite-state machine starts in state $s_0$. Each table entry gives **next state / output**.

| Current state | Input $0$ | Input $1$ |
|---|---|---|
| $s_0$ | $s_1/1$ | $s_0/0$ |
| $s_1$ | $s_0/0$ | $s_1/1$ |

What output string is generated by the input `01011`?

(a) `01011`

(b) `11000`

(c) `11100`

(d) `10011`

---

**20.** A sequence is defined by

$$
a_0=3,\qquad a_{n+1}=2a_n-1.
$$

A student conjectures that $a_n=2^{n+1}+1$.

Assuming $a_k=2^{k+1}+1$, which calculation correctly establishes the induction step?

(a) $a_{k+1}=2^{k+1}+1$

(b) $a_{k+1}=2(2^{k+1}+1)-1=2^{k+2}+1$

(c) $a_{k+1}=2(2^{k+1}+1)+1=2^{k+2}+3$

(d) $a_{k+1}=2^{k+1}+1-1=2^{k+1}$

---

## Section B — Extended Answer

**Each question is worth 10 marks.**

### Question 1 — Sets and Functions [10 marks]

**(a) [2 marks]** Let

$$
A=\{0,\{0\},\varnothing\}.
$$

Determine whether each statement is true or false.

(i) $\{0\}\subseteq A$

(ii) $\{\{0\}\}\in A$

(iii) $\varnothing\in\mathcal P(A)$

(iv) $|\mathcal P(A)|=8$

**(b) [4 marks]** Define

$$
f:\mathbb Z\to\mathbb Z,\qquad
f(n)=\left\lfloor\frac n3\right\rfloor.
$$

Determine whether $f$ is injective and whether it is surjective. Justify both answers.

**(c) [2 marks]** Define

$$
g:\mathbb Z\to\mathbb Z,\qquad g(n)=n^2.
$$

Find:

(i) $g(\{-2,-1,0,1,2\})$;

(ii) $g^{-1}(\{1,4\})$.

Here $g^{-1}(B)$ denotes the set of all inputs whose outputs belong to $B$.

**(d) [2 marks]** Let $u:X\to Y$ and $v:Y\to Z$.

Prove that if $v\circ u$ is surjective, then $v$ is surjective.

---

### Question 2 — Counting and Probability [10 marks]

**(a) [2 marks]** Find the coefficient of $x^3$ in

$$
(1+2x)^6.
$$

You may leave your answer in terms of a binomial coefficient.

**(b) [2 marks]** How many distinct arrangements of the letters in `BANANA` have the two letters `N` adjacent?

Explain your method.

**(c) [2 marks]** Seven identical counters are placed into three distinct boxes. Each box must contain at least one counter.

How many distributions are possible? Explain how you account for the restriction.

**(d) [4 marks]** Box $A$ contains three red balls and one blue ball. Box $B$ contains one red ball and three blue balls.

A box is chosen with equal probability, and one ball is drawn uniformly at random from that box.

(i) Find the probability that the ball is red.

(ii) Given that the ball is red, find the probability that Box $A$ was selected.

---

### Question 3 — Number Theory and Induction [10 marks]

**(a) [3 marks]** Use the Euclidean algorithm to find

$$
\gcd(493,319).
$$

Show all divisions with remainders.

**(b) [3 marks]** Prove that for every integer $n$,

$$
n^2\equiv0\text{ or }1\pmod3.
$$

**(c) [4 marks]** Prove by mathematical induction that

$$
8\mid(3^{2n}-1)
$$

for every $n\in\mathbb N_0$.

Clearly state the base case, induction hypothesis and induction step.

---

### Question 4 — Relations and Graph Theory [10 marks]

**(a) [4 marks]** Let $S=\{1,2,3,4\}$ and define

$$
R=
\{
(1,1),(2,2),(3,3),(4,4),
(1,2),(2,1),(2,3),(3,2)
\}.
$$

Determine whether $R$ is:

(i) reflexive;

(ii) symmetric;

(iii) transitive;

(iv) antisymmetric.

Give a reason or counterexample for each answer.

**(b) [3 marks]** Let $G$ have vertex set $\{1,2,3,4,5\}$ and edge set

$$
E=
\{
\{1,2\},\{2,3\},\{3,1\},
\{3,4\},\{4,5\}
\}.
$$

(i) State the degree of each vertex.

(ii) Determine whether $G$ has an Eulerian circuit or an Eulerian trail that is not a circuit. Justify your answer.

(iii) Write down an Eulerian trail if one exists.

**(c) [3 marks]** Prove that every simple graph on five vertices with at least seven edges is connected.

Your proof must explain why a disconnected graph on five vertices has at most six edges.

---

### Question 5 — Logic and Modelling Computation [10 marks]

**(a) [2 marks]** Write the negation of the following statement. Move the negation inside so that it applies only to $P$ and $Q$.

$$
\forall x\in D\;\bigl(P(x)\to Q(x)\bigr).
$$

**(b) [2 marks]** Determine whether the following argument is valid. Give a reason or a counterexample using truth values.

$$
p\to q,\qquad \neg q,\qquad \therefore\neg p.
$$

**(c) [3 marks]** A finite-state machine starts in $s_0$. Each entry gives **next state / output**.

| Current state | Input $0$ | Input $1$ |
|---|---|---|
| $s_0$ | $s_0/1$ | $s_1/0$ |
| $s_1$ | $s_0/0$ | $s_1/1$ |

For input `1010`:

(i) list the state reached after each input symbol;

(ii) give the output string;

(iii) give the final state.

**(d) [3 marks]** A grammar has start symbol $S$, terminal alphabet $\{a,b\}$ and productions

$$
S\to aS\mid bB,\qquad B\to bB\mid b.
$$

(i) Give a derivation of `aabbb`.

(ii) Describe the generated language using set-builder notation.

(iii) State whether the empty string belongs to the language, with a reason.

---

**End of Examination**