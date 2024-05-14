## 이벤트 루프

- 이벤트 루프는 태스크가 들어오길 기다렸다가 태스크가 드렁오면 이를 처리하고, 처리할 태스크가 없는 경우엔 잠드는, 끊임없이 돌아가는 자바스크립트 내 루프입니다.
- 자바스크립트 엔진은 매크로태스크 하나를 처리할때마다 또 다른 매크로태스크나 렌더링 작업을 하기 전에 마이크로태스크 큐에 쌓인 마이크로태스크 전부를 처리한다.
- 이벤트 루프 알고리즘
  1. 매크로태스크 큐에서 가장 오래된 태스크를 꺼내 실행
  2. 모든 마이크로캐스크를 실행
  3. 렌더링할 것이 있으면 처리
  4. 매크로태스크 큐가 비어있으면 새로운 매크로태스크가 나타날때 까지 기다린다
  5. 1번으로 들어간다
- 새로운 매크로태스크를 스케줄링 하는 방법
  > 지연시간이 0인 `setTimeout(f)` 사용
- 새로운 마이크로태스크를 스케줄링 하는 방법
  > `queueMicrotask(f)` 사용 / 이외에도 프로미스 핸들러는 마이크로태스크 큐에 들어가 처리