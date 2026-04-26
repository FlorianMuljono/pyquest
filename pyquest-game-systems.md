# PyQuest — Game Systems Reference

*Companion to the build plan. Encounter design, validation, scaffolding rules, boss mechanics, time pressure. Pull this up when designing or implementing any encounter.*

---

## The Core Principle

Every game mechanic *is* a Python concept. The fireball isn't called "For Loop Fireball" as decoration — **firing it requires the player to fill a working `for` loop scaffold.** Owning a spell = having that Python construct in their toolkit. Casting it = correctly completing the scaffold.

If you can strip the Python out of a mechanic and it still works, the integration isn't deep enough.

---

## 1. Encounter Anatomy

Every encounter is a JSON object. The engine reads it, renders the UI, runs validation, and reacts.

```json
{
  "id": "grove-001",
  "zone": 1,
  "title": "The Speaking Rune",
  "story": "A rune pulses on the floor. It seems to want a name.",
  "prompt": "Speak your name into the rune.",
  "scaffold": "print(\"___\")",
  "blanks": [{"id": "name", "placeholder": "Your name"}],
  "validators": [
    {"type": "ran_without_error"}
  ],
  "timer": 0,
  "hints": [
    "Type any name into the blank, then press Cast.",
    "The blank is between the quotes. Anything you type there will be spoken.",
    "Try typing your own name into the blank. Then press Cast."
  ],
  "on_success": {
    "narration": "The rune blazes. The path opens.",
    "xp": 10
  },
  "on_fail": {
    "narration": "The rune flickers, uncertain. Try again.",
    "hp_cost": 0
  }
}
```

### Validator types

**`ran_without_error`** — most permissive. Used in Zone 1. Player wins if their code runs without throwing.

**`stdout_match`** — code's printed output must match the expected string exactly.

**`stdout_contains`** — output must contain a substring. Used when the player's name is part of the expected output.

**`ast_check`** — parse the player's code, verify required constructs are present. Example: `{"type": "ast_check", "must_contain": ["For"]}` requires a `for` loop. Prevents hardcoded cheating.

**`combined`** — multiple validators that all must pass. Most boss encounters use this: AST check + stdout match.

### Scaffolding rules

The `scaffold` field shows the player code with `___` markers where they fill in. The UI renders these as inline editable spans, not free-form editor text. This is critical — beginners can't mess up indentation or punctuation when they only type into a single span.

For Zone 3 encounters and bosses, the scaffold can include multiple lines and multiple blanks. The Null Dragon's final phase has a 4-line scaffold with 2 blanks.

### Timer

`timer: 0` means no time pressure. Used for all of Zone 1.

`timer: N` means N seconds. Used in Zone 2+ for combat encounters. **The timer never causes game over** — when it hits zero, the boss gets a free attack and the timer resets. The player keeps going.

---

## 2. Zone-by-Zone Encounter Specs

### Zone 1 — The Awakening Grove (5 encounters + 1 mini-boss)

**Theme:** Fairy-tale forest. Whimsical. No timers. Pure confidence-building.

**Concepts:** `print()`, variables.

| # | Title | Concept | Scaffold | Validator |
|---|-------|---------|----------|-----------|
| 1 | The Speaking Rune | print + your name | `print("___")` | `ran_without_error` |
| 2 | The Echo Sprite | print a phrase | `print("___")` | `stdout_contains: "hello"` |
| 3 | The Naming Spell | variable assignment | `name = "___"\nprint(name)` | `ast_check: Assign` + `stdout_match` |
| 4 | The Number Rune | numeric variable | `gold = ___\nprint(gold)` | `ast_check: Assign` |
| 5 | The Echoing Door (mini-boss) | combine print + variable | `greeting = "___"\nprint(greeting)\nprint(greeting)` | `stdout_contains` matches their input twice |

**Mini-boss vibe:** A stone door asks "What do you say to me?" The player sets a greeting and prints it twice ("the door wants to hear it again, to be sure"). Door cracks open with a particle burst.

### Zone 2 — The Skeleton King's Keep (6 encounters + boss)

**Theme:** Dark castle. Tense. Timers introduced (generous). Loops are repetition spells.

**Concepts:** `for` loops, `range()`.

| # | Title | Concept | Scaffold | Timer |
|---|-------|---------|----------|-------|
| 1 | The First Strike | basic for loop | `for i in range(___):\n    print("strike")` | 60s |
| 2 | The Skeleton Pair | range with specific count | `for i in range(2):\n    print("___")` | 60s |
| 3 | The Counting Hall | iterate and print i | `for i in range(___):\n    print(i)` | 60s |
| 4 | The Bone Chant | string in loop | `for i in range(3):\n    print("___")` | 50s |
| 5 | The Phantom Volley | 5-strike combo | `for i in range(___):\n    print("___")` | 45s |
| 6 | The Echo Crypt | nested string + loop | `word = "___"\nfor i in range(3):\n    print(word)` | 45s |
| **BOSS** | **The Skeleton King** | 3-phase loop fight | (see below) | per phase |

#### Skeleton King boss design

**Phase 1 — The Horde** (45s)
- Setup: 5 skeletons march toward player. King watches, arms folded.
- Scaffold: `for i in range(___):\n    print("strike")`
- Required: print "strike" 5 times.
- Validators: `ast_check: For` + `stdout_match: "strike\nstrike\nstrike\nstrike\nstrike"`
- Success animation: fireball arcs from player → impact at each line of output → 5 skeletons fall in sequence.

**Phase 2 — The Armor** (60s)
- Setup: King raises a shield. Floating armor counter visible: `armor = 3`.
- Scaffold: `for i in range(___):\n    print("crack")`
- Required: 3 cracks.
- Validators: `stdout_match: "crack\ncrack\ncrack"`
- Success animation: armor visibly shatters per line.

**Phase 3 — The Fall** (75s)
- Setup: King exposed, low HP, raging.
- Scaffold: `for i in range(7):\n    print("___")`
- Required: any non-empty word in the blank, prints 7 times.
- Validators: `ast_check: For` + count of stdout lines = 7
- Success animation: 7 fireballs in rapid succession, screen shake on each, king collapses with vignette closing in.

After defeat: cinematic of the king fading into ash, the throne crumbling. XP burst. "Zone 2 Cleared" + cliffhanger text: *"From the ash, a deeper darkness rises..."*

### Zone 3 — The Function Foundry (4 encounters + Null Dragon)

**Theme:** Wizard's workshop, then an obsidian arena for the dragon. Climactic. Tense.

**Concepts:** `def`, parameters, return values.

| # | Title | Concept | Scaffold | Timer |
|---|-------|---------|----------|-------|
| 1 | The First Forge | define and call | `def cast():\n    return "___"\nprint(cast())` | 75s |
| 2 | The Named Spell | function with parameter | `def greet(name):\n    return "Hello " + name\nprint(greet("___"))` | 75s |
| 3 | The Twin Spells | two functions | `def fire():\n    return "fire"\ndef ice():\n    return "ice"\nprint(fire())\nprint(ice())` | 60s |
| 4 | The Composing | calling one function in another | `def power():\n    return "lightning"\ndef cast_spell():\n    return "I cast " + power()\nprint(cast_spell())` | 60s |
| **BOSS** | **The Null Dragon** | 4-phase function fight | (see below) | per phase |

#### Null Dragon boss design

**The dragon's dialogue is pre-written, hand-crafted, and typewriters in character by character.** No API calls. Each phase has 2-3 dialogue states (intro, success, failure) — see `pyquest-content.md` for the actual lines.

**Phase 1 — The Awakening** (90s)
- Dragon emerges, monologues about consuming all spells from the world.
- Scaffold: `def attack():\n    return "___"`
- Required: any non-empty string returned.
- Validator: `ast_check: FunctionDef` + `ast_check: Return`

**Phase 2 — The Mutation** (90s)
- Dragon shifts form. Demands a more powerful spell.
- Scaffold: `def attack(power):\n    return "Strike of " + ___`
- Required: use the parameter `power` in the return.
- Validator: `ast_check: FunctionDef` + the function, when called with test input, must include that input in output.

**Phase 3 — The Composition** (90s)
- Dragon roars; the air ripples.
- Scaffold:
```
def ember():
    return "___"
def inferno():
    return ember() + " " + ember()
print(inferno())
```
- Required: fill the ember return; inferno already defined to call ember twice.
- Validator: `stdout` must show the ember word repeated.

**Phase 4 — The Restoration** (no timer — let them breathe)
- Dragon, weakened, offers his final challenge: complete the broken spell that will restore magic to the world.
- Scaffold:
```
def restore():
    return "___"
print(restore())
```
- Required: any non-empty return. The dragon accepts.
- Validator: `ast_check: FunctionDef` + `ran_without_error`
- On success: extended cinematic, dragon's final monologue typewriters in slowly, screen fills with light, credits.

---

## 3. Visual Juice — When Each Effect Fires

| Event | Effect |
|-------|--------|
| Player types a character | Subtle cursor pulse |
| Player presses Cast | Editor border glows briefly |
| Code runs, validation passes | Screen flash (white) + camera zoom + particle burst at boss |
| Code runs, syntax error | Editor shake + smoke puff + hint surfaces |
| Code runs, wrong output | Boss looks unimpressed, no damage, gentle hint |
| Boss takes damage | HP bar drops (front instant, back delayed) + floating damage number + screen shake |
| Boss attacks (timer expired) | Red flash + screen shake + player HP drops |
| Boss phase change | Camera zoom + vignette tightens + boss sprite changes pose |
| Boss defeated | Slow zoom on collapse + particle storm + "Victory" text typewrites in |
| Encounter complete | XP number floats up + transition to next |
| Zone complete | Cinematic transition (5s) + cliffhanger text + "save" indicator |

---

## 4. Difficulty and Hint System

### The hint ladder

Every encounter has 3 hints. They surface automatically:
- After failure 1: nothing yet (silent — let them try again)
- After failure 2: hint level 1 appears (oblique)
- After failure 3: hint level 2 appears (more direct)
- After failure 5: hint level 3 appears (explicit, almost gives the answer)
- After failure 7: "skip this for now" option appears (offers partial XP, moves on)

Hints fade in below the editor. They never interrupt or block. They never lecture — they're in the Owl Sage's voice. See `pyquest-content.md` for hint content.

### Difficulty levers

The encounter JSON exposes these for tuning:

- `timer` — generous (60s+) early, tighter (30-45s) later
- `scaffold` density — more pre-filled = easier
- `validators` strictness — `ran_without_error` is loose, `stdout_match` is tight
- `hints` quality and explicitness

### The fun test (every encounter must pass before shipping)

1. **Comprehensibility** — does a non-programmer understand what to do within 10 seconds?
2. **Payoff** — when they solve it, does something visibly cool happen?
3. **Retry pull** — when they fail, do they want to try again?
4. **Re-play interest** — would it still be fun if they'd aced it first try?

Fail any one, fix it. Fail two, redesign.

---

## 5. Time Pressure Rules

1. **No timer in tutorials.** Zone 1 has no timers at all.
2. **Generous timers when concepts first appear.** First `for` encounter: 60s.
3. **Timers never cause game over.** Zero = boss free hit + reset, player keeps going.
4. **Bonus XP for speed, never penalty for slowness.**

### Timer visual states

- **Green (full)** — calm
- **Yellow (50%)** — timer bar pulses subtly
- **Red (25%)** — vignette darkens edges, pulse faster
- **Zero** — enemy strikes, timer resets

---

## 6. Save State

Single LocalStorage key: `pyquest.save`. JSON shape:

```json
{
  "version": 1,
  "zone": 2,
  "encounter": 3,
  "xp": 145,
  "level": 4,
  "completed_encounters": ["grove-001", "grove-002", "..."],
  "history": {
    "total_play_time_seconds": 1820,
    "encounters_completed": 12,
    "bosses_defeated": 1
  }
}
```

Auto-save before every encounter. Player never loses progress.

---

## 7. Implementation Notes

### Pyodide validation pattern

```javascript
async function validateEncounter(playerCode, validators) {
  for (const v of validators) {
    if (v.type === 'ran_without_error') {
      try { await pyodide.runPython(playerCode); }
      catch (e) { return { ok: false, error: e.message }; }
    }
    if (v.type === 'stdout_match') {
      const out = await runAndCapture(playerCode);
      if (out.trim() !== v.expected.trim()) {
        return { ok: false, error: 'output mismatch' };
      }
    }
    if (v.type === 'ast_check') {
      const tree = await pyodide.runPython(`
        import ast
        ast.parse(${JSON.stringify(playerCode)})
      `);
      // walk tree, verify v.must_contain nodes exist
    }
  }
  return { ok: true };
}
```

Wrap stdout capture by redirecting Pyodide's `sys.stdout` to a Python `io.StringIO`, then reading it back. Reset between runs.

### Scaffold rendering

Render the scaffold as text with `___` markers replaced by `<input class="blank" data-blank-id="...">`. On Cast, splice the player's input values back into the scaffold to produce the full code, then send that to Pyodide.

This is the simplest path. CodeMirror is overkill for blank-only inputs — use plain inputs in the scaffold view, save CodeMirror for the optional "advanced mode" that's out of scope for now.

**Reconsider:** Actually, even simpler — just one fixed-width font textarea per encounter, pre-filled with the scaffold text including the `___` markers. Player edits in place. Simple, robust, scales fine. CodeMirror only matters for the Null Dragon Phase 4 where they're staring at multi-line code and want syntax highlighting for confidence.

Decide later. Start with textarea. If it feels rough, add CodeMirror to bosses only.
