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

Use above to create fixed length array
```ts
type FixedSizeArray<N extends number, T> = N extends 0
  ? never[]
  : {
      [K in IntRange<0, N>]: T
    } & {
      length: N
    } & ReadonlyArray<T>
```
