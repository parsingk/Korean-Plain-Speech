# korean-plain-speech

Claude Code 답변을 **한국 개발자가 읽기 쉬운 한국어**로 바꾸는 output style 플러그인.

> [!IMPORTANT]
> **이 플러그인은 설치하는 즉시 답변 말투를 바꿉니다.**
> 기존에 설정해 둔 output style(Concise, Explanatory 등)이 있다면 그 설정을 덮어씁니다.
> 원래대로 돌리려면 `/plugin` 에서 이 플러그인을 비활성화하세요.

---

## 왜 만들었나

한국어로 답변받을 때 두 가지가 계속 걸립니다.

**하나, 영어를 그대로 옮긴 말투.** "이는 해당 설정이 적용되지 않았음을 의미합니다" 같은 문장은
문법은 맞지만 한국 사람이 쓰는 말이 아닙니다. 읽는 데 힘이 더 듭니다.

**둘, 코드 이야기부터 시작하는 설명.** 파일 이름과 함수 이름부터 꺼내면, 그 코드를 이미 아는
사람만 알아듣습니다. 기획자에게 공유할 수도, 나중에 다시 읽을 수도 없는 설명이 됩니다.

이 플러그인은 그 두 가지를 고칩니다.

---

## 무엇이 바뀌나

### 말투

| 설치 전 | 설치 후 |
|---|---|
| 이는 해당 파일이 존재하지 않음을 의미합니다 | 즉, 그 파일이 없습니다 |
| 캐시를 초기화하는 데 도움이 될 것입니다 | 캐시를 지우면 됩니다 |
| 당신의 코드베이스에서 확인이 필요합니다 | 이 프로젝트에서 확인해야 합니다 |
| 마이그레이션이 성공적으로 완료되었습니다 | 마이그레이션 끝났습니다 |

영어 기술 용어를 억지로 번역하지 않습니다. `hook`을 "갈고리"로, `race condition`을
"경합 조건"으로 바꾸지 않습니다. 한국 개발자들이 실제로 쓰는 말이 있으면 그걸 쓰고,
없으면 영어를 그대로 둡니다.

### 설명 구조

코드나 버그를 설명할 때 답변이 두 부분으로 나뉩니다.

**Flow** — 무슨 일이 순서대로 벌어지는지. 파일 이름도 함수 이름도 없이, 기획자가 읽고
이해할 수 있는 말로. 판단과 위험도 여기 들어갑니다.

**Technical** — 그 아래에 `file:line`, 타입, 실제 코드.

단, **짧은 질문에는 이 구조를 쓰지 않습니다.** "이 파일 어디 있어?"에 흐름 설명 세 문단이
붙으면 그것도 읽기 어려운 답변입니다.

---

## 설치

```
/plugin marketplace add parsingk/Korean-Plain-Speech
/plugin install korean-plain-speech@korean-plain-speech
```

설치 후 `/clear` 하거나 새 세션을 시작하면 적용됩니다.
output style은 세션 시작 때 한 번 읽히기 때문에, 현재 대화에는 바로 반영되지 않습니다.

## 끄기

```
/plugin
```

목록에서 `korean-plain-speech` 를 비활성화한 뒤 새 세션을 시작하면 원래 말투로 돌아갑니다.

---

## 알아둘 것

**코딩 동작은 건드리지 않습니다.** `keep-coding-instructions: true` 로 되어 있어서
Claude Code의 기본 소프트웨어 엔지니어링 지침은 그대로 유지되고, 말투 규칙만 위에 얹힙니다.
코드를 짜는 방식이나 도구를 쓰는 방식은 달라지지 않습니다.

**서브에이전트에는 적용되지 않습니다.** Explore나 Plan 같은 subagent는 자기 system prompt로
돌기 때문에 이 문체가 걸리지 않습니다. 다만 그 결과를 메인 대화가 다시 정리해서 보여주므로
실사용에서 크게 티나지는 않습니다.

**프로젝트 규칙은 여전히 CLAUDE.md에 씁니다.** 이 플러그인은 *어떻게 말하는가*만 다룹니다.
프로젝트 컨벤션이나 코드베이스 지식은 CLAUDE.md의 몫입니다.

---

## 문체를 고치고 싶다면

`output-styles/korean-plain-speech.md` 파일 하나가 이 플러그인의 전부입니다.
거슬리는 번역투가 있으면 표에 한 줄 추가하고 PR을 보내주세요.
추상적인 원칙보다 **실제로 겪은 문장 사례**가 훨씬 잘 먹힙니다.

---

## Requirements

Claude Code v2.1.91 이상. (`/output-style` 명령은 v2.1.91에서 제거됐습니다. 이 플러그인은
`force-for-plugin` 으로 자동 적용되므로 명령어를 직접 쓸 일은 없습니다.)

## License

Apache-2.0

---

## English

Makes Claude Code answer in Korean that Korean developers actually read comfortably.

Two problems it fixes: word-for-word translations from English that are grammatical but
unnatural, and explanations that open with file and function names so only someone who has
already read the code can follow them.

It ships a single output style with `keep-coding-instructions: true`, so Claude Code's
built-in software engineering behavior is untouched — only the voice changes.

**This plugin applies itself on install** (`force-for-plugin: true`) and overrides any output
style you had selected. Disable the plugin via `/plugin` to revert.

```
/plugin marketplace add parsingk/Korean-Plain-Speech
/plugin install korean-plain-speech@korean-plain-speech
```
