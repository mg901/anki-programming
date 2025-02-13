## [Tuple to Union](https://github.com/type-challenges/type-challenges/blob/main/questions/00010-medium-tuple-to-union/README.md)

<!-- notecardId: 1739479077407 -->

```ts
type TupleToUnion<T extends unknown[]> = T[number];

// or
type TupleToUnion<T extends unknown[]> = T extends [infer Head, ...infer Tail]
  ? Head | TupleToUnion<Tail>
  : never;
```
