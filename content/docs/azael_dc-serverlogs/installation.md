---
title: การติดตั้งทรัพยากร
weight: 210
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการติดตั้ง
---

## เริ่มต้นการใช้งาน

- ดาวน์โหลดและแตกไฟล์ลงในโฟลเดอร์ `resources` ของคุณ ชื่อของทรัพยากรจะต้องเป็น `azael_dc-serverlogs` ห้ามแก้ไขชื่อของทรัพยากรโดยเด็ดขาด เนื่องจากทรัพยากรจะไม่ทำงาน
- เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_dc-serverlogs` ไว้ด้านล่าง [es_extended][es_extended]

## ยกเลิกการใช้งาน

- เปิดไฟล์ `server.cfg` ค้นหา `ensure azael_dc-serverlogs`
- ทำการเพิ่ม `#` ไว้ข้างหน้า `ensure azael_dc-serverlogs`

ตัวอย่าง:
```
#ensure azael_dc-serverlogs
```

[es_extended]: https://github.com/esx-framework/es_extended
