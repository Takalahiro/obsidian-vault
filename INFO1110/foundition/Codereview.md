### **Q1: `txt`**
It's a **persistent storage file**. It saves ASCII art pictures. We use **append mode** to write, and **sort alphabetically** when reading
### Q2: `re` and `os`
`re` for **Regular expressions**, `os` for **File operations**
### Q3: `return bool(re.fullmatch(r"\d{9}|[A-Za-z]{4}\d{4}", user_input_id))`
It checks if the input matches our ID pattern - 9 numbers (like `123456789`) or 4 letters + 4 numbers (like `ABCD1234`) and return `True` or `False`.
`fullmatch`ensures the entire string matches the pattern, not just part of it.
`r`: raw string
`|`: or
`, user_input_id` is variable
### Q4: ``request_image``
Continuously requests image codes from the user, skips invalid formats, searches the `get image`database for matches, and returns the first found image or None when the user types "exit".
### Q5: `process image`
Opens gallery.txt in append mode and writes the title and image from img_data dictionary.
### Q6：`view gallery`
Scans the file line by line, storing each "Title: " and its following content as a dictionary entry, then prints everything sorted by the first letter of the title.
### Q7：Can we change loop?
No , we do not know how many times we need get in code , we can use `__iter__` or `itertools` to change while loop.
### Q8: `rf"[A-Za-z]{{{mid}}}\d{{{n - mid}}}"`
`r` : raw string
`f`: f string
`{{{mid}}}`means output is {mid}