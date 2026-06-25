---
categories:
  - "[[Learning]]"
subjects:
  - "[[Technology]]"
type: lesson
description: "Python Daily Bite day 2: string variables, f-string formatting and string methods."
tags:
  - python
  - coding
created: 2026-06-18
---

# 🐍 Python Daily Bite – Day X

## 🎯 Learning Goals
- [x] Understand how to create and aggregate strings
- [ ] 
- [ ] <Goal 3>
### **Day 2 – Strings**

-  Create variables:
    
    `first = "Google" second = "Cloud" print(first + " " + second)`
    Format is always variable string name = "content"
    Print function is print()
-  Use **f-string** formatting.
    f-string formatting embeds variables and expressions into strings.
    `name = "Carl"`
    `age = "56"`
    `print(f"my name is {name} and I am {age} years old")`
-  Try `.upper()`, `.lower()`, `.strip()`.
    
-  Reflection: When would string formatting be useful in a pipeline?
## 💻 Code Practice
```python
print("Hello, Python & SQL project!")
first = "Google"
first = "Microsoft" # Overwrites first
second = "Apple"
third = "Amazon"
fourth = first # fourth is now "Microsoft"

print(first + " " + second) # prints "Microsoft Apple"
print(fourth + " " + third) # prints "Microsoft Amazon"

name = "Carl"
age = 56
a, b = 5, 3

print(f"{a} + {b} = {a + b}")
# Output: 5 + 3 = 8

firstname, lastname = "Carl", "Sagan"
print(f"Hello, {firstname} {lastname}!")
# Output: Hello, Carl Sagan!
print(f"My name is {name} and I am {age} years old.")
# Output: My name is Carl and I am 42 years old.
```

## ✅ Checklist
- [ ] Run script in REPL  
- [ ] Save `.py` file and run in terminal  
- [ ] Commit code to GitHub repo (optional)  

## 🪞 Reflection
- What went well?  
- What was tricky?  
- How could I apply this in a real data engineering task?  
