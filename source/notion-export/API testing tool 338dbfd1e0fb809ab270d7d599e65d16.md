# API testing tool

속성: Backend

![image.png](image%2042.png)

Postman은 실제로 어떻게 돈을 벌고 있는 걸까?

모두가 무료로 사용하고 있는 걸 봐
요청 보내기만 하고
API 테스트만 하고

누가 돈 내는 걸 본 적 없어
광고 하나도 본 적 없고

그럼 Postman은 어떻게 그 모든 인프라 비용을 충당하는 거지?

- 무료 → 개인 API 테스트
- 유료 → 팀 협업, 워크스페이스, 거버넌스
- 엔터프라이즈 → 보안, 감사 로그, 통합
- API 플랫폼 → 모킹, 모니터링, 문서
- 당신은 팀들이 고객이 아닙니다.
    - 개인들은 무료로 사용하지만, 회사들은 다음을 위해 비용을 지불합니다:
    1. 협업
    2. 공유 작업 공간
    3. 거버넌스 & 보안
    4. API 모니터링 & 테스트

![image.png](image%2043.png)

![image.png](image%2044.png)

![image.png](image%2045.png)

---

#### Bruno v3.5.0의 새로운 기능

- 컬렉션 실행을 위한 공식 GitHub Action
- CI/CD를 위한 공식 Bruno CLI Docker 이미지
- 더 나은 가져오기: 오류 컨텍스트, 종속성 검사, 대량 Git 저장소 가져오기
- `bru.sendRequest()` / `bru.runRequest()`가 이제 타임라인에 표시됩니다
- CLI의 `--bail` 및 HTML 보고서 수정
- 자동화를 위한 더 부드러운 API 워크플로우를 위해 제작되었습니다.

![image.png](image%2046.png)

---

#### 학습 곡선에 따른 테스트 도구 순위

🟢 Postman — 쉬움
🟢 Jest — 쉬움
🟢 Vitest — 쉬움
🟢 Testing Library — 쉬움
🟢 Unit Testing — 쉬움

🔵 Cypress — 보통
🔵 Playwright — 보통
🔵 Integration Testing — 보통
🔵 API Testing — 보통
🔵 Mock Testing — 보통

🟠 Selenium — 어려움
🟠 Load Testing — 어려움
🟠 Performance Testing — 어려움
🟠 End to End Testing — 어려움
🟠 Contract Testing — 어려움

🔴 Chaos Testing — 매우 어려움
🔴 Distributed Load Testing — 매우 어려움
🔴 Large Scale Performance Testing — 매우 어려움
🔴 Fault Injection Testing — 매우 어려움
🔴 Production Resilience Testing — 매우 어려움