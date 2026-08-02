# Dutch Flashcards

A single-file flashcard app for learning everyday/survival Dutch, with per-topic
decks and basic spaced repetition (mark "Know it" / "Don't know yet" — unknown
words come back more often, known words fade out).

## How to use it

1. Push this repo to GitHub.
2. In repo Settings -> Pages, set source to the `main` branch, root folder.
3. GitHub gives you a URL like `https://<username>.github.io/dutch-flashcards/`.
   Open that on your phone or laptop — no login, no build step, works offline
   once loaded (progress is saved in the browser via localStorage).

## Adding new daily word batches

All the vocabulary lives in the `DECKS` object near the top of the `<script>`
tag in `index.html`. Each deck looks like this:

```js
"topicname": {
  label: "Human-Readable Topic Name",
  words: [
    { nl: "dutch word", pron: "simple phonetic spelling", en: "english meaning", example: "Example sentence." },
    ...
  ]
}
```

The `pron` field is a simplified English-friendly phonetic spelling (not IPA),
shown right on the card so you don't need a separate lookup. Key conventions
used throughout, also shown as a legend on the page itself:

- `kh` = the guttural Dutch g/ch sound (back-of-throat, like Scottish "loch")
- `ay` = like "day"
- `ew` = rounded "ee" (say "ee" with rounded lips, close to French "u")
- `uh` = short unstressed "a" as in "sofa"
- CAPS = stressed syllable

Ask Claude for new batches in this exact shape (with `pron` included) and
just paste them into the relevant deck.

To add a new day's batch:
- If it fits an existing topic (e.g. more shopping words), just append 10-15
  new `{ nl, en, example }` entries to that deck's `words` array.
- If it's a new topic (e.g. "Food", "Weather", "Work"), add a new key to
  `DECKS` following the same shape. It will automatically show up in the
  topic dropdown.

Ask Claude for the next day's batch already formatted as this JS object shape,
and just paste it in — no other code changes needed.

## Current decks

- Greetings & Basics
- Numbers
- Shopping
- Transport
- Small Talk

## Suggested daily rhythm

- 10-15 new words per day, added to the relevant deck
- Review the deck for 5-10 minutes in the morning and again after work
- Once a deck's mastery counter (shown in the dropdown) is close to full,
  start a new topic
