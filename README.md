# Algorithms and data structures

## Table of Contents

- [Introduction](#introduction)
- [Exercise 1](#exercise1)
- [Exercise 2](#exercise2)
- [Exercise 3](#exercise3)
- [Exercise 4](#exercise4)
- [License](#license)

## Introduction

The laboratory project consists in the implementation of four exercises (two developed in C language and two in Java language) as reported below.

## Exercise 1

Implement a library that offers two sorting algorithms: `Quick Sort` and `Quick Sort`. By `Binary Insertion Sort`, we refer to a version of the `Insertion Sort` algorithm in which the position within the sorted section of the array to insert the current element is determined through binary search. In the implementation of `Quick Sort`, the choice of the pivot should be studied and discussed in the report.

The code implementing `Quick Sort` and `Binary Insertion Sort` must be generic. Furthermore, the library must allow specifying (i.e., accepting as input) the criterion according to which to sort the data.


Implement the unit tests for the library as suggested in the Unit Testing document.


Using the implemented sorting library: the `records.csv` file that you can find (compressed) at

```
https://datacloud.di.unito.it/index.php/s/X7qC8JSLNRtLxPC
```

contains 20 million records to be sorted.
Each record is described on one line and contains the following fields:

- id: (integer type) unique identifier of the record;
- field1: (string type) contains words extracted from the divine comedy,
  you can assume that the values do not contain spaces or commas;
- field2: (integer type);
- field3: (floating point type);

The format is a standard CSV: fields are separated by commas; records are
separated by `\n`.

Using the implemented `Quick Sort` and `Binary Insertion Sort` algorithms, sort the *records* (it is not sufficient to sort the
individual fields) contained in the `records.csv` file in non-decreasing order according to the values contained in the three `field` fields (therefore, it is necessary to repeat the sorting three times, once for each field).

Measure the response times by varying the criterion for choosing the `pivot` in the `Quick Sort` and produce a short report in which the results obtained are given along with a commentary on them. In case the sorting goes on for more than 10 minutes you can stop the execution and report a failure of the operation.

Are the results what you would have expected? If yes, why? If no, make assumptions about why the algorithms do not perform as you expected, one algorithm offers better performance than the other, the choice of `pivot` affects the performance of `Quick Sort`. Check them out and report what you find in the report.

## Exercise 2

Realize a data structure called `skip_list`. The `skip_list` is a type of concatenated list that stores an ordered *list* of elements.

In contrast to classical concatenated lists, the `skip_list` is a probabilistic data structure that allows the search operation to be performed with `O(log n)` complexity in terms of time. The operations of inserting and deleting elements can also be realized in `O(log n)` time. For this reason, the `skip_list` is one of the data structures that are often used to index data.

Each node in a concatenated list contains a pointer to the next element in the list. We must then scroll through the list sequentially to find an element in the list. The `skip_list` speeds up the search operation by creating "express paths" that allow us to skip part of the list during the search operation. This is possible because each node of the `skip_list` contains not only a single pointer to the next element in the list, but an array of pointers that allow us to jump to different following points in the list. An example of this pattern is shown in the following figure:

![Example of a `skip_list`. From the node containing the number 6, one can jump directly to nodes 9 and 25, without visiting the other nodes.](skiplist.png)

Then implement a library that implements the `skip_list` data structure. The implementation should be generic in terms of the type of data stored in the structure. As a suggestion, a possible definition of the `skip_list` data type is as follows:

```
#define MAX_HEIGHT ....

typedef struct _SkipList SkipList;
typedef struct _Node Node;

struct _SkipList {
  Node *head;
  unsigned int max_level;
  int (*compare)(void*, void*);
};

struct _Node {
  Node **next;
  unsigned int size;
  void *item;
};
```

Where:

- `MAX_HEIGHT`: is a constant that defines the maximum number of pointers that can be in a single node of the `skip_list`. As seen in the figure, each node can have a distinct number of pointers.
- `unsigned int size`: is the number of pointers in a given node of the `skip_list`.
- `unsigned int max_level`: determines the current maximum among the various `sizes`.

The library must include the two operations listed below, which are given in pseudo-code. Translate the pseudo-code into C.


```
insertSkipList(list, I)

    new = createNode(I, randomLevel())
    if new->size > list->max_level
        list->max_level = new->size

    x = list->head
    for k = list->max_level downto 1 do
        if (x->next[k] == NULL || I < x->next[k]->item)
            if k < new->size {
              new->next[k] = x->next[k]
              x->next[k] = new
            }
        else
            x = x->next[k]
```

The ``randomLevel()`` function determines the number of pointers to be included in the new node and must be implemented in accordance with the following algorithm. Explain the advantage of this algorithm in the report to be delivered with the exercise:
```
randomLevel()
    lvl = 1

    // random() returns a random value in [0...1)
    while random() < 0.5 and lvl < MAX_HEIGHT do
        lvl = lvl + 1
    return lvl
```

```
searchSkipList(list, I)
    x = list->head

    // loop invariant: x->item < I
    for i = list->max_level downto 1 do
        while x->next[i]->item < I do
            x = x->next[i]

    // x->item < I <= x->next[1]->item
    x = x->next[1]
    if x->item == item then
        return x->item
    else
        return failure
```


The library must also include functions to create an empty `skip_list` and completely delete an existing `skip_list`. The latter operation, in particular, must properly free all memory allocated for the `skip_list`.

Implement unit tests for all `skip_list` operations according to the directions suggested in the Unit Testing document.

At address

```
https://datacloud.di.unito.it/index.php/s/taii8aA8rNnXgCN
```
you can find a dictionary (`dictionary.txt`) and a file to correct (`correctme.txt`).

The dictionary contains a list of words. The words are written below, each on a line.

The file `correctme.txt` contains text to correct. Some words in this text are not in the dictionary.

Implement an application that uses the ``skip_list`` data structure to efficiently determine the list of words in the text to be corrected that are not in the dictionary given as input to the program.

Experiment with the operation of the application by considering different values for the ``MAX_HEIGHT`` constant, reporting the results of the experiments in a brief report (about one page).

## Exercise 3

Implement a library that realizes the Minimum Heap data structure. The data structure must:
- represent the heap internally via a vector (other internal support structures can also be used if needed);
- allow any number of a priori unknown elements of the heap;
- be generic with regard to the type of the heap elements;
- be generic with regard to the criterion for comparing heap elements.

It must, in addition, offer (at least) the following operations (next to each operation is specified the
required complexity, where n indicates the number of heap elements):
- creation of a minimum empty heap - O(1);
- insertion of an element - O(log n);
- returning the size of the heap - O(1);
- return of the parent of an element - O(1);
- return of the left child of an element - O(1);
- return of the right child of an element - O(1);
- extraction of the element with minimum value - O(log n);
- decreasing the value of an element - O(log n).

A description of the Heap data structure can be found on the transparencies and handouts provided in the theory portion of the course,
 as well as on the text Cormen et al, `Introduction to Algorithms and Data Structures`, McGraw-Hill, Third Edition, 2010, in the chapter `Heapsort`. In particular, reference to the text is suggested for all those aspects not explicitly covered in class.

Implement unit tests for the library as suggested in the Unit Testing document.

## Esercizio 4

You implement a library that realizes the Grafo data structure in a way that **is optimal for sparse data**.
(IMPORTANT: The implementation choices you make must be justified in relation to the concepts presented
during the classroom lectures). The structure should allow you to represent both directed and undirected graphs
(HINT: an undirected graph can be represented using a modified implementation for directed graphs
to ensure that, for every arc (a,b), labeled w, present in the graph, the arc (b,a) is also present in the graph,
labeled w. Obviously, the graph must retain the information specifying whether it is a directed or undirected graph.).

The implementation must be generic in terms of both the type of the nodes and the labels
of the arcs.

The implemented data structure must offer (at least) the following operations (next to each operation is specified the
complexity required; n may indicate the number of nodes or the number of arcs, depending on the context):

- Creating an empty graph - O(1)
- Adding a node - O(1)
- Adding an arc - O(1)
- Checking whether the graph is directed - O(1)
- Verifies whether the graph contains a given node - O(1)
- Verification whether the graph contains a given arc - O(1) (*)
- Deletion of a node - O(n)
- Deletion of an arc - O(1) (*)
- Determination of the number of nodes - O(1)
- Determination of the number of arcs - O(n)
- Retrieval of the nodes of the graph - O(n)
- Recovery of the arcs of the graph - O(n)
- Recovery of adjacent nodes of a given node - O(1) (*)
- Retrieving label associated with a pair of nodes - O(1) (*)

(*) when the graph is truly sparse, assuming the operation is performed on a node whose adjacency list has a length in O(1).

Implement the unit tests for the library as suggested in the Unit Testing document.

Implement Dijkstra's algorithm to determine the minimum paths from a single source in a weighted oriented graph, with arc weights all non-negative.

The implementation of Dijkstra's algorithm must operate on a graph made using the library implemented according to the specifications given above and must also use within it a minimum priority queue represented with a heap made using the library implemented according to the specifications in Exercise 3.

Write an application that uses the implemented Dijkstra algorithm to determine the minimum paths from the city of Turin on the graph described in the italian\_dist\graph.csv file that you can find (compressed) at

```
https://datacloud.di.unito.it/index.php/s/PirTJpq4JMnpH3G
```

This file contains the distances in meters between some localities
Italy and a fraction of the localities nearest to them.
The format is a standard CSV: fields are separated by commas; records are separated by the end character
line (\n).

Each record contains the following data:

- location 1: (string type) name of the "source" location. The string can contain spaces; it cannot contain commas;
- location 2: (string type) "destination" location name. String can contain spaces, cannot contain commas;
- distance: (float type) distance in meters between the two locations.

## License

This project is licensed under the [MIT License](https://github.com/albertoomarino/algorithms-and-data-structures/blob/main/LICENSE).

© [Alberto Marino]
