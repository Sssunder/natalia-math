# Changelog — Natalia Math (`natalia-math`)

## 2026-11-12 — Constructor v3 (Tab 2 Builder, Auto-Sync, Tab 3 Reviews + Live Preview)
- **URL / Branch**: `https://sssunder.github.io/natalia-math/` (`origin/master`, Supabase `ngsonqwylcwcziwxurkc`, `SITE_SLUG='natalia-math'`)
- **What Changed (`index.html`)**:
  - Tab 2 (`#teacherTabTexts`): added `#cfgDefaultTheme` (`academic`/`minimal`/`light`/`emerald`) applied on load unless `natalia_theme_manual` is set; prevented `setThemeVariant()` from overwriting cloud `hero_subtitle`/`hero_motto`/`announcement` when `hasCloudConfig` is true; hardened `.photo-overlay-light` + light-theme badge/status contrast.
  - Phone & Messenger Auto-Sync: normalized `+7/8/9...`, TG (`@user`/`user`/phone/`t.me/...`), MAX, and channels; auto-synced `#cfgPhoneDisplay` -> `#cfgMaxUrl`/`#cfgTgUrl` (preserving custom TG handles) + `#syncMessengersFromPhoneBtn`; synced all site-wide `header`/`hero`/`booking`/`revSend`/`footer` links.
  - Review Channels & Programs: added `#cfgReviewsChannelUrl` -> `#reviewsChannelLink` + `#footerReviewsChannelLink`; upgraded `#cfgProgramsList` with inline icon/title/price/desc edits, `p.hidden` toggle (`>=1` active guard), and `#addProgramFormatBtn`.
  - Tab 3 (`#teacherTabReviews`): added 3-step TG/MAX/Avito owner tips; manual `#adminAddReviewForm` + `#admReviewLivePreview` sharing `buildPublicReviewCardHtml()` via `admin_add_review`; visible/hidden list badges + `admin_set_review_visibility` + `admin_delete_review`.
- **Verified**: JS `new Function` syntax OK (no hardcoded PIN); Playwright local E2E passed (4 themes × 3 viewports `1440x900`/`393x852`/`360x800`, 0 errors, 0px overflow, overlay contrast >0.45 lum / body contrast >=4.5; phone->MAX/TG auto-sync; `admin_save_config`; Tab 3 preview + add/show/hide/delete); DB restored to original config (`active_reviews=0`).
- **Remaining**: Push `master` to GitHub Pages, verify live `https://sssunder.github.io/natalia-math/` HTTP 200 & live Playwright audit; optional future move to neutral org/RU hosting.

## Earlier History (Compact)
- `acc126a` (2026-11-11): Connected Supabase cloud sync for slots whitelist, live copy editor, and reviews.
- `44dee8d` (2026-11-11): Focused offering on 9th-grade OGE mini-groups, interactive reviews, local dates, mobile wrap.
- `c38ca5e` (2026-11-11): Added frosted header theme popover, header clearance, real phone/TG/MAX links.
