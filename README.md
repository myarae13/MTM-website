# MTM Website

Conversion-focused portfolio site for **MTM Marketing** — a single-file static website built on the AIW "Trust + Conversion" wireframe. Styled to match the MTM logo: a retro, layered-offset look in navy · terracotta · cream-gold on a dusty-blue ground. Brand mark lives in `mtm-logo.svg`.

## Structure

`index.html` is fully self-contained (HTML + CSS + JS inline). No build step.

Sections, in order: Hero → 3 reason cards → Portfolio → 5-step Process → Pain & Solution → Testimonials → Reviews + logos → About → FAQ → CTA.

## Editing

Everything you need to customize is tagged with `<!-- EDIT -->` comments:
- Studio/your name, `[your niche]`, phone number
- Hero headline + founder photo
- Portfolio screenshots (replace each `.thumb` gradient with an `<img>`)
- Testimonials (the `TESTIMONIALS` array in the `<script>`)
- CTA link (currently `mailto:` — swap for Calendly/Formspree)

## Local preview

Open `index.html` directly in a browser, or serve it:

```bash
python3 -m http.server 8000
```

## Deploy

Hosted on Vercel as a static site.
