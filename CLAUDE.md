# CLAUDE.md — theplaylistemc.com

Read this before changing anything in this repo.

## What this is

The website for **The Playlist Entertainment Music Collective** ("The Playlist eMC"), Eron Trent's live-music booking business in Michigan. It is a single landing page: hero, the lineup options (trio/quartet, full band, custom set), "Meet Eron Trent", a booking form, and a footer.

- Live at **https://theplaylistemc.com** (and www.theplaylistemc.com)
- Hosted on **GitHub Pages**, served straight from the `main` branch, root folder
- Plain HTML + CSS + a few lines of JavaScript. No build step, no framework, no npm.
- Owner: Eron Trent. Set up by Erik Lauchie (Carbon Stories).

The person asking you for changes is usually Eron. He is not a developer. Make the change, keep it small, explain in one or two plain sentences what you changed, and publish it.

## Brand rules (do not drift)

- **Colors:** black `#000`, gold `#C9A43B`, white `#fff`. Muted gray `#5C5A55` for small print only. No new colors.
- **Font:** Archivo (Google Fonts, already loaded). Headlines use the condensed heavy style: class `cond` (Archivo, `font-stretch:62%`, weight 900, uppercase). Body copy is regular Archivo.
- **Name:** "The Playlist eMC" (lowercase e, capital MC) or the full "The Playlist Entertainment Music Collective". Never "EMC" in body copy (the CSS uppercases headings on its own).
- **Look:** big condensed gold type on black, gold bars, thick black rules, square corners (no rounded corners, no shadows, no gradients, no emoji).
- **Voice:** Eron's voice. Real, warm, direct, like a musician talking to a couple or an event planner. Short sentences. No hype words ("elevate", "unforgettable journey", "curated experiences", "seamless"), no em-dash-heavy marketing copy, no exclamation-point pileups. If Eron gives you exact wording, use his words as written (fix obvious typos only, and say so).

## File map

```
index.html        The whole site. <head> = title, description, favicon, social preview tags.
                  Between "SITE START" and "SITE END" = the page itself (styles, content, form script).
404.html          "Page not found" page. GitHub Pages serves it for bad URLs.
assets/
  eron-trent.jpg     Photo in the "Meet Eron Trent" section (720x743)
  og-image.jpg       Preview image when the link is shared (1200x630)
  favicon.ico, favicon-32.png, apple-touch-icon.png   Browser/phone icons
CNAME             Tells GitHub Pages the domain is theplaylistemc.com. DO NOT EDIT OR DELETE.
.nojekyll         Tells GitHub to serve files as-is. Leave it.
CLAUDE.md         This file.
README.md         Short human summary.
```

All styles are inside the `<style>` block in `index.html` and scoped under `.pemc`. The block of `!important` rules marked "readability overrides" was needed on Squarespace; it is harmless here, so leave it unless a change truly needs it.

### Where things are in index.html

| Section on the page | Look for |
|---|---|
| Top black hero ("Live music for your event.") | `<div class="hero">` |
| Hero paragraph + "Book live music" button | `<div class="hero-foot">` |
| "Pick the lineup" list | `<div class="tracks">`, one `<div class="track">` per option |
| "Meet Eron Trent" bio + photo | `<section class="about">` |
| Booking form | `<section class="book" id="pemc-book">` |
| Footer | `<footer>` |

To add a new section, copy the pattern of an existing one (`<section><div class="wrap">…</div></section>`, heading `<h2 class="cond">`). Black sections use `class="about"`-style styling; add a new class rather than reusing `about` if the layout differs.

### Adding photos

Put image files in `assets/` with a lowercase, hyphenated name (e.g. `assets/wedding-detroit-2026.jpg`). Resize to max ~1600px wide and keep under ~400 KB. Always add `alt` text describing the photo, plus `width` and `height` attributes. Reference with a relative path: `src="assets/…"`.

## The booking form (do not break it)

The form is handled by **FormSubmit** (free, no account). The script at the bottom of `index.html` sends the form with `fetch` to:

```
https://formsubmit.co/ajax/hello@theplaylistemc.com
```

Rules:
- Do **not** change that URL or the email in it. If it changes, inquiries stop arriving (or go to the wrong place) and FormSubmit has to be re-activated.
- Keep the form `id="pemc-form"`, the note `id="pemc-note"`, and the input names `name`, `email`, `date`, `type`, `details`. The script reads those exact names.
- The payload fields (`Name`, `Email`, `Event date`, `Event type`, `Details`, `_subject`, `_template:"table"`, `_captcha:"false"`) are what show up in Eron's inbox. You may add a field (add an input + add it to `payload`), but don't rename existing ones without telling Eron.
- Adding a new event type = add an `<option>` inside the `type` `<select>`.
- FormSubmit sends a one-time activation email to hello@theplaylistemc.com the first time it sees the form. Until that link is clicked, submissions are not delivered.
- Don't send test submissions casually. Each one lands in Eron's real inbox. If you must test, send one, and put "TEST" in the name.

## How to preview

- Fastest: describe the change, make it, publish, and check the live site about a minute later (it is one page, and undo is one commit).
- Local preview, if you have a shell: from the repo root run `python3 -m http.server 8000` and open http://localhost:8000. (The form works from localhost too, but see the testing rule above.)
- Bigger changes: work on a branch, open a pull request, and only merge to `main` when Eron says it looks right.

## How to publish

**Commit to `main` = live in about a minute.** GitHub Pages rebuilds automatically after every push to `main`. You can watch it under the repo's Actions tab ("pages build and deployment"). Hard-refresh the browser (or open in a private window) if the old version still shows.

Write commit messages in plain English, e.g. `Update hero paragraph`, `Add wedding photo to about section`.

**Undo:** revert the last commit (`git revert HEAD`, or the "Revert" button on the commit in GitHub) and push. Never force-push to `main`, never rewrite history.

## Before you commit: checklist

- [ ] Change is limited to what was asked. Copy and design are otherwise untouched.
- [ ] Brand: only black / gold `#C9A43B` / white, Archivo, square corners. Copy sounds like Eron, not like an ad.
- [ ] Mobile: the page still works at phone width (~375px). Long headline words don't overflow; the form stacks to one column under 520px; sections stack under 820px.
- [ ] Form: `pemc-form`, the input names and the FormSubmit URL are unchanged. The page has no JavaScript errors.
- [ ] Images: in `assets/`, reasonably small, with `alt`, `width`, `height`.
- [ ] Links: mailto and `#pemc-book` anchor still work.
- [ ] **CNAME untouched** (must contain exactly `theplaylistemc.com`).
- [ ] After publishing, load https://theplaylistemc.com and confirm the change is live.

## Do not

- Do not edit or delete `CNAME` or `.nojekyll`.
- Do not change the form email / FormSubmit endpoint.
- Do not add frameworks, build tools, trackers or cookie banners without Eron and Erik agreeing.
- Do not rename the repo or change GitHub Pages settings.
- Do not touch DNS (that lives in Squarespace Domains and also runs Eron's email).

## Background (for whoever maintains this)

The site used to be one Squarespace Code Block. It moved to GitHub Pages in October 2026 so Eron can make edits by asking Claude. The Squarespace site still exists (unpublished from the domain) as a fallback. DNS for theplaylistemc.com is managed in Squarespace Domains: the apex A records and the `www` CNAME point to GitHub Pages; email records (MX/TXT for hello@theplaylistemc.com) were left as they were.
