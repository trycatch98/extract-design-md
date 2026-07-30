<div align="center">

<p><a href="README.md">English</a> · <strong>한국어</strong></p>

<h1>extract-design-md</h1>

<p>
frontend 코드에 흩어진 디자인 규칙을<br>
근거가 분명하고 재사용 가능한 <code>DESIGN.md</code>로 정리합니다.
</p>

[![DESIGN.md 0.4.0](https://img.shields.io/badge/DESIGN.md-0.4.0-2563EB?style=classic)](https://github.com/google-labs-code/design.md)
[![Agent Skill](https://img.shields.io/badge/Agent-Skill-111827?style=classic)](skills/extract-design-md)
[![Apache License 2.0](https://img.shields.io/badge/License-Apache--2.0-64748B?style=classic)](LICENSE)

<p>
  <a href="#주요-특징">특징</a> ·
  <a href="#설치">설치</a> ·
  <a href="#사용-방법">사용</a> ·
  <a href="#결과-예시">예시</a>
</p>

</div>

---

`extract-design-md`는 기존 frontend codebase를 분석해 project root에 검토 가능한 `DESIGN.md`를 만듭니다. 완성된 문서에는 색상, typography, 간격, 형태, component, responsive behavior, 접근성, theme, motion에 관한 지침이 담깁니다. coding agent는 이후 UI를 만들거나 수정할 때 이 지침을 계속 활용할 수 있습니다.

> source code를 가장 중요한 근거로 삼습니다. 같은 앱의 로컬 실행 주소나 웹사이트 URL을 함께 제공하면 runtime에 실제로 적용된 디자인도 추가로 확인할 수 있습니다.

이 Skill은 `0.4.0`으로 고정한 [Google Labs DESIGN.md format specification](https://github.com/google-labs-code/design.md)을 따릅니다.

## 주요 특징

| 결과물 | 쓰임새 |
|---|---|
| project root의 `DESIGN.md` | coding agent가 계속 참고할 수 있는 디자인 지침을 제공합니다 |
| 근거가 확인된 규칙 | 사용하지 않는 값이나 추측이 project의 디자인 기준으로 굳어지는 것을 막습니다 |
| 기계가 읽을 수 있는 Token | 정확한 색상, typography, 간격, 형태, component 값을 보존합니다 |
| 사람이 이해하기 쉬운 설명 | 각 디자인 규칙을 언제, 왜 적용해야 하는지 알려줍니다 |
| 검토를 거친 업데이트 | 기존 `DESIGN.md`를 확인 없이 덮어쓰는 일을 막습니다 |

## DESIGN.md 생성 과정

<div align="center">

<code>frontend source</code> → <code>근거 기반 분석</code> → <code>선택적 runtime 확인</code> → <code>검토된 DESIGN.md</code>

</div>

## 분석 대상

Skill은 다음 항목을 차례로 확인합니다.

1. Design Token, theme 파일, Tailwind 설정
2. global CSS와 CSS Custom Property
3. 공통으로 사용하는 UI component
4. 주요 layout과 대표 page
5. 특정 page에만 적용되는 예외 규칙

project 안에서 근거를 찾을 수 있는 디자인 결정만 추출합니다. 설치된 dependency, build 결과물, cache, generated code, test snapshot, secret, environment 파일은 분석하지 않습니다.

## 설치

### coding agent에게 설치 요청하기 (권장)

Agent Skills를 지원하는 coding agent에게 다음 내용을 그대로 요청합니다.

```text
다음 GitHub 경로에 있는 extract-design-md Agent Skill을 설치해줘.
https://github.com/trycatch98/extract-design-md/tree/main/skills/extract-design-md
```

### Skills CLI

지원되는 coding agent와 설치 범위를 직접 선택하려면 [`skills` CLI](https://github.com/vercel-labs/skills)를 사용할 수 있습니다.

```bash
npx skills add https://github.com/trycatch98/extract-design-md/tree/main/skills/extract-design-md
```

이 명령은 실행 시점의 최신 Skills CLI release를 사용합니다. 이 README를 작성한 시점에는 Skills CLI `1.5.21`을 실행하려면 Node.js `22.20` 이상과 npm이 필요합니다. Node.js 버전 오류가 발생하면 현재 [package 요구 사항](https://github.com/vercel-labs/skills/blob/main/package.json)을 확인하세요.

## 사용 방법

Skill 이름을 분명하게 적어 요청합니다.

```text
$extract-design-md를 사용해 이 frontend project를 분석하고 DESIGN.md를 만들어줘.
```

runtime 확인이 필요하다면 같은 앱의 URL도 함께 제공합니다.

```text
$extract-design-md를 사용해 이 frontend project를 분석하고 DESIGN.md를 만들어줘. http://localhost:3000의 화면과도 비교해줘.
```

결과는 기본적으로 분석 대상 project의 root에 만들어집니다. 기존 `DESIGN.md`가 있다면 바로 교체하지 않고, 먼저 검토할 수 있는 업데이트안을 제시합니다.

## 결과 예시

아래는 실제 결과를 짧게 줄인 예시입니다.

```markdown
---
name: Acme Dashboard
description: 작업에 집중할 수 있는 운영 화면
colors:
  primary: "#2457D6"
  surface: "#FFFFFF"
typography:
  body:
    fontFamily: Inter
    fontSize: 1rem
spacing:
  md: 16px
rounded:
  control: 8px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    rounded: "{rounded.control}"
    padding: "{spacing.md}"
---

## Overview

정보를 먼저 보여주는 간결한 layout과 분명한 시각적 위계를 사용합니다.

## Colors

Primary blue는 실행할 수 있는 항목과 선택된 상태를 나타냅니다. White는 주요 content surface에 사용합니다.

## Components

Primary button에는 primary color, 중간 크기의 간격, 공통 control radius를 적용합니다.
```

실제 문서에는 대상 project에서 근거를 확인한 규칙만 들어갑니다. 필요한 경우 공식 명세의 다른 section이나 근거가 있는 추가 section도 포함될 수 있습니다.

## 호환성 및 버전 관리

| 대상 | 고정된 값 |
|---|---|
| 명세 tag | `0.4.0` |
| 명세 commit | `9bf8eae` |
| validator | `@google/design.md@0.4.0` |

새 명세 release가 나와도 자동으로 바뀌지 않습니다. 포함된 명세와 Skill을 함께 검토한 뒤 새 버전으로 업데이트해야 합니다.

source 분석 방법은 [Google Labs Code의 `extract-design-md` Agent Skill](https://github.com/google-labs-code/stitch-skills/tree/main/plugins/stitch-design/skills/extract-design-md)을 참고해 이 Skill에 맞게 조정했습니다. 이 구현은 Google Labs DESIGN.md `0.4.0` 형식으로 문서를 만들고 검사합니다.

## 라이선스 및 출처

이 project는 Apache License 2.0으로 배포됩니다. Skill에는 같은 License로 제공되는 Google `DESIGN.md` format specification의 tag `0.4.0`, commit `9bf8eae` snapshot이 포함되어 있습니다. 포함된 명세 파일에는 metadata와 출처 header만 추가했으며 명세 본문은 바꾸지 않았습니다. 자세한 출처는 [`NOTICE`](NOTICE)를 확인하세요.

질문이나 버그 제보는 [GitHub Issues](https://github.com/trycatch98/extract-design-md/issues)에 남겨 주세요.
