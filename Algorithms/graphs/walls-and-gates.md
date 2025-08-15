## [Walls and Gates](https://neetcode.io/problems/islands-and-treasure?list=neetcode150)

<!-- notecardId: 1755264849924 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/e69C6xhiSQE

// Complexity:
// - Time: O(rows * cols)
// - Space: O(rows * cols)
class Solution {
  islandsAndTreasure(grid) {
    if (!grid || !grid.length) return;

    const rows = grid.length;
    const cols = grid[0].length;
    const queue = [];

    for (let r = 0; r < rows; r += 1) {
      for (let c = 0; c < cols; c += 1) {
        if (grid[r][c] === 0) {
          queue.push([r, c]);
        }
      }
    }

    const directions = [
      [1, 0],
      [-1, 0],
      [0, 1],
      [0, -1],
    ];

    while (queue.length) {
      const [prevRow, prevCol] = queue.shift();

      for (const [dr, dc] of directions) {
        const row = prevRow + dr;
        const col = prevCol + dc;

        if (
          row < 0 ||
          col < 0 ||
          row === rows ||
          col === cols ||
          grid[row][col] !== 2147483647
        ) {
          continue;
        }
        {
          grid[row][col] = 1 + grid[prevRow][prevCol];
          queue.push([row, col]);
        }
      }
    }
  }
}
```
