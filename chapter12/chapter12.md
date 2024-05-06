## 제너레이터

#### 제너레이터 함수

- 제너레이터를 만들려면 `제너레이터 함수`라 불리는 특별한 문법 구조, `function*`이 필요하다.

- 제너레이터 함수는 일반 함수와 동작 방식이 다르다. 제너레이터 함수를 호출하면 코드가 실행되지 않고, 실행을 처리하는 특별객체, `제너레이터 객체`가 반환된다.

```
function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}

// '제너레이터 함수'는 '제너레이터 객체'를 생성합니다.
let generator = generateSequence();
alert(generator); // [object Generator]
```

#### next()

- `next()`를 호출하면 가장 가까운 `yield <value>`문을 만날때까지 실행이 지속된다.(value를 생략할 수도 있는데, 이 경우엔 undefined가 된다.)
- `yield <value>`문을 만나면 실행이 멈추고 산출하고자 하는 값인 `value`가 바깥 코드에 반환된다.
- `value` - 산출값
- `done` - 함수 코드 실행이 끝났으면 `true`, 아니면 `false`

#### 제너레이터와 이터러블

- 제너레이터는 이터러블이다.
- `for..of` 반복문을 사용해 값을 얻을 수 있다.
  > `done: true`일 때 마지막 `value`를 무시한다. 그러므로 모든 값이 출력되길 원한다면 `yield`로 값을 반환한다.
- 전개 구문(...)같은 관련 기능도 사용 가능하다.

#### 제너레이터 컴포지션

- 제너레이터 안에 제너레이터를 임베딩할 수 있게 해주는 제너레이터의 특별 기능이다.
- 제너레이터의 특수 문법 `yield*`를 사용하면 제너레이터를 다른 제너레이터에 끼워 넣을 수 있다.

#### async 이터레이터

- `Symbol.iterator` 대신 `Symbol.asyncIterator`를 사용해야 한다.
- `next()`는 프로미스를 반환한다.
- 비동기 이터러블 객체를 대상으로 하는 반복 작업은 `for await (let item of iterable)`반복문을 사용해 처리한다.
