# sudoku

A Clojure library designed to solve sudoku puzzles.


## Setup in Emacs

I use Emacs Live with the following steps to prepare this project for hacking in the REPL:

1. M-x cider-jack-in
2. C-x o (switch to non-REPL buffer)
3. C-x C-f src/sudoku/core.clj (open code file)
4. C-c C-k (compile src)
5. C-c M-n (change REPL namespace to sudoku.core)
6. switch to REPL buffer and start hacking...


## Usage

In this namespace, "data" is a blank sudoku data structure. To see a visual represenation of this data structure, write html to a file, per code below, and then open the resultant file in any browser:

```clojure
(write-data "/absolute/path/works/best/data.html" data)
```

The image at this link shows that every cell can have the possible values [1-9]:

[Blank Puzzle Data Structure](images/puzzle1/data.png)


## Example Puzzle

Given this puzzle: [Puzzle #1](images/puzzle1/puzzle1.png)

Load the encoded puzzle1 into a data structure, and then write html to a file to view in a browser:

```clojure
(def data2 (assign-values data puzzle1))
(write-data "/absolute/path/works/best/data.html" data2)
```

[Loaded Puzzle Data Structure](images/puzzle1/data2.png)


Solving the puzzle involves incrementally simplifying the data structure using increasingly complex algorithms dependent on puzzle difficulty.

The next step simplifies the puzzle by iterating over all groups and applying the intra-group algorithm. The first iteration:

```clojure
(def data3 (solve-puzzle puzzle1 1))
(write-data "/absolute/path/works/best/data.html" data3)
```

[Simplified Puzzle Data Structure (1 Iteration)](images/simplify/data1.png)


Each iteration of the algorithm attempts to simplify each group by creating sets within the group that contain exclusive values. The simplest case is a naked single in which a solved cell results in removing that cell's value from every other cell in the group. The algorithm continues by attempting to create exclusive value sets up to size 8.

The second iteration:

```clojure
(def data4 (solve-puzzle puzzle1 2))
(write-data "/absolute/path/works/best/data.html" data4)
```

[Simplified Puzzle Data Structure (2 Iterations)](images/simplify/data2.png)


After the 3rd iteration, the puzzle is solved:

```clojure
(def data5 (solve-puzzle puzzle1))
(write-data "/absolute/path/works/best/data.html" data5)
(data-is-solved data5)
```

[Solved Puzzle](images/simplify/data3.png)


The intra-group algorithm addresses all of these possible occurrences (previously addressed in separate algorithms):
* Naked Singles
* Naked Doubles
* Naked Triples
* Naked Quadruples
* Hidden Singles
* Hidden Doubles
* Hidden Triples
* Hidden Quadruples


In the case of harder puzzles, inter-group algorithms are needed to continue simplifying the problem space.

Inter-Group Algorithms to be encoded:
* Locked Candidates
* X-Wing
* XY-Wing
* Swordfish


## License

This project is a POC demonstrating what can be done with Clojure.
Please contact me if you have any comments or suggestions.

Copyright © 2015 Whit Chapman
