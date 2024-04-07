# 📘 Problem

- `T`에서 `K` 프로퍼티만 선택해 새로운 오브젝트 타입을 만드는 내장 제네릭 `Pick<T, K>`을 이를 사용하지 않고 구현하세요.

## 🔍 example

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

## 💭 Thinking

- T 인터페이스의 key 타입과 value 타입을 가져와야함
- 거기서 K와 맞는 타입을 가져오기
- `keyof T` : T 인터페이스의 key 타입 집합
- 해당 키값의 value 타입은 어떻게?
- 의도 : T 인터페이스의 key 타입들을 U가 갖고, U의 value 타입을 T 인터페이스에서 가져옴

## 😎 Try

```ts
type MyPick<T, K> = {[U keyof T] : T['U']};
```

## ✅ Answer

```ts
type MyPick<T, K extends keyof T> = { [key in K]: T[key] };
```
