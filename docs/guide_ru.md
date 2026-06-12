# Руководство (русский) — как управлять каталогом homgorn-catalog

Это пошаговые инструкции специально для вас (на русском). Я буду обновлять этот файл после важных изменений.

1) Безопасность токенов
- Никогда не публикуйте PAT в открытых чатах. Если токен был раскрыт — немедленно отзовите и замените.
- Храните PAT в GitHub Secrets: Settings → Secrets and variables → Actions → New repository secret.
  - Обязательный секрет: SYNC_PAT (используется workflow sync-forks и скрипты).
  - При интеграции Cloudflare: CLOUDFLARE_API_TOKEN.

2) Как включить Git LFS (локально)
- Установите Git LFS: `git lfs install`
- В репозитории уже есть `.gitattributes`, добавьте файлы дизайна: `git add designs/owner/repo/*.jpg` → `git commit` → `git push`.

3) Запуск индексации вручную (локально)
- Установите Python 3.11 и зависимости: `pip install PyGithub pyyaml`
- Клонируйте репо: `git clone https://github.com/homgorn/homgorn-catalog.git`
- Экспортируйте секрет как переменную окружения (на локальной машине): `export SYNC_PAT=<ваш_PAT>`
- Запустите: `python scripts/generate_index.py` — это создаст `index.json` и обновит `index.md`.

4) Тестовая синхронизация форков (dry-run)
- Workflow `sync-forks.yml` поддерживает запуск вручную (workflow_dispatch).
- По умолчанию скрипт `scripts/sync_forks.py` создаёт Pull Request в форке с изменениями из upstream (в dry-run настройте скрипт сначала печатать действия без создания PR).

5) Бэкапы
- Бэкапы каталога сохраняются в `backups/` (снимки index.json, LLM outputs, сборки сайта).
- Установка внешнего хранилища (Cloudflare R2 / S3) в roadmap — позже.

6) Дизайны и референсы
- Храните референсы в `overlays/{owner}/{repo}/designs/`.
- Для больших объёмов используйте Git LFS или R2/S3.

7) Кластеризация и теги
- Кластеризация запускается автоматически: 3 уровня + до 5 тегов на репо.
- Теги извлекаются из README, description и GitHub topics, с дообработкой LLM.

8) Логи и память проекта
- Все действия логируются в `chat-log.md` и в `logs/`.
- При необходимости можно экспортировать `index.json`, SQL dump (`db/schema.sql`) и graph dump (`graph/schema.cypher`).

9) Вопросы и управление
- Если хотите изменить стратегию синка (rebase vs merge vs PR-only) — укажите в комментарии.
- Напоминание: Cloudflare интеграция — в roadmap. Я напомню вам позже, как вы просили.

