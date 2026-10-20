# taiga-arm64

Сборка Docker-образов [Taiga](https://taiga.io) под `linux/arm64` (Raspberry Pi и т.п.).
Официальные образы `taigaio/*` на Docker Hub собраны только под amd64.

Workflow берёт последний релизный тег каждого компонента из `github.com/taigaio/*`,
собирает его официальный `docker/Dockerfile` на ARM-раннере GitHub и публикует в GHCR:

| Компонент | Образ |
|---|---|
| taiga-back | `ghcr.io/thehighestmath/taiga-back` |
| taiga-front | `ghcr.io/thehighestmath/taiga-front` |
| taiga-events | `ghcr.io/thehighestmath/taiga-events` |
| taiga-protected | `ghcr.io/thehighestmath/taiga-protected` |

Теги: версия upstream (`6.10.3`) и `latest`.

## Когда собирается

- при пуше в `main`;
- каждый понедельник по расписанию — если вышла новая версия;
- вручную: Actions → *Build Taiga arm64 images* → *Run workflow* (галочка `force` — пересобрать существующую версию).

Если образ с текущей версией уже есть, сборка пропускается.

## Использование

В `docker-compose.yml` из [taiga-docker](https://github.com/taigaio/taiga-docker) замените
`taigaio/<компонент>:latest` на `ghcr.io/thehighestmath/<компонент>:latest`.

## Патчи к upstream

- **taiga-front**: в Dockerfile версия папки при распаковке плагинов не совпадает
  с версией скачиваемого архива — заменяем её на шаблон `*`.
