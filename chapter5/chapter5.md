## 숫자

- 숫자 옆에 `e`를 붙이고 0의 개수를 그 옆에 붙여주면 숫자를 줄일 수 있다.
  > let billion = 1e9; // 10억
- 작은 숫자를 표현할 때도 큰 숫자를 표현할때 처럼 `e`를 사용할 수 있다.
  > let ms = 1e-6; // 1에서 왼쪽으로 6번 소수점 이동

#### toString(base)

- .toString(base) 메서드는 base진법으로 num을 표현한 후 이를 문자형으로 변환해 반환한다.

```
let num = 255;

alert( num.toString(16) );  // ff
alert( num.toString(2) );   // 11111111
```

#### 점 두 개와 메서드 호출

- 123456..toString(36) 처럼 .두개를 입력하여 직접 호출 가능하다
  > . 한개를 입력할 경우 소수점으로 인식하여 사용 불가

## 문자열

- 자바스크립트에선 UTF-16을 사용해 문자열을 인코딩합니다.

#### slice(start, end)

- start부터 end까지 (end는 미포함)
- 음수 허용

#### substring(start, end)

- start와 end 사이
- 음수는 0으로 취급함

#### substr(start, length)

- start부터 length개의 글자
- 음수허용

## 배열

- push와 pop은 빠르지만 shift와 unshift는 느리다.
- `for..in` 반복문은 객체와 함께 사용할 때 최적화되어 있어서 배열에 사용하면 객체에 사용하는 것 대비 10~100배 정도 느리다.
  > 배열엔 절대 `for..in`을 쓰지마라.

#### splice

- splice는 삭제된 요소로 구성된 배열을 반환한다.
- splice메서드의 deleteCount를 0으로 설정하면 요소를 제거하지 않으면서 새로운 요소를 추가할 수 있다.
- 음수 인덱스도 사용할 수 있다.

#### reduce와 reduceRight

```
let value = arr.reduce(function(accumulator, item, index, array) {
  //...
}, [initial]);
```

- `accumulator` - 이전 함수 호출의 결과, `initial`은 함수 최초 호출 시 사용되는 초기값(옵션)
- `item` - 현재 배열 요소
- `index` - 요소의 위치
- `array` - 배열

```
let arr = [1, 2, 3, 4, 5];

let result = arr.reduce((sum, current) => sum + current, 0); // 15
```

- 초기값 생략시 배열의 첫번째 요소를 초기값으로 설정하고 두번째 요소부터 실행

## iterable 객체

- 이터러블 객체의 핵심은 `관심사의 분리`
- 이터레이터엔 메서드 Symbor.iterator가 반드시 구현되어 있어야 한다.
- 이터레이터엔 {done: Boolean, value: any}을 반환하는 next()가 반드시 구현되어 있어야 한다.
- `이터러블`은 Symbol.iterator가 구현된 객체
- `유사 배열`은 인덱스와 length 프로퍼티가 있어서 배열처럼 보이는 객체

#### Symbol.iterator

```
// 1. for..of 최초 호출 시, Symbol.iterator가 호출됩니다.
range[Symbol.iterator] = function() {

  // Symbol.iterator는 이터레이터 객체를 반환합니다.
  // 2. 이후 for..of는 반환된 이터레이터 객체만을 대상으로 동작하는데, 이때 다음 값도 정해집니다.
  return {
    current: this.from,
    last: this.to,

    // 3. for..of 반복문에 의해 반복마다 next()가 호출됩니다.
    next() {
      // 4. next()는 값을 객체 {done:.., value :...}형태로 반환해야 합니다.
      if (this.current <= this.last) {
        return { done: false, value: this.current++ };
      } else {
        return { done: true };
      }
    }
  };
};

for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
```

## 맵(Map)

- 맵은 키에 다양한 자료형을 허용한다.
- 맵은 객체와 달리 키를 문자형으로 변환하지 않는다.
- map.set을 호출할때마다 맵 자신이 반환된다. 이를 이용하면 map.set을 `체이닝`할 수 있다.
  > map.set('1', 'str1).set(1, 'num1');
- 맵은 삽입 순서를 기억한다.
- Object.entries - 객체를 맵으로 바꾼다.
- Object.fromEntries - 맵을 객체로 바꾼다.

## 셋(Set)

- 셋은 중복을 허용하지 않는 값을 모아놓은 컬렉션

## 위크맵(WeakMap)

- 위크맵의 키가 반드시 객체여야 한다.
- 위크맵은 반복작업과 `keys()`, `values()`, `entries()` 메서드를 지원하지 않는다.
- 부차적인 데이터를 저장할때 유용하다.
- 위크맵은 캐싱이 필요할 때 유용하다.

## 위크셋(WeakSet)

- 위크셋은 객체만 저장 가능하다.
- 셋 안의 객체는 도달 가능할 때만 메모리에서 유지된다.
- `size`, `keys()`같은 반복 작업관련 메서드는 사용할 수 없다.
- 부차적인 데이터를 저장할때 유용하다.

## 구조 분해 할당

- 할당하고자 하는 변수의 개수가 분해하고자 하는 배열의 길이보다 클 경우 undefined로 취급된다.
- `=`을 이용해 할당할 값이 없을 때 기본으로 할당해 줄 값인 `기본값`을 설정할 수 있다.
- 객체를 분해 할당할때 `콜론:`을 이용하면 변수에 저장이 가능하다.
- 매개변수가 많은 함수에서 사용할 때 유용하다.

```
let options = {
  title: "Menu",
  width: 100,
  height: 200
};

// { 객체 프로퍼티: 목표 변수 }
let {width: w, height: h, title} = options;
```

#### 중첩 구조 분해

- 객체나 배열이 다른 객체나 배열을 포함하는 경우, 좀 더 복잡한 패턴을 사용하면 중첩 배열이나 객체의 정보를 추출할 수 있다.

```
let options = {
  size: {
    width: 100,
    height: 200
  },
  items: ["Cake", "Donut"],
  extra: true
};

// 코드를 여러 줄에 걸쳐 작성해 의도하는 바를 명확히 드러냄
let {
  size: { // size는 여기,
    width,
    height
  },
  items: [item1, item2], // items는 여기에 할당함
  title = "Menu" // 분해하려는 객체에 title 프로퍼티가 없으므로 기본값을 사용함
} = options;
```

## Date

- Date객체엔 자동 고침이라는 기능이 있어 범위를 벗어난 값이 있는경우 값을 자동으로 수정한다.

#### 날짜 구성요소

- `getFullYear()` - 연도를 반환
  > getYear()은 두 자릿수 연도를 반환하는 경우가 있기때문에 사용하지 않는다.
- `getMonth()` - 월을 반환(0이상 11이하)
- `getDate()` - 일을 반환(1이상 31이하)
- `getHours()`, `getMinutes()`, `getSeconds()`, `getMilliseconds()` - 시, 분, 초, 밀리초 반환
- `getDay()` - 요일을 반환 (0이상 6이하)
  > 0은 일요일
- `getTime()` - 타임 스탬프를 반환
- `getTimezoneOffset()` - 현지 시간과 표준 시간 차이를 반환

## JSON

- 문자열은 큰따옴표로 감싸야 한다. JSON에선 작은따옴표나 백틱을 사용할 수 없다.
- 객체 프로퍼티 이름은 큰따옴표로 감싸야한다.
- JSON.stringify가 불가능한 프로퍼티
  1. 함수 프로퍼티(메서드)
  2. 심볼형 프로퍼티(키가 심볼인 프로퍼티)
  3. 값이 undefined인 프로퍼티
- 순환 참조가 있으면 원하는대로 객체를 문자열로 바꾸는게 불가능하다.
- JSON은 주석을 지원하지 않는다.

#### JSON.parse

- 문자열을 `Date`로 전환해줘야 할 경우

```
let schedule = `{
  "meetups": [
    {"title":"Conference","date":"2017-11-30T12:00:00.000Z"},
    {"title":"Birthday","date":"2017-04-18T12:00:00.000Z"}
  ]
}`;

schedule = JSON.parse(schedule, function(key, value) {
  if (key == 'date') return new Date(value);
  return value;
});

```
