## [91 Decode Ways](https://leetcode.com/problems/decode-ways/description/)

<!-- notecardId: 1753267019068 -->

```js
// Sub-pattern: Fibonacci numbers
// Top-down
function numDecodings(s) {
  if (s.length === 0) return 0;

  const cache = [];

  return dfs(0);

  function dfs(index) {
    if (index === s.length) return 1;
    if (s[index] === '0') return 0;
    if (cache[index] !== undefined) return cache[index];

    let res = dfs(index + 1);

    if (
      index + 1 < s.length &&
      (s[index] === '1' || (s[index] === '2' && s[index + 1] <= '6'))
    ) {
      res += dfs(index + 2);
    }

    cache[index] = res;

    return res;
  }
}

// Bottom-up
function numDecodings(str) {
  const n = s.length;
  if (n === 0) return 0;

  const dp = new Array(n + 1).fill(0);
  dp[0] = 1; // an empty string (base case)
  dp[1] = s[0] === '0' ? 0 : 1; // the first string

  for (let i = 2; i <= n; i += 1) {
    const first = s[i - 1];
    const second = s[i - 2];

    if (first !== '0') {
      dp[i] += dp[i - 1];
    }

    if (second === '1' || (second === '2' && first <= '6')) {
      dp[i] += dp[i - 2];
    }
  }

  return dp[n];
}
```
