## [Counting Sort 'stable'](https://leetcode.com/problems/sort-an-array/description/)

```js
// - Time: O(n + k)
//    where:
//      k - count.length
// - Space: O(k)
function countingSort(arr) {
  const n = arr.length;
  if (n === 0) return arr;

  const min = Math.min(...arr);
  const max = Math.max(...arr);
  const range = max - min + 1;

  const count = new Array(range).fill(0);
  const output = new Array(n);

  for (let i = 0; i < n; i += 1) {
    count[arr[i] - min] += 1;
  }

  // 2) prefix sum
  for (let i = 1; i < range; i += 1) {
    count[i] = count[i] + count[i - 1];
  }

  // 3) fill output (right to left) → this makes it stable
  for (let i = n - 1; i >= 0; i -= 1) {
    const val = arr[i];
    const idx = val - min;
    const pos = count[idx] - 1;

    output[pos] = val;
    count[idx] -= 1;
  }

  // 4) copy back
  for (let i = 0; i < n; i += 1) {
    arr[i] = output[i];
  }

  return arr;
}
```

## [Counting Sort 'unstable'](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1763754920413 -->

```js
// Type: Unstable

// - Time: O(n + k)
// - Space: O(k)
//   where:
//     k = freq.length
function sortArray(nums) {
  if (nums.length < 2) return nums;

  const min = Math.min(...nums);
  const max = Math.max(...nums);

  const range = max - min + 1;
  const freq = new Array(range).fill(0);

  for (const num of nums) {
    freq[num - min] += 1;
  }

  const result = [];

  for (let i = 0; i < range; i += 1) {
    while (freq[i] > 0) {
      result.push(i + min);
      freq[i] -= 1;
    }
  }

  return result;
}
```
