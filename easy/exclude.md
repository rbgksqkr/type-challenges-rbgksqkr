# 📘 Problem

- `T`에서 `U`에 할당할 수 있는 타입을 제외하는 내장 제네릭 `Exclude<T, U>`를 이를 사용하지 않고 구현하세요.

## 🔍 example

```ts
type Result = MyExclude<"a" | "b" | "c", "a">; // 'b' | 'c'
```

## 💭 Thinking

- union 타입(T)에서 특정 타입(U)을 제외한 타입 구현하기
- T의 요소를 가져오기 : 객체에서는 `[key keyof T]` 이런식으로 가져올 수 있는데 union 타입에서는 요소 하나씩 어떻게 가져옴?
- 의도 : T를 반환하는데 해당 요소가 U에 포함되면 반환 안하고, 포함 안되는 것만 반환
- 해당 요소를 어떻게 표현해야할까?

## 😎 Try

```ts
type MyExclude<T, U extends T> = keyof T extends keyof U ? never : keyof T;
```

## ✅ Answer

- 비슷하면서도 `extends`와 `keyof` 를 제대로 이해못한 듯
- keyof T 하면 요소 하나하나를 의미할 줄 알았는데 그냥 집합의 개념으로 받아들이는 게 맞는 듯
- `<U extends T>` 하면 U가 T를 다 갖고 있는 게 되버리는데 이상함. 의도는 T의 요소다를 표현하고 싶었음.
- keyof 는 `객체(object) 타입` 에서 쓰는 게 적절한 듯
- `T extends U` : T가 더 큰 범위라 어색할 수 있지만 T = 'a', U = 'a' 인 경우를 true로 가져가는 조건식
- 삼항 연산자를 쓰려면 조건식을 써야함. `T extends U ? never` -> `U가 T에 포함되는 경우 타입에 포함 안함`

```ts
type MyExclude<T, U> = T extends U ? never : T;
```
