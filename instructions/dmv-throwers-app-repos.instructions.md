---
description: "Use when editing yoyo-player-map (Next.js) or dmvt-event-hub (React/Vite). Enforces DMV Throwers brand tokens, privacy constraints, app-specific guardrails, and last-modified documentation policy."
name: "DMV Throwers App Repos Maintainer"
applyTo:
  - "yoyo-player-map/**/*.{ts,tsx,js,jsx,css,json,md}"
  - "DMVEvents/**/*.{ts,tsx,js,jsx,css,json,md}"
---
# DMV Throwers App Repos Maintainer Rules

## Mission Context
- Organization: DMV Throwers (free yo-yo club, DC/MD/VA, est. 2021).
- Coordinator: Brandon Rogers (`contact@dmvthrowers.club`).
- VSYC-26: Sept 19, 2026, Dulles Town Center, Sterling VA. Free to spectate.

## Repositories
| Repo               | Stack                          | Live URL                                          | Status        |
|--------------------|--------------------------------|---------------------------------------------------|---------------|
| `yoyo-player-map`  | Next.js 14, Tailwind, Supabase | https://yoyo-player-map.vercel.app/en             | Live          |
| `dmvt-event-hub`   | React 18, Vite, Tailwind, shadcn/ui, Supabase | Target: `events.dmvthrowers.club` | Pre-launch    |

## Hard Guardrails
- Do not deploy `dmvt-event-hub` to production — pre-launch only.
- Never store or display user location below city level.
- Do not add tracking scripts, third-party analytics, or external fonts not already in the bundle.
- Do not add paywalls or monetization of any kind — the club is free.
- Preserve existing Supabase migration files; never alter applied migrations.
- yoyo-player-map red color must be `#B80000`, never `#D42B2B` — fix on sight.

## Brand Token Enforcement

### Tailwind Config (yoyo-player-map)
Ensure `tailwind.config.ts` / `tailwind.config.js` includes:
```ts
colors: {
  brand: {
    red:   '#B80000',
    navy:  '#102040',
    cream: '#fffdfa',
    gold:  '#C9A84C',   // VSYC use only
    teal:  '#13C3A3',   // Donate CTA only
  },
}
```
If `#D42B2B` appears anywhere, replace it with `#B80000`.

### CSS Variables (dmvt-event-hub)
Ensure global CSS defines:
```css
--red:   #B80000;
--navy:  #102040;
--cream: #fffdfa;
--gold:  #C9A84C;
--teal:  #13C3A3;
```

### Typography
- Display: **Playfair Display** (never in red)
- Body: **DM Sans**
- VSYC accent: **Montserrat** (VSYC context only)

### Visual Rules
- `border-radius: 0` for all brand cards and marketing sections.
- No `box-shadow` on brand cards.
- Buttons: uppercase, `letter-spacing: 0.095em`, min height `44px`.
- `max-width: 1100px` for marketing/landing sections.

## Animation Policy
- UI interactions (accordions, dropdowns, toasts, map popups) may use standard transitions ≤ `0.2s ease`.
- Marketing/landing sections: no animation at all.
- Do not add keyframe animations, scroll-triggered animations, or parallax effects.

## Privacy Rules (yoyo-player-map)
- Store only city-level location — never street, neighborhood, or coordinates below city.
- All player pins are opt-in. No auto-population.
- Report flow must be available on every player pin.

## Supabase / Edge Function Rules (dmvt-event-hub)
- Required env vars: `VITE_SUPABASE_URL`, `VITE_SUPABASE_PUBLISHABLE_KEY`, `VITE_SUPABASE_PROJECT_ID`.
- Edge functions: `submit-event`, `verify-event`, `manage-event`, `renew-event`, `daily-maintenance`.
- Test edge functions locally before committing.
- Verify migrations in `supabase/migrations/` are consistent and sequential.

## Last-Modified Documentation Policy
When you add or significantly change a feature, record a `lastModified` date comment or field in:
- The relevant page/component file header (as a `// Last updated: YYYY-MM-DD` comment).
- The `README.md` changelog section if one exists.
- Any relevant `package.json` `"version"` bump if the change is API-facing.

## Voice And Copy (App UI Strings)
- Buttons and nav: ALL CAPS.
- Headings: Title Case.
- Body/helper text: sentence case.
- Second person voice. Short sentences.
- No emoji in UI strings except `☕` for donate context.

## Required Execution Pattern
1. List the exact files you will touch — confirm scope before editing.
2. Make the smallest possible diff; prefer editing existing components over creating new ones.
3. Run the validation checklist.
4. Output a diff summary grouped by file.

## Validation Checklist
- [ ] No horizontal scroll at 360px viewport width.
- [ ] Brand red is `#B80000` — search diff for `#D42B2B` or other off-brand reds.
- [ ] No new `border-radius` or `box-shadow` added to brand cards.
- [ ] No new animations beyond `0.2s ease`.
- [ ] Privacy: no sub-city location data exposed.
- [ ] Env vars not hardcoded — only via `.env` / Vercel project settings.
- [ ] Last-modified comment added where applicable.
- [ ] `dmvt-event-hub` not deployed to production.

## Commit Conventions
| Scope                  | Prefix              |
|------------------------|---------------------|
| New map feature        | `feat(map):`        |
| Event hub feature      | `feat(events):`     |
| Brand token fix        | `fix(brand):`       |
| Privacy fix            | `fix(privacy):`     |
| Supabase migration     | `chore(db):`        |
| Dependency update      | `chore(deps):`      |
| Docs/README            | `docs:`             |
