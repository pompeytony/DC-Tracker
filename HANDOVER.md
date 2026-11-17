# HANDOVER: DC-Tracker

## What it is
A one-page reading tracker for Tony's comics. It currently covers the DC All In and Absolute era (2025–2026): 57 story entries and 326 tickable issue lines, in reading order. Each entry has a short 'What You Need to Know Before Reading' recap so Tony can pick up where he left off. Tony has short-term memory difficulties, so the recaps are the most important part of the app.

## Where it lives
- Code: https://github.com/pompeytony/DC-Tracker (public, branch main)
- Live site: https://pompeytony.github.io/DC-Tracker/ (GitHub Pages)
- Every merge to main goes live straight away.

## How it's built
- One file, index.html: plain HTML and JavaScript, no build step, no backend.
- Styling: Tailwind CSS from a CDN, with Google Fonts Inter (body text) and Oswald (headings).
- Look: dark page with a faint blue dot pattern and rounded cards. The page background is #070A12. The header and the `dcDark` token are #090D16. Cards are #111827. Other colours: DC blue #0476F2, Absolute red #E11D48 and gold #F59E0B. Emerald marks a story or issue as read (and is also the trade-paperback badge). Amber is the 'Next up' line (and is also the single-issue badge). Covers are drawn in CSS, not images.
- Data: a hard-coded list `READING_DATA` in index.html. Each entry has id, order, era, format (`TPB` or `Single Issues`), title, subtitle, whatYouNeedToKnow, issues (a list of issue names), coverTheme and ultraSearch. The recaps are short and friendly. The aim is about 25–50 words. In the file on 17 Nov 2026 they run from 22 to 52 words.
- `ultraSearch` is a search phrase, not a full web address. The page turns it into `https://www.dcuniverseinfinite.com/search?q=` plus that phrase.

## How progress is saved
- Only in the browser (localStorage), under the key `dc_ultra_tracker_2025_2026_v1`. It is separate for each device and browser.
- Ticks are saved by entry id and the issue's position in its list (for example `vol-01::0`). Never reorder or rename existing entries or issues. Some issue lines are ranges, such as `Deathstroke: The Terminator #1–5`, and the tracker counts each line as one tick.
- The completion percentage is based on finished entries, not on individual issues. The issue count is shown beside it.
- 'Backup JSON' downloads a file. 'Restore' reads one back and replaces the current progress. Tony should back up before any big update.

## Rules
1. Code changes go only through a cloud coding agent and a pull request. Never edit on Tony's Mac.
2. No merge and no deploy without Tony's explicit OK in chat. Merging means going live.
3. No secrets in the repo. It's public.
4. Only one assistant changes this app at a time.
5. Never invent results. Flag anything unverified, especially comic recaps and issue lists.
6. Keep the UI clean, friendly and in British English.
7. Keep the Status section up to date.

## Status (17 Nov 2026)
- DC track: live and working. Checked against index.html on 17 Nov 2026: 57 entries, 326 tickable issue lines (51 trades and 6 single-issue entries).
- Marvel extension: Tony approved the plan on 17 Nov 2026. He wants three tracks: (1) DC 2025 onwards (the existing track); (2) Marvel from 1990 onwards, single issues only, added ONE YEAR AT A TIME starting with 1990, with the next year added in its own PR when Tony nears the end of the current one; (3) Marvel 2025 onwards, single issues only. As with DC, each story arc has one 'What You Need to Know' recap, with its single issues ticked underneath.
- Marvel data source: the 'Marvel Comics powered by WEBTOON' app (launched 16 Nov 2026; it replaces Marvel Unlimited, which closes 7 Dec 2026). It has no public API and no export, and its terms ban scraping, so the Marvel lists are hand-curated and ticked by hand.
- Not built yet on this branch: the track switch, the Marvel lists, and the shared backup. Those belong in a separate pull request. Do not merge that work until Tony says so.
