Factory for common properties of object union type:

```ts
type CommonProperties<T extends object> = {
  [K in keyof T]: T[K] extends T[keyof T] ? K : never
}[keyof T]
```

