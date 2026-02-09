# The Clockwork House — Blind Playtest Brief

## Setup

I'm uploading a single-file HTML text adventure game. Read and internalize the entire file — all rooms, mechanics, and structure. Then play through it as described below.

## Your Role

You are a **first-time player**. You have never seen this game before. You do not know:

- The true path
- Which rooms are traps, recovery, or false leads
- The `correct` property on any room
- The `TRUE_PATH` array
- Any structural comments in the source code

You know only what a player sitting in front of this game would know: the room description you're currently reading, the exits available to you, and the hint system (if you choose to use it).

**Do not reference the source code, variable names, data structures, or developer comments in your reasoning or choices. Play from the prose.**

## How to Play

1. Start in Room 1. Read the description. Choose an exit based on the clues in the text.
2. For each room, state only:
   - The room number and title
   - Which exit you chose and the room number you're going to
3. **Do not narrate your reasoning for every room.** Just make your choices and move.
4. **Flag MAJOR moments only** — with a brief note in brackets. A major moment is:
   - A wrong turn that felt right (you were genuinely fooled)
   - Recognizing you're in a trap loop (and how many rooms it took you to notice)
   - Using a hint (and whether it helped)
   - The moment the false path revealed itself (if you hit it)
   - Any room where the clue simply didn't land — you had to guess
   - Any room where the writing made you stop and appreciate it
5. When you reach Room 200 (or give up), stop.

## Output Format

Play the game as a simple move log:

```
Room 1: The Entrance Hall → Room 4
Room 4: The Study → Room 8
Room 8: The Clock Tower → Room 16
...
```

Flag major moments inline:

```
Room 8: The Clock Tower → Room 21
  [WRONG TURN: The horse hatch. The "ignore the horse" clue wasn't visible yet — I only had clock faces to work with and the east hatch felt thematic.]
Room 21: The Attic Storeroom → Room 8
  [RECOVERY: Took 1 room to realize I was off-path. The letter mentioning "everything that matters is below" was clear.]
Room 8: The Clock Tower → Room 16
```

## After You Finish

Once you've reached Room 200 (or abandoned the attempt), provide a **debrief** covering:

1. **Stats**: Total moves, rooms visited, hints used, wrong turns taken
2. **Hardest rooms**: Which true-path rooms were the hardest to solve from prose alone? What knowledge did they require?
3. **Best trap**: Which trap loop was most convincing? How many moves before you escaped?
4. **False path**: Did you hit it? How far in before you realized? What tipped you off?
5. **Clue failures**: Any rooms where the clue was too obscure, contradictory, or required knowledge a thoughtful reader wouldn't have?
6. **Clue wins**: Any rooms where the puzzle design was particularly elegant?
7. **Writing highlights**: 3-5 rooms with the strongest prose
8. **Writing misses**: Any rooms that felt flat, generic, or off-voice
9. **Overall difficulty**: Rate 1-10 and say whether you think a human software engineer would find it easier or harder than you did
10. **One sentence**: Your overall impression of the game
