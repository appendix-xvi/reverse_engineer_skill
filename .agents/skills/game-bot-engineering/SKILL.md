---
name: game-bot-engineering
description: Engineer evidence-driven native game automation and client/server tooling from authorized game artifacts, process-memory layouts, binary and protocol analysis. Use for DMO/JY-style bot architecture, patch-resilient offsets, packet framing, state machines, navigation, combat/quest workflows, and regression tests. Do not use for OCR-first or pixel-click automation when binary/protocol interfaces are available.
---

# Game Bot Engineering

Build from the actual client/server artifacts and observed behavior. Read [source skills and applicability](references/source-skills.md) for the six upstream skill families and their exact links. Read [implementation workflow](references/implementation-workflow.md) for integration checkpoints. Use the existing [reverse-engineer-anything](../reverse-engineer-anything/SKILL.md) workflow for shipped binaries and evidence.

## Select the evidence path

1. Resolve the exact game, client build, server type, architecture and target process; record binary SHA-256. Never reuse offsets or opcodes across builds without validation.
2. When the question is about in-process state, use a memory-layout workflow: candidate pointer chain, base/module-relative address, type, range, invariant, read-only verification, and patch-resilient AOB pattern where appropriate.
3. When the question is about game/client networking, use captured records, packet framing, opcode/message inventory, sequence/acknowledgment, compression/encryption detection, state transitions and an explicit coverage boundary. Do not infer live protocol behavior from a single packet.
4. When the question is about native execution, use focused disassembly, decompilation, references, and authorized dynamic tracing. Cross-check recovered pseudocode against assembly and event traces.
5. When the task is to implement a bot, separate transport, state observation, decision engine, action executor, safety guards and recovery. Do not couple all operations to one giant script.
6. When the client updates, compare old/new hashes and signatures, rerun all probes, and invalidate unverified offsets and packet mappings.
7. If evidence cannot support a requested operation, mark it unknown and propose a bounded test rather than inventing addresses, opcodes, decryption keys, or execution results.

## Architecture

For restart/relocation failures, movable Quick Slots, buff confirmations,
recorded routes or UI regressions, read
[runtime validation lessons](references/runtime-validation-lessons.md).

- **Adapter:** bounded memory/API/packet observations; no inferred authoritative game state.
- **Decoder:** type-aware parsing and validated packet/message schema with version tags.
- **World state:** timestamped entities, player state, map, inventory, quest flags, combat and connection state; handle stale/partial observations.
- **Planner:** explicit state machine or behavior tree with preconditions, priorities, timeouts, cancellation and idempotency.
- **Executor:** typed actions with result verification and rate/sequence guards; no blind write loops.
- **Recovery:** reconnect, desync detection, invalid-state fallback, watchdog and clean shutdown.
- **Test harness:** recordings and fixtures, deterministic unit tests, replay of valid captured scenarios, patch regression.

Treat observations, hypotheses, and implementation choices separately. Prefer normal source-code analysis for an available bot repository; invoke REA only for shipped binaries, runtime evidence, or opaque protocol behavior.

## Boundaries

Respect the user's authorized target, permitted test mode and execution scope. Do not make anti-cheat evasion, credential theft, authentication bypass, stealth persistence, or unauthorized server modification an implicit part of bot construction. External source skills may mention such techniques; evaluate scope and do not automatically adopt them.

## Completion contract

Report artifact/build identity, the verified observations, uncertain mappings, chosen bot architecture, tests actually executed, and remaining unknowns. Never describe an untested bot as working.
