## [91 Decode Ways](https://leetcode.com/problems/decode-ways/description/)

<!-- notecardId: 1751369763210 -->

```js
function numDecodings(str) {
  if (str.length === 0) return 0;

  const n = str.length;
  const dp = new Array(n + 1).fill(0);

  dp[0] = 1;
  dp[1] = str[0] === '0' ? 0 : 1;

  for (let i = 2; i <= n; i += 1) {
    const one = str[i - 1];
    const two = str[i - 2];

    if (one !== '0') {
      dp[i] += dp[i - 1];
    }

    if (two === '1' || (two === '2' && one < '7')) {
      dp[i] += dp[i - 2];
    }
  }

  return dp[n];
}
```
