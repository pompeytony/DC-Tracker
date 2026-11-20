# HANDOVER: DC-Tracker

## What it is
A one-page reading tracker for Tony's comics. Tony has short-term memory difficulties, so each entry's 'What You Need to Know Before Reading' recap is the most important part of the app.

The page has three tracks:

1. DC 2025 onwards. The existing list: 57 story entries and 326 tickable issue lines.
2. Marvel from 1990 onwards, one year at a time. This branch has 1990 only: 29 story arcs and 99 issue lines. The next year to add is 1991.
3. Marvel 2025 onwards. A checked starter list: 23 story arcs and 114 issue lines. It is not the full line.

Merging to main publishes the site. The three tracks are already on the live site.

## Where it lives
- Code: https://github.com/pompeytony/DC-Tracker (public, branch main)
- Live site: https://pompeytony.github.io/DC-Tracker/ (GitHub Pages)
- Every merge to main goes live straight away.

## How it's built
- One file, index.html: plain HTML and JavaScript, no build step, no backend.
- Styling: Tailwind CSS from a CDN, with Google Fonts Inter (body text) and Oswald (headings).
- Look: dark page with a faint blue dot pattern and rounded cards. The page background is #070A12. The header and the `dcDark` token are #090D16. Cards are #111827. Other colours: DC blue #0476F2, Absolute red #E11D48, gold #F59E0B, and Marvel red #EC1D24 on the Marvel tracks. Emerald marks a story or issue as read (and is also the DC trade-paperback badge). Amber is the 'Next up' line (and is also the single-issue badge). Marvel story cards are still drawn CSS covers. On the DC track the big volume card shows a Comic Vine trade cover, and falls back to the drawn card if that picture fails (see Trade paperback covers). Each issue line shows a Comic Vine thumbnail (see Cover thumbnails).
- DC data: a hard-coded list `READING_DATA`. Each entry has id, order, era, format (`TPB` or `Single Issues`), title, subtitle, whatYouNeedToKnow, issues, coverTheme and ultraSearch. The recaps aim at about 25–50 words. In the DC file they run from 22 to 52 words.
- `ultraSearch` on a DC entry is a search phrase, not a full web address. The page turns it into `https://www.dcuniverseinfinite.com/search?q=` plus that phrase.
- Marvel entries use the same shape. Every Marvel link opens `https://www.marvelcomicsapp.com/`. On 17 Nov 2026 the addresses `/search` and `/search?q=spider-man` both returned 404, and issue pages use a private number (`/issues/2578`), so there is no confirmed search address. The button says so.

## How progress is saved
- Only in the browser (localStorage). Separate for each device and browser.
- DC key, unchanged: `dc_ultra_tracker_2025_2026_v1`.
- Marvel 1990 key: `marvel_1990s_tracker_v1`.
- Marvel 2025 key: `marvel_2025_tracker_v1`.
- The last track chosen is remembered under `reading_tracker_active_track_v1`. That key is not the progress.
- Ticks are saved by entry id and the issue's position in its list (for example `vol-01::0` or `m90-01::0`). Never reorder or rename existing entries or issues. Some DC lines are ranges, such as `Deathstroke: The Terminator #1–5`, and each line is one tick.
- The completion percentage is based on finished entries, not on individual issues. The issue count is shown beside it.
- 'Backup JSON' downloads all three tracks (version 2). 'Restore' replaces what is in the file. An old DC-only backup still works: it replaces the DC track and leaves the Marvel tracks as they are. Tony should back up before any big update.

## Cover thumbnails
Each issue line shows a small cover from Comic Vine. Only public image links are stored, in a `COVERS` constant in index.html. There is no API key in the repo, and one must never be added.

The shape is `{ base, note, tracks: { dc, marvel1990, marvel2025 } }`. Those track names are the same as `TRACK_KEYS`, so no extra mapping is used. A key is the same as a tick: `entryId::issueIndex`. For example, on the DC track, `vol-03::0` is Absolute Batman #1. The index is the position in that entry's `issues` array. The thumbnail address is `base` plus the stored path (about 104×160). The larger picture in the lightbox is that same address with `scale_avatar` replaced by `scale_medium`.

`COVERS` has to be refreshed whenever issues are added or the order of an entry's issues changes. That includes the next Marvel year (1991). Reordering issues would point a cover at the wrong line. One DC line has no cover: `vol-36::6`, The Flash 2025 Annual #1. That line, and any picture that fails to load, shows a plain placeholder in the track colour (DC blue or Marvel red). Tapping a thumbnail opens the larger cover and does not change the tick.

## Trade paperback covers
The big volume card on the DC track shows a trade cover from Comic Vine. Only public image links are stored, in a `TPB_COVERS` constant in index.html. There is no API key. Marvel tracks are unchanged and still use the drawn card.

The shape is `{ base, note, volumes }`. Each key is an entry `id`, such as `vol-03`, and the value is `{ path, source }`. The card picture is `base` plus `path`, with `scale_avatar` swapped for `scale_small` (about 417×640). Tapping the card opens the same lightbox as an issue thumbnail, using `scale_medium`, and does not mark the volume read. If the picture fails to load, the drawn colour card is shown instead.

`source` is `tpb` when the picture is the collected edition, and `issue1` when it is the first issue instead. Those cards show a small 'Issue #1 cover' tag. 24 trades are not on Comic Vine yet, so they use that first-issue cover and can be refreshed later. Five single-issue entries also use the first issue, which is the right picture for them.

Flag for Tony: `vol-19` is titled Titans Vol. 3: Out of the Shadows. Comic Vine says 'Out of the Shadows' is Titans Vol. 1, and Vol. 3 is 'Hard Feelings'. The title was not changed. That card uses the issue #1 cover rather than a guessed trade.

## Rules
1. Code changes go only through a cloud coding agent and a pull request. Never edit on Tony's Mac.
2. No merge and no deploy without Tony's explicit OK in chat. Merging means going live.
3. No secrets in the repo. It's public.
4. Only one assistant changes this app at a time.
5. Never invent results. Flag anything unverified, especially comic recaps and issue lists.
6. Keep the UI clean, friendly and in British English.
7. Keep the Status section up to date.

## Status (20 Nov 2026)
- DC volume cards now show a Comic Vine trade cover from `TPB_COVERS` (public links only). 24 trades not yet on Comic Vine use the first-issue cover, tagged 'Issue #1 cover', and can be refreshed later. `vol-19` (Titans Vol. 3: Out of the Shadows) may be the wrong title: Comic Vine says 'Out of the Shadows' is Titans Vol. 1, and Vol. 3 is 'Hard Feelings'. The title was not changed. See Trade paperback covers.
- Cover thumbnails are on every issue line, from public Comic Vine image links stored in `COVERS`. Lists, entry ids, issue order, names and storage keys are unchanged. One DC line has no picture: The Flash 2025 Annual #1 (`vol-36::6`). See Cover thumbnails.
- DC track: still the default. The list is unchanged: 57 entries, 326 tickable issue lines (51 trades and 6 single-issue entries). The storage key is still `dc_ultra_tracker_2025_2026_v1`.
- Three-track switch is on the live site. Tracks: 'DC 2025 →', 'Marvel 1990s →', 'Marvel 2025 →'. The page remembers the last one. Counts, the progress bar, Next up, era filters and search follow the selected track. The trade / single-issue filter is hidden on the Marvel tracks, because those lists are single issues only.
- Marvel 1990: 29 arcs, 99 issue lines. Key arcs for Amazing Spider-Man, Spectacular Spider-Man, the 1990 Spider-Man series, Uncanny X-Men, X-Factor, New Mutants, Avengers, Fantastic Four, Thor, Captain America, Iron Man and Wolverine. It is not every issue published in 1990. Chapters cover-dated 1991 are left out on purpose, including the last three chapters of X-Tinction Agenda, the last three issues of Armor Wars II, and Fantastic Four #348–349.
- The next Marvel year to add is 1991. Add it in its own pull request when Tony nears the end of 1990.
- Marvel 2025 onwards: 23 arcs, 114 issue lines. A starter list covering One World Under Doom and its main tie-ins, the 2025 Amazing Spider-Man launch, X-Manhunt, the Giant-Size anniversary, Hellfire Vigil, the spine of Age of Revelation, and the opening of Shadows of Tomorrow. Later issues of the ongoing 2026 books are not listed yet.
- Marvel data source: the Marvel Comics app powered by WEBTOON (launched 16 Nov 2026; it replaces Marvel Unlimited, which closes 7 Dec 2026). It has no public API and no export, and its terms ban scraping, so the lists are hand-curated from Marvel and reference pages, and ticked by hand.
- Anything still uncertain is written in the Marvel pull request. Do not treat a gap as a fact.
