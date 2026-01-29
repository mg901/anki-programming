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

## [Merge Sort 'in-place'](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1769691872192 -->

```js
// Explanation:
// - CS50: https://youtu.be/Qs3l8_wd_34

// Type: Stable

// - Time: O(n log(n))
// - Space: O(n)
function sortArray(nums) {
  const n = nums.length;
  if (n < 2) return nums;

  sort(nums, new Array(n));

  return nums;
}

function sort(nums, temp, left = 0, right = nums.length - 1) {
  if (left >= right) return;

  const THRESHOLD = 12;

  if (right - left < THRESHOLD) {
    insertionSort(nums, left, right);

    return;
  }

  const mid = left + ((right - left) >> 1);

  sort(nums, temp, left, mid);
  sort(nums, temp, mid + 1, right);

  if (nums[mid] <= nums[mid + 1]) return;

  merge(nums, temp, left, mid, right);
}

function insertionSort(nums, left, right) {
  for (let i = left + 1; i <= right; i += 1) {
    const current = nums[i];
    if (nums[i - 1] <= current) continue;

    let j = i - 1;

    while (j >= left && nums[j] > current) {
      nums[j + 1] = nums[j];
      j -= 1;
    }

    nums[j + 1] = current;
  }

  return nums;
}

function merge(nums, temp, left, mid, right) {
  for (let i = left; i <= right; i += 1) {
    temp[i] = nums[i];
  }

  let i = left;
  let j = mid + 1;
  let k = left;

  while (i <= mid && j <= right) {
    if (temp[i] < temp[j]) {
      nums[k] = temp[i];
      i += 1;
    } else {
      nums[k] = temp[j];
      j += 1;
    }

    k += 1;
  }

  while (i <= mid) {
    nums[k] = temp[i];
    i += 1;
    k += 1;
  }

  while (j <= right) {
    nums[k] = temp[j];
    j += 1;
    k += 1;
  }
}
```

## [Merge Sort 'bottom-up'](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1769691872195 -->

```js
// Explanation:
// - CS50: https://youtu.be/Qs3l8_wd_34
// - Mary Elaine Califf: https://youtu.be/IN_ZOU-LK08 (Bottom-up)

// Type: Stable

// - Time: O(n log(n))
// - Space: O(n)
function sortArray(nums) {
  const n = nums.length;
  if (n < 2) return nums;

  const temp = new Array(n);

  for (let step = 1; step < n; step *= 2) {
    let left = 0;

    while (left < n) {
      const mid = Math.min(left + step - 1, n - 1);
      const right = Math.min(left + step * 2 - 1, n - 1);

      merge(nums, temp, left, mid, right);

      left = right + 1;
    }
  }

  return nums;
}

function merge(nums, temp, left, mid, right) {
  for (let i = left; i <= right; i += 1) {
    temp[i] = nums[i];
  }

  let i = left;
  let j = mid + 1;
  let k = left;

  while (i <= mid && j <= right) {
    if (temp[i] <= temp[j]) {
      nums[k] = temp[i];
      i += 1;
    } else {
      nums[k] = temp[j];
      j += 1;
    }

    k += 1;
  }

  while (i <= mid) {
    nums[k] = temp[i];
    i += 1;
    k += 1;
  }

  while (j <= right) {
    nums[k] = temp[j];
    j += 1;
    k += 1;
  }
}
```
