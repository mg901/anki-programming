## [304 Range Sum Query 2D - Immutable](https://leetcode.com/problems/range-sum-query-2d-immutable/description/)

```js
// Explanation:
// - Algorithm:
//    Profound Academy: https://youtu.be/WibxoqMSMCw

// - Problem:
//    Neetcode: https://youtu.be/KE8MQuwE2yA

// - Time: O(1)
// - Space: O(m * n)
class NumMatrix {
  #prefix;

  constructor(matrix) {
    const rows = matrix.length;
    const cols = matrix[0].length;

    this.#prefix = Array.from({ length: rows + 1 }, () =>
      new Array(cols + 1).fill(0),
    );

    for (let r = 1; r <= rows; r += 1) {
      for (let c = 1; c <= cols; c += 1) {
        this.#prefix[r][c] =
          this.#prefix[r - 1][c] +
          this.#prefix[r][c - 1] -
          this.#prefix[r - 1][c - 1] +
          matrix[r - 1][c - 1];
      }
    }
  }

  sumRegion(ur, lc, br, rc) {
    return (
      this.#prefix[br + 1][rc + 1] -
      this.#prefix[ur][rc + 1] -
      this.#prefix[br + 1][lc] +
      this.#prefix[ur][lc]
    );
  }
}
```
