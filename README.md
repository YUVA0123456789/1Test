# 1Test
no desc
import random

class Maze:
    def __init__(self, rows, cols):
        self.rows = rows
        self.cols = cols
        self.grid = [['#' for _ in range(cols)] for _ in range(rows)]

    def generate_maze(self, start_row=1, start_col=1):
        stack = [(start_row, start_col)]
        while stack:
            current_row, current_col = stack[-1]

            neighbors = [(current_row - 2, current_col), (current_row, current_col + 2),
                         (current_row + 2, current_col), (current_row, current_col - 2)]
            random.shuffle(neighbors)

            found = False
            for neighbor_row, neighbor_col in neighbors:
                if 0 < neighbor_row < self.rows - 1 and 0 < neighbor_col < self.cols - 1 and self.grid[neighbor_row][neighbor_col] == '#':
                    self.grid[current_row + (neighbor_row - current_row) // 2][current_col + (neighbor_col - current_col) // 2] = ' '
                    self.grid[neighbor_row][neighbor_col] = ' '
                    stack.append((neighbor_row, neighbor_col))
                    found = True
                    break

            if not found:
                stack.pop()

    def display_maze(self):
        for row in self.grid:
            print(''.join(row))


if __name__ == "__main__":
    rows, cols = 11, 21
    maze = Maze(rows, cols)
    maze.generate_maze()
    maze.display_maze()
