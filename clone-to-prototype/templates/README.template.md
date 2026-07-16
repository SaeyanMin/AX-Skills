# {프로젝트/채널명} 화면설계 (현행본)

현행 화면을 자체완결 정적 프로토로 포팅하고 스펙과 함께 버전으로 관리하는 공간.

## 폴더 구조

```
{root}/
├── README.md · _templates/            # 규약·템플릿
├── specs/{화면키}/v{N}/spec.md · meta.json
└── prototypes/{화면키}/v{N}/index.html · style.css · index.js
```

채널이 여럿이면 상위에 채널 폴더(`com/`, `adm/` 등)를 두고 그 아래 `specs`/`prototypes`를 둔다.

## 규칙

- **specs / prototypes 별개 루트**, 그 아래 **화면키(플랫) → 버전 폴더(v1, v2…)**. 같은 화면키·버전으로 스펙↔프로토가 짝지어진다.
- **화면키**: 도메인 접두어로 충돌 방지 (`member-register`, `member-login`, `order-list`…).
- **그룹핑**: 폴더가 아니라 `meta.json`의 `groupName`.
- **프로토**: `index.html` + `style.css`(선택) + `index.js`(선택). 자체완결 정적(외부 의존 없음).

## 버전 관리

- 최초 = `v1/`. 스펙·프로토를 바꿀 땐 **새 버전 폴더(`v2/`)를 추가**하고 이전 버전은 보존(시점별 현행본 유지).
- `meta.json`의 `prototype.latest`를 최신 버전으로 갱신.
