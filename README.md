<div align="center">

# 안녕하세요, 김휘수입니다 👋

**기획을 아는 백엔드 개발자**

팀원들과 소통하며 '진짜 해결해야 할 문제'를 먼저 정의합니다.  
탄탄한 기획력을 바탕으로 예외 상황을 꼼꼼히 챙기며, 안정적인 코드를 만들겠습니다.

<br>

[![Gmail](https://img.shields.io/badge/Gmail-soshyzx123@gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:soshyzx123@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-HWISU96-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/HWISU96)
[![Portfolio](https://img.shields.io/badge/Portfolio-PPT-FF5722?style=flat-square&logo=files&logoColor=white)](https://github.com/HWISU96/Portfolio)

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

## 🚀 Projects

### 1. DON'T (2026.02 ~ 2026.03)

> **'삼성 청년 SW AI 아카데미' 교육생 대상 맞춤형 지출 관리 및 저축 플랫폼**

![DON'T 대표 화면](https://github.com/HWISU96/Portfolio/assets/preview-dont.png)
> *(이미지를 실제 스크린샷으로 교체해주세요)*

- **역할:** 6인 팀 / 금융 및 랭킹 도메인 백엔드 개발
- **기술스택:** `Java` `Spring Boot` `PostgreSQL` `Redis` `React` `Nginx` `Jenkins` `Docker` `FastAPI`
- **GitHub:** [ChickenBearTang/dont](https://github.com/ChickenBearTang/dont)

<details>
<summary>💡 주요 트러블슈팅 보기</summary>

<br>

**① Event-Driven 아키텍처를 통한 서비스 격리**

| | 내용 |
|---|---|
| **문제** | 저축 트랜잭션과 랭킹 갱신 로직이 강결합 → 랭킹 서버 장애가 핵심 금융 로직으로 전파 위험 |
| **해결** | Spring Event 기반 비동기 이벤트 아키텍처 도입 → 금융 서비스와 랭킹 서비스 완전 분리 |
| **결과** | 랭킹 서버 장애 시에도 금융 서비스 100% 정상 동작 확보 |

<br>

**② Redis ZSET 기반 실시간 랭킹 최적화**

| | 내용 |
|---|---|
| **문제** | 동시 접속자 1만 명 이상 환경에서 복잡한 집계 쿼리로 인한 DB 병목 발생 |
| **해결** | 별도 비동기 스레드 풀에서 이벤트 구독 + Redis Sorted Set 활용 |
| **결과** | O(log N)으로 실시간 랭킹 갱신, 동시 접속 환경에서도 지연 없는 시스템 제공 |

<br>

**③ SSE CPU 과부하 해결**

| | 내용 |
|---|---|
| **문제** | 다수 클라이언트에게 랭킹 변동 알림 전송 시 반복적인 JSON 직렬화로 CPU 부하 발생 |
| **해결** | 직렬화 로직을 브로드캐스트 루프 외부로 분리 |
| **결과** | 연산 복잡도 O(N) → O(1) 최적화 |

</details>

---

### 2. YEJI (2026.01 ~ 2026.02)

> **동서양 결합(사주/타로) 맞춤형 AI 운세 웹 서비스**

![YEJI 대표 화면](https://github.com/HWISU96/Portfolio/assets/preview-yeji.png)
> *(이미지를 실제 스크린샷으로 교체해주세요)*

- **역할:** 5인 팀 / 프론트엔드 개발 및 클라이언트-서버 통신 최적화
- **기술스택:** `React` `TypeScript` `Java` `Spring Boot` `PostgreSQL` `Redis` `FastAPI` `vLLM` `Qwen3`
- **GitHub:** [yeji-service](https://github.com/yeji-service)

<details>
<summary>💡 주요 트러블슈팅 보기</summary>

<br>

**① 클라이언트 친화적 API 설계 — BFF 패턴 도입**

| | 내용 |
|---|---|
| **문제** | 백엔드에서 비정형 Raw JSON(Depth 5↑, snake_case) 그대로 전달 → FE 타입 정의 복잡도 증가 및 렌더링 지연 |
| **해결** | UI 컴포넌트와 1:1 매핑되는 평탄화된 camelCase DTO 명세를 역제안 → BFF 구조 도입 주도 |
| **결과** | FE 내 데이터 정제 로직 100% 제거, 렌더링 속도 및 코드 가독성 향상 |

<br>

**② SSE 스트리밍 도입 — AI 응답 체감 지연 개선**

| | 내용 |
|---|---|
| **문제** | LLM 운세 생성에 평균 10~15초 소요 → 동기식 HTTP 통신 시 브라우저 타임아웃 및 이탈률 상승 |
| **해결** | SSE(Server-Sent Events) 단방향 스트리밍 도입 + 실시간 타이핑 애니메이션 구현 |
| **결과** | 첫 글자 노출(TTFB) 1초 이내로 단축, 사용자 체감 대기 시간 대폭 감소 |

</details>

---

### 3. SUDA (2026.04 ~ 진행 중)

> **농인 부모와 청인 자녀(CODA)를 위한 언어 발달 지원 앱**

- **역할:** 6인 팀 / 모바일 개발 및 팀장
- **기술스택:** `Kotlin` `Jetpack Compose` `Java` `Spring Boot` `Python` `FastAPI` `PyTorch` `Docker`

> 실제 사용자(농인 부모, CODA) 인터뷰를 직접 주도하여 요구사항을 도출하고 앱 방향성 피벗 진행.  
> 수어 데이터 수집 및 온디바이스 AI 모델 최적화 진행 중.

---

### 4. RICHBODY (2026.02 ~ 현재)

> **학원 브랜드 웹 홈페이지 구축 (프리랜서 외주)**

- **역할:** 1인 개인 프로젝트 / 클라이언트 요구사항 분석 및 정적 웹 페이지 구축
- **기술스택:** `React` `Vite` `Netlify`
- **배포:** [richbody 바로가기](#) *(링크 교체해주세요)*

> 비개발자 클라이언트와 직접 소통하며 요구사항을 기능 명세로 번역, 실제 운영 중인 서비스 납품.  
> MetaTags 적용 및 SEO 최적화로 포털 검색 노출 개선.

---

## 🎓 Education & Experience

| 기간 | 기관 | 내용 |
|---|---|---|
| 2025.07 ~ 2026.06 | 삼성 청년 SW AI 아카데미 (SSAFY) | Java 비전공자 트랙 이수 |
| 2024.03 ~ 2025.02 | 교보문고 | eBiz마케팅팀 온라인 광고 및 홈페이지 운영 보조 |
| 2022.04 ~ 2022.08 | 스파르타코딩클럽 내일배움캠프 | Python AI 트랙 이수 |
| 2021.04 ~ 2022.03 | 성원에프씨 | 스포츠 애플리케이션 서비스 기획 및 마케팅 |
| 2015.03 ~ 2022.02 | 국민대학교 | 스포츠산업레저학 전공 / 광고홍보학 복수전공 |

---

## 📜 Certifications

| 자격증 | 발급기관 | 취득일 |
|---|---|---|
| 정보처리기사 | 한국산업인력공단 | 2025.12 |
| 리눅스마스터 2급 | 한국정보통신진흥협회 | 2025.06 |
| SQLD | 한국데이터산업진흥원 | 2023.04 |
| TOEIC Speaking IM2 | YBM | 2026.04 |

---

<div align="center">

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=HWISU96&show_icons=true&theme=default&hide_border=true&count_private=true)
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=HWISU96&layout=compact&theme=default&hide_border=true)

</div>
