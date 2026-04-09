---
title: Chapter 2
published: 2026-04-08
description: Chapter 2 of Grokking Algorithms.
tags: [Book Review, Blogging]
category: Grokking Algorithms
draft: false
---

# Grokking Algorithms
## 2 - Selection Sort
### Arrays vs linked lists:

Arrays store data all together, one after another, while linked lists
store them randomly, and every element has a pointer to the address of
the next element.

This solves the problem that there might not be enough "drawers"
available that are one next to another when saving an array, and for
example when you want to add one more item to an array but the next
space is already taken by something else, you will have to move the
entire array to a new place.

Sometimes you might want to hold some spaces for this array, for example
10 spaces, but if you never end up using them, the memory is wasted,
and if you end up needing more than 10 spaces, you'll have to move the
array anyway.

Linked lists solve these problems because you can store each item on
any space, not needing for them to be in order. However, there are some
pros and cons for each of those two methods of storage.

### Pros and Cons

Differently from linked lists, when you have an array you know the
address of every element, while for a linked list, you need to start
from the beginning in order to find the element you want every time.

Arrays also support caching, and when computers read sections of memory,
it can read the entire section of the items. You can't do that with
linked lists because they are randomly distributed.

So, when reading, arrays clearly have the advantage. But when inserting,
that's when linked lists really shine. If you want to add an element to
the middle of the array, you need to shift all other elements down, but
with linked lists, you just need to change the pointer of the element
before yours, and your element will need the pointer that was on that
element. When thinking big O notation, it will look like this:

|             | Arrays | Linked Lists |
|-------------|--------|---------------|
| Reading     | O(1)   | O(n)          |
| Insertion   | O(n)   | O(1)          |
| Deletion    | O(n)   | O(1)          |

*\*N is the number of elements on the array or list.*

### Which is more used

Arrays are more used, because they provide **random access**. Lists only
support **sequential access** (reading all elements one by one).

And although you might save more space than you need with arrays, you
also use more space using lists, since you need to store the pointer
along with every element. When the element is very big, it might not
matter, but if the element is very small, that might double the size of
the space needed.

Only in specific use cases linked lists are used.

### Selection Sort

Selection sort is basically going to every element, finding the smallest
and putting that element into the new array.

Given an array of `n` elements, the runtime of the selection sort
algorithm will be $$\mathrm{O}(n^2)$$ . That is because constants in big
O notation are ignored, technically, the runtime is
$$\mathrm{O}(n \times \frac{1}{2} \times n)$$ , so we just write
$$\mathrm{O}(n \times n)$$ , or $$\mathrm{O}(n^2)$$

```python title="selection_sort.py"
def findSmallest(arr):
    smallest = arr[0]
    smallest_index = 0
    for i in range(1, len(arr)):
        if arr[i] < smallest:
            smallest = arr[i]
            smallest_index = i
        return smallest_index
def selectionSort(arr):
    newArr = []
    copiedArr = list(arr)
    for i in range(len(copiedArr)):
        smallest = findSmallest(copiedArr)
        newArr.append(copiedArr.pop(smallest))
    return newArr
print(selectionSort([5,3, 6, 2, 10]))
```

```js title="selection_sort.js"
function find_smallest(arr) {
    let smallest = arr[0];
    let smallest_index = 0;
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] < smallest) {
            smallest = arr[i];
            smallest_index = i;
        }
    }
return smallest_index;
}

function selection_sort(arr) {
    let newArr = [];
    let copiedArr = arr.slice();
    for (let i = 0; i < arr.length; i++) {
        let smallest = find_smallest(copiedArr);
        newArr.push(copiedArr.splice(smallest, 1)[0]);
    }
    return newArr;
}
console.log(selection_sort([5, 3, 6, 2, 10]));
```