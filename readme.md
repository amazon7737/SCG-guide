# 🗺️ Reactive Backend Master 클래스 로드맵 (Kido 스타일 학습 가이드)

> 본 로드맵은 어려운 기술 용어를 쉬운 비유로 풀고, 단계별 구조도를 통해 '눈에 보이는 학습'을 지향합니다.
> 최종 목표는 **Spring Cloud Gateway**의 실전 운영 역량 확보와 **Reactor Core/Netty** 오픈소스 기여입니다.

---

## 1단계: Gateway의 겉모습 - "문지기 세우기" (SCG 기초)

_이 단계에서는 '약간 긴 퀵스타트'를 작성하며 전체 흐름을 잡습니다._

- **핵심 키워드:** `Predicate`(조건), `Filter`(동작), `Route`(길)
- **📸 그림 구조도 실습 (나중에 그릴 것):**
  1. **단순 길 찾기:** 사용자 요청이 Gateway에 도착해 서비스 A로 분기되는 단순 흐름도.
  2. **톨게이트 비유:** Filter가 고속도로 톨게이트처럼 요청/응답을 가공(검사, 변조)하는 과정 시각화.
- **학습 내용:**
  - 자바 코드가 아닌 `YAML` 설정만으로 원하는 목적지까지 '길(Route)'을 뚫어보기.
  - `GlobalFilter`를 아주 간단히 구현해 로그를 찍어보며, 비동기 로그가 찍히는 순서의 생소함 체험하기.

---

## 2단계: 비동기의 파이프라인 - "데이터 배달 사고 막기" (Reactor Core)

_기여(Contribution)를 위한 첫 관문입니다. 연산자(Operators) 내부를 들여다보기 시작합니다._

- **핵심 키워드:** `Flux` & `Mono`, `Backpressure`(역압), `Schedulers`(스레드 관리)
- **📸 그림 구조도 실습 (나중에 그릴 것):**
  1. **구슬 다이어그램:** `Marble Diagram`을 직접 손으로 그려보며 데이터 흐름 이해하기.
  2. **잠깐만! 신호:** 데이터 생산이 너무 빠를 때 소비자가 "나 죽어! 천천히 줘!"라고 말하는 Backpressure 신호 체계도.
- **학습 내용:**
  - `Map` vs `FlatMap`의 차이를 "빨래를 하나씩 개기" vs "빨래를 여러 명이 동시에 개기"와 같은 비유로 풀어서 정리하기.
  - `publishOn`과 `subscribeOn` 스레드가 바뀌는 지점을 '파란색/빨간색 화살표'로 표시하며 시각화하기.

---

## 3단계: 네트워크의 심해 - "데이터의 통로" (Reactor Netty)

_Low-level 기여를 위한 가장 중요한 단계입니다. 실제 전선(TCP/HTTP) 레벨을 이해합니다._

- **핵심 키워드:** `Connection Pool`, `ByteBuf`, `Event Loop`, `Non-blocking I/O`
- **📸 그림 구조도 실습 (나중에 그릴 것):**
  1. **회전초밥집:** `EventLoop`가 수많은 손님(소켓)의 주문을 하나의 요리사(실)가 쉬지 않고 처리하는 모습 시각화.
  2. **책갈피:** 메모리를 아껴 쓰는 `ByteBuf`의 읽기/쓰기 포인터 움직임 개념도.
- **학습 내용:**
  - `HttpClient` 설정을 바꿔보며 성능(Timeout, Max Connections)이 어떻게 변하는지 실험하고 기록하기.
  - `reactor-netty` 소스코드에서 실제 `Channel`이 어떻게 Reactor의 흐름과 합쳐지는지 보물찾기하듯 탐색하기.

---

## 4단계: 고수의 운영 도구 - "보이지 않는 적과 싸우기" (Ops & Debugging)

_실전 프로젝트 운영 역량을 키우는 단계입니다. 장애 상황에서 빛을 발합니다._

- **핵심 키워드:** `Micrometer`, `BlockHound`(차단 감지), `Context Propagation`
- **📸 그림 구조도 실습 (나중에 그릴 것):**
  1. **꼬리표 추적:** 비동기 스레드를 건너 뛰어도 `Trace ID`가 유지되는 '바톤 터치' 구조도.
  2. **끊어진 단서:** 예외 발생 시 `StackTrace`가 왜 끊기는지와 이를 잇는 해결법 시각화.
- **학습 내용:**
  - 의도적으로 `Thread.sleep`을 넣어 `BlockHound`가 "너 지금 비동기 망치고 있어!"라고 경고하는 실습 해보기.
  - 프로메테우스+그라파나 대시보드에 Gateway의 건강 상태 직접 그려보기.

---

## 5단계: 오픈소스 기여의 문 - "코드로 대화하기" (Source Analysis)

_직접 오픈소스 조직의 일원이 되기 위한 최종 관문입니다._

- **핵심 키워드:** `Queue Drain`, `Operator Fusion`, `Work Stealing`
- **📸 그림 구조도 실습 (나중에 그릴 것):**
  1. **버그 재현:** GitHub Issue에 올라온 버그 상황을 나만의 다이어그램으로 재현해보기.
  2. **Before & After:** 내가 수정한 코드가 데이터 흐름을 어떻게 개선했는지 비교도 그리기.
- **학습 내용:**
  - `map`이나 `filter` 연산자의 내부 소스를 뜯어보며 `onNext`, `onSubscribe`가 서로 어떻게 인사(통신)하는지 분석하기.
  - 'Good First Issue'를 찾아 아주 작은 오타나 오해의 소지가 있는 주석 수정부터 기여 시도하기.

---

## ✍️ 미래의 나에게 주는 'Kido 스타일' 작성 팁

1. **"왜?"부터 시작하기:** "이 기술이 없었을 때 우리 조상님들(?)은 어떤 고생을 했을까?"를 생각하며 서술하세요.
2. **색깔에 의미 부여하기:** 구조도를 그릴 때 **사용자 스레드는 파란색**, **Netty 워커 스레드는 빨간색**으로 고정하면 나중에 보기 훨씬 편합니다.
3. **주석을 대화로 바꾸기:** 소스코드의 딱딱한 주석을 "자, 이제 데이터를 다음 사람에게 던질게!" 같은 친숙한 문장으로 재해석하세요.

## 작업할때 참고한 레퍼런스들

- https://docs.spring.io/spring-cloud-gateway/reference/index.html
- https://github.com/spring-cloud/spring-cloud-gateway
- https://projectreactor.io/docs
- https://github.com/reactor/reactor-core
- https://projectreactor.io/docs/netty/1.1.21/reference/index.html
- https://github.com/reactor/reactor-netty
