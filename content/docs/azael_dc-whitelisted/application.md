---
title: แอปพลิเคชัน Discord
weight: 220
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับแอปพลิเคชัน Discord
---

### เปิดใช้งานโหมดผู้พัฒนา

1. เปิดแอปพลิเคชัน Discord บน Desktop
2. ไปที่ ตั้งค่า สัญลักษณ์ <i class="fas fa-cog"></i>
3. เลือกเมนู หน้าตา เลื่อนลงไปด้านล่างจะพบหมวดหมู ขั้นสูง
4. ดำเนินการ เปิดใช้โหมดผู้พัฒนา

![Enable discord developer mode](/azael_dc-whitelisted/enable-discord-developer-mode.gif "Enable discord developer mode")

### สร้างแอปพลิเคชัน (Bot)

1. ไปยังเว็บไซต์ [Discord Developer Portal][discord-dev]
2. คลิกปุ่ม `New Application`
3. ระบุชื่อของแอปพลิเคชัน
4. คลิกปุ่ม `Creat`
5. เลือกเมนู `Bot`
6. คลิกปุ่ม `Add Bot`
7. คลิกปุ่ม `Yes, do it!`

![Creat discord application bot](/azael_dc-whitelisted/creat-discord-application-bot.gif "Creat discord application bot")

### เพิ่มบอทเข้ากลุ่ม Discord

1. นำลิงก์ด้านล่างไประบุยัง URL เว็บเบราว์เซอร์
```
https://discordapp.com/oauth2/authorize?client_id=CLIENT_ID&scope=bot
```
2. ไปยังเว็บไซต์ [Discord Developer Portal][discord-dev]
3. เลือก แอปพลิเคชันที่สร้างไว้
4. คัดลอก `CLIENT ID`
5. แก้ไข `CLIENT_ID` ที่ลิงก์ URL เว็บเบราว์เซอร์ เป็น `CLIENT ID` ของแอปพลิเคชัน
6. เลือกกลุ่ม และ ดำเนินการนำบอทเข้ากลุ่ม

![Add discord bot to guild](/azael_dc-whitelisted/add-discord-bot-to-guild.gif "Add discord bot to guild")

[discord]: https://discord.com
[discord-dev]: https://discord.com/developers/applications
