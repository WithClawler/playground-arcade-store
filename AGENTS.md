# LOA Game Portal

- Formal project root: `/Volumes/BigHugeMemory/works/playground-arcade-store`; Slack `#loa`; existing GitHub upstream `doctor-clawler/playground-arcade-store`.
- `games/<id>/` contains maintained game source; `site/` contains the portal shell; `config/games.json` is the catalog. Playground originals are retained historical inputs, not build dependencies.
- For imports use `skills/host-playground-games/SKILL.md` and `docs/ADDING_GAMES.md`. Add source files explicitly, never blindly copy a workspace. Keep original playground projects unchanged.
- `npm run build` rebuilds Vite games and generates `public/`. Do not commit `public/`, `dist/`, dependencies, logs, screenshots from QA, credentials or machine-local env. Source thumbnails under `assets-source/thumbnails/` are product assets.
- Preserve the iframe sandbox and provenance filtering. Games use the parent-owned browser save bridge without same-origin permission. Follow `docs/BROWSER_SAVES.md`; test gameplay restoration after a browser restart. Do not claim Unity/Defold compatibility without testing.
- Run focused tests for changes, then `npm run build`, `npm test`, `npm run validate` and the browser smoke for packaging/catalog changes. Keep tests that mutate the manifest in `tests/catalog.test.mjs` to avoid parallel publish races.
- `npm run build:web` uses the `_ops` managed backend preview. Read `env.dev.local` and keep the central allocator; the shared web publication path returns the verified port-free `http://loa.home.arpa/` or channel/variation hostname.
- Push to the current upstream after validation. Pages builds from source. Confirm workflow and public HTTP results for authorized publication; DNS/HTTPS readiness is a separate check.

## 공통 웹 빌드 주소

웹 빌드·미리보기를 제공할 때는 [웹 배포](../_ops/docs/local-web-deployment.md)와 [내부 DNS](../_ops/docs/internal-dns.md)의 공통 계약을 따른다. 대표 `http://loa.home.arpa/`, 변형 `http://loa.<variation>.home.arpa/`를 포트 없이 제공하며 기존 별칭을 보존한다. 채널명은 소문자·`_` → `-`로 정규화한다.

백엔드는 `env.dev.local`과 중앙 allocator로 LAN에 bind하고 소유 listener·LAN HTTP·대표/변형 주소의 이번 빌드를 검증한 뒤 요청 thread에 결과를 반환한다. 기존 빌드·데이터 보존·인증·배포 gate는 유지하며, 웹 미지원 프로젝트에 이 지침만으로 새 웹 지원이나 상시 서비스를 만들지 않는다.
