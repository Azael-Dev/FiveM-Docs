---
title: azael_dc-whitelisted
weight: 210
description: >
  คำถามที่พบบ่อยเกียวกับทรัพยากร azael_dc-whitelisted
---

## ไม่พบบัญชี Discord
ไม่พบบัญชี Discord กรุณาเปิดใช้งาน Discord และ FiveM ใหม่อีกครั้ง!

### แสดงไปยังผู้เล่นทุกคน
หากข้อความแสดงไปยังผู้เล่นทุกคน ให้ผู้ดูแลตรวจสอบที่ไฟล์ `server.cfg` หรือ `.cmd`, `.bat` ว่ามีการใช้งาน `set sv_lan 1` หรือไม่ หากมีการกำหนดค่านี้ ให้ดำเนินการ ปิดใช้งาน หรือ ลบออก เนื่องจาก `set sv_lan 1` เปรียบเสมือนการเปิดเซิร์ฟเวอร์แบบออฟไลน์ และจะไม่พึ่งพาบริการใดๆจากทาง [Cfx.re](https://cfx.re/) (ไม่สามารถเข้าถึงตัวระบุ [Discord](https://discord.com/) ได้ เนื่องจากเป็นบริการของทาง [Cfx.re](https://cfx.re/))

### แสดงเพียงผู้เล่นคนเดียว
หากข้อความแสดงเพียงผู้เล่นคนเดียว มีความจำเป็นที่จะต้องติดตั้งโปรแกรม [Discord สำหรับ PC](https://discord.com/download) เพื่อใช้ตรวจสอบสิทธิ์ในการเชื่อมต่อกับเซิร์ฟเวอร์ โปรดตรวจสอบให้เเน่ใจว่าคุณได้ติดตั้งโปรแกรม [Discord สำหรับ PC](https://discord.com/download) และได้ทำการเข้าสู่ระบบเรียบร้อยแล้ว หากคุณได้ทำการติดตั้งเรียบร้อยเเล้วและระบบยังเเสดงข้อความนี้อยู่ ให้ทำตามด้านล่างนี้ทีละขั้นตอน
1. ปิดใช้งาน FiveM และ [Discord สำหรับ PC](https://discord.com/download)
2. ถอนการติดตั้งโปรแกรม [Discord สำหรับ PC](https://discord.com/download) ให้เรียบร้อย
3. กดปุ่ม <kbd>Windows</kbd> **+** <kbd>R</kbd> พิมพ์ `%appdata%` คลิก OK และ ลบโฟลเดอร์ discord ทิ้ง
4. กดปุ่ม <kbd>Windows</kbd> **+** <kbd>R</kbd> พิมพ์ `%localappdata%` คลิก OK และ ลบโฟลเดอร์ Discord ทิ้ง
5. ดาวน์โหลด [Discord สำหรับ PC](https://discord.com/download) และดำเนินการติดตั้งใหม่
6. เข้าสู่ระบบบัญชี [Discord สำหรับ PC](https://discord.com/download) ให้เรียบร้อย
7. เปิด FiveM และ [Discord สำหรับ PC](https://discord.com/download) เพื่ออนุญาตสิทธิ์การเข้าถึงบัญชี Discord จาก FiveM

**วีดีโอตัวอย่าง:**
<iframe width="600" height="350" src="https://www.youtube.com/embed/akfmE3rKgpc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## สถานะ Discord (API) 401 หรือ 403
[Discord API](https://discord.com/developers/docs/intro) แสดงสถานะ 401 หรือ 403 ให้ผู้ดูแลเซิร์ฟเวอร์ตรวจสอบดังนี้
1. [Bot](../../azael_dc-whitelisted/application) อยู่ภายในกลุ่มบนชุมชน [Discord](https://discord.com/) หรือไม่?
2. [Bot Token](../../azael_dc-whitelisted/config/#discord_bot_token) ถูกต้องหรือไม่?
3. [Guild ID](../../azael_dc-whitelisted/config/#discord_guild_id) ถูกต้องหรือไม่? (ไอดีกลุ่ม)

## สถานะ Discord (API) 429
[Discord API](https://discord.com/developers/docs/intro) แสดงสถานะ 429 เกิดจากการใช้งาน [API](https://discord.com/developers/docs/intro) ของผู้ให้บริการ [Discord](https://discord.com/) ที่เกิน [Rate Limit](https://discord.com/developers/docs/topics/rate-limits) และถูกทางผู้ให้บริการระงับการใช้งาน API (การถูกระงับการใช้งานมี 2 รูปแบบดังนี้ **"ต่อเส้นทาง"** และ **"ทั่วโลก"**)

### ต่อเส้นทาง (Per-route)
มีการจำกัดที่ไม่ซ้ำกันสำหรับเส้นทางที่คุณกำลังเข้าถึงบน [API ของ Discord]((https://discord.com/developers/docs/intro)) ซึ่งบางครั้งรวมถึงวิธี HTTP (`GET`, `POST`, `PUT`, `DELETE`) และรวมถึงพารามิเตอร์หลักด้วย ซึ่งหมายความว่าเมธอด HTTP ที่แตกต่างกัน (เช่น ทั้ง `GET` และ `DELETE`) อาจใช้ขีดจำกัดเดียวกันหากเส้นทางเหมือนกัน นอกจากนี้ ขีดจำกัดยังคำนึงถึงพารามิเตอร์หลักใน URL ตัวอย่าง เช่น `/channels/:channel_id` และ `/channels/:channel_id/messages/:message_id` ทั้งคู่คำนึงถึง `channel_id` เนื่องจากเป็นพารามิเตอร์หลัก ปัจจุบันพารามิเตอร์หลักเพียงอย่างเดียวคือ `channel_id`, `guild_id` และ `webhook_id + webhook_token`

อาจ มีการแชร์ ขีดจำกัด **"ต่อเส้นทาง"** ในเส้นทางที่มีการใช้งานคล้ายกันหลายเส้นทาง (หรือแม้แต่เส้นทางเดียวกันกับวิธี HTTP ที่ต่างกัน) ตรวจสอบได้ที่ HTTP headers (`X-RateLimit-Bucket`) เพื่อแสดงถึงขีดจำกัด ([Discord](https://discord.com/) แนะนำให้ใช้ค่าส่วนหัวนี้เป็นตัวระบุเฉพาะสำหรับขีดจำกัด)

### ทั่วโลก (Global)
ทางผู้ให้บริการ [Discord](https://discord.com/) ระงับการใช้งาน API ทั้งหมด นั้นหมายถึง **"Bot"** หรือ **"Webhook"** จะไม่สามารถใช้งานได้ และ [Rate Limit](https://discord.com/developers/docs/topics/rate-limits) สูงสุดอยู่ที่ **10,000 ต่อ 10 นาที** (คำขอต่อเนื่องอยู่ที่ 16 หรือ 17 ต่อ วินาที) และ ที่อยู่ IP ที่สร้างคำขอ HTTP ที่ไม่ถูกต้องมากเกินไปจะถูกจำกัดไม่ให้เข้าถึง [Discord (API)](discord.com/developers/docs/intro) โดยอัตโนมัติ

{{% alert theme="info" %}}
สถานะ 429 จะหายไปเองตามเวลาที่ [Discord (API)](discord.com/developers/docs/intro) กำหนด (หากมีการใช้งาน API เกิน [Rate Limit](https://discord.com/developers/docs/topics/rate-limits) อีกครั้ง เวลาที่ถูกระงับการใช้งานจะเพิ่มขึ้น)
{{% /alert %}}
