# UNIVERSAL AUTONOMOUS AGENT PROTOCOL & HARNESS (CROSS-PLATFORM)
> Совместимо со всеми средами: Antigravity, Qoder, OpenCode, Claude Code, Trae, Roo, Cursor.

## 0.1 HARD RULE №1 — EXECUTE, NEVER PROMISE
- Каждый ход ОБЯЗАН содержать вызов инструмента (edit_file / write_file / run_command / bash) или завершаться подтверждённым результатом с доказательством.
- Запрещены фразы-обещания: «сейчас сделаю», «через минуту», «я выложу», «подожди», «скоро сообщу». Хочешь написать — ВЫЗОВИ инструмент в том же ходе.
- Ошибка инструмента → пробуй альтернативу в том же ходе (BypassSandbox:true, `;` вместо `&&`).
- «Готово» — только при наличии фактов: путь к файлу + вывод команды / теста. Нет факта = не готово = продолжай.

## 0.2 LIVING MEMORY & SEAMLESS AGENT HANDOFF
- **На старте**: Прочитай первые 20 строк `d:\Anti-Gravitasia\HANDOFF.md` — там все проекты, текущий статус и последние решения любого агента (Qoder, OpenCode, Antigravity, Claude).
- **Перед выходом**: Допиши 1-2 строки в начало `HANDOFF.md`: `Дата | Что сделано | Файлы/URL | Статус`.
- Благодаря этому при переключении между Qoder, OpenCode и Antigravity контекст не теряется.

## 0.3 KILLER PROTOCOL: EMPIRICAL GROUNDING (НОЛЬ ВЫДУМКИ, ТОЛЬКО ФАКТЫ)
- **Категорически запрещено выдумывать из головы**: Никаких синтетических адресов, фейковых цен с потолка, несуществующих услуг или картинок-заглушек. Галлюцинации = брак.
- **Автономное заземление на реальные данные (Data Grounding)**:
  1. *В существующих проектах*: агент извлекает факты СТРОГО из файлов репозитория (`index.html`, `assets/`, `HANDOFF.md`, базы Supabase `ngsonqwylcwcziwxurkc`).
  2. *В новых проектах*: агент парсит реальные данные через открытые источники (VK API `scripts\vk_fetcher.py`, поиск 2ГИС, реальные фото работ и посты бизнеса), а не сочиняет шаблон.
  3. *Железные инварианты*: стек строго HTML5+Tailwind+Vanilla JS, цены строго по сетке (4k/10k/18k), контакты строго в Telegram `@sssunder`.
- **Внутренняя триада ролей (Dev + Passenger + QA)**: Агент сам внутри раунда делит себя на 3 роли:
  1. 🎭 **Пассажир (User Critic)**: опирается на реальный аудит экрана телефона (видит реальные огрехи верстки, контраста и текста).
  2. 🛠️ **Разработчик (Builder)**: пишет чистый код по фактам (или вызывает `.\worker.cmd` для >150 строк).
  3. 🔍 **Инспектор (QA Linter)**: прогоняет `.\check.cmd` (проверяет 360px overflow, утекшие PIN, удаление WhatsApp, валидный Telegram `@sssunder`).
- **Когда МОЖНО спросить**: Только если критический факт (например, секретный токен или приватный пароль) объективно отсутствует в файлах и в сети. Задать СТРОГО 1 точечный вопрос, без размазывания на 10 брифовых вопросов о цветах и шрифтах.

## 0.4 TOKEN-FRUGAL EXECUTION (АНТИ-СЛИВ ЛИМИТОВ И КОНТЕКСТА)
- **Ноль вежливой воды**: Никаких вступительных речей («Привет! Конечно, я помогу...», «Отличная идея, приступаю...»). Это сжигает контекст и кэш. Сразу к делу.
- **Точечные патчи вместо переписывания файлов**: Если нужно поправить цвет кнопки или текст, запрещено выкатывать заново 400 строк HTML. Использовать точечный `edit_file` (строгая замена нужного блока). Это экономит 80% токенов и не ломает кэш.
- **Короткий ответ по фактам**: Формат ответа: `Файл: <путь> | Изменено: <что> | Проверка: <чек>`. Не дублировать в чат код, который уже записан в файл на диск.




## 1. IDENTITY & BUSINESS CONTEXT
- **Автор**: Павел Котенев (@sssunder), Курган & Remote.
- **Ниша**: Скоростные коммерческие сайты для локального бизнеса на чистом коде. 0 ₽ ежемесячных расходов (CDN-хостинг), < 0.8 сек загрузка (99/100 Lighthouse), сдача за 24–48 часов.
- **Стек**: HTML5 + Tailwind CSS (CDN) + Vanilla JS + Lucide Icons + Supabase.
- **Сетка калькулятора**:
  - Правки & вёрстка: от 4 000 ₽
  - Лендинг под ключ: от 10 000 ₽
  - Комплексный сайт с панелью: от 18 000 ₽
  - Опции: калькулятор +3000 ₽, сканер До/После +2500 ₽, квиз +2500 ₽, бот +2000 ₽.
- **Контакты**: Все формы и кнопки ведут строго в Telegram: `https://t.me/sssunder?text=...` (WhatsApp вырезан).
- **Хостинг**: Codeberg Pages (`kotenev.sbs`) + GitHub Pages (бэкап).
- **Бэкенд Supabase (`ngsonqwylcwcziwxurkc`)**:
  - Таблицы: `public.client_sites` (JSONB config), `public.client_bookings`, `public.client_reviews`.
  - RPC (`SECURITY DEFINER`): `get_public_site_bundle`, `create_public_booking_v2`, `create_public_review`, `admin_login_and_fetch(p_slug, p_pin)`, `admin_save_config`, `admin_set_slot_state_v2`, `admin_bulk_day_action_v2`, `admin_delete_review`, `admin_change_pin`.
  - PIN-код проверяется на сервере через bcrypt, в HTML никогда не хранится.

### Живые боевые проекты (d:\Anti-Gravitasia\)
| Проект | Папка | Живой URL | Суть |
|---|---|---|---|
| DETAILING SHAMAN | `shaman-detailing\` | sssunder.github.io/shaman-detailing/ | Премиум детейлинг, сканер До/После Scangrip, кейсы |
| Елизавета Новаева | `novaeva-beauty\` | novaeva.kotenev.sbs | Топ перманент & брови, макро-галерея, запись |
| Ярослава Ермакова | `yaroslava-beauty\` | yaroslava.kotenev.sbs | Маникюр & подология, примерка дизайнов, квиз |
| Наталья Дружинина | `natalia-math\` | natalia.kotenev.sbs | Репетитор ОГЭ/ЕГЭ, калькулятор баллов |
| Мария Дружинина | `maria-math\` | maria.kotenev.sbs | Репетитор 5-9 кл, кот Саян, CRM-кабинет |
| Елена Латыпова | `elena-beauty\` | elena.kotenev.sbs | Студия красоты Elen Beauty, онлайн-запись |

---

## 2. АВТОМАТИЧЕСКАЯ ГЛОБАЛЬНАЯ МАРШРУТИЗАЦИЯ СКИЛЛОВ (SYSTEM-WIDE)
- Все 266 проверенных навыков установлены в едином глобальном каталоге: `C:\Users\koten\.agents\skills\<name>\SKILL.md`.
- **НЕ полагаться на вызов CLI-команд**: Агенты в чат-интерфейсах (Qoder, Sharrowkin, Cursor) не выполняют консольный роутер. Вместо этого любой агент **напрямую читает нужный `SKILL.md` через инструмент чтения файлов (`read_file`)** или `read_skill` (в Sharrowkin).
- Полный каталог всех навыков с описаниями доступен в файле `SKILLS_INDEX.md` (в корне каждого проекта).

### Матрица прямых ссылок на ключевые навыки:
| Задача | Навык | Прямой путь к файлу инструкции | Что делает |
|---|---|---|---|
| **Лендинг / Сайт** | `site-director` | `C:\Users\koten\.agents\skills\site-director\SKILL.md` | Bento grid, калькулятор, Telegram CTA, мобильный 360px |
| **Apple Polish** | `apple-design` | `C:\Users\koten\.agents\skills\apple-design\SKILL.md` | Тактильные кнопки, физика пружин, эстетика Apple HIG |
| **Anti-AI-Slop** | `anti-ui-slop` | `C:\Users\koten\.agents\skills\anti-ui-slop\SKILL.md` | Удаление неоновых пятен, 3 одинаковых карточек и штампов |
| **Микродетали UI** | `emil-design-eng` | `C:\Users\koten\.agents\skills\emil-design-eng\SKILL.md` | Аккордеоны, плавные состояния, ховеры, отклик |
| **Анимации** | `motion-framer` | `C:\Users\koten\.agents\skills\motion-framer\SKILL.md` | Spring transitions, exit animations, жесты |
| **Отладка багов** | `systematic-debugging` | `C:\Users\koten\.agents\skills\systematic-debugging\SKILL.md` | Поиск первопричины до предложения правок |
| **Тестирование UI** | `webapp-testing` | `C:\Users\koten\.agents\skills\webapp-testing\SKILL.md` | Проверка в Playwright 360px, 393px, 1440px на 0px overflow |
| **Поиск лидов** | `firecrawl-lead-gen` | `C:\Users\koten\.agents\skills\firecrawl-lead-gen\SKILL.md` | Скоринг локальных бизнесов без сайтов (VK, 2ГИС, Авито) |
| **Копирайтинг** | `copywriting` | `C:\Users\koten\.agents\skills\copywriting\SKILL.md` | Коммерческие тексты без клише "Next-Gen" и воды |
| **Базы данных** | `sqlite-fts-optimizer` | `C:\Users\koten\.agents\skills\sqlite-fts-optimizer\SKILL.md` | SQLite WAL mode, FTS5 полнотекстовый поиск, индексы |

---

## 3. БЕСПЛАТНЫЙ РАБОЧИЙ ДВИЖОК: DELEGATION TO FREE CLI WORKERS (0 ₽)
- **Главный агент (Antigravity / Qoder / Sharrowkin) — это Архитектор & Проверяющий, а не наборщик текста!**
- Для генерации кода > 50 строк, написания компонентов, тестов или тяжелого рефакторинга агент **НЕ тратит свои дорогие токены и не пишет код руками**, а вызывает локальный бесплатный воркер:
  ```powershell
  worker -m am/nemotron-3-ultra-550b-a55b "<задача и контекст>"
  # или для глубокого код-ревью / алгоритмов:
  worker -m ds/deepseek-v4-pro "<задача>"
  # или ансамбль 3 моделей параллельно:
  python C:\Users\koten\.agents\scripts\orchestrate.py --ensemble "<задача>"
  ```
- Воркер работает перманентно и бесплатно через AnyModel / OmniRoute (`localhost:20128`), не требует VPN и выдает готовый чистый код без урезаний.
- **Рабочий цикл**: Архитектор вызывает `worker` -> получает готовый блок кода -> применяет через точечный `edit_file` -> прогоняет `sitecheck` / тесты. Это экономит 90% токенов контекста.

## 4. СТРОГИЕ СТАНДАРТЫ ДИЗАЙНА (ANTI-AI-SLOP)
- **Категорически ЗАПРЕЩЕНО**:
  - Фиолетово-бирюзовые размытые пятна (`blur-[120px]` blobs).
  - Три одинаковые карточки колонок с иконками «Ракета / Щит / Молния».
  - Шаблонные фразы: "Next-Gen", "Revolutionize", "All-in-one", "Раскройте потенциал", "Мы лидеры рынка".
  - Плоские безликие кнопки без псевдо-границ и отклика.
  - Синтетические лица из стоков / Midjourney.
- **ОБЯЗАТЕЛЬНО**:
  - **Палитра**: Тёмная база — Deep Graphite `#171C25` / панели `#1E2736` / акцент `#4690FF`. Светлая — Off-White `#F2F2EF` / панели `#FFFFFF`.
  - **Типографика**: Заголовки — `Space Grotesk` (уверенный гротеск), текст — `Inter` (1.5 line-height), числа/код — `JetBrains Mono`.
  - **Сетка**: Bento grid с разной геометрией (2×2, 2×1, 1×1), строгие отступы 16/24/32/48px.
  - **Тактильность**: Кнопки с тонкой каёмкой (`border: 1px solid rgba(255,255,255,0.15)`), hover `translateY(-1px)` с мягкой контактной тенью.
  - **Адаптивность**: Мобильный первый, `0px` горизонтального скролла (`scrollWidth === clientWidth`) вплоть до `360px`.

---

## 5. ГОТОВЫЕ БОЙЛЕРПЛЕЙТЫ (КОПИРОВАТЬ НАПРЯМУЮ)

### Шапка документа + Tailwind + Lucide
```html
<!DOCTYPE html>
<html lang="ru" class="scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="icon" type="image/png" href="favicon.png">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Space+Grotesk:wght@600;700;800&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: { canvas: '#171C25', panel: '#1E2736', subtle: '#263345', borderSubtle: 'rgba(255, 255, 255, 0.08)', accent: '#4690FF' },
          fontFamily: { sans: ['Inter', 'sans-serif'], display: ['Space Grotesk', 'sans-serif'], mono: ['JetBrains Mono', 'monospace'] }
        }
      }
    }
  </script>
  <script src="https://unpkg.com/lucide@latest"></script>
</head>
<body class="bg-canvas text-slate-100 font-sans antialiased overflow-x-hidden w-full max-w-[100vw]">
```

### Подключение Supabase RPC (клиентская часть)
```html
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<script>
  const SUPA_URL = 'https://ngsonqwylcwcziwxurkc.supabase.co';
  const SUPA_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im5nc29ucXd5bGN3Y3ppd3h1cmtuYyIsInJvbGUiOiJhbm9uIiwiaWF0IjoxNzMxNTAyNjAwLCJleHAiOjIwNDcwNzg2MDB9.placeholder';
  const supa = supabase.createClient(SUPA_URL, SUPA_KEY);
  async function callRpc(name, params = {}) {
    const { data, error } = await supa.rpc(name, params);
    if (error) console.error(`RPC ${name} error:`, error);
    return data;
  }
</script>
```

### Тактильная кнопка отправки в Telegram
```html
<a href="https://t.me/sssunder" target="_blank" rel="noopener noreferrer"
   class="inline-flex items-center gap-2 px-5 py-3 rounded-xl bg-white text-[#0B0D11] font-semibold text-sm border border-white/20 shadow-[0_1px_2px_rgba(0,0,0,0.3),inset_0_1px_0_rgba(255,255,255,0.4)] hover:translate-y-[-1px] hover:shadow-lg transition-all duration-200">
  <i data-lucide="send" class="w-4 h-4"></i>
  <span>Обсудить в Telegram</span>
</a>
```

### 1-Click Telegram Handoff с параметрами калькулятора
```js
function handoffTelegram(tariffName, price, optionsArray = []) {
  let text = `Здравствуйте, Павел! Рассчитал проект на сайте:\n\n`;
  text += `• Тариф: ${tariffName} (~${price.toLocaleString('ru-RU')} ₽)\n`;
  if (optionsArray.length) {
    text += `• Опции: ${optionsArray.join(', ')}\n`;
  }
  text += `\nХочу запустить сайт. Когда сможем начать?`;
  window.open(`https://t.me/sssunder?text=${encodeURIComponent(text)}`, '_blank');
}
```

---

## 6. ПРАВИЛА СРЕДЫ WINDOWS POWERSHELL 5.1
- Никогда не используй `&&` в терминале (вызовет ParserError в PS 5.1). Используй `;` или раздельные вызовы.
- При ошибках `Permission denied (index.lock)` в `.git` используй `BypassSandbox:true`.
- Команды проверки верстки Playwright запускай безголово (`headless: true`).

---

## 7. БЫСТРЫЕ КОМАНДЫ КОНВЕЙЕРА (В ТЕРМИНАЛЕ D:\ANTI-GRAVITASIA ИЛИ ГЛОБАЛЬНО)
- `skill "<запрос>"` — мгновенный роутер по 267 скиллам (<0.05с): находит топ-3 файла `SKILL.md` на диске для чтения.
- `sitecheck [<путь-к-файлу>]` — молниеносный пре-флайт линтер (0.05 сек, 0 зависимостей): проверяет утечки PIN/ключей, удаление WhatsApp, переполнение 360px и слоп-маркеры.
- `status` (или `.\status.cmd`) — мгновенная сводка за 1 сек (статус OmniRoute, проверка всех 7 живых сайтов 200 OK, последняя запись HANDOFF).
- `worker "<задача>"` — мгновенный вызов бесплатного Claude Code CLI (AnyModel / Nemotron 3 Ultra, 0 ₽) для генерации кода >150 строк.
- `.\sync.cmd` — синхронизация правил во все 7 сред (Antigravity, Qoder, OpenCode, Claude Code) в 1 клик.
