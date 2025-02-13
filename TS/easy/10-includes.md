## [Includes](https://github.com/type-challenges/type-challenges/blob/main/questions/00898-easy-includes/README.md)

<!-- notecardId: 1739478074486 -->

```ts
type Includes<T extends readonly any[], U> = {
  [P in keyof T]: Equal<T[P], U>;
}[number] extends false
  ? false
  : true;

// or
type Includes<T extends readonly any[], U> = {
  [P in keyof T]: Equal<T[P], U>;
} extends Record<number, false>
  ? false
  : true;

// or
type Includes<T extends readonly any[], U> = T extends [
  infer Head,
  ...infer Tail
]
  ? Equal<Head, U> extends true
    ? true
    : Includes<Tail, U>
  : false;
```
