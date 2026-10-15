# Reverse Engineering Skills — JY Online & Digimon

คลัง Skill กลางสำหรับ ChatGPT/Codex เพื่อใช้แนวทาง Reverse Engineering ซ้ำได้จากหลายแชท โดยไม่ต้องติดตั้ง REA เพียงเพื่ออ่านเอกสาร

## เริ่มจากตรงไหน

1. อ่าน [AGENTS.md](AGENTS.md) เพื่อเลือกขั้นตอนและข้อจำกัดให้ถูกงาน
2. อ่าน [Game Bot Reverse Engineering Skill](.agents/skills/game-bot-reverse-engineering/SKILL.md) สำหรับบอท JY Online หรือ Digimon
3. อ่าน [REA upstream Skill](.agents/skills/reverse-engineer-anything/SKILL.md) และ `references/` เมื่อต้องการวิธีใช้ REA ตามต้นฉบับ
4. อ่าน [UPSTREAM.md](UPSTREAM.md) สำหรับที่มา, pinned commit, license และการอัปเดต

## เรียกใช้จากแชทใหม่

> อ่าน `AGENTS.md` และ `.agents/skills/game-bot-reverse-engineering/SKILL.md` ใน `appendix-xvi/reverse_engineer_skill` ก่อน แล้วใช้แนวทางนี้วิเคราะห์บอท Digimon ที่ฉันระบุ พร้อมแยกสิ่งที่ตรวจพบจริง / ข้อสันนิษฐาน / สิ่งที่ยังไม่ทราบ ห้ามอ้างว่ารันเครื่องมือที่ไม่ได้รัน

สำหรับ JY ให้เปลี่ยนคำว่า Digimon เป็น JY Online และเลือกไฟล์อ้างอิงตามเกมนั้น

## ขอบเขตและข้อเท็จจริง

- **Skill ใน GitHub คือเอกสารวิธีทำงาน** ไม่ใช่ MCP server, decompiler หรือเครื่องมือสำหรับอ่าน memory
- การเปิดอ่าน Skill ผ่าน GitHub สามารถทำได้โดยไม่ต้องติดตั้ง REA
- การใช้งาน REA จริงจำเป็นต้องมี REA CLI/MCP ที่เข้าถึงไฟล์เป้าหมายและ provider ที่เหมาะสม; ยังไม่ได้ติดตั้งอะไรบนเครื่องผู้ใช้
- การเรียกใช้ข้ามแชทไม่เกิดอัตโนมัติ: แชท/เอเจนต์ต้องได้รับคำสั่งให้อ่าน repository นี้ หรือมี configuration ของตนที่ชี้มาที่นี่
- เก็บผลวิเคราะห์พร้อมหลักฐานต้นทางและเวอร์ชันไฟล์; ห้ามเดาว่ามีฟีเจอร์เพราะ README ของเครื่องมือบอกว่ารองรับ
- ห้าม commit game binaries, raw memory dumps, packets ที่มี secret, credentials หรือไฟล์ proprietary ที่ไม่มีสิทธิ์เผยแพร่

## Upstream

REA: https://github.com/morluto/rea

REA-authored Skill และ references ที่คัดลอกมาอยู่ใต้ `.agents/skills/reverse-engineer-anything/` พร้อมใบอนุญาตที่ `licenses/REA-MIT-LICENSE`. อ่าน [UPSTREAM.md](UPSTREAM.md) สำหรับ commit ที่ใช้เก็บ snapshot
