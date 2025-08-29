## [0/1 Knapsack 'one-row'](https://reimagined-orbit-7j4w5jq566hrv6j.github.dev/)

<!-- notecardId: 1756393181267 -->

```js
function zeroOneKnapsack(capacity, weights, values) {
  const n = weights.length;
  const dp = new Uint32Array(capacity + 1);

  for (let i = 0; i < n; i += 1) {
    for (let w = capacity; w >= weights[i]; w -= 1) {
      dp[w] = Math.max(dp[w], dp[w - weights[i]] + values[i]);
    }
  }

  return dp[capacity];
}
```

## [0/1 Knapsack](https://reimagined-orbit-7j4w5jq566hrv6j.github.dev/)

<!-- notecardId: 1756393181269 -->

```js
function zeroOneKnapsack(capacity, weights, values) {
  const n = weights.length;
  const dp = Array.from({ length: n + 1 }, () => new Uint32Array(capacity + 1));

  for (let i = 1; i <= n; i += 1) {
    for (let w = 0; w <= capacity; w += 1) {
      dp[i][w] = dp[i - 1][w];

      const weight = weights[i - 1];
      const value = values[i - 1];

      if (w >= weight) {
        dp[i][w] = Math.max(dp[i][w], dp[i - 1][w - weight] + value);
      }
    }
  }

  return dp[n][capacity];
}
```
