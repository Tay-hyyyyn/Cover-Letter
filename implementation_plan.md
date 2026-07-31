# 자소서 작성 어시스턴트 봇 운영 계획 (Implementation Plan)

사용자님이 여러 기업의 자소서 작성을 **병렬적(비동기적)으로 동시에 진행**하고, **3개의 디바이스(Main PC, 개인 Laptop, 캠퍼스 Laptop)** 간 작업 연속성을 보장받을 수 있도록 Multi-Track Pipeline 및 GitHub Sync 아키텍처를 적용했습니다.

---

## 📌 핵심 아키텍처 (Multi-Track Pipeline & 3-Device Git Sync)

### 1. 독립된 워크스페이스 (Isolated Workspace)
- 각 기업별로 독립된 폴더(예: `Amkor/`, `TCK/`, `Company_B/`)를 생성하여 분석 보고서와 초안을 별도로 관리합니다.

### 2. 상태 기반 태스크 관리 (Kanban Board)
- `task.md`를 단일 진실 출처(Single Source of Truth)로 사용하며, 각 기업별 작업이 현재 어느 단계(Phase 0~3)에 머물러 있는지 및 디바이스 동기화 상태를 추적합니다.

### 3. 비동기 최종본 적재 (Asynchronous Finalization)
- A기업의 최종본이 확정되지 않아도 B기업의 분석 및 작성을 즉시 시작할 수 있으며, 확정 시 언제든 적재 및 학습이 가능합니다.

### 4. 3개 디바이스 동기화 프로토콜 (Multi-Device Git Sync Protocol)
- **작업 장소 (3 Devices)**: `Main PC`, `개인 Laptop`, `캠퍼스 Laptop`
- **동기화 중앙 허브**: GitHub Remote Repository (`main` branch)
- **세션 시작 (Session Start)**: 작업 시작 전 `/sync` 실행 또는 `git pull --rebase origin main`으로 최신 상태 가져오기.
- **세션 종료 (Session End)**: 작업 완료 후 커밋 메시지에 디바이스 태그(`[Main-PC]`, `[Personal-Laptop]`, `[Campus-Laptop]`) 포함하여 `git push origin main` 실행.

---

## 🛠 제안하는 프로세스 (Multi-Track & Multi-Device Workflow)

### [동기화 단계] 세션 시작 (Session Start & Pre-Check)
**[AI / 사용자 수행]** `git pull` 실행으로 타 디바이스 작업 내역 동기화 및 `task.md` 상태 확인.

### [0단계] 포지션 추천 (Position Recommendation)
**[사용자 입력]** 타겟 기업 및 채용 중인 여러 직무의 JD  
**[AI 수행]** Resume 데이터와 각 직무 교차 검증 후 합격 확률 높은 포지션(1~2순위) 추천.

### [1단계] 기업 및 직무 정밀 분석 (Company & Role Analysis)
**[사용자 입력]** 타겟 직무 및 해당 기업 폴더 내 사업보고서/JD 파일 업로드  
**[AI 수행]** `[기업명]/[기업명]_Analysis.md` 분석 보고서 작성 및 `task.md` 갱신.

### [2단계] 자기소개서 초안 작성 (Drafting Cover Letter)
**[사용자 입력]** 각 기업 자소서 문항, 글자 수, 반영 희망 에피소드  
**[AI 수행]** STAR 기법 및 문체 가이드 적용 `[기업명]/[기업명]_Cover_Letter_Draft.md` 초안 작성.

### [3단계] 최종본 적재 및 지속적 학습 (Finalization & Learning)
**[사용자 입력]** 최종 다듬어진 자기소개서 완성본 텍스트 제공  
**[AI 수행]** `Reference/자소서_최종_정리/` 하위 적재 및 `episode-bank.md` 학습 연동.

### [동기화 단계] 세션 종료 (Session End & Push)
**[AI / 사용자 수행]** 작업 내용 커밋 및 `git push origin main`으로 GitHub 저장소에 변경 사항 동기화.
