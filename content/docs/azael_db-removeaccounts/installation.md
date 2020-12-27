---
title: การติดตั้งทรัพยากร
weight: 210
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการติดตั้ง
---

## ติดตั้งและใช้งาน

- ดาวน์โหลดและแตกไฟล์ลงในโฟลเดอร์ `resources` ของคุณ ชื่อของทรัพยากรจะต้องเป็น `azael_db-removeaccounts` ห้ามแก้ไขชื่อของทรัพยากรโดยเด็ดขาด เนื่องจากทรัพยากรจะไม่ทำงาน
- เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_db-removeaccounts` ไว้ด้านล่าง [mysql-async][mysql-async] และ [azael_dc-whitelisted][azael_dc-whitelisted]

## ยกเลิกการใช้งาน

- เปิดไฟล์ `server.cfg` ค้นหา `ensure azael_db-removeaccounts`
- ทำการเพิ่ม `#` ไว้ข้างหน้า `ensure azael_db-removeaccounts`

ตัวอย่าง:
```
#ensure azael_db-removeaccounts
```

[mysql-async]: https://github.com/brouznouf/fivem-mysql-async
[azael_dc-whitelisted]: https://fivem.azael.dev/digishop/azael-dc-whitelisted
