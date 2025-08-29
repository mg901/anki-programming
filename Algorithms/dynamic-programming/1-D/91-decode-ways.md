## [91 Decode Ways](https://leetcode.com/problems/decode-ways/description/)

<!-- notecardId: 1756417681238 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/6aEyTjOwlJU

// Sub-pattern:
// - Fibonacci numbers

// Top-down
//
// Without memo:
// - Time:  O(2^n)
// - Space: O(n)
//
// With memo:
// - Time: O(n)
// - Space: O(n)
function numDecodings(s) {
  const n = s.length;
  const cache = new Int32Array(n).fill(-1);

  return dfs(0);

  function dfs(i) {
    if (i === n) return 1;
    if (s[i] === '0') return 0;
    if (cache[i] !== -1) return cache[i];

    let res = dfs(i + 1);

    if (i + 1 < n && (s[i] === '1' || (s[i] === '2' && s[i + 1] <= '6'))) {
      res += dfs(i + 2);
    }

    cache[i] = res;

    return res;
  }
}

// Bottom-up
// Approach:
// - Right-to-left traversal

// Complexity:
// - Time: O(n)
// - Space: O(n)
function numDecodings(s) {
  const n = s.length;
  const dp = new Uint32Array(n + 1);
  dp[n] = 1;

  for (let i = n - 1; i >= 0; i -= 1) {
    if (s[i] === '0') continue;

    dp[i] += dp[i + 1];
    if (i + 1 < n && (s[i] === '1' || (s[i] === '2' && s[i + 1] <= '6'))) {
      dp[i] += dp[i + 2];
    }
  }

  return dp[0];
}

// Approach:
// - Left-to-right traversal

// Complexity:
// - Time: O(n)
// - Space: O(n)
function numDecodings(s) {
  const n = s.length;
  const dp = new Uint32Array(n + 1);
  dp[0] = 1; // One way to decode an empty string: do nothing.
  dp[1] = s[0] !== '0' ? 1 : 0; // An any first character from 1 to 9.

  for (let i = 2; i <= n; i += 1) {
    const first = s[i - 2];
    const second = s[i - 1];

    if (second !== '0') {
      dp[i] += dp[i - 1];
    }

    if (first === '1' || (first === '2' && second <= '6')) {
      dp[i] += dp[i - 2];
    }
  }

  return dp[n];
}
```

## [91 Decode Ways 'space-optimized'](https://leetcode.com/problems/decode-ways/description/)

<!-- notecardId: 1756417681241 -->

```js
// Space Optimized
// - Time: O(n)
// - Space: O(1)
function numDecodings(s) {
  const n = s.length;

  let one = 1;
  let two = 0;

  for (let i = n - 1; i >= 0; i -= 1) {
    let current = 0;

    if (s[i] !== '0') {
      current += one;

      if (i + 1 < n && (s[i] === '1' || (s[i] === '2' && s[i + 1] <= '6'))) {
        current += two;
      }
    }

    two = one;
    one = current;
  }

  return one;
}
```
