---
id: 268
title: If
lang: ja
level: easy
tags: utils
---

## 課題

Implement a utils `If` which accepts condition `C`, a truthy return type `T`,
and a falsy return type `F`. `C` is expected to be either `true` or `false`
while `T` and `F` can be any type.

条件 `C`、真の場合の返り値の型 `T`、偽の場合の返り値の型 `F` を受け取る `If` を実装してください。
`C` は `true` または `false` であることが期待されますが、`T` と `F` はどんな型でも構いません。

For example:

例:

```ts
type A = If<true, "a", "b">; // expected to be 'a'
type B = If<false, "a", "b">; // expected to be 'b'
```

## 解答

If you are not sure when to use
[conditional types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html)
in TypeScript, it is when you need to use an “if” statement on types. Exactly
what we tasked to do here.

TypeScript の Conditional 型を使用するタイミングは、型に対して "if" 文を使用する必要がある場合です。
ここで求められていることに

If the condition type evaluates to `true`, we need to take a “true” branch,
otherwise “false” branch:

条件を表わす型が `true` である場合、"true" ブランチに、そうでない場合は "false" ブランチに入ります:

```ts
type If<C, T, F> = C extends true ? T : F;
```

Going that way we will get a compilation error, because we are trying to assign
`C` to boolean type and not having a constraint that shows that. So let us fix
it by adding `extends boolean` to the type parameter `C`:

しかしこのままでは、`C` に割り当てられるのは boolean 型であることを示す制約がないため、エラーが発生します。
そのため、型変数 `C` に `extends boolean` を追加する必要があります:

```ts
type If<C extends boolean, T, F> = C extends true ? T : F;
```

## 参考

- [Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html)
