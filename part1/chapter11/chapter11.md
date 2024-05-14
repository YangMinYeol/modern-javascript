## 콜백

- 콜백 함수는 전달인자로 다른 함수에 전달되는 함수이다.

## 프로미스

- `new Promise`에 전달되는 함수는 executor(실행자, 실행함수)라고 부릅니다.
  > `executor`는 `new Promise`가 만들어질 때 자동으로 실행된다.
- `resolve(value)` - 일이 성공적으로 끝난 경우 그 결과를 나타내는 `value`와 함께 호출
- `reject(error)` - 에러 발새시 에러 객체를 나타내는 `error`와 함께 호출
- `executor`와 프로미스 핸들러 코드 주위엔 보이지 않는 `try...catch`가 있다. 예외가 발생하면 암시적 `try... catch`에서 예외를 잡고 이를 reject처럼 다룬다.

#### promise 객체 내부 프로퍼티

- `state` - 처음엔 `pending(보류)`이었다 `resolve`가 호출되면 `fulfilled`, `reject`가 호출되면 `rejected`로 변한다.
- `result` - 처음엔 `undefined`이었다 `resolve(value)`가 호출되면 `value`로, `reject(error)`가 호출되면 `error`로 변한다.

## 프로미스 메서드

#### Promise.all

- 요소 전체가 프로미스인 배열을 받고 새로운 프로미스를 반환
- 배열 안 프로미스가 모두 처리되면 새로운 프로미스가 이행되고, 배열 안 프로미스의 결과를 담은 배열이 새로운 프로미스의 `result`가 된다.
- 전달되는 프로미스중 하나라도 거부되면, 에러와함께 모두 거부된다.

#### Promise.allSettled

- 모든 프로미스가 처리될 때까지 기다린다.
- 응답이 성공한 경우 - `{status:"fulfilled", value:result}`
- 에러가 발생한 경우 - `{status:"rejected", reason:error}`
- 여러 요청 중 하나가 실패해도 다른요청 결과가 필요한 경우 사용된다.

#### Promise.race

- 가장 먼저 처리되는 프로미스의 결과를 반환한다.

#### Promise.resolve / Promise.reject

- `async/await`문법이 생긴후로는 거의 사용하지 않는다.
- `Promise.resolve` - 주어진 값을 사용해 이행 상태의 프로미스를 만든다.
- `Promise.reject` - 주어진 에러를 사용해 거부 상태의 프로미스를 만든다.

## 마이크로태스크 큐

- 마이크로태스크 큐는 먼저 들어온 작업을 먼저 실행한다.
- 실행할 것이 아무것도 남아있지 않을 때만 마이크로태스크 큐에 있는 작업이 실행된다.

## async와 await

- `async/await`을 사용하면 `promise.then/catch`가 거의 필요없다. 하지만 가장 바깥 스코프에서 비동기 처리가 필요할때는 사용한다.

#### async

- `async`가 붙은 함수는 반드시 프로미스를 반환하고, 프로미스가 아닌 것은 프로미스로 감싸 반환한다.

#### await

- `async`함수 안에서만 동작한다.
- `await` 키워드를 만나면 프로미스가 처리될 때까지 기다린다.
