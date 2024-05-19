# 📘 Problem

- 조건 `C`, 참일 때 반환하는 타입 `T`, 거짓일 때 반환하는 타입 `F`를 받는 타입 `If`를 구현하세요. `C`는 `true` 또는 `false`이고, `T`와 `F`는 아무 타입입니다.

## 🔍 example

```ts
  type A = If<true, 'a', 'b'>  // expected to be 'a'
  type B = If<false, 'a', 'b'> // expected to be 'b'
```

## 💭 Thinking

- 배열 T의 첫번째 원소 타입 반환하기
- C가 참이면 T 타입을 반환하고, 거짓이면 F 타입을 반환한다.
- C가 boolean 값이면 되는 것 아닌가? -> `C extends boolean`
- extends boolean이면 false여도 값이 true가 되니까 true를 extends 할까?

## 😎 Try
- 테스트 케이스는 둘다 통과했는데 에러 케이스를 통과하지 못한다.

```ts
type If<C, T, F> = C extends true ? T : F;
```

## ✅ Answer
- 왜 계산하는 곳에서 extends 할 생각만 했을까?
- 에러 케이스에서는 null 일 경우를 체크하고 있었는데 true이면서 null인 경우를 어떻게 체크하지?
- general에 boolean을 상속받아 입력 타입을 좁히고, extends true로 참을 표현할 수 있다.

```ts
type If<C extends boolean, T, F> = C extends true ? T : F
```
