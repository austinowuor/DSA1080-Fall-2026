# DSA 1080A — Programming for Data Science

## Overview

This Jupyter notebook introduces Python programming and gradually progresses from basic syntax to working with tabular data using pandas. It is intended for beginner data science students who want to understand Python through small, executable examples.

The notebook contains 57 code cells covering Python fundamentals, strings, arithmetic, collections, conditional statements, loops, text-file handling and introductory data analysis.

## Learning objectives

By completing the notebook, you should be able to:

- Display output, declare variables, accept keyboard input and convert data types.
- Manipulate strings and perform arithmetic calculations.
- Create and manipulate lists, tuples and sets.
- Use conditional statements to make decisions.
- Automate repetitive tasks using loops.
- Read and append content to text files.
- Load, inspect, select and filter data using pandas.
- Identify missing values in a dataset.

## 1. Getting started

### Requirements

- Python 3
- Visual Studio Code with the Python and Jupyter extensions, or Jupyter Notebook
- The pandas library
- The text file `file.txt` and dataset `DSA1080_Pandas_Student_Data.csv` for the final sections

Install the required packages in your terminal:

```bash
python -m pip install pandas notebook ipykernel
```

On Windows, use `py -m pip install pandas notebook ipykernel` if the `python` command is unavailable.

### Expected folder structure

```text
DSA1080A/
├── README.md
├── DSA 1080a.ipynb
├── file.txt
└── DSA1080_Pandas_Student_Data.csv
```

The two supporting data files are referenced by the notebook but were not included in the supplied upload. Obtain the original files from your instructor, or use the small practice files described below.

### Running the notebook

1. Open the project folder in VS Code.
2. Open `DSA 1080a.ipynb`.
3. Select a Python kernel with pandas installed.
4. Run each cell using the Run Cell button or `Shift + Enter`.
5. When prompted for input, enter a number and press Enter.
6. Read the output and modify the examples to test your understanding.

Run the notebook from top to bottom because the pandas examples reuse the `df` variable created when loading the CSV.

## 2. Notebook roadmap

Cell numbers below are counted from 1, in notebook order.

| Cells | Topic | Main concepts |
|---|---|---|
| 1–2 | Python basics | `print()`, `input()`, `float()`, formatted output |
| 3–7 | Strings | `upper()`, `lower()`, `replace()`, concatenation, `format()` |
| 8–9 | Arithmetic | Addition, subtraction, multiplication, division, exponentiation; modulus correction below |
| 10–18 | Lists | Creation, slicing, negative slicing, `append()`, `insert()`, `remove()`, `pop()` |
| 19–23 | Tuples | Creation, length, single-item tuples, conversion, concatenation |
| 24–29 | Sets | Unique elements, iteration, `add()`, `update()`, `pop()` |
| 30–38 | Decisions | `if`, `elif`, `else`, shorthand conditions, `and`, `or`, nested conditions |
| 39–47 | Loops | `while`, `for`, `break`, `continue`, `range()`, nested loops |
| 48–51 | File handling | `open()`, `read()`, `write()`, `readline()`, `close()` |
| 52–57 | pandas | CSV loading, inspection, selection, filtering, missing values |

## 3. Python fundamentals

### Output, input and variables

`print()` displays information. `input()` collects keyboard input as a string, even when the user enters digits. Use `float()` to convert numeric input before performing arithmetic.

```python
first = input("Enter first number: ")
second = input("Enter second number: ")
total = float(first) + float(second)
print("The sum is {}".format(total))
```

For inputs `10` and `5`, the result is `15.0`. Invalid numeric input raises a `ValueError`.

### Strings

A string is a sequence of characters used to represent text.

| Operation | Example | Result |
|---|---|---|
| Uppercase | `"Hello".upper()` | `HELLO` |
| Lowercase | `"HELLO".lower()` | `hello` |
| Replace | `"Hello World".replace("World", "Everyone")` | `Hello Everyone` |
| Concatenate | `"Hello" + " " + "World"` | `Hello World` |
| Format | `"Age: {}".format(36)` | `Age: 36` |

Strings are immutable: these methods produce new strings rather than changing the original string.

### Arithmetic operators

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `+` | Addition | `10 + 5` | `15` |
| `-` | Subtraction | `10 - 5` | `5` |
| `*` | Multiplication | `10 * 5` | `50` |
| `/` | Division | `10 / 5` | `2.0` |
| `%` | Remainder (modulus) | `9 % 5` | `4` |
| `**` | Exponentiation | `2 ** 3` | `8` |

**Important correction:** The notebook's modulus example uses `a / b`, which calculates division (`1.8`), not the remainder. Replace it with `a % b` to demonstrate modulus correctly.

## 4. Python collections

Think of collections as different ways of organizing a group of items.

| Feature | List | Tuple | Set |
|---|---|---|---|
| Syntax | `[1, 2, 3]` | `(1, 2, 3)` | `{1, 2, 3}` |
| Ordered | Yes | Yes | No guaranteed order |
| Mutable | Yes | No | Yes |
| Allows duplicates | Yes | Yes | No |
| Supports indexing | Yes | Yes | No |
| Example use | Student scores | Fixed coordinates | Unique course codes |

### Lists and slicing

Lists are useful when values need to be added, removed or updated.

```python
a = [1, 2, 3, 4, 5]
print(a[1:4])  # [2, 3, 4]
```

Python indexing begins at zero. Slicing follows `collection[start:stop:step]`, where the stop position is excluded.

```python
b = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(b[1:10:2])   # [2, 4, 6, 8, 10]
print(b[-6:-2])    # [5, 6, 7, 8]
print(b[-1:-6:-2]) # [10, 8, 6]
```

| Method | Purpose |
|---|---|
| `append(value)` | Add an item at the end |
| `insert(index, value)` | Add an item at a specified position |
| `remove(value)` | Remove the first matching value |
| `pop(index)` | Remove and return an item at a position |

`append()` modifies the list in place and returns `None`. In the notebook, `b = a.append("grapes")` therefore assigns `None` to `b`; the updated list remains in `a`.

### Tuples

Tuples are ordered but cannot be modified directly. A single-item tuple requires a trailing comma: `("python",)`.

The notebook demonstrates a workaround for changing a tuple: convert it into a list, modify the list, and convert it back into a new tuple.

### Sets

Sets store unique elements and are useful for eliminating duplicates.

```python
languages = {"python", "java", "python"}
print(languages)  # Two unique elements; order may vary
```

Use `add()` to add one element and `update()` to add elements from another collection. Unlike list `pop()`, set `pop()` removes an arbitrary element, not a predictable last item.

## 5. Conditional statements

Conditions allow a program to make decisions, such as checking whether a student has passed.

```python
score = 72

if score >= 70:
    print("High score")
elif score >= 50:
    print("Pass")
else:
    print("Below pass mark")
```

This is an additional practice example using the decision structures demonstrated in the notebook.

- `if` checks the first condition.
- `elif` checks another condition if the earlier conditions were false.
- `else` runs when none of the earlier conditions are true.
- `and` requires both conditions to be true; `or` requires at least one.
- Nested conditions place one decision inside another.

Indentation determines which statements belong to a condition or loop. Use consistent indentation (four spaces is recommended).

## 6. Loops

A loop repeats instructions instead of requiring the programmer to write the same code multiple times.

```python
i = 1
while i < 10:
    print(i)
    i += 1
```

The example prints 1 through 9. A `while` loop continues as long as its condition is true. A `for` loop iterates through items in a collection or another iterable.

| Construct | Purpose |
|---|---|
| `for x in fruits` | Visit each fruit |
| `for x in "banana"` | Visit each character |
| `range(6)` | Generate integers 0 through 5 |
| `break` | Exit the current loop |
| `continue` | Skip to the next iteration |
| Nested loops | Repeat an inner loop for each outer-loop item |

The notebook contains two `break` examples: printing before the `break` condition includes `banana` in the output, while checking the condition first excludes it.

## 7. Text-file handling

Create `file.txt` in the notebook folder if you do not have the original file. For practice, add two lines of text:

```text
Welcome to DSA 1080A.
Python is useful for data science.
```

The notebook reads the entire file, appends text, reads the first five characters and reads one line.

| Code | Behaviour |
|---|---|
| `open("file.txt", "r")` | Open for reading |
| `open("file.txt", "a")` | Open for appending |
| `read()` | Read remaining file content |
| `read(5)` | Read up to five characters |
| `readline()` | Read the next line |
| `close()` | Close the file |

Running the append cell repeatedly adds the same content repeatedly. The existing example does not add a newline automatically.

A recommended alternative to manually closing files is a context manager:

```python
with open("file.txt", "r", encoding="utf-8") as file:
    print(file.read())
```

The file is closed automatically when the block ends.

## 8. Introduction to pandas

pandas is a Python library for working with structured data. A DataFrame resembles a spreadsheet with rows and columns; a Series represents a one-dimensional collection, such as a single column.

### Loading and inspecting data

```python
import pandas as pd
df = pd.read_csv("DSA1080_Pandas_Student_Data.csv")
```

| Command | Purpose |
|---|---|
| `df.head()` | Preview the first five rows |
| `df.shape` | Return the number of rows and columns |
| `df.info()` | Display column types and non-null counts |
| `df.describe()` | Summarize numeric columns by default |
| `df.isna().sum()` | Count missing values in each column |

Use `df.info()` directly: wrapping it in `print()` also displays `None` because the method itself prints its summary.

### Selecting rows and columns

```python
df["Name"]                 # One column (Series)
df[["Name", "Score"]]       # Two columns (DataFrame)
df["Score"].mean()         # Average of non-missing scores
df.loc[0:4, ["Name", "Score"]]
df.iloc[0:5]
```

`loc` selects by labels, and label slices generally include the end label. `iloc` selects by integer position and excludes the stop position. With a default integer index, both row selections above cover the first five rows.

### Filtering and missing values

```python
high = df[df["Score"] >= 70]
city = df[df["City"] == "Nairobi"]
missing = df[df["Score"].isna()]
```

Filtering is similar to applying a filter in Excel: only records satisfying the condition are retained. Missing values are identified here, but the notebook does not yet demonstrate imputing or removing them.

### Optional practice dataset

If the original CSV is unavailable, save the following **illustrative, synthetic** data as `DSA1080_Pandas_Student_Data.csv`. It contains the three column names required by the notebook examples; it is not the original class dataset.

```csv
Name,Score,City
Amina,85,Nairobi
Brian,62,Mombasa
Carol,,Nairobi
David,74,Kisumu
Esther,90,Nairobi
Faith,55,Nakuru
```

With this sample, `df.shape` returns `(6, 3)`, three students score at least 70, and one score is missing.

## 9. Practice exercises

Try these after running the relevant examples:

1. Write a program that accepts two numbers and prints their product and remainder.
2. Convert a sentence to uppercase and replace one word.
3. Create a list of ten scores and extract every second score using slicing.
4. Add and remove elements from a list, then print the updated list.
5. Convert a list containing repeated city names into a set.
6. Write a conditional statement that classifies a score as pass or fail.
7. Use a loop to display numbers 1–20, skipping multiples of 3.
8. Append a new line to `file.txt`, then read the file.
9. Load the student CSV, display its dimensions and calculate the average score.
10. Filter students from Nairobi who scored at least 70, and count missing scores.

These exercises are supplementary learning activities, not existing notebook cells.

## 10. Troubleshooting

| Problem | Possible solution |
|---|---|
| `ModuleNotFoundError: No module named 'pandas'` | Install pandas in the environment selected as the notebook kernel. |
| `FileNotFoundError` | Ensure the required TXT and CSV files are in the working directory. |
| `NameError: name 'df' is not defined` | Run the CSV-loading cell first. |
| `KeyError: 'Score'` | Check exact CSV column names, capitalization and whitespace. |
| `ValueError` during numeric input | Enter a valid numeric value. |
| `IndentationError` | Check indentation in conditions and loops. |
| Set output changes order | This is normal; sets do not guarantee iteration order. |

To check the working directory:

```python
from pathlib import Path
print(Path.cwd())
```

## 11. Key takeaway

Python fundamentals are the building blocks of data science. Strings help process text, collections organize values, conditions support decisions, loops automate repetitive operations, file handling enables access to stored information, and pandas makes it possible to explore structured datasets.

The notebook is an introductory foundation for later topics such as data cleaning, visualization and exploratory data analysis. Those advanced topics are not implemented in this notebook.

---

**Course:** DSA 1080A — Programming for Data Science  
**Level:** Beginner  
**Environment:** Python / Jupyter Notebook  
**Purpose:** Classroom demonstration, guided practice and independent revision
