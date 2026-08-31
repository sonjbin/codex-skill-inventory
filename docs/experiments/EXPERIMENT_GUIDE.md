# Codex 실험 운영 가이드

## 목적

Codex를 사용한 장기·반복 실험의 재현성, 추적성, context 효율 관리.

## 문서 역할

| 문서 | 역할 |
| --- | --- |
| CURRENT_STATE.md | 현재 목표, baseline, 핵심 결론, 다음 실험 관리 |
| EXPERIMENT_INDEX.md | 실험 목록과 상태 관리 |
| experiments/E###.md | 개별 실험의 가설, 설정, 결과, 결정 관리 |
| runs/E###/ | raw log, compact status, 완료 marker, 산출물 관리 |

Raw log는 보존한다. 판단과 다음 조치는 개별 실험 요약 및 CURRENT_STATE.md에만 기록한다.

## 실험 시작

1. CURRENT_STATE.md와 baseline 실험을 확인한다.
2. 실험 ID를 발급하고 experiments/E###.md를 템플릿에서 생성한다.
3. 목적, 가설, baseline 대비 단일 주요 변경, 검증 기준, 중단 조건을 기록한다.
4. 데이터셋, checkpoint, 실행 명령, 출력 경로, 자원 충돌 여부를 확인한다.

## 실행과 추적

- baseline 대비 하나의 주요 가설만 변경한다. 여러 변경이 불가피하면 해석 불가 위험을 실험 문서에 기록한다.
- raw log 전체를 반복 조회하지 않는다. status.json, 정해진 milestone, 완료 marker, anomaly를 우선한다.
- 정상 상태 확인은 초기 5~10%, 중간 50%, 종료 시점으로 제한한다. 추가 확인은 오류·지표 급변·상태 갱신 중단에만 수행한다.
- 상태 파일이 없다면 실행 프로그램이 제공하는 가장 작은 구조화된 출력만 조회한다.

## 결과와 결정

개별 실험 문서에는 결과, baseline 비교, 해석, 결정, 다음 조치, 산출물 경로를 기록한다.

- ACCEPT: 가설 지지 및 다음 단계 진행
- REJECT: 가설 기각
- INCONCLUSIVE: 추가 검증 필요
- FAILED: 실행 또는 환경 실패

완료 상태는 실행 종료만으로 판단하지 않는다. 필요한 산출물, metric, baseline 비교, 해석, 결정, 상태 반영까지 완료해야 한다.

## subagent 운영

독립된 실험·로그 분석·코드 탐색처럼 결과를 분리해 회수할 수 있는 작업만 위임한다.

위임 요청에는 실험 ID, 목적, 가설, baseline, 변경·비변경 항목, 실행 설정, 검증 기준, 중단 조건, 출력 경로, 반환 형식을 포함한다.

worker는 raw output 대신 상태, 핵심 결과, baseline 비교, 해석과 권고, 실험 요약·raw log·checkpoint·metric 파일 경로를 반환한다.

## 프로젝트별 자동화

이 저장소에는 학습 코드와 로그 형식이 없으므로 범용 로그 파서나 실행 스크립트를 포함하지 않는다.

반복 추적이 확인된 프로젝트에서만 다음 절차로 자동화를 추가한다.

1. 학습 진입점, 실제 로그 샘플, metric 산출물, 완료·실패 신호를 확인한다.
2. 입력 형식과 출력 스키마를 문서화한다.
3. step, loss, validation metric, learning rate, error, status, last_update처럼 의사결정에 필요한 최소 정보만 추출하는 스크립트를 구현한다.
4. 정상 로그, 실패 로그, 누락 필드에 대한 동작을 검증한다.
5. 스크립트 실행 명령과 생성되는 status.json 또는 marker 경로를 CURRENT_STATE.md에 기록한다.

자동화가 검증되기 전에는 log 형식이나 완료 신호를 가정하지 않는다.

## 완료 조건

- 각 실험에 ID, 요약 문서, 실행 산출물 경로 존재
- CURRENT_STATE.md와 EXPERIMENT_INDEX.md 최신 상태 반영
- 결정과 다음 조치 기록

## 검증 방법

- 실험 ID별 문서, runs/E###/, index 항목의 경로 일치 확인
- summary의 설정·metric·결정과 실제 산출물 대조
- 상태 문서의 baseline·best experiment·next action 대조
