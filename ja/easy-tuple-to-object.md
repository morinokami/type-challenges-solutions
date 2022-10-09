---
id: 11
title: Tuple to Object
lang: ja
level: easy
tags: tuple
---

## 課題

Given an array, transform to an object type and the key/value must in the given
array.

For example:

配列が与えられたとき、配列の各要素をキーと値とするオブジェクト型に変換してください。

例:

```ts
const tuple = ["tesla", "model 3", "model X", "model Y"] as const;

// expected { tesla: 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
const result: TupleToObject<typeof tuple>;
```

## 解答

We need to take all the values from the array and make it as keys and values in
our new object.

配列のすべての値を取り出し、新しいオブジェクトのキーと値とする必要があります。

It is easy to do with indexed types. We can get the values from an array by
using `T[number]` construct. With the help of mapped types, we can iterate over
those values in `T[number]` and return a new type where the key and value is the
type from `T[number]`:

これは Indexed Access 型を使用すると実装が簡単です。
`T[number]` により、配列から値を取り出すことができます。
そして Mapped 型 を用いて `T[number]` に含まれる値を走査し、`T[number]` の型をキーと値とする新しい型を返すことができます:

```ts
type TupleToObject<T extends readonly PropertyKey[]> = { [K in T[number]]: K };
```

## 参考

- [Mapped Types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)
- [Indexed Types](https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html)
