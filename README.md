# 내 앱 디자인 업그레이드

기존 앱을 진단하고 적합한 UI 도구를 추천한 뒤, 별도 HTML 시안을 비교하고 선택한 디자인을 실제 앱에 적용하는 AI 스킬입니다.

**진단 → 추천 → HTML 시안 → 선택·수정 → 실제 적용 → 검증**

## 시작하기

설치한 AI 코딩 도구에서 앱 프로젝트를 열고 요청합니다.

```text
app-design-upgrade 스킬로 내 앱을 진단하고 HTML 시안을 보여줘.
비교할 가치가 있으면 2안을 제안해줘. 실제 앱에는 아직 적용하지 마.
```

시안을 검토한 뒤 다음처럼 이어갑니다.

```text
A안의 메뉴와 B안의 그래프를 조합해서 시안을 다시 보여줘.
```

```text
수정된 시안으로 확정할게. 실제 앱에 적용하고 검증해줘.
```

기본 동작은 별도 HTML 시안 제공까지입니다. 사용자가 선택과 적용을 요청하면 실제 앱 수정으로 이어집니다. “논의만” 요청하거나 작은 수정을 구체적으로 지정하면 해당 범위를 따릅니다.

## 설치

저장소가 비공개인 경우 GitHub 접근 권한이 있는 계정으로 로그인해야 내려받을 수 있습니다. 접근 권한이 없다면 전달받은 ZIP을 풀어 직접 설치합니다. 비공개 저장소의 링크만으로는 다른 사용자가 설치할 수 없습니다.

설치 대상은 저장소 전체가 아니라 `skills/app-design-upgrade` 폴더입니다. 기존 동명 스킬이 있으면 먼저 내용을 비교하고 별도로 보관하세요.

### AI에게 설치 요청

```text
https://github.com/Kyoungsoo2314/app-design-upgrade 저장소의
skills/app-design-upgrade 폴더를 현재 도구의 사용자 스킬로 설치해줘.
동일한 이름의 스킬이 있으면 덮어쓰지 말고 차이를 먼저 알려줘.
```

### 직접 설치

GitHub에서 `Code → Download ZIP`으로 내려받고 압축을 풉니다. `skills/app-design-upgrade` 폴더 전체를 아래 위치에 넣습니다.

| 도구 | macOS / Linux | Windows 사용자 폴더 기준 |
|---|---|---|
| Codex | `~/.codex/skills/app-design-upgrade` | `%USERPROFILE%\.codex\skills\app-design-upgrade` |
| Claude Code | `~/.claude/skills/app-design-upgrade` | `%USERPROFILE%\.claude\skills\app-design-upgrade` |

Codex에서 `CODEX_HOME`을 별도로 설정했다면 해당 폴더의 `skills`를 사용합니다. WSL에서 도구를 실행한다면 Windows 폴더 대신 WSL 홈 디렉터리에 설치합니다.

설치 위치 바로 아래에 `SKILL.md`, `references`, `agents`가 있어야 합니다. `app-design-upgrade/app-design-upgrade/SKILL.md`처럼 폴더가 중복되지 않도록 확인하세요. 설치 후 새 대화에서 스킬을 호출하고, 표시되지 않으면 도구를 다시 시작합니다.

- Codex 호출: `$app-design-upgrade`
- Claude Code 호출: `/app-design-upgrade`
- 스킬을 지원하지 않는 도구: [공식 가이드](skills/app-design-upgrade/references/guide.md)를 첨부하여 사용합니다.

Claude Code의 설치 위치와 호출 방식은 [공식 스킬 문서](https://code.claude.com/docs/en/skills)를 참고하세요. 다른 도구에서는 해당 도구의 스킬 지원 방식에 맞춰 설치합니다.

## 구성

```text
skills/app-design-upgrade/
  SKILL.md                  실행 지침
  agents/openai.yaml        Codex 표시 정보
  references/guide.md        공식 가이드와 도구 참고 목록
  references/proposals.md    시안 비교 구성과 선택 기록 기준
```

[공식 가이드](skills/app-design-upgrade/references/guide.md)에는 상세 사용법, 라이브러리 후보, 디자인 기준과 완료 조건이 포함되어 있습니다. `guide.md`가 이 저장소의 상세 가이드 기준본이며, 실행 범위를 바꾸면 `SKILL.md`와 함께 확인합니다.

고정 HTML 템플릿 대신 앱의 업무에 맞게 시안을 만들도록 합니다. 시안은 가상 데이터를 사용하고 운영 API와 연결하지 않습니다. 선택한 디자인은 현재 프레임워크와 실제 기능에 맞춰 적용합니다.

## 실행 조건

코드 확인, 파일 생성과 브라우저 검수가 가능한 AI 코딩 도구에서 전체 흐름을 사용할 수 있습니다. 특정 UI 라이브러리, 유료 서비스, MCP 또는 별도 에이전트를 필수로 요구하지 않습니다. 실행 기능이 없는 환경에서는 분석·시안·검증 가능 범위를 구분해 안내합니다.

이 저장소에는 지침과 문서만 포함됩니다. 스킬 설치 자체가 프로젝트를 수정하거나 외부 서비스에 연결하지 않습니다. 실행 시 AI는 사용자의 요청과 도구의 권한에 따라 작업합니다.

## 검증 범위

배포 시 스킬 구조, YAML 메타데이터, 내부 문서 링크와 설치 파일 복사를 확인합니다. 이러한 검사는 실제 프로젝트에서의 디자인 품질이나 모든 도구·운영체제의 동작을 보장하지 않습니다. 각 앱의 시안과 적용 결과는 실행 과정에서 검수합니다.

## 라이선스

MIT License. 문서와 스킬을 사용·수정·재배포할 수 있으며 라이선스와 저작권 고지를 유지해야 합니다. 참고한 외부 라이브러리에는 각각의 라이선스가 적용됩니다.
