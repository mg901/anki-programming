## [Last of Array](https://github.com/type-challenges/type-challenges/blob/main/questions/00015-medium-last/README.md)

<!-- notecardId: 1739479084132 -->

```ts
type Last<T extends unknown[]> = [never, ...T][T["length"]];

// or
type Last<T extends unknown[]> = T extends [...infer _, infer L] ? L : never;

// or
type Last<T extends any[]> = T extends [infer Head, ...infer Tail]
  ? Tail extends []
    ? Head
    : Last<Tail>
  : never;
```
