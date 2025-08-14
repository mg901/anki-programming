## [Walls and Gates](https://neetcode.io/problems/islands-and-treasure?list=neetcode150)

<!-- notecardId: 1749465239886 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/e69C6xhiSQE

// Complexity:
// - Time: O(rows * cols)
// - Space: O(rows * cols)
class Solution {
  islandsAndTreasure(rooms) {
    if (!rooms || !rooms.length) return;

    let rows = rooms.length;
    let cols = rooms[0].length;
    let queue = [];

    for (let r = 0; r < rows; r += 1) {
      for (let c = 0; c < cols; c += 1) {
        if (rooms[r][c] === 0) {
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
      const [row, col] = queue.shift();

      for (const [dr, dc] of directions) {
        const r = row + dr;
        const c = col + dc;

        if (
          r < 0 ||
          c < 0 ||
          r >= rows ||
          c >= cols ||
          rooms[r][c] !== 2147483647
        ) {
          continue;
        }

        rooms[r][c] = rooms[row][col] + 1;
        queue.push([r, c]);
      }
    }
  }
}
```
