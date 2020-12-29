---
title: การติดตั้งทรัพยากร
weight: 210
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการติดตั้ง
---

## เริ่มต้นการใช้งาน

1. ดาวน์โหลดและแตกไฟล์ลงในโฟลเดอร์ `resources` ของคุณ ชื่อของทรัพยากรจะต้องเป็น `azael_dc-whitelisted` ห้ามแก้ไขชื่อของทรัพยากรโดยเด็ดขาด เนื่องจากทรัพยากรจะไม่ทำงาน
2. เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_dc-whitelisted` ไว้ด้านล่าง [mysql-async][mysql-async] และ [es_extended][es_extended]
3. นำเข้าไฟล์ `azael_dc_whitelisted.sql` ไปยังฐานข้อมูลให้เรียบร้อย

## ยกเลิกการใช้งาน

1. เปิดไฟล์ `server.cfg` ค้นหา `ensure azael_dc-whitelisted`
2. ทำการเพิ่ม `#` ไว้ข้างหน้า `ensure azael_dc-whitelisted`

ตัวอย่าง:
```
#ensure azael_dc-whitelisted
```

[mysql-async]: https://github.com/brouznouf/fivem-mysql-async
[es_extended]: https://github.com/esx-framework/es_extended
