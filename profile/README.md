<div align="center">

# 💎 Team Crystal

**One Action, Infinite Clouds.**

SoftBank Hackathon 2026 powered by KOREC & Progate · 예선 2

로컬에서 만든 웹 애플리케이션을, AI와 함께 클릭 한 번으로 클라우드와 온프레미스에 배포합니다.<br>
ローカルで作ったWebアプリを、AIと一緒にワンアクションでクラウド・オンプレへデプロイします。

<br>

![기간](https://img.shields.io/badge/기간-2026.10.05~10.11-555555?style=flat-square)
![장소](https://img.shields.io/badge/장소-부산%20지오파트너스-1D9E75?style=flat-square)
![주최](https://img.shields.io/badge/SoftBank%20Hackathon-2026-185FA5?style=flat-square)

</div>

---

## 무엇을 만드는가

배포는 늘 같은 고민의 반복입니다. 어디에 올릴지, 로컬과 클라우드의 차이는 어떻게 맞출지, 데이터베이스는 어떻게 옮길지, 문제가 생기면 어떻게 되돌릴지.

**`oneaction`은 그 고민을 AI가 대신 판단하고 실행하는 배포 시스템입니다.**

개발자는 `deploy.yaml`에 **원하는 것만** 적습니다. 어디에 어떻게 띄울지는 적지 않습니다. 나머지는 AI가 환경에 맞게 채우고, 위험한 것은 막습니다.

![전체 흐름](https://raw.githubusercontent.com/Crystal-SBHackathon2026/.github/main/profile/architecture.png)

## 흐름

| | 단계 | 하는 일 |
| --- | --- | --- |
| ① | 개발자 | 앱 레포에 PR을 올린다. 이후는 손댈 일이 없다 |
| ② | AI 검토 | 정적 규칙 25개 → 근거 검색(규칙 문서·지난 판단 사례) → LLM 판단. 통과 / 고쳐서 통과 / 사람 확인 / 거절 |
| ③ | 배포 자동화 | 자동 병합 → 테스트·빌드·취약점 검사 → GitOps 레포 커밋 → Argo CD |
| ④ | 배포 환경 | 같은 커밋 하나가 여러 환경에. 카나리로 절반만 먼저 보내고, 틀리면 자동으로 되돌린다 |
| ⑤ | 되돌아오는 고리 | 배포 결과가 baseline이 되어 **다음 검토의 근거**가 된다 |

⑤가 이 시스템의 핵심입니다. "지금 명세만 봐서는 알 수 없는 위험"(DB 엔진 교체, 볼륨 축소 등)을 **이전에 성공한 배포와 비교해서** 잡아냅니다.

## 지금 돌아가는 것

| 환경 | 상태 |
| --- | --- |
| 부산 로컬 (k3s) | ✅ 배포됨 |
| 서울 AWS (EKS) | ✅ 배포됨 |
| 도쿄 GCP (GKE) | 준비 중 |

같은 소스 커밋 하나가 로컬과 AWS에 동시에 떠 있고, 환경별 설정만 다릅니다. 코드 수정부터 배포 완료까지 **약 5분**입니다.

## 저장소

| 저장소 | 내용 |
| --- | --- |
| [review-service](https://github.com/Crystal-SBHackathon2026/review-service) | AI 검토 서비스 — Review API · Kafka · LangGraph 워커 · 판단 로직 |
| [gitops](https://github.com/Crystal-SBHackathon2026/gitops) | Argo CD 배포 설정 (로컬 k3s · AWS EKS · GCP GKE) |
| [sample-app](https://github.com/Crystal-SBHackathon2026/sample-app) | 데모용 샘플 웹앱 — 어느 환경이 응답했는지 표시 |
| [sample-todo](https://github.com/Crystal-SBHackathon2026/sample-todo) | 앱 분석·변환 시연용 SQLite 할 일 앱 |
| Terraform-infrastructure | AWS 인프라 (EKS · MSK · RDS · ALB · IAM) |

## 팀원

| 이름 | 파트 | 담당 | GitHub |
|---|---|---|---|
| 김혜연 <sub>팀장</sub> | AI 검토 바깥 뼈대 | Review API · Kafka · 워커 실행 틀 · 업무 DB · 커밋 연동 | [@Hyeyeon-Kim](https://github.com/Hyeyeon-Kim) |
| 김연재 | AI 판단 로직 | 정적 검사 · 근거 검색 · LLM 판단 · 평가셋 · overlay 렌더러 | [@yeonjae1220](https://github.com/yeonjae1220) |
| 박찬건 | 클라우드 인프라 | EKS 구축 · Terraform · 네트워크 · 시크릿 · 권한 | [@coldgeon](https://github.com/coldgeon) |
| 이성진 | CI/CD · 배포 자동화 | CI 파이프라인 · GitOps · Argo CD · 카나리 · 배포 에이전트 | [@FAITRUEE](https://github.com/FAITRUEE) |

## 일정

| 날짜 | 내용 |
|---|---|
| 10/5 | 킥오프, 팀 빌딩, 역할 분담 |
| 10/6~10/9 | 사전 개발 — 아키텍처 확정, 각 파트 구현, 전 구간 연결 |
| 10/10 | Day 1 · 개발, 중간 보고 |
| 10/11 | Day 2 · 개발, 최종 발표 |

<div align="center">
<br>
<sub>설계 과정과 논의 기록은 팀 Notion에 있습니다.</sub>
</div>
