[[Python 技术文档]]
## 第1题：输出1–20之间的奇数  
**Task:** Print all odd numbers from 1 to 20, separated by spaces.

**示例 / Example Output:**  
```
1 3 5 7 9 11 13 15 17 19
```

**答案 / Answer:**
```python
for i in range(1, 21):
    if i % 2 != 0:
        print(i, end=" ")
```

---

## 第2题：输出1–20之间的偶数  
**Task:** Print all even numbers from 1 to 20, separated by spaces.

**示例 / Example Output:**  
```
2 4 6 8 10 12 14 16 18 20
```

**答案 / Answer:**
```python
for i in range(1, 21):
    if i % 2 == 0:
        print(i, end=" ")
```

---

## 第3题：计算列表中所有数字的总和  
**Task:** Create a function `sum_list(nums)` that returns the sum of all elements in a list.

**示例 / Example:**  
```
输入 Input: [5, 10, 15]
输出 Output: 30
```

**答案 / Answer:**
```python
def sum_list(nums):
    total = 0
    for n in nums:
        total += n
    return total

print(sum_list([5, 10, 15]))
```

---

## 第4题：合并两个列表  
**Task:** Combine two lists `[1, 2, 3]` and `[4, 5, 6]` into a new list.

**输出 / Output:**  
```
[1, 2, 3, 4, 5, 6]
```

**答案 / Answer:**
```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = list1 + list2
print(combined)
```

---

## 第5题：提取列表中的奇数元素  
**Task:** Write a function that returns a new list containing only the odd numbers.

**示例 / Example:**  
```
输入 Input: [1, 4, 7, 10, 13]
输出 Output: [1, 7, 13]
```

**答案 / Answer:**
```python
def odd_elements(lst):
    result = []
    for n in lst:
        if n % 2 != 0:
            result.append(n)
    return result

print(odd_elements([1, 4, 7, 10, 13]))
```

---

## 第6题：拼接字符串列表  
**Task:** Combine the list `["Python", "is", "fun"]` into a single sentence.

**输出 / Output:**  
```
Python is fun
```

**答案 / Answer:**
```python
words = ["Python", "is", "fun"]
sentence = " ".join(words)
print(sentence)
```

---

## 第7题：反转每个单词  
**Task:** Write a function `reverse_words(words)` that reverses each string in a list.

**示例 / Example:**  
```
输入 Input: ["apple", "banana", "orange"]
输出 Output: ["elppa", "ananab", "egnaro"]
```

**答案 / Answer:**
```python
def reverse_words(words):
    return [w[::-1] for w in words]

print(reverse_words(["apple", "banana", "orange"]))
```

---

## 第8题：计算列表元素总和  
**Task:** Given `[4, 7, 11, 3]`, print the total sum of numbers.

**输出 / Output:**  
```
Total: 25
```

**答案 / Answer:**
```python
numbers = [4, 7, 11, 3]
print("Total:", sum(numbers))
```

---

## 第9题：偶数翻倍  
**Task:** Write a function that doubles all even numbers, keeping odd numbers unchanged.

**示例 / Example:**  
```
输入 Input: [2, 5, 8, 3]
输出 Output: [4, 5, 16, 3]
```

**答案 / Answer:**
```python
def double_evens(nums):
    result = []
    for n in nums:
        if n % 2 == 0:
            result.append(n * 2)
        else:
            result.append(n)
    return result

print(double_evens([2, 5, 8, 3]))
```

---

## 第10题：统计每个单词中的元音字母数量  
**Task:** Write a function `count_vowels(words)` to count the number of vowels (a, e, i, o, u) in each word.

**示例 / Example:**  
```
输入 Input: ["apple", "sky", "orange"]
输出 Output: [2, 0, 3]
```

**答案 / Answer:**
```python
def count_vowels(words):
    vowels = "aeiou"
    result = []
    for w in words:
        count = sum(1 for c in w if c.lower() in vowels)
        result.append(count)
    return result

print(count_vowels(["apple", "sky", "orange"]))
```

---

## 第11题：两个列表按位相加  
**Task:** Given two lists of the same length, add corresponding elements.

**示例 / Example:**  
```
输入 Input: a = [3, 5, 2], b = [7, 1, 4]
输出 Output: [10, 6, 6]
```

**答案 / Answer:**
```python
a = [3, 5, 2]
b = [7, 1, 4]
result = [a[i] + b[i] for i in range(len(a))]
print(result)
```

---

## 第12题：筛选短单词  
**Task:** Print all words whose length is less than 5.

**示例 / Example:**  
```
输入 Input: ["elephant", "dog", "cat", "bear", "tiger"]
输出 Output:
dog
cat
bear
```

**答案 / Answer:**
```python
words = ["elephant", "dog", "cat", "bear", "tiger"]
for w in words:
    if len(w) < 5:
        print(w)
```

---

## 第13题：用索引序号替换字母  
**Task:** Convert each word to a string of index numbers joined by hyphens.

**示例 / Example:**  
```
输入 Input: ["hi", "sun"]
输出 Output: ["0-1", "0-1-2"]
```

**答案 / Answer:**
```python
def replace_with_index(words):
    result = []
    for w in words:
        indices = "-".join(str(i) for i in range(len(w)))
        result.append(indices)
    return result

print(replace_with_index(["hi", "sun"]))
```

---

## 第14题：计算平均值  
**Task:** Calculate and print the average of numbers in a list.

**示例 / Example:**  
```
输入 Input: [10, 15, 25]
输出 Output: Average: 16.6666667
```

**答案 / Answer:**
```python
nums = [10, 15, 25]
average = sum(nums) / len(nums)
print("Average:", average)
```

---

## 第15题：判断是否为回文字符串  
**Task:** Write a function to check if a word reads the same forward and backward.

**示例 / Example:**  
```
输入 Input: "level" → True
输入 Input: "python" → False
```

**答案 / Answer:**
```python
def is_palindrome(word):
    return word == word[::-1]

print(is_palindrome("level"))
print(is_palindrome("python"))
```

---

## 第16题：用连字符连接字符串  
**Task:** Join all strings in a list using hyphens.

**示例 / Example:**  
```
输入 Input: ["red", "green", "blue"]
输出 Output: red-green-blue
```

**答案 / Answer:**

```python
def combine(words):
    return "-".join(words)

print(combine(["red", "green", "blue"]))
```

---

## 第17题：打印奇数并求和  
**Task:** Input an integer n. Print all odd numbers from 1 to n and their total sum.

**示例 / Example:**  
```
输入 Input: 10
输出 Output:
Odd numbers are: 1 3 5 7 9
Sum of odd numbers: 25
```

**答案 / Answer:**

```python
n = int(input("Enter a number: "))
odd_sum = 0
print("Odd numbers are:", end=" ")
for i in range(1, n + 1):
    if i % 2 != 0:
        print(i, end=" ")
        odd_sum += i
print("\nSum of odd numbers:", odd_sum)
```

---

## 第18题：天数换算成几周几天  

**Task:**  
编写一个函数，将给定的天数转换为“几周几天”。

**示例 / Example:**  
```
输入 Input: 10  
输出 Output: "1 week(s) and 3 day(s)"
```

**答案 / Answer:**
```python
def days_to_weeks(days):
    weeks = days // 7
    remaining_days = days % 7
    return f"{weeks} week(s) and {remaining_days} day(s)"

print(days_to_weeks(10))
```

---

## 第19题：将列表转换为字典  

**Task:**  
将一个列表 `[key1, value1, key2, value2, ...]` 转换为字典。

**示例 / Example:**  
```
输入 Input: ["name", "Tom", "age", "18"]
输出 Output: {"name": "Tom", "age": "18"}
```

**答案 / Answer:**
```python
def list_to_dict(lst):
    result = {}
    for i in range(0, len(lst), 2):
        result[lst[i]] = lst[i + 1]
    return result

print(list_to_dict(["name", "Tom", "age", "18"]))
```

---

## 第20题：统计字母出现次数  

**Task:**  
统计字符串中每个字母出现的次数，返回字典。

**示例 / Example:**  
```
输入 Input: "banana"  
输出 Output: {"b": 1, "a": 3, "n": 2}
```

**答案 / Answer:**
```python
def count_letters(word):
    counts = {}
    for ch in word:
        counts[ch] = counts.get(ch, 0) + 1
    return counts

print(count_letters("banana"))
```

---

## 第21题：控制台输入多个单词，返回最短的  

**Task:**  
让用户在控制台输入多个单词（用空格分隔），返回最短的单词。  

**示例 / Example:**  

```
输入 Input: (console) hello sun python  
输出 Output: sun
```

**答案 / Answer:**
```python
def shortest_word():
    words = input("请输入多个单词（空格分隔）：").split()
    shortest = min(words, key=len)
    print(shortest)

# 示例运行
# shortest_word()
```

---

## 第22题：保留列表中只含 `'a'` 的单词  

**Task:**  
筛选出包含字母 `'a'` 的单词，只保留这些单词。

**示例 / Example:**  
```
输入 Input: ["apple", "sun", "banana", "pear"]
输出 Output: ["apple", "banana", "pear"]
```

**答案 / Answer:**

```python
def keep_words_with_a(words):
    return [w for w in words if 'a' in w]

print(keep_words_with_a(["apple", "sun", "banana", "pear"]))
```

---
# Python 基础编程练习（编号 23–55）

> **涵盖知识点：** for/while 循环、条件判断、列表操作、字符串处理、字典、函数定义、`input()`、列表推导式、切片、`range()`、`join()`、`split()`、列表↔字典↔字符串互转

---

## 23

**Task:** Print all multiples of 3 from 1 to 30, separated by spaces.

**示例 / Example Output:**
```
3 6 9 12 15 18 21 24 27 30
```

---

## 24

**Task:** Calculate the sum of all integers from 1 to 100.

**输出 / Output:**
```
5050
```

---

## 25

**Task:** Write a function `find_max(nums)` that returns the largest number in a list (without using `max()`).

**示例 / Example:**
```
输入 Input: [3, 8, 1, 12, 5]
输出 Output: 12
```

---

## 26

**Task:** Write a function `find_min(nums)` that returns the smallest number in a list.

**示例 / Example:**
```
输入 Input: [9, 4, 7, 2, 6]
输出 Output: 2
```

---

## 27

**Task:** Count how many positive numbers are in the list.

**示例 / Example:**
```
输入 Input: [-3, 5, 0, 8, -1, 2]
输出 Output: 3
```

---

## 28

**Task:** Reverse a list without using `reverse()` or `[::-1]`.

**示例 / Example:**
```
输入 Input: [1, 2, 3, 4, 5]
输出 Output: [5, 4, 3, 2, 1]
```

---

## 29

**Task:** Remove duplicate values from a list, preserving order.

**示例 / Example:**
```
输入 Input: [1, 2, 2, 3, 4, 4, 5]
输出 Output: [1, 2, 3, 4, 5]
```

---

## 30

**Task:** Write a function `is_prime(n)` that returns `True` if `n` is a prime number.

**示例 / Example:**
```
输入 Input: 7  → True
输入 Input: 10 → False
```

---

## 31

**Task:** Calculate the factorial of a given number `n` (i.e., `n!`).

**示例 / Example:**
```
输入 Input: 5
输出 Output: 120
```

---

## 32

**Task:** Print the first `n` numbers of the Fibonacci sequence.

**示例 / Example:**
```
输入 Input: 8
输出 Output: 0 1 1 2 3 5 8 13
```

---

## 33

**Task:** Count the total number of vowels in a string.

**示例 / Example:**
```
输入 Input: "Hello World"
输出 Output: 3
```

---

## 34

**Task:** Swap the case of each character in a string.

**示例 / Example:**
```
输入 Input: "Hello World"
输出 Output: "hELLO wORLD"
```

---

## 35

**Task:** Check whether a list is sorted in ascending order.

**示例 / Example:**
```
输入 Input: [1, 3, 5, 7]  → True
输入 Input: [1, 3, 2, 4]  → False
```

---

## 36

**Task:** Find the second-largest number in a list.

**示例 / Example:**
```
输入 Input: [4, 1, 9, 7, 3]
输出 Output: 7
```

---

## 37

**Task:** Capitalize the first letter of each word in a sentence.

**示例 / Example:**
```
输入 Input: "hello python world"
输出 Output: "Hello Python World"
```

---

## 38

**Task:** Count how many words are in a sentence.

**示例 / Example:**
```
输入 Input: "I love programming in Python"
输出 Output: 5
```

---

## 39

**Task:** Compute the greatest common divisor of two integers.

**示例 / Example:**
```
输入 Input: 12, 18
输出 Output: 6
```

---

## 40

**Task:** Convert Celsius to Fahrenheit using the formula `F = C * 9/5 + 32`.

**示例 / Example:**
```
输入 Input: 25
输出 Output: 77.0
```

---

## 41

**Task:** Determine whether a given year is a leap year.

**示例 / Example:**
```
输入 Input: 2024 → True
输入 Input: 2023 → False
```

---

## 42

**Task:** Return a new list with each number squared.

**示例 / Example:**
```
输入 Input: [1, 2, 3, 4]
输出 Output: [1, 4, 9, 16]
```

---

## 43

**Task:** Merge two dictionaries into one.

**示例 / Example:**
```
输入 Input: {"a": 1, "b": 2}, {"c": 3, "d": 4}
输出 Output: {"a": 1, "b": 2, "c": 3, "d": 4}
```

---

## 44

**Task:** Return the key with the maximum value in a dictionary.

**示例 / Example:**
```
输入 Input: {"a": 10, "b": 25, "c": 7}
输出 Output: "b"
```

---

## 45

**Task:** Calculate the product of all numbers in a list.

**示例 / Example:**
```
输入 Input: [1, 2, 3, 4]
输出 Output: 24
```

---

## 46

**Task:** Check if a string contains any digit.

**示例 / Example:**
```
输入 Input: "hello123" → True
输入 Input: "hello"    → False
```

---

## 47

**Task:** Remove all whitespace from a given string.

**示例 / Example:**
```
输入 Input: "  hello   world  "
输出 Output: "helloworld"
```

---

## 48

**Task:** Return a list of indices where the numbers are even.

**示例 / Example:**
```
输入 Input: [1, 2, 3, 4, 5, 6]
输出 Output: [1, 3, 5]
```

---

## 49

**Task:** Convert a number of seconds into `HH:MM:SS` format.

**示例 / Example:**
```
输入 Input: 3661
输出 Output: "01:01:01"
```

---

## 50

**Task:** Return the common elements between two lists.

**示例 / Example:**
```
输入 Input: [1, 2, 3, 4], [3, 4, 5, 6]
输出 Output: [3, 4]
```

---

## 51

**Task:** Return a dictionary mapping each word to its length.

**示例 / Example:**
```
输入 Input: "I love python"
输出 Output: {"I": 1, "love": 4, "python": 6}
```

---

## 52

**Task:** Print the 9×9 multiplication table.

**示例 / Example Output（部分）:**
```
1*1=1
2*1=2 2*2=4
3*1=3 3*2=6 3*3=9
...
9*1=9 9*2=18 ... 9*9=81
```

---

## 53

**Task:** Convert a list of words into a dictionary where each **key** is a unique word and each **value** is the number of times that word appears in the list (word frequency count).

**示例 / Example:**
```
输入 Input: ["apple", "banana", "apple", "orange", "banana", "apple"]
输出 Output: {"apple": 3, "banana": 2, "orange": 1}
```

**进阶 / Bonus:** 试试用一个英文句子作为输入，先 split 成 list，再统计每个单词的出现次数。
```
输入 Input: "the cat and the dog and the bird"
输出 Output: {"the": 3, "cat": 1, "and": 2, "dog": 1, "bird": 1}
```

---

## 54

**Task:** Convert a dictionary into a list of `(key, value)` tuples (or a list of `[key, value]` pairs).

**示例 / Example:**
```
输入 Input: {"name": "Alice", "age": 20, "city": "Sydney"}
输出 Output: [("name", "Alice"), ("age", 20), ("city", "Sydney")]
```

**进阶 / Bonus:** 只返回所有 keys 的列表 和 所有 values 的列表。
```
输入 Input: {"a": 1, "b": 2, "c": 3}
输出 Output:
  keys   = ["a", "b", "c"]
  values = [1, 2, 3]
```

---

## 55

**Task:** Convert a string into a list. Implement the following three conversions:

1. Convert a string into a list of **characters**.
2. Convert a sentence into a list of **words** (split by spaces).
3. Convert a comma-separated string into a list of **items** (strip extra spaces).

**示例 / Example:**
```
输入 Input 1: "hello"
输出 Output 1: ["h", "e", "l", "l", "o"]

输入 Input 2: "I love python programming"
输出 Output 2: ["I", "love", "python", "programming"]

输入 Input 3: "apple, banana, orange, grape"
输出 Output 3: ["apple", "banana", "orange", "grape"]
```

---

## 56

Write a function called `count_words` that takes a list of words as a parameter and returns a dictionary where each unique word is a key and its value is the number of times that word appears in the list.

**Function signature:**
```python
def count_words(words: list) -> dict:
```

**Requirements:**
- The function should be case-sensitive (e.g., "Hello" and "hello" are different words)
- If the input list is empty, return an empty dictionary
- The order of keys in the dictionary does not matter

**Example:**
```python
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
result = count_words(words)
print(result)
# Output: {'apple': 3, 'banana': 2, 'cherry': 1}

words = ["hello", "world", "hello"]
result = count_words(words)
print(result)
# Output: {'hello': 2, 'world': 1}

words = []
result = count_words(words)
print(result)
# Output: {}
```

---

## 57

Write a function called `dict_to_list` that takes a dictionary as a parameter and returns a list of tuples. Each tuple should contain a key-value pair from the dictionary, with the key as the first element and the value as the second element.

**Function signature:**
```python
def dict_to_list(data: dict) -> list:
```

**Requirements:**
- Each tuple in the list should be in the format (key, value)
- If the input dictionary is empty, return an empty list
- The order of tuples in the list does not matter

**Example:**
```python
data = {"name": "Alice", "age": 25, "city": "Boston"}
result = dict_to_list(data)
print(result)
# Output: [('name', 'Alice'), ('age', 25), ('city', 'Boston')]
# Note: Order may vary

data = {"apple": 3, "banana": 2}
result = dict_to_list(data)
print(result)
# Output: [('apple', 3), ('banana', 2)]

data = {}
result = dict_to_list(data)
print(result)
# Output: []
```

---

## **58**

Write a function called `calculate_grade_stats` that takes a list of student names and a list of their corresponding scores. The function should return a dictionary where each student name is a key and the value is another dictionary containing their score and grade letter.

**Function signature:**
```python
def calculate_grade_stats(names: list, scores: list) -> dict:
```

**Requirements:**
- The two lists will always have the same length
- Grade letters are assigned as follows:
  - 90-100: "A"
  - 80-89: "B"
  - 70-79: "C"
  - 60-69: "D"
  - Below 60: "F"
- Each student's value should be a dictionary with keys "score" and "grade"
- If both input lists are empty, return an empty dictionary

**Example:**
```python
names = ["Alice", "Bob", "Charlie"]
scores = [95, 82, 67]
result = calculate_grade_stats(names, scores)
print(result)
# Output: {
#     'Alice': {'score': 95, 'grade': 'A'},
#     'Bob': {'score': 82, 'grade': 'B'},
#     'Charlie': {'score': 67, 'grade': 'D'}
# }

names = ["David", "Emma"]
scores = [78, 55]
result = calculate_grade_stats(names, scores)
print(result)
# Output: {
#     'David': {'score': 78, 'grade': 'C'},
#     'Emma': {'score': 55, 'grade': 'F'}
# }

names = []
scores = []
result = calculate_grade_stats(names, scores)
print(result)
# Output: {}
```

---

