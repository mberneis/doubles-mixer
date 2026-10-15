# Doubles Mixer

**Round-robin doubles schedules for 2 courts, where everybody plays with everybody.**

Live site: **[double-mixer.pages.dev](https://double-mixer.pages.dev/)**

Doubles Mixer generates ready-to-play schedules for social doubles sessions (pickleball, tennis, padel, badminton, or any 2-vs-2 game) on two courts with four players per court. It rotates partners, mixes up opponents, alternates court sides and team positions, and keeps both courts busy every round.

---

## The problem

You have **2 courts** and a group of **8, 9, or 10 players**. You want a schedule where:

1. **Every player partners every other player** at least once (ideally exactly once).
2. **Opponents vary as much as possible**, so no one keeps facing the same people.
3. **Courts and sides rotate**, so no one is stuck on the "bad" court all session.
4. **Sit-outs are fair and spread out** when there are more than 8 players.

Shuffling names by hand rarely satisfies all four. The math behind a correct answer is a well-studied area of combinatorics called **whist tournament designs**.

## Why it's harder than it looks

Each round on two courts produces exactly **4 partnerships** (2 per game). The number of partnerships a group needs is `n × (n − 1) / 2`, so:

| Players | Partnerships needed | Rounds (÷ 4) | Sitting out per round | Perfect "partner exactly once"? |
|---|---|---|---|---|
| 8 | 28 | 7 | 0 | Yes |
| 9 | 36 | 9 | 1 | Yes |
| 10 | 45 | 11.25 | 2 | **No** (not a whole number) |

- **8 players:** a classic whist tournament. Every pair partners exactly once and faces each other as opponents exactly twice, in 7 rounds.
- **9 players:** a near-resolvable whist design. One player sits out each round, everyone sits out exactly once, every pair partners exactly once and opposes exactly twice, in 9 rounds.
- **10 players:** a perfect schedule is mathematically impossible, because 45 partnerships cannot be split evenly into rounds of 4. This version repeats only three pairs and gives everyone at least two games between sit-outs.

This matches the classic existence result for whist tournaments: they exist exactly when the number of players is congruent to 0 or 1 modulo 4. 8 and 9 qualify; 10 does not.

### A limit worth knowing (8 players)

With 8 players, you cannot have perfect partner balance, perfect opponent balance, **and** an even 3/4 split of courts for every player at the same time. An exhaustive search of every 8-player whist schedule confirms that at least one player ends up with a lopsided court split. If one court is noticeably worse, play the schedule twice and swap courts on the second pass, which gives everyone an exact 7/7 split.

## Features

- **Three schedules:** 8, 9, and 10 players
- **Follow a player:** highlight one player's games and dim the other rounds
- **Custom player names:** edit names for your group (saved locally in your browser)
- **Player summary:** games on Court A, games on Court B, and rest count per player
- **Export CSV** for spreadsheets or club software
- **Print schedule** for posting courtside

### Reading the schedule

- **Court A:** first match of the round
- **Court B:** second match of the round
- **Sitting out:** resting players for that round
- Left and right teams represent opposite playing sides. Teams and player positions rotate to limit repeated assignments.

## Tips for running a session

- **Draw numbers randomly** so any unavoidable imbalance (an extra sit-out or a lopsided court split) lands on chance, not on a particular person.
- **Score individually.** Since partners change every round, rank players by total points or games won across all rounds.
- **Give sit-out players a job**, such as keeping score or refereeing.
- **Budget your court time.** At roughly 15 minutes per round, 8 players take about 1¾ hours, 9 players about 2¼ hours, and 10 players about 3 hours.

## Background reading

The scheduling problem is a special case of the designs studied in:

> R. Julian R. Abel, Norman J. Finizio, Malcolm Greig, and Scott J. Lewis.
> **"Generalized whist tournament designs."**
> *Discrete Mathematics* 268 (2003), 1–19.
> [ResearchGate](https://www.researchgate.net/publication/222140264_Generalized_whist_tournament_designs)

In that paper's notation, a standard doubles mixer (two teams of two per game) is a **(2, 4) GWhD(v)**: a schedule for *v* players in which every pair are teammates once and opponents twice. The paper generalizes this to games with more teams and larger teams, and gives constructions and existence results for many cases.

## Deployment

The site is a static web app hosted on [Cloudflare Pages](https://pages.cloudflare.com/) at [double-mixer.pages.dev](https://double-mixer.pages.dev/).

## Author

© 2026 [Michael Berneis](https://michael.berneis.com)
