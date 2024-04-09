# 📘 Problem

- 배열(튜플) `T`를 받아 첫 원소의 타입을 반환하는 제네릭 `First<T>`를 구현하세요.

## 🔍 example

```ts
type arr1 = ["a", "b", "c"];
type arr2 = [3, 2, 1];

type head1 = First<arr1>; // expected to be 'a'
type head2 = First<arr2>; // expected to be 3
```

## 💭 Thinking

- 배열 T의 첫번째 원소 타입 반환하기
- 배열의 인덱스를 타입에서 어떻게 가리킬까?
- 이전 문제에서 배열의 인덱스를 `T[number]` 로 표현하였고, 인덱스에 해당하는 요소를 `key in T[number]` 로 가져옴
- 이번에는 객체 타입이 아니라 key/value 형태가 아님
- 의도 : 0번째 인덱스를 그대로 내보내 T[0] 자체가 리터럴 타입이 되도록 구현
- `Expect<Equal<First<[]>, never>>,` 케이스 통과 실패

## 😎 Try

```ts
type First<T extends any[]> = T[0];
```

## ✅ Answer

- 처음 풀었을 때 0번째 인덱스가 없는 경우 오류가 났는데, 타입에서도 삼항 연산자 사용
- 빈 배열을 extends 하여 any[] 타입에서 [] 리터럴 타입으로 변환할 수 있음
- `T['length'] 로 T의 length 프로퍼티를 체크할 수 있음

```ts
type First<T extends any[]> = T extends [] ? never : T[0];
type First<T extends any[]> = T["length"] extends 0 ? never : T[0];
```
