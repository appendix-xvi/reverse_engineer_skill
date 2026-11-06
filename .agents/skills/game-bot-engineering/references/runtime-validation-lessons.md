# Runtime validation and accepted baselines

Sanitized lessons transferred from DMO investigations on 2026-11-06.
These are validation methods, not portable offsets or claims about another bot.

## Restart failures with an unchanged executable

- Record the current process identity and mapped executable allocation as well
  as the file hash. The same file can load at a different base on the next run.
- Distinguish the PE preferred base, the base used by the reference capture,
  and the current mapped base. Do not subtract a customary default base from
  reference addresses whose capture base has not been established.
- Validate image path, architecture, headers, bounds and independent code/data
  references before rebinding. Reacquire runtime objects after process, actor
  or map-context changes; saved object pointers are not durable identifiers.
- Relocate only known absolute operands in a recorded instruction signature.
  Preserve exact checks on all other bytes; masking a mismatch is not recovery.
- Separate read-only data validation from action-call validation. A changed
  discard entrypoint need not disable inventory inspection, while disposal
  must still require its complete verified execution contract.

## Item identity, timers and confirmation

- Resolve the item currently assigned to a slot, then its typed effect metadata
  and live effect state. A slot number is not an item identity or buff duration.
- Recheck expected item, owner and current context at execution time. Slot
  movement between observation and dispatch must not use an unintended item.
- Compare public-source layouts with runtime types and multiple samples;
  similar field values or old headers alone do not establish a field offset.
- Distinguish action requested, dispatched, modal confirmation queued, effect
  applied, and quantity consumed. Each requires its own observation.
- A first-use confirmation and an overwrite-existing-effect dialog may look
  similar but have different semantics. Any authorized confirmation adapter
  must validate the exact new dialog, item, recipient and state; never approve
  an arbitrary existing modal or use a generic confirmation keystroke.
- Unknown/stale effect observations are not proof of absence. Use distinct
  valid samples, deduplicate equivalent effects and bound unconfirmed retries.
- Keep timer observation and confirmation waits outside the combat dispatch
  loop so one pending item cannot block attacks and ordered skill requests.

## Routes, encounters and failures

- Derive route points from a recorded run, but do not replay every manual pause.
  Use pass-through intermediate points and explicit final arrival conditions.
- Bind an encounter to validated identity, zone and runtime entity. Missing
  selection or a vanished HP bar does not by itself prove that entity died.
- Separate native-call acceptance from observed motion and completed arrival.
  A pathfinding or rendering symbol does not prove wall traversal capability.
- Recover only after known cancellation/cleanup. An unknown in-flight native
  call must not be overlaid with a new call and described as successful retry.

## UI evidence and release handoff

- Persist UI callback successes/errors even when no worker is running. Read
  those logs before changing behavior; record stage, reason and context needed
  to distinguish read, selection, dispatch and confirmation failures.
- Exercise the actual UI callback where feasible. An API-only pass does not
  establish that the user's Start button works. Label an owned hidden test UI
  separately from a user-operated live UI and from visual user acceptance.
- Preserve a known working commit with an immutable acceptance tag before
  further changes. Store failed hypotheses and limits alongside accepted runs.
- If a log is still growing, archive a hashed prefix and label it as such.
  Keep raw logs, process captures, proprietary source and settings local.
- Report the exact remote branch and commit verified on the server. A pushed
  feature branch does not mean main is current or that a release was deployed.

## Project evidence

Game-specific implementation and evidence limits remain in
[dmo-bot at f86dc2d](https://github.com/appendix-xvi/dmo-bot/tree/f86dc2d67ae01a01b0908127b7b3d44ceec30117/docs/knowledge):
`inventory-runtime-relocation.md`, `buff-confirmation-accepted.md`,
`buff-item-timers.md`, and `water-normal-smooth-accepted.md`.
The accepted inventory repair does not prove real disposal after every restart;
the accepted buff first-use path does not prove natural-expiry renewal or all
item families. Preserve those limits when reusing these methods.
