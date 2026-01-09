## [Tuple to Object](https://github.com/type-challenges/type-challenges/blob/main/questions/00011-easy-tuple-to-object/README.md)

```ts
type TupleToObject<T extends readonly PropertyKey[]> = {
  [P in T[number]]: P;
};
```
