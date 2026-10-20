# Cloud PVE API

[Русский](#русский) · [English](#english)

## Русский

Публичная спецификация **клиентского API** Cloud PVE (панель управления VPS): OpenAPI 3.1 и история изменений.
Репозиторий обновляется автоматически при каждом релизе, вручную его править не нужно: изменения вносятся в приватном
репозитории продукта и попадают сюда с тегом релиза.

| Файл | Что внутри |
|---|---|
| [`openapi.yaml`](openapi.yaml), [`openapi.json`](openapi.json) | Спецификация OpenAPI 3.1 клиентского API (`/api/v1`). Тот же документ отдаёт ваша панель: `https://<адрес панели>/api/v1/openapi.yaml` |
| [`CHANGELOG.md`](CHANGELOG.md) | История изменений по версиям API. Тот же текст: `https://<адрес панели>/api/v1/changelog.md` |

Адрес панели: в `servers` стоит заглушка `https://my.example.com`; подставьте адрес вашей панели (спецификация, которую отдаёт сама панель, уже содержит его).

### Версии и совместимость

- Версия API в пути (`/api/v1`) и в `info.version` спецификации (семвер, `1.0.0`). Теги этого репозитория совпадают с тегами релизов продукта.
- Внутри v1 допустимы только совместимые изменения: новые эндпоинты, необязательные параметры, поля ответов, значения enum. Клиент должен игнорировать неизвестные поля и считать enum открытыми.
- Несовместимые изменения выходят как `/api/v2`; v1 после этого работает не менее 6 месяцев.
- Устаревшие операции помечены `deprecated: true` и `x-sunset`, а их ответы содержат заголовки `Deprecation` (RFC 9745) и `Sunset` (RFC 8594).

### Как пользоваться

Импортируйте `openapi.yaml` в Postman или Insomnia либо сгенерируйте клиент, например
`openapi-generator-cli generate -i openapi.yaml -g python -o client`. Скрипты авторизуются API-токеном
(`Authorization: Bearer cpv_...`), который создаётся в клиентской панели, раздел «API-токены».

Вопросы и ошибки в документации: обращайтесь в поддержку вашего хостинг-провайдера.

## English

The public specification of the Cloud PVE **client API** (VPS control panel): OpenAPI 3.1 and the changelog.
This repository is updated automatically on every release and is not edited by hand: changes are made in the private
product repository and arrive here together with the release tag.

| File | Contents |
|---|---|
| [`openapi.yaml`](openapi.yaml), [`openapi.json`](openapi.json) | The OpenAPI 3.1 specification of the client API (`/api/v1`). Your panel serves the same document: `https://<panel address>/api/v1/openapi.yaml` |
| [`CHANGELOG.md`](CHANGELOG.md) | Changes by API version. The same text: `https://<panel address>/api/v1/changelog.md` |

Panel address: `servers` holds the placeholder `https://my.example.com`; use the address of your panel (the specification served by the panel itself already has it).

### Versions and compatibility

- The API version is in the path (`/api/v1`) and in `info.version` of the specification (semver, `1.0.0`). The tags of this repository match the product release tags.
- Within v1 only backwards-compatible changes are made: new endpoints, optional parameters, response fields, enum values. Clients must ignore unknown fields and treat enums as open.
- Breaking changes are released as `/api/v2`; v1 keeps working for at least 6 months after that.
- Deprecated operations are marked `deprecated: true` and `x-sunset`, and their responses carry the `Deprecation` (RFC 9745) and `Sunset` (RFC 8594) headers.

### Usage

Import `openapi.yaml` into Postman or Insomnia, or generate a client, for example
`openapi-generator-cli generate -i openapi.yaml -g python -o client`. Scripts authenticate with an API token
(`Authorization: Bearer cpv_...`) created in the client panel, section API tokens.

Questions and documentation errors: contact the support of your hosting provider.
