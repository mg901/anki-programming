## [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/description/)

<!-- notecardId: 1763217613800 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/3jvWodd7ht0

// Complexity:
// - Time: O(n * n^2)
// - Space: O(n * n^2)
function partition(s) {
  const n = s.length;
  const result = [];
  backtrack(0, []);

  return result;

  function backtrack(start, path) {
    if (start === n) {
      result.push([...path]);

      return;
    }

    for (let end = start + 1; end <= n; end += 1) {
      const substr = s.slice(start, end);

      if (isPalindrome(substr)) {
        path.push(substr);
        backtrack(end, path);
        path.pop();
      }
    }
  }
}

function isPalindrome(str) {
  const n = str.length;
  if (n === 1) return true;

  let left = 0;
  let right = n - 1;

  while (left < right) {
    if (str[left] !== str[right]) return false;

    left += 1;
    right -= 1;
  }

  return true;
}
```
