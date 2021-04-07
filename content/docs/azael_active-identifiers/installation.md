---
title: การติดตั้งทรัพยากร
weight: 210
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการติดตั้ง
---

## เริ่มต้นการใช้งาน

1. ดาวน์โหลดและแตกไฟล์ลงในโฟลเดอร์ `resources` ของคุณ ชื่อของทรัพยากรจะต้องเป็น `azael_active-identifiers` ห้ามแก้ไขชื่อของทรัพยากรโดยเด็ดขาด เนื่องจากทรัพยากรจะไม่ทำงาน
2. เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_active-identifiers`

## ยกเลิกการใช้งาน

1. เปิดไฟล์ `server.cfg` ค้นหา `ensure azael_active-identifiers`
2. ทำการเพิ่ม `#` ไว้ข้างหน้า `ensure azael_active-identifiers`

ตัวอย่าง:
```
#ensure azael_active-identifiers
```

[mysql-async]: https://github.com/brouznouf/fivem-mysql-async
[es_extended]: https://github.com/esx-framework/es_extended
[esx_status]: https://github.com/esx-framework/esx_status
