## [Concat](https://github.com/type-challenges/type-challenges/blob/main/questions/00533-easy-concat/README.md)

<!-- notecardId: 1739477936022 -->

```ts
type Tuple = readonly unknown[];

type Concat<T extends Tuple, U extends Tuple> = [...T, ...U];
```
