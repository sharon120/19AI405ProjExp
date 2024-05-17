# Implement a Sudoku Solver From Scratch
## Steps to solve the Sudoku Puzzle in Python
<ol>
  <li>In this method for solving the sudoku puzzle, first, we assign the size of the 2D matrix to a variable M (M*M).</li>
 <li>Then we assign the utility function (puzzle) to print the grid.</li>
<li>Later it will assign num to the row and col.</li>
<li>If we find the same num in the same row or same column or in the specific 3*3 matrix, ‘false’ will be returned.</li>
<li>Then we will check if we have reached the 8th row and 9th column and return true for stopping further backtracking.</li>
<li>Next, we will check if the column value becomes 9 then we move to the next row and column.</li>
<li>Further now we see if the current position of the grid has a value greater than 0, then we iterate for the next column.</li>
<li>After checking if it is a safe place, we move to the next column and then assign the num in the current (row, col) position of the grid. Later we check for the next possibility with the next column.</li>
<li>As our assumption was wrong, we discard the assigned num and then we go for the next assumption with a different num value</li>
</ol>

## PROGRAM
# DEVELOPED BY:Sharon Harshini L M
# REG NO:212223040193
    def print_grid(grid):
     for row in grid:
        print(" ".join(map(str, row)))

    def is_safe(grid, row, col, num):
    # Check if num is not already present in current row, column, or 3x3 subgrid
    for i in range(9):
        if grid[row][i] == num or grid[i][col] == num or grid[row//3*3 + i//3][col//3*3 + i%3] == num:
            return False
    return True

    def solve_sudoku(grid):
    # Find empty location in grid
    empty_location = find_empty_location(grid)
    if not empty_location:
        return True  # Sudoku solved successfully
    
    row, col = empty_location

    # Try placing numbers from 1 to 9
    for num in range(1, 10):
        if is_safe(grid, row, col, num):
            # Assign the number if it's safe
            grid[row][col] = num
            
            # Recursive call to solve Sudoku for next position
            if solve_sudoku(grid):
                return True
            
            # Backtrack if current assignment doesn't lead to a solution
            grid[row][col] = 0
    
    # No number from 1 to 9 fits at this location, backtrack
    return False
    def find_empty_location(grid):
    for i in range(9):
        for j in range(9):
            if grid[i][j] == 0:
                return (i, j)
    return None

    #Example Sudoku grid (0 represents empty cells)
    grid = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],
    [6, 0, 0, 1, 9, 5, 0, 0, 0],
    [0, 9, 8, 0, 0, 0, 0, 6, 0],
    [8, 0, 0, 0, 6, 0, 0, 0, 3],
    [4, 0, 0, 8, 0, 3, 0, 0, 1],
    [7, 0, 0, 0, 2, 0, 0, 0, 6],
    [0, 6, 0, 0, 0, 0, 2, 8, 0],
    [0, 0, 0, 4, 1, 9, 0, 0, 5],
    [0, 0, 0, 0, 8, 0, 0, 7, 9]
    ]

    if solve_sudoku(grid):
    print("Sudoku Solved Successfully:")
    print_grid(grid)
    else:
    print("No solution exists.")

## Output

   Sudoku Solved Successfully:
   
   5 3 4 6 7 8 9 1 2
   
   6 7 2 1 9 5 3 4 8
   
   1 9 8 3 4 2 5 6 7
   
   8 5 9 7 6 1 4 2 3
   
   4 2 6 8 5 3 7 9 1
   
   7 1 3 9 2 4 8 5 6
   
   9 6 1 5 3 7 2 8 4
   
   2 8 7 4 1 9 6 3 5
   
   3 4 5 2 8 6 1 7 9

## Result

Thus the above program is written and executed successfully.
