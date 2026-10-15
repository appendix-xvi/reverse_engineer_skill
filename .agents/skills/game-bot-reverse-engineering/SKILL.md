---
name: game-bot-reverse-engineering
description: Evidence-first analysis of user-authorized JY Online/JYU/JYK-U and Digimon Masters/DATS client or bot artifacts; trace client data and behavior into independently tested bot features without assuming protocol or memory mechanisms.
---

# Game Bot Reverse Engineering

This skill wraps the upstream `../reverse-engineer-anything/SKILL.md`. It does not replace REA or make an analysis engine available.

## Activate for

- JY Online, JYU, JYK-U, JY bot protocol, events, NPC interaction, automated combat, client behavior.
- Digimon Masters Online, DMO, DATS, target/monster discovery, live HP/MP, inventory, combat or movement.
- Questions where real shipped artifacts, runtime observations, or saved captures are needed to distinguish possible implementations.

Read the relevant file in `references/` before acting.

## Evidence-first workflow

1. **Define the question and artifact.** Identify the exact EXE/DLL/assembly/archive, source directory, version/hash and whether it is an original game client, third-party bot, server, or previously extracted data. Never substitute a similarly named executable.
2. **Inventory first.** Determine file formats, architecture, imports, resources, dependency and configuration files. For PE/.NET distinguish managed inspection from native analysis. For full source projects use source-reading tools before any REA.
3. **Choose only a working route.** REA may inspect native binary via Ghidra/Hopper/IDA, managed PE metadata, or recorded packets with specified prerequisites. Do not claim runtime memory scanning, dynamic instrumentation or packet acquisition is provided when it has not been demonstrated. Existing OS tools may be used with their own provenance.
4. **Trace the requested behavior.** Search strings, references, call sites, data structures and control flow relevant to the feature. Focused questions beat bulk blind decompilation. Link a value or network field to a producer, consumer and validation condition.
5. **Identify how information is obtained, do not guess.** Candidate mechanisms include process memory, an API, game/client IPC, captured network traffic, controls or files. Document evidence for each candidate and eliminate only with actual tests.
6. **Reconstruct an explicit design.** Separate readers/decoders, state model, selectors, action executor, recovery, verification and logs. Mark protocol offsets, pointers, keys and field meanings as unknown until verified.
7. **Validate against the running client only when authorized.** Confirm values/actions using the real source of truth and repeated controlled observations. Do not generalize one build/session/address to another.
8. **Write a reproducible handoff.** Summarize facts, competing explanations, failed tests, limitations and exact next check. Do not assert full bot support or success before exercising it.

## Priority when implementing an actual bot

- Accurate live state (actor, target, monsters, HP/MP, available actions), with field validity checks.
- Target discovery and selection, including predictable handling of no target or stale target.
- Known input/action mapping based on verified behavior; never invent buttons, memory offsets or packet opcodes.
- Combat, consumables, loot, navigation and recovery based on the verified state machine.
- Repeatable instrumentation and acceptance tests. Start read-only; grant write/action capabilities only in the intended test environment.

## Required reporting

Use `references/evidence-rules.md`. Explicitly label:
- `OBSERVED` — actually seen in artifact/tool output or controlled test.
- `DERIVED` — conclusion justified by specified observations.
- `HYPOTHESIS` — possible but untested.
- `UNKNOWN` — not determined or unavailable.
- `NOT RUN` — command/verification was not executed.

If REA is unavailable, say so once, use available read-only analyses and provide specific missing evidence instead of producing fabricated pseudocode or pretending a provider was used.

## Guardrails

Do not install anything just to read this skill. Do not modify original binaries, bypass license expiration, inject into a protected live process, alter the user's bot accounts, or start gameplay tests unless requested and permitted. Treat unknown, proprietary, credential-bearing or third-party artifacts cautiously. Respect the target project's own AGENTS.md and readme when altering that project.
