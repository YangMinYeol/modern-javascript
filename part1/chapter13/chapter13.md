## 모듈

- `export` - 지시자를 변수나 함수 앞에 붙이면 외부 모듈에서 해당 변수나 함수에 접근할 수 있다.
- `import` - 지시자를 사용하면 외부 모듈의 기능을 가져올 수 있다.
- 동일한 모듈이 여러 곳에서 사용되더라도 모듈은 최초 호출 시 단 한번만 실행된다.
- 모듈 최상위 레벨의 `this`는 `undefined`이다.
- HTML문서가 완전히 만들어진 이후에 실행된다.
- 지연 실행된다.
- 인라인 모듈 스크립트도 비동거 처리할 수 있다.
- 외부 오리진에서 스크립트를 불러오려면 CORS헤더가 있어야 한다.
- 중복된 외부 스크립트는 무시한다
- 항상 엄격모드로 실행된다.

#### export

- 선언부와 떨어진 곳에 export를 붙일 수 있다.

```
// 📁 say.js
function sayHi(user) {
  alert(`Hello, ${user}!`);
}

function sayBye(user) {
  alert(`Bye, ${user}!`);
}

export {sayHi, sayBye}; // 두 함수를 내보냄
```

- `as`를 사용하면 이름을 바꿔서 내보낼 수 있다.

#### import

- 모듈을 가져오고 싶을때 목록을 만들어 `import {...}`안에 적어주면 된다.
  > import {sayHi, sayBye} from './say.js';
- 가져올 것이 많으면 `import * as <obj>`처럼 객체 형태로 원하는것을 가져올 수 있다.
  > import \* as say from './say.js';
- `as`를 사용하면 이름을 바꿔서 모듈을 가져올 수 있다.

#### export default

- 해당 모듈엔 객체가 하나만 있다라는 사실을 명확히 나타낼 수 있다.

#### 모듈 다시 내보내기

- `export ... from ...` 문법을 사용하면 개체를 즉시 다시 내보내기 할 수 있다.

```
export {sayHi} from './say.js'; // sayHi를 다시 내보내기 함

export {default as User} from './user.js'; // default export를 다시 내보내기 함
```

#### import() 표현식

- 동적으로 모듈을 가져올 수 있다.

```
// 📁 say.js
export function hi() {
  alert(`안녕하세요.`);
}

export function bye() {
  alert(`안녕히 가세요.`);
}

let {hi, bye} = await import('./say.js');

hi();
bye();
```
