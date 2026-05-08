---
description: "Use when editing any vsyc26-*.html page. Enforces VSYC-26 immutable facts, gold brand system, division/sponsor/schedule rules, and prevents accidental changes to date, venue, or pricing."
name: "VSYC-26 Page Maintainer"
applyTo:
  - "dmvthrowers.github.io/vsyc26*.html"
---
# VSYC-26 Page Maintainer Rules

## Immutable Facts — Never Change These
| Field        | Value                                                        |
|--------------|--------------------------------------------------------------|
| Event name   | Virginia State YoYo Contest 2026 (VSYC-26)                  |
| Date         | **Saturday, September 19, 2026**                            |
| Hours        | **10 AM – 7 PM**                                            |
| Venue        | **Dulles Town Center — Center Court**, Sterling, VA          |
| Address      | 21100 Dulles Town Circle, Sterling, VA 20166                 |
| Spectator    | **Free to spectate** — this line must appear on every page  |
| Registration | $15–$25 per division                                        |
| Contest email| `vastateyoyocontest@gmail.com`                              |

If any edit touches these values, **stop and ask for explicit confirmation**.

## VSYC Page Inventory
| File                      | Purpose                          |
|---------------------------|----------------------------------|
| `vsyc26.html`             | Main landing / hero              |
| `vsyc26-register.html`    | Registration info and links      |
| `vsyc26-schedule.html`    | Day-of schedule                  |
| `vsyc26-sponsors.html`    | Sponsor tiers and logos          |
| `vsyc26-venue.html`       | Venue details and directions     |
| `vsyc26-rules.html`       | Contest rules                    |
| `vsyc26-faq.html`         | Frequently asked questions       |
| `vsyc26-divisions.html`   | Division descriptions            |
| `vsyc26-terms.html`       | Terms, waiver, refund policy     |

Only edit files from this list when performing VSYC-26 work.

## VSYC Brand System
- Primary accent: `--gold: #C9A84C` replaces `--red` on all VSYC pages.
- Background: `--cream: #fffdfa`.
- Text/headings: `--navy: #102040`.
- Font stack: **Montserrat** (display/headings) + **DM Sans** (body) — VSYC only.
- `border-radius: 0`, no `box-shadow`, no animations beyond `0.2s ease`.

## Sponsor Workflow
1. Source logo files from `DMVT-Design/assets/logos/` — never create new logos.
2. Optimize sponsor logos to < 500 KB.
3. Add `alt="[Company Name] — [Tier] Sponsor"` to every logo `<img>`.
4. Maintain tier order: Title > Gold > Silver > Bronze > Community.
5. Do not invent sponsor tiers not already defined in `vsyc26-sponsors.html`.

## Schedule Workflow
- Confirm division time slots against `vsyc26-divisions.html` before committing.
- Keep AM/PM format consistent (e.g., `10:00 AM`, not `10am`).
- Do not remove "Spectator — Free" labels from schedule rows.

## Registration Workflow
- Registration links must open externally (Ticket Tailor or official registration platform).
- Per-division pricing must match: $15–$25 range.
- Do not add payment fields or collect personal data inline.

## Document / PDF Workflow
When updating a linked PDF in `assets/documents/`:
- Append a version suffix: `vsyc26-rulebook-v2.pdf`, not overwriting the original.
- Update the `href` in `vsyc26-rules.html` to point to the new versioned file.

## Required Execution Pattern
1. List every VSYC file you will touch.
2. Confirm immutable facts will not change.
3. Make minimal edits.
4. Run validation checklist.
5. Output diff summary.

## Validation Checklist
- [ ] Date, venue, and pricing are unchanged.
- [ ] "Free to spectate" language present on every touched page.
- [ ] Gold `#C9A84C` used instead of red on VSYC pages.
- [ ] Sponsor logos have descriptive `alt` text.
- [ ] No new `border-radius` or `box-shadow`.
- [ ] Nav is consistent with other VSYC pages and with the main site nav.
- [ ] `sitemap.xml` `<lastmod>` updated for changed VSYC page URLs.
- [ ] PDF version suffix applied if a document was replaced.

## Commit Conventions
| Change type             | Prefix                     |
|-------------------------|----------------------------|
| New sponsor added       | `feat(vsyc26-sponsors):`   |
| Schedule update         | `feat(vsyc26-schedule):`   |
| Rules/divisions update  | `fix(vsyc26-rules):`       |
| FAQ / copy update       | `fix(vsyc26-faq):`         |
| General VSYC fix        | `fix(vsyc26):`             |
| Asset/logo update       | `chore(assets):`           |
