# 📘 Problem

- `T`의 모든 프로퍼티를 읽기 전용(재할당 불가)으로 바꾸는 내장 제네릭 `Readonly<T>`를 이를 사용하지 않고 구현하세요.

## 🔍 example

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

## 💭 Thinking

- T의 모든 프로퍼티에 `readonly` 붙이기
- `readonly` type modifier 는 배열이나 tuple 리터럴 타입에만 허용된다.
- 의도 : T의 모든 키를 가져와 해당 타입에 readonly 를 붙인다.
- 테스트케이스에서 인자는 1개만 받으므로 K 가 아닌 keyof T를 사용한다.

## 😎 Try

```ts
type MyReadonly<T> = { readonly [key in keyof T]: T[key] };
```

## ✅ Answer

```ts
type MyReadonly<T> = {
  readonly [P in keyof T]: T[P];
};
```
