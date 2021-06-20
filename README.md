# sudoku-solver-go
A simple sudoku solver in go

The solver employs two different sub-approaches to solve a sudoku (concurrent and recursive)

1. The solver first maps the set of eligible numbers for each cell. It also fills the cells which have just a single eligible number. This is a "map and reduce"    performed on each cell.

2. If each iteration keeps reducing the number of unfilled cells, the solver keeps repeating "map and reduce" until the sudoku is solved.

3. When the number of unfilled cells stops reducing, the solver switches to a brute force trial and error approach.

4. Under this approach, the cell with least number of eligible numbers is identified.

5. The solver fires a go routine as a recursive call to itself for each of these eligible numbers after filling the cell with the number.

6. In the next iteration, the next cell with least number of eligible numbers is picked up, so on and so forth

7. This keeps repeating until either the sudoku is solved or a total of ten million iterations are exhausted.


The important thing to note aswell is this. The sudoku is represented as a slice of int slice. A custom Copy method is written to perform deep copy of a sudoku. This is important since each thread of solver must work on a distinct copy of a sudoku to avoid data race.
