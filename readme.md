# Python Binary Search

#### my solution made from scratch before reading math rules used below some times it reduces loop to 70 times some times it reduce to 270270.2702702703 times, (i say sometimes becuase there are 1 signle random part which is dividing list number I selected 50 random, math could imporve this and return the number always makes it 27027.027027027027 times 
```python
    import numpy as np
    """(Copyright inspred from reading point in ternary search divide big list to small lists added min and max to target which small list have target) Improve can done with: eg target / something * something + len(items) = divide number to something, eg when target was 700000 it and divided to 50 it done in only 37 loops 50 was random number"""
    # also bigest note as this is core of algo, I can do it in any language only as python fancy it has binary_search but others will not has go, java,c++, js
    #this is core of algo but samilir to it not same copyright 
    items = list(range(10000000))
    algoDivding = np.array_split(items, 50)
    print(algoDivding)
    # algo dividing
    target = 541367
    loops_done = 0
    
    need_break = False
    for arr in algoDivding:
        loops_done += 1
        minNumOfThisArr = min(arr)
        maxNumOfThisArr = max(arr)
        if target >= minNumOfThisArr and target <= maxNumOfThisArr:
            # instead of loop on all values loop on fewer length list 1
            for num in arr:
                loops_done += 1
                if num == target:
                    print(loops_done,"instead of {}".format(len(items)), "found target by looping on small length list otherwise should loop on all numbers but np slowed things", min(arr), max(arr))
                    break
        if need_break:
            break
```

#### same example reduce it to 27027.027027027027 times 
```python
items = list(range(1000000))
algoDivding = np.array_split(items, 50)
print(algoDivding)
# algo dividing
target = 700000
loops_done = 0
for arr in algoDivding:
    loops_done += 1
    minNumOfThisArr = min(arr)
    maxNumOfThisArr = max(arr)
    if target >= minNumOfThisArr and target <= maxNumOfThisArr:
        # instead of loop on all values loop on fewer length list 1
        for num in arr:
            loops_done += 1
            if num == target:
                print(loops_done,"instead of {}".format(len(items)), "found target by looping on small length list otherwise should loop on all numbers but np slowed things", min(arr), max(arr))
        

```
Hey :wave: <br>
~ let's talk about binary search today! <br>

So, what is **Binary Search**? <br><br>
<em>"Binary Search is a search algorithm that finds the position of a target value within a **sorted** array."</em> <br>
~ [Wikipedia](https://en.wikipedia.org/wiki/Binary_search_algorithm)

> It works in **every** programming language, but i'm gonna show how it works with Python.

## Examples

Let's take a look here:

```python
def loop_search(arr, target):
    for pos in arr: # loop through the array
        if arr[pos] == target: # if we find our target
            return arr.index(target) # return its index

    return False # else, return false

loop_search( [1, 2, 3, 4, 5], 4 ) # 3
```

Okay, it's a basic thing we all know how to do. But what if we want to do it with a LARGE amount of elements? _For example:_

```python
import random
import math

# create an array with numbers between 1 and 500, with 10.000 numbers in it
someArray = [math.floor(random.randint(1, 500)) for _ in range(10000)]

loop_search( someArray, 4 ) # input will be random in this case
```
> Obs: This `[for _ in range(10000)]` is called [List Comprehension](https://www.programiz.com/python-programming/list-comprehension), if you want to learn more!

You see? It's going to loop through **every** element until it finds the target we want.
What if our target is in `len(someArray)` position? It will loop through it **10.000** times!! You don't wanna do that.

## So, what can we do?

That's simple! We do the same thing we did but with **Binary Search**.

### Binary Search Example

Ok, let's pretend we have a **Phone Book**, those large ones. We want to call **Michael**, just because we want to hang out with him.<br>
~ How can we do this thing? Let's do this **algorithmically**:
 
 * We take the **Phone Book**
 * Search for the `M` letter
 * Find **Michael** on page `236`
 * Call him
 
 That's simple, right? But what if we do the same thing the way we did with the code? <br>
 ~ It's gonna be like this:
 
 * Take **Phone Book**
 * `Check page`
    * Is **Michael** there?
        * Yes!
            * Call him
        * No.
            * Back to `Check page` + 1
            
We're going to do this until we reach page `236`, it's a lot of work.

### Decrease work

So, to do less, we need to do exactly what we did in the first example, but in code. <br>

**The best way to do this is writing it in human language first, with as many details as you can.**
For example:

* Take **Phone Book**
* Go to the **center** of the phone book
* Page word is **M**?
    * No
        * Page word comes first than `M` on alphabet?
            * Yes
                * So we can discard all the pages to the **left**!
            * No
                * So we can discard all the pages to the **right**!
    * Yes!
        * Let's search for `Michael` here!

That's basically what we're going to do! `but with numbers!`

```python
# we have to import math, because "mid" must be an integer
import math

# pretend we wanna find 30's index in some array

def binary_search(arr, target):
    arr.sort() # we MUST sort it

    # define left-side as the first "book's page"
    left = 0
    # define right-side as the array's length (last book's page)
    right = len(arr) - 1

    # so, while we don't find our target
    while left <= right:
        # we define mid, so we can discard left or right
        mid = math.floor((left + right) / 2)

        # arr[mid] = 18, target = 30
        if target > arr[mid]:
            # we can discard all the left pages
            left = mid + 1
        # arr[mid] = 36, target = 30
        elif target < arr[mid]:
            # we can discard all the left pages
            right = mid - 1
        # we find it!
        else:
            # return it's index
            return arr.index(target)
```

**That's it! Let's test this code:**

```python
binary_search( [1, 2, 3, 4, 5], 3 ) # 2
binary_search( [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 7 ) # 6
binary_search( [3, 2, 5, 9, 1, 6, 10], 10 ) # 6, because it's sorted: [1, 2, 3, 5, 6, 9, `10`]

# It also works FAST with an array with 50.000 items for example. If you want to find some item index there!
```

> Hey, **item's index** isn't the only thing you can return from this function. Be creative!

## That's it

Hope you learned something about **Binary Search**! <br>
> _Obs:_ Binary Search isn't the only kind of search we have in programming languages, you can see some of'em [here](https://realpython.com/binary-search-python/#understanding-search-algorithms).

If you want to know more about this, or if you didn't understand something here, you can check some websites for more information:

* [Real Python (Binary Search)](https://realpython.com/binary-search-python/#binary-search)
* [Geek for Geeks (Binary Search)](https://www.geeksforgeeks.org/binary-search/)
* [CS50](https://cs50.harvard.edu/x/2020/) `CS50 is a Harvard's course, that talks about it and much more. I strongly recommend.`

**Thank you!** :purple_heart: 
