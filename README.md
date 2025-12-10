This solution is nice and clear. Turning the "solve" function into a generator for ALL solutions of the SuDoKu is straightforward.

def solve(grid, r=0, c=0):
    if r == 9:
        yield [row[:] for row in grid]  # yield a copy of the grid as a solution
    elif c == 9:
        yield from solve(grid, r + 1, 0)
    elif grid[r][c] != 0:
        yield from solve(grid, r, c + 1)
    else:
        for k in range(1, 10):
            if is_valid(grid, r, c, k):
                grid[r][c] = k
                yield from solve(grid, r, c + 1)
                grid[r][c] = 0

for solution in solve([row[:] for row in grid]):
    print(*solution, sep='\n')
    print('-' * 20)
