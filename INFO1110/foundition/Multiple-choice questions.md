[[Python 技术文档]]

---

# Python Foundation Test - Multiple Choice Questions

## Section 1: Basics (Q1-5)

**1. What will the following code print?**
```python
print("Python", end="@")
print("Code")
```

a) Python Code  
b) Python@Code  
c) Python@ Code  
d) PythonCode@

**2. Which of the following is NOT a valid variable name in Python?**

a) `user_name`  
b) `data2024`  
c) `2nd_value`  
d) `my_list`

**3. Which of the following is a valid assignment statement with correct type hint?**

a) `count#int = 50`  
b) `price: float = 19.99`  
c) `is_active: bool = "True"`  
d) `@name = "Alice"`

**4. What will the following code print?**
```python
print("A", "B", "C", sep=" - ")
```

a) "A", "B", "C"  
b) A - B - C  
c) A B C  
d) A-B-C

**5. What will the following code print?**
```python
print("Ha" * 3 + "!")
```

a) Ha3!  
b) HaHaHa!  
c) Ha Ha Ha!  
d) HaHa!

---

## Section 2: Flow Control (Q6-10)

**6. If the missing lines are filled in correctly, the program should add each number in the list `scores` to the running total. The `total` should be printed after all additions are completed. For example, if `scores` is `[10, 20, 30]` then the output will be:**

```
Total: 60

1  scores = [10, 20, 30]
2  total = 0
3
4  for score in scores:
5      # (code WILL go here)
6  # ...
```

Which of the following options is the correct missing code?

a) `5 total = total + scores[score]  6 print('Total:', total)`  
b) `5 total = total + score  6 print('Total:', total)`  
c) `5 print('Total:', total)  6 total = total + score`  
d) `5 total = score  6 print('Total:', total)`

**7. What will be the output of the program after the following code fragment is executed?**

```python
1  colors = ['red', 'blue', 'green']
2  positions = [0, 2, 1]
3  for color in colors:
4      for pos in positions:
5          print(color[pos], end=' ')
6      print()
```

a) r d e  
   b u l  
   g e r

b) r e d  
   b l u  
   g r e

c) d e r  
   l u b  
   e r g

d) e r d  
   u b l  
   r g e

**8. Consider the code fragment below. It has a missing piece of code indicated by XXXXX. The program checks if a number is divisible by either 5 or 7, and prints "Divisible by 5 or 7." if it is.**

```python
number = int(input("Enter a number: "))
while XXXXX:
    print("Divisible by 5 or 7.")
    number = int(input("Enter another number: "))
```

Which of the following is the correct completion of the while loop?

a) `number % 5 == 0 or number % 7 == 0`  
b) `number % 5, 7 == 0`  
c) `number % 5 == 7 or number % 7 == 5`  
d) `number % 0 == 5 or number % 0 == 7`

**9. What will be the output of the program after the following code fragment is executed?**

```python
1  limit = 3
2  n = 27
3
4  while n > limit:
5      print(n, end=' ')
6      n = n // 3
7
8  print(n, end=' ')
```

a) 27 9 3  
b) 27 9 3 1  
c) 9 3 1  
d) 9 3

**10. What will be the output of the program after the following code fragment is executed?**

```python
1  names = ['A', 'L', 'I', 'C', 'E']
2  for i in range(5):
3      print(names[4 - i], end=' ')
```

a) E C I L A  
b) A L I C  
c) It will print an IndexError  
d) A L I C E

---

## Section 3: Functions (Q11-15)

**11. If the missing lines are correctly filled in, the program should define a function named `create_label` that returns a formatted label with a given product and quantity. The `main()` function will use the `create_label` function to get the label and print it. Below is the output of the program:**

```
Product: Laptop - Quantity: 5
```

```python
1  def # (code WILL go here):
2      label = f'Product: {product} - Quantity: {qty}'
3      # (code MAY go here)
4
5  def main():
6      product = 'Laptop'
7      amount = 5
8      result = create_label(product, amount)
9      print(result)
10
11 main()
```

Which of the following options is the correct missing code?

a) `1 def create_label(product: str, amount: int):  3 return label`  
b) `1 def create_label(product: str, qty: int):  3 return label`  
c) `1 def create_label(name: str, amount: int):  3 # no code`  
d) `1 def create_label(product: str, qty: int):  3 print(label)`

**12. A function named `generate_code` has already been defined in the program. The function has the following signature:**

```python
generate_code(prefix: str, number: int) -> str:
```

The program should ask the user for a prefix and number, then use the `generate_code` function to create the formatted code from that input.

```python
# generate_code defined above
11 def main():
12     prefix = input('Enter prefix: ')
13     number = input('Enter number: ')
14     # (code WILL go here)
15     print(code)
16
17 main()
```

Which of the following options is the correct missing code on line 14?

a) `14 code = generate_code("PRE", 12345)`  
b) `14 code = generate_code(prefix, int(number))`  
c) `14 code = generate_code(prefix, number)`  
d) `14 generate_code(code)`

**13. What will be the output of the program after the following code fragment is executed?**

```python
def add_five(num: int):
    result = num + 5
    return result

def multiply_three(num: int):
    result = num * 3
    return result - 2

def main():
    a = 5
    b = 10
    print(add_five(a), end=' ')
    print(multiply_three(b), end=' ')
    print(a, end=' ')
    print(b)

main()
```

a) 10 28 5 10  
b) 10 28 10 28  
c) 5 10 5 10  
d) 5 10 10 28

**14. What will be the output of the program after the following code fragment is executed?**

```python
def convert_upper(text: str):
    print(text.upper())

def convert_lower(message: str):
    text = message
    print(text.lower())

def main():
    text = 'Hello WORLD'
    convert_lower('PYTHON ROCKS')
    convert_upper(text)

main()
```

a) HELLO WORLD  
   hello world

b) python rocks  
   HELLO WORLD

c) Hello World  
   PYTHON ROCKS  
   hello world

d) PYTHON ROCKS  
   python rocks

**15. What will be the output of the program after the following code fragment is executed?**

```python
def check_score(points: int):
    if points == 100:
        return 'Perfect score!'
    elif points >= 80:
        return 'Great job!'
    elif points >= 50:
        return 'Keep trying!'
    else:
        return 'Need more practice.'

print(check_score(100))
print(check_score(75))
print(check_score(90))
```

a) Perfect score!  
   Keep trying!  
   Great job!

b) Perfect score!  
   Great job!  
   Great job!

c) Perfect score!  
   Keep trying!  
   Keep trying!

d) Great job!  
   Great job!  
   Great job!

---

## Section 4: Testing/Debugging (Q16-20)

**16. Which of the following inputs would cause an error to be thrown in the code below?**

```python
values = ####
result = 0
for i in range(0, 3):
    idx = values[i]
    result += values[idx - 1]
```

a) No error will be thrown  
b) `values = [1, 2, 3, 4]`  
c) `values = [3, 2, 1, 0]`  
d) `values = [0, 1, 2, 3]`

**17. You're writing a program to categorize students based on age. You'd like to group them as follows:**

- child: 12 years or younger
- teen: Between 12 and 18 years, exclusive
- adult: 18 years or older

Which of the following sets of values, representing ages, would be most useful for testing your program?

a) `[5, 15, 25, 35]`  
b) `[0, 12, 15, 18]`  
c) `[10, 14, 20, 30]`  
d) `[11, 17, 19, 25]`

**18. Which line of code would cause an error to be thrown when this script is executed with the following inputs in this order: Alice, 999**

```python
1  name = input("Please enter your name: ")
2  code = input("Please enter a code: ")
3  merged = name + code
4  merged = merged * 2
5  target_char = merged[15]
6  print(target_char)
```

a) 5  
b) 2  
c) 3  
d) 4

**19. You're writing a function to categorize students based on age. It should return a category based on the following (assume all ages are positive integers):**

- child: 12 years or younger
- teen: Between 12 and 18 years, exclusive
- adult: 18 years or older

Which of the following implementations would have a logic error, based on the above problem description?

a) 
```python
def age_group(age):
    category = "child"
    if age >= 18:
        category = "adult"
    if age > 12:
        category = "teen"
    return category
```

b) 
```python
def age_group(age):
    if age <= 12:
        return "child"
    elif age < 18:
        return "teen"
    else:
        return "adult"
```

c) 
```python
def age_group(age):
    if age <= 12:
        return "child"
    if age < 18:
        return "teen"
    return "adult"
```

d) 
```python
def age_group(age):
    if age >= 18:
        category = "adult"
    elif age > 12:
        category = "teen"
    else:
        category = "child"
    return category
```

**20. Which of the following lines of code will run but then give a runtime error?**

a) `nums = [1, 3, 5]`  
   `print(nums[nums[0]])`

b) `nums = [1, 3, 5]`  
   `print(nums[nums[1]])`

c) `nums = [1, 3, 5]`  
   `print(nums[nums[2]])`

d) They will all give a runtime error.

---

# Python Foundation Test - Multiple Choice Questions (Advanced)

## Section 1: Basics (Q1-5)

**1. What will be the output of the following code?**
```python
x = "123"
y = "456"
z = x + y
print(z[2:5])
```

a) 345  
b) 234  
c) 456  
d) 3456

**2. Which of the following statements about Python variables and types is TRUE?**

a) Type hints in Python enforce type checking at runtime and will raise errors if violated  
b) Variables declared with type hints cannot be reassigned to values of different types  
c) The expression `x: int = "hello"` will cause a syntax error  
d) Type hints are optional annotations that don't affect runtime behavior

**3. What will be the output of the following code?**
```python
a = 10
b = 3
result = a // b + a % b * 2
print(result)
```

a) 5  
b) 7  
c) 9  
d) 11

**4. What will be the output of the following code?**
```python
text = "Python"
print(text[-2:] + text[:2])
```

a) onPy  
b) Pyon  
c) thonPy  
d) Pyth

**5. Which of the following expressions evaluates to `True`?**

a) `"abc" * 2 == "abcabc"`  
b) `"5" + "3" == 8`  
c) `len("hello") == 4`  
d) `"Python"[0] == "p"`

---

## Section 2: Flow Control (Q6-10)

**6. What will be the output of the following code?**
```python
numbers = [1, 2, 3, 4, 5]
count = 0
for num in numbers:
    if num % 2 == 0:
        count += num
    else:
        count += 1
print(count)
```

a) 3  
b) 9  
c) 10  
d) 15

**7. What will be the output of the following nested loop?**
```python
result = ""
for i in range(1, 4):
    for j in range(i):
        result += str(i)
print(result)
```

a) 123  
b) 122333  
c) 111222333  
d) 112233

**8. Consider the following code. What value of `x` would cause the loop to execute exactly 3 times?**
```python
x = ####
count = 0
while x > 5:
    x = x - 3
    count += 1
print(count)
```

a) 11  
b) 12  
c) 13  
d) 14

**9. What will be the output of the following code?**
```python
data = [10, 20, 30, 40]
total = 0
for i in range(len(data)):
    if i % 2 == 0:
        total += data[i]
    else:
        total -= data[i]
print(total)
```

a) 0  
b) -20  
c) 40  
d) 100

**10. What will be the output of the following code?**
```python
word = "PROGRAM"
output = ""
for i in range(0, len(word), 2):
    output += word[i]
print(output)
```

a) PORM  
b) PORA  
c) PRGA  
d) POGM

---

## Section 3: Functions (Q11-15)

**11. What will be the output of the following code?**
```python
def modify_list(items: list):
    items.append(100)
    items = [1, 2, 3]
    items.append(200)

def main():
    my_list = [10, 20]
    modify_list(my_list)
    print(my_list)

main()
```

a) `[10, 20]`  
b) `[10, 20, 100]`  
c) `[1, 2, 3, 200]`  
d) `[10, 20, 100, 200]`

**12. What will be the output of the following code?**
```python
def calculate(a: int, b: int) -> int:
    if a > b:
        return a - b
    elif a < b:
        return b - a
    return a + b

def main():
    x = 5
    y = 8
    result = calculate(y, x) + calculate(x, y)
    print(result)

main()
```

a) 0  
b) 3  
c) 6  
d) 13

**13. Consider the following code. What will be printed?**
```python
def process_text(text: str, repeat: int = 2) -> str:
    return text.upper() * repeat

def main():
    print(process_text("hi", 3))
    print(process_text("bye"))

main()
```

a) HIHIHI  
   BYEBYE

b) hihihi  
   byebye

c) HI HI HI  
   BYE BYE

d) HIHIHI  
   BYE

**14. What will be the output of the following code?**
```python
def mystery(n: int) -> int:
    if n <= 1:
        return 1
    return n + mystery(n - 2)

print(mystery(5))
```

a) 5  
b) 9  
c) 15  
d) The function will cause infinite recursion

**15. What will be the output of the following code?**
```python
def transform(values: list) -> list:
    result = []
    for val in values:
        if val > 10:
            result.append(val * 2)
        else:
            result.append(val)
    return result

def main():
    nums = [5, 15, 8, 20]
    new_nums = transform(nums)
    print(len(new_nums), sum(new_nums))

main()
```

a) 4 48  
b) 4 83  
c) 2 70  
d) 4 70

---

## Section 4: Testing/Debugging (Q16-20)

**16. Which of the following test cases would be MOST effective at detecting a boundary error in a function that categorizes temperature as "cold" (below 10), "mild" (10-25), or "hot" (above 25)?**

a) `[0, 15, 30]`  
b) `[5, 20, 35]`  
c) `[9, 10, 25, 26]`  
d) `[-10, 18, 40]`

**17. Consider the following function that should return the largest number in a list:**
```python
def find_max(numbers: list) -> int:
    max_val = 0
    for num in numbers:
        if num > max_val:
            max_val = num
    return max_val
```

Which input would reveal a bug in this implementation?

a) `[1, 2, 3, 4, 5]`  
b) `[10, 20, 5, 15]`  
c) `[-5, -2, -8, -1]`  
d) `[0, 0, 0, 0]`

**18. What type of error will occur when the following code is executed?**
```python
def calculate_average(scores: list) -> float:
    total = sum(scores)
    return total / len(scores)

grades = []
result = calculate_average(grades)
print(result)
```

a) Syntax error  
b) Type error  
c) ZeroDivisionError  
d) IndexError

**19. A programmer writes the following function to check if a string is a palindrome (reads the same forwards and backwards):**
```python
def is_palindrome(text: str) -> bool:
    reversed_text = ""
    for i in range(len(text)):
        reversed_text = text[i] + reversed_text
    return text == reversed_text
```

Which of the following test cases would FAIL with this implementation?

a) `is_palindrome("racecar")`  
b) `is_palindrome("Racecar")`  
c) `is_palindrome("hello")`  
d) `is_palindrome("noon")`

**20. Consider the following code that attempts to find the index of a target value in a list:**
```python
def find_index(items: list, target) -> int:
    for i in range(len(items)):
        if items[i] == target:
            return i
    return -1

numbers = [10, 20, 30, 40, 50]
position = find_index(numbers, 60)
result = numbers[position]
print(result)
```

What will happen when this code is executed?

a) It will print -1  
b) It will print 60  
c) It will raise an IndexError  
d) It will print 50

---

我会根据原始文件的考试结构，创建更多关于错误和调试的题目，保持相似的难度水平。

---

# Python Foundation Test - Error & Debugging Focus

## Section 1: Basics (Q1-5)

**1. Which of the following code snippets will cause a TypeError?**

a) `print("Score: " + str(85))`  
b) `print("Score: " + 85)`  
c) `print("Score:", 85)`  
d) `print(f"Score: {85}")`

**2. What error will occur when executing the following code?**
```python
name = "Alice"
age = 25
message = name + age
print(message)
```

a) SyntaxError  
b) TypeError  
c) ValueError  
d) NameError

**3. Which line will cause an error in the following code?**
```python
1  text = "Python"
2  print(text[0])
3  print(text[6])
4  print(text[-1])
```

a) Line 1  
b) Line 2  
c) Line 3  
d) Line 4

**4. What will happen when the following code is executed?**
```python
numbers = [10, 20, 30]
print(numbers[3])
```

a) It will print 30  
b) It will print None  
c) It will raise an IndexError  
d) It will print an empty value

**5. Which of the following will NOT cause an error?**

a) `result = 10 / 0`  
b) `result = 10 // 0`  
c) `result = 10 % 0`  
d) `result = 10 ** 0`

---

## Section 2: Flow Control (Q6-10)

**6. What error will occur when the following code is executed?**
```python
colors = ["red", "blue", "green"]
for i in range(5):
    print(colors[i])
```

a) No error will occur  
b) IndexError on the 4th iteration  
c) IndexError on the 5th iteration  
d) TypeError

**7. Which input would cause an error in the following code?**
```python
user_input = input("Enter a number: ")
number = int(user_input)
result = 100 / number
print(result)
```

a) "50"  
b) "0"  
c) "10"  
d) "25"

**8. Consider the following code. Which value of `data` will cause an error?**
```python
data = ####
total = 0
for item in data:
    total += item
print(total)
```

a) `data = [1, 2, 3, 4]`  
b) `data = [10, 20, 30]`  
c) `data = [5, "10", 15]`  
d) `data = []`

**9. What will happen when the following code is executed with the input "abc"?**
```python
value = input("Enter a number: ")
number = int(value)
if number > 10:
    print("Large")
else:
    print("Small")
```

a) It will print "Small"  
b) It will print "Large"  
c) It will raise a ValueError  
d) It will raise a TypeError

**10. Which of the following code snippets will cause an error?**

a) 
```python
count = 0
while count < 3:
    print(count)
    count += 1
```

b) 
```python
items = [1, 2, 3]
for item in items:
    print(item * 2)
```

c) 
```python
numbers = [5, 10, 15]
for i in range(len(numbers) + 1):
    print(numbers[i])
```

d) 
```python
x = 10
while x > 0:
    print(x)
    x -= 2
```

---

## Section 3: Functions (Q11-15)

**11. What error will occur when the following code is executed?**
```python
def greet(name):
    message = "Hello, " + name
    return message

def main():
    greet("Alice")
    print(message)

main()
```

a) SyntaxError  
b) NameError  
c) TypeError  
d) No error

**12. Which function call will cause an error?**
```python
def calculate(x: int, y: int) -> int:
    return x + y

def main():
    # Which of these will cause an error?
    pass
```

a) `result = calculate(5, 10)`  
b) `result = calculate(5)`  
c) `result = calculate(5, 10, 15)`  
d) Both b and c will cause errors

**13. What will happen when the following code is executed?**
```python
def process_data(values):
    return values[0] + values[-1]

def main():
    data = []
    result = process_data(data)
    print(result)

main()
```

a) It will print 0  
b) It will print None  
c) It will raise an IndexError  
d) It will raise a TypeError

**14. Which of the following function definitions will cause a SyntaxError?**

a) 
```python
def add_numbers(a, b):
    return a + b
```

b) 
```python
def multiply(x, y)
    return x * y
```

c) 
```python
def subtract(a: int, b: int) -> int:
    return a - b
```

d) 
```python
def divide(x, y):
    result = x / y
    return result
```

**15. What error will occur when the following code is executed?**
```python
def get_first_item(items: list):
    return items[0]

def main():
    my_list = None
    first = get_first_item(my_list)
    print(first)

main()
```

a) IndexError  
b) TypeError  
c) ValueError  
d) NameError

---

## Section 4: Testing/Debugging (Q16-20)

**16. A function is supposed to return the average of numbers in a list. Which test input would most likely reveal a division by zero error?**
```python
def calculate_average(numbers: list) -> float:
    total = sum(numbers)
    return total / len(numbers)
```

a) `[10, 20, 30]`  
b) `[]`  
c) `[0, 0, 0]`  
d) `[5]`

**17. Consider the following code that processes user scores:**
```python
scores = [85, 92, 78, 95]
index = int(input("Enter index (0-3): "))
print("Score:", scores[index])
```

Which user input would cause an IndexError?

a) 0  
b) 2  
c) 3  
d) 4

**18. A programmer writes the following code to find the maximum value in a list:**
```python
def find_max(numbers: list) -> int:
    max_value = numbers[0]
    for num in numbers:
        if num > max_value:
            max_value = num
    return max_value

result = find_max([])
print(result)
```

What error will occur?

a) ValueError  
b) IndexError  
c) TypeError  
d) No error, it will print None

**19. Which line will cause an error when this code is executed?**
```python
1  def calculate(a, b):
2      result = a / b
3      return result
4
5  def main():
6      x = 10
7      y = 0
8      answer = calculate(x, y)
9      print(answer)
10
11 main()
```

a) Line 2  
b) Line 7  
c) Line 8  
d) Line 9

**20. Consider the following code:**
```python
def process_string(text: str) -> str:
    return text.upper()

def main():
    data = ["hello", "world", 123]
    for item in data:
        print(process_string(item))

main()
```

What will happen when this code is executed?

a) It will print all items in uppercase  
b) It will raise a TypeError on the first iteration  
c) It will raise a TypeError on the third iteration  
d) It will raise an AttributeError on the third iteration


---

# Python Foundation Test - Functions Focus

## Section 3: Functions 

**11. Which of the following function definitions has a SYNTAX ERROR?**

a) 
```python
def calculate_total(price, quantity):
    total = price * quantity
    return total
```

b) 
```python
def calculate_total(price: float, quantity: int)
    total = price * quantity
    return total
```

c) 
```python
def calculate_total(price: float, quantity: int) -> float:
    total = price * quantity
    return total
```

d) 
```python
def calculate_total(price, quantity):
    return price * quantity
```

**12. Consider the following function. What will be printed when `main()` is called?**
```python
def add_numbers(a: int, b: int):
    result = a + b
    print(result)

def main():
    answer = add_numbers(5, 10)
    print(answer)

main()
```

a) 15  
b) 15  
   None

c) None  
d) 15  
   15

**13. Which of the following function calls will cause an error?**
```python
def greet(name: str, age: int) -> str:
    return f"Hello {name}, you are {age} years old."

# Which call will cause an error?
```

a) `greet("Alice", 25)`  
b) `greet(name="Bob", age=30)`  
c) `greet("Charlie")`  
d) `greet(age=20, name="David")`

**14. What will be the output of the following code?**
```python
def modify_value(x: int):
    x = x + 10
    return x

def main():
    num = 5
    modify_value(num)
    print(num)

main()
```

a) 5  
b) 10  
c) 15  
d) None

**15. Which of the following function definitions is CORRECT for a function that should take two parameters `width` and `height`, and return their product?**

a) 
```python
def calculate_area(width, height):
    area = width * height
    print(area)
```

b) 
```python
def calculate_area(width, height):
    return width * height
```

c) 
```python
def calculate_area(width, height) -> int:
    area = width * height
```

d) 
```python
def calculate_area():
    return width * height
```

**16. What will be the output of the following code?**
```python
def process(value: int) -> int:
    value = value * 2
    print(value)
    return value

def main():
    x = 10
    result = process(x)
    print(result)

main()
```

a) 20  
b) 20  
   20

c) 10  
   20

d) 20  
   10

**17. Which of the following function calls matches the function definition correctly?**
```python
def create_message(greeting: str, name: str, punctuation: str) -> str:
    return greeting + " " + name + punctuation
```

a) `create_message("Hello", "Alice")`  
b) `create_message("Hello", "Alice", "!")`  
c) `create_message(greeting="Hello")`  
d) `create_message("Hello", "Alice", "!", "Extra")`

**18. What will be the output of the following code?**
```python
def calculate(a: int, b: int):
    result = a + b
    return result
    print(result)

def main():
    answer = calculate(3, 7)
    print(answer)

main()
```

a) 10  
   10

b) 10  
c) None  
d) Error

**19. Consider the following code. What is the problem?**
```python
def get_discount(price: float, rate: float) -> float:
    discount = price * rate
    print(f"Discount: {discount}")

def main():
    original_price = 100
    discount_rate = 0.2
    saved = get_discount(original_price, discount_rate)
    final_price = original_price - saved
    print(f"Final price: {final_price}")

main()
```

a) The function has incorrect parameter names  
b) The function prints instead of returning the discount value  
c) The function has incorrect type hints  
d) The function call has wrong arguments

**20. What will be the output of the following code?**
```python
def multiply(x: int, y: int) -> int:
    print(x * y)

def main():
    result = multiply(4, 5)
    print(f"Result: {result}")

main()
```

a) 20  
   Result: 20

b) Result: 20  
c) 20  
   Result: None

d) Result: None

**21. Which of the following function definitions has the parameters in the WRONG order for this function call to work: `format_name(first="John", last="Smith")`?**

a) `def format_name(first: str, last: str) -> str:`  
b) `def format_name(last: str, first: str) -> str:`  
c) `def format_name(first, last):`  
d) All of them would work

**22. What will be the output of the following code?**
```python
def calculate_sum(numbers: list) -> int:
    total = 0
    for num in numbers:
        total += num
    return total
    return total * 2

def main():
    values = [1, 2, 3, 4]
    result = calculate_sum(values)
    print(result)

main()
```

a) 10  
b) 20  
c) 10  
   20

d) Error

**23. Which function definition correctly accepts a parameter called `student_name` and returns a greeting message?**

a) 
```python
def greet(name: str) -> str:
    return f"Welcome, {student_name}!"
```

b) 
```python
def greet(student_name: str) -> str:
    return f"Welcome, {student_name}!"
```

c) 
```python
def greet(student_name: str):
    print(f"Welcome, {student_name}!")
```

d) 
```python
def greet() -> str:
    return f"Welcome, {student_name}!"
```

**24. What will happen when the following code is executed?**
```python
def divide(a: int, b: int) -> float:
    result = a / b

def main():
    x = 10
    y = 2
    answer = divide(x, y)
    print(answer)

main()
```

a) It will print 5.0  
b) It will print None  
c) It will print 5  
d) It will cause an error

**25. Consider the following two functions. What is the key difference in their behavior?**
```python
def function_a(value: int) -> int:
    result = value * 2
    return result

def function_b(value: int):
    result = value * 2
    print(result)
```

a) function_a returns a value that can be used later; function_b only displays output  
b) function_a is faster than function_b  
c) function_b is more efficient than function_a  
d) There is no practical difference

**26. What will be the output of the following code?**
```python
def process_data(data: list):
    data.append(100)
    print(data)

def main():
    my_data = [10, 20, 30]
    process_data(my_data)
    print(my_data)

main()
```

a) [10, 20, 30, 100]  
   [10, 20, 30]

b) [10, 20, 30]  
   [10, 20, 30, 100]

c) [10, 20, 30, 100]  
   [10, 20, 30, 100]

d) [10, 20, 30]  
   [10, 20, 30]

**27. Which function call will cause a TypeError?**
```python
def calculate_area(length: int, width: int) -> int:
    return length * width
```

a) `calculate_area(5, 10)`  
b) `calculate_area(length=5, width=10)`  
c) `calculate_area(5, width=10)`  
d) `calculate_area(5, 10, 15)`

**28. What will be the output of the following code?**
```python
def get_message(name: str) -> str:
    message = f"Hello, {name}!"
    print(message)
    return message

def main():
    result = get_message("Alice")
    print(result)

main()
```

a) Hello, Alice!  
b) Hello, Alice!  
   Hello, Alice!

c) None  
d) Error

**29. Which of the following is the CORRECT way to define a function that takes no parameters and returns nothing?**

a) 
```python
def display_menu():
    print("1. Option A")
    print("2. Option B")
```

b) 
```python
def display_menu() -> None:
    print("1. Option A")
    print("2. Option B")
```

c) 
```python
def display_menu():
    print("1. Option A")
    print("2. Option B")
    return None
```

d) All of the above are correct

**30. What will be the output of the following code?**
```python
def calculate(x: int, y: int) -> int:
    return x + y
    x = x * 2
    return x + y

def main():
    result = calculate(5, 3)
    print(result)

main()
```

a) 8  
b) 13  
c) 16  
d) Error

---

# Python Foundation Test - Loops Focus

## Section 2: Flow Control - Loops (Q6-10 + Extended)

**6. What will be the output of the following code?**
```python
for i in range(3):
    print(i)
```

a) 0 1 2  
b) 1 2 3  
c) 0 1 2 3  
d) 1 2

**7. What will be the output of the following code?**
```python
count = 0
for i in range(5):
    count += 1
print(count)
```

a) 4  
b) 5  
c) 6  
d) 0

**8. Which of the following will cause an INFINITE LOOP?**

a) 
```python
x = 10
while x > 0:
    print(x)
    x -= 1
```

b) 
```python
x = 0
while x < 5:
    print(x)
    x += 1
```

c) 
```python
x = 10
while x > 0:
    print(x)
```

d) 
```python
for i in range(10):
    print(i)
```

**9. What will be the output of the following code?**
```python
numbers = [10, 20, 30]
for i in range(len(numbers)):
    print(numbers[i])
```

a) 0 1 2  
b) 10 20 30  
c) 1 2 3  
d) Error

**10. What will be the output of the following code?**
```python
total = 0
for i in range(1, 4):
    total += i
print(total)
```

a) 3  
b) 6  
c) 10  
d) 4

**11. Which of the following code snippets will print the numbers 2, 4, 6, 8, 10?**

a) 
```python
for i in range(2, 11, 2):
    print(i)
```

b) 
```python
for i in range(2, 10, 2):
    print(i)
```

c) 
```python
for i in range(1, 6):
    print(i * 2)
```

d) Both a and c

**12. What will be the output of the following code?**
```python
x = 5
while x > 0:
    print(x)
    x -= 2
```

a) 5 3 1  
b) 5 4 3 2 1  
c) 5 3 1 -1  
d) 4 2 0

**13. What is wrong with the following code?**
```python
colors = ["red", "blue", "green"]
for i in range(5):
    print(colors[i])
```

a) The range should be range(3)  
b) The loop will cause an IndexError  
c) The variable name should be 'color' not 'i'  
d) Both a and b are correct

**14. What will be the output of the following code?**
```python
for i in range(3):
    for j in range(2):
        print(i, j)
```

a) 0 0  
   0 1  
   1 0  
   1 1  
   2 0  
   2 1

b) 0 1 2  
   0 1

c) 0 0  
   1 1  
   2 2

d) 3 2

**15. What will be the output of the following code?**
```python
count = 0
while count < 3:
    print(count)
    count += 1
print("Done")
```

a) 0 1 2  
b) 0 1 2 Done  
c) 0  
   1  
   2  
   Done

d) 1 2 3 Done

**16. Which of the following will print "Hello" exactly 4 times?**

a) 
```python
for i in range(4):
    print("Hello")
```

b) 
```python
for i in range(1, 5):
    print("Hello")
```

c) 
```python
count = 0
while count < 4:
    print("Hello")
    count += 1
```

d) All of the above

**17. What will be the output of the following code?**
```python
numbers = [5, 10, 15, 20]
for num in numbers:
    if num > 12:
        print(num)
```

a) 5 10 15 20  
b) 15 20  
c) 10 15 20  
d) 20

**18. What is the problem with the following code?**
```python
x = 10
while x < 20:
    print(x)
```

a) The condition should be x <= 20  
b) The loop will never execute  
c) The loop will run infinitely  
d) The variable x should be initialized to 0

**19. What will be the output of the following code?**
```python
result = ""
for i in range(3):
    result += str(i)
print(result)
```

a) 0 1 2  
b) 012  
c) 123  
d) 3

**20. What will be the output of the following code?**
```python
count = 1
while count <= 3:
    print(count)
    count += 1
```

a) 0 1 2  
b) 1 2 3  
c) 1 2 3 4  
d) 2 3 4

**21. Which of the following loops will execute ZERO times?**

a) 
```python
for i in range(0):
    print(i)
```

b) 
```python
for i in range(1, 1):
    print(i)
```

c) 
```python
x = 5
while x < 5:
    print(x)
    x += 1
```

d) All of the above

**22. What will be the output of the following code?**
```python
numbers = [1, 2, 3, 4, 5]
for i in range(len(numbers)):
    numbers[i] = numbers[i] * 2
print(numbers)
```

a) [1, 2, 3, 4, 5]  
b) [2, 4, 6, 8, 10]  
c) [1, 4, 9, 16, 25]  
d) Error

**23. What will be the output of the following code?**
```python
for i in range(5, 2, -1):
    print(i)
```

a) 5 4 3  
b) 5 4 3 2  
c) 2 3 4 5  
d) 3 4 5

**24. What is wrong with the following code?**
```python
total = 0
for i in range(10)
    total += i
print(total)
```

a) Missing colon after range(10)  
b) The variable 'total' should not be initialized  
c) The range should start from 1  
d) Nothing is wrong

**25. What will be the output of the following code?**
```python
x = 0
while x < 5:
    x += 1
    if x == 3:
        continue
    print(x)
```

a) 1 2 3 4 5  
b) 1 2 4 5  
c) 0 1 2 4 5  
d) 1 2 3 4

**26. What will be the output of the following code?**
```python
for i in range(2, 8, 3):
    print(i)
```

a) 2 5  
b) 2 5 8  
c) 2 3 4 5 6 7  
d) 3 6

**27. Which of the following will cause an error?**

a) 
```python
for i in range(10):
    print(i)
```

b) 
```python
for i in range(1, 10):
    print(i)
```

c) 
```python
for i in range(10, 1):
    print(i)
```

d) None of them will cause an error

**28. What will be the output of the following code?**
```python
count = 0
for i in range(3):
    for j in range(2):
        count += 1
print(count)
```

a) 3  
b) 5  
c) 6  
d) 2

**29. What will be the output of the following code?**
```python
numbers = [10, 20, 30, 40]
for i in range(0, len(numbers), 2):
    print(numbers[i])
```

a) 10 20 30 40  
b) 10 30  
c) 20 40  
d) 0 2

**30. What will happen when the following code is executed?**
```python
x = 5
while x > 0:
    print(x)
    if x == 3:
        break
    x -= 1
```

a) It will print 5 4 3  
b) It will print 5 4 3 2 1  
c) It will print 5 4  
d) It will cause an infinite loop

**31. What will be the output of the following code?**
```python
text = "Python"
for char in text:
    print(char)
```

a) Python  
b) P y t h o n  
c) P  
   y  
   t  
   h  
   o  
   n

d) 0 1 2 3 4 5

**32. Which of the following correctly iterates through a list backwards?**
```python
numbers = [1, 2, 3, 4, 5]
```

a) 
```python
for i in range(len(numbers), 0, -1):
    print(numbers[i])
```

b) 
```python
for i in range(len(numbers) - 1, -1, -1):
    print(numbers[i])
```

c) 
```python
for i in range(5, 0, -1):
    print(numbers[i])
```

d) 
```python
for num in numbers:
    print(num)
```

**33. What will be the output of the following code?**
```python
sum_value = 0
for i in range(1, 6):
    if i % 2 == 0:
        sum_value += i
print(sum_value)
```

a) 6  
b) 12  
c) 15  
d) 9

**34. What is the problem with the following code?**
```python
items = ["apple", "banana", "cherry"]
i = 0
while i < len(items):
    print(items[i])
```

a) The loop will cause an IndexError  
b) The loop will run infinitely  
c) The variable 'i' is not incremented  
d) Both b and c are correct

**35. What will be the output of the following code?**
```python
for i in range(3):
    print(i, end=" ")
print()
```

a) 0 1 2  
b) 0  
   1  
   2

c) 012  
d) 1 2 3

---

