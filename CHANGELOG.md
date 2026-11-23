# Changelog — Natalia Math (`natalia-math`)

## 2026-11-24 — Clean Telegram Alerts & Bot Username Input Removal
- **Очистка карточки Telegram**:
  - Полностью удалён сырой блок ввода «Username бота / https:t.me» с кнопкой «Сохранить», сбивавший преподавателя.
  - Убраны громоздкие технические списки шагов и VPN-ссылки.
  - Бот намертво преднастроен на платформенного `@GojoNotifyBot` с санитаризацией (любые испорченные значения с `:` или `/` сбрасываются на `GojoNotifyBot`).
  - Аккуратная карточка с 1 кнопкой «Подключить бота» и статусом перенесена в раздел «Контакты и мессенджеры».
  - В онбординг-туре удалены лишние технические шаги про бота и VPN.
- **Проверки**:
  - `sitecheck`: 100% Clean.
  - `node --check`: 100% Valid JavaScript.
  - Playwright: 0px overflow на 360px и 1440px, 0 ошибок.

## 2026-11-24 — Bright Photo Mode, Patronymic Support & MAX Messenger Connect Guide
- **Фото без затемнения**:
  - Убран принудительный затемняющий CSS-фильтр `brightness-95 contrast-105` с портрета.
  - Полноразмерный градиент-затемнение `absolute inset-0 from-black/95 via-black/40` заменён на компактную плашку снизу `bottom-0 inset-x-0 h-24 from-black/75 via-black/30` — верхние 75% фото (лицо, улыбка, класс) теперь полностью открыты и светлые в естественном дневном свете.
  - В личном кабинете (Вкладка 2) и в окне «Примерка фото» добавлен переключатель режима затемнения: «✨ Без затемнения (Светлое фото)» vs «🌑 С затемнением».
  - Смягчён градиент hero-баннера (`black/80 via-black/55 to-black/20`).
- **Отчество преподавателя**:
  - На сайте везде добавлено отчество: **Наталья Игоревна Дружинина** (шапка, портрет, подвал, title страницы).
  - В конструкторе личного кабинета (Вкладка 2 «Тексты, цены и ссылки») добавлен отдельный блок «ФИО преподавателя (с отчеством)» (`#cfgTeacherName`) и «Статус/квалификация» (`#cfgTeacherSub`). При смене имени в кабинете оно обновляется по всему сайту и в облаке Supabase.
  - Исправлен сброс отчества при примерке пресетов фото (`selectPresetPhoto` сохраняет ФИО с отчеством).
- **Подключение мессенджера МАКС**:
  - Под полем «Ссылка МАКС» в личном кабинете добавлена пошаговая подсказка: как за 10 секунд скопировать персональную ссылку в приложении MAX (Профиль → значок QR-кода / Поделиться → Скопировать ссылку) и вставить в кабинет.
- **Проверки**:
  - `sitecheck`: 100% Clean.
  - `node --check`: 4 inline-скрипта без синтаксических ошибок.
  - Playwright: 0px overflow на 360px и 1440px, 0 ошибок консоли.

## 2026-11-12 — Obvious «Пройти обучение заново» button + post-skip hint, local only, NOT pushed
- Faint «Экскурсия» pill → prominent white «Пройти обучение заново» in cabinet tab bar; on skip (Пропустить/Esc) a ~6s bottom toast + button pulse point back to it (toast `pointer-events:none`).
- Verified `maria-loop/verify_tour.py` (8 steps) + live skip-hint check: PASS, 0 overflow 1440/360, 0 errors, zero DB writes. Additive UI only.

## 2026-11-12 — Plain-language connect guide + VPN links in Telegram card, local only, NOT pushed
- Telegram card now self-explains for non-technical owners: persistent «Как подключить (2 минуты)» list (VPN → «Подключить уведомления» → «Запустить» /start → «Я подписался — обновить статус») + Pavel's VPN referral links (`quattro.app/register?ref=HEmqibBsi5vz1Qz2` / `QuattroVPN_BOT?start=r_HEmqibBsi5vz1Qz2`); slim VPN line when connected.
- Tour Telegram section now 3 steps (8 total) switching to Texts before spotlighting the card.
- Verified `maria-loop/verify_platform.py` + `verify_tour.py` (mocked RPC, zero DB writes): PASS, 0 overflow 1440/360, 0 errors. Additive; booking logic untouched.

## 2026-11-12 — Joined universal Telegram booking-notification platform, local only, NOT pushed
- Connect-card + auto-notify ported from maria-math: `TG_NOTIFY_URL`, `notifyNewBooking()` after `create_public_booking` success, Telegram card in cabinet Texts tab (navy/gold theme), `saveTelegramBotUsername`/`setTelegramEnabled`/`refreshTelegramStatus` via `persistConfigToCloud`. `DEFAULT_SITE_CONFIG.telegram.bot_username='GojoNotifyBot'` (shared platform bot → one-click connect), deep-merge in `mergeSiteConfig`.
- Tour gained a Telegram step (6 steps) that switches to Texts before spotlighting the card.
- Verified `maria-loop/verify_platform.py` + `verify_tour.py` (mocked RPC, zero DB writes): PASS, 0 overflow 1440/360, 0 errors. Additive; booking logic untouched.

## 2026-11-12 — Cabinet mini-tour (onboarding «Экскурсия»), local only, NOT pushed
- Same self-contained tour as maria-math appended before `</body>`: first cabinet login → spotlight + card walks «Расписание», «Тексты», «Отзывы» step-by-step; «Экскурсия» pill replays; shown once via localStorage. Auto-detects cabinet tabs; theme-safe, mobile-clamped.
- Verified via `maria-loop/verify_tour.py` (mocked RPC, zero DB writes): 5 steps, auto-start, spotlight, card in viewport, flag, relaunch, 0 overflow 1440/360, 0 errors — PASS. Additive UI only; booking/data logic untouched.

## 2026-11-12 — Constructor v3 (Tab 2 Builder, Auto-Sync, Tab 3 Reviews + Live Preview)
- **URL / Branch**: `https://sssunder.github.io/natalia-math/` (`origin/master`, Supabase `ngsonqwylcwcziwxurkc`, `SITE_SLUG='natalia-math'`)
- **What Changed (`index.html`)**:
  - Tab 2 (`#teacherTabTexts`): added `#cfgDefaultTheme` (`academic`/`minimal`/`light`/`emerald`) applied on load unless `natalia_theme_manual` is set; prevented `setThemeVariant()` from overwriting cloud `hero_subtitle`/`hero_motto`/`announcement` when `hasCloudConfig` is true; hardened `.photo-overlay-light` + light-theme badge/status contrast.
  - Phone & Messenger Auto-Sync: normalized `+7/8/9...`, TG (`@user`/`user`/phone/`t.me/...`), MAX, and channels; auto-synced `#cfgPhoneDisplay` -> `#cfgMaxUrl`/`#cfgTgUrl` (preserving custom TG handles) + `#syncMessengersFromPhoneBtn`; synced all site-wide `header`/`hero`/`booking`/`revSend`/`footer` links.
  - Review Channels & Programs: added `#cfgReviewsChannelUrl` -> `#reviewsChannelLink` + `#footerReviewsChannelLink`; upgraded `#cfgProgramsList` with inline icon/title/price/desc edits, `p.hidden` toggle (`>=1` active guard), and `#addProgramFormatBtn`.
  - Tab 3 (`#teacherTabReviews`): added 3-step TG/MAX/Avito owner tips; manual `#adminAddReviewForm` + `#admReviewLivePreview` sharing `buildPublicReviewCardHtml()` via `admin_add_review`; visible/hidden list badges + `admin_set_review_visibility` + `admin_delete_review`.
- **Verified**: JS `new Function` syntax OK (no hardcoded PIN); Playwright local E2E passed (4 themes × 3 viewports `1440x900`/`393x852`/`360x800`, 0 errors, 0px overflow, overlay contrast >0.45 lum / body contrast >=4.5; phone->MAX/TG auto-sync; `admin_save_config`; Tab 3 preview + add/show/hide/delete); DB restored to original config (`active_reviews=0`).
- **Status**: Commit `a0d0ad0` pushed to `origin/master`; live site verified 2026-11-12 via `tutor-platform-template/check_live_sites.py` (HTTP 200, Constructor v3 markers present, 0 console/network errors, 0px overflow at 1440x900 & 360x800). Optional future move to neutral org/RU hosting stays in backlog.

## Earlier History (Compact)
- `acc126a` (2026-11-11): Connected Supabase cloud sync for slots whitelist, live copy editor, and reviews.
- `44dee8d` (2026-11-11): Focused offering on 9th-grade OGE mini-groups, interactive reviews, local dates, mobile wrap.
- `c38ca5e` (2026-11-11): Added frosted header theme popover, header clearance, real phone/TG/MAX links.
