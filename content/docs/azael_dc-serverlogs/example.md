---
title: การติดตั้งรหัสส่งข้อมูล
weight: 230
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับการติดตั้งรหัสเพื่อส่งข้อมูลจากทรัพยากรอื่น
---

## การติดตั้งรหัสส่งข้อมูลฝั่ง Server

การติดตั้งรหัสเพื่อส่งข้อมูลจากทรัพยากรอื่นฝั่ง Server

### ใช้งาน TriggerEvent

###### ภาษา Lua

```lua
local content = 'ข้อความที่ต้องการส่งไปยังทรัพยากร azael_dc-serverlogs'
TriggerEvent('azael_dc-serverlogs:insertData', 'eventName', content, source, 0, false)
```

###### ภาษา JavaScript

```js
const content = 'ข้อความที่ต้องการส่งไปยังทรัพยากร azael_dc-serverlogs';
emit('azael_dc-serverlogs:insertData', 'eventName', sendToDiscord, source, 0, false);
```

* **azael_dc-serverlogs:insertData**
    - ชื่อเหตุการณ์ทริกเกอร์ (Trigger) ระบุให้ตรงกับการตั้งค่าชื่อของ [Event](../config/#options)
* **eventName** 
    - ชื่อของ [event](../config/#events)
* **content**
    - ข้อความที่ต้องการส่งไปยังทรัพยากร [azael_dc-serverlogs](https://fivem.azael.dev/digishop/azael-dc-serverlogs/)
* **source**
    - ไอดีของผู้เล่นฝั่ง Server
* **0 (number | string)**
    - รหัส [color](../config/#colors) ของกล่องข้อความ (หากไม่ระบุ ค่าเริ่มต้นจะเป็น `0`)
* **public (boolean)**
    - หากกำหนดเป็น `true` จะปิดการเเสดงข้อมูลของผู้เล่นบนแอปพลิเคชัน [Discord](https://discord.com/) (หากไม่ระบุ ค่าเริ่มต้นจะเป็น `false`)

### ใช้งาน exports

###### ภาษา Lua

```lua
local content = 'ข้อความที่ต้องการส่งไปยังทรัพยากร azael_dc-serverlogs'
exports['azael_dc-serverlogs']:insertData('eventName', content, source, 0, false)
```

###### ภาษา JavaScript

```js
const content = 'ข้อความที่ต้องการส่งไปยังทรัพยากร azael_dc-serverlogs';
exports['azael_dc-serverlogs']['insertData']('eventName', content, source, 0, false);
```

* **insertData**
    - ฟังก์ชันที่ใช้ในการรับข้อมูลของทรัพยากร [azael_dc-serverlogs](https://fivem.azael.dev/digishop/azael-dc-serverlogs/)
* **eventName** 
    - ชื่อของ [event](../config/#events)
* **content**
    - ข้อความที่ต้องการส่งไปยังทรัพยากร [azael_dc-serverlogs](https://fivem.azael.dev/digishop/azael-dc-serverlogs/)
* **source**
    - ไอดีของผู้เล่นฝั่ง Server
* **0 (number | string)**
    - รหัส [color](../config/#colors) ของกล่องข้อความ (หากไม่ระบุ ค่าเริ่มต้นจะเป็น `0`)
* **public (boolean)**
    - หากกำหนดเป็น `true` จะปิดการเเสดงข้อมูลของผู้เล่นบนแอปพลิเคชัน [Discord](https://discord.com/) (หากไม่ระบุ ค่าเริ่มต้นจะเป็น `false`)

### ตัวอย่างการเพิ่มรหัส

ทรัพยากร `es_extended` ไปที่ `es_extended/server/main.lua`

##### ก่อนเพิ่มรหัส

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

##### หลังเพิ่มรหัส

```lua
RegisterNetEvent('esx:useItem')
AddEventHandler('esx:useItem', function(itemName)
    local xPlayer = ESX.GetPlayerFromId(source)
    local count = xPlayer.getInventoryItem(itemName).count
		
    if count > 0 then
        ESX.UseItem(source, itemName)

        local content = '' .. xPlayer.name .. ' ใช้ ' .. ESX.GetItemLabel(itemName) .. ' จำนวน 1 Ea.'
        TriggerEvent('azael_dc-serverlogs:insertData', 'UseItem', content, xPlayer.source, 3)
    else
        xPlayer.showNotification(_U('act_imp'))
    end
end)
```

### ตัวอย่างการตั้งค่า

ไปที่ `config/default/server.config.js`

##### ก่อนตั้งค่า

```js
AZAEL.SERVER.CONFIG.Events = {
    'Login': 'Discord Webhook URL - Login',                 // เข้าสู่เซิร์ฟเวอร์
    'Logout': 'Discord Webhook URL - Logout',               // ออกจากเซิร์ฟเวอร์
    'Chat': 'Discord Webhook URL - Chat',                   // ข้อความแชท
    'Dead': 'Discord Webhook URL - Dead'                    // สาเหตุการตาย
};
```

##### หลังตั้งค่า

```js
AZAEL.SERVER.CONFIG.Events = {
    'Login': 'Discord Webhook URL - Login',                 // เข้าสู่เซิร์ฟเวอร์
    'Logout': 'Discord Webhook URL - Logout',               // ออกจากเซิร์ฟเวอร์
    'Chat': 'Discord Webhook URL - Chat',                   // ข้อความแชท
    'Dead': 'Discord Webhook URL - Dead',                   // สาเหตุการตาย
    /* es_extended */
    'UseItem': 'Discord Webhook URL - Use Item'             // ใช้งาน-ไอเทม
};
```

{{% alert theme="info" %}}
ไม่ต้องกำหนดค่าต่างๆในส่วนนี้ หากคุณไม่ได้ เปิดการใช้งาน Discord - Webhooks ในการตั้งค่า [Options](../config/#options)
{{% /alert %}}

## การติดตั้งรหัสส่งข้อมูลฝั่ง Client

การติดตั้งรหัสเพื่อส่งข้อมูลจากทรัพยากรอื่นฝั่ง Client

### ใช้งาน TriggerServerEvent

###### ภาษา Lua

```lua
local content = 'ข้อความที่ต้องการส่งไปยังทรัพยากร azael_dc-serverlogs'
TriggerServerEvent('azael_dc-serverlogs:insertData', 'eventName', content, GetPlayerServerId(PlayerId()), 0, false)
```

###### ภาษา JavaScript

```js
const content = 'ข้อความที่ต้องการส่งไปยังทรัพยากร azael_dc-serverlogs';
emitNet('azael_dc-serverlogs:insertData', 'eventName', content, GetPlayerServerId(PlayerId()), 0, false);
```
* **azael_dc-serverlogs:insertData**
    - ชื่อเหตุการณ์ทริกเกอร์ (Trigger) ระบุให้ตรงกับการตั้งค่าชื่อของ [Event](../config/#options)
* **eventName** 
    - ชื่อของ [event](../config/#events)
* **content**
    - ข้อความที่ต้องการส่งไปยังทรัพยากร [azael_dc-serverlogs](https://fivem.azael.dev/digishop/azael-dc-serverlogs/)
* **GetPlayerServerId(PlayerId())**
    - ไอดีของผู้เล่นฝั่ง Client
* **0 (number | string)**
    - รหัส [color](../config/#colors) ของกล่องข้อความ (หากไม่ระบุ ค่าเริ่มต้นจะเป็น `0`)
* **public (boolean)**
    - หากกำหนดเป็น `true` จะปิดการเเสดงข้อมูลของผู้เล่นบนแอปพลิเคชัน [Discord](https://discord.com/) (หากไม่ระบุ ค่าเริ่มต้นจะเป็น `false`)

### ใช้งาน exports

###### ภาษา Lua

```lua
local content = 'ข้อความที่ต้องการส่งไปยังทรัพยากร azael_dc-serverlogs'
exports['azael_dc-serverlogs']:insertData('eventName', content, GetPlayerServerId(PlayerId()), 0, false)
```

###### ภาษา JavaScript

```js
const content = 'ข้อความที่ต้องการส่งไปยังทรัพยากร azael_dc-serverlogs';
exports['azael_dc-serverlogs']['insertData']('eventName', content, GetPlayerServerId(PlayerId()), 0, false);
```

* **insertData**
    - ฟังก์ชันที่ใช้ในการรับข้อมูลของทรัพยากร [azael_dc-serverlogs](https://fivem.azael.dev/digishop/azael-dc-serverlogs/)
* **eventName** 
    - ชื่อของ [event](../config/#events)
* **content**
    - ข้อความที่ต้องการส่งไปยังทรัพยากร [azael_dc-serverlogs](https://fivem.azael.dev/digishop/azael-dc-serverlogs/)
* **GetPlayerServerId(PlayerId())**
    - ไอดีของผู้เล่นฝั่ง Client
* **0 (number | string)**
    - รหัส [color](../config/#colors) ของกล่องข้อความ (หากไม่ระบุ ค่าเริ่มต้นจะเป็น `0`)
* **public (boolean)**
    - หากกำหนดเป็น `true` จะปิดการเเสดงข้อมูลของผู้เล่นบนแอปพลิเคชัน [Discord](https://discord.com/) (หากไม่ระบุ ค่าเริ่มต้นจะเป็น `false`)

### ตัวอย่างการเพิ่มรหัส

ทรัพยากร `esx_policejob` ไปที่ `esx_policejob/client/main.lua`

##### ก่อนเพิ่มรหัส

```lua
function ImpoundVehicle(vehicle)
	--local vehicleName = GetLabelText(GetDisplayNameFromVehicleModel(GetEntityModel(vehicle)))
	ESX.Game.DeleteVehicle(vehicle)
	ESX.ShowNotification(_U('impound_successful'))
	currentTask.busy = false
end
```

##### หลังเพิ่มรหัส

```lua
function ImpoundVehicle(vehicle)
    local content = '' .. GetPlayerName(PlayerId()) .. ' ส่ง พาหนะ ทะเบียน ' .. GetVehicleNumberPlateText(vehicle) .. ' ไปยังพาวท์'
    TriggerServerEvent('azael_dc-serverlogs:insertData', 'PoliceImpound', content, GetPlayerServerId(PlayerId()), 5)

	--local vehicleName = GetLabelText(GetDisplayNameFromVehicleModel(GetEntityModel(vehicle)))
	ESX.Game.DeleteVehicle(vehicle)
	ESX.ShowNotification(_U('impound_successful'))
	currentTask.busy = false
end
```

### ตัวอย่างการตั้งค่า

ไปที่ `config/default/server.config.js`

##### ก่อนตั้งค่า

```js
AZAEL.SERVER.CONFIG.Events = {
    'Login': 'Discord Webhook URL - Login',                 // เข้าสู่เซิร์ฟเวอร์
    'Logout': 'Discord Webhook URL - Logout',               // ออกจากเซิร์ฟเวอร์
    'Chat': 'Discord Webhook URL - Chat',                   // ข้อความแชท
    'Dead': 'Discord Webhook URL - Dead'                    // สาเหตุการตาย
};
```

##### หลังตั้งค่า

```js
AZAEL.SERVER.CONFIG.Events = {
    'Login': 'Discord Webhook URL - Login',                 // เข้าสู่เซิร์ฟเวอร์
    'Logout': 'Discord Webhook URL - Logout',               // ออกจากเซิร์ฟเวอร์
    'Chat': 'Discord Webhook URL - Chat',                   // ข้อความแชท
    'Dead': 'Discord Webhook URL - Dead',                   // สาเหตุการตาย
    /* esx_policejob */
    'PoliceImpound': 'Discord Webhook URL - Police Impound' // ตำรวจ: พาวท์-รถ
};
```

{{% alert theme="info" %}}
ไม่ต้องกำหนดค่าต่างๆในส่วนนี้ หากคุณไม่ได้ เปิดการใช้งาน Discord - Webhooks ในการตั้งค่า [Options](../config/#options)
{{% /alert %}}
