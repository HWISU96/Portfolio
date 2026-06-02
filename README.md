<div align="center">

# 김휘수 | Backend Developer

### "사용자 문제를 먼저 읽고, 안정적인 코드로 푸는 개발자"

기획/마케팅 실무에서 출발해 백엔드 개발자로 전환했습니다.  
**비즈니스 흐름을 이해하고**, **예외 상황까지 고려하는 개발**을 지향합니다.

<br>

[![Gmail](https://img.shields.io/badge/Gmail-soshyzx123@gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:soshyzx123@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-HWISU96-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/HWISU96)

<br>

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)

</div>

---

## 💡 About Me

저는 기획자로 일하며 **"사용자가 겪는 문제를 먼저 정의하는 것"** 이 좋은 서비스의 출발점임을 배웠습니다.  
이후 개발을 시작하면서도 같은 관점을 유지했습니다.

- 기능을 구현하기 전에 **왜 이 기능이 필요한지**, 어떤 예외가 생길 수 있는지를 먼저 생각합니다.
- 팀 프로젝트에서 프론트엔드·백엔드·기획 관점을 오가며 **크로스펑셔널 커뮤니케이션**에 익숙합니다.
- 금융 서비스처럼 **데이터 정합성과 안정성이 중요한 도메인**에서의 설계 경험이 있습니다.

---

## 🚀 Projects

### 1. DON'T — 맞춤형 지출 관리 및 저축 플랫폼

> SSAFY 교육생 대상 핀테크 서비스 | 2026.02 ~ 2026.03

[![GitHub](https://img.shields.io/badge/GitHub-dont-181717?style=flat-square&logo=github)](https://github.com/HWISU96/dont)

**6인 팀 | 백엔드 엔지니어 | 금융 및 랭킹 도메인 담당**

`Java` `Spring Boot` `PostgreSQL` `Redis` `FastAPI` `Docker` `Jenkins` `Nginx`

특정 키워드 입금 감지 시 자동 저축, 게이미피케이션 기반 실시간 랭킹, AI 소비 리포트를 제공하는 핀테크 웹 플랫폼입니다.  
**금융 트랜잭션의 안정성과 실시간 시스템의 성능**을 함께 고려한 아키텍처 설계를 주도했습니다.

<details>
<summary><b>🔍 트러블슈팅 상세 보기</b></summary>

<br>

#### ① 외부 API 동기화 시 데이터 정합성 보장

**문제**  
스케줄러와 사용자 요청이 동시에 발생하는 상황에서, 단순 Lock 적용 시 트랜잭션 커밋 전에 Lock이 해제되어 **Dirty Read 및 이중 과금** 위험이 있었습니다.

**해결**  
`ReentrantLock` + `TransactionSynchronization`을 조합하여 **DB 커밋 시점에 Lock이 해제**되도록 동기화했습니다.  
또한 API 거래 고유번호와 상태 플래그 기반 멱등성 처리로 동일 거래의 중복 이체를 원천 차단했습니다.

**결과**  
동시 요청 환경에서도 중복 이체 및 데이터 불일치 위험 제거, 안정적인 금융 처리 구조 확보

<br>

#### ② Event-Driven 아키텍처로 서비스 격리 및 랭킹 최적화

**문제**  
저축 트랜잭션(코어 금융 로직)과 랭킹 갱신 쿼리가 강결합된 구조에서, **랭킹 서버 장애가 금융 서비스로 전파**될 위험과 대규모 트래픽 시 DB 병목 가능성을 파악했습니다.

**해결**  
`Spring Event`를 활용해 금융 서비스와 랭킹 서비스를 **비동기 이벤트 기반으로 완전 분리**했습니다.  
RDB 집계 쿼리 대신 Redis `Sorted Set(ZSET)`을 도입하여 O(log N)으로 실시간 랭킹을 산출했습니다.

**결과**  
랭킹 서버 장애 시에도 금융 서비스 100% 정상 동작 보장, 동시 접속 환경에서도 지연 없는 랭킹 제공

<br>

#### ③ SSE 브로드캐스트 CPU 부하 O(N) → O(1) 최적화

**문제**  
랭킹 변동 알림을 위해 SSE를 도입했으나, N명의 클라이언트에게 전송 시 **루프 내부에서 JSON 직렬화가 반복**되어 CPU 부하가 접속자 수에 비례해 선형 증가했습니다.

**해결**  
직렬화 로직을 브로드캐스트 루프 **외부로 분리**하여 1회만 수행하고, 변환된 String을 그대로 전달하도록 구조를 변경했습니다.

**결과**  
직렬화 연산 복잡도 O(N) → O(1) 최적화, 대규모 접속 환경에서 API 호출 폭주 및 서버 CPU 부하 절감

</details>

---

### 2. YEJI — 동서양 결합 맞춤형 AI 운세 웹 플랫폼

> AI 기반 사주/타로 운세 서비스 | 2026.01 ~ 2026.02

[![GitHub](https://img.shields.io/badge/GitHub-yeji--portfolio-181717?style=flat-square&logo=github)](https://github.com/HWISU96/yeji-portfolio)

**5인 팀 | 프론트엔드 전담 | 클라이언트-서버 통신 최적화**

`React` `TypeScript` `Java` `Spring Boot` `PostgreSQL` `Redis` `FastAPI` `vLLM` `Qwen3`

팀 내 인력 공백으로 프론트엔드를 자진 전담하며, **클라이언트 입장에서 API를 직접 연동하는 경험**을 쌓았습니다.  
이 과정에서 서버 응답 구조가 프론트엔드 작업량에 미치는 영향을 체감하고, API 재설계를 주도했습니다.

<details>
<summary><b>🔍 트러블슈팅 상세 보기</b></summary>

<br>

#### ① FE 렌더링 병목 해소 — BFF(Adapter) 패턴 도입 주도

**문제**  
백엔드에서 비정형 Raw JSON(Depth 5 이상, snake_case)을 그대로 전달하여 **FE 타입 정의 복잡도 증가 및 불필요한 데이터 정제 로직 발생**, 렌더링 지연으로 이어졌습니다.

**해결**  
UI 컴포넌트와 1:1 매핑되는 **평탄화된 camelCase DTO 명세를 역제안**했습니다.  
백엔드가 프론트엔드 맞춤형 Adapter 역할을 수행하는 BFF 구조를 팀 내에서 이끌어냈습니다.

**결과**  
FE 내 데이터 정제 로직 100% 제거, 렌더링 속도 및 코드 가독성 대폭 향상

<br>

#### ② SSE 스트리밍 도입 — AI 응답 체감 지연 개선

**문제**  
LLM 운세 생성에 평균 10~15초가 소요되어, 동기식 HTTP 통신 시 **브라우저 타임아웃 및 사용자 이탈** 위험이 높았습니다.

**해결**  
SSE(Server-Sent Events) 단방향 스트리밍을 도입해 AI가 텍스트를 생성하는 즉시 청크 단위로 수신하고,  
수신 즉시 **타이핑 애니메이션으로 렌더링**하여 사용자가 응답을 실시간으로 보는 UX를 구현했습니다.

**결과**  
첫 글자 노출(TTFB) 1초 이내로 단축, 긴 생성 시간 동안 지속적인 시각적 피드백으로 이탈률 방지

</details>

---

### 3. SUDA — 농인 부모와 청인 자녀를 위한 언어 발달 지원 앱

> 온디바이스 AI 모바일 애플리케이션 | 2026.04 ~ 2026.05 | 🏆 SSAFY 자율 프로젝트 우수상

[![GitHub](https://img.shields.io/badge/GitHub-suda-181717?style=flat-square&logo=github)](https://github.com/HWISU96/suda)

**6인 팀 | 팀장 | 모바일 개발**

`Kotlin` `Jetpack Compose` `Java` `Spring Boot` `Python` `FastAPI` `PyTorch` `Docker`

실제 사용자(농인 부모, CODA) 인터뷰를 직접 주도하여 요구사항을 도출하고 앱 방향성을 피벗했습니다.  
초기 계획했던 백엔드/인프라 역할 대신, **프로젝트 목표에 맞춰 Android/Kotlin 개발로 역할을 전환**하며 Jetpack Compose를 새로 학습하고 모바일 화면·상태 관리·온디바이스 추론 기능을 구현했습니다.

**팀장으로서 역할**  
- 기능 범위와 서비스 방향에 대한 팀원 간 관점 차이를 사용자 문제·구현 가능성·완성도 기준으로 조율
- GitLab, Jira 스프린트, Git Flow, 브랜치/커밋/리뷰 규칙 정립으로 협업 체계 구축
- MediaPipe, TFLite 기반 온디바이스 추론 구조 적용, AI팀과 수어 인식 불일치 원인 분석 및 재보정

---

### 4. Rich Body — 성장 클리닉 웹사이트 (프리랜서 외주)

> 실제 운영 중인 학원 홈페이지 | 2025.11 ~ 현재

**1인 개발 | 클라이언트 요구사항 분석 및 정적 웹 구축**

`React` `Vite` `Netlify`

KINESS 근무 시절 인연을 맺은 원장님의 의뢰로 구축한 실제 운영 중인 웹사이트입니다.  
비개발자 클라이언트의 모호한 요구사항을 기능 명세로 번역하고, 지속적인 피드백을 통해 결과물을 납품했습니다.  
배포 초기 검색 노출 문제를 발견하고 MetaTags 적용 및 SEO 작업을 수행하여 접근성을 개선했습니다.

---

## 🎓 Education & Experience

| 기간 | 기관 | 내용 |
|---|---|---|
| 2025.07 ~ 2026.06 | 삼성청년SW·AI아카데미 (SSAFY) | Java Web 트랙 이수 |
| 2024.03 ~ 2025.02 | 교보문고 | eBiz마케팅팀 온라인 광고 검수 및 운영 |
| 2022.04 ~ 2022.08 | 스파르타코딩클럽 내일배움캠프 | Python AI 트랙 수료 |
| 2021.04 ~ 2022.03 | 성원에프씨 | 스포츠 애플리케이션 서비스 기획 및 마케팅 |
| 2015.03 ~ 2022.02 | 국민대학교 | 스포츠산업레저학 전공 / 광고홍보학 복수전공 |

---

## 📜 Certifications

| 자격증 | 취득일 |
|---|---|
| 정보처리기사 | 2025.12 |
| 리눅스마스터 2급 | 2025.06 |
| SQLD | 2023.04 |
| TOEIC Speaking IM2 | 2026.04 |

---

<div align="center">

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=HWISU96&show_icons=true&theme=default&hide_border=true&count_private=true)

</div>
