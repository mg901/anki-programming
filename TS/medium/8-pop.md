## [Pop](https://github.com/type-challenges/type-challenges/blob/main/questions/00016-medium-pop/README.md)

<!-- notecardId: 1739479087561 -->

```ts
type Pop<T extends unknown[]> = T extends [...infer Rest, infer _] ? Rest : [];
```
