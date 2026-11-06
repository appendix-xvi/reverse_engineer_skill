# Implementation workflow for native game automation

## 1. Discover

- Inventory the actual bot repository and current client build. Read its entrypoints, transport, scheduling, state handling and test setup first.
- Record supported operations and baseline failures. Do not start by rewriting an existing working transport.
- List each requested behavior as a testable contract: inputs, preconditions, expected observable results, timeouts and failure recovery.

## 2. Establish interfaces

### Process memory

- Identify module/base and ASLR context; use read-only probes first.
- For each value, store: symbol/field name, width/signedness, address expression, pointer dereference order, validity invariant, sample values, build hash, confidence and evidence.
- Validate dynamic pointer chains across independent restarts. Ensure AOB signatures match the intended function uniquely on the verified build.
- Never guess an offset from a screenshot, text search, or a prior client patch.

### Protocol

- Index original captures with timestamps, direction, endpoint, session and raw frame index.
- Recover transport framing before interpreting message opcodes.
- Separate observed opcode and payload bytes from inferred field meaning, then test each field with controlled state changes.
- Model stateful ordering: handshake, authentication, world entry, movement, combat, response, retry, disconnect.
- Document compression, encryption and unknown framing without claiming decrypted content where none was observed.

### Native logic

- Follow the action from UI/service entrypoint to its call sites and serialization/storage effects.
- Cross-validate disassembly and pseudocode; use authorized dynamic evidence for ambiguous branches.
- Record caller/callee addresses, offsets and dependencies under the exact build.

## 3. Build bot components

Use separable modules:
- `transport`: connection, packet framing, retry, backpressure.
- `decoder`: versioned schema and validation.
- `observation`: snapshots and freshness.
- `world_model`: entities, map, inventory, quest, combat.
- `policy`: state machines or behavior trees.
- `actions`: typed action dispatch and acknowledgment.
- `recovery`: watchdog, timeout, reconnect and safe stop.
- `tests`: unit fixtures, trace replay and integration checks.

Do not mix parsing, planning and action emission into one loop. Each operation must have an explicit success condition, timeout and cancellation route.

## 4. Verify and maintain

- Test parser round trips on captures/fixtures and malformed records.
- Test state transitions with fake adapters before connecting to a live target.
- Compare before/after observations for actual actions and measure timeout/failure behavior.
- On game updates, invalidate unverified build-specific structures and rerun signature, decoder and behavior regression.
- End every report with passed/failed/not-run tests, artifacts and remaining unknowns.

## Source skill routing

- Pointer/offset or patch recovery: see [game-re-skills](source-skills.md).
- Hooking, trace or disassembly: see [as0ler/skills](source-skills.md) and the existing REA skill.
- Protocol schemas: see [wshobson/agents](source-skills.md).
- Large binary investigation: see [reverse-skill](source-skills.md).
- Windows game code reconstruction: see [windows-game-matching-decomp-skill](source-skills.md).
