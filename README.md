# Jumple

A daily word game: like [Squaredle](https://squaredle.app/), but the letters don't need to touch.
You can jump from any letter to any other.

## Playing

Each Jumple is a 3×3 board of nine different letters. Find words of 4 or more letters by tapping the
letters in order, or by typing, then pressing Enter. Each letter can be used once per word, and it
doesn't matter where on the board the letters are. ⤨ Shuffle moves them around to help you spot new
words.

As the progress bar fills you earn the same help as Squaredle:

1. ★ Red numbers: how many words still to find start with each letter.
2. ★ White numbers: how many words still to find use each letter. A letter goes dark once every word
   that uses it is found.
3. ★ Hints: show the first letters of each missing word and sort the word list alphabetically.

As in Squaredle, tap the word count above the board to open the word list. Each board comes with one
💡 reveal, and the third star earns another. Reveals only work on 4, 5 and 6 letter words: the word
list offers a random one of each length, and once the hints are unlocked you can tap a missing word
twice to reveal it. Its letters then light up in order on the board, and it counts once you tap it
out.

There's a new board every day, and every earlier board stays playable from the home screen.

## Running locally

It's a static site with no build step:

```sh
python3 -m http.server
```

then open http://localhost:8000.

## Boards

`boards.js` holds 1,000 boards, one per day from the first Jumple (`FIRST_DAY` in `game.js`). Regenerate
them with:

```sh
python3 tools/gen.py
```

The generator tries random sets of nine different letters, keeps the ones with 25 to 60 required words
where every letter is used by at least one of them, and prefers boards with a long word to hunt for.
Common American English words (SCOWL up to size 55) become required words; everything else in the
dictionary counts as a bonus word. To move a word across that line, add it to `tools/data/avoid.txt`
or `tools/data/promote.txt` and regenerate. The generator is seeded, so regenerating gives the same
boards unless the word lists change; changing them can change boards people have already played.

Any board that spells a word from `tools/data/blocklist.txt` is thrown away, apart from the everyday
words listed in `tools/data/unblock.txt`. Word list sources and licenses are in `tools/data/SOURCES.md`.

Jumple is based on [Birdle](https://github.com/peterhudson/Birdle).

## License

GNU General Public License v3.0. See [LICENSE](LICENSE).
