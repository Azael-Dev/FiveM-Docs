---
title: แอปพลิเคชัน Discord
weight: 220
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับแอปพลิเคชัน Discord
---

### เปิดใช้งานโหมดผู้พัฒนา

- เปิดแอปพลิเคชัน Discord บน Desktop
- ไปที่ ตั้งค่า สัญลักษณ์ <i class="fas fa-cog"></i>
- เลือกเมนู หน้าตา เลื่อนลงไปด้านล่างจะพบหมวดหมู ขั้นสูง
- ดำเนินการ เปิดใช้โหมดผู้พัฒนา

![Enable discord developer mode](/azael_dc-whitelisted/enable-discord-developer-mode.gif "Enable discord developer mode")

### สร้างแอปพลิเคชัน (Bot)

- ไปยังเว็บไซต์ [Discord Developer Portal][discord-dev]
- คลิกปุ่ม `New Application`
- ระบุชื่อของแอปพลิเคชัน
- คลิกปุ่ม `Creat`
- เลือกเมนู `Bot`
- คลิกปุ่ม `Add Bot`
- คลิกปุ่ม `Yes, do it!`

![Creat discord application bot](/azael_dc-whitelisted/creat-discord-application-bot.gif "Creat discord application bot")

### เพิ่มบอทเข้ากลุ่ม Discord

- นำลิงก์ด้านล่างไประบุยัง URL เว็บเบราว์เซอร์
```
https://discordapp.com/oauth2/authorize?client_id=CLIENT_ID&scope=bot
```
- ไปยังเว็บไซต์ [Discord Developer Portal][discord-dev]
- เลือก แอปพลิเคชันที่สร้างไว้
- คัดลอก `CLIENT ID`
- แก้ไข `CLIENT_ID` ที่ลิงก์ URL เว็บเบราว์เซอร์ เป็น `CLIENT ID` ของแอปพลิเคชัน
- เลือกกลุ่ม และ ดำเนินการนำบอทเข้ากลุ่ม

![Add discord bot to guild](/azael_dc-whitelisted/add-discord-bot-to-guild.gif "Add discord bot to guild")

[discord]: https://discord.com
[discord-dev]: https://discord.com/developers/applications

