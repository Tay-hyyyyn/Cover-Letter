---
description: 자기소개서 작성 Multi-Track Pipeline & 3-Device Git Sync 워크플로우
---

# 자기소개서 작성 Multi-Track Pipeline 워크플로우

이 워크플로우는 사용자가 3개의 디바이스(Main PC, 개인 Laptop, 캠퍼스 Laptop)에서 여러 기업의 자기소개서를 병렬(Multi-Track)로 작성하고 GitHub을 통해 상태를 동기화할 수 있도록 안내합니다.

## 📌 주요 프로세스 (Phase 0 ~ Phase 3)

### [동기화] 세션 시작 체크포인트 (Session Start)
1. 작업 시작 전 `/sync` 워크플로우 또는 `git pull --rebase origin main`을 실행하여 타 디바이스의 최신 상태를 받아옵니다.
2. `task.md`를 열어 현재 어떤 디바이스에서 어떤 기업이 진행 중인지 확인합니다.

### Phase 0: [선택] 포지션 추천 (Position Recommendation)
1. 사용자가 타겟 기업 및 채용 중인 직무 JD를 입력합니다.
2. `Reference/Resume_Backups/episodes/episode-bank.md` 및 지원자의 이력과 JD를 교차 검증합니다.
3. 가장 합격 가능성이 높은 포지션(1~2순위) 및 추천 이유를 작성하여 사용자에게 제시합니다.

### Phase 1: 기업 및 직무 정밀 분석 (Company & Role Analysis)
1. 타겟 기업 전용 독립 폴더(`[기업명]/`)를 생성합니다.
2. 해당 기업 폴더 내에 사업보고서, 채용 공고(JD), 참고 자료 등을 배치합니다.
3. 기업 SWOT 분석, 산업 트렌드, 직무 핵심 역량을 분석합니다.
4. `[기업명]/[기업명]_Analysis.md` 파일로 분석 보고서를 저장하고 `task.md` 진행 현황을 갱신합니다.

### Phase 2: 자기소개서 항목별 초안 작성 (Drafting Cover Letter)
1. 지원 플랫폼에 따른 자소서 문항 분기 처리:
   - **사람인 지원 시**: 사용자가 명시적으로 "사람인으로 지원한다"고 한 경우, 3가지 고정 항목([지원동기 및 포부], [직무적강점], [협업경험])으로 자소서를 작성합니다.
   - **일반 지원 시**: "사람인" 언급이 없으면 당 회사가 요구하는 별도의 자소서 문항이 있는 것으로 간주하고, 사용자가 제공한 문항에 맞춰 작성합니다.
2. 글자 수 제한 및 반영 희망 에피소드를 확인합니다.
3. `Reference/Resume_Backups/profile/style-guide.md`의 규칙(두괄식, STAR 구조, '직장인 vs 직업인' 지원동기 프레임워크, 미사여구 최소화 등)을 엄격히 적용합니다.
4. `[기업명]/[기업명]_Cover_Letter_Draft.md` 파일로 초안을 생성합니다.
5. 사용자 검토 대기 상태로 `task.md`를 갱신합니다. (초안 검토 중에도 다른 기업의 작업을 동시 수행 가능)

### Phase 3: 최종본 적재 및 에피소드 학습 (Finalization & Learning)
1. 사용자로부터 최종 확정된 자기소개서 텍스트를 전달받습니다.
2. `Reference/자소서_최종_정리/` 하위에 `[기업명]_[직무]_[연도].txt` 또는 파일로 최종본을 적재합니다.
3. 최종본에서 새롭게 도출된 에피소드나 강조점을 추출하여 `Reference/Resume_Backups/episodes/episode-bank.md`에 반영 및 보완합니다.
4. `task.md`의 Kanban 진행 상황을 완료(`[x]`)로 이동합니다.

### [동기화] 세션 종료 체크포인트 (Session End)
1. 해당 세션의 작업 내역을 커밋하고 현재 디바이스 태그(`[Main-PC]`, `[Personal-Laptop]`, `[Campus-Laptop]`)를 커밋 메시지에 명시합니다.
2. `git push origin main`을 실행하여 GitHub에 변경 사항을 최종 공유합니다.
