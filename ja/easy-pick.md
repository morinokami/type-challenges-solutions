---
id: 4
title: Pick
lang: ja
level: easy
tags: union built-in
---

## 課題

Implement the built-in `Pick<T, K>` generic without using it.

Constructs a type by picking the set of properties `K` from `T`.

組み込みの `Pick<T, K>` を使用せず、`T` から `K` のプロパティを抽出する型を実装してください。

例:

```ts
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type TodoPreview = MyPick<Todo, "title" | "completed">;

const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
};
```

## 解答

For this challenge to solve, we need to use Lookup Types and Mapped Types.

この課題を解くためには、Lookup 型と Mapped 型を使う必要があります。

Lookup Types allow for us to extract a type from another type by its name. Kind
of getting a value from an object by using its key.

Lookup 型により、ある型から別の型を名前を用いて抽出することができます。あるオブジェクトからそのキーにより値を取得することと似ています。

Mapped Types allow for us to transform each property in a type into a new type.

Mapped 型により、ある型に含まれるプロパティを新しい型へと変換することができます。

You can read more about them and understand what they are doing on TypeScript
website:
[lookup types](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-1.html#keyof-and-lookup-types)
and
[mapped types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html).

TypeScript のウェブサイト上で [Lookup 型](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-1.html#keyof-and-lookup-types)と [Mapped 型](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)に関する説明を読み、その挙動について理解することができます。

Now, knowing that there are lookup types and mapped types in TypeScript. How to
implement the required type?

以上で TypeScript には Lookup 型と Mapped 型が存在することがわかりました。では、要求された型をどのように実装すればいいでしょうか?

We need to take everything from the union `K`, iterate over it, and return a new
type that will consist only of those keys. Exactly what mapped types are doing.

ユニオン `K` からすべてのプロパティを抜き出し、各値について走査し、そしてそれらのみをキーとする新たな型を返す必要があります。これはまさしく Mapped 型の挙動と一致します。

The type of values itself are going to be without change. Although, we need to
take its type from the original type and that is where lookup type is useful:

値の型自体は変更する必要はありません。与えられた型から型情報を抜き出さなければなりませんが、それには Lookup 型を使うことができます:

```ts
type MyPick<T, K extends keyof T> = { [P in K]: T[P] };
```

We are saying “get everything from `K`, name it as `P` and make it as a new key
in our new object with a value type taken from the input type”. It's hard to
grasp at first, so if you didn’t understand something, try to read the info
again and wrap it in your head step by step.

ここで表現していることは、「`K` からすべてのプロパティを抜き出し、各値の名前を `P` とした上で、新しいオブジェクトのキーを `P`、それに対応する型を入力された型 `T` から得られた得られたものとする」ということです。最初は理解することが難しいかもしれません。もし何かわからないことがあれば、もう一度説明を読み直し、順を追って理解していってください。

## 参考

- [Lookup Types](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-1.html#keyof-and-lookup-types)
- [Mapped Types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)
- [Indexed Types](https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html)
