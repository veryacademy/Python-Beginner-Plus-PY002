# 005 Insertion Sort

Welcome to Python challenges. Practice your Python Skills daily with Python challenges. 

## ***Code Challenge:***
Given a list of numbers sort the numbers from lowest to highest.

----
#### **Prerequisites:**
- Level: Beginner
- Python 3.5+

----
### Tags/Keywords
range, sorting, selection sort

----

### Code Examples

```
# ex1.0.1 Measuring algorithm performance
import timeit
from random import randint


def run_sorting(algorithm, nts):
    setup_code = f"from __main__ import {algorithm}"

    stmt = f"{algorithm}({nts})"

    # repeat specifies the number of samples to take
    # number specifies the number of times to repeat the code for each sample.
    time = timeit.repeat(stmt=stmt, setup=setup_code, repeat=1, number=1)

    print(f"Quickest execution time: {min(time)}")

def selection_sort(nts):

    n = len(nts)

    for i in range(n):
        idx = i
        for p in range(i + 1, n):
            if nts[p] < nts[idx]:
                idx = p

        nts[i], nts[idx] = nts[idx], nts[i]

def insertion_sort(nts):

    for i in range(1, len(nts)):
        current_num = nts[i]

        p = i - 1

        while p >= 0 and nts[p] > current_num:
            nts[p + 1] = nts[p]
            p -= 1

        nts[p + 1] = current_num

def bubbleSort(nts):

    nts_len = len(nts)

    for i in range(len(nts)):
        for p in range(nts_len - i - 1):
            if nts[p] > nts[p + 1]:
                nts[p], nts[p + 1] = nts[p + 1], nts[p]


if __name__ == "__main__":

    nts = [randint(0, 10000) for i in range(55000)]
    run_sorting(algorithm="selection_sort", nts=nts)

```
---
### **Further reading**
https://realpython.com/sorting-algorithms-python/
https://www.pyscoop.com/sorting-algorithms-implementation-in-python/
https://stackoverflow.com/questions/176011/python-list-vs-array-when-to-use
http://web.engr.oregonstate.edu/~sinisa/courses/OSU/CS261/CS261_Textbook/Chapter04.pdf
http://z-sword.blogspot.com/2014/02/advantages-and-disadvantages-of-sorting.html
https://core.ac.uk/download/pdf/42956228.pdf