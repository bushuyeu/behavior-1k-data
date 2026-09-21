# BEHAVIOR-1K 2026 — data composition

A composition study of all 100 tasks in the 2026 BEHAVIOR Challenge, built only
from the files the evaluator opens: its own constants, the robot configuration it
loads, the BDDL goal definitions it scores against, all 20,000 recorded
demonstrations, and the archived 2025 leaderboard.

**Read it:** https://bushuyeu.github.io/behavior-1k-data/

## What is in it

- What the benchmark is — corpus, robot, observation and action spaces, scoring
- How well the corpus fits π0.5, Team Comet's fine-tune, and Diffusion Policy
- Four places where the challenge documentation disagrees with the evaluator
- Where Q-score points actually live, and which goal predicates anyone satisfies
- What predicts a hard task
- All 100 tasks, with the organisers' demo recordings

## Provenance

Every figure is read from code or data rather than documentation. That is how the
first finding surfaced: `task_data.json`'s `duration` field disagrees with the
length the evaluator actually uses on 48 of the 50 tasks added for 2026.

| Source | Used for |
|---|---|
| `datasets/2026-challenge-task-instances/metadata/task.jsonl` | demo length, episode count, tiebreaker metrics |
| `bddl3/bddl/activity_definitions/*/problem0.bddl` | goal predicates (1,018 definitions) |
| `omnigibson/tasks/behavior_task.py` | the Q-score formula |
| `omnigibson/eval/utils/eval_utils.py` | control rate, resolutions, timeout, instance ids |
| `omnigibson/eval/r1pro.yaml` | robot, controllers, observation space |
| `docs/challenge_submissions/*.json` | the 2025 results, 23 submissions from 18 teams |
| `behavior-1k/2026-challenge-demos` `meta/` | per-episode lengths across all 20,000 episodes |

`tasks.json` is the parsed per-task dataset behind the page, if you want the
numbers without the prose.

## Caveats

Predicate counts are syntactic and are a **floor** on the 66 tasks whose goals
are quantified — see the Method section. The 2025 comparison covers only the 50
tasks carried over from that year, the only ones anyone has run.

Not affiliated with the BEHAVIOR Challenge organisers. Corrections welcome as
issues.
