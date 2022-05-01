---
title: การติดตั้งรหัสทริกเกอร์
weight: 230
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับการติดตั้งรหัสทริกเกอร์
---

## การติดตั้งรหัสทริกเกอร์ฝั่ง Server

การติดตั้งรหัสทริกเกอร์ (Trigger) เพื่อรับกิจกรรม (Event) จากทรัพยากรอื่นฝั่ง Server

### รหัสทริกเกอร์ฝั่ง Server

###### ภาษา Lua

```lua
local sendToDiscord = 'ข้อความที่ต้องการส่งไปยัง Discord'
TriggerEvent('azael_dc-serverlogs:sendToDiscord', 'eventName', sendToDiscord, source, '^1')
```

###### ภาษา JavaScript

```js
const sendToDiscord = 'ข้อความที่ต้องการส่งไปยัง Discord';
emit('azael_dc-serverlogs:sendToDiscord', 'eventName', sendToDiscord, source, '^1');
```

### รายละเอียดรหัสทริกเกอร์ฝั่ง Server

* **azael_dc-serverlogs:sendToDiscord**
    - ชื่อเหตุการณ์ทริกเกอร์ (Trigger) ให้ระบุตรงกับ [Event](../config/#options) หากมีการแก้ไขการตั้งค่า
* **eventName** 
    - ชื่อของ [event](../config/#Events)
* **sendToDiscord**
    - ข้อความที่ต้องการส่งไปยังกลุ่ม Discord
* **source**
    - ไอดีของผู้เล่นฝั่ง Server
* **^1**
    - รหัส [color](../config/#colors) ของกล่องข้อความ

### ตัวอย่างการเพิ่มรหัสทริกเกอร์ฝั่ง Server

ทรัพยากร `es_extended` ไปที่ `es_extended/server/main.lua`

##### ก่อนเพิ่มรหัสทริกเกอร์

```lua
RegisterNetEvent('esx:useItem')
AddEventHandler('esx:useItem', function(itemName)
    local xPlayer = ESX.GetPlayerFromId(source)
    local count = xPlayer.getInventoryItem(itemName).count
	
    if count > 0 then
        ESX.UseItem(source, itemName)
    else
        xPlayer.showNotification(_U('act_imp'))
    end
end)
```

##### หลังเพิ่มรหัสทริกเกอร์

```lua
RegisterNetEvent('esx:useItem')
AddEventHandler('esx:useItem', function(itemName)
    local xPlayer = ESX.GetPlayerFromId(source)
    local count = xPlayer.getInventoryItem(itemName).count
		
    if count > 0 then
        ESX.UseItem(source, itemName)

        local sendToDiscord = '' .. xPlayer.name .. ' ใช้ ' .. ESX.GetItemLabel(itemName) .. ' จำนวน 1 Ea.'
        TriggerEvent('azael_dc-serverlogs:sendToDiscord', 'UseItem', sendToDiscord, xPlayer.source, '^3')
    else
        xPlayer.showNotification(_U('act_imp'))
    end
end)
```

### ตัวอย่างการตั้งค่า Webhook ฝั่ง Server

ไปที่ `config/default/server.config.js`

##### ก่อนตั้งค่า Webhook

```js
AZAEL.SERVER.CONFIG.Events = {
    'Login': 'Discord Webhook URL - Login',                 // เข้าสู่เซิร์ฟเวอร์
    'Logout': 'Discord Webhook URL - Logout',               // ออกจากเซิร์ฟเวอร์
    'Chat': 'Discord Webhook URL - Chat',                   // ข้อความแชท
    'Dead': 'Discord Webhook URL - Dead'                    // สาเหตุการตาย
};
```

##### หลังตั้งค่า Webhook

```js
AZAEL.SERVER.CONFIG.Events = {
    'Login': 'Discord Webhook URL - Login',                 // เข้าสู่เซิร์ฟเวอร์
    'Logout': 'Discord Webhook URL - Logout',               // ออกจากเซิร์ฟเวอร์
    'Chat': 'Discord Webhook URL - Chat',                   // ข้อความแชท
    'Dead': 'Discord Webhook URL - Dead',                   // สาเหตุการตาย
    'UseItem': 'Discord Webhook URL - Use Item'            // สาเหตุการตาย
};
```

{{% alert theme="info" %}}
ไม่ต้องกำหนดค่าต่างๆในส่วนนี้ หากคุณไม่ได้ เปิดการใช้งาน Discord - Webhooks ในการตั้งค่า [Options](../config/#options)<br>
บรรทัดสุดท้ายจะต้องไม่มีเครื่องหมาย <kbd>,</kbd> เพราะอาจจะทำให้เกิดข้อผิดพลาดได้
{{% /alert %}}

## การติดตั้งรหัสทริกเกอร์ฝั่ง Client

การติดตั้งรหัสทริกเกอร์ (Trigger) เพื่อรับเหตุการณ์ (Event) จากทรัพยากรอื่นฝั่ง Client

### รหัสทริกเกอร์ฝั่ง Client

###### ภาษา Lua

```lua
local sendToDiscord = 'ข้อความที่ต้องการส่งไปยัง Discord'
TriggerServerEvent('azael_dc-serverlogs:sendToDiscord', 'eventName', sendToDiscord, GetPlayerServerId(PlayerId()), '^1')
```

###### ภาษา JavaScript

```js
const sendToDiscord = 'ข้อความที่ต้องการส่งไปยัง Discord';
emitNet('azael_dc-serverlogs:sendToDiscord', 'eventName', sendToDiscord, GetPlayerServerId(PlayerId()), '^1');
```

### รายละเอียดรหัสทริกเกอร์ฝั่ง Client

* **azael_dc-serverlogs:sendToDiscord**
    - ชื่อเหตุการณ์ทริกเกอร์ (Trigger) ให้ระบุตรงกับ [Event](../config/#options) หากมีการแก้ไขการตั้งค่า
* **eventName** 
    - ชื่อของ [event](../config/#Events)
* **sendToDiscord**
    - ข้อความที่ต้องการส่งไปยังกลุ่ม Discord
* **GetPlayerServerId(PlayerId())**
    - ไอดีของผู้เล่นฝั่ง Client
* **^1**
    - รหัส [color](../config/#colors) ของกล่องข้อความ

### ตัวอย่างการเพิ่มรหัสทริกเกอร์ฝั่ง Client

ทรัพยากร `esx_policejob` ไปที่ `esx_policejob/client/main.lua`

##### ก่อนเพิ่มรหัสทริกเกอร์

```lua
function ImpoundVehicle(vehicle)
	--local vehicleName = GetLabelText(GetDisplayNameFromVehicleModel(GetEntityModel(vehicle)))
	ESX.Game.DeleteVehicle(vehicle)
	ESX.ShowNotification(_U('impound_successful'))
	currentTask.busy = false
end
```

##### หลังเพิ่มรหัสทริกเกอร์

```lua
function ImpoundVehicle(vehicle)
    local sendToDiscord = '' .. GetPlayerName(PlayerId()) .. ' ส่ง พาหนะ ทะเบียน ' .. GetVehicleNumberPlateText(vehicle) .. ' ไปยังพาวท์'
    TriggerServerEvent('azael_dc-serverlogs:sendToDiscord', 'PoliceImpound', sendToDiscord, GetPlayerServerId(PlayerId()), '^5')

	--local vehicleName = GetLabelText(GetDisplayNameFromVehicleModel(GetEntityModel(vehicle)))
	ESX.Game.DeleteVehicle(vehicle)
	ESX.ShowNotification(_U('impound_successful'))
	currentTask.busy = false
end
```

### ตัวอย่างการตั้งค่า Webhook ฝั่ง Client

ไปที่ `config/default/server.config.js`

##### ก่อนตั้งค่า Webhook

```js
AZAEL.SERVER.CONFIG.Events = {
    'Login': 'Discord Webhook URL - Login',                 // เข้าสู่เซิร์ฟเวอร์
    'Logout': 'Discord Webhook URL - Logout',               // ออกจากเซิร์ฟเวอร์
    'Chat': 'Discord Webhook URL - Chat',                   // ข้อความแชท
    'Dead': 'Discord Webhook URL - Dead'                    // สาเหตุการตาย
};
```

##### หลังตั้งค่า Webhook

```js
AZAEL.SERVER.CONFIG.Events = {
    'Login': 'Discord Webhook URL - Login',                 // เข้าสู่เซิร์ฟเวอร์
    'Logout': 'Discord Webhook URL - Logout',               // ออกจากเซิร์ฟเวอร์
    'Chat': 'Discord Webhook URL - Chat',                   // ข้อความแชท
    'Dead': 'Discord Webhook URL - Dead',                   // สาเหตุการตาย
    'PoliceImpound': 'Discord Webhook URL - Police Impound' // ตำรวจ: ส่งพาหนะไปพาวท์
};
```

{{% alert theme="info" %}}
ไม่ต้องกำหนดค่าต่างๆในส่วนนี้ หากคุณไม่ได้ เปิดการใช้งาน Discord - Webhooks ในการตั้งค่า [Options](../config/#options)<br>
บรรทัดสุดท้ายจะต้องไม่มีเครื่องหมาย <kbd>,</kbd> เพราะอาจจะทำให้เกิดข้อผิดพลาดได้
{{% /alert %}}

## การใช้งาน Custom - Webhooks
การส่งข้อมูลบันทึกกิจกรรมต่างๆไปยังเซิร์ฟเวอร์ที่กำหนดเอง สามารถเปิดการใช้งาน Custom - Webhooks ในการตั้งค่า [Options](../config/#options)

### ตัวอย่าง HTTP POST Request
ข้อมูลจะถูกส่งออกในรูปแบบ [JSON](https://en.wikipedia.org/wiki/JSON) ดังตัวอย่างด้านล่างนี้

```json
{
    "event": "Login",
    "color": "#99CC00",
    "content": "เข้าสู่เซิร์ฟเวอร์",
    "screenshot": "https://media.discordapp.net/attachments/819858829884915753/845634322181914664/screenshot.jpg",
    "timestamp": 1621685334,
    "player": {
       "id": 1,
       "ip": "ip:192.168.1.101",
       "license": "license:c89b466e4624e53d972f5dd188fa53c34689e653",
       "discord": "discord:443334508020891658",
       "steam": "steam:1100001332e7216",
       "steam_name": "Azael Dev",
       "steam_profile": "https://steamcommunity.com/profiles/76561198818947606",
       "steam_avatar": "https://cdn.cloudflare.steamstatic.com/steamcommunity/public/images/avatars/93/93178f63ab1be3720d78340a72ca518798ca6707_full.jpg"
    }
}
```

| Name                  | Possible Values        | Description              |
|---------------------- |------------------------|--------------------------|
| event                 | string                 | ชื่อของเหตุการณ์             |
| color                 | string                 | รหัสสี                     |
| content               | string                 | เนื้อหา                    |
| screenshot            | string หรือ string ว่าง  | ภาพหน้าจอ                 |
| timestamp             | number                 | วันและเวลา (unix)          |
| player                | object                 | ข้อมูลรูปแบบวัตถุ             |
| id                    | number                 | source                   |
| ip                    | string                 | ip ที่ใช้งาน                |
| license               | string                 | ตัวระบุ rockstar           |
| discord               | string หรือ string ว่าง  | ตัวระบุ discord            |
| steam                 | string                 | ตัวระบุ steam              |
| steam_name            | string                 | ชื่อ steam                 |
| steam_profile         | string                 | ลิงก์โปรไฟล์ steam          |
| steam_avatar          | string                 | รูปโปรไฟล์ steam           |

{{% alert theme="info" %}}
สำหรับ API ในการรับข้อมูล และ Client ที่ใช้ในการตรวจสอบข้อมูล ยังอยู่ระหว่างการพัฒนา 
{{% /alert %}}
