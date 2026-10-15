# JY Online / JYU / JYK-U investigation profile

## Distinguish targets

- `appendix-xvi/remote-automation`: operating existing Windows JYK-U bots and account-specific workflows. Read its current `AGENTS.md` and configuration before any UI/process action.
- `appendix-xvi/jythai-server`: original-client-compatible Thai game server project. It is **not** automatically a JYK-U bot project. Read its own `AGENTS.md` for test-client and account constraints.
- `appendix-xvi/game-notes`, folder `jy-online`: game and quest reference, not proof of executable implementation.
- `K:\Information\Game\JY\Dev\jy-event`: previously supplied workspace for merged JYU event analysis. Check that it exists before relying on it.
- `K:\Information\Game\JY\Dev\jy-event\jyu_all_events_merged.sqlite`: previously discussed event database, not a verified source for every original condition.
- Do not invent a binary path. Determine the current executable and build from the actual filesystem and process.

## Important known reliability issue

Prior JYU event parsing has displayed condition type 31 as `上线N小时`. Those hour values were not established to be original server prerequisites. Query the event reliability notes and verify original condition semantics through client/server/runtime evidence. `UNKNOWN` is preferable to a confident wrong prerequisite.

## Target analysis order

1. Select an exact feature: event and its conditions, NPC conversation/event dispatch, map travel, combat training, inventory, item use, command mapping or server/client messages.
2. Establish whether the relevant behavior belongs to JYK-U, the original client, custom server implementation or a script.
3. For existing JYK-U, inspect its live UI controls/commands and matching local bot files. Do not interpret navigation commands as dungeon automation without evidence.
4. For event data, correlate map ID, NPC ID, event ID, script flags, outcome and character state; do not equate a missing condition with a wrong event.
5. For protocol reverse engineering, use actual recorded action/capture pairs. Preserve offsets and endian assumptions as unverified until decoded and replay-confirmed.
6. For client binaries, identify native/managed architecture and exact checksum before function analysis. Compare observed UI behavior to decompiled candidates.
7. Produce a minimal verified API/state-machine design and test against authorized instances.

## Operator safety

Read the current target project's AGENTS.md first. Never touch another account just because it appears in earlier chat notes. Preserve unrelated game processes, windows and sessions. Avoid OCR or pixel heuristics when real application controls/native values are accessible, but also never claim native values without evidence.

## Desired deliverable

A per-feature evidence table: source artifact/build, verified inputs and action, read state, produced side effects, unknown conditions and reproducible verification. If implementation is requested, keep reverse-engineering notes and tested source changes in the appropriate JY project repository, not in this shared skill repository.
