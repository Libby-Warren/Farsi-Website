# Zabān: Academy of Persian Charms

A Persian (Farsi) learning web app built by Libby, a Stanford student, as the final
project for CS193T. The course requires an agentic component and a rubric-graded
presentation. Live site: https://libby-warren.github.io/Farsi-Website/ (GitHub Pages,
deployed from the `main` branch root). This repo is the source of truth; the old
claude.ai artifact link is no longer the main copy.

## Who it's for
- Libby is a complete beginner. Her partner and close friends are from Tehran.
- Goal: a real conversation with them within 1 year; comfortable in any social
  setting within 5 years.
- Duolingo has no Farsi, and Stanford's Persian 1 assumed a heritage background and
  moved too fast on script, pace, and grammar. Zabān exists to fix that.
- She wants to learn mostly independently. Native speakers are a supplement, not a
  crutch (no relying on her partner for pronunciation audio).

## Content rules
- Colloquial Tehrani Persian first (e.g. اون/un, خونه/khune, کوچیک/kuchik).
  Formal/written Persian is added later, as notes.
- Always show Persian script and transliteration together.
- Explicit grammar rule first, then examples.
- Vocabulary-focused. Alphabet/letter lessons were removed on purpose; don't add them back.
- About 20-30 minutes of study a day: flashcards, listening, reading/writing, AI role-play.

## How to work with Libby
- Suggest, then wait. She approves every action, including every commit.
- Short iterative changes and working builds quickly. "Bland," "boring," or "basic"
  results frustrate her.
- When creative direction is ambiguous, offer 2-4 multiple-choice options rather than
  guessing or asking open-ended questions.
- Visual references (screenshots, named styles) steer design better than adjectives.
- Write clear commit messages that describe the change in plain words.

## Design
- Night-castle look: night-sky hero with animated owls; isometric castle path where
  towers light up as lessons finish and spires light up for passed unit tests; unit
  switcher showing real per-unit progress; light/dark mode.
- Tappable sky/scene elements reveal Persian words: shooting stars (night words),
  three constellations with Persian names, tabby cats (cat words), and two teams of
  three robed California ground squirrels on broomsticks (squirrel words).
- Everything must be an original design. Do NOT recreate protected characters or
  designs (Hogwarts architecture, house robes/crests, golden snitches, specific book
  characters, logos). Decline in one line and offer an original alternative; Libby
  is happy with that.

## Code
- The whole site is one self-contained `index.html` (HTML, CSS, JS inline). No build
  step, no framework. Keep it that way unless Libby asks otherwise.
- Progress (streak, XP, lit towers, spaced-repetition cards) lives in localStorage,
  per browser. It doesn't sync across devices; this is stated in "Good to know."
- Lesson engine: `exercisesFor(n)` builds each lesson's queue from exercise builders
  (`exFaEn`, `exEnFa`, `exMatch`, `mkBuild`, `exSay`, `exType`, ...); `check()`,
  `exHTML()`, and `renderPlayer()` grade and draw them. Hearts, XP, streak, and
  unit-test gating must keep working after any change.
- Typed answers (`exType` / `gradeType`) are checked in the browser, no API: accepts
  script or transliteration, ignores macrons/case/spaces/half-spaces, maps Arabic
  ي/ك to Persian ی/ک, and treats a one-letter typo (words of 4+ letters) as correct
  with a spelling note.
- Mixed Persian + Latin text in one line goes in `<bdi>` so it doesn't render backwards.

## Testing before every commit
- Screenshot QA with Playwright at 1280x820 (desktop) and 390x800 (phone).
- Use `force=True` to click elements with continuous CSS animations; use
  `full_page=True` to catch layout issues outside the viewport.
- For bigger changes, play a full lesson end to end, check dark mode, and confirm that
  progress persists after a reload.

## Next up
- AI-graded sentence practice (and possibly role-play) using the Claude API. The API
  key must NEVER go in `index.html` or anywhere in this public repo. Plan: a small
  Cloudflare Worker holds the key as a secret; the site sends the learner's sentence
  to the Worker, which calls Claude and returns feedback on meaning, grammar, and
  colloquial Tehrani style.
- Later: feed words "caught" from stars, constellations, cats, and squirrels into the
  spaced-repetition review deck.
