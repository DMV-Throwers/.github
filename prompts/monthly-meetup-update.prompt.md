---
description: "Run this prompt to perform a monthly meetup update on dmvthrowers.github.io. It auto-calculates the 3rd Sunday, checks the flyer, and updates index.html, events.html, and sitemap.xml."
mode: agent
---

# Monthly Meetup Update

## Context
You are maintaining the DMV Throwers static site (`dmvthrowers.github.io`). Perform the monthly meetup update following the exact workflow below.

## Step 1 — Resolve the Date
The meetup is **every 3rd Sunday of the month, 1–4 PM**.

Calculate the 3rd Sunday for the **next upcoming month** relative to today's date.
- If today is already past the 3rd Sunday of the current month, target next month.
- If today is before the 3rd Sunday of the current month, target the current month.

State the resolved date clearly before proceeding: e.g., `"Next meetup: Sunday, June 15, 2026, 1–4 PM."`

## Step 2 — Check the Flyer
Look for a flyer image at:
```
dmvthrowers.github.io/assets/images/events/DMV Throwers [Month YYYY].png
```
Example: `DMV Throwers June 2026.png`

- If it **exists**: confirm its file size is under 500 KB and that the `alt` text in any `<img>` referencing it is descriptive.
- If it **does not exist**: note the gap and remind Brandon to add the flyer before publishing. Continue the rest of the update without blocking.

## Step 3 — Update `index.html`
Locate the NEXT MEET banner section. It typically contains a date string and time range. Update it to reflect the newly calculated 3rd Sunday date and time `1–4 PM`. Keep all surrounding markup unchanged.

Rules:
- Do not change any nav markup.
- Do not change any other section content.
- Preserve relative links.

## Step 4 — Update `events.html`
Locate the "Upcoming Events" or equivalent list. Update or add an entry for the meetup:
- **Name:** DMV Throwers Monthly Meetup
- **Date:** [3rd Sunday you calculated], 1–4 PM
- **Location:** Arlington Central Library, Barbara M. Donnellan Auditorium, 1015 N Quincy St, Arlington, VA 22201
- **Cost:** Free
- **Description:** All ages and skill levels welcome. Bring a yo-yo or borrow one of ours.

If an entry for a past meetup date exists, move it to the "Past Events" section (or remove it if there is no past section — do not create one that doesn't already exist).

## Step 5 — Update `sitemap.xml`
Set `<lastmod>` to today's date (ISO 8601: `YYYY-MM-DD`) for:
- The `index.html` URL entry
- The `events.html` URL entry

Do not touch any other `<lastmod>` values.

## Step 6 — Validation Checklist
Before finishing, confirm:
- [ ] Correct 3rd Sunday date used (verify: month calendar check).
- [ ] Flyer exists or gap noted.
- [ ] NEXT MEET banner in `index.html` shows correct date and time.
- [ ] `events.html` entry is present with full location and "Free" cost.
- [ ] Nav is unchanged across both `index.html` and `events.html`.
- [ ] No horizontal scroll introduced at 360px.
- [ ] `sitemap.xml` `<lastmod>` updated for both URLs, no other entries touched.
- [ ] `CNAME` file is untouched.

## Step 7 — Output
Provide:
1. The resolved meetup date.
2. A diff summary for each changed file.
3. The flyer status (exists / missing).
4. Suggested commit message following convention: `feat(events): add [Month YYYY] meetup date`
