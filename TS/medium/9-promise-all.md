## [Promise All](https://github.com/type-challenges/type-challenges/blob/main/questions/00020-medium-promise-all/README.md)

<!-- notecardId: 1739479092107 -->

```ts
declare function PromiseAll<T extends readonly unknown[] | []>(
  values: T
): Promise<{
  -readonly [P in keyof T]: Awaited<T[P]>;
}>;

// or
declare function PromiseAll<T extends any[]>(
  values: readonly [...T]
): Promise<{
  [P in keyof T]: Awaited<T[P]>;
}>;
```
