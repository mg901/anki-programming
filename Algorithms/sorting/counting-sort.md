## [Counting Sort 'stable'](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1765200225881 -->

```js
// Explanation:
// - Quoc Dat Phung: https://youtu.be/IcIig2uY0YI

// Type: Stable

// - Time: O(n + k)
//    where:
//      k - counter.length

// - Space: O(n + k)
function countingSort(ints) {
  const n = ints.length;

  const min = Math.min(...ints);
  const max = Math.max(...ints);

  if (min === max) return ints;

  const range = max - min + 1;
  const counter = new Array(range).fill(0);
  const sorted = new Array(n);

  for (const int of ints) {
    counter[int - min] += 1;
  }

  for (let i = 1; i < range; i += 1) {
    counter[i] += counter[i - 1];
  }

  for (let i = n - 1; i >= 0; i -= 1) {
    const num = ints[i];
    const idx = num - min;
    counter[idx] -= 1;
    sorted[counter[idx]] = num;
  }

  return sorted;
}
```

## [Counting Sort 'unstable'](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1765200225885 -->

```js
// Explanation:
// - Quoc Dat Phung: https://youtu.be/4gK9bnlOq8o

// Type: Unstable

// - Time: O(n + k)
//   where:
//     k = counter.length

// - Space: O(k)
function countingSort(ints) {
  const n = ints.length;

  const min = Math.min(...ints);
  const max = Math.max(...ints);

  if (min === max) return ints;

  const range = max - min + 1;
  const counter = new Array(range).fill(0);

  for (const int of ints) {
    counter[int - min] += 1;
  }

  const sorted = [];

  for (let i = 0; i < range; i += 1) {
    while (counter[i] > 0) {
      sorted.push(i + min);
      counter[i] -= 1;
    }
  }

  return sorted;
}
```
