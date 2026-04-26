# PyQuest — Content (Hand-Written)

*All player-facing text. Hints, NPC dialogue, boss monologues. No API calls — every line below is hand-crafted and ships in JSON.*

---

## Voice Guide

**Read every line below imagining it spoken aloud by a wise, slightly mischievous mentor.** Not a teacher. Not a manual. Not a chirpy encouragement bot.

Bad: *"Incorrect! Remember, a `for` loop uses the keyword `for` followed by a variable."*
Better: *"The spell fizzled. Did you remember to begin with the word of repetition?"*

Bad: *"Great job! You successfully used a for loop."*
Better: *"The skeletons crumble. The Spell of Repetition settles into your bones — it is yours now."*

### Forbidden words (never appear in any player-facing text)

- "Python", "code", "programming"
- "function", "variable", "loop", "string", "integer"
- "syntax error", "bug", "compile"
- "correct" / "incorrect"
- "you got it!" / "good job!"

### Translations (use these instead)

- variable → rune, name, vessel
- function → spell, forged spell
- for loop → spell of repetition
- string → words of power, inscription
- print → speak, sound, voice
- error → fizzle, misspoken incantation
- run/execute → cast
- correct → "the magic holds"
- incorrect → "the spell fizzled"

---

## Cold Open (the first 60 seconds)

When the page loads, **before** any UI appears:

```
[black screen, faint pulse of red light]

A whisper, then silence.

Magic is fading from the world.
The spells have been stolen.
Names have lost their power.
And in the ash of the old age,
one rune still glows.

You see it now, on the floor before you.
Step forward. Touch it.
Speak.
```

Then the rune fades into view, the editor scaffold appears with `print("___")`, and the game begins.

---

## Zone 1 — The Awakening Grove

### Encounter 1: The Speaking Rune

**Story:** *"A rune pulses on the floor of the dark room. It seems to want a name."*

**Prompt:** *"Speak your name into the rune."*

**Hints:**
1. *"The rune waits between the marks of speaking. Place a name there."*
2. *"Anything written between the two curves will be spoken. Try your name."*
3. *"Type your name between the quotation marks. Then press Cast."*

**On success:** *"The rune blazes. The path opens. You hear, faintly, the world remembering."*

**On fail (rare — this one is nearly impossible to fail):** *"The rune flickers, uncertain. Try again."*

### Encounter 2: The Echo Sprite

**Story:** *"A small light flickers in the trees. It mimics whatever sound you make."*

**Prompt:** *"Make the sprite say `hello`."*

**Hints:**
1. *"The sprite repeats what you speak. Speak the word `hello`."*
2. *"Inside the marks of speaking, write the word the sprite should echo."*
3. *"Type `hello` between the quotation marks, then Cast."*

**On success:** *"The sprite chirps your word back at you and giggles."*

### Encounter 3: The Naming Spell

**Story:** *"An old badger sits on a rock, lost. He has forgotten his own name. You may give him one."*

**Prompt:** *"Bind a name to the badger using a rune, then speak it back."*

**Hints:**
1. *"First, write the name you wish to give him into the rune `name`. Then speak the rune."*
2. *"The line `name = \"___\"` binds your chosen name into the rune called `name`. The next line speaks whatever the rune holds."*
3. *"Type a name between the quotation marks on the first line. Press Cast."*

**On success:** *"The badger raises his head. He says the name back to you, slowly. He smiles."*

### Encounter 4: The Number Rune

**Story:** *"A merchant offers a satchel of gold coins. He wants to know how many you'll take."*

**Prompt:** *"Bind a number of coins to the rune `gold`, then speak it."*

**Hints:**
1. *"Runes can hold numbers, not only words. The numbers go without quotation marks."*
2. *"Replace the blank with any number — say, 7 — and press Cast."*
3. *"Type a number, like `7`, where the blank is. No quotes for numbers."*

**On success:** *"The merchant counts the coins onto his palm and grunts approvingly."*

### Encounter 5 — Mini-boss: The Echoing Door

**Story:** *"A great stone door blocks the path. Carved into its surface: 'I open only to those who can speak the word twice.'"*

**Prompt:** *"Bind a greeting to a rune, then speak it twice."*

**Hints:**
1. *"Bind your greeting into the rune `greeting`. Then speak the rune. Then speak it again."*
2. *"You will need three lines. Two of them are already there. Fill the blank in the first line."*
3. *"Type any greeting in the quotation marks on the first line. Press Cast."*

**On success:** *"The door rumbles. Then, slowly, it splits down the middle. Beyond it, a darker corridor stretches into shadow."*

---

## Transition: Grove → Keep

```
[the screen darkens slowly]

You walk a long while.
The trees thin. The earth grows cold.
A castle of black stone rises from the mist.

Inside, something old is waking.
```

---

## Zone 2 — The Skeleton King's Keep

### Encounter 1: The First Strike

**Story:** *"Three skeletons rise from the floor. They will fall to a single repeated strike."*

**Prompt:** *"Cast the Spell of Repetition: speak `strike` three times."*

**Hints:**
1. *"The Spell of Repetition begins with the word `for` and ends with a colon. Tell it how many times to repeat."*
2. *"`range(3)` will cause the spell to cast three times. Place a 3 inside the range."*
3. *"Type `3` in the blank inside `range()`. Press Cast."*

**On success:** *"Three skeletons. Three strikes. Three falls."*

### Encounter 2: The Skeleton Pair

**Story:** *"Two armored skeletons step forward. They do not fall to bare hands. Speak the word that breaks them."*

**Prompt:** *"Cast a repetition that speaks `crack` twice."*

**Hints:**
1. *"The repetition is set for two casts. You need only choose the word."*
2. *"Type `crack` between the quotation marks."*
3. *"Type `crack` (without the quotes — the quotes are already there)."*

**On success:** *"Two cracks. Two armors broken. The skeletons crumble."*

### Encounter 3: The Counting Hall

**Story:** *"A long hall stretches before you. Numbered torches line the walls, but they are unlit. Speak each number, and they will ignite."*

**Prompt:** *"Speak the numbers from 0 to 4."*

**Hints:**
1. *"`range(5)` produces the numbers 0, 1, 2, 3, 4 — five numbers in all. Place 5 in the range."*
2. *"`for i in range(5):` will let `i` take each of those five numbers in turn. Speak `i` inside the spell."*
3. *"Put 5 in the range. Press Cast."*

**On success:** *"Five torches. Five numbers spoken. The hall blazes with light."*

### Encounter 4: The Bone Chant

**Story:** *"Skeletal voices rise from the walls. They will not stop until you join their chant — three times."*

**Prompt:** *"Speak any single word, three times in repetition."*

**Hints:**
1. *"Choose any word — a name, a curse, a song. Speak it three times in the spell."*
2. *"Type any word in the quotation marks. The repetition is already set to three."*
3. *"Type any word — like `peace` or `gold` — in the blank."*

**On success:** *"The skeletal voices fade, soothed by your chant."*

### Encounter 5: The Phantom Volley

**Story:** *"A wraith hovers at the corridor's end. Five strikes will banish it."*

**Prompt:** *"Cast a repetition that speaks any battle word, five times."*

**Hints:**
1. *"Set the range to 5. Choose any word as your strike."*
2. *"Place a 5 in `range()` and any word in the quotation marks."*
3. *"`5` in the range. Any word in the blank. Press Cast."*

**On success:** *"Five blows. The wraith dissipates."*

### Encounter 6: The Echo Crypt

**Story:** *"In a chamber of obsidian, your voice echoes back to you. The room demands a chosen word, repeated thrice."*

**Prompt:** *"Bind a word to a rune, then speak the rune three times."*

**Hints:**
1. *"First bind your word into the rune `word`. Then a repetition of three speaks it."*
2. *"Replace the blank with any word."*
3. *"Type any word between the quotation marks. Press Cast."*

**On success:** *"The chamber drinks your voice and falls silent."*

### BOSS — The Skeleton King

#### King's intro (typewritered in slowly when he appears)

```
THE SKELETON KING:
"Another fool seeks the throne.

Another body for my floor.

Cast your little spells, child.
I have buried wiser than you."
```

#### Phase 1 — The Horde

**Prompt:** *"His five guardians charge. Strike each with the Spell of Repetition."*

**Hints:**
1. *"Five guardians. Five strikes. Set the range, then speak the strike-word."*
2. *"`range(5)` for five repetitions. `strike` for the word."*
3. *"5 in the range. `strike` between the quotes."*

**On success:** *"Five strikes. Five guardians fall. The Skeleton King draws his blade."*

#### Phase 2 — The Armor

**King's taunt:** *"Steel is not so easily broken, child."*

**Prompt:** *"His armor cracks under repeated blows. Speak `crack` three times."*

**Hints:**
1. *"Three cracks. Set the range, speak the word."*
2. *"3 in the range, `crack` in the blank."*
3. *"Type 3 and `crack`. Press Cast."*

**On success:** *"The armor splits. The Skeleton King recoils, exposed."*

#### Phase 3 — The Fall

**King's last words (before the fight):** *"Then strike, child. Strike and end this."*

**Prompt:** *"Seven strikes. Choose your final word."*

**Hints:**
1. *"Seven repetitions are already set. Choose the word that ends this fight."*
2. *"Any word will do. Make it one you will remember."*
3. *"Type any word in the blank. Press Cast."*

**On success — King's death cinematic:**

```
THE SKELETON KING:
"Ah... so this is how it ends...

I yield, child.
I yield to the spells of one I should have feared.

Take... the corridor... the throne... the dust...

Take it all..."

[King crumbles. Throne collapses behind him.]
[Vignette darkens. White flash. Zone complete.]
```

---

## Transition: Keep → Foundry

```
[a long walk through ash and silence]

The throne is dust now.
But behind it, a doorway you did not see before.
Stairs leading down.
And, far below — a forge,
its fire burning blue and cold.

Something is being made there.
Or something is waiting to make you.
```

---

## Zone 3 — The Function Foundry

### Encounter 1: The First Forge

**Story:** *"An ancient forge glows blue. The hammer waits. To craft your first true spell — to *forge* it, not merely cast it — you must give it a name and a shape."*

**Prompt:** *"Forge a spell that returns any word of power."*

**Hints:**
1. *"A forged spell is named with `def`. It gives back what it returns. Place a word in the blank."*
2. *"Anything between the quotation marks will be the spell's gift. Choose a word."*
3. *"Type any word in the blank. Press Cast."*

**On success:** *"You strike the hammer once. The spell takes shape — small, bright, and yours."*

### Encounter 2: The Named Spell

**Story:** *"A friendlier spell waits at the forge — one that greets whoever it is given. You must give it the name to greet."*

**Prompt:** *"The spell is forged. Choose whom it greets."*

**Hints:**
1. *"The spell `greet` takes any name and returns a greeting. Give it a name."*
2. *"Place a name in the blank — your own, perhaps."*
3. *"Type any name in the blank between quotation marks. Press Cast."*

**On success:** *"The spell speaks. The forge approves."*

### Encounter 3: The Twin Spells

**Story:** *"Two spells lie unfinished on the anvil — `fire` and `ice`. They wait to be cast in order."*

**Prompt:** *"Cast both spells. Speak each in turn."*

**Hints:**
1. *"Both spells are forged. The bottom two lines speak them. Press Cast."*
2. *"Nothing to fill — just press Cast and let the spells speak."*
3. *"Press Cast. The spells are ready."*

**On success:** *"Fire. Ice. The forge sings with both elements at once."*

### Encounter 4: The Composing

**Story:** *"The deepest craft of forging: a spell that uses another spell within it. The mark of a true caster."*

**Prompt:** *"Forge `power` to return a word of force. The greater spell will weave it inward."*

**Hints:**
1. *"`power` returns a word; `cast_spell` weaves that word into a larger phrase."*
2. *"Choose any word for `power`. Any force you can name."*
3. *"Type any word in the blank — `lightning`, `flame`, `frost`. Press Cast."*

**On success:** *"One spell within another. The forge grows still — it has nothing more to teach you."*

---

## BOSS — The Null Dragon

The dragon's dialogue is the demo moment of the game. **Every line typewriters in character by character at ~30 chars/second.** The slow reveal *is* his voice.

### Dragon's first appearance (long monologue, slow)

```
A shape unfolds from the dark.
Vast. Indifferent. Old.

THE NULL DRAGON:
"So.

Another forger. Another small,
bright will, come to take back
what I devoured.

I have eaten every spell
this world ever knew.
I have hollowed out the very word
for *return*.

Show me what scraps you've forged in my absence.
Show me, and I will show you why
no one returns from this hall."
```

### Phase 1 — The Awakening

**Prompt:** *"Forge any spell that returns a word."*

**Dragon's challenge:** *"Begin, then. Forge me one true spell. I will see how you have learned."*

**Hints:**
1. *"A spell needs a name (`def attack():`), and it must return something. Place a word in the blank."*
2. *"Anything between the quotation marks will be returned. Choose any word."*
3. *"Type any word in the blank. Press Cast."*

**On success:**
*"Hm. So. The last of your kind still remembers how to forge. Your spell is small — but it returns what it promised. That is more than many before you could say."*

**On failure:**
*"You gathered the runes but did not speak them aright. A forging without its proper shape is only an intention. Try again — and this time, leave the structure as it stands."*

### Phase 2 — The Mutation

**Dragon transitions:** *"A small spell. Now I will see if you can shape one to take an offering."*

**Prompt:** *"Forge a spell that uses what is given to it."*

**Hints:**
1. *"The spell takes `power` as its offering. Place `power` after the plus sign — without quotes — so the spell uses the offering itself."*
2. *"After `\"Strike of \" + ` write `power` (no quotes). The offering is a rune, not a word."*
3. *"Type `power` (no quotes) in the blank."*

**On success:**
*"You shape the offering and the spell accepts it. A small craft, and yet — deftly done. I begin to see why you were sent to me."*

**On failure:**
*"You filled the vessel with the wrong substance. The offering is not a word in quotation marks — it is the rune itself. Try again."*

### Phase 3 — The Composition

**Dragon's roar:** *"Now — the true craft. Two spells, one woven into the other. Show me you understand the deeper forging."*

**Prompt:** *"Forge `ember` to return any word. The greater spell will repeat it."*

**Hints:**
1. *"`ember` returns a word. `inferno` calls `ember` twice. Choose your word."*
2. *"Place any word — `flame`, `rage`, `light` — in the blank."*
3. *"Type any word between the quotation marks. Press Cast."*

**On success:**
*"One spell calling another... a weave I have not seen in this age. It is beautiful. It will not save me — but it is beautiful."*

**On failure:**
*"The outer spell reaches for its companion — and grasps nothing. You have left the heart of it empty. Place a word in the heart, and try again."*

### Phase 4 — The Restoration (no timer — let them breathe)

**Dragon, weakened, wounded, almost respectful:**

```
THE NULL DRAGON:
"Enough.

You have shown me the craft. I see now
what you are, and what I was.

Here is the last spell. The one I tried
to consume and could not. Restore it,
forger, and the world is yours again."
```

**Prompt:** *"Forge the spell of restoration. Any return. Any word. Make it yours."*

**Hints:**
1. *"Any word will do. The dragon waits. Place a word in the blank."*
2. *"It does not matter which word — the dragon honors the *making*, not the choice."*
3. *"Type any word — even a single letter. Press Cast."*

**On success — final cinematic, very slow typewriter:**

```
THE NULL DRAGON:
"So.

A true forging, at the last.

Take it, then.
Take the light back, and the word,
and the craft of it.

I was a good thief.
You will be a better maker.

Go."

[The dragon dissolves slowly into light.]
[The screen fills with white.]
[Long pause.]
[Text fades in:]

You stand alone in the forge.
Your spells are your own.

The world begins to remember.

You have completed PyQuest.
```

---

## Generic Hint Voices (for catchall situations)

If an encounter throws a Python error not anticipated by the encounter's hint list, fall back to one of these generic mentor lines:

- *"The spell fizzled. Look closely at your runes — one of them is misshapen."*
- *"Something in the cast went amiss. Try again, slower this time."*
- *"The magic flickered and went out. Begin once more."*
- *"Your spell wavered at the threshold. Check the marks of speaking — the curves and the points."*
- *"Almost. The shape was right, but a detail betrayed you. Try again."*

Pick one at random when you don't have a specific hint.

---

## Final Credits Screen

```
PYQUEST

You came as a stranger.
You leave as a maker.

The spells you cast here
will work in any forge
in any world.

Real Python. Real magic.
That was always the secret.

Built for the Claude hackathon.
Made with care.
```
