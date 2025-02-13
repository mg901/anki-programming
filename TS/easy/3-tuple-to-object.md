## [Tuple to Object](https://github.com/type-challenges/type-challenges/blob/main/questions/00011-easy-tuple-to-object/README.md)

<!-- notecardId: 1739477913338 -->

```ts
type TupleToObject<T extends readonly ProperyKey[]> = {
  [P in T[number]]: P;
};
```
