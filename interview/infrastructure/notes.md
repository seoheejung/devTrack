## 인프라 / 운영 / DevOps (실제 운영 환경 대응)


<details>
<summary><strong>1. [Kubernetes pod 제한] 기본적으로 쿠버네티스에서 노드당 몇 개의 파드를 실행할 수 있나요?</strong></summary>

1. [Kubernetes pod 제한] 기본적으로 쿠버네티스에서 노드당 몇 개의 파드를 실행할 수 있나요?
    
    
    ```
    A. 기본적으로 약 110개입니다.
    
    이유
    kubelet의 maxPods 설정 기본값입니다.
    
    확장
    네트워크 CIDR과 리소스에 따라 변경 가능합니다.
    ```
    

</details>

---


<details>
<summary><strong>2. [로그 구조 개선] 시스템 로그가 너무 시끄러워서 중요한 문제점을 식별하기 어렵습니다. 어떻게 개선하시겠습니까?</strong></summary>

2. [로그 구조 개선] 시스템 로그가 너무 시끄러워서 중요한 문제점을 식별하기 어렵습니다. 어떻게 개선하시겠습니까?
    
    ```
    A. 로그 구조와 레벨을 재설계합니다.
    
    이유
    불필요한 로그가 많으면 실제 장애 신호를 식별하기 어렵습니다.
    
    확장
    structured logging, log level 분리, sampling 적용합니다.
    ```
    

</details>

---


<details>
<summary><strong>3. [로드밸런싱] 로드 밸런서가 트래픽을 어떤 서버로 보낼지 어떻게 결정하나요?</strong></summary>

3. [로드밸런싱] 로드 밸런서가 트래픽을 어떤 서버로 보낼지 어떻게 결정하나요?
    
    ```
    A. 로드 밸런싱 알고리즘을 기반으로 결정합니다.
    
    이유
    트래픽을 균등 분산하거나 특정 조건에 따라 최적 서버를 선택하기 위함입니다.
    
    확장
    round-robin, least connections, IP hash 등이 사용됩니다.
    ```
    

</details>

---


<details>
<summary><strong>4. [CORS] 프론트엔드는 <code>localhost:3000</code>에 있고 백엔드는 <code>localhost:8000</code>에 있습니다. 왜 CORS 오류가 발생하나요?</strong></summary>

4. [CORS] 프론트엔드는 `localhost:3000`에 있고 백엔드는 `localhost:8000`에 있습니다. 왜 CORS 오류가 발생하나요?
    
    ```
    CORS 오류가 여기서 발생하는 이유는 
    브라우저가 동일 출처 정책(same origin policy) 하에서 
    서로 다른 포트의 localhost를 별개의 출처로 취급하기 때문입니다. 
    3000 포트의 프론트엔드가 8000 포트의 백엔드에 허가 없이 호출할 수 없습니다. 
    백엔드 측에서 프론트엔드 URL이나 개발용으로 *로 설정한 
    Access-Control-Allow-Origin 헤더를 추가하여 이를 수정하세요. 
    필요에 따라 메서드와 헤더도 허용하세요.
    
    A. 서로 다른 origin이기 때문입니다.
    
    이유
    포트가 다르면 동일 출처 정책에 의해 다른 origin으로 간주됩니다.
    
    확장
    Access-Control-Allow-Origin 헤더 설정으로 해결합니다.
    ```
    

</details>

---


<details>
<summary><strong>5. [Preflight 문제] CORS는 <code>/api/users</code> 에 대해서는 작동하지만 동일한 서버에서 <code>/api/orders</code> 에 대해서는 실패합니다. 둘 다 동일한 백엔드 코드를 사용합니다. 왜 그런가요?</strong></summary>

5. [Preflight 문제] CORS는 `/api/users` 에 대해서는 작동하지만 동일한 서버에서 `/api/orders` 에 대해서는 실패합니다. 둘 다 동일한 백엔드 코드를 사용합니다. 왜 그런가요?
    
    ```
    / api / orders 경로는 서버 구성에서 다른 실행 경로입니다. 
    > / api / orders 가 비단순 요청(예: POST 또는 DELETE)인 경우, 
    브라우저는 숨겨진 사전 요청(Preflight, OPTIONS) 요청을 보냅니다. 
    서버나 역방향 프록시가 해당 OPTIONS 요청을 차단하면, 
    실제 '코드'가 실행되지 않고 CORS 오류가 발생합니다. 
    > / api / users 는 아마도 사전 요청이 필요 없는 
    단순 GET 요청이기 때문에 작동할 것입니다.
    
    A. Preflight 요청 처리 실패입니다.
    
    이유
    POST/DELETE 요청은 OPTIONS 요청을 먼저 보내며, 이 응답이 차단되면 실패합니다.
    
    확장
    서버 또는 프록시에서 OPTIONS 허용 설정이 필요합니다.
    ```
    

</details>

---


<details>
<summary><strong>6. [글로벌 latency 해결 geo routing] 당신의 API는 호주에서 90ms에 응답하지만 인도에서는 600ms에 응답합니다. 동일한 백엔드. 동일한 코드. 이걸 고치기 위해 무엇을 사용하겠습니까?</strong></summary>

6. [글로벌 latency 해결 geo routing] 당신의 API는 호주에서 90ms에 응답하지만 인도에서는 600ms에 응답합니다. 동일한 백엔드. 동일한 코드. 이걸 고치기 위해 무엇을 사용하겠습니까?
    
    ```
    A. 지리적 분산 아키텍처를 적용합니다.
    
    이유
    네트워크 거리로 인한 latency 차이입니다.
    
    확장
    CDN, edge server, geo routing을 사용합니다.
    ```
    

</details>

---


<details>
<summary><strong>7. [Git 히스토리 전략] 일부 팀은 왜 PR 워크플로우에서 “병합 전에 리베이스(Rebase)”를 강제하나요?</strong></summary>

7. [Git 히스토리 전략] 일부 팀은 왜 PR 워크플로우에서 “병합 전에 리베이스(Rebase)”를 강제하나요?
    
    ```
    팀에서 "병합 전 리베이스"를 시행하는 이유는 
    깔끔하고 선형적인 커밋 히스토리를 생성하여 가독성과 디버깅을 크게 향상시키기 위함입니다. 
    메인 브랜치에 불필요한 병합 커밋이 쌓이는 것을 방지합니다.
    
    A. 추적 가능성을 높이고 선형적(Linear)인 Git 히스토리를 유지하기 위해서입니다.
    
    이유
    다수의 개발자가 작업할 때 단순 Merge를 남발하면 거미줄 같은 히스토리가 생성되어, 
    장애 발생 시 원인 커밋을 추적하는 `git bisect`나 `git log` 분석이 극도로 어려워집니다.
    
    확장
    대규모 프로젝트나 오픈소스에서는 Rebase 후 Merge(Fast-forward) 
    혹은 Squash Merge를 엄격하게 컨벤션으로 가져가 불필요한 병합 노이즈를 제거합니다.
    ```
    

</details>

---


<details>
<summary><strong>8. 팀원의 커밋을 공유 브랜치에서 force-push로 지워버렸습니다. 팀원의 작업을 복구하고 브랜치를 안전하게 복원하는 방법은 무엇인가요?</strong></summary>

8. 팀원의 커밋을 공유 브랜치에서 force-push로 지워버렸습니다. 팀원의 작업을 복구하고 브랜치를 안전하게 복원하는 방법은 무엇인가요?
    
    ```
    A. git reflog로 이전 커밋을 찾아 복구합니다.
    
    이유
    force-push로 히스토리가 사라져도 로컬 reflog에는 참조 기록이 남아 있습니다.
    
    확장
    복구 후 git reset --hard <commit> → git push --force로 
    브랜치를 정상 상태로 되돌립니다.
    ```
    

</details>

---


<details>
<summary><strong>9. 중요한 브랜치를 실수로 삭제했는데, 그 브랜치가 병합된 적이 없고 아무도 로컬 복사본을 가지고 있지 않습니다. 어떻게 복구하시겠습니까?</strong></summary>

9. 중요한 브랜치를 실수로 삭제했는데, 그 브랜치가 병합된 적이 없고 아무도 로컬 복사본을 가지고 있지 않습니다. 어떻게 복구하시겠습니까?
    
    ```
    A. reflog 또는 원격 dangling commit을 찾아 브랜치를 복구합니다.
    
    이유
    Git은 삭제된 브랜치의 커밋을 일정 기간 GC 전까지 보존합니다.
    
    확장
    git fsck --lost-found 또는 원격 저장소 로그를 통해 
    commit을 찾아 branch를 다시 생성합니다.
    ```
    

</details>

---


<details>
<summary><strong>10. 6개월 전에 만든 기능 브랜치를 메인 브랜치로 리베이스했는데, 커밋의 절반이 사라졌습니다.</strong></summary>

10. 6개월 전에 만든 기능 브랜치를 메인 브랜치로 리베이스했는데, 커밋의 절반이 사라졌습니다.  
작업 내용을 잃지 않고 이 문제를 어떻게 해결할 수 있을까요?
    
    ```
    오래된 브랜치를 리베이스할 때 수많은 충돌이 발생하고, 이를 해결하는 과정에서 
    실수로 `git rebase --skip`을 실행했거나 잘못된 충돌 병합으로 인해 
    커밋이 유실되었을 가능성이 높습니다.
    
    A. `git reflog`를 사용하여 리베이스 이전 상태로 브랜치를 되돌립니다.
    
    왜 이렇게 판단했는지
    Git의 참조 로그(Reference logs) 시스템 설계 기준. 
    Git은 브랜치 업데이트나 리베이스 등 
    HEAD가 변경되는 모든 작업의 로컬 이력을 기본 90일간 보관합니다.
    
    이유
    리베이스는 기존 커밋을 삭제하는 것이 아니라, 
    새로운 커밋을 만들어 HEAD를 이동시키는 작업입니다. 
    따라서 눈에 보이지 않는 기존 커밋들은 가비지 컬렉션(GC)이 실행되기 전까지 
    로컬 저장소에 그대로 남아있어 참조 해시값만 알면 100% 복구가 가능합니다.
    
    확장
    복구 절차 및 대안 전략:
    1. `git reflog` 명령어를 실행하여 리베이스를 시작하기 직전의 
        커밋 해시값(예: HEAD@{5})을 찾습니다.
    2. `git reset --hard <복구할해시값>`을 실행하여 브랜치를 원상 복구합니다.
    3. 6개월 된 브랜치는 베이스가 너무 크게 달라져 리베이스가 위험하므로, 
       대신 `git merge main`을 수행하여 충돌을 한 번에 해결하거나, 
       새 브랜치를 판 뒤 `git cherry-pick`으로 필요한 커밋만 
       선별적으로 가져오는 방식을 적용합니다.
    ```
    

</details>

---


<details>
<summary><strong>11. [클라우드 리소스 IP 관리] EC2 인스턴스가 중지되고 시작될 때 인스턴스의 IP 주소가 자동으로 변경됩니다. 이 문제의 원인은 무엇일까요?</strong></summary>

11. [클라우드 리소스 IP 관리] EC2 인스턴스가 중지되고 시작될 때 인스턴스의 IP 주소가 자동으로 변경됩니다. 이 문제의 원인은 무엇일까요?
    
    ```
    IP가 변경되는 이유는 인스턴스가 자동 할당된 동적 공용 IP를 사용하기 때문입니다. 
    중지/시작 후 동일한 공용 IP를 유지하려면 Elastic IP를 연결하세요.
    
    A. 인스턴스가 고정 IP를 할당받지 않고, 
    AWS의 동적 퍼블릭 IP(Public IP) 풀(Pool)을 사용하고 있기 때문입니다.
    
    이유
    AWS EC2 인스턴스는 시작 시 기본적으로 동적 퍼블릭 IP를 할당받습니다. 
    하지만 인스턴스가 '중지(Stopped)' 상태가 되면 이 IP는 AWS의 전체 IP 풀로 반납되며, 
    다시 시작할 때 새로운 IP를 무작위로 재할당받게 됩니다.
    
    확장
    DNS와 연동하거나 고정된 엔드포인트가 필요한 경우 Elastic IP(EIP)를 할당하여 
    인스턴스에 고정하거나, ALB(Application Load Balancer)와 같은 정적 진입점을 두어 
    아키텍처를 구성해야 합니다.
    ```
    

</details>

---


<details>
<summary><strong>12. [Kubernetes Pod 네트워크] 같은 Pod 내의 두 컨테이너가 동일한 포트에 바인딩할 수 있나요?</strong></summary>

12. [Kubernetes Pod 네트워크] 같은 Pod 내의 두 컨테이너가 동일한 포트에 바인딩할 수 있나요?
    
    ```
    A. 불가능합니다.
    
    왜 이렇게 판단했는지
    Pod는 단순한 컨테이너 묶음이 아니라 하나의 “네트워크 단위”이기 때문에, 
    내부 컨테이너들이 서로 독립된 네트워크를 가진다고 보면 안 되기 때문입니다.
    
    이유
    Pod 내의 모든 컨테이너는 동일한 Network Namespace를 공유하므로 
    동일한 IP와 포트 공간을 사용합니다. 
    따라서 같은 포트에 바인딩을 시도하면 포트 충돌(Port Conflict)이 발생합니다.
    
    확장 (실제 적용)
    - Sidecar 패턴 사용 시 메인 컨테이너와 포트 충돌이 자주 발생하므로 주의해야 합니다.
    - Exporter나 Agent 컨테이너는 반드시 메인 애플리케이션과 다른 포트를 사용하도록 
      구성해야 합니다.
    - 디버깅 시 컨테이너 내부에서 `netstat` 또는 `ss` 명령어로 바인딩된 포트를 확인합니다.
    ```
    

</details>

---


<details>
<summary><strong>13. [Kubernetes 트래픽 트러블슈팅] 파드가 실행 중입니다. 서비스가 존재하며 파드를 올바르게 선택합니다. 하지만 트래픽이 여전히 실패합니다. 어떤 쿠버네티스 구성 요소를 먼저 확인하시겠습니까?</strong></summary>

13. [Kubernetes 트래픽 트러블슈팅] 파드가 실행 중입니다. 서비스가 존재하며 파드를 올바르게 선택합니다. 하지만 트래픽이 여전히 실패합니다. 어떤 쿠버네티스 구성 요소를 먼저 확인하시겠습니까?
    
    ```
    A. Service → Endpoint → kube-proxy 순으로 트래픽 흐름 경로를 확인합니다.
    
    왜 이렇게 판단했는지
    문제를 단순히 “리소스의 정상 작동 상태”가 아니라, 실제 네트워크 패킷이 전달되는 
    “트래픽 흐름 경로” 기준으로 쪼개서 분석해야 하기 때문입니다.
    
    이유
    Service의 selector가 맞더라도, Readiness Probe 실패 등으로 인해 
    Endpoint 리스트가 비어있거나, 워커 노드의 kube-proxy 룰(iptables/IPVS)이 
    깨져 있다면 실제 파드로의 트래픽 전달은 실패합니다.
    
    확장 (실제 적용)
    - `kubectl get endpoints <서비스명>`을 통해 파드 IP가 매핑되어 있는지 확인합니다.
    - 노드에 접속하여 kube-proxy가 생성한 iptables 룰을 확인합니다.
    - CNI(Container Network Interface) 플러그인 문제일 경우 
      패킷 드롭(Packet Drop)이 발생할 수 있으므로 CNI 로그를 확인합니다.
    ```
    

</details>

---


<details>
<summary><strong>14. [컨테이너 vs 가상머신(VM)] 도커 컨테이너가 가볍다면, 왜 여전히 가상 머신을 사용하는 걸까요?</strong></summary>

14. [컨테이너 vs 가상머신(VM)] 도커 컨테이너가 가볍다면, 왜 여전히 가상 머신을 사용하는 걸까요?
    
    ```
    컨테이너는 호스트 OS 커널을 공유하고 앱과 종속성만 패키징하기 때문에 가볍지만, 
    VM은 더 강력한 격리와 다양한 운영 체제를 실행할 수 있는 기능을 위해 
    전체 OS 에뮬레이션을 제공합니다.
    
    A. 강력한 격리(Isolation) 수준과 완벽한 OS 독립성이 필요하기 때문입니다.
    
    왜 이렇게 판단했는지
    “왜 VM을 쓰냐”는 질문은 시스템의 성능이나 가벼움의 기준이 아니라 
    “보안 및 격리 요구사항”을 묻는 것이기 때문입니다.
    
    이유
    컨테이너는 호스트 OS의 커널을 공유하고 애플리케이션과 종속성만 패키징하여 가볍지만 
    커널 레벨의 취약점을 공유합니다. 반면 VM은 하이퍼바이저를 통해 
    자체 커널을 포함한 전체 OS를 에뮬레이션하므로 완벽한 하드웨어 수준의 격리를 제공합니다.
    
    확장 (실제 적용)
    - 금융/의료 등 엄격한 보안 컴플라이언스가 요구되는 시스템에는 VM 격리가 필수적입니다.
    - 호스트 OS(Linux)와 완전히 다른 운영체제(Windows, FreeBSD 등) 환경이 필요할 때 
      사용합니다.
    - SaaS 서비스 등에서 테넌트 간(Multi-tenancy) 완벽한 보안 격리가 필요할 때 적용합니다.
    ```
    

</details>

---


<details>
<summary><strong>15. [Dockerfile 명령어] Dockerfile에서 ENTRYPOINT와 CMD의 차이점은 무엇인가요?</strong></summary>

15. [Dockerfile 명령어] Dockerfile에서 ENTRYPOINT와 CMD의 차이점은 무엇인가요?
    
    ```
    A. ENTRYPOINT는 실행될 바이너리를 고정하고, 
    CMD는 그 바이너리에 전달할 기본 인자(Argument)를 제공합니다.
    
    왜 이렇게 판단했는지
    컨테이너 실행(`docker run`) 시 “어떤 값을 외부에서 쉽게 덮어쓸(Override) 수 있는가”를 
    기준으로 두 명령어를 구분하기 때문입니다.
    
    이유
    ENTRYPOINT에 지정된 명령은 컨테이너가 실행될 때 항상 수행되는 반면, 
    CMD에 지정된 값은 `docker run` 명령어 뒤에 추가 인자를 주입할 경우 
    쉽게 무시되고 덮어씌워지기 때문입니다.
    
    확장 (실제 적용)
    - ENTRYPOINT: 컨테이너가 반드시 실행해야 하는 메인 실행 파일 경로를 지정합니다.
    - CMD: 해당 실행 파일에 넘겨줄 디폴트 옵션이나 파라미터를 지정합니다.
    - 결합 사용 예시: `ENTRYPOINT ["nginx"]` / `CMD ["-g", "daemon off;"]`
       → 실행 시 `docker run my-nginx -t` 처럼 인자를 변경하여 동작을 제어할 수 있습니다.
    ```
    

</details>

---


<details>
<summary><strong>16. [모니터링 시스템 파이프라인] Java 백엔드 개발자로서, Splunk, Dynatrace, Grafana, ELK와 같은 경고 및 모니터링 도구를 구성하는 것이 기대됩니다. Spring Boot Actuator를 Grafana와 같은 외부 모니터링 및 경고 시스템과 어떻게 통합할 수 있나요?</strong></summary>

16. [모니터링 시스템 파이프라인] Java 백엔드 개발자로서, Splunk, Dynatrace, Grafana, ELK와 같은 경고 및 모니터링 도구를 구성하는 것이 기대됩니다. Spring Boot Actuator를 Grafana와 같은 외부 모니터링 및 경고 시스템과 어떻게 통합할 수 있나요?
    
    ```
    Actuator = 데이터 소스, Prometheus = 수집기, Grafana = 시각화, Alerts = 액션
    Spring Boot Actuator를 Micrometer와 통합하여 Prometheus 호환 메트릭을 노출하고, 
    Prometheus를 사용하여 이를 스크랩하며, Grafana에서 시각화하고, 
    임계값에 기반한 알림을 구성하겠습니다.
    
    A. Actuator + Micrometer + Prometheus + Grafana 구조로 통합합니다.
    
    이유
    각 구성 요소의 역할이 명확히 분리되어 동작하기 때문입니다. 
    (Actuator는 메트릭 제공, Prometheus는 수집, Grafana는 시각화 역할 수행)
    
    확장
    Prometheus의 Alertmanager를 통해 특정 임계값 기준의 알림(Alerts) 파이프라인을 
    추가 구성합니다.
    ```
    

</details>

---


<details>
<summary><strong>17. [빌드 아티팩트(Build Artifact)] CI/CD에서 빌드 아티팩트란 무엇인가요?</strong></summary>

17. [빌드 아티팩트(Build Artifact)] CI/CD에서 빌드 아티팩트란 무엇인가요?
    
    ```jsx
    빌드 아티팩트는 CI 빌드 과정에서 생성되는 버전이 지정된 출력물로, 
    JAR, 바이너리, 또는 Docker 이미지와 같은 형태이며, 저장된 후 환경 전반에 배포됩니다.
    
    A. CI 파이프라인(빌드/테스트 과정)이 완료된 후 생성되는, 
    배포 가능한 불변의(Immutable) 최종 결과물을 의미합니다.
    
    이유
    소스 코드를 컴파일 및 패키징하여 언제든 즉시 실행 가능한 형태로 고정해 두어야, 
    개발(Dev) - 스테이징(Staging) - 운영(Prod) 환경을 거칠 때마다 다시 빌드하여 
    발생할 수 있는 환경 격차(사이드 이펙트)를 차단하고 일관된 배포를 보장할 수 있기 때문입니다.
    
    확장
    이러한 아티팩트(예: JAR 파일, Docker 이미지)는 생성 직후 Nexus, Artifactory, AWS ECR 등의 
    중앙화된 Artifact Repository에 안전하게 저장되고 버전 관리되어야 롤백과 추적이 가능합니다.
    ```
    

</details>

---


<details>
<summary><strong>18. [클라우드 스토리지 분류] 오브젝트 스토리지, 블록 스토리지, 파일 스토리지 간의 차이점은 무엇인가요?</strong></summary>

18. [클라우드 스토리지 분류] 오브젝트 스토리지, 블록 스토리지, 파일 스토리지 간의 차이점은 무엇인가요?
    
    ```jsx
    오브젝트 스토리지는 파일을 메타데이터와 함께 객체로 저장하며 API를 통해 접근합니다. 
    블록 스토리지는 VM/데이터베이스를 위한 원시 디스크 볼륨을 제공하며 지연 시간이 낮습니다. 
    파일 스토리지는 여러 서버를 위한 공유 폴더를 경로/디렉토리로 노출합니다.
    
    A. 데이터 접근 방식과 내부 저장 구조의 차이입니다.
    
    이유
    각 스토리지는 접근 속도, 확장성, 공유 방식에 따라 최적화된 아키텍처가 근본적으로 다르기 때문입니다.
    
    확장
    - 오브젝트 스토리지(예: AWS S3): 데이터를 고유 식별자와 메타데이터를 가진 '객체'로 묶어 
      HTTP API를 통해 접근합니다. 지연 시간은 다소 있지만 무한한 수평 확장에 유리합니다.
    - 블록 스토리지(예: AWS EBS): 데이터를 고정된 '블록' 단위로 나누어 저장하며, 
      OS나 DB가 직접 마운트하여 사용하는 원시 볼륨입니다. 가장 빠르고 지연 시간이 낮습니다.
    - 파일 스토리지(예: AWS EFS): 계층형 디렉토리 구조를 가지며, 여러 서버 인스턴스가 
      동시에 공유 폴더처럼 접근(NFS/SMB)할 수 있습니다.
    ```
    

</details>

---


<details>
<summary><strong>19. [Dockerfile COPY vs ADD] Dockerfile에서 COPY와 ADD의 차이점은 무엇인가요?</strong></summary>

19. [Dockerfile COPY vs ADD] Dockerfile에서 COPY와 ADD의 차이점은 무엇인가요?
    
    ```jsx
    COPY는 단순히 로컬 시스템에서 Docker 이미지로 파일을 복사합니다.
    ADD는 동일한 작업을 수행하지만, 압축된 파일을 자동으로 추출하거나 
    URL에서 다운로드하는 등의 추가 기능을 갖추고 있습니다.
    
    A. COPY는 단순 로컬 파일 복사, ADD는 압축 해제 및 원격 URL 다운로드 기능을 포함합니다.
    
    이유
    COPY는 명확하고 투명한 복사를 수행하여 예측 가능성이 높습니다. 
    ADD는 추가적인 자동화 기능을 제공하나 이미지 레이어 관리에 주의가 필요합니다.
    
    확장
    Docker 공식 가이드는 명확성을 위해 COPY를 권장하며, 
    외부 자원 다운로드는 RUN curl/wget 후 파일 삭제를 포함한 단일 레이어 처리가 더 효율적입니다.
    ```
    

</details>

---


<details>
<summary><strong>20. [리눅스 배포판 비교] 우분투, CentOS, 데비안과 같은 리눅스 배포판 간의 차이점은 무엇인가?</strong></summary>

20. [리눅스 배포판 비교] 우분투, CentOS, 데비안과 같은 리눅스 배포판 간의 차이점은 무엇인가?
    
    ```
    A. 패키지 관리 시스템과 소프트웨어 업데이트 주기의 차이입니다.
    
    이유
    Debian/Ubuntu는 apt를 사용하며 최신 패키지 도입에 유연합니다. 
    CentOS(RHEL 계열)는 yum/dnf를 사용하며 기업용 서버의 장기 안정성에 특화되어 있습니다.
    
    확장
    운영 목적에 따라 최신 런타임이 필요한 경우 Ubuntu를, 
    보수적인 시스템 안정성이 우선인 경우 RHEL 계열을 선택합니다.
    ```
    

</details>

---


<details>
<summary><strong>21. [파일 시스템 계층 구조] 리눅스 파일 시스템 계층 구조를 설명하시오.</strong></summary>

21. [파일 시스템 계층 구조] 리눅스 파일 시스템 계층 구조를 설명하시오.
    
    ```
    A. FHS 표준에 따른 트리 구조로, 역할별로 디렉토리가 분리되어 있습니다.
    
    이유
    /bin(핵심 실행파일), /etc(설정), /var(로그/데이터) 등 위치를 표준화하여 
    시스템 관리의 일관성과 애플리케이션 호환성을 유지합니다.
    
    확장
    각 디렉토리의 마운트 지점을 분리하여 특정 영역의 용량 부족이 
    시스템 전체 중단으로 이어지지 않도록 설계합니다.
    ```
    

</details>

---


<details>
<summary><strong>22. [cron 작업 자동화] cron 작업을 사용하여 작업을 자동화하는 방법은 무엇인가?</strong></summary>

22. [cron 작업 자동화] cron 작업을 사용하여 작업을 자동화하는 방법은 무엇인가?
    
    ```
    A. crontab 설정 파일에 실행 주기와 명령어를 등록합니다.
    
    이유
    정해진 시간에 주기적으로 실행해야 하는 작업(백업, 로그 정리)을 
    OS 레벨에서 자동화하여 인적 오류를 방지하기 위함입니다.
    
    확장
    실행 결과를 로그 파일로 리다이렉트하고, 실패 시 알림을 보내는 
    모니터링 체계를 갖추는 것이 운영 측면에서 중요합니다.
    ```
    

</details>

---


<details>
<summary><strong>23. [systemd 서비스 관리] systemd란 무엇이며, 서비스를 어떻게 관리하는가?</strong></summary>

23. [systemd 서비스 관리] systemd란 무엇이며, 서비스를 어떻게 관리하는가?
    
    ```
    A. 리눅스의 최신 init 시스템으로, 유닛 파일을 통해 서비스 생명주기를 제어합니다.
    
    이유
    병렬 부팅을 지원하여 속도가 빠르며, 서비스의 의존성 및 
    자동 재시작 로직을 선언적으로 관리할 수 있습니다.
    
    확장
    systemctl 명령어를 사용하여 서비스의 활성화, 시작, 중지 및 상태를 통합 관리합니다.
    ```
    

</details>

---


<details>
<summary><strong>24. [systemctl vs service] systemctl과 service 명령어의 차이점은 무엇인가?</strong></summary>

24. [systemctl vs service] systemctl과 service 명령어의 차이점은 무엇인가?
    
    ```
    A. systemctl은 systemd의 통합 제어 도구이며, service는 구형 호환용 도구입니다.
    
    이유
    최신 리눅스는 systemd가 표준이므로 systemctl 사용이 정석입니다. 
    service는 내부적으로 systemctl을 호출하여 제한적인 기능을 수행합니다.
    
    확장
    부팅 시 자동 시작 설정(enable/disable) 등 상세 제어는 systemctl에서만 지원됩니다.
    ```
    

</details>

---


<details>
<summary><strong>25. [리눅스 로그 관리] 리눅스 로그는 무엇이며, 어디에 저장되는가?</strong></summary>

25. [리눅스 로그 관리] 리눅스 로그는 무엇이며, 어디에 저장되는가?
    
    ```
    A. 시스템 활동 기록이며, 주로 /var/log 디렉토리에 저장됩니다.
    
    이유
    장애 발생 시 원인 분석을 위한 핵심 데이터로, syslog, auth.log, dmesg 등이 대표적입니다.
    
    확장
    logrotate를 통해 로그 크기를 제한하고, 중앙 로그 분석 서버로 전송하여 가시성을 확보합니다.
    ```
    

</details>

---


<details>
<summary><strong>26. [환경 편차(Env Drift)] 로컬에서는 서비스가 작동하는데 프로덕션에서는 왜 실패하는가?</strong></summary>

26. [환경 편차(Env Drift)] 로컬에서는 서비스가 작동하는데 프로덕션에서는 왜 실패하는가?
    
    ```
    A. 환경 간의 종속성 불일치, 네트워크 제약, 혹은 구성 데이터(Secret) 오설정 때문입니다.
    
    이유
    로컬 환경과 프로덕션은 커널 버전, OS 라이브러리, DB 상태, 방화벽 규칙 등이 다르므로 
    이러한 미세한 차이가 런타임 에러를 유발합니다.
    
    확장
    Docker와 같은 컨테이너 기술을 통해 실행 환경을 일치시키고, IaC(Terraform 등)를 도입하여 
    인프라 구성의 일관성을 강제해야 합니다.
    ```
    

</details>

---


<details>
<summary><strong>27. [Kafka 컨슈머 병목] 명확한 오류 없이 Kafka 지연(Lag)이 계속 증가하는 이유는 무엇인가요?</strong></summary>

27. [Kafka 컨슈머 병목] 명확한 오류 없이 Kafka 지연(Lag)이 계속 증가하는 이유는 무엇인가요?
    
    ```
    A. 컨슈머의 처리 속도가 프로듀서의 생산 속도를 따라가지 못하는 '처리 병목' 상태입니다.
    
    이유
    에러가 없더라도 비즈니스 로직 수행 시간이 길거나 DB I/O 지연이 발생하면 
    컨슈머는 메시지를 가져오는 속도가 느려져 지연이 누적됩니다.
    
    확장
    컨슈머 그룹의 파티션 수를 늘려 병렬성을 높이거나, 컨슈머 내부 로직을 최적화하고 
    일괄 처리(Batch Processing) 설정을 조정하여 처리량을 개선해야 합니다.
    ```
    

</details>

---


<details>
<summary><strong>28. [심층 헬스 체크 실패] 헬스 체크는 통과되는데 API가 여전히 500 오류를 반환하는 이유는 무엇인가요?</strong></summary>

28. [심층 헬스 체크 실패] 헬스 체크는 통과되는데 API가 여전히 500 오류를 반환하는 이유는 무엇인가요?
    
    ```
    A. 헬스 체크 범위가 '단순 프로세스 생존'에만 국한되어 실질적인 종속성 검증이 빠졌기 때문입니다.
    
    이유
    로드밸런서는 포트가 열려 있어 200 응답을 받지만, 실제 로직 수행 시 필요한 
    DB 연결이나 외부 API 권한에 문제가 있으면 실제 요청은 실패하게 됩니다.
    
    확장
    'Deep Health Check'를 도입하여 DB 커넥션 및 필수 연동 서비스의 상태까지 
    검증 로직에 포함시켜야 비정상 노드를 즉시 격리할 수 있습니다.
    ```
    

</details>

---


<details>
<summary><strong>29. [도커 데이터 영속성] 당신은 Docker에서 Redis를 실행하고 있습니다. <code>docker compose down</code>, <code>docker compose up</code> 모든 캐시 데이터가 사라집니다. 세션 저장소가 지워집니다 사용자들이 모든 곳에서 로그아웃됩니다. 뭐를 잊으셨나요 설정하는 걸?</strong></summary>

29. [도커 데이터 영속성] 당신은 Docker에서 Redis를 실행하고 있습니다. `docker compose down`, `docker compose up` 모든 캐시 데이터가 사라집니다. 세션 저장소가 지워집니다 사용자들이 모든 곳에서 로그아웃됩니다. 뭐를 잊으셨나요 설정하는 걸?
    
    ```
    지속적 볼륨
    
    Redis 데이터를 Docker 볼륨/바인드 마운트에 마운트하지 않으면, 
    컨테이너 파일 시스템은 짧은 시간 동안만 지속됩니다.
    
    그래서 컨테이너가 파괴될 때:
    - 메모리 내 캐시가 사라집니다
    - Redis 지속성 파일이 사라집니다
    
    A. 컨테이너 파일 시스템 외부에 데이터를 영구 저장하기 위한 Docker 볼륨(Volume) 또는 
    바인드 마운트(Bind Mount) 설정입니다.
    
    이유
    Docker 컨테이너의 내부 레이어는 일시적(Ephemeral)인 특성을 가집니다. `down` 명령어로 
    컨테이너가 파괴되면 Redis 런타임에 디스크로 쓰여졌던 영속성 파일(RDB snapshot 또는 AOF)이 
    함께 소멸하므로, 새 컨테이너로 부팅할 때 메모리와 디스크가 모두 초기화된 상태로 시작됩니다.
    
    확장
    호스트의 물리 경로를 컨테이너 내부의 Redis 데이터 디렉토리(`/data`)에 볼륨 매핑해야 하며, 
    Redis 설정 파일(`redis.conf`)에서 `appendonly yes` 또는 `save` 정책이 올바르게 가동 중인지 
    교차 검증하여 인프라 다운타임 시 세션 유실을 원천 차단해야 합니다.
    ```
    

</details>

---


<details>
<summary><strong>30. [K8s 라이프사이클 트러블슈팅] 쿠버네티스 파드가 계속 재시작됩니다. 로그를 보면 성공적으로 시작됩니다. 헬스 체크도 통과합니다. 그런데 30초 후에 죽어버립니다. 오류는 없습니다. 크래시도 없습니다. 그냥 사라집니다. 뭐가 그걸 죽이는 걸까요?</strong></summary>

30. [K8s 라이프사이클 트러블슈팅] 쿠버네티스 파드가 계속 재시작됩니다. 로그를 보면 성공적으로 시작됩니다. 헬스 체크도 통과합니다. 그런데 30초 후에 죽어버립니다. 오류는 없습니다. 크래시도 없습니다. 그냥 사라집니다. 뭐가 그걸 죽이는 걸까요?
    
    ```
    Kubernetes는 애플리케이션 자체는 정상적으로 작동하는 것처럼 보이더라도 파드를 종료할 수 있으므로, 
    먼저 OOMKill 오류나 프로브 실패 여부를 확인해 보는 것이 좋습니다.
    
    A. 호스트 노드의 자원 임계치 초과로 인한 'OOMKilled(Out Of Memory Killer)' 작동 또는 
    라이브니스 프로브(Liveness Probe) 설정 오류입니다.
    
    이유
    애플리케이션 자체 런타임 로그에 예외(Exception)나 크래시 흔적이 전혀 없음에도 프로세스가 즉각 
    소멸하는 것은 오케스트레이터(Kubelet)나 OS 커널 등의 외부 주체가 강제 시그널(SIGKILL)을 보냈기 때문입니다. 
    특히 Pod 메니페스트에 지정된 `resources.limits.memory` 한도를 초과하면 커널단에서 즉시 강제 종료합니다.
    
    확장
    `kubectl describe pod <파드명>` 명령을 실행하여 `Last State: Terminated` 항목의 `Reason` 코드가 
    `OOMKilled`인지 팩트 체크해야 합니다. 만약 메모리 문제가 아니라면 라이브니스 프로브의 
    `initialDelaySeconds`(초기 대기 시간)가 너무 짧아 초기화 중인 컨테이너를 비정상으로 오판했는지 
    검토해야 합니다.
    ```
    

</details>

---


<details>
<summary><strong>31. [파이프라인 단계 정의] 개발자 대다수가 아직도 다음의 차이를 모를 거야 : CI(Continuous Integration) &amp; CD(Continuous Deployment)의 차이는 무엇인가요?</strong></summary>

31. [파이프라인 단계 정의] 개발자 대다수가 아직도 다음의 차이를 모를 거야 : CI(Continuous Integration) & CD(Continuous Deployment)의 차이는 무엇인가요?
    
    ```json
    CI는 코드가 제대로 작동하는지 확인하는 것입니다.
    CD는 그 작동하는 코드를 프로덕션에 배포하는 것입니다.
    
    A. CI는 '지속적인 코드 통합 및 검증(품질 관리)' 단계이며, 
    CD는 '검증된 코드를 프로덕션에 자동 배포(인프라 반영)'하는 단계입니다.
    
    이유
    CI는 다수의 개발자가 변경한 코드가 메인 브랜치에 병합될 때마다 자동으로 빌드, 테스트, 
    정적 분석을 수행하여 결함을 조기에 발견하는 데 목적이 있습니다. CD는 CI 과정을 통과하여 
    안정성이 확보된 아티팩트를 수동 개입 없이 실제 운영 환경까지 
    안전하게 릴리스하는 자동화 프로세스이기 때문입니다.
    
    확장
    [이미지 처리 CI/CD 파이프라인]
    CI 단계에서 테스트 커버리지를 강제하고 빌드가 성공하면 도커 이미지를 생성하여 레지스트리에 푸시합니다. 
    이후 CD 단계에서 블루-그린(Blue-Green) 또는 카나리(Canary) 배포 전략을 통해 사용자 중단 없이 
    안전하게 인프라의 상태를 갱신하는 연속적 파이프라인을 구축하는 것이 핵심입니다.
    ```
    

</details>

---


<details>
<summary><strong>32. [도커 이미지 용량 최적화 결함] 이 <code>.dockerignore</code> 파일(<code>node_modules</code>, <code>.git</code>, <code>.env</code>)이 있습니다. </strong></summary>

32. [도커 이미지 용량 최적화 결함] 이 `.dockerignore` 파일(`node_modules`, `.git`, `.env`)이 있습니다. 
    
    도커 이미지가 여전히 890MB로, 예상했던 ~150MB가 아닙니다. 이 중에서 가장 가능성 있는 원인은 무엇인가요?
    
    A) .dockerignore가 COPY 명령에 적용되지 않음 — ADD를 사용하세요
    B) 기본 이미지 node:18이 큽니다. 수정: node:18-alpine으로 전환
    C) 모든 npm 의존성이 복사됨 devDependencies를 포함합니다. 수정: npm ci --only=production 실행
    D) B와 C 둘 다 — 기본 이미지가 크고 dev 의존성이 이미지를 부풀림
    
    ```json
    D) B와 C 모두
    
    → node:18은 Alpine에 비해 상대적으로 큽니다.
    → devDependencies를 설치하면 이미지 크기가 엄청나게 증가할 수 있습니다.
    → 이 둘을 함께 사용하면 ~150MB 이미지로 시작한 것이 수백 MB로 변하는 경우가 많습니다.
    
    일반적인 해결 방법: 
    → node:18-alpine을 사용하세요
    → npm ci --only=production 실행 (또는 npm ci --omit=dev)
    → 더 작은 이미지를 위해 멀티스테이지 빌드를 사용하세요.
    
    A. D) B와 C 모두 — 프로동션에 불필요한 기본(Base) 이미지의 물리적 크기가 비대하고, 
    개발용 의존성(devDependencies)이 이미지 내부에 그대로 포함되었기 때문입니다.
    
    이유
    기본 이미지로 `node:18`을 사용하면 빌드 도구 및 운영체제 전체 패키지가 포함되어 
    기본 용량 자체가 수백 MB를 초과합니다. 여기에 더해 빌드 시점에 테스트 툴이나 린터 등 
    개발 환경용 종속성(devDependencies)까지 전부 설치된 상태로 아티팩트가 고정되면 
    용량이 기하급수적으로 부풀어 오르기 때문입니다.
    
    확장
    해결을 위해서는 세 가지 최적화 전략을 결합해야 합니다. 
    첫째, 불필요한 패키지가 제거된 최소형 OS 기반인 `node:18-alpine` 이미지로 전환합니다. 
    둘째, 의존성 설치 시 `npm ci --only=production` 또는 `--omit=dev` 옵션을 강제하여 
    운영에 필수적인 라이브러리만 남깁니다. 
    셋째, 멀티스테이지 빌드(Multi-stage Build) 아키텍처를 도입하여 
    빌드 단계와 최종 실행 단계를 분리함으로써 최종 프로덕션 이미지 크기를 150MB 이하로 최소화합니다.
    ```
    

</details>

---


<details>
<summary><strong>33. [포트 기반 동일 출처 정책] 모든 주니어 개발자의 첫 번째 CORS 순간: 프론트엔드는 <code>localhost:3000</code>, 백엔드는 <code>localhost:8000</code>. 둘 다 로컬에서 실행 중인데 여전히 CORS 오류 발생. 왜?</strong></summary>

33. [포트 기반 동일 출처 정책] 모든 주니어 개발자의 첫 번째 CORS 순간: 프론트엔드는 `localhost:3000`, 백엔드는 `localhost:8000`. 둘 다 로컬에서 실행 중인데 여전히 CORS 오류 발생. 왜?
    
    ```bash
    CORS 오류는 브라우저가 동일 출처 정책을 강제하기 때문에 발생합니다: 
    localhost:3000과 localhost:8000은 포트가 다르기 때문에 서로 다른 출처로 간주되므로, 
    백엔드는 Access-Control-Allow-Origin 헤더를 통해 프론트엔드의 출처를 명시적으로 허용해야 합니다.
    
    A. 브라우저의 동일 출처 정책(Same-Origin Policy) 체계에서 '포트 번호의 다름'은 
    완전히 다른 출처(Origin)로 취급되기 때문입니다.
    
    이유
    브라우저는 보안을 위해 출처를 '프로토콜(http) + 호스트명(localhost) + 포트번호(:3000)'의 세 가지 조합으로 
    완벽히 일치할 때만 동일 출처로 판단합니다. 따라서 호스트가 같더라도 3000번 포트의 프론트가 
    8000번 포트의 백엔드로 자원을 요청하는 것은 허가되지 않은 교차 출처(Cross-Origin) 요청으로 
    간주되어 브라우저 단에서 선제적으로 차단(CORS 오류)하는 것입니다.
    
    확장
    이 문제를 해결하려면 백엔드(8000) 측 프레임워크 설정에서 CORS 미들웨어를 활성화하고, 
    응답 헤더에 `Access-Control-Allow-Origin: http://localhost:3000`을 명시적으로 추가하여 
    해당 프론트엔드 출처의 접근을 인가해야 합니다.
    ```
    

</details>

---


<details>
<summary><strong>34. [소프트웨어 기본 포트 컨벤션] 왜 항상? :3000 for Node / :8080 for Java / :5432 for Postgres / :6379 for Redis / :27017 for MongoDB 일까요?</strong></summary>

34. [소프트웨어 기본 포트 컨벤션] 왜 항상? :3000 for Node / :8080 for Java / :5432 for Postgres / :6379 for Redis / :27017 for MongoDB 일까요?
    
    ```bash
    기본값은 그냥 최소 저항의 길일 뿐입니다. 
    Node에는 3000, Java에는 8080, 필요할 때까지는 절대 바꾸지 마세요.
    
    A. 포트 충돌을 피하기 위한 역사적 관례와 개발 커뮤니티의 
    '최소 저항 경로(Path of Least Resistance)'로 굳어진 암묵적 표준입니다.
    
    이유
    HTTP 기본 포트인 80/443은 OS 커널 단에서 루트(Root) 권한을 요구하는 Privileged Port이므로 
    일반 개발 환경에서는 접근이 제한됩니다. 따라서 권한 제약이 없는 1024번 이상의 비권한(Unprivileged) 
    포트 영역 중에서 각 프레임워크와 도구들이 겹치지 않게 임의로 채택한 기본값들이 튜토리얼과 도큐먼트를 
    통해 수십 년간 전파되면서 산업 표준처럼 굳어졌기 때문입니다.
    
    확장
    개발 생산성 향상을 위해 로컬 환경에서는 이러한 기본값을 유지하는 것이 좋지만, 실제 프로덕션 서버로 
    배포하거나 도커 컨테이너로 감쌀 때는 보안 공격(알려진 포트 스캐닝)의 표적을 피하고 
    역방향 프록시(Nginx 등) 라우팅을 최적화하기 위해 환경 변수(Environment Variables)를 통해 
    포트 바인딩을 동적으로 오버라이드(Override)하는 유연한 아키텍처 설정이 필수적입니다.
    ```
    

</details>

---


<details>
<summary><strong>35. [IaC 핵심 명령어 이해] 테라폼(Terraform)에서 제일 중요한 명령어 3가지를 설명하시오.</strong></summary>

35. [IaC 핵심 명령어 이해] 테라폼(Terraform)에서 제일 중요한 명령어 3가지를 설명하시오.
    
    ```
    A. `terraform init`, `terraform plan`, `terraform apply` 입니다.
    
    이유
    테라폼의 Infrastructure as Code(IaC) 라이프사이클을 구성하는 3대 핵심 단계이기 때문입니다.
    - `init`: 작업 디렉토리를 초기화하고 필요한 프로바이더(AWS, GCP 등) 플러그인과 모듈을 다운로드합니다.
    - `plan`: 작성된 코드를 기반으로 현재 인프라 상태와 비교하여 어떤 리소스가 생성/수정/삭제될지 실행 계획을 미리 보여줍니다. (Dry-run 역할)
    - `apply`: `plan`에서 확인된 실행 계획을 클라우드 환경에 실제 프로비저닝(반영)합니다.
    
    확장
    실무에서는 `apply`를 로컬에서 직접 실행하기보다 CI/CD 파이프라인(GitHub Actions, Terraform Cloud 등)에 
    통합하여, 코드 리뷰를 거친 후 `plan` 결과를 검증하고 인프라 변경 이력을 추적 가능하게 관리하는 것이 모범 사례입니다.
    ```
    

</details>

---


<details>
<summary><strong>36. [심층 헬스 체크의 필요성] 사용자의 요청이 로드 밸런서를 거쳐 서버 A, B, C로 분배되고 있습니다. 서버 C는 '200 OK'를 반환하면서도 실제로는 잘못된 응답을 주는 고장 난 상태입니다. 로드 밸런서는 3개 서버 모두 건강하다고 판단해 C로도 요청을 보냅니다. 사용자들이 이 문제를 겪기 전에 어떻게 알아챌 수 있을까요?</strong></summary>

36. [심층 헬스 체크의 필요성] 사용자의 요청이 로드 밸런서를 거쳐 서버 A, B, C로 분배되고 있습니다. 서버 C는 '200 OK'를 반환하면서도 실제로는 잘못된 응답을 주는 고장 난 상태입니다. 로드 밸런서는 3개 서버 모두 건강하다고 판단해 C로도 요청을 보냅니다. 사용자들이 이 문제를 겪기 전에 어떻게 알아챌 수 있을까요?
    
    ```
    헬스 체크는 단순히 "살아있어?"라고 묻는 데 그쳐서는 안 돼요 — "올바른 상태야?"라고 물어야 해요.
    헬스 체크에서 합성 트랜잭션, 카나리 요청, 또는 응답 검증을 사용하세요. 
    그러면 로드 밸런서가 단순히 200 OK뿐 아니라 잘못된 응답도 감지할 수 있습니다.
    
    A. 로드 밸런서의 헬스 체크(Health Check) 엔드포인트에 
    응답 코드(200 OK) 확인을 넘어선 '응답 데이터 검증(Deep Health Check)' 로직을 추가해야 합니다.
    
    이유
    기본적인 L7 헬스 체크는 단순히 `/health` 경로가 HTTP 200을 반환하는지만 확인합니다. 서버 프로세스는 
    살아있으나 내부 캐시가 오염되었거나 로직에 결함이 생긴 경우를 걸러내지 못하므로, "살아있어?"가 아니라 
    "정상적으로 작동해?"를 물어보는 구조가 필요하기 때문입니다.
    
    확장
    합성 트랜잭션(Synthetic Transaction)이나 카나리(Canary) 테스트를 활용하여 헬스 체크 API 내부에 
    가상의 읽기/쓰기 검증 로직을 포함시키고, 예상되는 특정 문자열이나 JSON 구조가 반환되는지 정규식으로 
    검사(Pattern Matching)하도록 로드 밸런서 설정을 고도화해야 합니다.
    ```
    

</details>

---


<details>
<summary><strong>37. [오픈소스 API 도구 선정] 오픈소스 프로젝트를 위해 어떤 API 도구를 선택하시겠어요? (Postman, Insomnia, Bruno, Hoppscotch, Swagger)</strong></summary>

37. [오픈소스 API 도구 선정] 오픈소스 프로젝트를 위해 어떤 API 도구를 선택하시겠어요? (Postman, Insomnia, Bruno, Hoppscotch, Swagger)
    
    ```java
    A. 로컬 중심의 독립성, 완전한 오픈소스 철학, 텍스트 기반 형상 관리의 이점을 고려하여 
    Bruno 또는 Hoppscotch를 선택하겠습니다. (문서화 병행 시 Swagger)
    
    이유
    Postman과 Insomnia는 과거의 명성과 달리 클라우드 동기화 강제, 유료화 제약, 계정 생성 필수 정책 등 
    오픈소스 커뮤니티의 개방형 협업 환경과 마찰을 빚고 있습니다. Bruno는 모든 API 컬렉션을 로컬 `.bru` 
    텍스트 파일로 저장하여 Git을 통한 형상 관리와 PR(Pull Request) 리뷰에 완벽히 호환됩니다. 
    Hoppscotch는 설치조차 필요 없이 웹 브라우저에서 즉시 접근 가능한 강력한 경량 대안을 제공합니다.
    
    확장
    코드 레벨의 문서화가 핵심인 프로젝트라면, 소스 코드 주석으로부터 자동으로 API 스펙(OpenAPI 규격)을 
    생성하는 Swagger를 병행하는 것이 모범 사례입니다. "아키텍처 설계와 문서는 Swagger로 자동화하고, 
    개발 중인 API의 실행 및 스크립트 테스트는 Bruno로 형상 관리하는 구조"가 오픈소스 생태계에 
    가장 부합하는 파이프라인입니다.
    ```

언어/CS


</details>

---


<!-- migration-navigation:start -->  
[인터뷰 질문](../README.md)  
<!-- migration-navigation:end -->
