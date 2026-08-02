# Dutch Flashcards

Flashcard app for everyday/survival Dutch. Per-topic decks, phonetic
pronunciation on every card, and basic spaced repetition. Words live in
separate data files so adding a daily batch is a one-file commit.

## Setup (once)

1. Push this repo to GitHub.
2. Settings -> Pages -> source: `main` branch, root folder.
3. Open `https://<username>.github.io/dutch-flashcards/`.

Progress is stored in your browser (localStorage), so it survives reloads but
is per-device.

## Repo layout

```
index.html            the app (rarely needs editing)
data/
  manifest.json       list of every data file to load
  seed-*.json         starter decks
  _TEMPLATE.json      copy this for new batches
  2026-08-02.json     your daily files
```

## The daily workflow (your green squares)

Each day, two small edits:

**1. Add a new file** `data/YYYY-MM-DD.json`:

```json
{
  "topic": "food",
  "label": "Food & Drink",
  "words": [
    { "nl": "het brood", "pron": "ut broht", "en": "the bread", "example": "Ik koop het brood." }
  ]
}
```

**2. Add its filename to `data/manifest.json`:**

```json
{ "files": ["seed-greetings.json", "...", "2026-08-02.json"] }
```

Commit both. Done — that's your daily commit, and the app picks the words up on
next load.

### How merging works

Files are merged by their `topic` field, not by filename. So a daily file with
`"topic": "shopping"` adds its words to the existing Shopping deck rather than
creating a new one. Use a new `topic` value to start a fresh deck; it appears in
the dropdown automatically.

Duplicate Dutch words within a topic are ignored, so re-adding a word is
harmless.

## Word format

```json
{ "nl": "dutch", "pron": "phonetic", "en": "english", "example": "Sentence." }
```

`pron` is simplified English-friendly phonetics, not IPA. Conventions (also
shown as a legend in the app):

- `kh` = guttural Dutch g/ch (back of throat, like Scottish "loch")
- `ay` = as in "day"
- `ew` = rounded "ee" (say "ee" with rounded lips)
- `uh` = short unstressed "a" as in "sofa"
- CAPS = stressed syllable

## Local preview

Opening `index.html` directly via `file://` will fail — browsers block fetches
from the filesystem. Run a local server instead:

```bash
python3 -m http.server
```

Then open `http://localhost:8000`.

## Notes

- Words are sorted alphabetically within a deck, and progress is keyed by the
  Dutch word itself, so reordering or inserting words never scrambles your
  learning progress.
- A file listed in the manifest but missing from disk is skipped with a console
  warning rather than breaking the app.
