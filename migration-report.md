# Migration Report

## Source

Notion: 개발 기술 정리

- 분석 대상: 저장소에 제공된 `source/notion-export/`의 모든 195개 파일.
- 원본 ZIP은 제공되지 않았으므로 압축 파일과의 대조는 수행하지 않았다. 새 ZIP을 원본처럼 생성하지 않았다.
- 원본 파일 집합과 모든 파일의 SHA-256을 작업 시작 시점과 비교했다. 195개 모두 일치하며 원본 파일은 변경하지 않았다.
- Markdown 27개, PNG 164개, GIF 1개, CSV 2개, TXT 1개.
- 두 CSV를 모두 읽어 각각 27개 페이지의 이름과 속성을 Markdown의 제목·속성과 대조했다. 불일치 0건.
- 목차의 페이지 순서는 일반 CSV의 순서를 따른다. 각 문서 내부의 원문 순서와 반복 내용은 유지했다.

## Directory Structure

```text
DevTrack/
├── .gitattributes
├── README.md
├── source/
│   └── notion-export/                # 제공된 원본 195개 파일, 변경 없음
├── interview/
├── backend/
├── programming-languages/
├── security/
├── networking/
├── infrastructure/
├── devops/
├── database/
├── system-design/
├── tools/
├── open-source/
├── frontend/
├── design/
├── data-engineering/
├── ai/
├── assets/
└── migration-report.md
```

각 카테고리에는 README 목차가 있다. 원본 페이지마다 독립 문서를 유지했다. Infrastructure에는 Cloud, Kubernetes, Docker 🐳, 리눅스 문서를, DevOps에는 DevOps와 CI/CD 문서를, 데이터베이스에는 데이터베이스·Redis·Kafka 문서를 각각 연결했다. AI의 7개 페이지도 각각 독립 문서다. 모든 원본 `속성:` 값은 해당 문서에 그대로 남겼다.

인터뷰 질문은 원문 서두와 원래의 8개 분류 경계에 따라 README와 8개 문서로 나눴다. 아래 Source Files의 대상 순서대로 연결하면 원문의 순서가 복원된다. 분류 제목은 일반 Heading으로 유지했다.

## Conversion Rules Applied

- 개별 메모 제목을 `<details>` / `<summary><strong>…</strong></summary>`로 변환했다. 제목의 내용은 바꾸지 않았으며 제목 안의 강조, 코드, 링크는 HTML로 표시했다.
- 제목 수준이 섞인 페이지는 실제 독립 메모 경계를 확인했다. Kubernetes의 Control Plane과 Worker Nodes, 기술 메모 내부의 설명 Heading 등은 원래의 Heading으로 Toggle 안에 유지했다.
- 제목 없는 AI·Jev·API testing tool의 첫 메모는 원문 첫 문장을 접기 제목으로 사용하고 해당 본문 전체를 유지했다.
- 각 인터뷰 질문은 원래의 질문 번호·질문·선택지·답변·코드·들여쓰기를 Toggle 안에 그대로 유지했다. 접기 제목에도 원래 질문을 사용했다. 원문 목록 구조를 보존하기 위해 질문 본문을 삭제하지 않았다.
- 이미지와 TXT의 상대 경로만 실제 복사한 파일 위치로 변경했다. 외부 URL과 Notion URL은 변경하지 않았으며 외부 링크 유효성이나 기술적 사실은 검증하지 않았다.
- 중복 제거, 문장 수정, 기술 설명 추가, 코드 수정은 하지 않았다. 아래 두 쌍의 바깥 코드 fence 길이 조정만 적용했다.
- `.gitattributes`에서 원본과 첨부에 Git 줄바꿈 변환을 적용하지 않도록 지정했다. Git에 저장된 원본·첨부의 바이트도 보존한다.

### Code Fence Repairs

| Source | 원본 줄 | Before | After |
| --- | ---: | --- | --- |
| [Codex 3cbdbfd1e0fb80eb8246d3f50d30cc0a.md](source/notion-export/Codex%203cbdbfd1e0fb80eb8246d3f50d30cc0a.md) | 94 | <code>```</code> | <code>````</code> |
| [Codex 3cbdbfd1e0fb80eb8246d3f50d30cc0a.md](source/notion-export/Codex%203cbdbfd1e0fb80eb8246d3f50d30cc0a.md) | 326 | <code>```</code> | <code>````</code> |
| [바이브코딩 3c3dbfd1e0fb80a38fc2eff8e3be010e.md](source/notion-export/%EB%B0%94%EC%9D%B4%EB%B8%8C%EC%BD%94%EB%94%A9%203c3dbfd1e0fb80a38fc2eff8e3be010e.md) | 797 | <code>```markdown</code> | <code>````markdown</code> |
| [바이브코딩 3c3dbfd1e0fb80a38fc2eff8e3be010e.md](source/notion-export/%EB%B0%94%EC%9D%B4%EB%B8%8C%EC%BD%94%EB%94%A9%203c3dbfd1e0fb80a38fc2eff8e3be010e.md) | 1458 | <code>```</code> | <code>````</code> |

원본에 동일한 길이의 바깥·안쪽 backtick fence가 중첩되어 있었다. 정리본의 바깥 fence를 4개 backtick으로 늘려 내부 Markdown 및 코드를 보존했다. 내부 코드, 언어 표기, 주석, 들여쓰기와 순서는 바꾸지 않았다. 원본 파일의 fence는 변경하지 않았다.

## Source Files

모든 대상은 검증을 통과했다. 경로는 저장소 루트 기준이다.

| Source | Target (원문 순서) | Notion 속성 | Toggles | Status |
| --- | --- | --- | ---: | --- |
| [인터뷰 질문 33cdbfd1e0fb8053bdcbd9fbb2e6e4f0.md](source/notion-export/%EC%9D%B8%ED%84%B0%EB%B7%B0%20%EC%A7%88%EB%AC%B8%2033cdbfd1e0fb8053bdcbd9fbb2e6e4f0.md) | [interview/README.md](interview/README.md)<br>[interview/architecture.md](interview/architecture.md)<br>[interview/performance.md](interview/performance.md)<br>[interview/database.md](interview/database.md)<br>[interview/api-http.md](interview/api-http.md)<br>[interview/security.md](interview/security.md)<br>[interview/infrastructure.md](interview/infrastructure.md)<br>[interview/languages-cs.md](interview/languages-cs.md)<br>[interview/mindset.md](interview/mindset.md) | Interview | 286 | Complete |
| [Backend 336dbfd1e0fb8071b81ce67e9e2199e6.md](source/notion-export/Backend%20336dbfd1e0fb8071b81ce67e9e2199e6.md) | [backend/notes.md](backend/notes.md) | Backend | 65 | Complete |
| [Programming Languages 337dbfd1e0fb80cdb38fc7a6a4ec505d.md](source/notion-export/Programming%20Languages%20337dbfd1e0fb80cdb38fc7a6a4ec505d.md) | [programming-languages/notes.md](programming-languages/notes.md) | Backend | 10 | Complete |
| [보안 336dbfd1e0fb808ba1bfcb86a337f7ba.md](source/notion-export/%EB%B3%B4%EC%95%88%20336dbfd1e0fb808ba1bfcb86a337f7ba.md) | [security/notes.md](security/notes.md) | Security | 5 | Complete |
| [Networking 336dbfd1e0fb808db8bddae6f1f94a00.md](source/notion-export/Networking%20336dbfd1e0fb808db8bddae6f1f94a00.md) | [networking/notes.md](networking/notes.md) | Infra | 9 | Complete |
| [Cloud 336dbfd1e0fb80eabe3cd640d347349e.md](source/notion-export/Cloud%20336dbfd1e0fb80eabe3cd640d347349e.md) | [infrastructure/cloud.md](infrastructure/cloud.md) | Infra | 12 | Complete |
| [DevOps 33cdbfd1e0fb800698f1f8bf31c5dd3d.md](source/notion-export/DevOps%2033cdbfd1e0fb800698f1f8bf31c5dd3d.md) | [devops/notes.md](devops/notes.md) | DevOps | 15 | Complete |
| [CI CD 337dbfd1e0fb8097b517d53f74c26798.md](source/notion-export/CI%20CD%20337dbfd1e0fb8097b517d53f74c26798.md) | [devops/ci-cd.md](devops/ci-cd.md) | DevOps | 15 | Complete |
| [Kubernetes 338dbfd1e0fb8066a7ebc86cf8a6769c.md](source/notion-export/Kubernetes%20338dbfd1e0fb8066a7ebc86cf8a6769c.md) | [infrastructure/kubernetes.md](infrastructure/kubernetes.md) | Infra | 14 | Complete |
| [Docker 🐳 338dbfd1e0fb805abffcdc82c13eaa65.md](source/notion-export/Docker%20%F0%9F%90%B3%20338dbfd1e0fb805abffcdc82c13eaa65.md) | [infrastructure/docker.md](infrastructure/docker.md) | Infra | 18 | Complete |
| [Redis 35cdbfd1e0fb80ac9bbcf9d1e944ee92.md](source/notion-export/Redis%2035cdbfd1e0fb80ac9bbcf9d1e944ee92.md) | [database/redis.md](database/redis.md) | Backend | 2 | Complete |
| [Kafka 338dbfd1e0fb8017bbf0f4b789589498.md](source/notion-export/Kafka%20338dbfd1e0fb8017bbf0f4b789589498.md) | [database/kafka.md](database/kafka.md) | Backend | 2 | Complete |
| [시스템 디자인 33cdbfd1e0fb8089b2f9ed165c8b65a5.md](source/notion-export/%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EB%94%94%EC%9E%90%EC%9D%B8%2033cdbfd1e0fb8089b2f9ed165c8b65a5.md) | [system-design/notes.md](system-design/notes.md) | Architecture | 25 | Complete |
| [리눅스 33ddbfd1e0fb80a8bf99c9604c19ec43.md](source/notion-export/%EB%A6%AC%EB%88%85%EC%8A%A4%2033ddbfd1e0fb80a8bf99c9604c19ec43.md) | [infrastructure/linux.md](infrastructure/linux.md) | Infra | 28 | Complete |
| [데이터베이스 33fdbfd1e0fb80bea6e5c71df89fc9a9.md](source/notion-export/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%2033fdbfd1e0fb80bea6e5c71df89fc9a9.md) | [database/notes.md](database/notes.md) | Backend | 28 | Complete |
| [API testing tool 338dbfd1e0fb809ab270d7d599e65d16.md](source/notion-export/API%20testing%20tool%20338dbfd1e0fb809ab270d7d599e65d16.md) | [tools/api-testing.md](tools/api-testing.md) | Backend | 3 | Complete |
| [오픈소스 351dbfd1e0fb80c98910f4a1924cb373.md](source/notion-export/%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4%20351dbfd1e0fb80c98910f4a1924cb373.md) | [open-source/notes.md](open-source/notes.md) | Free | 3 | Complete |
| [프론트엔드 358dbfd1e0fb80f79ba6f07ec19ae743.md](source/notion-export/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C%20358dbfd1e0fb80f79ba6f07ec19ae743.md) | [frontend/notes.md](frontend/notes.md) | FrontEnd | 4 | Complete |
| [디자인 3dadbfd1e0fb80988f72c01a6667a35d.md](source/notion-export/%EB%94%94%EC%9E%90%EC%9D%B8%203dadbfd1e0fb80988f72c01a6667a35d.md) | [design/notes.md](design/notes.md) | Design | 10 | Complete |
| [데이터 엔지니어링 3b5dbfd1e0fb807792cac6fda23eec3d.md](source/notion-export/%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A7%81%203b5dbfd1e0fb807792cac6fda23eec3d.md) | [data-engineering/notes.md](data-engineering/notes.md) | Architecture | 5 | Complete |
| [AI 33ddbfd1e0fb802488caf63be99c4ae4.md](source/notion-export/AI%2033ddbfd1e0fb802488caf63be99c4ae4.md) | [ai/notes.md](ai/notes.md) | AI | 51 | Complete |
| [바이브코딩 3c3dbfd1e0fb80a38fc2eff8e3be010e.md](source/notion-export/%EB%B0%94%EC%9D%B4%EB%B8%8C%EC%BD%94%EB%94%A9%203c3dbfd1e0fb80a38fc2eff8e3be010e.md) | [ai/vibe-coding.md](ai/vibe-coding.md) | AI | 41 | Complete |
| [AI 에이전트 3addbfd1e0fb807eb0ebdf3bf05f8ea8.md](source/notion-export/AI%20%EC%97%90%EC%9D%B4%EC%A0%84%ED%8A%B8%203addbfd1e0fb807eb0ebdf3bf05f8ea8.md) | [ai/agents.md](ai/agents.md) | AI | 41 | Complete |
| [RAG 3afdbfd1e0fb805db6c9f13ae46d983f.md](source/notion-export/RAG%203afdbfd1e0fb805db6c9f13ae46d983f.md) | [ai/rag.md](ai/rag.md) | AI | 21 | Complete |
| [Claude 3cbdbfd1e0fb80f38fb9d99569eaec68.md](source/notion-export/Claude%203cbdbfd1e0fb80f38fb9d99569eaec68.md) | [ai/claude.md](ai/claude.md) | AI | 36 | Complete |
| [Codex 3cbdbfd1e0fb80eb8246d3f50d30cc0a.md](source/notion-export/Codex%203cbdbfd1e0fb80eb8246d3f50d30cc0a.md) | [ai/codex.md](ai/codex.md) | AI | 42 | Complete |
| [Jev 3dfdbfd1e0fb80ab9474f4d5dc8ce95f.md](source/notion-export/Jev%203dfdbfd1e0fb80ab9474f4d5dc8ce95f.md) | [ai/jev.md](ai/jev.md) | AI | 25 | Complete |

## Assets

- Source images: 165 (PNG 164, GIF 1)
- Migrated images: 165
- Missing images: 0
- Source other assets: 3 (CSV 2, TXT 1)
- Migrated other assets: 3
- Missing other assets: 0
- 원본 이미지 참조 165개를 모두 처리했다. 모든 상대 경로의 파일이 실제로 존재한다.
- 미참조 이미지: 0. CSV 2개도 별도 첨부로 복사했다.
- 최종 경로 및 파일명 충돌: 0 (대소문자를 구분하지 않고 검사).
- 첨부 168개 모두 원본과 SHA-256이 일치한다.

### Asset Mapping and SHA-256

각 행의 SHA-256은 원본과 대상 양쪽에서 일치한 값이다.

| Source | Target | Status | SHA-256 |
| --- | --- | --- | --- |
| [1785241869033.gif](source/notion-export/1785241869033.gif) | [assets/agents/1785241869033.gif](assets/agents/1785241869033.gif) | Complete | `e2d1720aaba4f92b94ea4f35828d8a72e774781ca38eb6a3d5b6111d52b5dc91` |
| [image 1.png](source/notion-export/image%201.png) | [assets/backend/image-001.png](assets/backend/image-001.png) | Complete | `a2fa22055c9d901cea52d7a20cc8a58268039a5acdf17cb1924614d3c91cd687` |
| [image 10.png](source/notion-export/image%2010.png) | [assets/backend/image-010.png](assets/backend/image-010.png) | Complete | `2d4025c4c8f07f89b644a97ee1cf44f94522583029e18dbf17b414c70e7b5406` |
| [image 100.png](source/notion-export/image%20100.png) | [assets/agents/image-100.png](assets/agents/image-100.png) | Complete | `d83d5f8847637af1a0cdda82c7e72408fcd3203cd334abe563316a4175de0668` |
| [image 101.png](source/notion-export/image%20101.png) | [assets/rag/image-101.png](assets/rag/image-101.png) | Complete | `60aaaded83fe722846dc2e39c280c485148c69973784f0a889865c1f76e21edc` |
| [image 102.png](source/notion-export/image%20102.png) | [assets/rag/image-102.png](assets/rag/image-102.png) | Complete | `9248c32a400afa447ac1e5b942ea5e2fb01a585e0dc90cc0104ab334fe8db3ad` |
| [image 103.png](source/notion-export/image%20103.png) | [assets/rag/image-103.png](assets/rag/image-103.png) | Complete | `2f93f096a65b28f351cd5b3b24a3f2c03ade14b9b3e454af912ba25effe3e82e` |
| [image 104.png](source/notion-export/image%20104.png) | [assets/rag/image-104.png](assets/rag/image-104.png) | Complete | `4ab52d98a99785e77bc698f9de6653899d3fb770a29e6592301c1862c05de381` |
| [image 105.png](source/notion-export/image%20105.png) | [assets/rag/image-105.png](assets/rag/image-105.png) | Complete | `019a763b9d31a92c61c2aae3a2700c75e4b1a96e93f6103f604775a20d612bd6` |
| [image 106.png](source/notion-export/image%20106.png) | [assets/rag/image-106.png](assets/rag/image-106.png) | Complete | `fb1a7836108fa7e6985ee7dd82f74c5a0ef3d279ab5e60e5a715dfab5fafabe0` |
| [image 107.png](source/notion-export/image%20107.png) | [assets/rag/image-107.png](assets/rag/image-107.png) | Complete | `1ba8a9090a2331a07eefaa88fa505e672928d8b126974e59c4dc620e0770d698` |
| [image 108.png](source/notion-export/image%20108.png) | [assets/rag/image-108.png](assets/rag/image-108.png) | Complete | `2678ec7729990efe0aa3aff89c5e7567df0ae0567304f46fc338ec77b802cda1` |
| [image 109.png](source/notion-export/image%20109.png) | [assets/rag/image-109.png](assets/rag/image-109.png) | Complete | `1ec8a2eda623086b4e6cafbb1c7a2961ae4f28da164fb18cd2c2a64a9465413b` |
| [image 11.png](source/notion-export/image%2011.png) | [assets/backend/image-011.png](assets/backend/image-011.png) | Complete | `4ee9e30613336ffda2b877b8ebe3e52698cb723a9c1b48c2f89181259b15fab5` |
| [image 110.png](source/notion-export/image%20110.png) | [assets/rag/image-110.png](assets/rag/image-110.png) | Complete | `37776fd0e16b84120cf72918675f2caccbecc47b0d9b85941cd66df94467c793` |
| [image 111.png](source/notion-export/image%20111.png) | [assets/rag/image-111.png](assets/rag/image-111.png) | Complete | `b38641d52b4ac9b88d6edcd54fac69e68b81c1e1a8b7e1cf1c602b7ae2bc5d2c` |
| [image 112.png](source/notion-export/image%20112.png) | [assets/rag/image-112.png](assets/rag/image-112.png) | Complete | `33a991b893eb5c6033ee24e15383b7bc4d21b912fc0c88dbdf60ed2db1551aa3` |
| [image 113.png](source/notion-export/image%20113.png) | [assets/rag/image-113.png](assets/rag/image-113.png) | Complete | `411e8756729cdd9d52ffee5b4878d050be29f082f484c54ab0709514bd827892` |
| [image 114.png](source/notion-export/image%20114.png) | [assets/rag/image-114.png](assets/rag/image-114.png) | Complete | `f678b777940fcb9979e31f08f01d72bfb5d46eb370a57ce18e9011a320228ce3` |
| [image 115.png](source/notion-export/image%20115.png) | [assets/rag/image-115.png](assets/rag/image-115.png) | Complete | `695e4782cedffe0a5593b645f49135c1c49c6ba3c5b5d71f4569092e18332938` |
| [image 116.png](source/notion-export/image%20116.png) | [assets/rag/image-116.png](assets/rag/image-116.png) | Complete | `4f8a48e4f6d2b05dea193bae69a1f726cd5e1dede53339f877ec84489a9e2db6` |
| [image 117.png](source/notion-export/image%20117.png) | [assets/rag/image-117.png](assets/rag/image-117.png) | Complete | `5c48847d75680f91f61f5f92ae02c1aea961ff271f32468ca034bdc26c6098d3` |
| [image 118.png](source/notion-export/image%20118.png) | [assets/rag/image-118.png](assets/rag/image-118.png) | Complete | `b84be3526d26bb5a79f401f9a297448646b7b22267ae9d0abe83a258e08572da` |
| [image 119.png](source/notion-export/image%20119.png) | [assets/rag/image-119.png](assets/rag/image-119.png) | Complete | `910d00ba13baad329eb8369fda2cee5655d1bc70366252509d8eb7682fba4a17` |
| [image 12.png](source/notion-export/image%2012.png) | [assets/security/image-012.png](assets/security/image-012.png) | Complete | `32071ca6c047409977cca9c2d302ac52eb9eecf06f87dd9d87979f4d3dde4bc4` |
| [image 120.png](source/notion-export/image%20120.png) | [assets/rag/image-120.png](assets/rag/image-120.png) | Complete | `a05c5feb12247e4e6330117da68150cea0b64f9ebf5c479fe21f6e13c3ab1e6b` |
| [image 121.png](source/notion-export/image%20121.png) | [assets/data-engineering/image-121.png](assets/data-engineering/image-121.png) | Complete | `d4d9582cf5cd1f1ab56519199a10ef70cc300f34a8c0d31b512d871fa4e0d9b3` |
| [image 122.png](source/notion-export/image%20122.png) | [assets/vibe-coding/image-122.png](assets/vibe-coding/image-122.png) | Complete | `d6416eb2a3e46fb192d86325a0326c976dc4427ed254695a88d4d8bfd64dd210` |
| [image 123.png](source/notion-export/image%20123.png) | [assets/vibe-coding/image-123.png](assets/vibe-coding/image-123.png) | Complete | `2c741b320306cd60ac1ccb962ee944adef345e7cfb6a4258028873f4967d38d6` |
| [image 124.png](source/notion-export/image%20124.png) | [assets/vibe-coding/image-124.png](assets/vibe-coding/image-124.png) | Complete | `663c325a8b03f1f853f4770e805ea2e52cf06b7cfa9f65068ab904451dedd70d` |
| [image 125.png](source/notion-export/image%20125.png) | [assets/vibe-coding/image-125.png](assets/vibe-coding/image-125.png) | Complete | `8456fc3d44e74d9b4e4b07e658525cce4c52ea5896a336b651debccb07833e53` |
| [image 126.png](source/notion-export/image%20126.png) | [assets/vibe-coding/image-126.png](assets/vibe-coding/image-126.png) | Complete | `644e9096947e60b853fcc75fd5d3e94b144e816328c2deafa7d9fa2e31a24c63` |
| [image 127.png](source/notion-export/image%20127.png) | [assets/vibe-coding/image-127.png](assets/vibe-coding/image-127.png) | Complete | `cd9e06df7f14955f47d84716e652241bd2c2d8a24071aed8556284c39c5c66b5` |
| [image 128.png](source/notion-export/image%20128.png) | [assets/vibe-coding/image-128.png](assets/vibe-coding/image-128.png) | Complete | `6165e15e3f71a765620c3899e894f3aa966639e570ef9d07a05f874cfd5d80b3` |
| [image 129.png](source/notion-export/image%20129.png) | [assets/vibe-coding/image-129.png](assets/vibe-coding/image-129.png) | Complete | `2a9d4da5cfea6a469e75954c83ea3face2fae316d5d3f65495c487197c348e05` |
| [image 13.png](source/notion-export/image%2013.png) | [assets/security/image-013.png](assets/security/image-013.png) | Complete | `ebba5fc6bfe559cc4a92d3c0c632b52cbe6fb9bb0ca90d94031574d44a98fb0d` |
| [image 130.png](source/notion-export/image%20130.png) | [assets/vibe-coding/image-130.png](assets/vibe-coding/image-130.png) | Complete | `92de1bffbd9841d281fcb23e628fbd86a55675f23b8350491dbfd012ac6e33c6` |
| [image 131.png](source/notion-export/image%20131.png) | [assets/vibe-coding/image-131.png](assets/vibe-coding/image-131.png) | Complete | `0bb8b2f206c0698bb887aeadbebd9665f012b785e395e10ae3c037ce8e3977a2` |
| [image 132.png](source/notion-export/image%20132.png) | [assets/vibe-coding/image-132.png](assets/vibe-coding/image-132.png) | Complete | `9840b478297ff80590b3b574526ee20bf745499a61c94c73f3f4b3d4f099378d` |
| [image 133.png](source/notion-export/image%20133.png) | [assets/vibe-coding/image-133.png](assets/vibe-coding/image-133.png) | Complete | `49855743dcd680029bb2fed57bde10c0c252860f8c789d3db38e7998c8c4a402` |
| [image 134.png](source/notion-export/image%20134.png) | [assets/vibe-coding/image-134.png](assets/vibe-coding/image-134.png) | Complete | `7b26bdddef40ffd08bfd3a2cd47ef6e880ac30cc1c57ba2ccea59b5b1ac07328` |
| [image 135.png](source/notion-export/image%20135.png) | [assets/codex/image-135.png](assets/codex/image-135.png) | Complete | `52abf4fb970a538c23832b5571b63e545104079cdd76bf4a6a0dc852579e73ed` |
| [image 136.png](source/notion-export/image%20136.png) | [assets/codex/image-136.png](assets/codex/image-136.png) | Complete | `ce7ba7454940ca39302127326b2d0d7a0d35d45f4069ad25b6b4f21fa3190d87` |
| [image 137.png](source/notion-export/image%20137.png) | [assets/codex/image-137.png](assets/codex/image-137.png) | Complete | `7eeae1e545747fce3bda37792029eee0156622d3ba28e26ee1463c5192e9db09` |
| [image 138.png](source/notion-export/image%20138.png) | [assets/codex/image-138.png](assets/codex/image-138.png) | Complete | `a53d011bde25dde88b7ca365633a1722b2919eae634e906f3a1424415df5f515` |
| [image 139.png](source/notion-export/image%20139.png) | [assets/codex/image-139.png](assets/codex/image-139.png) | Complete | `920c76bd6215ac0bfb058b61043c84a4c16561d8fe6c50df7f6645a029766c83` |
| [image 14.png](source/notion-export/image%2014.png) | [assets/networking/image-014.png](assets/networking/image-014.png) | Complete | `54ea440c0b938008e6eed8be03a98f946462cd51141d97ec081519c48690a040` |
| [image 140.png](source/notion-export/image%20140.png) | [assets/codex/image-140.png](assets/codex/image-140.png) | Complete | `1a8fab6552c0c20df9cd7737402ace5f1e2caeb2b3403c55b09c0748fe3fa03a` |
| [image 141.png](source/notion-export/image%20141.png) | [assets/codex/image-141.png](assets/codex/image-141.png) | Complete | `067cbcf9782772566ced93049626904b127cffede7fd200eb2d23e7a246759c9` |
| [image 142.png](source/notion-export/image%20142.png) | [assets/codex/image-142.png](assets/codex/image-142.png) | Complete | `949119b11d924a4d4ef3b169f2004ff200f4917d24975b20cef4a2a6f80935fa` |
| [image 143.png](source/notion-export/image%20143.png) | [assets/codex/image-143.png](assets/codex/image-143.png) | Complete | `b4a887b9e9e64d601f052da2c0a9b26babbf198a3479f78b5886442ba028c32e` |
| [image 144.png](source/notion-export/image%20144.png) | [assets/codex/image-144.png](assets/codex/image-144.png) | Complete | `99cf8af39ba1b9b83a6e79d3b4abebbf09f1060edfe09863ee38b52bec7512ab` |
| [image 145.png](source/notion-export/image%20145.png) | [assets/codex/image-145.png](assets/codex/image-145.png) | Complete | `95c01309b622440ace4dbfa7f836266e2f132b0b218b494902517ff474a079ba` |
| [image 146.png](source/notion-export/image%20146.png) | [assets/claude/image-146.png](assets/claude/image-146.png) | Complete | `a4df1c0fcf9e095cf5da70b983d3d16171db94401d86a51bf288f28efa381690` |
| [image 147.png](source/notion-export/image%20147.png) | [assets/claude/image-147.png](assets/claude/image-147.png) | Complete | `c65b46877c8db9c7660b1a0a30753f6451a6f685d13fe52dec397813542c94cc` |
| [image 148.png](source/notion-export/image%20148.png) | [assets/claude/image-148.png](assets/claude/image-148.png) | Complete | `72ef2e3b73fe807aa1d951291ea93da83bed262d7acfe50973ae54afdc3007de` |
| [image 149.png](source/notion-export/image%20149.png) | [assets/claude/image-149.png](assets/claude/image-149.png) | Complete | `7179a3aee391eb0f2af4153a320b9858c7c3f9703d733cdcedc93d4b0c3c5782` |
| [image 15.png](source/notion-export/image%2015.png) | [assets/networking/image-015.png](assets/networking/image-015.png) | Complete | `f23c24492515404c91fa4ff9168b8e60c21e260d86f08ff8f203f3daf53b2775` |
| [image 150.png](source/notion-export/image%20150.png) | [assets/claude/image-150.png](assets/claude/image-150.png) | Complete | `091677c9bf298e6d05bc53d2b063ad476610f4d2fb41140707c9db34efbb322c` |
| [image 151.png](source/notion-export/image%20151.png) | [assets/claude/image-151.png](assets/claude/image-151.png) | Complete | `ed2545c7033d4094b003544056f23e2e3217df55299e352fc1c52925765f60b7` |
| [image 152.png](source/notion-export/image%20152.png) | [assets/claude/image-152.png](assets/claude/image-152.png) | Complete | `50214311853b7634da4ea0436cb0e26e07328deebf4f3b37510ae2e37670f842` |
| [image 153.png](source/notion-export/image%20153.png) | [assets/claude/image-153.png](assets/claude/image-153.png) | Complete | `2581ece12e85225475de14e5ac68ab2636436d76cb3a485e18724d5a6b22e5f8` |
| [image 154.png](source/notion-export/image%20154.png) | [assets/claude/image-154.png](assets/claude/image-154.png) | Complete | `40f447ef42aff69871e551df6b2c68a337cd4a4c2544f930ebc3fd795c1df97e` |
| [image 155.png](source/notion-export/image%20155.png) | [assets/claude/image-155.png](assets/claude/image-155.png) | Complete | `97841547384d747a641f55d88e787d3040fa3cc0e154cb681a545f811f15dc2a` |
| [image 156.png](source/notion-export/image%20156.png) | [assets/claude/image-156.png](assets/claude/image-156.png) | Complete | `ec803d435167cff4acc1e671d72332a1fb9ac7af30f2bf6ddd6162af587dcd24` |
| [image 157.png](source/notion-export/image%20157.png) | [assets/design/image-157.png](assets/design/image-157.png) | Complete | `e114853c834791180b68780ba0be230f82cd6080eeec6b00b8d8e6ed3c531736` |
| [image 158.png](source/notion-export/image%20158.png) | [assets/design/image-158.png](assets/design/image-158.png) | Complete | `f9b7eb3c87792d9eb6e445fb82a869ea2c3ee718f765556bbf78be496ac4cc26` |
| [image 159.png](source/notion-export/image%20159.png) | [assets/design/image-159.png](assets/design/image-159.png) | Complete | `1ffad286571c44b8dba33d4433d44518b321808ac7158b93de04c3f9a14f6674` |
| [image 16.png](source/notion-export/image%2016.png) | [assets/networking/image-016.png](assets/networking/image-016.png) | Complete | `4e64c4e011ac93c90f551a6feeeec8b6bc978adec44e19acfcb823fcbf5dc32f` |
| [image 160.png](source/notion-export/image%20160.png) | [assets/jev/image-160.png](assets/jev/image-160.png) | Complete | `0386cb6eadaf5358da32a37293e4fa7f31a42f9273e59c5b4356c2f6d7454d28` |
| [image 161.png](source/notion-export/image%20161.png) | [assets/jev/image-161.png](assets/jev/image-161.png) | Complete | `382331ba279ac5bdbab9e9357b0373e59ffcebc681397425fc722c1e0e5a5a02` |
| [image 162.png](source/notion-export/image%20162.png) | [assets/jev/image-162.png](assets/jev/image-162.png) | Complete | `1aaeb1ec7981cb4db933bf513ee30e1f8ea2e36c92c1352933ecda3dc0b4c228` |
| [image 163.png](source/notion-export/image%20163.png) | [assets/jev/image-163.png](assets/jev/image-163.png) | Complete | `166f99a6cebed3ea3d2eec20a887a30b426a88ab0e538f09a8d17e9eab5e4bbf` |
| [image 17.png](source/notion-export/image%2017.png) | [assets/cloud/image-017.png](assets/cloud/image-017.png) | Complete | `e5569de4591c6ae404fc0e5b8bd0be6c3c69892e3de5cf7e44da26dc4c977a94` |
| [image 18.png](source/notion-export/image%2018.png) | [assets/cloud/image-018.png](assets/cloud/image-018.png) | Complete | `dd84c8aa107f0b67ba2aa803fd709a736d720e6a34b6d2e5941aef5918896399` |
| [image 19.png](source/notion-export/image%2019.png) | [assets/cloud/image-019.png](assets/cloud/image-019.png) | Complete | `b1b1638e8e0d34c491c476d9727f2a13078f18419ead666236f43e0c5a3da5e6` |
| [image 2.png](source/notion-export/image%202.png) | [assets/backend/image-002.png](assets/backend/image-002.png) | Complete | `f181cca699c5492321d7766f3bc061d6640bb90cd4d55f3bd9907a433cd00877` |
| [image 20.png](source/notion-export/image%2020.png) | [assets/ci-cd/image-020.png](assets/ci-cd/image-020.png) | Complete | `ede72e608fab9344879c1b1542c6c58808acfa871c9a62c37f8f884414d438e0` |
| [image 21.png](source/notion-export/image%2021.png) | [assets/ci-cd/image-021.png](assets/ci-cd/image-021.png) | Complete | `d5298bdcb8c445d834e714cea117d0617f3e29f588492390cb419422f7df0c29` |
| [image 22.png](source/notion-export/image%2022.png) | [assets/ci-cd/image-022.png](assets/ci-cd/image-022.png) | Complete | `248caddefcdfb815ceddd5cbd5815becc309d275f563c46fc1433bc8f4580255` |
| [image 23.png](source/notion-export/image%2023.png) | [assets/kafka/image-023.png](assets/kafka/image-023.png) | Complete | `9247f2a59b60472b5bff97aa093bf64f5d92dd65c1dff243b0f3fbf472587d36` |
| [image 24.png](source/notion-export/image%2024.png) | [assets/kafka/image-024.png](assets/kafka/image-024.png) | Complete | `206269d22c4edd9fbace670d89c7395c08a4a0f30fa8540ca6be262d4e6bbbc9` |
| [image 25.png](source/notion-export/image%2025.png) | [assets/docker/image-025.png](assets/docker/image-025.png) | Complete | `8f87678201535bac0478df5d7054697bf97d6452df605c06b10f01e7dfbf59e0` |
| [image 26.png](source/notion-export/image%2026.png) | [assets/docker/image-026.png](assets/docker/image-026.png) | Complete | `3eb73d45cfb7eee1fedb45be50a251ffad9efa6cf74fc098ed9d068b0a190439` |
| [image 27.png](source/notion-export/image%2027.png) | [assets/docker/image-027.png](assets/docker/image-027.png) | Complete | `5c0c92ad22879d3512f31bd2626ede13b699673546c037b801d955f98464bc15` |
| [image 28.png](source/notion-export/image%2028.png) | [assets/docker/image-028.png](assets/docker/image-028.png) | Complete | `4f3e2c3c0f33d6c89b37d823e6075090cb28bd9a22fcd5ba703e9a28302a4682` |
| [image 29.png](source/notion-export/image%2029.png) | [assets/docker/image-029.png](assets/docker/image-029.png) | Complete | `6f3575e0e3b8b9eb7f27bddef80994aa3591ee6d6df2edb076816d8eccde8f06` |
| [image 3.png](source/notion-export/image%203.png) | [assets/backend/image-003.png](assets/backend/image-003.png) | Complete | `ff82749e37b7b8b9cd30ec14fc8b96cc69712d79a2e4a576bf24fb2d37dee16d` |
| [image 30.png](source/notion-export/image%2030.png) | [assets/docker/image-030.png](assets/docker/image-030.png) | Complete | `a352084bce4419b809f48b126760cdc2de8bf273323b4c1a4ca8956ec738e392` |
| [image 31.png](source/notion-export/image%2031.png) | [assets/docker/image-031.png](assets/docker/image-031.png) | Complete | `6b7559a61b65068e7def3050161be723ed201544bd7e42dcd6d77eaa66a3f0fc` |
| [image 32.png](source/notion-export/image%2032.png) | [assets/docker/image-032.png](assets/docker/image-032.png) | Complete | `a242eb4bcfcfda18ce08430b2e1929636b6d921507fbc8da48edea69f78c8d2c` |
| [image 33.png](source/notion-export/image%2033.png) | [assets/docker/image-033.png](assets/docker/image-033.png) | Complete | `9848eaa1cffdaf5ff8f4b6f669ae36cb5a879d5bad23518695116801b8d9095a` |
| [image 34.png](source/notion-export/image%2034.png) | [assets/kubernetes/image-034.png](assets/kubernetes/image-034.png) | Complete | `ca6dbe915273d9072a99269d33402318654ab1edf5d44876d1d033d8ff173495` |
| [image 35.png](source/notion-export/image%2035.png) | [assets/kubernetes/image-035.png](assets/kubernetes/image-035.png) | Complete | `66f7bdc887abca9878695a91f41f47a827d228680abf3ac8869378ea047d8a83` |
| [image 36.png](source/notion-export/image%2036.png) | [assets/kubernetes/image-036.png](assets/kubernetes/image-036.png) | Complete | `a9b0d3946a9ce1ecc3deef136b98908747595479223b974dbb45ab69636f01f4` |
| [image 37.png](source/notion-export/image%2037.png) | [assets/kubernetes/image-037.png](assets/kubernetes/image-037.png) | Complete | `cce9ecad01f47b67c2a33fdd00a89d64a5c55837f7862c701a62dba652978e8c` |
| [image 38.png](source/notion-export/image%2038.png) | [assets/kubernetes/image-038.png](assets/kubernetes/image-038.png) | Complete | `f7cfa2798d6e3bc2f1e3db80f7c9f7b204d11c9413a12978d9da6b582095f3fc` |
| [image 39.png](source/notion-export/image%2039.png) | [assets/kubernetes/image-039.png](assets/kubernetes/image-039.png) | Complete | `19a06811ff4f55a964f53d90c0357db379160d2a0a0c5bdb36dce4050dcb624c` |
| [image 4.png](source/notion-export/image%204.png) | [assets/backend/image-004.png](assets/backend/image-004.png) | Complete | `038b195bcb2eb575a94d31e0b263db69c69815d5c3cfc75cea77c2ac3dd84980` |
| [image 40.png](source/notion-export/image%2040.png) | [assets/kubernetes/image-040.png](assets/kubernetes/image-040.png) | Complete | `3468aaad91c4265e5f775c443e4609b6b17d8fb51ad8b996dc40d251e61284ca` |
| [image 41.png](source/notion-export/image%2041.png) | [assets/kubernetes/image-041.png](assets/kubernetes/image-041.png) | Complete | `9eef4172398b6fd146153b309fbb73ee7f6e546c23a886738e082d53bcebfc8d` |
| [image 42.png](source/notion-export/image%2042.png) | [assets/api-testing/image-042.png](assets/api-testing/image-042.png) | Complete | `da8cfc8512999dd5e904fceede2cb2e2bf82d420e084f7abee358665e35191dc` |
| [image 43.png](source/notion-export/image%2043.png) | [assets/api-testing/image-043.png](assets/api-testing/image-043.png) | Complete | `0dec30c9141ac9f136dc3cd4428ec1a494e6d7a754f10c8b649b6c75571bb200` |
| [image 44.png](source/notion-export/image%2044.png) | [assets/api-testing/image-044.png](assets/api-testing/image-044.png) | Complete | `f53200029836994c049b1f80419937fdefe38b7cf8934ec2623799a6b5026411` |
| [image 45.png](source/notion-export/image%2045.png) | [assets/api-testing/image-045.png](assets/api-testing/image-045.png) | Complete | `04da06b3b325a503011b5d33223845a8fe3faa6d92f6095638e985d64539cab2` |
| [image 46.png](source/notion-export/image%2046.png) | [assets/api-testing/image-046.png](assets/api-testing/image-046.png) | Complete | `f4704bdba663ae32294c4e26d8c6fc30d3971a03e5ce674ff19630a868c37b9b` |
| [image 47.png](source/notion-export/image%2047.png) | [assets/devops/image-047.png](assets/devops/image-047.png) | Complete | `28eefc23c49133988edf66079ffc255a54d58c7b1be8301c48c57dea7cd866ed` |
| [image 48.png](source/notion-export/image%2048.png) | [assets/devops/image-048.png](assets/devops/image-048.png) | Complete | `557cce59f33abb339fa8983a772b393a8b5d3204785e0a9e7f994baa0e2e023a` |
| [image 49.png](source/notion-export/image%2049.png) | [assets/devops/image-049.png](assets/devops/image-049.png) | Complete | `937512df757d381d9106ba178989357d2f5257eed887ae372d5c5d7048cce55e` |
| [image 5.png](source/notion-export/image%205.png) | [assets/backend/image-005.png](assets/backend/image-005.png) | Complete | `77066009eeddba3760ba74afcf8a8e0a236553ff61a0ae3098b2288d905eabf3` |
| [image 50.png](source/notion-export/image%2050.png) | [assets/system-design/image-050.png](assets/system-design/image-050.png) | Complete | `5d3704f838a72695f96ca0d2632bfa8632679c3341af672f9bcb7e9a927048c9` |
| [image 51.png](source/notion-export/image%2051.png) | [assets/system-design/image-051.png](assets/system-design/image-051.png) | Complete | `4000dad803a43348a11eae5f8b5314aac2d994b735465b47ba957dee35c37165` |
| [image 52.png](source/notion-export/image%2052.png) | [assets/system-design/image-052.png](assets/system-design/image-052.png) | Complete | `f603dfbf97e909298949ee40f1979744a1852e9271648d8d20c2fffa5fbf91be` |
| [image 53.png](source/notion-export/image%2053.png) | [assets/system-design/image-053.png](assets/system-design/image-053.png) | Complete | `e08dafc64e12fdaa6f08de9abb5206476b27dae21cb88d90c4daec7a48139500` |
| [image 54.png](source/notion-export/image%2054.png) | [assets/system-design/image-054.png](assets/system-design/image-054.png) | Complete | `abe98d8486d2041f8d2028154e1ab8c6a3a4d71ca895242ee6844c287f40df3c` |
| [image 55.png](source/notion-export/image%2055.png) | [assets/system-design/image-055.png](assets/system-design/image-055.png) | Complete | `d0b313c4c9fe61e3c50899225ecfc5b59a51f3eb2ffc86fc2e8da5e3dc5e2083` |
| [image 56.png](source/notion-export/image%2056.png) | [assets/system-design/image-056.png](assets/system-design/image-056.png) | Complete | `7a35470d937b25f78db463ebec31b1b7d0e4b160a1f0f50e411399f3f2d4591a` |
| [image 57.png](source/notion-export/image%2057.png) | [assets/system-design/image-057.png](assets/system-design/image-057.png) | Complete | `389ac9f24afcb43d9b422d0c7154b62133f12913b9549a244ab8e5c0b6537b60` |
| [image 58.png](source/notion-export/image%2058.png) | [assets/system-design/image-058.png](assets/system-design/image-058.png) | Complete | `455847608f814fcdce5821827ff8743787565fda1799b643ce2ae3d917527ce2` |
| [image 59.png](source/notion-export/image%2059.png) | [assets/system-design/image-059.png](assets/system-design/image-059.png) | Complete | `e0a20e6fa562ee2b1e33f9eddfa627a50f38687b2b1bffc01bc416a04e49c719` |
| [image 6.png](source/notion-export/image%206.png) | [assets/backend/image-006.png](assets/backend/image-006.png) | Complete | `294cb079437f7a591b1774ed49bc105a1090250d174778518a924abdcfe3dd11` |
| [image 60.png](source/notion-export/image%2060.png) | [assets/ai/image-060.png](assets/ai/image-060.png) | Complete | `6f61de9c726836def35b230d1227b66dc042088e431d7b66283a4de2232b6c17` |
| [image 61.png](source/notion-export/image%2061.png) | [assets/ai/image-061.png](assets/ai/image-061.png) | Complete | `f12b5cedf59e5b9293772163da9413660d67878887f650c6f2068bc131e3bffe` |
| [image 62.png](source/notion-export/image%2062.png) | [assets/ai/image-062.png](assets/ai/image-062.png) | Complete | `77b2c21ae4788b91b404dfc83e7744e2548c138d7f3b65427c2dc200da3d2dc1` |
| [image 63.png](source/notion-export/image%2063.png) | [assets/ai/image-063.png](assets/ai/image-063.png) | Complete | `844488e335d4cd50fe22c9728dddb804e734e7356f42c29df5d3df21b2713c6d` |
| [image 64.png](source/notion-export/image%2064.png) | [assets/ai/image-064.png](assets/ai/image-064.png) | Complete | `46cd06733b44231e6305bcb82228fa0a57f460cf96580a5c043e5eb7dd72afac` |
| [image 65.png](source/notion-export/image%2065.png) | [assets/ai/image-065.png](assets/ai/image-065.png) | Complete | `3a0cdd2540b139e596bd8894ac4d0a4d27c8045ea1f5e90acd54f7de94974d2c` |
| [image 66.png](source/notion-export/image%2066.png) | [assets/ai/image-066.png](assets/ai/image-066.png) | Complete | `023029aea8f7808f3b1281d1a7fac69782680c673b1d4ace29a7f66d96dc97cc` |
| [image 67.png](source/notion-export/image%2067.png) | [assets/ai/image-067.png](assets/ai/image-067.png) | Complete | `b499c4189d1c0f073bf8898d3afa31cabaa2f7d03095017fd4764a3942058773` |
| [image 68.png](source/notion-export/image%2068.png) | [assets/ai/image-068.png](assets/ai/image-068.png) | Complete | `76056e56c18388088f518d37b58d40bb06a367df5a3629d2d8044347e626b005` |
| [image 69.png](source/notion-export/image%2069.png) | [assets/ai/image-069.png](assets/ai/image-069.png) | Complete | `ef57a9bd7782b532491b297cbacfaf7f9d940a6fffa1aa7083ddfdff25eec912` |
| [image 7.png](source/notion-export/image%207.png) | [assets/backend/image-007.png](assets/backend/image-007.png) | Complete | `d8383acd632bba2b9a77d7e0f873b2107488eeb487c5875548b8d52684d5be23` |
| [image 70.png](source/notion-export/image%2070.png) | [assets/ai/image-070.png](assets/ai/image-070.png) | Complete | `1cc9431fb7b7df839cc87456c25a28e1edb21707b3b47d52d7522768f3a26625` |
| [image 71.png](source/notion-export/image%2071.png) | [assets/linux/image-071.png](assets/linux/image-071.png) | Complete | `91c75418c910bccf8c9953b4ae5ed22cbbb464b19d72b976e7534031d912cfaa` |
| [image 72.png](source/notion-export/image%2072.png) | [assets/linux/image-072.png](assets/linux/image-072.png) | Complete | `0d0cd608cf00cd4b849033985f1b93209daf55dbd813622851b0a418661e622c` |
| [image 73.png](source/notion-export/image%2073.png) | [assets/linux/image-073.png](assets/linux/image-073.png) | Complete | `2806771c157ea0c482b3c37d907800a5cd63ac9894c0b9d986a68e1dbd3c5114` |
| [image 74.png](source/notion-export/image%2074.png) | [assets/linux/image-074.png](assets/linux/image-074.png) | Complete | `35dcd959e24787c5e9b1b87240ecd8e8851f9b850d9a16ebf214b556863b184e` |
| [image 75.png](source/notion-export/image%2075.png) | [assets/linux/image-075.png](assets/linux/image-075.png) | Complete | `34d1dcb544023cc307b0f494fea93a2f75bf711ccb605b45841a4690070ba945` |
| [image 76.png](source/notion-export/image%2076.png) | [assets/linux/image-076.png](assets/linux/image-076.png) | Complete | `c0ca8cad04abafc5a49ae3f997d92e38f2dacd4fd148f4c0c4c1474ce4875b57` |
| [image 77.png](source/notion-export/image%2077.png) | [assets/linux/image-077.png](assets/linux/image-077.png) | Complete | `78e453023efa1b90628ede3fab4b7dfb9c059fa5af725ad877d80b07a6b247d6` |
| [image 78.png](source/notion-export/image%2078.png) | [assets/database/image-078.png](assets/database/image-078.png) | Complete | `08ff44e2cc383e58320c9914f8f69013704a32406583cab61613604d4af43655` |
| [image 79.png](source/notion-export/image%2079.png) | [assets/database/image-079.png](assets/database/image-079.png) | Complete | `d1189cf3a307ec12c3e23c96bc17a43142550ade33e21b2ec5e6f108b6f466b9` |
| [image 8.png](source/notion-export/image%208.png) | [assets/backend/image-008.png](assets/backend/image-008.png) | Complete | `76ac7a59a180121e0c4dd3835259edd444e69529d61a3cc67fae8d01ecd033e6` |
| [image 80.png](source/notion-export/image%2080.png) | [assets/database/image-080.png](assets/database/image-080.png) | Complete | `c5a29b29b59d4cf2349324d61c1c2ae1010c538344bbb5526a108d30451d503e` |
| [image 81.png](source/notion-export/image%2081.png) | [assets/database/image-081.png](assets/database/image-081.png) | Complete | `df5a090f8a05aee41409cb81ef2f9ba15d91bf836abbb8cc7c142041e320c7ae` |
| [image 82.png](source/notion-export/image%2082.png) | [assets/database/image-082.png](assets/database/image-082.png) | Complete | `ecb00cb2004f44c1b608181e94e8fe132140bca4fce135ec391cfeeb7697b4df` |
| [image 83.png](source/notion-export/image%2083.png) | [assets/frontend/image-083.png](assets/frontend/image-083.png) | Complete | `3f9cd0b117aa8346013e17ed373d6e3ce42df08b4f36f715944e8c90317d94a5` |
| [image 84.png](source/notion-export/image%2084.png) | [assets/agents/image-084.png](assets/agents/image-084.png) | Complete | `aff8a826ffde786d2e7baf38aac976fd6617830005b307d20190b3c028f62fb5` |
| [image 85.png](source/notion-export/image%2085.png) | [assets/agents/image-085.png](assets/agents/image-085.png) | Complete | `37b3a5138727ba5f46c6736bef01ecf16a53c00078fecd1b48c597623f1aa2a8` |
| [image 86.png](source/notion-export/image%2086.png) | [assets/agents/image-086.png](assets/agents/image-086.png) | Complete | `8de2baf4f06a32f29f89d9ad0aba916e3e0ceb7bda7992772ab8ed50f0557220` |
| [image 87.png](source/notion-export/image%2087.png) | [assets/agents/image-087.png](assets/agents/image-087.png) | Complete | `47ec458b757d07b7b07e858c39bc223180d21f7d9ac22d3bddd3be65e7ffe649` |
| [image 88.png](source/notion-export/image%2088.png) | [assets/agents/image-088.png](assets/agents/image-088.png) | Complete | `52e9bfd41a9ca2223973e9f1ebce597d9068ee59fb07b109c5a54fd18e8cc8b6` |
| [image 89.png](source/notion-export/image%2089.png) | [assets/agents/image-089.png](assets/agents/image-089.png) | Complete | `cf8f6bd8a149428ec13dc0a1a4d1c83c029daf8b0198e29d96dbacbdf512e6c5` |
| [image 9.png](source/notion-export/image%209.png) | [assets/backend/image-009.png](assets/backend/image-009.png) | Complete | `a13eb680bd3ec55997abe80bae0c5b629cb7c422e9770e555ad0c3ff18edcd22` |
| [image 90.png](source/notion-export/image%2090.png) | [assets/agents/image-090.png](assets/agents/image-090.png) | Complete | `66b3b6ad54e47a4f7d1df719863c572516f8ea0833e0e3af505877f35fa4de32` |
| [image 91.png](source/notion-export/image%2091.png) | [assets/agents/image-091.png](assets/agents/image-091.png) | Complete | `69e7b193e981617245cdb6bb0061279f93571de5a1e6c2b178b4509c6a01b888` |
| [image 92.png](source/notion-export/image%2092.png) | [assets/agents/image-092.png](assets/agents/image-092.png) | Complete | `e90daf3e7087f75ec1c484714798b8f661bf42ca56380b3a7f4101b79de8cb9a` |
| [image 93.png](source/notion-export/image%2093.png) | [assets/agents/image-093.png](assets/agents/image-093.png) | Complete | `5c346b0e74fc64d8636d57f7af0fa50e834a21aa1542c135b7948579d50eeeaf` |
| [image 94.png](source/notion-export/image%2094.png) | [assets/agents/image-094.png](assets/agents/image-094.png) | Complete | `4662c6c538683888d5866e68c2b142c34883284b78118363d18251118bc6b731` |
| [image 95.png](source/notion-export/image%2095.png) | [assets/agents/image-095.png](assets/agents/image-095.png) | Complete | `54cd38bd65496b7c1ecb0436837b5eaa3301a1c1286d3c36fe24d73be3e98546` |
| [image 96.png](source/notion-export/image%2096.png) | [assets/agents/image-096.png](assets/agents/image-096.png) | Complete | `e57a129fd4fa7c4012fb0eae6076c0af1501dcab12055a0c0354bebb847d1eef` |
| [image 97.png](source/notion-export/image%2097.png) | [assets/agents/image-097.png](assets/agents/image-097.png) | Complete | `e286964e89173e25d7531dd1d34618f9aba72b6a82ab3d22f7308266a1fe4961` |
| [image 98.png](source/notion-export/image%2098.png) | [assets/agents/image-098.png](assets/agents/image-098.png) | Complete | `041e16b33e4964dcba71fb4ebc7ab0ef7c3c42adb64107c12938b1a830a6d0d6` |
| [image 99.png](source/notion-export/image%2099.png) | [assets/agents/image-099.png](assets/agents/image-099.png) | Complete | `9fefdfe48b4c7dc9103b2c4571c7b6e41a4eb6f7576df53b262c6c74009cb195` |
| [image.png](source/notion-export/image.png) | [assets/backend/image-000.png](assets/backend/image-000.png) | Complete | `95eda45d81e717c82749498eb049cdd922f465c66c2329a3ec40ec282c035ee0` |
| [llms.txt](source/notion-export/llms.txt) | [assets/rag/llms.txt](assets/rag/llms.txt) | Complete | `6077a5ddf0a9a54eae176011976f8bcf2d6b92f6cbce8e05831c16b09fe5f204` |
| [📌개발 기술 정리 34bdbfd1e0fb80b6b1aaf9f6a0fb78ef.csv](source/notion-export/%F0%9F%93%8C%EA%B0%9C%EB%B0%9C%20%EA%B8%B0%EC%88%A0%20%EC%A0%95%EB%A6%AC%2034bdbfd1e0fb80b6b1aaf9f6a0fb78ef.csv) | [assets/notion-database/pages.csv](assets/notion-database/pages.csv) | Complete | `a0b8df1892726815ff21b8e5a6649ef2aab4514db4981007089b516d7d248cb2` |
| [📌개발 기술 정리 34bdbfd1e0fb80b6b1aaf9f6a0fb78ef_all.csv](source/notion-export/%F0%9F%93%8C%EA%B0%9C%EB%B0%9C%20%EA%B8%B0%EC%88%A0%20%EC%A0%95%EB%A6%AC%2034bdbfd1e0fb80b6b1aaf9f6a0fb78ef_all.csv) | [assets/notion-database/pages-all.csv](assets/notion-database/pages-all.csv) | Complete | `7662c238e7981cc70b58e5454cabea9579f35350faa3c3bb7b3131dc536e25ad` |

## Content Validation

| Check | Result |
| --- | ---: |
| Export files inventoried | 195 |
| Markdown files checked | 27 |
| Migrated content Markdown files | 35 |
| Additional navigation Markdown files | 15 |
| Final Markdown files including report | 51 |
| Toggles generated | 816 |
| Missing page or memo titles | 0 |
| Missing sections / sentences / paragraphs | 0 |
| Original URL occurrences checked | 242 |
| Missing links | 0 |
| Code blocks checked | 374 |
| Missing or modified code block contents | 0 |
| Image references checked | 165 |
| Missing assets | 0 |
| Markdown task checkbox lines in source | 0 |
| Missing checklist / list items | 0 |
| Original file hashes checked | 195 |
| Copied asset hashes checked | 168 |
| Local references checked (content / indexes / report) | 627 |
| Unreachable content documents | 0 |
| Git staged files compared with working file bytes | 415 |
| Original / asset files stored in Git without byte changes | 363 |
| Temporary verification files staged | 0 |

### Verification Method

일회성 Node.js 스크립트로 다음 자동 비교를 수행했다.

1. 원본의 전체 파일 집합, 크기, SHA-256을 기록하고 모든 파일을 읽었다. PNG/GIF는 복사본의 형식 헤더와 해시도 확인했다.
2. 각 Markdown의 변환 구간이 처음부터 끝까지 연속하며 누락·겹침이 없는지 검사했다.
3. 실제 저장된 정리본을 다시 읽어 생성한 Toggle을 제거하고 원래 제목을 복원했다. 새 목차 링크를 제거하고 변경한 첨부 상대 경로와 4개 fence 줄을 원래대로 되돌렸다.
4. 복원된 27개 문서를 원본과 문서 전체 문자열로 비교했다. 줄바꿈 형식(CRLF/LF) 외에는 공백·문장·문단·목록·순서를 정규화하거나 삭제하지 않았다. 모두 일치했다. 이 비교는 제목, 중복 문장, 체크리스트, 표, 개인 말투, 내부 Heading, 코드 및 URL의 보존을 함께 확인한다.
5. 별도로 외부 URL의 발생 횟수, 코드 블록의 전체 내용과 순서, 이미지 참조 수, 원본 제목·속성, Toggle 개수와 닫힘을 비교했다. 코드 블록은 바깥 fence 길이 조정 후의 원본과 비교했으며 내부 내용은 그대로 일치한다.
6. 이미지/TXT/CSV의 SHA-256과 최종 경로의 고유성을 검사했다. 원본 195개 파일의 해시와 파일 집합도 다시 비교했다.
7. 루트·카테고리 목차와 보고서의 로컬 파일 링크가 실제 경로를 가리키는지 검사했다. 외부 링크 접속 및 GitHub에서의 실제 렌더링 확인은 수행하지 않았다.
8. Git 인덱스의 파일 집합과 각 blob ID를 작업 파일에서 직접 계산한 blob ID와 비교했다. 415개 모두 일치하고, 원본·첨부 363개의 바이트가 Git에도 그대로 저장됨을 확인했다. 임시 검증 파일은 커밋 대상에 포함하지 않았다.

원본에는 Markdown 체크박스 구문 `- [ ]` / `- [x]` 행이 없었다. 일반 목록 형태의 체크리스트는 문서 전체 비교에 포함되어 모두 보존됐다. 검증용 임시 스크립트는 최종 저장소에 남기지 않는다.

### Per-page Validation

Source SHA-256은 줄바꿈을 포함한 제공된 파일의 바이트 해시이며, 원본 변경 여부를 확인한 값이다.

| Page | URL occurrences | Code blocks | Image references | Source SHA-256 | Result |
| --- | ---: | ---: | ---: | --- | --- |
| 인터뷰 질문 | 2 | 285 | 0 | `6c71fd5c92c0520f4d047fcd0becd28d0ad897f7631e9567fe670e612621a6a3` | Complete |
| Backend | 18 | 3 | 12 | `c20e62dc54bab45956ccac18fbf8cd4e277ef2cb05a6d6a81b1cdd9d243bcafb` | Complete |
| Programming Languages | 0 | 0 | 0 | `0142999b8d6199cb96e5e49e421f7f8be850e126b8c90a5417f34cf40f52533d` | Complete |
| 보안 | 0 | 1 | 2 | `069d50af0ec59532002ce3f2e744d7843a333ecb88a47a1da0123dfaee31cc44` | Complete |
| Networking | 2 | 3 | 3 | `bcf614971be2438acd396ec48bd60697e82422bc9e437b90cd58cae73a614b2a` | Complete |
| Cloud | 3 | 0 | 3 | `bfd00ff1b74985b0928d38d0eb1c33712198265e63463d1d7177e7c2f71978d9` | Complete |
| DevOps | 2 | 0 | 3 | `9adb2c714c77fad1c7b30f2b5fc0069b92a0e90a3f5c884469515947f9b4b06e` | Complete |
| CI/CD | 14 | 12 | 3 | `4873f68727fed0b3a5ca2cd24eaec10bc4bcba44d5ec6ea9e01a41a55bec72dd` | Complete |
| Kubernetes | 2 | 0 | 8 | `06857117a49e70ef108177c8ed5ce59265d777b3c793094d6848c35ad96afd24` | Complete |
| Docker 🐳 | 3 | 2 | 9 | `45bbba3814a558b213e2d5727a547e7c01ca5dc71337456c3497ddac595d286a` | Complete |
| Redis | 0 | 0 | 0 | `fb165bf7c7c7ec45dd847dc9a6f2dbd8c9721d5bc68dfa8e18c66b38beedd125` | Complete |
| Kafka | 0 | 4 | 2 | `c9dfeb7a27856bd48b1a66c9f8444456d4c90fdc0ee8a6c34b7a66209360fc2d` | Complete |
| 시스템 디자인 | 9 | 1 | 10 | `b2feac957200b9f9fc011006e21c453ad733ab17a92e4e5e974d15aab342510d` | Complete |
| 리눅스 | 5 | 31 | 7 | `4d8350abcb5de2d597e804a1f76ed486febac254a615202f0e7d94f41aa9955a` | Complete |
| 데이터베이스 | 5 | 0 | 5 | `b118c57dea95984f9f9702a9532ea6d70bd5bd2da0179a47f50332c17ee9f90b` | Complete |
| API testing tool | 0 | 0 | 5 | `7dac61b2d93468a051db9411c6e4282e9b878ccc85855e93b690a62948160871` | Complete |
| 오픈소스 | 13 | 0 | 0 | `70bf284995e950e5fed2ec73c9de5461a2fa7a2dbb1c694dc3ac13e282948b18` | Complete |
| 프론트엔드 | 4 | 0 | 1 | `efdaf972e9ba2631349af0f92ab05de48af7b8f32d0329d3a05a44235396d953` | Complete |
| 디자인 | 25 | 0 | 3 | `b4819fde8c350b6575af2150acf4815d7ce5944a3e44ec95e6b2e2187c9ad8ab` | Complete |
| 데이터 엔지니어링 | 4 | 1 | 1 | `7ba22d808766b7e404b805e318f8291786fb1ce505f03841ac5839dd37da8906` | Complete |
| AI | 13 | 2 | 11 | `f4b55020e975a124269a3461f0035afcc3ada7a9ea72955002dd999e3b883fd7` | Complete |
| 바이브코딩 | 4 | 1 | 13 | `c47ccdead32795eb198407b64b278b3a5a33a925345f5fb19c11b9ee95ef9fe3` | Complete |
| AI 에이전트 | 39 | 3 | 18 | `c9b2d92632cd31fcd3c0f7742d787f07df4f9beedb05eda9d19799ee1eb2933b` | Complete |
| RAG | 7 | 1 | 20 | `23edfb6779fdf7f86166e28343efae6a2ada38e8abe9cc0d34a93f103b6c8389` | Complete |
| Claude | 37 | 10 | 11 | `a7d7561a90464264b71fd770e92fdad11e0eedee74708819b592ef3c4491349c` | Complete |
| Codex | 17 | 11 | 11 | `0108f1550156b8e98f0204bd4a04e98fe1af613c8d54b7975fe0e0d57f2ec276` | Complete |
| Jev | 14 | 3 | 4 | `ce02a36a529222a28873e98ab77d12b65c66d86167c627868347afdbadf29ee2` | Complete |

## Result

No known content loss.

제공된 Export 전체 기준 알려진 콘텐츠 손실 0건. 원본 ZIP 대조 및 GitHub의 실제 렌더링은 위에 기재한 미검증 범위다.
