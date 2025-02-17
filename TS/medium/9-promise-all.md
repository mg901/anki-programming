## [Promise All](https://github.com/type-challenges/type-challenges/blob/main/questions/00020-medium-promise-all/README.md)

<!-- notecardId: 1739798763193 -->

```ts
declare function PromiseAll<T extends unknown[] | []>(
  values: T
): Promise<{
  -readonly [P in keyof T]: Awaited<T[P]>;
}>;

// or
declare function PromiseAll<T extends unknown[]>(
  values: readonly [...T]
): Promise<{
  [P in keyof T]: Awaited<T[P]>;
}>;
```
