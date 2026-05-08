---
description: "Use when editing static HTML/CSS/JS pages, VSYC-26 pages, assets, navigation, or branding in dmvthrowers.github.io or DMV Throwers Design System. Enforces voice, brand tokens, static-site guardrails, nav consistency, and update workflow checklists."
name: "DMV Throwers Static Site Maintainer"
applyTo:
  - "dmvthrowers.github.io/**/*.{html,css,js,xml,txt}"
  - "DMV Throwers Design System/**/*.{html,css,js,md}"
---
# DMV Throwers Static Site Maintainer Rules

## Mission Context
- Organization: DMV Throwers (free yo-yo and skill toy club, DC/MD/VA, est. 2021).
- Coordinator: Brandon Rogers (`contact@dmvthrowers.club`).
- Meetup: Every 3rd Sunday, 1–4 PM at Arlington Central Library, 1015 N Quincy St, Arlington, VA 22201.
- VSYC-26: Sept 19, 2026 at Dulles Town Center, Sterling, VA. Free to spectate.

## Repository
`dmvthrowers.github.io` is a static GitHub Pages site served at `dmvthrowers.club`.
`DMV Throwers Design System` is the brand source of truth — pull logos and tokens from there; never push back.

## Hard Guardrails
- Never edit `CNAME` — it must stay `dmvthrowers.club`.
- Never add paywalls, tracking scripts, external fonts, or third-party embeds.
- Never introduce `border-radius`, `box-shadow`, or animations beyond `0.2s ease`.
- Never delete historical flyers or gallery photos.
- Use relative links only (no absolute URLs for internal navigation).
- Keep navigation markup **identical** across all 15 static site pages.
- For VSYC edits, touch only `vsyc26-*.html` files unless explicitly directed otherwise.
- VSYC-26 date, venue, and pricing are immutable — do not change them.

## Brand System
### Colors
| Token        | Hex       | Usage                        |
|--------------|-----------|------------------------------|
| `--red`      | `#B80000` | Primary accent, buttons, borders |
| `--navy`     | `#102040` | Headings, nav background     |
| `--cream`    | `#fffdfa` | Page background              |
| `--gold`     | `#C9A84C` | VSYC pages only              |
| `--teal`     | `#13C3A3` | Donate CTA only              |

### Typography
- Display: **Playfair Display** (never in red)
- Body: **DM Sans**
- VSYC-only accent: **Montserrat**

### Visual Rules
- `border-radius: 0` everywhere.
- No shadows on any element.
- Cards: white fill, 1px border, top `3px` red accent **or** left `4px` navy accent.
- Buttons: uppercase, `letter-spacing: 0.095em`, min height `44px`.
- Nav: `64px` sticky, active link gets `2px` red underline.
- `max-width: 1100px` for all content containers.
- Section padding: `80px` vertical, `24px` horizontal.

## Voice And Copy Rules
- Nav labels: ALL CAPS.
- Headings: Title Case.
- Body copy: sentence case.
- Voice: second person, short sentences.
- Preferred tagline: "All ages, all levels, always free."
- Emoji policy: `☕` only in donate context — nowhere else.

## Content Workflows

### Monthly Meetup Update
1. Calculate the 3rd Sunday of the target month.
2. Add flyer: `assets/images/events/DMV Throwers [Month YYYY].png` (< 500 KB, meaningful alt text).
3. Update the NEXT MEET banner in `index.html`.
4. Add/update the entry in `events.html` upcoming list.
5. Update `sitemap.xml` — set `<lastmod>` on affected page URLs to today's date.

### VSYC-26 Update
1. Edit only `vsyc26-*.html` files.
2. Preserve immutable date/venue/pricing.
3. Add sponsor logos sourced from `DMVT-Design/assets/logos/`.
4. Update any PDF in `assets/documents/` with a version suffix.
5. Update `sitemap.xml` `<lastmod>` for changed pages.

### Asset Sync
- Logos: pull from `DMVT-Design/assets/logos/`, copy into `assets/images/`.
- Optimize all new images to under 500 KB.
- Every `<img>` tag must have descriptive `alt` text.

## Required Execution Pattern
1. List the exact files you will touch — confirm scope before editing.
2. Make the smallest possible diff.
3. Run the validation checklist.
4. Output a diff summary grouped by file.

## Validation Checklist
- [ ] No horizontal scroll at 360px viewport width.
- [ ] All changed `href`/`src` links resolve correctly (no 404s).
- [ ] `sitemap.xml` `<lastmod>` updated for every changed page URL.
- [ ] Nav markup is identical across all affected static pages.
- [ ] Colors match `#B80000` / `#102040` / `#fffdfa` — no off-brand hex.
- [ ] `border-radius: 0` confirmed (search for `border-radius` diff).
- [ ] `CNAME` file is untouched.
- [ ] All new images have `alt` text and are < 500 KB.

## Commit Conventions
| Scope              | Prefix            |
|--------------------|-------------------|
| New event content  | `feat(events):`   |
| VSYC-26 fix        | `fix(vsyc26):`    |
| Asset/logo sync    | `chore(assets):`  |
| Docs/README        | `docs:`           |
| Nav/style fix      | `fix(style):`     |
