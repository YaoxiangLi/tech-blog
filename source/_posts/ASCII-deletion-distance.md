---
title: ASCII deletion distance
categories: Algorithm
abbrlink: 53234
date: 2018-03-02 17:13:23
tags:
    - Dynamic Programming
    - LCS
---
The deletion distance between two strings is the minimum sum of ASCII values of characters that you need to delete in the two strings in order to have the same string. The deletion distance between "cat" and "at" is 99, because you can just delete the first character of cat and the ASCII value of 'c' is 99. The deletion distance between "cat" and "bat" is 98 + 99, because you need to delete the first character of both words. Of course, the deletion distance between two strings can't be greater than the sum of their total ASCII values, because you can always just delete both of the strings entirely. Implement an efficient function to find the deletion distance between two strings. You can refer to the Wikipedia article on the algorithm for edit distance if you want to. The algorithm there is not quite the same as the algorithm required here, but it's similar.

```python
def ascii_deletion_distance(str1, str2):
    pass



test1 = ("at", "cat")
test2 = ("boat", "got")
test3 = ("thought", "sloughs")

print (ascii_deletion_distance(test1)) # Expected result 99
print (ascii_deletion_distance(test2)) # Expected result 298
print (ascii_deletion_distance(test3)) # Expected result 674
```
