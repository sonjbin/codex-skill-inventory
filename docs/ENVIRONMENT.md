# 공통 환경 프로파일 템플릿

- Revision:
- Workspace / 소유 레포:
- Runtime: conda/Python 경로, 검증된 버전, 근거·시점
- GPU: 장비 조건, 실제 가용성 확인 방법
- 추론 프로파일: 모델 범위, TP/DP, memory utilization, concurrency, generation, seed
- 학습 프로파일: 모델 범위, precision, 분산 전략, batch/accumulation, config
- 재평가 프로파일: metric 구현·normalization·aggregation
- 적용 순서: 공통 기본 → 모델/작업 프로파일 → 등록 예외 → 명시적 실행 변경

| 예외 ID | 적용 범위 | 변경값 | 사유·근거 | 지속/일회 | 검증 상태 |
|---|---|---|---|---|---|

- Run에 프로파일 revision/hash와 실제 환경·최종 설정 snapshot 저장
- 기본값 변경 시 이전 값·사유·검증 근거와 revision 이력 보존
- 문서의 값은 자동 적용되지 않으므로 실제 config/명령 대조 필수
