---
name: research-report
description: Turn experiment records, benchmark results, error analyses, or research updates into decision-oriented Markdown reports and presentation summaries for human readers.
---

# 연구 보고서 작성

1. **독자와 결정**을 정한다. 첫 화면에서 독자가 어떤 선택을 할 수 있어야 하는가? 발표용이면 판단과 근거를 압축하고, 기술 검토용이면 비교 조건과 방법을 남긴다.
2. **근거를 대조한다.** Study 기록과 원본 metric에서 baseline, 평가 대상과 분모, 단위, 지표 방향, 실행 조건을 확인한다. 확인되지 않은 값은 미측정 또는 출처 미상으로 표시한다. 원본 기록과 manifest는 보존한다.
3. **정보를 선별한다.** 결정을 바꿀 주요 결과 3~5개 이내를 상단에 놓고 방법과 세부 분석은 해당 결론 아래에 둔다. 검증 실패가 결과의 유효성을 좌우하면 첫 요약에도 명시한다.
4. **독자의 질문 순서로 작성한다.** 목적과 핵심 결과, 기존 문제와 개선 원리, 평가 조건, 비교 결과, 한계와 다음 조치를 연결한다. 관찰과 해석을 구분하고 후속 실험에서 확인할 가설을 명시한다.
5. **원본과 초안을 대조하고 수정한다.** 요약과 결론을 다시 읽고 뜻이 모호한 표현은 관찰한 결과나 다음에 할 일로 풀어 쓴다. 전달 전 [품질 검토표](references/quality-rubric.md)를 적용한다. 출력은 기본적으로 ClickUp에도 붙여넣을 수 있는 Markdown을 사용한다.

초안에는 [보고서 템플릿](templates/research-report.md)의 필요한 절만 사용한다. 기술 설명과 표 구성은 [작성 가이드](references/writing-guide.md)를 참고한다. 처리 시간과 적용 조건은 [추론 최적화 예시](examples/inference-optimization.md), 지표 간 상충과 운영 판단은 [모델 학습 예시](examples/model-training.md)를 참고한다.
