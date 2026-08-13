# The Clockwork House — Pass 2 Prompt for Code

## Context

The Clockwork House is a 200-room single-file HTML text adventure at `index.html`. It's been through two blind playtests via a headless harness. Both resulted in perfect runs (0 wrong turns, 0 hints). Current difficulty rating: 4/10. Target: 6-7/10 for an LLM, 7-8/10 for a human software engineer.

The writing quality is strong. The voice (CS-major-turned-venue-systems-architect, 10% Adams, 10% Anthony) is dialed in. This pass is about difficulty tuning, structural fixes, and polishing the rooms that don't hit as hard as the best ones. Do NOT flatten the voice or reduce the personality. The goal is harder puzzles, not worse writing.

## Structural Fixes (do these first)

### 1. Path enforcement bug
Room 6 is directly reachable from Room 37, allowing players to skip Room 91 entirely (37→6 instead of 37→91→6). The true path is `...37 → 91 → 6 → 128...` and all 20 rooms should be required.

**Fix:** Remove Room 6 as a direct exit from Room 37. The glass corridor should show the ballroom below but not offer a direct route — you have to go through 91 first. Alternatively, gate Room 6's correct exit (128) behind information that's only available in Room 91, so even if someone reaches 6 early, they can't solve it without visiting 91.

### 2. Room 1's "91 is not prime" callback is too strong
The cross-room clue planted in Room 1 ("91 is not prime — remember this when the glass lies") was designed to create tension at Room 37. Instead, it convinced a blind playtester to skip Room 91 entirely. The clue should make Room 37 *harder*, not make Room 91 *avoidable*.

**Fix:** Reframe the Room 1 clue. Instead of warning about 91 as a destination, warn about the *sign* in Room 37 that lies. Something like: "Not every sign tells the truth. When glass sings a number, check whether it's prime." This creates suspicion at Room 37 without telling you what to do about it. The player should still need to visit 91 to proceed — the warning just means they arrive suspicious, not that they skip it.

### 3. "Three-eighths of the time the hour lies" — loose thread
This clue is planted in Room 1 but never pays off anywhere. Either wire it into a puzzle (e.g., Room 8 has 8 clock mechanisms, 3 of which show wrong times) or remove it. Chekhov's guns that don't fire erode trust in the clue system.

## Difficulty Fixes

### 4. Rooms that are too direct (flagged by both playtests)

**Room 33 (Taxidermist's Workshop):** The taxidermist's note just says "the 20th is in room 20." That's a sign, not a puzzle. The number 20 should be encoded — maybe the taxidermist has preserved exactly 19 animals, and the workbench has materials laid out for a 20th. The HashMap can stay but shouldn't literally say `key: 20, value: "go to room 20"`. Make the player assemble the answer.

**Room 77 (Sorting Chamber):** Bogosort producing 45 is arbitrary — there's no discoverable logic connecting 77 or bogosort to the number 45. Give it a reason. Maybe the sort is running on an array where the 45th element is the only one in its correct position. Or the bogosort has been running for 45 hours. Something that makes 45 *derivable*, not just *stated*.

**Room 45 (The Threshold):** "13 squared = 169" is stated too directly. Encode it. Maybe the tally marks on the walls: 13 rows of 13 marks each. Or the living door has 13 branches, each with 13 leaves. Let the player do the multiplication.

### 5. The "loudest signal" problem
Across both playtests, the correct exit was always the most prominent clue in the room. The agent described it as "the loudest signal always wins." In at least 3-4 true-path rooms, the correct answer should NOT be the most prominent element. It should be the quietest — buried in a detail, a secondary paragraph, a throwaway line. The loud clue should point somewhere wrong. Force the player to read carefully, not just scan for emphasis.

Candidates for this treatment: Rooms 16, 42, 127, 144 — these are mid-path rooms where a wrong turn is recoverable, so the risk is acceptable.

### 6. False path needs to be indistinguishable from true path
Both playtesters avoided Rooms 110-117 entirely. The entrance in Room 20 is labeled "Shortcut (beta)" — any engineer reads that as "do not use."

**Fix:** Remove all warning language from the false path entrance. In Room 20, the exit to 110 should look exactly like the exit to 42 — same tone, same confidence, same level of supporting evidence. The false path should feel like a legitimate branch that happens to be wrong. The "beta" label, the "DO NOT SHIP" annotation — all of that has to go. The player should enter the false path because it *genuinely looks correct*, not despite warnings.

### 7. Add one room with genuinely competing clues
Somewhere on the true path (ideally in the back half, rooms 91-169), add or rewrite a room where two exits have equally strong, equally valid-looking evidence supporting them. Not "obvious answer vs. clearly-wrong trap" but a genuine coin flip between two plausible answers. One is wrong. This is the single change most likely to cause a wrong turn.

## Voice/Writing Polish

### 8. Late-game recovery rooms (130-168) need more personality
Both playtests flagged these as flatter than the first 50 rooms. The early rooms have specific characters (the sommelier in 9, the laundress in 14, the sentient typewriter in 29). The late-game recovery rooms tend to be 1:1 CS-concept-to-room translations without the weird specificity that makes the best rooms memorable.

Pick the 5-6 weakest rooms in the 130-168 range and give them the same treatment as the best rooms: a specific character, a specific absurd detail, a specific voice. The bar is Room 10's "Escalated to God. God closed the ticket." and Room 53's daemon with "the thousand-yard stare of a process that has never been restarted."

### 9. Xanth rooms (95, 125, 159, 160) — tighten the systems-architect frame
These rooms were flagged as breaking the voice by dipping into straight fantasy. The Pun Compiler rewrite (95) improved this — extend the same approach to the remaining Xanth/Incarnations rooms. Every Anthony reference should be viewed through the lens of someone who's spent 20 years in production environments. Death isn't a robed figure — Death is the process that kills your containers at 3 AM. Fate isn't weaving a tapestry — Fate is the dependency graph you can't refactor.

## Validation

After all changes:
1. Run the syntax/path validator to confirm all 200 rooms present, all exits valid, true path intact, Room 200 has victory:true
2. Regenerate the harness module from the updated source
3. Run a fresh blind playtest from a clean agent session using the harness — agent must interact via `node /tmp/clockwork_harness.js` commands only, no source access
4. Target: at least 1 wrong turn, at least 1 hint used, difficulty rating 6+/10
