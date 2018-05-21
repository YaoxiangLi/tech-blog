---
title: Almost palindrome
categories: Algorithm
abbrlink: 62152
date: 2018-03-02 17:31:26
tags:
    - Algorithm
---
The palindromic score of a string is the number of errors(characters which do not match) when the string is read forwards and backwards. For example, the palindromic score of 'fox' is 2, because 'fox' and 'xof' differ by two characters. Write a function to take a string and return its palindromic score.

```python
def almost_palindromes(str):
    cnt = 0
    for x, y in str[::-1], str:
        if x != y:
            cnt += 1
    
    return cnt

test1 = "abba"
test2 = "abcdcaa"
test3 = "aaabbb"
print(almost_palindromes(test1)) # Expected result 0
print(almost_palindromes(test2)) # Expected result 2
print(almost_palindromes(test3)) # Expected result 6

```