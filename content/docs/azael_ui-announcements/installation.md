---
title: การติดตั้งทรัพยากร
weight: 210
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการติดตั้ง
---

## เริ่มต้นการใช้งาน

- ดาวน์โหลดและแตกไฟล์ลงในโฟลเดอร์ `resources` ของคุณ ชื่อของทรัพยากรจะต้องเป็น `azael_ui-announcements` ห้ามแก้ไขชื่อของทรัพยากรโดยเด็ดขาด เนื่องจากทรัพยากรจะไม่ทำงาน
- เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_ui-announcements`

## ยกเลิกการใช้งาน

- เปิดไฟล์ `server.cfg` ค้นหา `ensure azael_ui-announcements`
- ทำการเพิ่ม `#` ไว้ข้างหน้า `ensure azael_ui-announcements`

ตัวอย่าง:
```
#ensure azael_ui-announcements
```
