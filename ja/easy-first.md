---
id: 14
title: First of Array
lang: ja
level: easy
tags: array
---

## 課題

Implement a generic `First<T>` that takes an Array `T` and returns it's first
element's type.

配列 `T` を取り、その最初の要素の型を返すような `First<T>` を実装してください。

For example:

例:

```ts
type arr1 = ["a", "b", "c"];
type arr2 = [3, 2, 1];

type head1 = First<arr1>; // expected to be 'a'
type head2 = First<arr2>; // expected to be 3
```

## 解答

The first thing that could come up is to use lookup types and just write `T[0]`:

最初に思いつくのは Lookup 型を使用して `T[0]` と書くことです:

```ts
type First<T extends any[]> = T[0];
```

But there is an edge case that we need to handle. If we pass an empty array,
`T[0]` will not work, because there is no element.

しかし、ここで考慮すべきエッジケースがあります。
空の配列を渡した場合、要素がないため `T[0]` は期待通り動作しないのです。

So that, before accessing the first element in the array, we need to check if
the array is empty. To do that, we can use
[conditional types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html)
in TypeScript.

そのため、配列の最初の要素にアクセスする前に、配列が空であるかどうかをチェックする必要があります。
これは TypeScript の [Conditional 型](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html) によって実現することができます。

The idea behind them is pretty straightforward. If we can assign the type to the
type of condition, it will go into “true” branch, otherwise it will take “false”
path.

Conditional 型の考え方はとてもシンプルです。
`extends` の左にある型を右側の型に割り当てることができる場合、"true" ブランチに入ります。
そうでない場合は "false" ブランチに入ります。

We are going to check, if the array is empty, we return nothing, otherwise we
return the first element of the array:

配列が空であるかどうかをチェックし、空である場合は何も返さず、その他の場合は配列の最初の要素を返すようにします:

```ts
type First<T extends any[]> = T extends [] ? never : T[0];
```

## 参考

- [Indexed Types](https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html)
- [Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html)
