# Extended platform and specialist reverse-engineering workflows

Source review: 2026-11-06. This guide complements the REA tool routing in SKILL.md and [external methods](external-methods-and-sources.md). It describes independent methods and authoritative sources; it does **not** claim that a connected REA release implements every workflow. Verify versions and prerequisites when used.

## Before choosing a specialist workflow

- Confirm target provenance, legal scope, OS, CPU/ABI, artifact version and SHA-256. Keep the original read-only.
- Identify container format and embedded members before assuming the extension represents executable code.
- Compare observed bytes and symbols with the governing specification. State which fields are parsed, missing, inferred or unsupported.
- Use an isolated test environment for any authorized execution, fuzzing, debugger attachment, extraction of untrusted firmware, or malware investigation. Do not launch arbitrary shipped content merely because a parser found an executable.
- Prefer a narrow question and independent corroboration to a whole-target dump. Preserve tool versions, parameters, timeouts and evidence identifiers.

## Linux ELF and architecture-specific ABI

Sources:
- [System V ELF generic ABI](https://gabi.xinuos.com/elf/00-foreword.html)
- [Linux elf(5)](https://man7.org/linux/man-pages/man5/elf.5.html)
- [LLVM llvm-readobj](https://llvm.org/docs/CommandGuide/llvm-readobj.html)

Workflow:
1. Identify ELF class, endianness, machine, OS ABI, type and interpreter from the original header.
2. Cross-check program headers (loader view) against section headers (linker/static view); they answer different questions.
3. Inspect symbol tables, dynamic dependencies, relocations, notes, TLS and hardening-related entries where present. Distinguish absence of symbols from absence of code.
4. Use the target architecture's psABI for calling conventions, relocation meanings and register roles. Do not apply x86-64 assumptions to ARM64, RISC-V or another target.
5. Correlate disassembly addresses with load bias/PIE before comparing runtime addresses to file offsets.

## macOS / iOS Mach-O

Sources:
- [Apple Mach-O documentation](https://developer.apple.com/documentation/kernel/mach-o)
- [Apple Mach-O overview](https://developer.apple.com/library/archive/documentation/Performance/Conceptual/CodeFootprint/Articles/MachOOverview.html)
- [Apple XNU Mach-O loader definitions](https://github.com/apple/darwin-xnu/blob/main/EXTERNAL_HEADERS/mach-o/loader.h)

Workflow:
1. Inspect fat/universal wrappers and select the relevant architecture slice.
2. Review Mach-O header, load commands, segments/sections, dependent dylibs, chained fixups and available symbol information.
3. Treat code-signing metadata, entitlements and hardened runtime as environment constraints; do not infer successful runtime injection or execution from file structure.
4. Match loaded image slides and arm64e pointer-authentication behavior to the concrete host/build before interpreting addresses.
5. When runtime access is absent, stop at static conclusions instead of fabricating Objective-C/Swift call traces.

## WebAssembly

Sources:
- [W3C WebAssembly Core](https://www.w3.org/TR/wasm-core/)
- [WebAssembly specifications](https://webassembly.github.io/spec/)

Workflow:
1. Hash the exact module and validate its binary structure, imports, exports, memory/table declarations and custom sections.
2. Decode sections and WAT with a format-aware tool, preserving byte offsets and undecoded payloads. Version-dependent features must be interpreted against the module's applicable specification and tool support.
3. Trace imports/exports into the specific host embedding and JavaScript glue. A Wasm module alone does not establish network behavior, filesystem access or the host's permissions.
4. Treat names and source maps as optional metadata. WAT and recovered pseudocode are not source code; optimization and stripped names limit reconstruction.

## Game engines and packed assets

Sources:
- [Unity IL2CPP introduction](https://docs.unity.com/en-us/engine/6000.6/manual/programming-environment/scripting-backends/il2cpp/il2cpp-introduction)
- [Unreal Engine packaging](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-your-project)

Workflow:
1. Fingerprint the build and engine from reproducible file/metadata evidence; never infer engine solely from an executable filename.
2. For Unity, distinguish Mono managed assemblies from IL2CPP-generated native code. With IL2CPP, correlate native logic and available metadata, and explicitly report missing or stripped metadata.
3. For Unreal, distinguish executable logic, cooked assets, package/PAK or IoStore containers, and engine-version-specific serialization. Do not assume assets can be reconstructed into original editor projects.
4. Compare client-side states with authorized observed runtime behavior. Static client code cannot establish server-authoritative game rules.
5. Do not bypass anti-cheat, authentication or account controls as an implicit analysis step. Seek an authorized test artifact or offline copy when such boundaries prevent observation.

## Firmware and embedded images

Sources:
- [Binwalk upstream](https://github.com/ReFirmLabs/binwalk)
- [Binwalk extraction documentation](https://github.com/ReFirmLabs/binwalk/blob/master/README.md)

Workflow:
1. Inventory firmware image, header, candidate partitions, compression, filesystem boundaries and processor/board identity.
2. Validate each discovered magic signature against offsets, sizes and decompressed data; signature hits may be false positives.
3. Extract only into a dedicated new directory, with resource limits and safe path/symlink handling. Review extraction tools before executing them on untrusted input.
4. Identify bootloader, kernel, device tree, root filesystem and user-space binaries separately; static filesystem presence does not prove a service runs.
5. Note encryption, vendor signing and OTA delta packaging when content cannot be recovered from the provided image.

## Coverage-guided fuzzing and bug reproduction

Sources:
- [LLVM libFuzzer](https://llvm.org/docs/LibFuzzer.html)
- [LLVM structured fuzzing notes](https://llvm.org/docs/FuzzingLLVM.html)

Workflow:
1. Restrict fuzzing to an authorized isolated target and an explicitly defined parser/function harness.
2. Establish a known-good seed corpus and a deterministic baseline. Record compiler/sanitizer flags, harness, build identity and machine limits.
3. Use coverage feedback to expand inputs; distinguish coverage percentage from code correctness or exploitability.
4. Reduce and reproduce crashes independently, classify sanitizer traces and confirm a bug against the relevant source/assembly when possible.
5. Treat a non-crashing run as bounded evidence only; document corpus, duration, resource budgets and coverage gaps.

## Malware triage and pattern detection

Sources:
- [YARA-X documentation](https://virustotal.github.io/yara-x/docs/)
- [YARA-X rule guide](https://virustotal.github.io/yara-x/docs/writing_rules/anatomy-of-a-rule/)

Workflow:
1. Preserve hashes and chain of custody. Triage format, imports, packing indicators, strings and capabilities without launching the sample.
2. Run trusted scanners or YARA-X only in a suitable isolated environment; label every rule hit as a pattern match rather than proof of family, intent or execution.
3. Correlate patterns with code paths, configuration, embedded payloads and authorized sandbox traces. Do not extrapolate from one string.
4. Mark encrypted/polymorphic samples, anti-analysis behavior, missing dependencies and bounded execution time as major uncertainty.
5. Keep dangerous samples and derived payloads out of general-purpose repositories and user-facing deliverables unless explicitly authorized.

## Update and acceptance checklist

For a proposed addition to this skill:
- Is the source primary, reputable and directly linked to the exact claim?
- Is the technique applicable to a specified artifact type and version?
- Is it an REA tool advertised by the active server, an external CLI, or a conceptual workflow?
- Are prerequisites, permissions, side effects and observability limits stated?
- Is the result reusable and more useful than an ordinary web search at task time?
- Has the guidance been validated on a safe sample, or clearly labeled as documentation-only?

Do not silently invent support for new architectures, game engines, anti-cheat workarounds, or engines that the connected server does not advertise.
