# Spark Street Advisors — Website Source

**Plain, hand-authored static HTML.** There is no build step — every page is
a real `.html` file in this repo, and Netlify publishes them exactly as-is
whenever `main` is pushed.

## The easiest way to make changes

If you're not comfortable editing code directly, the simplest path is to
work with an AI coding assistant (e.g. Claude, at claude.ai or Claude Code).
Just describe what you want changed in plain English — "add so-and-so to
the team page," "fix this typo," "change this color" — and have it:

1. Clone this repo (`https://github.com/sscnyc/spark-street-website`)
2. Make the edit directly in the relevant `.html` file(s)
3. Commit and push to `main`

Netlify automatically rebuilds and redeploys within a minute or two of any
push to `main`. No build command is configured or needed.

To push, the assistant will need a **GitHub personal access token** with
`repo` scope (Settings → Developer settings → Personal access tokens →
Tokens (classic) → Generate new token). Generate one, share it for that
session, and revoke it afterward (Settings → Developer settings → Personal
access tokens) once the changes are confirmed live.

## Structure

```
index.html                  → homepage
assets/style.css            → all site styling (CSS custom properties at the top control colors/fonts)
assets/img/team/            → team headshots
team/
  core-team/index.html      → Core Team listing (person cards)
  analysts/index.html       → Analysts listing (current + past)
  <person-slug>/index.html  → one bio page per core team member
publications/
  index.html                → Publications listing + topic/category filter
  <pub-slug>/index.html     → one page per publication
policies/index.html         → Policies listing page
coreTeam.json, analysts.json, publications.json
                             → reference data files, kept in sync with the
                               HTML by convention; NOT read by the live site
```

## Adding a new team member

1. Copy an existing folder under `team/` (e.g. `team/clara-greiner/`) to a
   new folder named after the person's slug (e.g. `team/jane-doe/`)
2. Edit the name, role, location, and bio text inside that new `index.html`
3. Add a matching card to `team/core-team/index.html` (copy an existing
   `<div class="person-card">` block, update the details and the link)
4. Optionally update `coreTeam.json` to match, for reference

## Adding a new publication

1. Copy an existing folder under `publications/` to a new slug-named folder
2. Edit the title, authors, source, summary, and the "View publication"
   link inside that new `index.html`
3. Add a matching card to `publications/index.html` (copy an existing
   `<div class="pub-item">` block — note the `data-cat` and `data-topic`
   attributes control which filter tabs it shows under; multiple topics
   can be given as `topic-one;topic-two`, separated by a semicolon, **not**
   a comma, since several topic names contain commas themselves)
4. Optionally update `publications.json` to match, for reference

## Colors & fonts

All colors are CSS custom properties at the very top of `assets/style.css`
(`--teal`, `--amber`, `--ink`, `--paper`, etc.) — change them there and
they update sitewide. Fonts (Fraunces for headings, IBM Plex Sans for body)
are loaded via Google Fonts in every page's `<head>`.

