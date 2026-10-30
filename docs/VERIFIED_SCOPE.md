# ขอบเขตที่ตรวจสอบจากระบบจริง

Repository: `intasan/tarot-3d-interactive`
ฐาน source ที่ตรวจ: `b00027f2fa874656783657b50e7ca1fb723c7c15`

**สถานะ: ผ่าน browser checks เฉพาะเลือกไพ่ เปลี่ยนไพ่ และเริ่มใหม่**

พัฒนาใหม่เป็น CSS 3D ที่ไม่พึ่ง CDN; ทดสอบเลือกไพ่ 2, reset และเลือกไพ่ 3 จาก browser จริงแล้ว ยังไม่ได้ตรวจมือถือจริงและทุก browser

## แหล่งหลักฐาน

- [evidence/source-audit.json](../evidence/source-audit.json)

## Traceability จาก source

| ไฟล์ที่ตรวจ | ขอบเขตที่ยืนยันได้ |
|---|---|
| [Tarot.html](../Tarot.html) | พบ source ใน commit ข้างต้น; การมีไฟล์ไม่ใช่การทดสอบผ่าน |

## เกณฑ์ตรวจรับ BA / SA

| เกณฑ์ | หลักฐาน / สถานะ |
|---|---|
| ขอบเขตปัจจุบันตรงกับ source | ผ่าน browser checks เฉพาะเลือกไพ่ เปลี่ยนไพ่ และเริ่มใหม่ |
| End-to-end ด้วยข้อมูลจริง | พัฒนาใหม่เป็น CSS 3D ที่ไม่พึ่ง CDN; ทดสอบเลือกไพ่ 2, reset และเลือกไพ่ 3 จาก browser จริงแล้ว ยังไม่ได้ตรวจมือถือจริงและทุก browser |
| ผลการทดสอบที่ทำซ้ำได้ | อ่าน command, stdout, exit code ใน evidence; syntax check ไม่ใช่ runtime test |
| ข้อมูลจริงและ provenance | เฉพาะราคาทองใน live-verification.txt ที่มี URL/เวลา publication; ไม่ใช้ fixture เป็นข้อมูลจริง |
| UAT โดยเจ้าของงานหรือผู้ใช้งาน | ยังไม่ได้ดำเนินการในรอบนี้ |

## ข้อจำกัดการแสดงผลงาน

ผล unit tests เป็นการตรวจ logic โดยมี fixture ตาม suite เดิม ไม่ใช่หลักฐานธุรกรรมจริง การฝึกโมเดลจริง การทำงานของอุปกรณ์จริง หรือการรับรองจากผู้ใช้ ไม่สร้างข้อมูลธุรกิจทดแทนข้อมูลที่ขาด และไม่อนุมานว่าไม่มีข้อมูลเท่ากับปลอดภัย


## Requirement และ traceability หลังพัฒนา

| Requirement | Implementation | ผลตรวจจริง |
|---|---|---|
| เลือกไพ่และเปิดข้อความ | Tarot.html: data-card click handler | เปิดใบ 2 และ 3 แล้วตรงกับ heading |
| เลือกได้ครั้งละใบ | aria-pressed บน card buttons | ใบ 2 reset กลับ false; ใบ 3 เป็น true |
| เริ่มใหม่ | #reset handler | คืน heading และ selected states แล้ว |
| ไม่ส่งข้อมูลส่วนตัว | ไม่มี network API หรือ storage | ตรวจ source; ไม่ใช่ penetration test |

Workflow: เลือกไพ่ → อัปเดต aria-pressed → CSS 3D flip และแสดงข้อความ → เปลี่ยนไพ่หรือเริ่มใหม่ ไม่มีฐานข้อมูลหรือผล UAT จากผู้ใช้จริง
