## [91 Decode Ways](https://leetcode.com/problems/decode-ways/description/)

<!-- notecardId: 1754345834230 -->

```js
// Sub-pattern:
// - Fibonacci numbers

// Top-down
// - Time: O(n) or O(2^n) without memo
// - Space: O(n)
function numDecodings(s) {
  const n = s.length;
  const cache = new Int32Array(n).fill(-1);

  return dfs(0);

  function dfs(index) {
    if (index === s.length) return 1;
    if (s[index] === '0') return 0;
    if (cache[index] !== -1) return cache[index];

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
