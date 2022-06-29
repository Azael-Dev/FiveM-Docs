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

### `hardware_bans`

เปิดใช้งาน แบน Hardware (Tokens) สามารถเพิ่มรายการได้ที่ไฟล์ `hardware-bans.json`

```lua
Config['hardware_bans'] = false
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `identifier_license`

เปิดใช้งาน ตรวจสอบ R* License แทน Steam

```lua
Config['identifier_license'] = false
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน (ไม่แนะนำให้ใช้งาน R* License เนื่องจากเป็นตัวระบุผลิตภัณฑ์เกมประจำเครื่อง)
{{% /alert %}}

### `discord_api_auto`

เปิดใช้งาน ตรวจสอบ Discord API โดยอัตโนมัติ

```lua
Config['discord_api_auto'] = true
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `discord_api_timer`

เวลาในการตรวจสอบ Discord API โดยอัตโนมัติ (นาที)

```lua
Config['discord_api_timer'] = 1
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น
{{% /alert %}}

### `discord_api_down`

เปิดใช้งาน ตรวจสอบ Whitelist ใน Database แทน ในกรณี Discord ล้ม

```lua
Config['discord_api_down'] = false
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

{{% alert theme="info" %}}
ระบบจะทำการตรวจสอบว่าผู้เล่นที่เชื่อมต่อเซิร์ฟเวอร์ ว่ามีข้อมูลในตาราง azael_dc_whitelisted คอลั่มน์ Identifier หรือไม่ ในกรณีผู้เล่นที่ Admin พึ่งดำเนินการเพิ่มยศ หรือ บทบาท ในกลุ่ม Discord เเละ ผู้เล่นยังไม่มีข้อมูลบนฐานข้อมูล ตาราง azael_dc_whitelisted ผู้เล่นจะไม่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้ ผู้ดูแลระบบต้องใช้คำสั่ง [เพิ่ม Whitelist](../command/#เพม-whitelist) ให้ผู้เล่น ผู้เล่นจึงจะสามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้
<br><br>
คุณสามารถตรวจสอบสถานะ Discord ได้ที่ [Discord Status](https://discordstatus.com/)
{{% /alert %}}

### `discord_bot_token`

Discord Bot ที่ใช้ตรวจสอบบทบาทภายในกลุ่ม Discord

```lua
Config['discord_bot_token'] = 'Bot Token'
```

{{% alert theme="info" %}}
วิธีการรับ Token ของ Discord Bot ให้ไปที่ [Discord Developer Portal](https://discord.com/developers/applications/) เลือก แอปพลิเคชันที่สร้างไว้ เลือกเมนู Bot ดำเนินการ คัดลอก Token
{{% /alert %}}

![Check bot token](/resources/azael_dc-whitelisted/check_discord_bot_token.gif "Check bot token")

### `discord_guild_id`

รหัสกลุ่ม Discord ของเซิร์ฟเวอร์

```lua
Config['discord_guild_id'] = 'Guild ID'
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น
{{% /alert %}}

{{% alert theme="info" %}}
วิธีการรับรหัส ไปที่กลุ่ม Discord คลิกขวาที่รูปประจำตัวกลุ่ม และเลือก คัดลอก ID
{{% /alert %}}

![Check guild id](/resources/azael_dc-whitelisted/check_guild_id.gif "Check guild id")


### `discord_role_whitelist`

รหัสบทบาท Whitelist ในกลุ่ม Discord

```lua
Config['discord_role_whitelist'] = 'Whitelist Role ID'
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น
{{% /alert %}}

{{% alert theme="info" %}}
วิธีการรับรหัส ให้พิมพ์ในกลุ่ม @ชื่อบทบาทไวริส แล้วเพิ่มเครื่องหมาย \ ไว้ข้างหน้า <br> ยกตัวอย่าง: \\@ชื่อบทบาทไวริส
{{% /alert %}}

![Check role id](/resources/azael_dc-whitelisted/check_role_id.gif "Check role id")

### `discord_role_maintenance`

รหัสบทบาท Whitelist สำหรับ ผู้ดูแลระบบ ในกลุ่ม Discord

```lua
Config['discord_role_maintenance'] = 'Maintenance Role ID'
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น
{{% /alert %}}

{{% alert theme="info" %}}
วิธีการรับรหัส ให้พิมพ์ในกลุ่ม @ชื่อบทบาทไวริส แล้วเพิ่มเครื่องหมาย \ ไว้ข้างหน้า <br> ยกตัวอย่าง: \\@ชื่อบทบาทไวริส
{{% /alert %}}

![Check role id](/resources/azael_dc-whitelisted/check_role_id.gif "Check role id")

### `server_maintenance_enable`

Whitelist สำหรับ ผู้ดูแลระบบ ที่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้เท่านั้น เเละผู้เล่นที่มีบทบาท Whitelist จะไม่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้ หากผู้ดูแลระบบเปิดใช้งานการตั้งค่านี้

```lua
Config['server_maintenance_enable'] = false
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `discord_webhook`

Discord Logs (Webhook)

```lua
Config['discord_webhook'] = {
	['data'] = 'Webhook URL',			-- เก็บข้อมูลของผู้เล่น
	['alert'] = 'Webhook URL',			-- การเเจ้งเตือนต่างๆ
	['command'] = 'Webhook URL'			-- ประวัติการใช้งานคำสั่ง
}
```

### `url_community`

เปิดใช้งาน ลิงก์ชุมชนของเซิร์ฟเวอร์ จะเเสดงในกรณีผู้เล่นที่ไม่มี Whitelist เชื่อมต่อเซิร์ฟเวอร์ หรือ ข้อความที่ระบุให้ติดต่อกับผู้ดูแลเซิร์ฟเวอร์ได้ที่ใด

```lua
Config['url_community'] = true 
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `url_community_link`

ระบุ ลิงก์ชุมชนของเซิร์ฟเวอร์ จะเเสดงในกรณีผู้เล่นที่ไม่มี Whitelist เชื่อมต่อเซิร์ฟเวอร์ หรือ ข้อความที่ระบุให้ติดต่อกับผู้ดูแลเซิร์ฟเวอร์ได้ที่ใด

```lua
Config['url_community_link'] = 'https://discord.gg/invite'
```

### `anti_spam`

เปิดใช้งาน Anti Spam เพื่อป้องกันการฟลัด Discord API

```lua
Config['anti_spam'] = true
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `anti_spam_timer`

เวลา Anti Spam แบบสุ่ม เพื่อป้องกันผู้เล่นนับเวลาเข้าเซิร์ฟ (ระบุเป็น วินาที)

```lua
Config['anti_spam_timer'] = {
	['minimum'] = 10,
	['maximum'] = 30,
}
```

{{% alert theme="info" %}}
**minimum** เท่ากับ ขั้นต่ำ | **maximum** เท่ากับ สูงสุด
{{% /alert %}}

### `whitelist_expire`

เปิดใช้งาน ตรวจสอบวันหมดอายุ Whitelist เหมาะสำหรับเซิร์ฟเวอร์ที่เก็บค่าบริการ Whitelist

```lua
Config['whitelist_expire'] = false
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `whitelist_give_day`

จำนวนวันใช้งาน สำหรับการเชื่อมต่อเซิร์ฟเวอร์ในครั้งเเรกหลังจากที่เพิ่มยศ หรือ บทบาท Whitelist ให้ในกลุ่ม Discord

```lua
Config['whitelist_give_day'] = 30
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น
{{% /alert %}}

{{% alert theme="info" %}}
ในกรณี ปิดใช้งาน `whitelist_expire` (ตรวจสอบวันหมดอายุ Whitelist) ระบบจะทำการเพิ่มวันให้ 0 วัน โดยอัตโนมัติ
{{% /alert %}}

### `whitelist_onhold`

ตรวจผู้เล่นว่าเชื่อมต่อเซิร์ฟเวอร์ติดต่อกันตามวันที่เรากำหนดหรือไม่ หากไม่เชื่อมต่อเซิร์ฟเวอร์ติดต่อกัน ระบบจะทำการระงับ Whitelist ไว้ชั่วคราว

```lua
Config['whitelist_onhold'] = true
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `whitelist_onhold_limit`

จำนวนวันในการตรวจสอบผู้เล่น หากผู้เล่นไม่เชื่อมต่อเซิร์ฟเวอร์ติดต่อกันตามจำนวนวันที่ระบุ Whitelist ผู้เล่นจะถูกระงับโดยทันที (บทบาทในกลุ่ม Discord ยังคงสถานะ Whitelist)

```lua
Config['whitelist_onhold_limit'] = 7
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น
{{% /alert %}}

### `whitelist_onhold_queue_points`

เปิดใช้งาน ตรวจสอบผู้เล่นที่มี VIP Queue Points ที่ไม่เชื่อมต่อเซิร์ฟเวอร์ติดต่อกัน

```lua
Config['whitelist_onhold_queue_points'] = false
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `queue_bypass`

หากมี Slot ว่าง ผู้เล่นจะข้ามระบบ Queue ชั้นที่ 2 และ เข้าสู่เซิร์ฟเวอร์โดยทันที

```lua
Config['queue_bypass'] = true
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `queue_max_waiting`

จำกัดจำนวน Queue สูงสุด สำหรับการรอเชื่อมต่อกับเซิร์ฟเวอร์

```lua
Config['queue_max_waiting'] = {
	['enable'] = true,										-- เปิดใช้งาน จำกัดจำนวน Queue สูงสุด (true เท่ากับ เปิดใช้งาน | false เท่ากับ ปิดใช้งาน)
	['limit'] = {											-- จำกัดจำนวน Queue สูงสุด
		[0] = 250,											-- ผู้เล่นออนไลน์ 0 จำกัดจำนวน Queue สูงสุด 250
		[200] = 200,										-- ผู้เล่นออนไลน์ 200 จำกัดจำนวน Queue สูงสุด 200
		[400] = 150,										-- ผู้เล่นออนไลน์ 400 จำกัดจำนวน Queue สูงสุด 150
		[600] = 100,										-- ผู้เล่นออนไลน์ 600 จำกัดจำนวน Queue สูงสุด 100
		[800] = 50											-- ผู้เล่นออนไลน์ 800 จำกัดจำนวน Queue สูงสุด 50
	},
	['bypass'] = {
		['enable'] = false,									-- เปิดใช้งาน ในกรณีจำนวน Queue รอเชื่อมต่อกับเซิร์ฟเวอร์เต็ม ตัวระบุที่กำหนดด้านล่างนี้จะสามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้ (true เท่ากับ เปิดใช้งาน | false เท่ากับ ปิดใช้งาน)
		['identifier'] = {									-- ระบุ Identifier ที่สามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้ ในกรณีจำนวน Queue รอเชื่อมต่อกับเซิร์ฟเวอร์เต็ม (หากเปิดใช้งาน License แทน Steam ให้ระบุ Identifier เป็น License)
			'steam:001',
			'steam:002'
		}
	}
}
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `queue_points_expire`

เปิดใช้งาน VIP Queue Points วันหมดอายุของ Points ที่ใช้สำหรับการเชื่อมต่อเซิร์ฟเวอร์ก่อนผู้เล่นอื่นในระบบ Queue หากมี Points มากกว่ายิ่งมีสิทธิ์เข้าสู่เซิร์ฟเวอร์ได้ก่อนผู้เล่นที่มี Points น้อยกว่า

```lua
Config['queue_points_expire'] = true 
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `queue_refresh_client`

เวลาในการตรวจสอบผู้เล่นที่ทำการเชื่อมต่อ และ อัพเดทข้อความ (วินาที)

```lua
Config['queue_refresh_client'] = 3
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น
{{% /alert %}}

### `queue_update_points`

เวลาในการอัพเดท Points ให้ผู้เล่นระหว่างรอคิว ไม่มีผลกับ Points ในฐานข้อมูล (วินาที)

```lua
Config['queue_update_points']	= 6	
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น
{{% /alert %}}

### `queue_add_points`

จำนวน Points ที่ได้รับระหว่างรอคิวเชื่อมต่อเซิร์ฟเวอร์ ไม่มีผลกับ Points ในฐานข้อมูล (วินาที)

```lua
Config['queue_add_points'] = 1
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น
{{% /alert %}}

### `queue_bonus_points`

จำนวน Points ที่ได้รับ สำหรับผู้ที่มีอีโมจิเหมือนกัน 4 ตัว ไม่มีผลกับ Points ในฐานข้อมูล

```lua
Config['queue_bonus_points'] = 10
```

{{% alert theme="info" %}}
ระบุเฉพาะ **ตัวเลข** เท่านั้น | ระบุ 0 หากต้องการปิดการใช้งานการสุ่ม Emoji และ Bonus Points
{{% /alert %}}

### `queue_emoji_lists`

รายการ Emoji ของระบบ Queue

```lua
Config['queue_emoji_lists'] = {
	'❌',
	'⭕'
}
```

- [Emoji Unicode Tables](https://apps.timwhitlock.info/emoji/tables/unicode)

### `client_crashes`

หากผู้เล่นหลุดออกจากเซิร์ฟเวอร์ด้วยสาเหตุที่เกิดจากข้อผิดพลาดต่างๆ ผู้เล่นจะสามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้อีกครั้งโดยไม่ผ่าน ระบบคิว และ การตรวจสอบใดๆ

```lua
Config['client_crashes'] = {
	['enable'] = true,										-- เปิดใช้งาน ผู้เล่นสามารถเชื่อมต่อกับเซิร์ฟเวอร์ได้อีกครั้ง หากออกจากเซิร์ฟเวอร์อย่างไม่ถูกต้องจากข้อผิดพลาดต่างๆ (true เท่ากับ เปิดใช้งาน | false เท่ากับ ปิดใช้งาน)
	['timeout'] = 2,										-- ระบุ เวลาที่ผู้เล่นจะต้องเชื่อมต่อกับเซิร์ฟเวอร์ภายในเวลาที่กำหนด (นาที)
	['excepting'] = {										-- รายการที่ยกเว้น และ ไม่อยู่ในเงื่อนไขการผ่อนผัน (อ้างอิงจาก reason เหตุการณ์ playerDropped)
		'Disconnected',
		'Exiting',
		'Banned',
		'Kicked',
		'แบน',
		'เตะ'
	}
}
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `server_launcher`

อนุญาตให้ผู้เล่นเชื่อมกับเซิร์ฟเวอร์ผ่านทาง Launcher ของเซิร์ฟเวอร์เท่านั้น (หากเซิร์ฟเวอร์ของคุณมีการใช้งาน)

```lua
Config['server_launcher'] = {
	['enable'] = false,										-- เปิดใช้งาน ผู้เล่นสามารถเชื่อมต่อกับเซิร์ฟเวอร์ผ่านทาง Launcher ของเซิร์ฟเวอร์เท่านั้น (true เท่ากับ เปิดใช้งาน | false เท่ากับ ปิดใช้งาน)

	--- รับข้อมูลการเชื่อมต่อจากทรัพยากร Launcher
	--- @param identifier string ตัวระบุ steam หรือ license (ขึ้นอยู่กับการใช้งาน Config['identifier_license'])
	--- @return boolean boolean true หรือ false
	['connected'] = function(identifier)
		return exports['resource_name']:GetPlayerConnection(identifier)	-- ฟังก์ชันของทรัพยากร Launcher เพื่อใช้ในการตรวจสอบ
	end
}
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `adaptive_cards`

[Adaptive Cards](https://adaptivecards.io/) แสดงข้อมูลของผู้เล่นในขณะเชื่อมต่อกับเซิร์ฟเวอร์

```lua
Config['adaptive_cards'] = {								-- FiveM Adaptive Cards in Deferrals
	['enable'] = true,										-- เปิดใช้งาน Adaptive Cards เพื่อแสดงข้อมูลของผู้เล่นในขณะเชื่อมต่อกับเซิร์ฟเวอร์ (true เท่ากับ เปิดใช้งาน | false เท่ากับ ปิดใช้งาน)
	['disconnect'] = false,									-- หากผู้เล่นไม่คลิกที่ปุ่ม ยืนยันการเชื่อมต่อ ตามเวลาที่กำหนดในการตั้งค่า ['timeout'] ระบบจะตัดการเชื่อมต่อของผู้เล่นโดยทันที หากปิดใช้งาน การเชื่อมต่อจะเริ่มต้นโดยอัตโนมัติหากหมดเวลา (true เท่ากับ เปิดใช้งาน | false เท่ากับ ปิดใช้งาน)
	['timeout'] = 10,										-- เวลาในการแสดงข้อมูลของผู้เล่น หากหมดเวลา ระบบจะดำเนินการตามการตั้งค่า ['disconnect'] (วินาที)

	['card'] = {											-- ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้ (Adaptive Cards: https://adaptivecards.io)
		...
	}
}
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

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

ตรวจสอบวันหมดอายุของ Whitelist เเละ สถานะการ Ban ของผู้เล่นภายในเซิร์ฟเวอร์

```lua
Config['whitelist_realtime'] = {
	['enable'] = false,										-- เปิดใช้งาน ตรวจสอบการตรวจสอบ (true เท่ากับ เปิดใช้งาน | false เท่ากับ ปิดใช้งาน)
	['timer'] = 15											-- ระบุ เวลาในการตรวจสอบผู้เล่นที่อยู่ภายในเซิร์ฟเวอร์ (นาที)
}
```

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน<br>
{{% /alert %}}
