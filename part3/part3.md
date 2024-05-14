## 텍스트 디코더

- 내장 객체, `TextDecoder`는 주어진 버퍼와 인코딩으로 값을 실제 자바 스크립트 문자열로 읽을 수 있게 해준다.
  > let decoder = new TextDecoder([label], [options]);
- `label` - 기본적인 인코딩 방식은 `utf-8`이지만 `big5`, `windows-1251` 및 다른 인코딩 방식도 지원된다.
- `options` - 선택 항목
  - `fatal` - 불린값, `true`인 경우, 잘못된 글자를 대상으로 예외를 던진다. `false(기본값)`인 경우, 글자를 `\uFFFD`로 대체한다.
  - `ignoreBOM` - 불린 값이 `true`인 경우 사용되지 않는 바이트 순서 표식을 무시한다.

> let str = decoder.decode([input], [options]);

- `input` - 디코딩할 `BufferSource`를 입력한다
- `options` - 선택 항목
  - `stream` - 많은 양의 데이터를 받아들여 `decoder`를 반복적으로 호출할 때도 decoding이 반복적으로 실행된다. 이런 경우 멀티 바이트 문자가 많은 데이터로 분할될 수 있습니다. 이 옵션은 데이터 분할을 방지하기 위해 TextDecoder에 “unfinished” 문자를 입력시키고 다음 데이터가 오면 디코딩하도록 지시한다.

## 텍스트 인코더

- `TextEncoder`는 문자열을 바이트로 변환한다.
  > let encoder = new TextEncoder();
- `encode(str)` – `Uint8Array`에 문자열을 반환한다.
- `encodeInto(str, destination)` – `Uint8Array` 구조 형태로 문자열 str를 destination에 인코딩한다.

## fetch

> let promise = fetch(url, [options])

- `url` - 접근하고자 하는 URL
- `options` - 선택 항목, 메소드나 헤더 등을 지정할 수 있다.
- `options`에 아무것도 넘기지 않으면 요청은 `GET`메서드로 진행되어 `url`로부터 콘텐츠가 다운로드 된다.
- `fetch()`를 호출하면 프로미스가 반환된다.
- HTTP상태는 응답 프로퍼티를 사용해 확인할 수 있다.
  - `status` - HTTP 상태 코드 (예: 200)
  - `ok` - 불린 값, HTTP 상태 코드가 200과 299 사이일 경우 true
- `response`에는 프로미스를 기반으로 하는 다양한 메서드가 있다
  - `response.text()` - 응답을 읽고 텍스트를 반환
  - `response.json()` - 응답을 JSON 형태로 파싱
  - `response.formData()` - 응답을 `FormData` 객체 형태로 반환
  - `response.blob()` - 응답을 Blob 형태로 반환
  - `response.arrayBuffer()` - 응답을 ArrayBuffer형태로 반환
  - `response.body()` - 응답 본문을 청크? 단위로 읽을 수 있다.
- 응답 헤더는 `response.headers`에 맵과 유사한 형태로 저장된다.
  > 맵은 아니지만 맵과 유사한 메서드를 지원한다.
- `headers`옵션을 사용하면 `fetch`에 요청 헤더를 설정할 수 있다. `headers`엔 다양한 헤더 정보가 담긴 객체를 넘기면 된다.

##### POST 요청

- `GET`이외의 요청을 보내려면 추가 옵션을 사용
- `method` - HTTP 메서드(예: POST)
- `body` - 요청 본문으로 다음 항목 중 하나이어야 한다.
  - 문자열(예:JSON 문자열)
  - `FormData`객체 - `form/multipart` 형태로 데이터를 전송하기 위해 쓰인다.
  - `Blob` 또는 `BufferSource` - 바이너리 데이터 전송을 위해 쓰인다.
  - `URLSearchParams` - 데이터를 `x-www-form-urlencoded` 형태로 보내기 위해 쓰이는데, 요즘엔 잘 사용하지 않는다.
- `POST`요청을 보낼 때 주의할 점은 요청 본문이 문자열일 때 `Content-Type`헤더가 `text/plain;charset=URF-8`로 기본 설정된다.

## CORS

- 도메인이나 서브도메인, 프로토콜, 포트가 다른 곳에 요청을 보내는 것을 Cross-Origin Request라고 하며 크로스 오리진 요청을 보내려면 리모트 오리진에서 전송받은 특벽한 헤더가 필요하다. 이러한 정책을 CORS라고 부른다.
- 안전한 요청과 안전하지 않은 요청에 대해서는 필요시에 찾아보자.
  > https://ko.javascript.info/fetch-crossorigin

## 웹 소켓

- 서버와 브라우저 간 연결을 유지한 상태로 데이터를 교환할 수 있다.
- 데이터는 `패킷`형태로 전달되며, 전송은 커넥션 중단과 추가 HTTP요청 없이 양방향으로 이루어진다.
- 웹 소켓 커넥션을 만들려면 `new WebSocker`을 호출하고, 이때 `ws`라는 특수 프로토콜을 사용한다.
  > let socket = new WebSocket("ws://javascript.info");
- ws말고 wss://라는 프로토콜도 있는데, 두 프로토콜의 관계는 HTTP와 HTTPS의 관계와 유사합니다.

##### 웹 소켓 메서드

- `open` - 커넥션이 제대로 만들어졌을 때 발생
- `message` - 데이터를 수신하였을 때 발생
- `error` - 에러가 생겼을 때 발생
- `close` - 커넥션이 종료되었을 때 발생
- 커넥션이 만들어진 상태에서 무언가를 보내고 싶으면 `socket.send(data)`를 사용하면 된다.

##### 웹 소켓 핸드셰이크

- 커넥션이 유지되는 동안, 브라우저는(헤더를 사용해) 서버에 웹 소켓 지원 여부를 묻고 이에 서버가 응답하면 서버-브라우저간 통신은 HTTP가 아닌 웹 소켓 프로토콜을 사용해 진행된다.

##### 데이터 전송

- 웹 소켓 통신은 `프레임`이라 불리는 데이터 조각을 사용해 이루어진다. 프레임은 서버와 클라이언트 양측 모두에서 보낼 수 있는데, 프레임 내 담긴 데이터 종류에 따라 다음과 같이 분류 가능하다
  - `텍스트 프레임(text frame)` – 텍스트 데이터가 담긴 프레임
  - `이진 데이터 프레임(binary data frame)` – 이진 데이터가 담긴 프레임
  - `핑·퐁 프레임(ping/pong frame)` – 커넥션이 유지되고 있는지 확인할 때 사용하는 프레임으로 서버나 브라우저에서 자동 생성해서 보내는 프레임
  - 이 외에도 커넥션 종료 프레임(connection close frame) 등 다양한 프레임이 있음

## 쿠키

##### 쿠키 읽기

- `document.cookie`는 `name=value` 쌍으로 구성되어있고, 각 쌍은 `;`로 구분한다.

##### 쿠키 쓰기

- `document.cookie`에 직접 값을 쓸 수 있다.
  > document.cookie = "user=John"; // 이름이 'user'인 쿠키의 값만 갱신함
- 형식의 유효성을 일관성 있게 유지하기 위해 반드시 내장함수 `encodeURIComponent`를 사용하여 이름과 값을 이스케이프 처리해 줘야 한다.
  > document.cookie = encodeURIComponent(name) + '=' + encodeURIComponent(value)

##### 쿠키 옵션

- `path=/`의 기본값은 현재 경로이고, 설정한 경로나 그 하위 경로에서만 쿠키 정보를 볼 수 있다.
- `domain=site.com`옵션에 아무런 값을 입력하지 않았다면 쿠키를 설정한 도메인에서만 쿠키 정보를 얻을 수 있으며. 명시적으로 도메인 주소를 설정한 경우엔, 해당 도메인의 서브 도메인에서도 쿠키 정보를 얻을 수 있다.
- `expires/max-age`는 쿠키의 만료 시간을 정해준다. 이 옵션이 없으면 브라우저가 닫힐 때 쿠키도 같이 삭제된다.
- `secure` 는 HTTPS 연결에서만 쿠키를 사용할 수 있게한다.
- `samesite` 는 요청이 외부 사이트에서 일어날 때, 브라우저가 쿠키를 보내지 못하도록 막아준다. XSRF 공격을 막는 데 유용하다.

## 스토리지

- 쿠키와 다르게 웹 스토리지 객체는 네트워크 요청 시 서버로 전송되지 않는다.
- 쿠키보다 더 많은 자료를 보관할 수 있다
- 개발자는 브라우저 내 웹 스토리지 구성 방식을 설정할 수 있다.

##### 스토리지 메서드

- `setItem(key, value)` – 키-값 쌍을 보관
- `getItem(key)` – 키에 해당하는 값을 받는다.
- `removeItem(key)` – 키와 해당 값을 삭제
- `clear()` – 모든 것을 삭제
- `key(index)` – 인덱스(index)에 해당하는 키를 받는다.
- `length` – 저장된 항목의 개수

## localStorage

- 오리진이 같은 경우 데이터는 모든 탭과 창에서 공유된다.
- 브라우저나 OS가 재시작하더라도 데이터가 파기되지 않는다.
- 키와 값은 반드시 문자열이어야 한다.

## sessionStorage

- 현재 떠 있는 탭내에서만 유지된다.
- 페이지를 새로 고침할 대 저장된 데이터는 사라지지않는다. 하지만 탭을 닫고 새로 열 때는 사라진다

##### storage 이벤트

- `localStorage`나 `sessionStorage`의 데이터가 갱신될 때, storage이벤트가 실행된다.
- `key` – 변경된 데이터의 키(.clear()를 호출했다면 null)
- `oldValue` – 이전 값(키가 새롭게 추가되었다면 null)
- `newValue` – 새로운 값(키가 삭제되었다면 null)
- `url` – 갱신이 일어난 문서의 url
- `storageArea` – 갱신이 일어난 localStorage나 sessionStorage 객체
