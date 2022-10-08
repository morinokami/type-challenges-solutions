---
id: 7
title: Readonly
lang: ja
level: easy
tags: built-in readonly object-keys
---

## Challenge

Implement the built-in `Readonly<T>` generic without using it.

Constructs a type with all properties of `T` set to `readonly`, meaning the
properties of the constructed type cannot be reassigned.

組み込みの `Readonly<T>` を使用せず、与えられた `T` のすべてのプロパティを `readonly` とするような型、すなわち、すべてのプロパティを再割り当て不能とするような型を実装してください。

例:

```ts
interface Todo {
  title: string;
  description: string;
}

const todo: MyReadonly<Todo> = {
  title: "Hey",
  description: "foobar",
};

todo.title = "Hello"; // Error: cannot reassign a readonly property
todo.description = "barFoo"; // Error: cannot reassign a readonly property
```

## 解答

We need to make all the properties in the object read-only. Therefore, we need
to iterate over all the properties and add a modifier to them.

オブジェクトのすべてのプロパティを読み取り専用とする必要があります。つまり、すべてのプロパティについて、修飾子を付加するように捜査する必要があります。

We are going to use the usual
[Mapped Type](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)
here, nothing serious. For each property in the type, we take its key and add a
`readonly` modifier to it:

ここでは [Mapped 型](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)を使用するだけであり、それほど難しくはありません。与えられた型の各プロパティについて、そのキーを取り出し、`readonly` 修飾子を付加します:

```ts
type MyReadonly<T> = { readonly [K in keyof T]: T[K] };
```

## 参考

- [Mapped Types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)
