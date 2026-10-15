# เรียก Skill ผ่านหลายแชท โดยไม่ต้องติดตั้ง

Repo กลาง: https://github.com/appendix-xvi/reverse_engineer_skill

## สำหรับ ChatGPT แชทใหม่

ส่งข้อความ:

> อ่านไฟล์จริง `AGENTS.md` และ `.agents/skills/game-bot-reverse-engineering/SKILL.md` จาก `appendix-xvi/reverse_engineer_skill` รวมถึง references สำหรับเกมที่เกี่ยวข้องก่อนลงมือทำ ใช้ upstream REA SKILL เฉพาะเมื่อจำเป็น บอกผลที่ตรวจจริงกับสิ่งที่ยังไม่ตรวจให้ชัด ห้ามติดตั้งเครื่องมือเอง

หากอยากวิเคราะห์ REA แบบทั่วไป ไม่เกี่ยวกับเกม:

> อ่าน `.agents/skills/reverse-engineer-anything/SKILL.md` และ references ที่เกี่ยวข้องใน `appendix-xvi/reverse_engineer_skill` ก่อน แล้ววิเคราะห์ไฟล์ที่ฉันระบุโดยใช้เครื่องมือที่มีจริง

## สำหรับ Codex หรือเอเจนต์ที่เปิด repo นี้

อ่าน `AGENTS.md` เพื่อโหลดตามงาน; ไม่มีเหตุผลต้องติดตั้ง REA แค่เพื่อโหลดเอกสาร. หากต้องการให้ Codex ใช้ REA MCP/CLI ของจริงในอนาคต จะเป็นงานตั้งค่าแยก ซึ่งต้องตรวจและได้รับอนุญาตก่อน

## ข้อจำกัดสำคัญ

- GitHub centralizes instructions; a different chat will **not** automatically read them without explicit routing.
- GitHub repository is not a remote analysis engine or a hosted REA MCP.
- ChatGPT may have GitHub access but not a direct REA connection; say which execution tool was actually available.
- The full upstream skill is a **pinned snapshot**. It may become stale; see `UPSTREAM.md`.
- Do not guess JY/Digimon bot architecture, memory offsets, protocol or event conditions from Skill prose alone.

## คำสั่งตรวจเร็ว

User request: `ดึงสกิล reverse engineer มาใช้กับ DATS v9.98`.
Expected assistant behavior: open this repository, read AGENTS, game skill, Digimon reference and any relevant upstream reference, check available filesystem/tool access, inspect actual supplied files and report findings with evidence. If not accessible, state the blocker; do not invent results.
