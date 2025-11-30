## [2013 Detect Squares](https://leetcode.com/problems/detect-squares/description/)

```js
// Explanation:
// - Neetcode: https://youtu.be/bahebearrDc

// - Space: O(n)
class DetectSquares {
  #points = new Map();

  // Time: O(1)
  add([x, y]) {
    if (!this.#points.has(x)) {
      this.#points.set(x, new Map());
    }

    const counterY = this.#points.get(x);
    counterY.set(y, (counterY.get(y) ?? 0) + 1);

    return this;
  }

  // - Time: O(n)
  count([x, y]) {
    let count = 0;
    if (!this.#points.has(x)) return 0;

    for (const [otherX, counterY] of this.#points) {
      if (otherX === x) continue;

      const diff = x - otherX;

      for (const deltaY of [diff, -diff]) {
        const otherY = y + deltaY;

        const count1 = counterY.get(otherY) ?? 0;
        const count2 = this.#points.get(x).get(otherY) ?? 0;
        const count3 = counterY.get(y) ?? 0;

        count += count1 * count2 * count3;
      }
    }

    return count;
  }
}
```
