---
toc: false
comments: false
layout: post
title: Week 3 Review Ticket
description: This is my week 3 review ticket
courses: {csp: {week: 3}}
type: tangibles
---

<h2>HTML Structure</h2>
- &lt;div&gt; element: This element defines a division or section in an HTML document. It is often used to group and structure content. In the context of a grade calculator, &lt;div&gt; elements can be used to organize headings, total displays, and input fields.
<br>

```html
<div>
    <h1>Welcome to Our Website</h1>
    <p>This is the main content of our website.</p>
</div>
```

- &lt;span&gt; element: The &lt;span&gt; element defines an inline container within text. It is often used to style or target specific portions of text. In a grade calculator, &lt;span&gt; elements can be used to display different types of totals or labels.
<br>

```html
<title>Span Example</title>
<style>
    .highlight {
        color: red;
        font-weight: bold;
    }

    .italicize {
        font-style: italic;
    }
</style>
<body>
    <p>
        This is a <span class="highlight">highlighted</span> word in a sentence.
    </p>
    <p>
        You can <span class="italicize">italicize</span> text using the <span class="highlight">span</span> element.
    </p>
</body>
```
- "&lt;input&gt;" tag: The &lt;input&gt; tag specifies an input field where the user can enter data. It is commonly used to capture user input, such as scores or values. To distinguish and manipulate these input fields individually, they are often assigned unique id attributes.
<br>

```html
<body>
    <label for="name">Enter your name:</label>
    <input type="text" id="name" placeholder="Your name here">
    
    <br>
    
    <label for="email">Enter your email:</label>
    <input type="email" id="email" placeholder="Your email address">
    
    <br>
    
    <label for="password">Enter a password:</label>
    <input type="password" id="password" placeholder="Your password">
</body>
```

- "&lt;script&gt;" tag: The "&lt;script&gt;" tage is used to embed JavaScript code inside of HTML code.
<br>

```html 
<body>
    <h1>Hello, World!</h1>
    <script>
        // JavaScript code embedded within the <script> tag
        // You can also interact with HTML elements using JavaScript
        var heading = document.querySelector("h1");
        heading.style.color = "blue";
    </script>
</body>
```

<h2>Python Structure</h2>
- Variables & Data Structures: Variables are used to store data. Python supports various data types, including integers, floating-point numbers, strings, lists, tuples, dictionaries, sets, and more.
<br>
- Comments: Comments in Python are marked using the # symbol. They are used to provide explanations and make code more understandable.
<br>

```python
# This is a comment
```
- Conditional Statements: Python supports if, elif, and else statements for making decisions in code based on conditions.
<br>

```python
if condition:
    # Code to execute if condition is True
elif another_condition:
    # Code to execute if another_condition is True
else:
    # Code to execute if no conditions are True
```
- Loops: Python provides for and while loops for iterating over sequences, such as lists and strings.
<br>

```python
for item in iterable:
    # Code to repeat for each item in the iterable
i = 0
while(i <= 10):
    print(i)
    i = i + 1
```
- Functions: Functions allow you to encapsulate and reuse blocks of code. You define functions using the def keyword.
<br>

```python
def addition(n1, n2):
    return n1 + n2

print(addition(5,3))
```

- Modules and Packages: Python's standard library includes modules and packages that provide pre-written code for common tasks. You can also create your own modules and packages for code organization and reuse.
<br>

```python
import math  # Importing the math module
```
