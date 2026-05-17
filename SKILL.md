---
name: fact-checker
description: "삼각측량·수치정합·출처등급 기반 팩트체크 엔진. 문서·주장·수치의 참/거짓/부분일치/오도 가능성을 판정하고 수정안을 제시한다. P1: 팩트체크, fact check, 사실확인, 수치검증, 교차검증. P2: 팩트체크해줘, 검증해줘, verify. P3: triangulation, source grading, numerical consistency. P5: 검증보고서로, .md로. NOT: 맞춤법(→submission-cleanup), 리서치확장(→research-skill), 글쓰기(→shaper-skill)."
license: Proprietary
---

# Fact Checker

팩트체크, fact check, 사실확인, 수치검증, 교차검증 요청이 오면 문서 안의 주장·숫자·고유명사를 분리해 검증한다. 목표는 그럴듯한 서술이 아니라 제출 전 위험한 오류를 잡는 것이다.


## Skill Boundaries

- **하는 것** — "삼각측량·수치정합·출처등급 기반 팩트체크 엔진.
- **안 하는 것** — 맞춤법(→submission-cleanup), 리서치확장(→research-skill), 글쓰기(→shaper-skill)."

## When to Use

- 사용자가 "팩트체크해줘", "검증해줘", "verify." 같은 표현으로 발동
- 도메인 작업이 필요한 시점
- **안 쓸 때** — 맞춤법(→submission-cleanup), 리서치확장(→research-skill), 글쓰기(→shaper-skill)."


## Prerequisites

| # | 체크 | 미충족 시 |
|---|------|-----------|
| 1 | 대상·입력 명확 (스킬 발동 의도 확인) | 1줄 확인 후 진입 |
| 2 | references/ 폴더 접근 가능 | inline fallback |
| 3 | scripts/ 실행 권한 | 권한 보정 후 재시도 |


## 절대 규칙

1. 주장, 근거, 판단을 분리한다.
2. 최신 정보·법령·가격·인물·회사·일정처럼 변동 가능성이 있으면 웹 또는 원자료로 확인한다.
3. 수치는 단위, 기준일, 분모, 반올림을 함께 본다.
4. 확실하지 않은 항목은 추정으로 메우지 않고 `확인 필요`로 남긴다.
5. 수정안은 원문 의도를 보존하되 위험한 단정만 줄인다.

## 모드

| 모드 | 사용 상황 | 출력 |
|---|---|---|
| LIGHT | 숫자·날짜만 빠르게 확인 | 오류 후보와 수정안 |
| DEEP | 제출 전 문서 전수 검증 | 판정표 + 위험도 + 수정안 |

## 실행

1. 원문에서 검증 대상 문장을 추출한다.
2. 각 항목을 `사실 주장`, `수치`, `날짜`, `고유명사`, `인과 주장`으로 나눈다.
3. 원자료 또는 신뢰도 높은 출처로 확인한다.
4. `TRUE`, `PARTIAL`, `FALSE`, `MISLEADING`, `UNVERIFIED` 중 하나로 판정한다.
5. 제출 문서에 바로 넣을 수 있는 수정 문장을 제시한다.

references/ 자료는 모두 읽고 시작하지 않는다. 숫자, 삼각측량, 추론, 보정 중 필요한 축만 연다.

## 출력 형식

| 항목 | 원문 | 판정 | 근거 | 수정안 |
|---|---|---|---|---|

필요하면 마지막에 `맹점`을 1~2줄로만 붙인다.

## Output Path

| 산출물 | 경로 |
|---|---|
| 주 산출물 | `mnt/outputs/fact-checker_{topic}_{YYYY-MM-DD}.md` |
| 형식 | 검증보고서로, .md로. |
| 리서치 결과 (해당 시) | `{VAULT}/_skills research/fact-checker/{YYYY-MM-DD}_{topic}.md` |

## Reference Index

| 파일 | 내용 | 언제 |
|---|---|---|
| `references/axis-deduction.md` | axis deduction | 해당 단계 진입 시 |
| `references/axis-numerical.md` | axis numerical | 해당 단계 진입 시 |
| `references/axis-triangulation.md` | axis triangulation | 해당 단계 진입 시 |
| `references/llm-weakness.md` | llm weakness | 해당 단계 진입 시 |
| `references/tolerance.md` | tolerance | 해당 단계 진입 시 |


## Next Phase

본 스킬 작업 후 자연스럽게 이어지는 흐름:

- 후속 작업 → `submission-cleanup`
- 후속 작업 → `research-skill`
- 후속 작업 → `shaper-skill`

## Failure Modes (Gotchas)

| 함정 | 대응 |
|---|---|
| 출처가 많다는 이유로 참이라고 판단 | 가장 원출처에 가까운 자료를 우선한다 |
| 통계 기준연도 누락 | 기준일·표본·분모를 같이 적는다 |
| 부분 사실을 전체 사실처럼 확대 | `PARTIAL` 또는 `MISLEADING`으로 분리한다 |
| ❌ 소문 출처를 여러 개 모아 참으로 처리 | ✅ 원자료 또는 1차 발표를 기준으로 다시 판정 |

## Self-Check

- P1 키워드가 본문에도 등장하는가?
- 판정과 수정안이 분리되어 있는가?
- 변동 가능 정보는 현재성 검증을 거쳤는가?
