## [First of Array](https://github.com/type-challenges/type-challenges/blob/main/questions/00014-easy-first/README.md)

<!-- notecardId: 1739477918080 -->

```ts
type First<T extends unknown[]> = T extends [] ? never : T[0];

// or
type First<T extends unknown[]> = T[Extract<keyof T, "0">];

// or
type First<T extends unknown[]> = T["length"] extends 0 ? never : T[0];

// or
type First<T extends unknown[]> = T extends [infer Head, ...infer _]
  ? Head
  : never;
```
