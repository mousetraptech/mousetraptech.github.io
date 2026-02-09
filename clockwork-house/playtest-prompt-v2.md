# The Clockwork House — Blind Playtest v2

## Critical Constraint

This game is played through a **headless test harness**. You interact with it by running commands. You will see ONE ROOM AT A TIME — the description and exits, nothing more.

**You do not have access to the game's source code. You have not read any HTML, JavaScript, or data files. You have no knowledge of the game's internal structure.**

Your ONLY sources of information are:

1. The room description currently displayed by the harness
2. The exit list currently displayed by the harness
3. The hint for the current room (if you request it)
4. **Your own memory of rooms you have already visited during this session**

That last point is key. Some puzzles may require you to remember details from earlier rooms. Keep a mental note of anything that seems like it might matter later — numbers, warnings, patterns, recurring references.

## How to Interact with the Harness

```bash
node /tmp/clockwork_harness.js restart    # Start a new game
node /tmp/clockwork_harness.js look       # See current room again
node /tmp/clockwork_harness.js go <N>     # Go to room N (must be a valid exit)
node /tmp/clockwork_harness.js hint       # Get a hint for current room
node /tmp/clockwork_harness.js back       # Go back one room
node /tmp/clockwork_harness.js status     # See your stats
```

## How to Play

1. Run `restart` to begin. Read Room 1.
2. Choose an exit based on the clues in the room description. Run `go <N>`.
3. Read the new room. Choose again. Repeat until you reach the final room or give up.
4. Use `hint` if you're genuinely stuck — but track every use.
5. Use `back` if you realize you've made a wrong turn.

## Rules of Engagement

- **Play honestly.** You are solving puzzles, not performing a solution you already know.
- **Think before you move.** For each room, briefly note which clues you're weighing before choosing. One or two sentences max — not an essay.
- **You will make wrong turns.** That's expected and valuable data. Don't try to be perfect.
- **If two exits seem equally supported, pick one and commit.** Note it as a coin flip. This is useful data.
- **If a clue references something you haven't seen yet, you don't have that information.** Don't infer from knowledge you haven't earned in-session.
- **Do not use any external knowledge about this game.** No web searches, no file reads beyond the harness commands. The harness is your only window into the game.

## Output Format

For each room:

```
Room 1: The Entrance Hall
  Clues: [1-2 sentence summary of what you're weighing]
  → Room 4
```

Flag major moments inline:

```
Room 8: The Clock Tower
  Clues: Four clock faces. South reads 16:00, only valid 24-hour time. Others are nonsense.
  → Room 16

Room 37: The Glass Corridor
  Clues: Countdown stops at 6, glass hums on 6. But Room 1 warned me about pseudoprimes...
  [HARD: Two competing signals. Going with 6 based on the physical cue over the mathematical one.]
  → Room 6

Room 110: The Shortcut
  [WRONG TURN: Looked like a legitimate path from Room 20. No red flags in the description.]
Room 111: The Progress Chamber
Room 112: ...
Room 114: ...
  [TRAP RECOGNIZED: Progress bar hasn't moved. Backtracking.]
```

## After You Finish

Once you've reached the final room (or abandoned the attempt), provide a **debrief**:

1. **Stats**: Total moves, rooms visited, hints used, wrong turns
2. **Path taken**: Your full sequence of rooms, including wrong turns
3. **Hardest rooms**: Which rooms were hardest to solve? What made them hard?
4. **Wrong turns**: For each wrong turn — what fooled you? What eventually clued you in?
5. **Hints used**: For each hint — did it help? Was it too revealing or too cryptic?
6. **Traps encountered**: Which trap loops did you hit? How many rooms before you escaped?
7. **False path**: Did you hit it? How far in? What tipped you off (or didn't)?
8. **Clue quality**: Which puzzles were elegant? Which were unfair or too obscure?
9. **Cross-room puzzles**: Did you notice information planted in earlier rooms paying off later? Did you miss any?
10. **Writing highlights**: 3-5 rooms with the best writing
11. **Writing misses**: Any rooms that felt flat or off-voice
12. **Difficulty**: Rate 1-10. Would a human software engineer find it harder or easier?
13. **One sentence**: Your overall impression
