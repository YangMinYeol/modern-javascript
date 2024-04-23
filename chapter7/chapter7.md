## 프로퍼티 플래그

- 객체 프로퍼티는 값과 함께 플래그(flag)라 불리는 특별한 속성 세 가지를 갖는다
- `writable` - `true`이면 값을 수정할 수있다. 그렇지 않다면 읽기만 가능
- `enumerable` - `true`이면 반복문을 사용해 나열할 수 있다. 그렇지 않다면 반복문을 사용해 나열할 수 없다.
- `configurable` - `true`이면 프로퍼티 삭제나 플래그 수정이 가능하다. 그렇지 않다면 프로퍼티 삭제와 플래그 수정이 불가능하다.
- `Object.getOwnPropertyDescriptor`메서드를 사용하면 특정 프로퍼티에 대한 정보를 얻을 수 있다.
  > let descriptor = Object.getOwnPropertyDescriptor(obj, propertyName);
- `Object.defineProperty`를 사용하면 플래그를 변경할 수 있다.
  > Object.defineProperty(obj, propertyName, descriptor)
- `Object.preventExtensions(obj)` - 객체에 새로운 프로퍼티를 추가할 수 없다.
- `Object.seal(obj)` - 새로운 프로퍼티 추가나 기존 프로퍼티 삭제를 막아준다. 프로퍼티 전체에 `configurable: false`를 설정하는것과 동일한 효과
- `Object.freeze(obj)` - 새로운 프로퍼티 추가나 기존 프로퍼티 삭제, 수정을 막아준다. 프로퍼티 전체에 `configurable: false`, `writable: false`를 설정하는 것과 동일한 효과입니다.
- `Object.isExtensible(obj)` - 새로운 프로퍼티를 추가하는 게 불가능한 경우 `false`를, 그렇지 않은 경우 `true`를 반환합니다.
- `Object.isSealed(obj)` - 프로퍼티 추가, 삭제가 불가능하고 모든 프로퍼티가 `configurable: false`이면 `true`를 반환합니다.
- `Object.isFrozen(obj)` - 프로퍼티 추가, 삭제, 변경이 불가능하고 모든 프로퍼티가 `configurable: false, writable: false`이면 `true`를 반환합니다.

## 프로퍼티 getter와 setter

- `데이터 프로퍼티` - 데이터를 조작하는 프로퍼티
- `접근자 프로퍼티` - 값을 `get`하고 설정`set`하는 역할을 담당한다. 외부코드에서는 함수가 아닌 일반적인 프로퍼티처럼 보인다.

#### getter와 setter

```
let obj = {
  get propName() {
    // getter, obj.propName을 실행할 때 실행되는 코드
  },

  set propName(value) {
    // setter, obj.propName = value를 실행할 때 실행되는 코드
  }
};
```

#### 접근자 프로퍼티

- `value`와 `writable`이 없는 대신에 `get`과 `set`이 있다.
- `get` – 인수가 없는 함수로, 프로퍼티를 읽을 때 동작
- `set` – 인수가 하나인 함수로, 프로퍼티에 값을 쓸 때 호출
- `enumerable` – 데이터 프로퍼티와 동일
- `configurable` – 데이터 프로퍼티와 동일
