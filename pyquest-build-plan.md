# PyQuest — Build Plan (Simplified Submission Edition)

*A browser-based, gamified Python foundations experience. Three zones. No external services. Ship-ready in days, not months.*

---

## 1. The North Star

> **A complete non-programmer sits down, gets pulled in within 60 seconds, and finishes 3 zones having written real (if small) Python — without ever feeling like they were studying.**

If a decision doesn't serve this sentence, cut it.

---

## 2. Constraints (these define the project)

- **No external services.** No Anthropic API, no Cloudflare, no AWS, no accounts beyond GitHub.
- **No build step.** Open `index.html` in a browser, the game runs.
- **No npm, no node_modules.** Third-party libraries (Pyodide, CodeMirror) load from a CDN via `<script>` tags. From your perspective these are just URLs in your HTML — no installs, no dependency management.
- **Time-boxed.** A few days to ship. Cut anything that doesn't fit.

---

## 3. Scope — Three Zones

Cut from the original six. These three cover the most important Python foundations and provide a complete dramatic arc.

**Zone 1 — The Awakening Grove** *(print, variables)*
A fairy-tale forest. Cold open: dark room, pulsing rune, player clicks → a pre-filled `print("I am ___")` appears, they type their name, the room opens. ~5 encounters total. Ends with a small puzzle door (mini-boss).

**Zone 2 — The Skeleton King's Keep** *(for loops)*
Dark castle. The whole zone is about repetition. Multiple encounter types lead up to the Skeleton King boss — your flagship fight. Player writes scaffolded `for` loops to fire fireballs at the king across 3 phases. ~6 encounters + boss.

**Zone 3 — The Function Foundry** *(defining functions)*
A wizard's workshop. Player learns to define their own simple spells. ~4 encounters culminating in the Null Dragon final boss with pre-written cinematic dialogue. The dragon's lines are crafted, hand-tuned text — not API-generated, but still dramatic and memorable.

### What's deliberately cut from the original plan

- Zones 2, 3, 5 from the original (Arithmetic Caverns, Fork in the Road, Library of Collections)
- Tuples, dictionaries, conditionals, while loops, break/continue, exception handling
- All Claude API integrations
- Weapon and armor progression systems
- Adaptive difficulty / dynamic difficulty adjustment
- Code review feature
- Player-authored bosses
- Audio, voice, music
- Character classes and cosmetics
- Daily puzzles
- Achievement system

These were great ideas for a longer build. They'd sink you now. The three zones we kept demonstrate the core thesis of the game cleanly.

---

## 4. Tech Stack

**HTML + CSS + vanilla JavaScript.** No framework. No build step. No bundler.

**Pyodide via CDN.** One `<script>` tag in your HTML:
```html
<script src="https://cdn.jsdelivr.net/pyodide/v0.28.0/full/pyodide.js"></script>
```
This loads CPython compiled to WebAssembly. Players' code runs as real Python. No account, no API key, no service to manage.

**CodeMirror 6 via CDN.** Loaded the same way — a few `<script>` tags pointing at the CDN. Gives you a real syntax-highlighted code editor without installing anything.

**LocalStorage** for save state. Single JSON blob under key `pyquest.save`.

**No audio.** Visual feedback (screen shake, particle bursts, floating numbers, typewriter text, vignettes, flashes) carries all juice.

---

## 5. Hosting

**GitHub + GitHub Pages.** Both free, both included with a normal GitHub account.

The flow:
1. Push your code to GitHub
2. Go to repo Settings → Pages
3. Set source to `main` branch, root folder
4. Wait ~30 seconds, your game is live at `https://YOUR-USERNAME.github.io/pyquest/`
5. Every push automatically redeploys

That URL is what you submit to the hackathon. Anyone can play it instantly in their browser.

Set this up the same day you make the repo. Discovering a CORS or path issue at hour 60 is pain you don't need.

---

## 6. Game Design Pillars

Five rules that decide every detail.

**Scaffolding always.** Every encounter has pre-filled code with a small blank to fill. Players type one word, one number, one short expression. They never face an empty editor. They build typing muscle without facing the terror of starting from scratch.

**Feedback is instant and visible.** Every correct line of code triggers a particle effect, a number popping up, a flash, a bar filling. Action → visual payoff within 200ms.

**Failure is cheap.** No lives, no game over. Wrong answers are misfires that respawn instantly. Encourage experimentation.

**The story does the heavy lifting.** Players aren't learning `for` loops — they're learning the Spell of Repetition to damage the Skeleton King.

**Three zones, one arc.** Whimsical → tense → climactic. Tone deepens. By the Null Dragon, players feel they've earned their final spell.

---

## 7. The Core Loop

Three nested loops:

- **Second-to-second** — type into the scaffold, hit Cast, see an effect
- **Minute-to-minute** — clear an encounter
- **Zone-to-zone** — finish a zone (5–6 encounters + boss), see new content unlock

Total play time: **30–45 minutes** for the full three-zone arc. That's a complete experience that demos cleanly.

---

## 8. Phased Build Plan

### Phase 1 — Vertical Slice (target: ~1 day)

Single goal: make the Skeleton King fireball moment work end-to-end.

- `index.html` with Pyodide loading from CDN
- Run `print("hello")` from a textarea, output to a `<pre>`
- Add CodeMirror 6 (CDN) replacing the textarea
- Build the Skeleton King battle screen: two sprites (CSS), two HP bars (CSS), one editor, one timer, one prompt
- Wire submit code → validate → play animation → update HP
- One hardcoded encounter: the fireball-loop fight

**Exit criteria:** A non-programmer friend types into the scaffold, hits Cast, watches the boss take damage, smiles. You have a game.

### Phase 2 — Engine Generalization (target: ~1 day)

- Encounter JSON format: prompt, scaffold, validators, hints, success/fail copy
- Encounter loader: read JSON, render the right UI, run validators
- Three validation modes: `stdout_match`, `ast_check`, `combined`
- Save state in LocalStorage
- Zone navigation: complete an encounter → next encounter loads
- Visual juice library: screen shake, flash, particle burst, floating numbers, typewriter text — implemented once, reusable everywhere

### Phase 3 — Content Fill (target: ~1.5 days)

- Zone 1 fully built: 5 encounters + mini-boss
- Zone 2 fully built: 6 encounters + Skeleton King (already partially done from vertical slice)
- Zone 3 fully built: 4 encounters + Null Dragon
- All hand-written hints, dialogue, and flavor text from `pyquest-content.md`

### Phase 4 — Polish & Submission (target: ~half a day)

- Cold-open polish (the dark-room rune moment must land)
- Null Dragon typewriter dialogue is smooth
- One playthrough end-to-end on the deployed GitHub Pages URL in incognito
- README polished with what it is, how to play, link to live game
- Commit history is clean
- Submit

---

## 9. Visual Feedback Toolkit

Without audio, visuals carry everything. Implement these as reusable utilities once.

**Screen shake** on impact, damage, phase transitions. CSS keyframes triggered by class toggle.

**Flash overlay** on success, level up, spell cast. Full-screen color flash fading over 150ms.

**Floating numbers** for damage and XP. DOM element animating upward, fading out over 800ms. Single most important feedback element.

**Particle bursts** on spell impacts. Canvas-drawn particles expanding outward. 15–30 particles per burst, no assets needed.

**HP bar trail effect.** Two layered bars: foreground drops instantly, background lags by 300ms. Damage feels weighty.

**Typewriter text** for all dialogue, especially the Null Dragon. Characters appear one at a time at ~30 chars/second. Critical: this *is* the dragon's voice without sound.

**Camera zoom** on critical moments. `transform: scale(1.05)` for 200ms. Subtle but powerful.

**Vignette darkening** during boss encounters. Radial gradient overlay.

**Button press feedback.** `:active { transform: scale(0.95); }` on every interactive element.

If pressing Cast doesn't feel *satisfying*, fix that before anything else. Juice is the highest-leverage work in the game.

---

## 10. Risks and How to Avoid Them

**Risk: Pyodide boot is slow (2–5s first load).**
Mitigation: themed loading screen ("Consulting the ancient scrolls..."). Cold-open cinematic plays in parallel.

**Risk: Players get stuck and quit.**
Mitigation: Tiered hints. After 3 fails, more explicit hint surfaces automatically. After 5, "skip with partial XP" offered.

**Risk: Encounter validation is wrong and rejects correct answers.**
Mitigation: Test every encounter with 3 different correct solutions before considering it done.

**Risk: GitHub Pages serves stale or broken content the night of submission.**
Mitigation: Deploy to GitHub Pages on day one, push small changes throughout. Don't first-deploy on submission day.

**Risk: Scope creep into the cut zones (Conditionals! Lists! Dictionaries!).**
Mitigation: re-read this doc. Three zones. The cut content is post-submission work.

---

## 11. Submission Checklist

Night-before reality check:

- [ ] Public GitHub repo with all source code
- [ ] README explains what it is, how to play, links to live game URL
- [ ] License file (MIT)
- [ ] Game is live on GitHub Pages and tested in incognito browser
- [ ] No `.env`, no API keys, no secrets anywhere in repo
- [ ] All three zones playable end-to-end
- [ ] Cold open hits in under 60 seconds
- [ ] Skeleton King and Null Dragon both polished
- [ ] Demo video recorded (optional but nice — 2-3 min screen capture, music added in post)
