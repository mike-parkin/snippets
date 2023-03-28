Factory for common properties of object union type:

```ts
type CommonProperties<T extends object> = {
  [K in keyof T]: T[K] extends T[keyof T] ? K : never
}[keyof T]
```
Factory for common values of object union type:
```ts
type CommonValues<T, K extends keyof T> = T[K] extends {
  [index: string]: infer R
}
  ? R
  : never
```

Type set range of integers
```ts
type Enumerate<
  N extends number,
  Acc extends number[] = []
> = Acc['length'] extends N
  ? Acc[number]
  : Enumerate<N, [...Acc, Acc['length']]>

type IntRange<F extends number, T extends number> = Exclude<
  Enumerate<T>,
  Enumerate<F>
>
```

Fixed length array
```ts
type FixedSizeArray<
  L extends number,
  T,
  Acc extends T[] = []
> = Acc['length'] extends L
  ? Acc
  : MaxSizeArray<L, T, [...Acc, T]>
```

Max length array (can be between 1 and the max lenght)
```ts
type MaxSizeArray<
  L extends number,
  T,
  Acc extends T[] = []
> = Acc['length'] extends 0
  ? MaxSizeArray<L, T, [T]>
  : Acc['length'] extends L
  ? Acc
  : MaxSizeArray<Acc['length'], T> | MaxSizeArray<L, T, [...Acc, T]>
```


