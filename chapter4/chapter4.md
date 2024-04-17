## 객체

- 몇가지 특수한 기능을 가진 연관 배열이다.
- `키(key) : 값(value)`쌍으로 구성된 프로퍼티
- 키느 문자열이나 심볼, 값은 모든 자료형이 허용
- 빈 객체를 만드는 방법은 두가지

```
let user = new Object(); // 객체 생성자 문법
let user = {}; // 객체 리터럴 문법
```

- `delete`연산자를 사용하면 프로퍼티를 삭제할 수 있습니다.

```
delete user.age;
```

- 여러 단어를 조합해 프로퍼티 이름을 만든 경우엔 프로퍼티 이름을 따옴표로 묶어줘야 한다.
- 읽을때는 대괄호 표기법을 사용 user["likes birds"]

```
let user = {
  name: "Minyeol",
  age: 28,
  "likes birds": true
}
```

#### 계산된 프로퍼티

- 객체 리터럴 안의 프로퍼티 키가 대괄호로 둘러싸여 있는 경우

```
let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");
let bag = {
  [fruit]: 5,
}
```

#### 객체 복사

- 새로운 객체를 만든 다음 기존 객체의 프로퍼티들을 순회해 원시 수준까지 프로퍼티를 복사

```
let user = {
  name: "Minyeol"
  age: 29
}

let clone = {};

for(let key in user){
  clone[key] = user[key];
}
```

- Object.assign을 사용

```
let clone = Object.assign({}, user);
```

#### 중첩 객체 복사

- 객체안에 객체가 있는경우 복사시 객체 참조 주소만 복사되기때문에 깊은 복사를 해야한다.
  > 자바스크립트 라이브러리 lodash를 사용하면 알고리즘을 직접 구현하지 않고도 깊은 복사를 처리할 수 있다.

#### 가비지 컬렉션

- 엔진이 자동으로 수행하며 개발자는 이를 억지로 실행하거나 막을 수 없다.
- 객체는 도달 가능한 상태일 때 메모리에 남는다.
- 참조된다고 해서 도달 가능한것은 아니다. 서로 연결된 객체들도 도달 불가능할 수 있다.

#### 메서드

- 객체 프로퍼티에 저장된 함수를 `메서드`라고 부른다.

#### this

- this값은 런타임에 결정된다.
- 화살표 함수는 자신만의 this를 가지지 않는다. 화살표 함수 안에서 this를 사용하면 외부에서 this를 가져온다.

#### 생성자 함수

- 함수 이름의 첫 글자는 대문자로 시작
- 반드시 `new` 연산자를 붙여 실행

#### 옵셔널 체이닝 `?.`

- 프로퍼티가 없는 중첩 객체를 에러없이 접근할 수 있다.
- `?.`은 평가 대상이 `undefined`나 `null`이면 평가를 멈추가 `undefined`를 반환한다.
- `?.()`

```
let user1 = {
  admin() {
    alert("관리자 계정입니다.");
  }
}

let user2 = {};

user1.admin?.(); // 관리자 계정입니다.
user2.admin?.();
```

- `?.[]`

```
let user1 = {
  firstName: "Violet"
};

let user2 = null; // user2는 권한이 없는 사용자라고 가정해봅시다.

let key = "firstName";

alert( user1?.[key] ); // Violet
alert( user2?.[key] ); // undefined
```

- delete와 조합해 사용도 가능하다

  > delete user?.name; // user가 존재하면 user.name을 삭제한다.

- `?.`은 읽기나 삭제하기에는 사용이 가능하다 쓰기에는 사용이 불가하다.

## 심볼형

- 심볼은 유일한 식별자를 만들고 싶을때 사용한다.
- Symbol()을 사용하면 심볼값을 만들 수 있다.
- 심볼형 키를 사용하면 프로퍼티가 우연히라도 사용되거나 덮어씌워 지는 걸 예방할 수 있다.
- 심볼을 만들때 심볼 이름이라 불리는 설명을 붙일 수도 있다. 디버깅시 유용하다.
  > let id = Symbol("id");
- 심볼은 for..in에서 배제된다.
- Object.assign은 키가 심볼인 프로퍼티를 배제하지않고 객체 내 모든 프로퍼티를 복사한다.

#### 전역 심볼

- 전역 심볼 레저스트리 안에 이는 심볼은 전역 심볼이라고 부른다.

```
// 전역 레지스트리에서 심볼을 읽습니다.
let id = Symbol.for("id"); // 심볼이 존재하지 않으면 새로운 심볼을 만듭니다.

// 동일한 이름을 이용해 심볼을 다시 읽습니다(좀 더 멀리 떨어진 코드에서도 가능합니다).
let idAgain = Symbol.for("id");

// 두 심볼은 같습니다.
alert( id === idAgain ); // true
```

- `Symbol.keyFor`을 사용하면 이름을 얻을수 있다.
- 전역 심볼이 아닌경우 사용이 불가하다.

```
// 이름을 이용해 심볼을 찾음
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// 심볼을 이용해 이름을 얻음
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id
```
