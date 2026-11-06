# Source skill families and adoption map

Reviewed 2026-11-06. These are upstream skill collections, not installed executables. The source repositories retain their own licenses and updates. This local skill integrates their domain workflows through independently authored routing; it does not reproduce every upstream file. Read exact upstream SKILL.md and any required references before adopting a task-specific procedure.

| Source collection | Upstream license | Skills / relevant scope | Apply to |
| --- | --- | --- | --- |
| [juzorei/game-re-skills](https://github.com/juzorei/game-re-skills/tree/main/skills) | MIT | [AOB signatures](https://github.com/juzorei/game-re-skills/tree/main/skills/aob-signatures), [pointer chains](https://github.com/juzorei/game-re-skills/tree/main/skills/cheat-engine-pointer-chains), [external memory readers](https://github.com/juzorei/game-re-skills/tree/main/skills/external-memory-reader), [patch recovery](https://github.com/juzorei/game-re-skills/tree/main/skills/game-patch-recovery), [Unity IL2CPP offsets](https://github.com/juzorei/game-re-skills/tree/main/skills/unity-il2cpp-offsets), [Unreal SDK offsets](https://github.com/juzorei/game-re-skills/tree/main/skills/unreal-sdk-offsets) | Patch-resistant process-state observation and game engine layouts |
| [as0ler/skills](https://github.com/as0ler/skills) | Apache-2.0 | [radare2](https://github.com/as0ler/skills/tree/main/radare2), [Frida](https://github.com/as0ler/skills/tree/main/frida), [r2frida](https://github.com/as0ler/skills/tree/main/r2frida), [Unreal 5](https://github.com/as0ler/skills/tree/main/unreal5), [deobfuscation](https://github.com/as0ler/skills/tree/main/deobfuscation) | Native analysis, authorized runtime instrumentation, structured engine inspection |
| [wshobson/agents](https://github.com/wshobson/agents/tree/main/plugins/reverse-engineering/skills) | MIT | [protocol RE](https://github.com/wshobson/agents/tree/main/plugins/reverse-engineering/skills/protocol-reverse-engineering), [binary patterns](https://github.com/wshobson/agents/tree/main/plugins/reverse-engineering/skills/binary-analysis-patterns), [memory forensics](https://github.com/wshobson/agents/tree/main/plugins/reverse-engineering/skills/memory-forensics), [anti-reversing techniques](https://github.com/wshobson/agents/tree/main/plugins/reverse-engineering/skills/anti-reversing-techniques) | Packet schemas, assembly control-flow, memory artifacts, analysis limitations |
| [zhaoxuya520/reverse-skill](https://github.com/zhaoxuya520/reverse-skill/tree/main/skills/reverse-engineering) | MIT | Broad RE reference: native and managed platforms, debugging, tool selection, binary diffing and deobfuscation | Investigations beyond a single specialized tool |
| [DohmBoy64Bit/windows-game-matching-decomp-skill](https://github.com/DohmBoy64Bit/windows-game-matching-decomp-skill) | MIT | Windows game matching decompilation, compiler identification, Unity/Unreal reconstruction and SDK design | Native-client reconstruction and controlled regression |
| [appendix-xvi/reverse_engineer_skill](https://github.com/appendix-xvi/reverse_engineer_skill/tree/main/.agents/skills/reverse-engineer-anything) | Project-local | REA integration, evidence ledger, target routing and specialist references | Canonical evidence acquisition and limits |

## How to use without silent capability inflation

1. Read the source skill for the selected task and inspect its license, linked files, commands and prerequisites.
2. Check whether the current agent actually has the proposed MCP tool, CLI, debugger, host access and target artifact. A written skill does not provide any of these.
3. Translate its method to the present artifact/version. Skip advice that assumes a different game engine, OS, target ownership or protection model.
4. Preserve primary evidence and test the implementation. Keep a clear chain from observation to offset, packet field, function or behavior.
5. Record source URL, specific revision or access date for each method adopted. Do not treat community recipes as established facts.

## Coverage gaps

The upstream collections focus mainly on reverse engineering, instrumentation and game memory. They do **not** collectively provide a complete, verified DMO/JY bot implementation. Bot state machines, quest/combat policies, navigation, transport lifecycle and regression fixtures must be designed against the actual client/server artifacts.
