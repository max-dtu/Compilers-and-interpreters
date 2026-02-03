# Lecture in a nutshell
* **What do we study in this lecture?** Program Graphs :) 
* **Why?** Nice model to understand how programs, compilers and interpreters work! We will use them extensively during the course, so please make sure you build a solid understanding of how they work.
* **How do I know I understood how PGs work?** 👉 Do the [exercises](#Exercises).


## Program Graphs in a nutshell

Download the following book from findit

> ***Formal Methods: An Appetiser, by Flemming Nielson and Hanne Riis Nielson.***
https://findit.dtu.dk/en/catalog/5d4ab0c9d9001d1f5204d936

Read the following parts
* Prologue, upto paragraph **Guarded Commands** (pages ix--x)
* Section 1.1 of Chapter 1 (pages 1--2)

You are welcome to read other sections of the chapter if you are curious, but this is not necessary.

## Examples of PGs

To complement the book, here are some examples of PGs for very simple programs

### Incrementing x

```
x := x + 1
```
 <details>
  <summary>PG</summary>
  ![PG](figures/pg-increment.png)
</details>

### Max via if-then-else

```
if x >= y then
  x := x
else
  z := y >
```
 <details>
  <summary>PG</summary>
  ![PG](figures/pg-max.png)
</details>

### Countdown

```
while x >= 0
  x := x-1
```
 <details>
  <summary>PG</summary>
  ![PG](figures/pg-countdown.png)
</details>

## Runnings PGs

Still missing an intuition of how PGs run?

The state of the computation of a PG is called a *configuration*. It is just a pair (q,m), where q is the current node in the PG in m is the memory (i.e. the value of variables).

Here is the sequence of configurations that illustrates how to run the countdown example if we start with `x` equal to `3`:

```
(q▷,x=3)
(q1,x=3)
(q▷,x=2)
(q1,x=2)
(q▷,x=1)
(q1,x=1)
(q▷,x=0)
(q◀,x=0)
```

et voilà! The PG has finished the computation, `x` is now 0, the countdown is over :)

## Important properties of PGs

Two important properites of programs that also apply for PGs are whether they are 
* *terminating*, i.e. whatever the initial memory is, the PG will finish the computation by reachingthe final node.
* *evolving*, i.e. whatever the initial memory is,  the PG does not get *stuck* in a non-final node during execution;
* *deterministic*, i.e. i.e. whatever the initial memory is, if the PG can finish the computation by reaching a final node, then it will have only one way to do so (i.e. one path in the graph) and the final memory will be determined by such path.

Below you can see related examples

### A non-terminating PG

Consider this new PG for the countdown example that we saw above. 

![PG](figures/pg-countdown-forever.png)

Is it terminating?

 <details>
  <summary>answer</summary>
  Nope 🤦 If `x` is initially negative, the PG will loop forever!
</details>

### A non-evolving PG

Imagine we want to compute in `y` the *polarity* of `x`. That is we want to set `y` to `1` if `x` is positive and `-1` if it is negative and we come out with the following PG

![PG](figures/pg-not-evolving.png)

Well, unfortunately, it is **not** evolving, as it will get stuck if `x` is `0`.

What will make a PG get stuck? A state where all outgoint edges have actions that cannot be executed. Examples...
* Boolean predicates that are false (as in the example above).
* Actions referring to variables that do not exist in memory
* Actions that result in undefined values, for example division by 0, index out of bounds, ...

### A non-deterministic PGs

Let's go back to the problem of computing the polarity of `x` We can fix the problem of the program above by considering the case when `x` is `0` as in the following PG:

![PG](figures/pg-not-deterministic.png)

... but now we have another problem!

Which path do we take if `x` is `0`? The choice will determine the final value of `y`! Same program, two different outcomes... who decides? which one is the right one?


## Solving the exercises
At the end of this page, you find a bunch of exercises. Addresss each exercise like this:

0. Prepare pen & paper! Or find choke/marker and find a board.
1. Read carefully the exercise and try to solve it alone.
2. Discuss your solution with your group members (if you still don't have a group please join/form one!).
3. Compare your solution(s) with the ones provided. Discuss in the group.
4. Stuck? Write down the pseudo-code of the program first, then build the PG.
5. Still stuck? Try this https://formalmethods.dk/fm4fun/ 🥷
6. Doubts about the solutions? Disagreements in your solutions? 👉 Ask the TAs!

***HINT Do not focus on solving as many exercises as possible. Focus instead on being sure you build a solid understanding of how Program Graphs work!***

## Exercises

Draw Program Graphs that solve the following coding problems.

A. Arithmetics
* (a) Factorial. Compute in variable `y` the factorial of `x`. <details>
  <summary>Solution</summary>
  ![solution](solutions/solution-A.a.png)
</details>

* (b) Power. Compute in `z` the value of `x`<sup>`y`</sup>without using an exponential operator `^`. That is, you try to use addition and multiplication. <details>
  <summary>Solution</summary>
  ![solution](solutions/solution-A.b.png)
</details>


* c) Fibbonacci. Compute in `y` the `n`-th Fibonnacci number. <details>
  <summary>Solution</summary>
  ![solution](solutions/solution-A.c.png)
</details>


B. Arrays
* a) Find the maximum integer in array `A` of size `n`. Store the result in variable `max`. <details>
  <summary>Solution</summary>
  ![solution](solutions/solution-B.a.png)
</details>


* b) Search for integer `x` in unordered array `A` of size `n`. If `x` is in the array, store in `j` the index where it lies. Otherwise, `j` should be `-1`. <details>
  <summary>Solution</summary>
  ![solution](solutions/solution-B.b.png)
</details>


* c) Binary search in ordered array. <details>
  <summary>Solution</summary>
  ![solution](solutions/solution-B.c.png)
</details>


C. Sorting
We will write CGL programs that sort an array `A` of size `n`. Store the result in `A`. Each exercise requires a different sorting algorithm.

* a) Insertion sort <details>
  <summary>Solution</summary>
  ![solution](solutions/solution-C.a.png)
</details>


* b) Bubble sort <details>
  <summary>Solution</summary>
  ![solution](solutions/solution-C.b.png)
</details>


* c) Counting sort <details>
  <summary>Solution</summary>
  ![solution](solutions/solution-C.c.png)
</details>

