---
id: 18
title: Length of Tuple
lang: ja
level: easy
tags: tuple
---

## 課題

For given a tuple, you need create a generic `Length`, pick the length of the
tuple.

タプルが与えられたとき、そのタプルの長さを返すような `Length` を実装してください。

例:

```ts
type tesla = ["tesla", "model 3", "model X", "model Y"];
type spaceX = [
  "FALCON 9",
  "FALCON HEAVY",
  "DRAGON",
  "STARSHIP",
  "HUMAN SPACEFLIGHT"
];

type teslaLength = Length<tesla>; // expected 4
type spaceXLength = Length<spaceX>; // expected 5
```

## 解答

We know that we can use property `length` to access the length of the array in
JavaScript. We can do the same in types as well:

JavaScript では `length` プロパティを使用して配列の長さにアクセスできることをご存知でしょう。
型においても同様のことが可能です:

```ts
type Length<T extends any> = T["length"];
```

But going that way we will get the compilation error “Type 'length' cannot be
used to index type 'T'.”. So we need to give a hint to TypeScript and tell that
our input type parameter has this property:

しかし、この方法では「Type 'length' cannot be used to index type 'T'」というコンパイルエラーが発生してしまいます。
そのため、型変数への入力がこのプロパティをもっていることを TypeScript に伝える必要があります:

```ts
type Length<T extends { length: number }> = T["length"];
```

## 参考

- [Indexed Types](https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html)
