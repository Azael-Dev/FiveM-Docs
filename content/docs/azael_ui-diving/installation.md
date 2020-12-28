---
title: การติดตั้งทรัพยากร
weight: 210
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการติดตั้ง
---

## เริ่มต้นการใช้งาน

- ดาวน์โหลดและแตกไฟล์ลงในโฟลเดอร์ `resources` ของคุณ ชื่อของทรัพยากรจะต้องเป็น `azael_ui-diving` ห้ามแก้ไขชื่อของทรัพยากรโดยเด็ดขาด เนื่องจากทรัพยากรจะไม่ทำงาน
- เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_db-health&armor` ไว้ด้านล่าง [mysql-async][mysql-async], [es_extended][es_extended] และ [esx_status]
- สำหรับ [es_extended][es_extended] เวอร์ชั่น `1.1.x` นำเข้าไฟล์ `azael_diving-esx_limit.sql` ไปยังฐานข้อมูลให้เรียบร้อย
- สำหรับ [es_extended][es_extended] เวอร์ชั่น `1.2.x` นำเข้าไฟล์ `azael_diving-esx_weight.sql` ไปยังฐานข้อมูลให้เรียบร้อย

## ยกเลิกการใช้งาน

- เปิดไฟล์ `server.cfg` ค้นหา `ensure azael_ui-diving`
- ทำการเพิ่ม `#` ไว้ข้างหน้า `ensure azael_ui-diving`

ตัวอย่าง:
```
#ensure azael_ui-diving
```

[mysql-async]: https://github.com/brouznouf/fivem-mysql-async
[es_extended]: https://github.com/esx-framework/es_extended
[esx_status]: https://github.com/esx-framework/esx_status
