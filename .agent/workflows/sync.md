---
description: 3개 디바이스 (Main PC, 개인 Laptop, 캠퍼스 Laptop) GitHub 동기화 워크플로우
---

# Multi-Device GitHub 동기화 워크플로우 (/sync)

이 워크플로우는 Main PC, 개인 Laptop, 캠퍼스 Laptop 간의 작업 연속성을 유지하기 위해 GitHub 동기화를 수행합니다.

## 📌 실행 순서

### 1. 세션 시작 동기화 (Pull & Status Check)
1. 현재 로컬 워크스페이스에서 `git pull --rebase origin main`을 실행하여 타 디바이스에서 추가된 기업 폴더, 분석 보고서, 초안, `task.md` 최신 상태를 가져옵니다.
2. `task.md`를 열어 현재 어떤 기업이 어느 Phase에 있는지 확인합니다.

### 2. 세션 종료 동기화 (Commit & Push)
1. 작업이 완료되면 현재 진행한 내역(`task.md`, `[기업명]/`, `Reference/` 등)을 스테이징합니다:
   ```bash
   git add .
   ```
2. 작업한 디바이스 명칭을 커밋 메시지 프리픽스로 사용하여 커밋합니다:
   - Main PC인 경우: `git commit -m "[Main-PC] Update: TCK Phase 2 draft written"`
   - 개인 Laptop인 경우: `git commit -m "[Personal-Laptop] Update: Amkor Phase 3 final finalized"`
   - 캠퍼스 Laptop인 경우: `git commit -m "[Campus-Laptop] Update: Company_B Phase 1 analysis added"`
3. GitHub 원격 저장소로 푸시합니다:
   ```bash
   git push origin main
   ```

### 3. 충돌 발생 시 조치 (Conflict Resolution)
- 디바이스 간 동일 파일(예: `task.md`)에서 충돌이 발생하는 경우, 각 기업별 항목이 유실되지 않도록 두 디바이스의 진행 현황 항목을 병합(Merge)하여 보존합니다.
