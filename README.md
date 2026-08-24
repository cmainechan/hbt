# Hebrew Interlinear Practice Widget

A self-contained, static web app for practicing word-by-word translation of the
Hebrew Bible. Type a citation, get blanks above each Hebrew word, press Enter
to check each word.

## What's in here

- `index.html` — the app (HTML/CSS/JS, no build step, no dependencies)
- `data/*.json` — one file per book of the Tanakh (39 files), each containing
  every verse broken into words with Hebrew text and accepted English glosses
- `data/index.json` — a summary (chapter/verse counts per book), not used by
  the app itself but handy for sanity-checking the data

## Data source & license

The word-level Hebrew text and English glosses come from the **STEPBible
TAHOT** dataset (Translators Amalgamated Hebrew Old Testament), produced by
Tyndale House, Cambridge, and STEPBible.org, licensed **CC BY 4.0**.
Source: https://github.com/STEPBible/STEPBible-Data

If you publish this anywhere public, keep a credit line along the lines of:

> Hebrew text and interlinear glosses: STEPBible-Data (Tyndale House,
> Cambridge / STEPBible.org), CC BY 4.0.

The data was reformatted (from STEPBible's tab-separated format into
per-book JSON) for use in this app; no wording was changed.

## Deploying to GitHub Pages

1. Create a new GitHub repository (public or private with Pages enabled on
   your plan).
2. Add these files to the repo root, preserving the folder structure:
   ```
   your-repo/
     index.html
     data/
       genesis.json
       exodus.json
       ...
       index.json
   ```
3. Commit and push.
4. In the repo settings, go to **Settings → Pages**, set the source to the
   branch you pushed (e.g. `main`) and folder `/ (root)`.
5. GitHub will publish it at `https://<your-username>.github.io/<repo-name>/`.
   It can take a minute or two after the first push.
6. Open that URL — the citation box should work immediately, since the JSON
   files are served from the same origin.

No server, database, or build step is required — it's plain static files.

## Using the app

Type a citation like:
- `Genesis 1:1`
- `Genesis 1:1-5` (ranges within a single chapter, up to 30 verses)
- `Psalm 23:1-6`
- `1 Samuel 3:10`

Then press Enter on each word's blank to check it. "Check remaining" grades
everything left on the page; "Reset" reloads the same passage with blanks
cleared.

## Notes on the glosses

Each word's "answers" list has a primary gloss (shown on reveal) plus
accepted variants — mostly to account for how STEPBible marks:
- `<angle-bracket>` content — present in Hebrew but not usually translated
  (e.g. the untranslatable direct object marker את) — accepted answers
  include `-`, `(untranslated)`, and the literal marker.
- `[square-bracket]` content — implied by Hebrew grammar though not a
  separate word (e.g. "[the]") — included in the primary gloss since a
  translator would normally supply it.

If you want stricter or looser matching, that logic lives in the
`checkWord()`/`normalize()` functions in `index.html` and is easy to adjust.
