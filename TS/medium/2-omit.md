## [Omit](https://github.com/type-challenges/type-challenges/blob/main/questions/00003-medium-omit/README.md)

<!-- notecardId: 1739479067183 -->

```ts
type MyOmit<T, K extends keyof T> = {
  [P in keyof T as P extends K ? never : P]: T[P];
};

// Or
type MyOmit<T, K extends keyof T> = {
  [P in keyof T as Exclude<P, K>]: T[P];
};

// Or like original Omit type
type MyOmit<T, K extends PropertyKey> = {
  [P in keyof T as P extends K ? never : P]: T[P];
};
```
