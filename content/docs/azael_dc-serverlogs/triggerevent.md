---
title: การติดตั้งรหัสทริกเกอร์
weight: 230
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับการติดตั้งรหัสทริกเกอร์
---

## การติดตั้งรหัสทริกเกอร์ฝั่ง Server

การติดตั้งรหัสทริกเกอร์ (Trigger) เพื่อรับกิจกรรม (Event) จากทรัพยากรอื่นฝั่ง Server

### รหัสทริกเกอร์ฝั่ง Server
```lua
local sendToDiscord = 'ข้อความที่ต้องการส่งไปยัง Discord'
TriggerEvent('azael_discordlogs:sendToDiscord', 'EventName', sendToDiscord, source, '^1')
```

### รายละเอียดรหัสทริกเกอร์ฝั่ง Server

* **azael_discordlogs:sendToDiscord**
    - ชื่อเหตุการณ์ทริกเกอร์ (Trigger) ให้ระบุตรงกับ [event_name](../config/#event_name) หากมีการแก้ไขการตั้งค่า
* **EventName** 
    - ชื่อของ Webhook ที่ตั้งค่าใน `config.server.lua`
* **sendToDiscord**
    - ข้อความที่ต้องการส่งไปยังกลุ่ม Discord
* **source**
    - ไอดีของผู้เล่นฝั่ง Server
* **^1**
    - รหัสแถบสีของกล่องข้อความ สามารถดูรหัสสีได้ที่ไฟล์ `config.server.lua`

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
        TriggerEvent('azael_discordlogs:sendToDiscord', 'UseItem', sendToDiscord, xPlayer.source, '^3')
    else
        xPlayer.showNotification(_U('act_imp'))
    end
end)
```

### ตัวอย่างการตั้งค่า Webhook ฝั่ง Server

ไปที่ `azael_dc-serverlogs/config.server.lua`

##### ก่อนตั้งค่า Webhook

```lua
Config['webhook'] = {
	['Login'] = 'Webhook URL - Login',						-- เชื่อมต่อกับเซิร์ฟเวอร์
	['Logout'] = 'Webhook URL - Logout',					-- ตัดการเชื่อมต่อเซิร์ฟเวอร์
	['Chat'] = 'Webhook URL - Chat',						-- ข้อความแชท
	['Dead'] = 'Webhook URL - Dead'							-- สาเหตุการเสียชีวิต
}
```

##### หลังตั้งค่า Webhook

```lua
Config['webhook'] = {
	['Login'] = 'Webhook URL - Login',						-- เชื่อมต่อกับเซิร์ฟเวอร์
	['Logout'] = 'Webhook URL - Logout',					-- ตัดการเชื่อมต่อเซิร์ฟเวอร์
	['Chat'] = 'Webhook URL - Chat',						-- ข้อความแชท
    ['Dead'] = 'Webhook URL - Dead',						-- สาเหตุการเสียชีวิต
    ['UseItem'] = 'Webhook URL - Use Item'	                -- ใช้งานไอเทม
}
```

{{% alert theme="info" %}}
บรรทัดสุดท้ายจะต้องไม่มีเครื่องหมาย <kbd>,</kbd> เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

## การติดตั้งรหัสทริกเกอร์ฝั่ง Client

การติดตั้งรหัสทริกเกอร์ (Trigger) เพื่อรับกิจกรรม (Event) จากทรัพยากรอื่นฝั่ง Client

### รหัสทริกเกอร์ฝั่ง Client
```lua
local sendToDiscord = 'ข้อความที่ต้องการส่งไปยัง Discord'
TriggerServerEvent('azael_discordlogs:sendToDiscord', 'EventName', sendToDiscord, GetPlayerServerId(PlayerId()), '^1')
```

### รายละเอียดรหัสทริกเกอร์ฝั่ง Client

* **azael_discordlogs:sendToDiscord**
    - ชื่อเหตุการณ์ทริกเกอร์ (Trigger) ให้ระบุตรงกับ [event_name](../config/#event_name) หากมีการแก้ไขการตั้งค่า
* **EventName** 
    - ชื่อของ Webhook ที่ตั้งค่าใน `config.server.lua`
* **sendToDiscord**
    - ข้อความที่ต้องการส่งไปยังกลุ่ม Discord
* **GetPlayerServerId(PlayerId())**
    - ไอดีของผู้เล่นฝั่ง Client
* **^1**
    - รหัสแถบสีของกล่องข้อความ สามารถดูรหัสสีได้ที่ไฟล์ `config.server.lua`

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
    TriggerServerEvent('azael_discordlogs:sendToDiscord', 'PoliceImpound', sendToDiscord, GetPlayerServerId(PlayerId()), '^5')

	--local vehicleName = GetLabelText(GetDisplayNameFromVehicleModel(GetEntityModel(vehicle)))
	ESX.Game.DeleteVehicle(vehicle)
	ESX.ShowNotification(_U('impound_successful'))
	currentTask.busy = false
end
```

### ตัวอย่างการตั้งค่า Webhook ฝั่ง Client

ไปที่ `azael_dc-serverlogs/config.server.lua`

##### ก่อนตั้งค่า Webhook

```lua
Config['webhook'] = {
	['Login'] = 'Webhook URL - Login',						-- เชื่อมต่อกับเซิร์ฟเวอร์
	['Logout'] = 'Webhook URL - Logout',					-- ตัดการเชื่อมต่อเซิร์ฟเวอร์
	['Chat'] = 'Webhook URL - Chat',						-- ข้อความแชท
	['Dead'] = 'Webhook URL - Dead'							-- สาเหตุการเสียชีวิต
}
```

##### หลังตั้งค่า Webhook

```lua
Config['webhook'] = {
	['Login'] = 'Webhook URL - Login',						-- เชื่อมต่อกับเซิร์ฟเวอร์
	['Logout'] = 'Webhook URL - Logout',					-- ตัดการเชื่อมต่อเซิร์ฟเวอร์
	['Chat'] = 'Webhook URL - Chat',						-- ข้อความแชท
    ['Dead'] = 'Webhook URL - Dead',						-- สาเหตุการเสียชีวิต
    ['PoliceImpound'] = 'Webhook URL - Police Impound'	    -- ตำรวจ: ส่งพาหนะไปพาวท์
}
```

{{% alert theme="info" %}}
บรรทัดสุดท้ายจะต้องไม่มีเครื่องหมาย <kbd>,</kbd> เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}
