# AX-Skills

Personal, reusable [Claude Code](https://claude.com/claude-code) skills. Framework-agnostic and free of any private/company-specific data.

개인용 재사용 [Claude Code](https://claude.com/claude-code) 스킬 모음. 프레임워크 무관, 비밀정보 없음.

---

## `clone-to-prototype`

Port a **screen from an already-cloned frontend repo** into a self-contained static 3-file prototype (`index.html` / `style.css` / `index.js`), then open it directly in the browser — no dev server, no live app run.

이미 로컬에 **클론된 프론트엔드 레포의 현행 화면**을, 외부 의존성이 전혀 없는 정적 3파일(`index.html` / `style.css` / `index.js`) 프로토로 포팅하고 브라우저에서 바로 여는 스킬. 개발 서버·라이브 앱 실행 없음.

### Why / 배경

- **EN** — You often want a quick, shareable, dependency-free snapshot of an existing screen. This skill reads the real source (components, CSS, i18n strings) and reproduces the design, structure, labels, branches, and styles — instead of running the live app.
- **KO** — 기존 화면을 의존성 없이 빠르게 공유 가능한 스냅샷으로 만들고 싶을 때. 라이브 앱을 실행하는 대신 실제 소스(컴포넌트·CSS·i18n 문구)를 읽어 디자인·구조·라벨·분기·스타일을 재현한다.

### Prerequisite / 대전제

- **EN** — The reference frontend repo (and backend repo, if needed) must already be cloned locally. The skill never runs the live app (`npm run dev`, etc.).
- **KO** — 참고할 프론트엔드(및 필요시 백엔드) 레포가 이미 로컬에 클론되어 있어야 한다. 라이브 앱을 실행하지 않는다.

### Scope tiers / 커버 범위 티어

Chosen at the start via a question:

시작할 때 질문으로 고른다:

- **T1 Prototype only / 프로토만** — 3 files in a folder + `open`. Throwaway check, no versioning.
  3파일 + `open`. 임시 확인용, 버저닝·템플릿 없음.
- **T2 Versioned save / 버저닝 저장** — files saved under `prototypes/{screen-key}/v{N}/` + `meta.json`, previous versions preserved.
  `prototypes/{화면키}/v{N}/`에 저장 + `meta.json`, 이전 버전 보존.
- **T3 Screen-design set / 화면설계 세트** — T2 + `specs/{screen-key}/v{N}/spec.md` (case table), spec↔proto paired by screen-key/version.
  T2 + `specs/{화면키}/v{N}/spec.md`(케이스표), 스펙↔프로토 짝.

**Project conventions win / 자체 규약 우선** — for T2/T3, if the output location has its own conventions (`README.md`, `_templates/`, `CLAUDE.md`, existing `specs`/`prototypes`), the skill detects and follows them; otherwise it uses the generic templates in `templates/`.
T2/T3에서 출력 위치에 자체 규약이 있으면 감지해 그걸 따르고, 없을 때만 `templates/`의 범용 템플릿을 쓴다.

### Flow / 동작 흐름

1. **EN** Pick the scope tier (T1/T2/T3). **KO** 커버 범위 티어(T1/T2/T3) 선택.
2. Confirm the repo is cloned locally → if not, stop and clone first.
   대상 레포가 로컬에 클론돼 있는지 확인 → 안 돼 있으면 클론부터 안내하고 중단.
3. Ask which repo (local path) to reference — plus the backend repo path if branch/state logic needs it.
   어떤 레포(로컬 경로)를 참고할지 확인 — 분기·상태 근거가 필요하면 백엔드 경로도.
4. Ask which screen/component to prototype.
   어떤 화면/컴포넌트를 프로토로 만들지 확인.
5. Ask where to output (kept out of the reference repo); for T2/T3 detect project conventions.
   출력 위치 확인 (참고 레포를 오염시키지 않도록); T2/T3면 자체 규약 감지.
6. Read the source and port → output as code blocks **and** real files → `open index.html`.
   소스를 읽어 포팅 → 코드블록 출력 + 실제 파일 생성 → `open index.html`.

### Static 3-file rules / 정적 3파일 규칙

- No external CDN / font / CSS / JS / image URLs — everything inline or drawn in CSS.
  외부 CDN·폰트·CSS·JS·이미지 URL 금지 — 전부 인라인/CSS.
- No frameworks or libraries — Vanilla JS only.
  프레임워크·라이브러리 금지 — Vanilla JS만.
- No ES modules — classic scripts only.
  ES module 금지 — classic script만.
- No `localStorage`/`sessionStorage`/`alert`/`confirm`/`prompt`/`window.open`/`location` navigation/`eval`.
  스토리지·네이티브 다이얼로그·페이지 이탈·`eval` 금지.
- `index.js` runs as an IIFE (not wrapped in `DOMContentLoaded`).
  `index.js`는 `DOMContentLoaded` 대신 IIFE로 즉시 실행.
- Append to an `#app` container, never directly to `document.body`.
  `document.body` 직접 append 금지, `#app` 컨테이너에 append.
- Stable `id`s + semantic tags on major blocks.
  주요 블록에 안정적 `id` + 시맨틱 태그.

### Install / 설치

```bash
git clone https://github.com/SaeyanMin/AX-Skills.git
ln -sfn "$PWD/AX-Skills/clone-to-prototype" ~/.claude/skills/clone-to-prototype
```

### Usage / 사용

Trigger the slash command in Claude Code:

Claude Code에서 슬래시 커맨드로 트리거:

```
/clone-to-prototype
```
