## [Merge Sort](https://www.greatfrontend.com/questions/algo/merge-sort)

<!-- notecardId: 1764464515632 -->

```js
// Explanation:
// - CS50: https://youtu.be/Qs3l8_wd_34

// Type: Stable

// - Time: O(n log(n))
// - Space: O(n)
export default function recursiveMergeSort(arr) {
  const n = arr.length;
  if (n < 2) return arr;

  const mid = Math.floor(n / 2);
  const left = recursiveMergeSort(arr.slice(0, mid));
  const right = recursiveMergeSort(arr.slice(mid));

  return merge(left, right);
}

function merge(a, b) {
  const m = a.length;
  const n = b.length;

  let i = 0;
  let j = 0;

  const merged = [];

  while (i < m && j < n) {
    if (a[i] <= b[j]) {
      merged.push(a[i]);
      i += 1;
    } else {
      merged.push(b[j]);
      j += 1;
    }
  }

  while (i < m) {
    merged.push(a[i]);
    i += 1;
  }

  while (j < n) {
    merged.push(b[j]);
    j += 1;
  }

  return merged;
}
```

## [Merge Sort 'in-place'](https://bigfrontend.dev/problem/implement-Merge-Sort)

<!-- notecardId: 1764467458974 -->

```js
// Explanation:
// - CS50: https://youtu.be/Qs3l8_wd_34

// Type: Stable

// - Time: O(n log(n))
// - Space: O(n)
function mergeSort(arr) {
  const n = arr.length;
  if (n < 2) return;

  sort(arr, new Array(n));
}

function sort(arr, temp, left = 0, right = arr.length - 1) {
  if (left >= right) return;

  const mid = left + ((right - left) >> 1);

  sort(arr, temp, left, mid);
  sort(arr, temp, mid + 1, right);

  merge(arr, temp, left, mid, right);
}

function merge(arr, temp, left, mid, right) {
  let i = left;
  let j = mid + 1;
  let k = left;

  while (i <= mid && j <= right) {
    if (arr[i] <= arr[j]) {
      temp[k] = arr[i];
      i += 1;
    } else {
      temp[k] = arr[j];
      j += 1;
    }

    k += 1;
  }

  while (i <= mid) {
    temp[k] = arr[i];
    i += 1;
    k += 1;
  }

  while (j <= right) {
    temp[k] = arr[j];
    j += 1;
    k += 1;
  }

  for (let l = left; l <= right; l += 1) {
    arr[l] = temp[l];
  }
}
```
