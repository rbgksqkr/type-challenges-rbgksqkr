# 📘 Problem

- 배열(튜플)을 받아, 각 원소의 값을 key/value로 갖는 오브젝트 타입을 반환하는 타입을 구현하세요.

## 🔍 example

```ts
const tuple = ["tesla", "model 3", "model X", "model Y"] as const;

type result = TupleToObject<typeof tuple>; // expected { 'tesla': 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
```

## 💭 Thinking

- 배열, 튜플, Symbol 등이 인자로 들어오면 각각의 값들을 key/value로 갖는 타입 만들기
- key, value 타입을 나타내는 것 -> `Record<객체의 key타입, 객체의 value타입>`
- 배열의 요소들의 타입을 가져오는 방법은 무엇일까?
- 의도 : 배열의 요소를 가져와 key값과 value값으로 설정한 Record 타입으로 설정

## 😎 Try

```ts
type TupleToObject<T extends readonly any[]> = Record<T, T>;
```

## ✅ Answer

- `PropertyKey` 는 타입스크립트에서 지원하는 global type -> string | number | symbol
- 배열의 인덱스를 `T[number]` 로 가져올 수 있고, 인덱스에 해당하는 요소를 `in T[number]` 로 가져올 수 있음
- 프로퍼티의 key 타입을 `[key in T[number]]`, value 타입을 key로 지정

```ts
type TupleToObject<T extends readonly PropertyKey[]> = {
  [key in T[number]]: key;
};
```

reference : https://www.typescriptlang.org/docs/handbook/2/mapped-types.html
