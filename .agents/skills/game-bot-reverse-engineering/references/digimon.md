# Digimon Masters / DATS investigation profile

## Actual user-supplied reference

The previously supplied sample bot is at:

`K:\Information\Game\Digimon\Bot\DATS v9.98`

This is a **reported path**, not proof that the directory is currently accessible. Inspect its present contents, exact executable filenames, file types, checksums and architecture before claiming anything about how DATS works. A past note says its runnable bot license had expired; do not infer that its program is nonfunctional or that its live behavior has been observed in this session. Do not attempt license bypass.

## Actual development goal

Build a practical client-aware Digimon bot which reads authoritative game state (rather than estimating it from OCR/color matching), discovers nearby monsters and their identities, selects an intended target, tracks real HP/MP/other state, and executes/reconciles movement, battle, consumables and recovery.

The user allows understanding DATS as a reference but does **not** require copying DATS's architecture or protocol.

## Research questions (not claims)

- Does DATS read the client process, use IPC, receive network messages, call UI controls, or combine approaches?
- Where do monster IDs/names, target selection, player/Digimon HP/MP, cooldowns and position originate?
- How does the program determine that an action succeeded and detect map changes or reconnects?
- Which data models depend on specific client versions, ASLR/module relocation, language localization or server patches?
- Can a clean independent implementation obtain the needed state from authorized local observation without imitating unverified DATS internals?

## Investigation route

1. Read inventory of DATS directory and game client; classify executables and DLLs as native PE, .NET or other.
2. Identify configuration, imports, resource strings and references to window/process APIs, networking and local storage.
3. Trace one complete goal at a time: `list visible monsters` -> `select named monster` -> `observe real target/HP` -> `issue action` -> `verify change`.
4. If packet recordings exist, correlate user actions with captures; packet tools analyze **saved** data, not live wire traffic unless another capture system was actually run.
5. If memory reads are considered, validate pointer paths, field widths and stability on a specific test build. Never treat a plausible raw value as authoritative without cross-checks.
6. If the DATS program cannot execute, report a static-analysis boundary and proceed with separate game-client evidence; do not invent DATS runtime results.
7. Implement independent modules only after the relevant input/output contracts are observed. Test each state/action pair before automating gameplay loops.

## Acceptance checkpoints

- Monster identity and selection match what the client actually holds.
- HP/MP readings track controlled known changes without OCR/color dependencies.
- Actions, cooldowns and state transitions are confirmed after execution rather than assumed from sent input.
- Stale targets, disconnects, missing access, unrecognized game builds and corrupt state produce explicit errors and safe recovery.
- All reported verification includes binary/game version, observation and what has **not** been tested.

Never claim a full autonomous bot from successful string extraction, pseudocode, or a single action capture. Original client and third-party bot binaries remain unmodified by default.
