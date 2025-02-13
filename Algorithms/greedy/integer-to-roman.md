## [Integer to Roman](https://bigfrontend.dev/problem/integer-to-roman)

<!-- notecardId: 1739476705484 -->

```js
const romanNumerals = [
  { value: 1000, symbol: "M" },
  { value: 900, symbol: "CM" },
  { value: 500, symbol: "D" },
  { value: 400, symbol: "CD" },
  { value: 100, symbol: "C" },
  { value: 90, symbol: "XC" },
  { value: 50, symbol: "L" },
  { value: 40, symbol: "XL" },
  { value: 10, symbol: "X" },
  { value: 9, symbol: "IX" },
  { value: 5, symbol: "V" },
  { value: 4, symbol: "IV" },
  { value: 1, symbol: "I" },
];

function integerToRoman(integer) {
  let result = "";

  for (const { value, symbol } of romanNumerals) {
    while (integer >= value) {
      result += symbol;
      integer -= value;
    }
  }

  return result;
}
```
