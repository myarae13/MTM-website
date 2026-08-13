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

**Go High Level embeds.** Two ids near the bottom of the `<script>` block drive
everything:

```js
const GHL = {
  CALENDAR_ID: "",   // 15-minute call  → contact section
  FORM_ID:     "",   // teardown form   → offer section
};
```

- `CALENDAR_ID` — GHL → Calendars → your calendar → **Copy Link**, then take the
  last path segment of `.../widget/booking/<id>`.
- `FORM_ID` — GHL → Sites → Forms → your form → **Integrate → Inline**, then take
  the last path segment of `.../widget/form/<id>`.

Each `[data-ghl]` mount ships with a working `mailto:` / `tel:` fallback inside
it. If the id is blank the fallback stays; if the id is set, an iframe replaces
it and GHL's `form_embed.js` resizer is appended (only then — a blank config
pulls no third-party script). **Nothing is ever a dead link in either state.**

The two CTAs are deliberately different asks: the form is the low-commitment
teardown, the calendar is the bigger phone-call ask. Don't collapse them into one.

Note that the embeds are styled by GHL, not by this stylesheet. Match them in
GHL's own form/calendar builder or they'll read as foreign to the page.

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

Hosted on Vercel, deployed from `main` on GitHub.
