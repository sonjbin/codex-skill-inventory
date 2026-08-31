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

- 실험 작업 시작 전 docs/experiments/EXPERIMENT_GUIDE.md와 docs/experiments/CURRENT_STATE.md를 확인한다.
- 각 실험은 docs/experiments/templates/EXPERIMENT.md를 사용해 목적, 가설, baseline 대비 변경, 성공 기준, 중단 조건을 기록한다.
- 독립적이고 경계가 명확한 실험만 worker subagent에 위임한다. 동일 working tree 또는 출력 경로의 동시 쓰기는 금지한다.
- main agent는 raw training log를 반복 polling하지 않는다. status.json, 완료 marker, milestone 또는 anomaly가 있을 때만 상태를 확인한다.
- 실험 종료 시 결과 요약, 아티팩트 경로, 결정, 다음 조치를 기록하고 CURRENT_STATE.md를 갱신한다.
- 반복적인 로그·상태 추출은 프로젝트별 형식과 검증 방법이 확인된 후 experiment-runner 스킬 절차에 따라 결정적 스크립트로 자동화한다.
