# fact-checker

> 🇺🇸 [English README](./README.md)

**삼각측량·연역·수치정합·LLM보정 4축 기반 팩트체크 엔진. 문서 내 팩트를 자동 추출→검색 검증→판정→수정안 생성. LIGHT/DEEP 2모드.**

## 사전 요구

- **Claude Cowork 또는 Claude Code** 환경
- 웹 검색 접근 (소스 검증용)

## 목표

문서에는 매출 수치, 날짜, 비율, 시설 규모 같은 팩트가 포함된다. 반올림, 단위 혼동, 오래된 소스로 인해 실제와 어긋날 수 있다. 이 스킬은 검증 가능한 모든 팩트를 체계적으로 추출하고, 독립 소스와 교차검증한 뒤, 수정안까지 생성한다.

## 사용 시점 & 방법

`"팩트체크해줘"` + 파일 경로. **LIGHT**는 숫자·날짜·수량만, **DEEP**(기본)은 인과·누락까지 전수 검증. 검증 후 수정안을 제시하고 컨펌 후 일괄 적용.

## 사용 사례

| 상황 | 프롬프트 | 동작 |
|---|---|---|
| 제안서 제출 전 검토 | `"이 제안서 팩트체크해줘"` | DEEP: 5W1H 추출 → 15+회 검색 → 수정안 보고 |
| 빠른 숫자 확인 | `"라이트 팩트체크 — 숫자만"` | LIGHT: When+Where+How much 3축만 |
| IR 자료 준비 | `"IR 자료 수치 검증해줘"` | 엄격 허용치(소수점), Python 산술 전수 |

## 주요 기능

- **5W1H 추출** — Who/What/When/Where/How much/Why 6축으로 빠짐없이 추출
- **소스 등급(S1~S4)** — 공시>업종지>일반지>위키. 등급 없는 판정 금지
- **Python 산술 검증** — 비율은 분자/분모 나눗셈으로 확인. 97.94% vs 98.26% 차이 포착
- **LLM 취약점 보정** — 괄호·표·접힘 내부 수치를 2패스로 재스캔
- **용도별 허용 임계** — IR은 소수점 필수, 제안서는 반올림 허용. 맥락 인식 판정
## 연동 스킬

- **[research-frame](https://github.com/jasonnamii/research-frame)** — 팩트체크 중 지식 공백 발견 시 딥 리서치
- **[trigger-dictionary](https://github.com/jasonnamii/trigger-dictionary)** — 부재 증거 탐지에 프리모르템 사고 활용

## 설치

```bash
git clone https://github.com/jasonnamii/fact-checker.git ~/.claude/skills/fact-checker
```

## 업데이트

```bash
cd ~/.claude/skills/fact-checker && git pull
```

`~/.claude/skills/`에 배치된 스킬은 Claude Code 및 Cowork 세션에서 자동으로 사용 가능합니다.

## Cowork Skills

25개 이상의 커스텀 스킬 중 하나입니다. 전체 카탈로그: [github.com/jasonnamii/cowork-skills](https://github.com/jasonnamii/cowork-skills)

## 라이선스

MIT License — 자유롭게 사용, 수정, 공유 가능합니다.