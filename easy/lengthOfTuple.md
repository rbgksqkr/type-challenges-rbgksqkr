# 📘 Problem

- 배열(튜플)을 받아 길이를 반환하는 제네릭 `Length<T>`를 구현하세요.

## 🔍 example

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

## 💭 Thinking

- T라는 배열(튜플)을 받아 길이를 반환해야함
- 저번 문제에서 T의 프로퍼티를 참조할 수 있었음
- 일단 length를 참조할 때 타입 오류가 안나려면 T가 배열임을 나타내야함
- 어떤 타입을 요소로 가질지 모르니 any[] 를 상속
- 테스트 케이스 오류로 readonly를 추가했는데 배열에 `as const` 가 붙으면 배열 자체가 readonly
- 의도 : T의 length 프로퍼티를 참조해 배열(튜플)의 길이를 반환

## 😎 Try

```ts
type Length<T extends readonly any[]> = T["length"];
```

## ✅ Answer

```ts
type Length<T extends readonly any[]> = T["length"];
```
