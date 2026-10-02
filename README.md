# VNO atvykimai — PWA прилётов в аэропорт Вильнюса

Файлы:
- `index.html` — само приложение (литовский язык, тёмная/светлая тема)
- `manifest.webmanifest`, `sw.js`, иконки — чтобы ставилось на телефон как приложение
- `worker.js` — сервер-посредник для реальных данных (Cloudflare Worker)

## Цвета
- Зелёный — сядет в течение 10 минут или уже летит ближе 50 км от VNO
- Жёлтый — задержка 15+ минут
- Красный — уже приземлился (показываются последние 3 часа)
- Серый — по расписанию

## 1. Реальные данные (Cloudflare Worker, бесплатно)
Браузер не может напрямую читать Flightradar24 (блокировка CORS), поэтому нужен посредник.
1. dash.cloudflare.com → Workers & Pages → Create → Create Worker → Deploy.
2. Edit code → удалить всё → вставить содержимое `worker.js` → Deploy.
3. Скопировать адрес вида `https://vno-xxx.workers.dev`.
   Проверка: откройте `https://vno-xxx.workers.dev/arrivals` — должен быть JSON со списком рейсов.

## 2. Хостинг на GitHub Pages
1. Загрузить в репозиторий все файлы, кроме `worker.js` и `README.md`.
2. Settings → Pages → Deploy from branch → main / root.
3. Можно сразу вписать адрес воркера в `index.html` в строку `const DEFAULT_API = ""`,
   либо ввести его в приложении: шестерёнка → Duomenų serverio adresas → Išsaugoti.

## 3. Установка на телефон
- iPhone (Safari): Поделиться → «На экран Домой».
- Android (Chrome): меню ⋮ → «Установить приложение».

Без адреса воркера приложение показывает демо-рейсы с пометкой «Pavyzdiniai duomenys».
