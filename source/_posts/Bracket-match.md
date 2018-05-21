---
title: Bracket match
categories: Algorithm
abbrlink: 1469
date: 2018-03-01 12:20:59
tags:
    - Stack
    - Algorithm
---
A string of brackets is correctly matched if you can pair every opening bracket up with a later closing bracket, and vice versa. For example, "(()())" is correctly matched, and "(()" and ")(" are not. Implement a function which takes a string of brackets and returns the minimum number of brackets you'd have to add to the string to make it correctly matched. For example, "(()" could be correctly matched by adding a single closing bracket at the end, so you'd return 1. ")(" can be correctly matched by adding an opening bracket at the start and a closing bracket at the end, so you'd return 2. If your string is already correctly matched, you can just return 0.

```python
def bracket_match(bracket_string):
    cnt = 0
    stack = []
    for char in bracket_string0:
        if char == '(':
            stack.append(char)
        elif char == ')':
            if stack == []:
                cnt += 1
            elif stack[-1] == '(':
                stack.pop()
    
    cnt += len(stack)

    return cnt


# Test Input
if __name__ == "__main__":
    test1 = "(()())" # Expected Result 0
    test2 = "((())" # Expected Result 1
    test3 = "())" # Expected Result 1
    print(bracket_match(test1))
    print(bracket_match(test2))
    print(bracket_match(test3))

```
