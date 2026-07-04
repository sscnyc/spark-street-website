# Spark Street Advisors — Website Source

This is a data-driven site: **Team** and **Publications** pages are generated
automatically from two simple data files. To add a new team member or
publication, you edit one entry — you never touch HTML or create new pages
by hand.

## Editing content

- **Team members:** `src/_data/coreTeam.json`
- **Analysts:** `src/_data/analysts.json`
- **Publications:** `src/_data/publications.json`

To add a new team member, copy one of the existing `{ ... }` entries in
`coreTeam.json`, fill in the fields, and give it a unique `slug` (used in
the URL, e.g. `"jane-doe"` becomes `/team/jane-doe/`). A full bio page for
them is generated automatically.

Same idea for publications: copy an entry in `publications.json`, fill in
`title`, `authors`, `summary`, `source`, `url`, `year`, and a unique `slug`.
Set `category` to `"journal"`, `"pandemic"`, or `"report"` (or `"both"` if it
belongs on more than one list) — this controls which filter tab it shows
under on the Publications page.

## Building the site locally

```
npm install
npx @11ty/eleventy        # builds once, output in _site/
npx @11ty/eleventy --serve  # builds and serves locally at localhost:8080, rebuilds on save
```

## Deploying (GitHub + Netlify)

1. Push this whole folder to your GitHub repo (`spark-street-website`).
2. In Netlify, under **Site configuration → Build & deploy**, set:
   - **Build command:** `npx @11ty/eleventy`
   - **Publish directory:** `_site`
3. From now on: edit a JSON file in GitHub, commit, and Netlify rebuilds
   and redeploys automatically within a minute or two — new pages included.

## Structure

```
src/
  _data/            → the three JSON files you'll edit
  _includes/base.njk → shared nav + footer, applies to every page
  assets/style.css   → all site styling (placeholder sage/teal/amber palette)
  index.njk          → homepage
  team/
    core-team.njk    → Core Team listing page
    member.njk       → template that generates one page per person
    analysts.njk     → Analysts listing (current + past)
  publications/
    index.njk        → Publications listing with category filter
    entry.njk        → template that generates one page per publication
```

## Colors

Currently using placeholder brand colors (sage/paper background, deep teal,
amber accent — see `src/assets/style.css` `:root` variables). Swap in your
actual brand hex codes there whenever you're ready.
