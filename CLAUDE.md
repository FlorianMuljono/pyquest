# CLAUDE.md — PyQuest Working Brief

**Read this at the start of every session. Update the "Current Phase" and "Next Task" sections as work progresses.**

---

## What PyQuest Is

A browser-based gamified Python foundations experience. A complete non-programmer sits down, gets pulled in within 60 seconds, and finishes ~3 zones having written real (if small) Python — `print`, variables, `for` loops, functions — without ever feeling like they were studying.

The entire project serves this sentence. If a decision doesn't, push back.

---

## Current Phase

**Phase 1 — Vertical Slice**

Goal: one complete encounter end-to-end that feels good. Specifically, a Skeleton King battle scene where a player types into a scaffolded `for` loop, hits Run, and watches a fireball hit the boss. Once that feels great, replication and content fill out the rest.

## Next Task

**Get Pyodide loaded via CDN in a blank HTML page, with one textarea and one Run button. `print("hello")` typed into the textarea must produce `hello` in an output element when the button is clicked.**

Acceptance criteria:
- One `index.html` file at the repo root
- Pyodide loaded via `<script src="https://cdn.jsdelivr.net/pyodide/v0.28.0/full/pyodide.js"></script>`
- One textarea, one Run button, one `<pre>` output element
- Clicking Run executes the textarea's content through Pyodide
- `print("hello")` produces `hello` in the output
- A "Loading..." message hides the page until Pyodide finishes booting
- Works in Chrome on desktop

Once this works: replace the textarea with CodeMirror 6 (also via CDN), then start building the Skeleton King battle screen.

## Recently Shipped

*(empty — project just started)*

Update this list after every completed task. Format: `- [YYYY-MM-DD] Short description of what shipped.`

---

## Non-Negotiables

These principles sit behind every decision. Re-read them before designing any encounter, mechanic, or UI element.

### Design non-negotiables

1. **The mechanic IS the concept.** Owning a game element = having that Python construct unlocked. Using it = writing that construct correctly (even if just one word in a scaffold). If you can strip the Python out of a mechanic and it still works, the mechanic isn't integrated deeply enough.

2. **The 200ms rule.** Every player action gets a visible response within 200 milliseconds. If pressing Run doesn't feel juicy, nothing else matters.

3. **First win is free.** The first encounter any player hits must be essentially impossible to fail. It exists to create the feeling of "oh, I can do this."

4. **Diegetic teaching, always.** The editor is the Spell Scroll. Running code is casting. XP is Arcane Knowledge. Never break the fiction to explain a concept.

5. **The fun test — every encounter must pass all four.**
   - Do they understand what to do within 10 seconds?
   - When they solve it, does something visibly cool happen?
   - When they fail, do they want to try again?
   - If they'd solved it first try, would it still be fun?

### Product non-negotiables

6. **No fake urgency.** Timers exist only inside battles, where they serve game fun.
7. **Syntax errors never cost HP.** A typo is not a game failure.
8. **No game over.** Failure means retry with optional gentler scaffolding.

### Pedagogical non-negotiables

9. **Real Python, not a subset.** Pyodide runs actual CPython. What works here must work identically on a player's laptop.
10. **Always scaffolded.** Every encounter has pre-filled code. The player types small amounts (one word, one number, one expression) into blanks. No blank-editor encounters in this scope.
11. **Failure is cheap and fun.** No game over. No shame. Only retries.

---

## Architectural Commitments (locked — do not re-litigate without explicit discussion)

- **Stack:** HTML + CSS + vanilla JS only. No framework.
- **No build step.** Plain JS modules (`<script type="module">`). Open `index.html` in a browser, the game runs.
- **No npm, no node_modules, no package.json.** All third-party code loaded via CDN `<script>` tags.
- **Python execution:** Pyodide via `cdn.jsdelivr.net`. Not Brython, not Skulpt.
- **Code editor:** CodeMirror 6 via `cdn.jsdelivr.net`. Not Monaco.
- **No Claude API in the product.** All hints, dialogue, and feedback are hand-written and stored as JSON.
- **No backend, no proxy, no accounts.** GitHub for source. GitHub Pages for hosting the live game.
- **No audio.** Visual feedback carries all juice.
- **Visuals:** CSS keyframes for UI transitions, 2D Canvas for battle effects (fireball, particles).
- **Save state:** LocalStorage. Single JSON blob under key `pyquest.save`.

---

## Coding Conventions

- **JavaScript:** ES2022+. Prefer `const`. Use ES modules (`import`/`export`).
- **File names:** `kebab-case.js`. One primary concept per file.
- **CSS:** Plain CSS, no preprocessors. Use CSS custom properties (`--color-spell-glow`) for theming.
- **HTML:** Semantic tags. Use data attributes (`data-encounter-id`) for game-state hooks.
- **Naming — game terms in the fiction, technical terms in the code.** UI says "Spell Scroll," class is `CodeEditor`. Player-facing strings live in encounter JSON, not in code.
- **Comments:** Explain *why*, not *what*.
- **One file = one responsibility.** If a file exceeds ~300 lines, it's probably two files.

---

## Project Structure

```
pyquest/
├── index.html
├── style.css
├── CLAUDE.md                 # this file
├── pyquest-build-plan.md     # strategy
├── pyquest-game-systems.md   # tactics — encounters, bosses
├── pyquest-content.md        # all hand-written hints and dialogue
├── README.md
├── LICENSE
├── src/
│   ├── main.js               # entry point, game loop
│   ├── pyexec.js             # Pyodide wrapper + validation
│   ├── editor.js             # CodeMirror setup
│   ├── encounter.js          # encounter loader and runner
│   ├── battle.js             # boss fight UI and animations
│   ├── effects.js            # particles, screen shake, floating numbers
│   └── state.js              # save/load, XP, progression
└── data/
    └── encounters/           # one JSON file per zone
        ├── zone1.json
        ├── zone2.json
        └── zone3.json
```

Do not create new top-level directories without updating this tree.

---

## Never Do This

- **Never introduce a framework** (React, Vue, Svelte, etc.) without explicit user approval.
- **Never add a build step.** No Vite, no Webpack, no bundler. Plain HTML + JS modules only.
- **Never add an npm dependency.** Everything third-party comes from a CDN URL.
- **Never simulate Python.** If the player writes something, it goes through Pyodide.
- **Never write text that breaks the fiction.** "You got the right answer!" is wrong. "The rune blazes — the path is open." is right.
- **Never ship an encounter that hasn't passed the four-question fun test.**
- **Never render text instantly for the Null Dragon.** His dialogue must always typewriter in, character by character — without sound, the typewriter effect *is* his voice.
- **Never commit secrets.** No API keys, no `.env` files. Always check `git status` before committing.

---

## Session Protocol

At the start of a session:
1. Read this file top to bottom.
2. Check **Current Phase** and **Next Task**.
3. Skim **Non-Negotiables** — they're the filter for every decision.
4. Pull up the reference docs as needed.

At the end of a session:
1. Update **Recently Shipped** with a dated line describing what landed.
2. Update **Next Task** to reflect the new front of work.
3. If **Current Phase** has changed, update it.
4. Run `git status`, review, commit, push.

---

## Reference Documents

- **`pyquest-build-plan.md`** — strategic plan. Vision, scope, phased build, hosting.
- **`pyquest-game-systems.md`** — encounter design, boss mechanics, scaffolding rules, time pressure. Pull up while designing any encounter.
- **`pyquest-content.md`** — all hand-written player-facing text: hints, NPC dialogue, boss monologues. Pull up when writing copy.

---

## Open Questions

*(Use this section to flag pending decisions. Clear entries when resolved.)*

- None currently.

---

*Last updated: project inception.*
