---
title: การตั้งค่าทรัพยากร
weight: 230
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการตั้งค่า
---

## การตั้งค่าฝั่ง Server

สามารถตั้งค่าได้ที่ไฟล์ `config.server.lua`

### `script_token`

ตัวระบุ API เพื่อใช้ในการตรวจสอบสิทธิ์การใช้งานของทรัพยากร ดูได้ที่ [สินค้าที่ซื้อ](https://fivem.azael.dev/dashboard/digishop)

```lua
Config['script_token'] = 'Token Key'
```

### `esx_routers`

เส้นทางกิจกรรมของทรัพยากร ESX Framework หาก es_extended เซิร์ฟเวอร์ของคุณ มีการแก้ไขชื่อกิจกรรมของทรัพยากร เพื่อป้องกันโปรแกรมโกงต่างๆ

```lua
Config['esx_routers'] = {
	['server_shared_obj'] = 'esx:getSharedObject'
}
```

{{% alert theme="info" %}}
ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

### `identifier_license`

เปิดใช้งาน ตรวจสอบ R* License แทน Steam

```lua
Config['identifier_license'] = false
```

- **true** = ใช้ตัวระบุ R* License
- **false** = ใช้ตัวระบุ Steam

{{% alert theme="info" %}}
หากเปิดใช้งาน ตรวจสอบ R* License จำเป็นที่จะต้องใช้งาน es_extended เวอร์ชั่น 1.2.0 ขึ้นไป (ไม่แนะนำให้ใช้งาน R* License)
{{% /alert %}}

### `discord_api_auto`

เปิดใช้งาน ตรวจสอบ Discord API โดยอัตโนมัติ

```lua
Config['discord_api_auto'] = true
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `discord_api_timer`

เวลาในการตรวจสอบ Discord API โดยอัตโนมัติ (นาที)

```lua
Config['discord_api_timer'] = 5
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

### `discord_api_down`

เปิดใช้งาน ตรวจสอบ Whitelist ใน Database แทน ในกรณี Discord ล้ม

```lua
Config['discord_api_down'] = false
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

{{% alert theme="info" %}}
ระบบจะทำการเช็คว่าผู้เล่นที่เชื่อมต่อเซิร์ฟเวอร์มีข้อมูล Identifier ในตาราง azael_dc_whitelisted หรือไม่ ในกรณีผู้เล่นที่ Admin พึ่งดำเนินการเพิ่มยศ หรือ บทบาท ในกลุ่ม Discord เเละ ยังไม่มีข้อมูลในฐานข้อมูลตาราง azael_dc_whitelisted ผู้เล่นจะไม่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้ คุณสามารถตรวจสอบสถานะ Discord ได้ที่ [Discord Status](https://status.discordapp.com)
<br><br>
หากกำหนด `Config['discord_api_down'] = true` แนะนำให้ไปกำหนดค่า `Config['discord_api_auto'] = false` เพื่อให้ทรัพยากรทำงานได้อย่างถูกต้อง 
{{% /alert %}}

### `discord_role_whitelist`

รหัสบทบาท Whitelist ในกลุ่ม Discord

```lua
Config['discord_role_whitelist'] = 'Role ID'
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

{{% alert theme="info" %}}
วิธีการรับรหัส ให้พิมพ์ในกลุ่ม @ชื่อบทบาทไวริส แล้วเพิ่มเครื่องหมาย \ ไว้ข้างหน้า <br> ยกตัวอย่าง: \\@ชื่อบทบาทไวริส
{{% /alert %}}

![Check role id](/resources/azael_dc-whitelisted/check_role_id.gif "Check role id")

### `discord_guild_id`

รหัสกลุ่ม Discord ของเซิร์ฟเวอร์

```lua
Config['discord_guild_id'] = 'Guild ID'
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

{{% alert theme="info" %}}
วิธีการรับรหัส ไปที่กลุ่ม Discord คลิกขวาที่รูปประจำตัวกลุ่ม และเลือก คัดลอก ID
{{% /alert %}}

![Check guild id](/resources/azael_dc-whitelisted/check_guild_id.gif "Check guild id")

### `discord_bot_token`

Discord Bot ที่ใช้ตรวจสอบบทบาทภายในกลุ่ม Discord

```lua
Config['discord_bot_token'] = 'Bot Token'
```

{{% alert theme="info" %}}
วิธีการรับ Token ของ Discord Bot ให้ไปที่ [Discord Developer Portal](https://discord.com/developers/applications/) เลือก แอปพลิเคชันที่สร้างไว้ เลือกเมนู Bot ดำเนินการ คัดลอก Token
{{% /alert %}}

![Check bot token](/resources/azael_dc-whitelisted/check_discord_bot_token.gif "Check bot token")

### `server_maintenance_enable`

Whitelist สำหรับ ผู้ดูแลระบบ ที่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้เท่านั้น เเละผู้เล่นที่มีบทบาท Whitelist จะไม่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้ หากผู้ดูแลระบบเปิดใช้งานการตั้งค่านี้

```lua
Config['server_maintenance_enable'] = false
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `discord_role_whitelist_maintenance`

รหัสบทบาท Whitelist สำหรับ ผู้ดูแลระบบ ในกลุ่ม Discord

```lua
Config['discord_role_whitelist_maintenance'] = 'Maintenance Role ID'
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

{{% alert theme="info" %}}
วิธีการรับรหัส ให้พิมพ์ในกลุ่ม @ชื่อบทบาทไวริส แล้วเพิ่มเครื่องหมาย \ ไว้ข้างหน้า <br> ยกตัวอย่าง: \\@ชื่อบทบาทไวริส
{{% /alert %}}

![Check role id](/resources/azael_dc-whitelisted/check_role_id.gif "Check role id")

### `discord_webhook_logs`

Discord Webhook URL สำหรับ เก็บข้อมูล Whitelist ของผู้เล่น

```lua
Config['discord_webhook_logs'] = 'Webhook Logs'
```

### `discord_webhook_alert`

Discord Webhook URL สำหรับ การเเจ้งเตือนสถานะ Whitelist

```lua
Config['discord_webhook_alert'] = 'Webhook Alert'
```

### `discord_webhook_command`

Discord Webhook URL สำหรับ การใช้งานคำสั่ง Whitelist

```lua
Config['discord_webhook_command'] = 'Webhook Command'
```

### `url_community`

เปิดใช้งาน ลิงก์ชุมชนของเซิร์ฟเวอร์ จะเเสดงในกรณีผู้เล่นที่ไม่มี Whitelist เชื่อมต่อเซิร์ฟเวอร์ หรือ ข้อความที่ระบุให้ติดต่อกับผู้ดูแลเซิร์ฟเวอร์ได้ที่ใด

```lua
Config['url_community'] = true 
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `url_community_link`

ระบุ ลิงก์ชุมชนของเซิร์ฟเวอร์ จะเเสดงในกรณีผู้เล่นที่ไม่มี Whitelist เชื่อมต่อเซิร์ฟเวอร์ หรือ ข้อความที่ระบุให้ติดต่อกับผู้ดูแลเซิร์ฟเวอร์ได้ที่ใด

```lua
Config['url_community_link'] = 'https://discord.gg/url'
```

### `anti_spam`

เปิดใช้งาน Anti Spam เพื่อป้องกันการฟลัด Discord API

```lua
Config['anti_spam'] = true
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `anti_spam_timer`

เวลา Anti Spam (วินาที เเนะนำ 15 วินาที ขึ้นไป)

```lua
Config['anti_spam_timer'] = 15
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

### `whitelist_expire`

เปิดใช้งาน ตรวจสอบวันหมดอายุ Whitelist เหมาะสำหรับเซิร์ฟเวอร์ที่เก็บค่าบริการ Whitelist

```lua
Config['whitelist_expire'] = false
```
- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `whitelist_give_day`

จำนวนวันใช้งาน สำหรับการเชื่อมต่อเซิร์ฟเวอร์ในครั้งเเรกหลังจากที่เพิ่มยศ หรือ บทบาท Whitelist ให้ในกลุ่ม Discord

```lua
Config['whitelist_give_day'] = 30
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

{{% alert theme="info" %}}
ในกรณี ปิดใช้งาน `whitelist_expire` (ตรวจสอบวันหมดอายุ Whitelist) ระบบจะทำการเพิ่มวันให้ 0 วัน โดยอัตโนมัติ
{{% /alert %}}

### `whitelist_onhold`

ตรวจผู้เล่นว่าเชื่อมต่อเซิร์ฟเวอร์ติดต่อกันตามวันที่เรากำหนดหรือไม่ หากไม่เชื่อมต่อเซิร์ฟเวอร์ติดต่อกัน ระบบจะทำการระงับ Whitelist ไว้ชั่วคราว

```lua
Config['whitelist_onhold'] = true
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `whitelist_onhold_limit`

จำนวนวันในการตรวจสอบผู้เล่น หากผู้เล่นไม่เชื่อมต่อเซิร์ฟเวอร์ติดต่อกันตามจำนวนวันที่ระบุ Whitelist ผู้เล่นจะถูกระงับโดยทันที (บทบาทในกลุ่ม Discord ยังคงสถานะ Whitelist)

```lua
Config['whitelist_onhold_limit'] = 7
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

### `whitelist_onhold_queue_point`

เปิดใช้งาน ตรวจสอบผู้เล่นที่มี VIP Queue Points ที่ไม่เชื่อมต่อเซิร์ฟเวอร์ติดต่อกัน

```lua
Config['whitelist_onhold_queue_point'] = false
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `queue_rocademption`

เปิดใช้งาน Queue - Rocademption ระบบที่ใช้สำหรับการรอเชื่อมต่อกับเซิร์ฟเวอร์ในกรณีที่เซิร์ฟเวอร์เต็ม ผู้เล่นจะต้องรอให้เซิร์ฟเวอร์ว่างก่อนจึงจะสามารถเชื่อมต่อเข้าไปยังเซิร์ฟเวอร์ได้

```lua
Config['queue_rocademption'] = true	
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `queue_point_expire`

เปิดใช้งาน VIP Queue Points วันหมดอายุของ Points ที่ใช้สำหรับการเชื่อมต่อเซิร์ฟเวอร์ก่อนผู้เล่นอื่นในระบบ Queue หากมี Points มากกว่ายิ่งมีสิทธิ์เข้าสู่เซิร์ฟเวอร์ได้ก่อนผู้เล่นที่มี Points น้อยกว่า

```lua
Config['queue_point_expire'] = true 
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `queue_max_server_slots`

จำนวนผู้เล่นสูงสุดของเซิร์ฟเวอร์ หากเปิดใช้งาน One Sync ให้ระบุ 256

```lua
Config['queue_max_server_slots'] = 256
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

### `queue_timer_refresh_client`

เวลาในการอัพเดท ข้อความ และ อิโมจิ (วินาที)

```lua
Config['queue_timer_refresh_client'] = 3
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

### `queue_timer_check_places`

เวลาในการตรวจสอบผู้เล่นที่ทำการเชื่อมต่อกับเซิร์ฟเวอร์ (วินาที)

```lua
Config['queue_timer_check_places'] = 3
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

### `queue_timer_update_points`

เวลาในการอัพเดท Points ให้ผู้เล่นระหว่างรอ Queue เชื่อมต่อเซิร์ฟเวอร์ (วินาที)

```lua
Config['queue_timer_update_points']	= 6	
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

### `queue_add_points`

จำนวน Points ที่ได้รับระหว่างรอคิวเชื่อมต่อเซิร์ฟเวอร์ (ไม่มีผลกับ Points ในฐานข้อมูล)

```lua
Config['queue_add_points'] = 1
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

### `queue_bonus_points`

จำนวน Points ที่ได้รับสำหรับผู้ที่มีอีโมจิ 3 ตัว (ไม่มีผลกับ Points ในฐานข้อมูล)

```lua
Config['queue_bonus_points'] = 25
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น

### `blacklisted_enable`

เปิดใช้งาน License Blacklisted

```lua
Config['blacklisted_enable'] = false
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `blacklisted_license`

ระบุ License ที่ต้องการขึ้นบัญชีดำ (จะไม่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้)

```lua
Config['blacklisted_license'] = {
	'license:001',
	'license:002',
	'license:003',
	'license:004',
	'license:005'
}
```

## การตั้งค่าฝั่ง Client

สามารถตั้งค่าได้ที่ไฟล์ `config.client.lua`

### `esx_routers`

เส้นทางกิจกรรมของทรัพยากร ESX Framework หาก es_extended เซิร์ฟเวอร์ของคุณ มีการแก้ไขชื่อกิจกรรมของทรัพยากร เพื่อป้องกันโปรแกรมโกงต่างๆ

```lua
Config['esx_routers'] = {
	['client_player_load'] = 'esx:playerLoaded'
}	
```

{{% alert theme="info" %}}
ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

### `whitelist_realtime`

ตรวจสอบ วันหมดอายุ และ สถานะการ Ban ของ Whitelist สำหรับผู้เล่นที่อยู่ภายในเกม หาก Whitelist หมดอายุ หรือ ถูก Ban ระบบจะทำการ"เตะ"ผู้เล่นออกจากเกมโดยอัตโนมัติ

```lua
Config['whitelist_realtime'] = true
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `whitelist_realtime_timer`

เวลาในการตรวจสอบ วันหมดอายุ และ สถานะการ Ban ของ Whitelist สำหรับผู้เล่นที่อยู่ภายในเกม (นาที)

```lua
Config['whitelist_realtime_timer'] = 15	
```

- ระบุเฉพาะ **ตัวเลข** เท่านั้น
