# External reverse-engineering methods and authoritative sources

Use this guide when REA evidence is incomplete, an external tool is needed, a platform-specific method is unclear, or the user asks for a broad research update. This is a source-and-method routing guide, not a claim that these tools are installed or that REA exposes them. Verify current upstream documentation and tool versions at task time.

## Research and evidence discipline

1. Identify the exact artifact, version/build, OS, architecture, provenance, and SHA-256 before comparing claims.
2. Prefer maintainers' official documentation, specifications, source repositories, and reproducible papers. Capture URL, access date, applicable version, and the specific documented behavior. Treat blog posts and community recipes as hypotheses to verify.
3. Distinguish format facts, static observations, reconstructed/decompiled interpretations, runtime observations, and hypotheses. A decompiler output is *not* original source; an API's availability is *not* proof the target uses it.
4. Compare independent evidence at the same abstraction level: header/section parser against raw bytes; disassembly against control flow and references; pseudocode against assembly; runtime trace against instrumented event and an uninstrumented baseline.
5. Record limits: stripped symbols, obfuscation, packed/encrypted code, unreachable paths, anti-instrumentation, incomplete captures, sampling, architecture differences, and tool/parser errors. Do not elevate absence in one bounded search to global absence.
6. For behavioral questions, define a minimal repeatable input/output experiment and note whether instrumentation or hooking could change timing or behavior. Do not run or modify a target without authorization.
7. Before importing new techniques into this skill, check that the documented feature exists in the connected REA version or mark it as an independent external workflow. Avoid invented MCP tool names and unverified installation commands.
8. Use citations that point to individual claims, not merely a generic tool homepage. Recheck changing releases and APIs instead of copying version-specific instructions indefinitely.

## Tool and method selection

| Investigation | External reference and fallback | What it can establish | What it cannot establish alone |
| --- | --- | --- | --- |
| PE/COFF headers, sections, imports, relocations | [Microsoft PE/COFF](https://learn.microsoft.com/en-us/windows/win32/debug/pe-format); [LLVM llvm-readobj](https://llvm.org/docs/CommandGuide/llvm-readobj.html) | On-disk layout and parsed metadata | Which runtime branches executed |
| ELF, Mach-O, COFF cross-check | [LLVM llvm-readobj](https://llvm.org/docs/CommandGuide/llvm-readobj.html) | Object-format structures and symbol/relocation records where present | Complete semantics of optimized or stripped code |
| Native disassembly and decompilation | [Ghidra](https://github.com/NationalSecurityAgency/ghidra); [Ghidra headless analysis](https://github.com/NationalSecurityAgency/ghidra/blob/master/Ghidra/RuntimeScripts/support/analyzeHeadlessREADME.md) | Function candidates, references, control/data flow and pseudocode | Original high-level code or runtime coverage |
| Dynamic native and mobile instrumentation | [Frida modes](https://frida.re/docs/modes/); [Frida JavaScript API](https://frida.re/docs/javascript-api/); [frida-trace](https://frida.re/docs/frida-trace/) | Calls and values actually observed under declared instrumentation | Unobserved paths or reliable behavior when hooks perturb execution |
| Android DEX/APK and mobile test workflow | [JADX](https://github.com/skylot/jadx); [OWASP MASTG techniques](https://mas.owasp.org/MASTG/techniques/) | Decompiled candidates, resources, manifest, platform test methodology | Guaranteed decompilation correctness or all runtime behavior |
| iOS mobile investigation | [OWASP MASTG iOS techniques](https://mas.owasp.org/MASTG/techniques/); [Frida iOS](https://frida.re/docs/ios/) | Platform-relevant static/dynamic testing routes | A usable iOS runtime or permissions on the present host |
| .NET CLI metadata | [ECMA-335](https://ecma-international.org/publications-and-standards/standards/ecma-335/); [System.Reflection.Metadata](https://learn.microsoft.com/en-us/dotnet/api/system.reflection.metadata) | Metadata signatures, tables and managed-assembly structures | NativeAOT source-level restoration from absent metadata |
| Saved network evidence | [TShark manual](https://www.wireshark.org/docs/man-pages/tshark.html); [Wireshark filter reference](https://www.wireshark.org/docs/man-pages/wireshark-filter.html) | Packets, fields, timing and endpoints present in the recording | Traffic not captured, encrypted plaintext, live server state |

## Practical cross-check recipes

### Native feature reconstruction

- Inventory executable format, imports/exports, strings, sections, symbols, compiler/runtime clues, and protections with a format-aware parser.
- Find candidate entry points using xrefs and call/data flow; review actual assembly around branches, writes, network dispatch and error paths.
- Decompile only targeted routines; validate argument types, calling convention, ownership and state transitions against disassembly.
- If authorized runtime evidence exists, compare outputs and branch effects under controlled inputs. Label reconstructed behavior separately from observed behavior.

### Android or iOS behavior

- Record app package/build ID and integrity hash. Inspect platform declarations, resources and native libraries before following app logic.
- Treat JADX output as a navigational representation; verify suspicious decompilation with DEX/Smali or native code. Follow OWASP's platform technique index for test design.
- When dynamic instrumentation is authorized, select a narrow call target, preserve original inputs/outputs, and test whether tracing changes the result. Document rooted/jailbroken, simulator, and embedded-gadget constraints rather than silently assuming access.

### Network or protocol reconstruction

- Keep an immutable original capture and hash. Record capture point, clock, interface, snap length and known dropped or missing events.
- Separate capture filters from display filters. Inspect protocol decode and raw bytes for important claims; retain frame numbers, endpoints, directions and timestamps.
- Correlate client-side calls with server-side packets only when there is a defensible shared identifier or timing/transport evidence. A missing packet in a limited capture does not prove no request was made.

## Maintenance cadence

For each major skill revision, revisit the official source links above; check REA's actual MCP inventory and upstream release documentation, and add only capabilities tested or explicitly marked as external. Record a dated source review in the change description. Do not claim the global literature has been exhaustively searched.
