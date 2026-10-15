# Shared reverse-engineering skill router

This repository stores reusable instructions, not an automatically connected REA engine. It is intended to be read from any ChatGPT or coding-agent session that has permission to access this GitHub repository.

## Start here

When the user asks about reverse engineering, decompiling, binary/protocol investigation, tracing a game's client/bot, JY Online, JYU, JYK-U, Digimon or DATS:

1. Read `.agents/skills/game-bot-reverse-engineering/SKILL.md` for game bot investigations; follow its referenced game-specific file.
2. Read `.agents/skills/reverse-engineer-anything/SKILL.md` and its targeted references when actual REA commands/capabilities are needed.
3. Prefer inspecting the actual target files and relevant source repository to guessing from prior chats, tool descriptions, or outdated notes.
4. If the requested target is source code with complete sources, use normal source analysis first. REA is for questions that require binary/package/runtime evidence.
5. Preserve the separation between **evidence found**, **interpretation**, **unverified hypothesis**, and **not inspected**.

## Tools and scope

- Do not install REA, Node.js, Ghidra, Hopper, IDA or other programs because this repository was read. The user explicitly wants a GitHub-centered, multi-chat workflow with no install by default.
- This repository cannot make a new ChatGPT conversation discover or run MCP tools automatically. Read it explicitly through GitHub when needed.
- If REA CLI/MCP is not actually available in the active environment, continue with supported normal file/code inspection and describe exactly what cannot be verified without that engine. Never claim REA ran.
- Do not infer current game behavior from the REA tool catalog. Confirm the target, version and capabilities of the environment used.
- Work read-only by default. Keep original client/bot executables, other bot instances, user credentials and online accounts unchanged. Obtain explicit authorization for intrusive live tests or mutations.
- Respect target permissions, license terms, and applicable law. Do not place proprietary binaries, secrets, process dumps, account details or raw confidential captures in this public repository.

## Project routing

- JY Online / JYU / JYK-U: `.agents/skills/game-bot-reverse-engineering/references/jy-online.md`.
- Digimon Masters / DATS: `.agents/skills/game-bot-reverse-engineering/references/digimon.md`.
- Common output and validation: `.agents/skills/game-bot-reverse-engineering/references/evidence-rules.md`.
- Sharing across chats: `docs/CROSS_CHAT.md`.
- Third-party upstream integrity and attribution: `UPSTREAM.md`.

Do not conflate `appendix-xvi/jythai-server` (server implementation), `appendix-xvi/remote-automation` (Windows/JYK-U operator workflows), `appendix-xvi/game-notes` (game notes), and this repository (shared RE Skill).

## Expected answer to an investigation

State the precise analyzed target and location, tool/read method, known file hashes/versions when available, observed findings with evidence coordinates, uncertainty, implications for the requested bot feature, and the next reproducible check. Never substitute an unperformed test with an estimated success percentage.
