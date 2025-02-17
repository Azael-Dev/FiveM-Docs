---
title: คำสั่งการใช้งาน
weight: 240
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับคำสั่งการใช้งาน
---

## การใช้งานคำสั่ง

สามารถใช้คำสั่งผ่าน Server Console เเละ Live Console ของระบบ [txAdmin](https://docs.fivem.net/docs/resources/txAdmin/) หรือ ช่อง Chat กด <kbd>T</kbd> สำหรับฝั่ง Client โดยใช้ [ACE Permissions](https://forum.cfx.re/t/ace-permissions/107706/7?u=azael.dev) ในการอนุญาตสิทธิ์ในการใช้งานคำสั่ง

### ตรวจสอบ วันหมดอายุ และ Points

ผู้เล่น สามารถตรวจสอบวันหมดอายุของ Whitelist และ Points ได้ด้วยคำสั่งนี้

```lua
/wlexp
```

{{% alert theme="info" %}}
สามารถใช้คำสั่งนี้ได้ด้วยการกด <kbd>T</kbd> และพิมพ์ใช้คำสั่งผ่านช่องเเชทภายในเกมเท่านั้น
{{% /alert %}}

### ตรวจสอบ Queue

ผู้เล่น และ ผู้ดูแลระบบ สามารถตรวจสอบ คิวรอเข้าร่วมเซิร์ฟเวอร์ ได้ด้วยคำสั่งนี้

```lua
/wlqueue
```

### โหลด Hardware Banned

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อโหลด Hardware Banned (ในกรณีมีการแก้ไขไฟล์ hardware-bans.json)

```lua
/wlloadhardware
```

### โหลด Points (คิวชั้นที่ 1)

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อโหลด Points จากฐานข้อมูล สำหรับคิวชั้นที่ 1 (คิวรอเชื่อมต่อกับฐานข้อมูล)

```lua
/wlloadpoints
```

### เพิ่ม Whitelist

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อเพิ่มข้อมูล Whitelist ของผู้เล่นไปยัง Database (ในกรณี Discord API ล่ม และ ระบบไม่สามารถบันทึกข้อมูลของผู้เล่นใหม่ได้)

```lua
wladd ไอดีดิสคอส ไอดีตัวระบุ จำนวนวันหมดอายุของไวริส
```

ตัวอย่าง:

```lua
wladd 443334508020891658 steam:1100001332e7216 30
```

### ลบ Whitelist

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อลบข้อมูล Whitelist ของผู้เล่นบน Database ได้

```lua
wlremove ไอดีดิสคอส
```

ตัวอย่าง:

```lua
wlremove 443334508020891658
```

{{% alert theme="info" %}}
ในกรณี้นี้ ผู้เล่นยังสามารถเชื่อมต่อกับ Server ได้ เป็นเพียงการลบข้อมูลออกจาก Database เท่านั้น หากต้องการปลด Whitelist เเนะนำให้ปลดบทบาท Whitelist ในกลุ่ม Discord
{{% /alert %}}

### รีเซ็ต Identifier (ตัวระบุ)

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อรีเซ็ต Identifier ของ Whitelist สำหรับผู้เล่นที่ต้องการเปลี่ยน Identifier

```lua
wlreset ไอดีดิสคอส
```

ตัวอย่าง:

```lua
wlreset 443334508020891658
```

### เพิ่มวันใช้งาน

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อเพิ่มจำนวนวันใช้งาน Whitelist ของผู้เล่นได้

```lua
wladdday ไอดีดิสคอส จำนวนวันที่ต้องการเพิ่ม
```

ตัวอย่าง:

```lua
wladdday 443334508020891658 30
```

### ลดวันใช้งาน

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อลดจำนวนวันใช้งาน Whitelist ของผู้เล่นได้

```lua
wlreday ไอดีดิสคอส จำนวนวันที่ต้องการลด
```

ตัวอย่าง:

```lua
wlreday 443334508020891658 5
```

### เพิ่ม Points

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อเพิ่มจำนวน Points ให้กับผู้เล่นได้

**เพิ่ม Points**

```lua
wladdpoints ไอดีดิสคอส จำนวนเเต้ม
```

ตัวอย่าง:

```lua
wladdpoints 443334508020891658 1000
```

**เพิ่ม Points และ วันหมดอายุ**

```lua
wladdpoints ไอดีดิสคอส จำนวนเเต้ม จำนวนวันหมดอายุ
```

ตัวอย่าง:

```lua
wladdpoints 443334508020891658 1000 30
```

### ลด Points

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อลดจำนวน Points ของผู้เล่นได้

**ลด Points**

```lua
wlrepoints ไอดีดิสคอส จำนวนเเต้ม
```

ตัวอย่าง:

```lua
wlrepoints 443334508020891658 500
```

**ลด Points และ วันหมดอายุ**

```lua
wlrepoints ไอดีดิสคอส จำนวนเเต้ม จำนวนวันที่ต้องการลด
```

ตัวอย่าง:

```lua
wlrepoints 443334508020891658 500 15
```

### ระงับถาวร

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อระงับ Whitelist อย่างถาวร ทำให้ผู้เล่นไม่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้

```lua
wlban ไอดีดิสคอส เหตุผล
```

ตัวอย่าง:

```lua
wlban 443334508020891658 ใช้โปรแกรมช่วยเล่น
```

### ยกเลิกระงับถาวร

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อยกเลิกระงับ Whitelist อย่างถาวร ทำให้ผู้เล่นสามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้ตามปกติ

```lua
wlunban ไอดีดิสคอส
```

ตัวอย่าง:

```lua
wlunban 443334508020891658
```

### ยกเลิกระงับ (ไม่เข้าเซิร์ฟติดต่อกัน)

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อยกเลิกการระงับ Whitelist สำหรับผู้เล่นที่ไม่เชื่อมต่อเซิร์ฟเวอร์ติดต่อกันตามวันที่กำหนด

```lua
wlunhold ไอดีดิสคอส
```

ตัวอย่าง:

```lua
wlunhold 443334508020891658
```

### ตรวจสอบ Whitelist

ผู้ดูแลเซิร์ฟเวอร์ สามารถใช้คำสั่งนี้เพื่อตรวจสอบข้อมูล Whitelist ของผู้เล่น

```lua
wlcheck ไอดีดิสคอส
```

ตัวอย่าง:

```lua
wlcheck 443334508020891658
```
