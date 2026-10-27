# Live Slot: a 3-reel slot game with a free-spins bonus

A small browser slot game built as a learning project. It uses **virtual credits only**: no real money, no payments.

**Live demo:** https://artm-x.github.io/slot-demo/

## Features

- 3 reels, 7 symbols: 6 paying symbols and 1 bonus (scatter) symbol 🎁
- Adjustable bet (5 / 10 / 20 / 50 / 100)
- **Free spins bonus:** three 🎁 award 10 free spins in which every win is multiplied by ×3
- Win highlighting, sound effects generated with the Web Audio API (no audio files), confetti on big wins
- **Localisation:** English, Polski, Українська, Deutsch. The language is detected from the browser and can be switched in the page
- Balance, spin counters and bonus state are saved in the browser (`localStorage`)
- A single HTML file with no dependencies

## The math

Every combination of the three reels is equally likely (7 × 7 × 7 = 343 outcomes).

| Symbols (3 of a kind) | Pays |
|---|---|
| 🍒 | ×13 |
| 🍋 | ×15 |
| 🍉 | ×23 |
| 🔔 | ×38 |
| ⭐ | ×62 |
| 7️⃣ | ×116 |

- Two matching symbols on the first two reels return the bet (×1)
- 🎁🎁🎁 pays nothing itself but triggers 10 free spins (no bet taken, wins ×3, no re-trigger)

| Measure | Value |
|---|---|
| RTP from the base game | 88.34% |
| RTP from the bonus | 7.73% |
| **Total RTP** | **96.06%** |
| Hit frequency (any win) | 12.2% |
| Bonus frequency | 1 in 343 spins |

The page computes the exact RTP itself by enumerating all 343 outcomes, and a built-in simulator (100,000 spins) lets you compare the simulated RTP with the theoretical value. Because the top prizes are large, the simulated result fluctuates noticeably between runs (variance), which is why real games are tested on hundreds of millions of spins.

## Design notes

- The outcome of a spin is decided **before** the animation starts. The animation and the sounds only display a result that is already known.
- One function (`rollSpin`) draws the symbols for both the game and the simulator, so the game and its math cannot drift apart.
- All visible text lives in a `translations` object, separate from the game logic. Adding a language means adding one block of translations and one `<option>`.

## Run it

Open `index.html` in any modern browser. No installation or server is needed.

## Important

This is an educational demo. It uses `Math.random()`, which is **not** suitable for real-money games. Real-money gaming is regulated, requires licensing, and requires certified random number generators and independent testing. Do not use this code to offer real-money gambling.

Built while learning web development, with the help of an AI assistant.
