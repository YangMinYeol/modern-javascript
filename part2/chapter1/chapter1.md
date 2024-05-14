## 문서

#### DOM

- 문서 객체 모델(Document Object Model)은 웹페이지 내의 모든 콘텐츠를 객체로 나타낸다.

#### BOM

- 브라우저 객체 모델(Browser Object Model)은 문서 이외에 모든 것을 제어하기 위한 브라우저가 제공하는 추가 객체를 나타낸다.

#### 명세서

- DOM 명세서

  > https://dom.spec.whatwg.org

- CSSOM 명세서

  > https://www.w3.org/TR/cssom-1/

- HTML 명세서
  > https://html.spec.whatwg.org

## DOM 트리

- 태그는 요소 노드가 되고 트리 구조를 형성한다.
- 문자는 텍스트 노드가 된다.
- HTML내의 모든 것은 DOM을 구성한다. (주석 포함)

## DOM에서 노드 검색 메서드

- `querySelector`
- `querySelectorAll`
- `getElementById`
- `getElementsByName`
- `getElementsByTagName`
- `getElementsByClassName`

#### 속성과 프로퍼티

- `속성` - HTML안에 쓰임
- `프로퍼티` - DOM 객체 안에 쓰임
- 대부분의 상황에서 속성보다는 프로퍼티를 사용하는 경우가 더 많다.
- 비표준 속성이 필요한 경우 `dataset(data-*)`을 사용하는게 좋다.

#### insertAdjacentHTML(where, html)

- `where`값에 따라 특정 위치에 HTML을 삽입함
- `beforebegin` - 바로 앞에 html을 삽입
- `afterbegin` - 첫 번째 자식 요소 바로 앞에 html을 삽입
- `beforeend` - 마지막 자식 요소 바로 다음에 html을 삽입
- `afterend` - 바로 다음에 html을 삽입
- 문자열이나 요소 삽입에 쓰이는 유사 메서드 elem.insertAdjacentText와 elem.insertAdjacentElement도 있는데, 잘 쓰이지는 않는다.

#### 기하 프로퍼티

- 기하 프로퍼티를 그림으로 나타낸 화면
  > https://ko.javascript.info/size-and-scroll
