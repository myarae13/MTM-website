# MTM Website

Marketing site for **MTM Marketing** — websites for local trade and home-service
businesses. Single static page, no build step, hosted on Vercel.

## Design

Light ground, one typeface (Schibsted Grotesk), brass as a graphic accent and
brick as the readable accent. The boldness is spent in one place: the work index.

Tokens live in `:root` at the top of the `<style>` block in `index.html`.

| Token | Value | Use |
|---|---|---|
| `--ink` | `#12100e` | headings, primary buttons |
| `--ink-2` | `#4f4a43` | body copy |
| `--ink-3` | `#6f6960` | meta, captions |
| `--brick` | `#9c4a2f` | readable accent, eyebrows, hover |
| `--brass` | `#b57a2e` | graphic only — underlines, rules |

## Structure

`index.html` is fully self-contained (HTML + CSS + JS inline).

Hero → Work index → Founder → Free teardown → Good to know → Contact → Footer.

Other files: `og.png` (social card), `robots.txt`, `sitemap.xml`, `vercel.json`
(security headers), `work/` (project screenshots), `founder.jpg`, logo assets.

## Editing

**Go High Level embed.** One id near the bottom of the `<script>` block drives
everything:

```js
const GHL = {
  CALENDAR_ID: "",   // 30-minute call → both the offer and contact sections
};
```

- `CALENDAR_ID` — GHL → Calendars → your calendar → **Copy Link**, then take the
  last path segment of `.../widget/booking/<id>`.

The same calendar mounts twice, at `[data-ghl="calendar"]` in the offer section
and again in the contact section. Each iframe gets its own DOM id (the second is
suffixed `-2`) because `form_embed.js` resizes by id and would otherwise only
ever find the first one. The resizer script is appended only if a calendar
actually mounted, so a blank config pulls no third-party script.

**The calendar is the only contact path on the page.** There is no phone number,
no email address and no form anywhere in the markup or the JSON-LD, by choice.
That means a blank `CALENDAR_ID` ships a page nobody can respond to. Never
deploy with it blank.

Note that the embed is styled by GHL, not by this stylesheet. Match it in
GHL's own calendar builder or it'll read as foreign to the page.

**Adding a build.** Copy one `<article class="w-row">`, bump the number, drop a
screenshot in `work/`, and set the tag honestly — `w-tag--client` for a real
paying client, `w-tag--concept` for self-initiated work.

**Standing rule: no fabricated social proof.** No testimonials, client logos or
results that aren't real. The page labels client builds vs concepts on purpose.

**If the domain changes,** update the absolute URLs in `<head>` (canonical, `og:`,
`twitter:`), the JSON-LD block, `robots.txt` and `sitemap.xml`.

## Local preview

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Regenerating the social card

`og.png` is rendered from a standalone HTML card at 1200×630 with headless
Chromium. Keep it in sync with the hero headline if that changes.

## Deploy

Hosted on Vercel at https://mtmmarketer.com, deployed from `main` on GitHub.
