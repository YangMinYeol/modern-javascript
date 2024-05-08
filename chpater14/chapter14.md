## Proxy

> let proxy = new Proxy(target, handler)

- `target` - 감싸게 될 객체로, 함수를 포함한 모든 객체가 가능하다.
- `handler` - 동작을 가로채는 메서드인 `트랩`이 담긴 객체로, 여기서 프록시를 설정한다
  > `get`트랩은 `target`의 프로퍼티를 읽을 때, `set`트랩은 `target`의 프로퍼티를 쓸 때 활성화됨
- `handler`가 비어있으면 `Proxy`에 가해지는 작업은 `target`에 곧바로 전달된다.
- 프록시에 대한 다양한 메서드들은 아래에서 확인이 가능하다
  > https://ko.javascript.info/proxy

#### get

- 프로퍼티를 읽을때 작동한다.
- `target` - 동작을 전달할 객체로 `new Proxy`의 첫 번째 인자
- `property` - 프로퍼티 이름
- `receiver` - 타깃 프로퍼티가 getter라면 `receiver`는 getter가 호출될 때 `this`이다.

#### set

- 프로퍼티에 쓸때 작동한다.
- `target` - 동작을 전달할 객체로 `new Proxy`의 첫 번째 인자
- `propert` - 프로퍼티 이름
- `value` - 프로퍼티 값
- `receiver` - `get`트랩과 유사하게 동작하는 객체로, setter프로퍼티에만 관여한다.

## Eval

- 내장 함수`eval`을 사용하면 문자열 형태의 코드를 실핼할 수 있다
  > let result = eval(code);
- 현재는 문제가많아 사용되지 않으며 사용해야 할 경우가 있으면 다른 방법으로 유도한다.
- 전역 스코프에서 `eval`을 사용하지 말고, `window.eval(code)`를 이용하라.
- 외부 스코프에 있는 데이터가 필요하다면 `new Function`의 인수에 코드를 전달해 사용해라.

## 커링

- 커링은 `f(a, b, c)`처럼 단일 호출로 처리하는 함수를 `f(a)(b)(c)`와 같이 각각의 인수가 호출 가능한 프로세스로 호출된 후 병합되도록 변환하는 것이다.
- 커링은 함수를 호출하지 않는다. 단지 변환할 뿐이다.

```
function curry(f) { // 커링 변환을 하는 curry(f) 함수
  return function(a) {
    return function(b) {
      return f(a, b);
    };
  };
}
```

- 커링은 고정된 개수의 인수를 가지도록 요구한다. `...args`같은 나머지 매개변수를 사용하는 함수는 사용할 수 없다.

## BitInt

- 길이의 제약없이 정수를 다룰 수 있게 해주는 숫자형
- 정수 리터럴 끝에 `n`을 붙이거나 함수 `BigInt`를 호출하면 문자열이나 숫자를 가지고 `BigInt` 타입의 값을 만들 수 있다.
- `BigInt`형 값과 일반 숫자를 섞어서 사용할 수 없다.
- 비교 연산자 `<`,`>`sms `BigInt`와 일반 숫자 모두 사용할 수 있다.
