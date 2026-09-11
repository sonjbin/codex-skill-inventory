# Codex 작업 규칙

## 일반 작업

- 복수 단계 작업, 파일 변경, 외부 작업은 목표·범위·완료 조건·검증 방법을 포함한 action plan을 먼저 작성하고 즉시 실행한다.
- 범위가 모호하거나 승인된 범위를 넘는 변경이 필요하면 중단하고 확인한다.
- 최소 변경 원칙을 따른다. 명시되지 않은 리팩터링, 스타일 변경, fallback 구현은 수행하지 않는다.
- 사용자 지시가 일반 규칙과 충돌하면 사용자 지시를 우선한다.
- 파일 생성은 승인된 작업 범위 안에서 경로·목적·필요성을 plan에 명시한 후 수행한다.
- 검증은 변경 범위에 비례하는 최소 단위로 실행한다. 전체 테스트·빌드는 명시적으로 필요할 때만 실행한다.
- 완료 보고에는 변경 내용, 변경 파일, 검증 결과, 미검증 사항 또는 잔여 리스크를 포함한다.

## 실험 작업

- Workspace `AGENTS.md`에서 공통 실험 관리 루트 확인. 권장 배치 `<workspace>/experiment-management/`, 실제 경로는 workspace 선언 우선. 아래 실험 경로는 해당 관리 루트 기준.
- 결과 조회 시 `experiments/INDEX.md` → 관련 주제 `INDEX.md` → 필요한 보고서 순서로 탐색. 전체 보고서·archive 일괄 로딩 금지.
- 실행 전 공통 `experiments/EXPERIMENT_GUIDE.md`, `experiments/CURRENT_STATE.md`, `ENVIRONMENT.md`의 해당 프로파일 확인.
- Action plan에 기존 주제 검색 결과와 저장 위치 명시. 같은 실험 재실행은 새 run, 관련 비교는 기존 주제 하위 study, 독립 목적만 새 주제 폴더 생성.
- 신규 study는 공통 템플릿 사용 및 주제 인덱스 등록. 전역 ID 중복 확인 후 예약, 여러 주제 관련 결과는 한 곳에 저장하고 교차 링크 사용.
- 환경·기본 설정은 `ENVIRONMENT.md`에서 관리. 지속 예외와 일회 예외의 범위·사유·근거 기록. 실행마다 실제 자원 가용성 확인.
- Run manifest에 프로파일 revision/hash, 최종 설정, 참여 레포별 commit 및 dirty patch/hash, 데이터·프롬프트·모델·지표 식별 정보 기록.
- 코드·로그·prediction·checkpoint는 소유 레포의 고유 run 경로에 보존. 실험 문서에서는 workspace 상대 경로와 hash로 참조.
- 독립적이고 경계가 명확한 실험만 위임. 동일 working tree 또는 출력 경로의 동시 쓰기 금지.
- Raw training log 반복 polling 금지. `status.json`, 완료 marker, milestone 또는 anomaly 중심 확인.
- 종료 시 결과·baseline 차이·해석·결정·다음 조치·아티팩트 기록 및 주제 인덱스 갱신. `CURRENT_STATE.md`는 활성 작업·차단 사유·다음 조치만 60줄 이내 유지.
- 로그·상태 자동화는 실제 형식과 검증 방법 확인 후 experiment-runner 절차 적용.
