# 데이터 엔지니어링

속성: Architecture

#### 주변에 이걸로 데이터 사이언스에 입문해서 기초를 탄탄히 잡은 분도 있어요.

📘 마이크로소프트 무료 > 초보자를 위한 데이터 과학 - 커리큘럼
[https://github.com/microsoft/Data-Science-For-Beginners/blob/main/translations/ko/README.md](https://github.com/microsoft/Data-Science-For-Beginners/blob/main/translations/ko/README.md)

Data Science for Beginners..
이건 10주 / 20개 레슨 구성의 완전 무료 커리큘럼이예요.

한국어도 잘 제공되고 있어서 더 좋으실 거예요. 커리큘럼 구성도 깔끔..

- 데이터 사이언스란 무엇인가 / 윤리
- SQL, NoSQL, Pandas로 데이터 다루기
- Matplotlib 중심의 시각화
- 데이터 사이언스 라이프사이클
- Azure 클라우드 활용
- 실제 프로젝트까지

각 레슨마다 퀴즈, 실습, 과제, 솔루션이 다 들어있어서,,

그냥 읽고 끝나는 게 아니라 손으로 해보면서 배우는 구조..

데이터 사이언스 쪽 무료 고퀄리티 자료 참고해보시길~~

첨부한 로드맵도 참고하세요!

#### 데이터 사이언스 궁금하거나 좀 더 깊게 파보고 싶은 분들은 여기도 좋음.

모두 무료 고퀄리티 강의..
[https://boostcourse.org/opencourse](https://boostcourse.org/opencourse)

- [MIT] 데이터 사이언스 기초
- 파이썬으로 시작하는 데이터 사이언스
- AI로 핵심 데이터를 모아 한눈에 파악하기
- 모두를 위한 데이터 사이언스
- 데이터 시각화를 위한 태블로
- 기초 데이터 분석을 위한 핵심 SQL
- Hello, 데이터 사이언스!
- DataLit : 데이터다루기
- 캐글 실습으로 배우는 데이터 사이언스
- 프로젝트로 배우는 데이터사이언스

#### 데이터 엔지니어링을 처음 시작하는 사람부터 실무자까지..

📕 데이터 엔지니어링 핸드북
[https://github.com/DataExpert-io/data-engineer-handbook](https://github.com/DataExpert-io/data-engineer-handbook)

데이터 엔지니어가 되기 위해 필요한 모든 자료를 한곳에 모아놓은 큐레이션 저장소.

```java
data-engineer-handbook/
├ 4주 무료 입문 부트캠프 자료
├ 6주 무료 중급 부트캠프 자료
├ Databricks AI 부트캠프 자료
├ 추천 도서 25권+
├ 커뮤니티 10개+
├ 실습용 무료 프로젝트 목록
├ 인터뷰 대비 자료
└ 뉴스레터 목록
```

코드보다는 로드맵 + 학습 리소스 링크를 많이 제안하고 있죠.

백서, 필독서, 커뮤니티, 블로그, 소셜... 아 정말 많음.

#### AI를 공부하다 보면 '데이터 엔지니어'라는 직업을
자주 보게 됩니다.

쉽게 말하면, AI나 데이터 분석에 필요한 데이터를
모으고, 정리하고, 전달하는 시스템을
만드는 사람입니다.

The Data Engineering Handbook은
이 분야를 처음 배우는 사람을 위한
오픈소스 학습 자료입니다.

무엇부터 공부해야 하는지,
어떤 기술을 익혀야 하는지,
순서대로 정리해 두었습니다.
기초 학습부터
실무 프로젝트,
면접 준비 자료까지
한곳에서 살펴볼 수 있습니다.
특히 AI를 활용하다가
"데이터는 어디서 오고
어떻게 관리되는 걸까?"
궁금했던 분들에게
좋은 출발점이 될 수 있는 자료입니다.

[https://github.com/DataExpert-io/data-engineer-handbook](https://github.com/DataExpert-io/data-engineer-handbook)

#### AI 엔지니어로서 Top-k와 Top-p의 차이를 아시나요?

90%가 "둘 다 후보 잘라내는 거 아닌가요"에서 멈춥니다.
마트 진열대로 비유하면 끝납니다 👇

A. Top-k
→ 무조건 상위 5개만 올리는 진열대
→ 1등이 압도적이든 다 고만고만하든 항상 5칸입니다
→ LLM 디코딩에서 확률 상위 k개만 남깁니다. 남기는 개수가 고정입니다

B. Top-p
→ 매출 누적 90%까지만 채우는 진열대
→ 1등이 압도적이면 2칸, 다 비슷하면 30칸이 됩니다
→ LLM 디코딩에서 누적 확률이 p에 닿을 때까지만 남깁니다. 개수가 매번 달라집니다

A는 개수,
B는 비중.

Top-k는 몇 개를 남길지 미리 정하고, Top-p는 분포를 보고 몇 개를 남길지 그때그때 정합니다.

![image.png](image%20121.png)