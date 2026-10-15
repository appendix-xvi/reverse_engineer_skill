# Evidence and reporting contract

## Record identity

For any investigation record:
- Date/time and timezone
- Task and exact question
- Target kind (game client / third-party bot / server / script / packet capture)
- Exact verified path and working directory
- File hash (SHA-256), architecture and version if actually measured
- Tool and tool version, whether REA MCP/CLI, Ghidra provider or ordinary shell/static tools
- Input command/tool request and exact output or durable artifact identifier
- Scope, permissions and whether any program was executed, files modified, or game actions sent

## Claims

| Status | Required support |
| --- | --- |
| OBSERVED | Quote/locate specific extracted bytes, function, file, command output, capture record, or real test |
| DERIVED | Explain the reasoning and cite the observed facts that imply it |
| HYPOTHESIS | Give at least one falsification test and do not report as proven |
| UNKNOWN | Explain why not established; distinguish unexamined from unsupported |
| NOT RUN | Explicitly identify any suggested command or validation never executed |

When a tool or transport truncates output, read further pages or report partial coverage. Static inspection is not evidence of runtime behavior. Tool capability listing is not evidence that a particular target was successfully analyzed.

## Per-feature handoff template

### Question
What exact input/state/output is required?

### Targets
List exact paths and checksums; mark missing checksums `NOT MEASURED`.

### Verified observations
Each item: `OBSERVED`; source, location, reproduction, version, limitation.

### Interpretation
Each item: `DERIVED` or `HYPOTHESIS`; supporting IDs and falsification step.

### Unknowns
Each item: `UNKNOWN`, cause, impact on implementation and the shortest next read-only check.

### Implementation
Interfaces, state-transition diagram or pseudocode, plus acceptance tests. Do not claim an implementation exists unless committed/tested in its own repo.

### Results
Commands/tests actually run and their outcomes; avoid invented success rates or performance percentages.

## Data and repository boundaries

- This repository contains reusable skills and generic, sanitized examples. Keep game-specific code and validated implementation results in their project repositories.
- Do not commit original game/bot executables, proprietary source, license files, tokens, passwords, character/account profiles, raw process dumps or raw traffic that can contain secrets.
- Keep references to private Windows paths as descriptive user-supplied leads, not publicly verified inventories.
- Never overwrite/delete source or unrelated projects as a side effect of an investigation.
