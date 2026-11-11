# nimbx-versions

Публичный источник «последней версии» для приложения NimbX.
Используется встроенной проверкой обновлений: приложение читает `version.json`, сравнивает с установленной версией и, если сервер выше, предлагает обновление (кнопка ведёт в RuStore).

## Первичная настройка (один раз)

1. На GitHub создай публичный репозиторий **`nimbx-versions`** (New repository → Repository name: `nimbx-versions` → Public → Create).
2. Заливь содержимое этой папки в `main`:
   ```bash
   git init
   git add .
   git commit -m "init version.json"
   git remote add origin https://github.com/nix19875-lgtm/nimbx-versions.git
   git branch -M main
   git push -u origin main
   ```
3. Включи GitHub Pages: репозиторий → **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main` `/ (root)` → Save (хватит примерно минуты).
4. Проверка: открой `https://nix19875-lgtm.github.io/nimbx-versions/version.json` — должен показаться JSON.

## Обновление версии (после публикации APK в RuStore)

Вручную поменяй `"version"` в `version.json` и запушь, либо из корня проекта:

```bash
node app/scripts/bump-version-json.mjs          # берёт versionName из android/app/build.gradle
node app/scripts/bump-version-json.mjs 1.19     # или явно указать версию
```

Затем `git add version.json && git commit -m "bump to 1.19" && git push`.
Через ~1 минуту новая версия начнёт предлагаться пользователям NimbX.

## Формат файла

```json
{
  "version": "1.18",
  "url": "https://www.rustore.ru/catalog/app/ru.nimbx.voice",
  "notes": ""
}
```

- `version` — обязателен, сравнение посегментное числовое (`1.10` > `1.9`).
- `url` — необязателен, по умолчанию страница каталога RuStore.
- `notes` — необязателен, не используется в текущей версии приложения.
