---
layout: post
title:  "Lynda.com: Four Semesters of Computer Science in 5 Hours"
categories: drafts
---

* <strong><a href="https://www.lynda.com/JavaScript-tutorials/Four-Semesters-Computer-Science-5-Hours/604270-2.html" title="Get a practical introduction to computer science concepts and take your knowledge of JavaScript to the next level.">Four Semesters of Computer Science in 5 Hours</a></strong> by <a href="https://www.lynda.com/author/10466045">Brian Holt</a>
* Released: 6/2/2017
* Duration: 4h 46m
* Skill Level: Intermediate

> Get a practical introduction to computer science concepts and take your knowledge of JavaScript to the next level. This course starts by exploring recursion, followed by how to use sorting algorithms. Next, the main elements of data structure interfaces are explained followed by demonstrations of how to implement list, tree, and table structures. Then, functional programming is covered, including use of map, reduce, and filter. For each section of the course, exercises are provided so you can practice.

> Note: This course was created by Frontend Masters. It was originally released on 07/12/2016. We're pleased to host this training in our library.

> Topics include:
> * Big O
> * Recursion
> * Sort: Bubble, insertion, and merge,
> * Quicksort
> * Median values
> * Interfaces
> * Set, map, stack, and queue
> * Array lists and linked lists
> * Binary search tree
> * AVL tree
> * Single rotation and double rotation
> * Hash table
> * Functional programming
> * Map, reduce, and filter

## Table of Content
{:.no_toc}

* A markdown unordered list which will be replaced with the ToC, excluding the "Contents header" from above
{:toc}

## 1. Big O and Recursion

### 1.1 Introduction
* [http://bit.ly/4semesters](http://bit.ly/4semesters)
* Also a fork with a more mobile-friendly layout: <a href="https://jizusun.github.io/four-semesters-of-cs" target="_blank">https://jizusun.github.io/four-semesters-of-cs</a>
* clickbait title
* Some knowledge of ES6 required
* https://mitpress.mit.edu/books/introduction-algorithms

### 1.2 Big O
> Think of the O as a vacuum that sucks in all the unimportant information and just leaves you with the important stuff. 

### 1.3 Finding Big O
* O(n): without exponential terms
* O(n<sup>2</sup>): nested loop
* O(1)
* O(log n): merge sort, quick sort

### 1.4 Recursion
* a bit of cost because of many callings of functions
* readability over performance, and refactor it later if you figure it's a big bottleneck 

### 1.5 Recursion Example
* Codepen : <http://codepen.io/btholt/pen/rxwEVQ?editors=001>

### 1.6 Exercise 1: Recursion
* Factorial: 
```
function factorial(n) {
    if (n < 2) return 1;
    return n * factorial(n-1;)
}
```

## 2. Sorting Algorithms
### Bubble sort

- The outer loop continues running as long as there are numbers swapped in the previous iteration, which is always going to run at least once.
- The inner loop is gonna go through and swap numbers if they're out of order
- Big O: O(n<sup>2</sup>)
- sort in ascending order
```
5, 7, 6, 4
first outer loop
5, [6, 7], 4 
5, 6, [4, 7]
second outer loop
5, [4, 6], 7
third outer loop
[4, 5], 6, 7
```

### Exercise 2: Bubble sort

- Exercise: <http://codepen.io/btholt/pen/PZKPjj?editors=001>
- Answer (Visualization): <http://codepen.io/btholt/pen/KdYPqa?editors=001>

### Exercise 2: Solution
```javascript
const bubbleSort = (nums) => {
  do {
    let swapped = false;
    for (let i = 0; i < nums.length; i++) {
      // snapshot(nums);
      if (num[i] > num[i+1]) {
        const t = num[i];
        num[i] = num[i+1];
        num[i+1] = t;
        swapped = true;
      }
    }
  } while (swapped)
  // snapshot(nums);
}
```

### Insertion sort

- It's really great for arrays that are very close to sorted. But where it falls apart is if the array is not sorted at all.
- We're going to start grabbing things from the unsorted part of the list and inserting that into the sorted part. 
- Example 
```
5, 3, 6
the 1st element as the sorted part
[5], 3, 6
the first two elements as the sorted part
[3, 5], 6
the whole array is sorted now
[3, 5, 6]
```

### Exercise 3: Insertion sort

### Exercise 3: Solution

- <http://bigocheatsheet.com/>
- `Array.prototype.splice`: a destructive method
- Solution

```js
var insertionSort = nums => {
  for (let i = 1; i < nums.length; i++) {
    for (j = 0; j < i; j++) {
      if (nums[i] < nums[j]) {
        let spliced = nums.splice(i, 1)
        nums.splice(j, 0, spliced[0])
      }
    }
  }
}
```
- Solution from [AP Computer Science A Course Description - Appendix C: Sample Search and Sort Algorithms](https://apcentral.collegeboard.org/pdf/ap-computer-science-a-course-description.pdf
)

```js
function insertionSort (nums) {
  for (let j = 1; j < nums.length; j++) {
    snapshot(nums)
    const temp = nums[j] 
    let possibleIndex = j
    // debugger;
    while (possibleIndex > 0 && temp < nums[possibleIndex-1]) {
      nums[possibleIndex] = nums[possibleIndex - 1]
      possibleIndex-- 
    }
    nums[possibleIndex] = temp;
  }
}
```

### Merge sort

- stable: quick sorting is not stable
- consistent
- uses recursion
- device-and-conquer
- complexity: O(n log n)
  + <https://stackoverflow.com/questions/7801861/why-is-merge-sort-worst-case-run-time-o-n-log-n>
  + <https://www.toptal.com/developers/sorting-algorithms>

### Exercise 4: Merge sort
- You must **assume** the sub-array to be merged are already sorted

### Exercise 4: Solution

```js
function stitch(left, right) {
  const results = [];

  while (left.length && right.length) {
    if (left[0] <= right[0]) {
      results.push(left.shift())
    } else {
      results.push(right.shift())
    }
  }

  return [...results, ...left, ...right];
}

function mergeSort(nums) {
  if (nums.length < 2) {
    return nums;
  }

  const length = nums.length;
  const middle = Math.floor(length / 2);
  const left = nums.slice(0, middle);
  const right = nums.slice(middle, length);

  return stitch(mergeSort(left), mergeSort(right));
}

```

### Median values

```
Find the median of two sorted arrays e.g.
[1, 5, 8, 9]
[2, 3, 7, 10]
```

Solutions:
- concat and sort: [1, 5, 8, 9, 2, 3, 7, 10], then sort it
- sort by stitching: stop at the index of the median value

### Quicksort

- Pivot (always the last one)
- Divide and Conquer
- Example

### Exercise 5: Quicksort

### Exercise 5: Solution
```js
const quickSort = (nums) => {
  if (nums.length <= 1) return nums;

  const pivot = num[nums.length - 1];
  const left = [];
  const right = [];

  for (let i = 1; i< nums.length - 1; i++) {
    if (nums[i] < pivot) {
      left.push(nums[i]);
    } else {
      right.push(nums[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)]
}
```
## 3. Data Structure Interfaces

### Interfaces

(nothing ...)

### Set

- more of an object
- an amorphous cloud
- has no duplicate
- no guarantee of order
- ES6 has native `Set`

### Map

- aka `dictionary`
- normal objects in JavaScript
- just key-value pairs
- no concept of order
- ES6 has native `Map` 
- <http://2ality.com/>

### Stack

- `last-in-first-out`
- `pop`
- `push`
- `peek`

### Queue
- `enqueue`
- `dequeue`
- priority queue

## 4. Implementing Data Structures

### Array list

- shifting becomes very very expensive
- optimized for `get`, de-optimized for `delete` and `insert`

### Exercise 6: Array list

* <http://codepen.io/btholt/pen/adLxyv?editors=001>

```js
class ArrayList {
  constructor() {
    this.length = 0;
    this.data = {};
  }

  push(value) { }

  pop() { }

  get(index) { }

  delete(index) { }

  _collapseTo(index) { }
}
```

### Exercise 6: Solution

* Also see at: <https://github.com/jizusun/learn-data-structures-with-javascript/blob/master/lib/ArrayList.js>

### Linked list

- <https://jizusun.github.io/four-semesters-of-cs/#linked-list>
- `head`
- `next`
- `tail` 
- get (by index): i s very expensive
- delete: really cheap
- pop: easy, simple by pointing to `null`

### Exercise 7: Linked list

### Exercise 7: Solution, part 1

### Exercise 7: Solution, part 2

### Binary search tree

### Exercise 8: Binary search tree

### Exercise 8: Solution

### AVL tree

* <https://jizusun.github.io/four-semesters-of-cs/#avl-tree>

### Single rotation

### Double rotation
* <https://www.lynda.com/JavaScript-tutorials/Double-rotation/604270/623686-4.html>

### Exercise 9: Solution, part 1

### Exercise 9: Solution, part 2

### Hash table

## 5. Functional Programming 101

### Functional programming concepts

### Map

### Reduce

### Filter

