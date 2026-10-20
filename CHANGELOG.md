# Cloud PVE API: changelog / История изменений

Клиентский API (`/api/v1`) версионируется и обратно совместим: внутри v1 только аддитивные изменения, несовместимые уходят в `/api/v2`
с перекрытием не менее 6 месяцев и заголовками `Deprecation` / `Sunset`.
The client API (`/api/v1`) is versioned and backwards compatible: within v1 only additive changes; breaking changes go to
`/api/v2` with at least 6 months of overlap and `Deprecation` / `Sunset` headers.

Версия API — `info.version` спецификации. Записи идут от новых к старым.
The API version is `info.version` of the specification. Newest entries first.

## 1.0.0 — первый публичный релиз / first public release

Клиентский API опубликован как продукт: все маршруты лежат под `/api/v1`, спецификация OpenAPI 3.1 — `GET /api/v1/openapi.yaml` и
`GET /api/v1/openapi.json`, история изменений — `GET /api/v1/changelog.md`.
The client API is published as a product: every route lives under `/api/v1`; the OpenAPI 3.1 specification is served at
`GET /api/v1/openapi.yaml` and `GET /api/v1/openapi.json`, the changelog at `GET /api/v1/changelog.md`.

### Изменено / Changed

- Все маршруты клиентского API перенесены с `/api/...` на `/api/v1/...`. Псевдонимов нет: прежние пути `/api/...` вне `/api/v1` отвечают
  `404 not_found` (`application/problem+json`). Это единственное несовместимое изменение; оно относится к закрытой бете, до релиза.
  Не изменились `/auth/*` (SSO и вход из браузера), `/ws/console` (консоль) и `/healthz`.
  Every client API route moved from `/api/...` to `/api/v1/...`. There are no aliases: the former `/api/...` paths outside
  `/api/v1` answer `404 not_found` (`application/problem+json`). This is the only breaking change and it predates the
  release (closed beta). `/auth/*` (SSO and browser sign-in), `/ws/console` (the console) and `/healthz` are unchanged.

### Эндпоинты v1 / Endpoints in v1

| | |
|---|---|
| Аккаунт / Account | `POST /api/v1/auth/logout`, `GET /api/v1/config`, `GET /api/v1/me`, `PATCH /api/v1/me` |
| Серверы / Servers | `GET /api/v1/vms`, `GET`/`PATCH /api/v1/vms/{id}`, `GET /api/v1/vms/{id}/templates`, `GET /api/v1/vms/{id}/metrics`, `GET /api/v1/vms/{id}/operations` |
| Действия / Actions | `POST /api/v1/vms/{id}/power`, `/reset-password`, `/reinstall`, `/console`; `PUT /api/v1/vms/{id}/ips/{ip}/rdns` |
| Операции / Operations | `GET /api/v1/operations/{id}`, `POST /api/v1/operations/{id}/reveal-secret` |
| Аудит / Audit | `GET /api/v1/audit` |
| API-токены / API tokens | `GET`/`POST /api/v1/api-tokens`, `GET /api/v1/api-tokens/scopes`, `DELETE /api/v1/api-tokens/{id}` |
| Документация / Docs | `GET /api/v1/openapi.yaml`, `GET /api/v1/openapi.json`, `GET /api/v1/changelog.md` |

### Добавлено / Added

- Метаданные версии в спецификации: `info.version: 1.0.0`, `info.x-api-lifecycle` (стадия, политика совместимости, срок перекрытия).
  Version metadata in the specification: `info.version: 1.0.0` and `info.x-api-lifecycle` (stage, compatibility policy, overlap period).
- Политика устаревания: операция помечается `deprecated: true` и `x-sunset`, а её ответы получают заголовки `Deprecation` (RFC 9745)
  и `Sunset` (RFC 8594). Устаревших операций в 1.0.0 нет.
  Deprecation policy: a deprecated operation gets `deprecated: true` and `x-sunset`, and its responses carry the `Deprecation`
  (RFC 9745) and `Sunset` (RFC 8594) headers. Nothing is deprecated in 1.0.0.

<!--
Как добавить запись / How to add an entry:
  make api-changelog BASE=<ref>   # oasdiff changelog между <ref> и рабочим деревом; вставьте результат выше новой версии
  и поднимите info.version в api/openapi.yaml (MINOR для новых возможностей, PATCH для правок описаний).
-->
