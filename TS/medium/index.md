## [Last Index Of](https://github.com/type-challenges/type-challenges/blob/main/questions/05317-medium-lastindexof/README.md)

<!-- notecardId: 1738788069342 -->

```ts
type LastIndexOf<T extends unknown[], Target> = T extends [
  ...infer Rest,
  infer Last
]
  ? Equal<Last, Target> extends true
    ? Rest["length"]
    : LastIndexOf<Rest, Target>
  : -1;
```

## [Check Repeated Tuple](https://github.com/type-challenges/type-challenges/blob/main/questions/27958-medium-checkrepeatedtuple/README.md)

<!-- notecardId: 1738788069363 -->

```ts
type Includes<T extends unknown[], U> = T extends [infer Head, ...infer Tail]
  ? Equal<Head, U> extends true
    ? true
    : Includes<Tail, U>
  : false;

type CheckRepeatedTuple<T extends unknown[]> = T extends [
  infer Head,
  ...infer Tail
]
  ? Includes<Tail, Head> extends false
    ? CheckRepeatedTuple<Tail>
    : true
  : false;
```

## [Deep Omit](https://github.com/type-challenges/type-challenges/blob/main/questions/29785-medium-deep-omit/README.md)

<!-- notecardId: 1738788069366 -->

```ts
type DeepOmit<
  T,
  Path extends string
> = Path extends `${infer Head}.${infer Tail}`
  ? {
      [P in keyof T]: Head extends P ? DeepOmit<T[P], Tail> : T[P];
    }
  : Omit<T, Path>;

// or
type DeepOmit<
  T,
  Path extends string
> = Path extends `${infer Head}.${infer Tail}`
  ? {
      [P in keyof T]: Head extends P ? DeepOmit<T[P], Tail> : T[P];
    }
  : {
      [P in keyof T as P extends Path ? never : P]: T[P];
    };
```

## [Greater Than](https://github.com/type-challenges/type-challenges/blob/main/questions/04425-medium-greater-than/README.md)

<!-- notecardId: 1738788069368 -->

```ts
type ParseInt<T> = T extends `${infer X extends number}` ? X : never;

type RemoveLeadingZeros<T extends string> = T extends "0"
  ? T
  : T extends `${0}${infer Rest}`
  ? RemoveLeadingZeros<Rest>
  : T;

type InnerMinusOne<T extends string> =
  T extends `${infer X extends number}${infer Y}`
    ? X extends 0
      ? `9${InnerMinusOne<Y>}`
      : `${[-1, 0, 1, 2, 3, 4, 5, 6, 7, 8][X]}${Y}`
    : "";

type Reverse<T extends string> = T extends `${infer X}${infer Y}`
  ? `${Reverse<Y>}${X}`
  : "";

type MinusOne<T extends number> = ParseInt<
  RemoveLeadingZeros<Reverse<InnerMinusOne<Reverse<`${T}`>>>>
>;

type InnerGreaterThan<T extends number, U extends number> = T extends U
  ? true
  : T extends 0
  ? false
  : InnerGreaterThan<MinusOne<T>, U>;

type GreaterThan<T extends number, U extends number> = T extends U
  ? false
  : U extends 0
  ? true
  : InnerGreaterThan<T, U>;
```

## [Trunk](https://github.com/type-challenges/type-challenges/blob/main/questions/05140-medium-trunc/README.md)

<!-- notecardId: 1738788069370 -->

```ts
type Prefix = "" | "-";

type Trunc<
  T extends string | number,
  S = `${T}`
> = S extends `${infer R}.${string}` ? (R extends Prefix ? `${R}0` : R) : S;
```

## [Replace First](https://github.com/type-challenges/type-challenges/blob/main/questions/25170-medium-replace-first/README.md)

<!-- notecardId: 1738788069371 -->

```ts
type ReplaceFirst<
  T extends readonly unknown[],
  Target,
  Replacement
> = T extends [infer Head, ...infer Tail]
  ? Head extends Target
    ? [Replacement, ...Tail]
    : [Head, ...ReplaceFirst<Tail, Target, Replacement>]
  : T;

type A = ReplaceFirst<[true, true, true], true, false>;

// becomes
type A = [false, true, true];
```
