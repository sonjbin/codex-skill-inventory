# 실험 관리 가이드

## 탐색과 분류

- 조회: 전체 `INDEX.md` → 관련 주제 `INDEX.md` → 필요한 study 보고서 순서
- 실행: 위 탐색 후 `CURRENT_STATE.md`와 `../ENVIRONMENT.md`의 해당 프로파일 확인
- 같은 목적·가설·조건의 재실행: 기존 study에 고유 run 추가
- 관련 모델·프롬프트·해상도·데이터·지표 비교: 기존 주제의 `studies/<ID>-<slug>/REPORT.md` 생성
- 해당 연구 목적을 포함하는 주제 부재: 새 주제 폴더와 `README.md`, `INDEX.md` 생성
- 주제 간 비교: 소유 주제 하나 선정 후 관련 인덱스에서 교차 참조. 결과 복제 금지
- ID: 모든 주제 인덱스에서 중복 검사 후 다음 E번호 예약. 예약·인덱스 쓰기는 main agent 직렬 처리

## 기록 범위

- Study 템플릿: [EXPERIMENT.md](templates/EXPERIMENT.md)
- 주제 `README.md`: 연구 범위, 현행 baseline 링크, 비교 가능 조건
- 주제 `INDEX.md`: ID, 제목/검색어, 상태, 결정, 보고서 링크. 신규 항목에 데이터 버전·주 지표·baseline 명시
- Study 보고서: 목적·가설·baseline·설정 차이·성공/중단 기준·결과·해석·다음 조치
- Run manifest: 참여 레포별 commit/dirty patch와 hash, 모델/checkpoint·입력·프롬프트·평가 코드 hash, seed, 실행 명령, 프로파일 revision/hash, 최종 설정, 실제 환경·GPU 배치
- 서로 다른 데이터·marker 정책·metric·aggregation의 점수는 동등 조건으로 병합 금지. `supersedes`, `derived_from`, 비교 제한 명시
- 과거 manifest 누락은 `unknown` 기록. 현재 환경으로 과거 설정 추정 금지

## 환경과 아티팩트

- 공통 기본값 → 모델/작업 프로파일 → 범위가 명시된 예외 → 명시적 실행 변경 순서 적용
- 모든 기본값·예외는 `../ENVIRONMENT.md` 한 곳에서 관리. Study에는 참조와 변경 요약만 기록
- 문서는 실행 설정을 자동 적용하지 않으므로 실행 명령·config와 최종 manifest 대조 필수
- 실제 GPU 점유 상태 매 실행 확인. 일회 예외를 다음 실행의 기본값으로 전파 금지
- 기존 산출물 경로 보존. 신규 실행은 소유 레포의 `<output-root>/<topic>/<study>/<run-id>/` 사용
- Run 내부 `manifest.json`, `status.json`, `summary.json`, `logs/`, `predictions/`, `plots/` 중 해당 항목 저장
- Checkpoint는 학습 레포에서 관리. 공통 문서 Git에 로그·prediction·가중치 추가 금지
- Smoke 정책은 적용 workspace/레포 AGENTS 기준 확인. 실제 오류 수정 검증은 해당 최소 조건으로 수행 후 본 실행 재개

## Context와 완료 조건

- `CURRENT_STATE.md`: 활성·차단 작업, 다음 조치, 링크만 60줄 이내 유지. 완료 결과의 장기 누적 금지
- 상태 확인: `status.json`의 상태·처리량·오류 수·갱신 시각 확인. Raw log는 이상 시 관련 구간만 확인
- 형식 불명 상태·로그에 범용 parser 가정 금지. 실제 정상/실패 로그 확인 후 자동화
- 표적 수정 후 동일 실패 재발 시 반복 재시작 중단, 근거와 다음 진단 기록
- 완료 시 입력 hash·누락/중복·평가 수·저장 metric 재현 확인, 오류·미검증 사항 기록
- 사용한 프로세스 종료·자원 반환 확인, 보고서와 주제 인덱스 및 현재 상태 갱신
- 신규 주제에만 전체 인덱스 갱신. 기존 주제 하위 실험마다 전체 문서 로딩 금지

## 검증 방법

- 인덱스의 ID 유일성·보고서 링크·baseline 관계 확인
- 환경 프로파일과 run 최종 설정 차이 및 예외 등록 대조
- 아티팩트 존재·입력 및 metric 재현성 확인
- 이관 시 원본 hash 보존과 기존 경로 호환 링크 확인
