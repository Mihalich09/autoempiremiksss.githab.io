# AUTO EMPIRE

Браузерная игра про перепродажу автомобилей с живым общим чатом (Firebase).
Весь проект — один файл `index.html`, сборка не нужна.

## Файлы

| Файл | Зачем |
|---|---|
| `index.html` | Сама игра и чат |
| `404.html` | Страница «не найдено» для GitHub Pages |
| `.nojekyll` | Говорит GitHub Pages не обрабатывать сайт через Jekyll |
| `firestore.rules` | Правила безопасности для базы чата (копируются в консоль Firebase) |

## Публикация на GitHub Pages

1. Создай репозиторий на GitHub (например, `auto-empire`), можно публичный.
2. Загрузи в него все файлы из этой папки, включая скрытый `.nojekyll`.
   Через сайт: **Add file → Upload files**. Через терминал:
   ```bash
   git init
   git add .
   git commit -m "AUTO EMPIRE"
   git branch -M main
   git remote add origin https://github.com/ИМЯ/auto-empire.git
   git push -u origin main
   ```
3. В репозитории: **Settings → Pages → Build and deployment**:
   - Source: **Deploy from a branch**
   - Branch: **main**, папка **/ (root)** → **Save**
4. Через 1–2 минуты игра откроется по адресу
   `https://ИМЯ.github.io/auto-empire/`

Если репозиторий назван `ИМЯ.github.io`, игра будет прямо на `https://ИМЯ.github.io/`.
Для репозитория с обычным названием впиши его имя в переменную `REPO` в `404.html`.

## Настройка Firebase (обязательно, иначе чат не заработает)

1. **Authentication → Sign-in method** → включи **Anonymous**.
2. **Authentication → Settings → Authorized domains** → **Add domain** →
   добавь `ИМЯ.github.io` (только домен, без `https://` и без пути).
   Без этого вход выдаст ошибку `auth/unauthorized-domain`.
3. **Firestore Database** → **Rules** → вставь содержимое `firestore.rules` → **Publish**.
4. Если базы ещё нет: **Firestore Database → Create database**.

Ключ `apiKey` в `index.html` публичный по замыслу Firebase. Данные защищают правила из п. 3,
а не секретность ключа.

## Локальный запуск

Открывать `index.html` двойным кликом нельзя: Firebase Auth не работает с `file://`.
Запусти маленький сервер в папке проекта:

```bash
python3 -m http.server 8000
```

и открой `http://localhost:8000`. Домен `localhost` Firebase разрешает по умолчанию.

## Если что-то не работает

- **Чат пишет «Подключаемся…»**: проверь пункты 1–3 выше и консоль браузера (F12).
- **`auth/unauthorized-domain`**: домен GitHub Pages не добавлен в Authorized domains.
- **`Missing or insufficient permissions`**: правила Firestore не опубликованы.
- **Страница не обновилась после пуша**: подожди пару минут и обнови с Ctrl+F5.
