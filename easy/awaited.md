# 📘 Problem

- Promise와 같은 타입에 감싸인 타입이 있을 때, 안에 감싸인 타입이 무엇인지 어떻게 알 수 있을까요?
- 예를 들어 `Promise<ExampleType>`이 있을 때, `ExampleType`을 어떻게 얻을 수 있을까요?

## 🔍 example

```ts
type ExampleType = Promise<string>;

type Result = MyAwaited<ExampleType>; // string
```

## 💭 Thinking

- Promise<T> 타입을 받아 T를 반환
- 의도 : Promise 타입이면 Promise로 감싸진 내부 타입을 반환하고 아니면 반환 X

## 😎 Try

```ts
type MyAwaited<T> = T extends Promise<any> ? any : never;
```

## ✅ Answer

- `Awaited<T>` : T로 들어오는 Promise 타입을 재귀적으로 돌아 안에 감싸진 타입 반환
- `PromiseLike<T>` : ArrayLike처럼 Promise보다 좀더 넓은 의미의 Promise. Promise가 아니라 then 메서드를 갖는 타입도 허용.
- PromiseLike<any>를 상속받지 않으면 `MyAwaited<number>` 과 같은 Promise 타입이 아닌 경우를 잡지 못함
- `infer` : 런타임에서 결정되는 타입 정의. 조건부 타입 extends절에서만 사용 가능. U 가 추론 가능한 타입이면 참, 아니면 거짓
- 타입스크립트는 “정적 타이핑 (정적 타입 검사 )”를 지원하는 “점진적 타이핑 ” 언어다.
  - “`점진적 타이핑(점진적 타입 검사)` 은 컴파일 타임에 타입 검사를 수행하면서 필요에 따라 타입 선언의 생략을 허용한다.”

```ts
type MyAwaited<T extends PromiseLike<any>> = Awaited<T>;

type MyAwaited<T extends PromiseLike<any>> = T extends PromiseLike<infer U>
  ? U extends PromiseLike<any>
    ? MyAwaited<U>
    : U
  : never;
```

### reference

- https://www.typescriptlang.org/docs/handbook/utility-types.html#awaitedtype
- https://velog.io/@from_numpy/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%EC%A0%90%EC%A7%84%EC%A0%81-%ED%83%80%EC%9D%B4%ED%95%91#%EC%A0%90%EC%A7%84%EC%A0%81-%ED%83%80%EC%9D%B4%ED%95%91
- https://velog.io/@from_numpy/TypeScript-infer
