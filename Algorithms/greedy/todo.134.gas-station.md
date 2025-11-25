## [134 Gas Station](https://leetcode.com/problems/gas-station/description/)

```js
function canCompleteCircuit(gas, cost) {
  let totalGas = 0;
  let totalCost = 0;
  let start = 0;
  let tank = 0;

  for (let i = 0; i < gas.length; i += 1) {
    totalGas += gas[i];
    totalCost += cost[i];
    tank += gas[i] - cost[i];

    if (tank < 0) {
      start = i + 1;
      tank = 0;
    }
  }

  return totalCost <= totalGas ? start : -1;
}
```
