---
toc: True
comments: False
layout: post
title: Python Quiz
description: This is my Python quiz. Test your knowledge on Python basics with my quiz.
type: tangibles
courses: {'csp': {'week': 2, 'categories': ['4.A']}}
---

```python
import getpass, sys

# formats question with prompt
def question_with_response(prompt):
    print("Question: " + prompt)
    msg = input()
    return msg

# formats question with prompt and formats answer with user's input
def question_and_answer(prompt):
    print("Question: " + prompt)
    msg = input()
    print("Answer: " + msg)

# checks if user's response and actual answer is correct
def check_answer (rsp, answer):
    if rsp == answer:
        print(rsp + " is correct!")
        return 1
    else:
        print(rsp + " is incorrect!")
        return 0

questions = 5
correct = 0

print('Hello, ' + getpass.getuser() + " running " + sys.executable)
print("You will be asked " + str(questions) + " questions.")
question_and_answer("Are you ready to take a test?")

rsp = question_with_response("The ______ method is used to get user input in Python") 
# checks if answer is correct and if correct, correct count increases
correct = correct + check_answer(rsp, "input()")

rsp = question_with_response("The elif keyword is short for ________.")
correct = correct + check_answer(rsp, "else if")

rsp = question_with_response("The return statement is used to specify the ________ of a function.")
correct = correct + check_answer(rsp, "output")

rsp = question_with_response("A collection of elements that is ordered and changeable is called a ________.")
correct = correct+ check_answer(rsp, "list")

rsp = question_with_response("The == operator is used to check if two values are ________.")
correct = correct + check_answer(rsp, "equal")

# outputs the user's score
print(getpass.getuser() + " you scored " + str(correct) +"/" + str(questions))
```

    Hello, nitinb running /opt/homebrew/opt/python@3.11/bin/python3.11
    You will be asked 5 questions.
    Question: Are you ready to take a test?
    Answer: yes
    Question: The ______ method is used to get user input in Python
    input() is correct!
    Question: The elif keyword is short for ________.
    else if is correct!
    Question: The return statement is used to specify the ________ of a function.
    output is correct!
    Question: A collection of elements that is ordered and changeable is called a ________.
    list is correct!
    Question: The == operator is used to check if two values are ________.
    equal is correct!
    nitinb you scored 5/5


