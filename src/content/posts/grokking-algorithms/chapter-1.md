---
title: Chapter 1
published: 2026-04-08
description: Chapter 1 of Grokking Algorithms.
tags: [Book Review, Blogging]
category: Grokking Algorithms
draft: false
---

# Grokking Algorithms
## 1 - Binary Search

Its input is a sorted list of elements, and when looking for a specific
element, the search returns the position it's located or `null` if it
doesn't exist.

The basic concept is cutting the possibilities in half for every guess.

For example, when picking a predefined number between 1 and 100 on a
sorted list, the first guess should be 50.

When using normal search, on a list of `n` elements the worst case
scenario is `n` guesses. With binary search, the worst case is
$\log_2 n$ .

For a list of 1024 elements, the worst case scenario for normal search
is 1024, while for binary search is $\log_2 1024$ , which is 10.

**Binary search only works when said list is sorted.**

```python title="binary_search.py"
def binary_search(arr, item):
    low = 0
    high = len(arr) - 1   # last position... in this case 4
    while low <= high:
        mid = (low + high) // 2    # in this case is 2
        guess = arr[mid]           # first guess is 5, position number 3
        if(guess == item):
            return mid
        elif (guess > item):       # first guess is 5. it's bigger than 3, therefore new guesses should be below current mid.
            high = mid - 1          # the new high becomes 1
        else:
            low = mid + 1
    return None

my_list = [1,3,5,7,9]
print(binary_search(my_list,3))   # => 1
print(binary_search(my_list, -1)) # => None
```

```js title="binary_search.js"
function binary_search(array, item) {
    let low = 0;
    let high = array.length - 1;
    while (low <= high) {
        let mid = Math.floor((low + high) / 2);
        let guess = array[mid];
        if (guess == item) return mid;
        else if (guess > item) high = mid - 1;
        else low = mid + 1;
    }
    return null;
}
const my_array = [1, 3, 5, 7, 9];
console.log(binary_search(my_array, 3)); // returns 1
console.log(binary_search(my_array, -1)); //returns null
```

### Exercises
**1.1**  On a list of 128 names, when searching using binary search, what is the maximum
number of guesses it would take to find the answer?
**r:** $\log_2 128$, which is 7.

**1.2**  Doubling the size of the list, what is the maximum number of guesses then?
**r:** $\log_2 256$, which is 8.


On regular search, the maximum number of guesses is always the same as
the number of items. That is called **linear time**. Binary search uses
**logarithmic time** (or log time).

With 4 billion items, binary search would take only 32 guesses maximum!]

## Big O notation

Big O notation tells you how fast an algorithm is. Supposing we have a
list of `n` elements, with simple search, the algorithm would take
`O(n)` run time. It doesn't tell us how many seconds it would take, but
it lets us compare the number of operations.

Comparing to binary search, the algorithm would take
$$O(log_2n)$$

Big O always gives us the **worst case scenario**, so you know an
algorithm will never be slower than its notation. It is different from
the average case.

### Five most common big O run times:

- `O(log_2 n)`, also known as log time. Example: binary search.
- `O(n)`, also known as linear time. Example: simple search.
- `O(n * log_2 n)`. Example: fast sorting algorithm like quicksort.
- `O(n^2)`. Example: slow sorting algorithm, like selection sort.
- `O(n!)`. Example: really slow sorting algorithm, like traveling
  salesperson.

### Traveling salesperson

One of the classic unsolved problems of computer science is the
traveling salesperson problem.

The salesperson has to go to five cities, while traveling the minimum
distance. Looking at every order possible, and adding up the total
distance, he ends up with 120 permutations with only 5 cities. For six
cities, that would take 720 operations, that algorithm has a runtime of
`O(n!)`, also known as factorial time.

There is no fast known algorithm for it, many think it is impossible to
have a better one.

### Takeaways:

- Algorithm speed is not measured in seconds, but in growth of
  operations.
- We measure how quickly the run time of an algorithm increases as the
  size of the input increases.
- Run time is expressed in big O notation.