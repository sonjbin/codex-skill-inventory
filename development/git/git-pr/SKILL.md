---
name: git-pr
description: Repository AGENTS.md 규칙 기반의 Pull Request 생성 가이드
---

# git-pr Skill

## 목적
- PR 생성 시 제목/본문/브랜치 규칙을 표준화한다.

## 기본 동작
- 기본 base 브랜치: `develop`
- 기본 head 브랜치: 현재 작업 브랜치
- 사용자가 base/head를 명시하면 사용자 입력을 우선한다.

## 필수 규칙
- 브랜치 정보는 PR 생성 직전에 반드시 사용자에게 1회 재확인한다.
- PR은 단일 논리 목적만 포함한다.
- PR 제목 prefix는 다음 중 하나를 사용한다:
  - `add:` 새로운 파일/에셋/설정을 추가할 때 사용
  - `feat:` 사용자/시스템 관점 기능을 추가하거나 확장할 때 사용
  - `fix:` 일반 버그를 수정할 때 사용
  - `hotfix:` 즉시 대응이 필요한 치명적 문제를 수정할 때 사용
  - `refactor:` 동작 변경 없이 구조를 개선할 때 사용
  - `docs:` 문서 변경(README, 가이드, 주석성 문서 등)일 때 사용
  - `chore:` 빌드/CI/도구/유지보수성 작업 등 운영성 변경일 때 사용
  - `demo:` 데모/실험/프로토타입 성격 변경일 때 사용
- Labels는 목적에 맞게 부여한다:
  - `feature`, `bug`, `enhancement`, `documentation`
- Assignees 는 pr 생성하는 계정 user로 지정한다.

## 실행 절차
1. PR 대상 브랜치를 수집한다.
- 기본값: `head=$(git branch --show-current)`, `base=develop`
- 완료 조건: head/base 후보가 정리됨.
- 검증 방법: `git branch --show-current` 출력 확인.

2. 사용자에게 최종 브랜치 확인을 요청한다.
- 완료 조건: `head -> base` 조합이 사용자에게 명시적으로 확인됨.
- 검증 방법: 사용자 확인 응답 확보.

3. 제목과 본문을 규칙에 맞춰 구성한다.
- 완료 조건: 제목 prefix와 본문 템플릿 섹션이 모두 충족됨.
- 검증 방법: `templates/pr_body.md` 항목 충족 여부 체크.

4. PR을 생성하고 결과를 검증한다.
- 완료 조건: PR URL 또는 번호가 확인됨.
- 검증 방법: `gh pr create` 결과/`gh pr view` 확인.

## 템플릿 사용
- 기본 본문 템플릿: `templates/pr_body.md`
- `gh pr create` 시 개행 보존을 위해 `--body-file` 사용을 우선한다.

## 중단 조건
- 브랜치 정보 미확정
- 제목 prefix 부적합
- 사용자 확인 없이 PR 생성 시도
