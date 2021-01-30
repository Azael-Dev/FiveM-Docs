---
title: การติดตั้งทรัพยากร
weight: 210
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการติดตั้ง
---

## เริ่มต้นการใช้งาน

1. ดาวน์โหลดและแตกไฟล์ลงในโฟลเดอร์ `resources` ของคุณ ชื่อของทรัพยากรจะต้องเป็น `azael_ui-acceptitems` ห้ามแก้ไขชื่อของทรัพยากรโดยเด็ดขาด เนื่องจากทรัพยากรจะไม่ทำงาน
2. เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_ui-acceptitems` ไว้ด้านล่าง [es_extended][es_extended]

## การติดตั้งไฟล์ export

### es_extended

ไปที่ `es_extended/__resource.lua` หรือ `es_extended/fxmanifest.lua`

ค้นหา

```lua
server_scripts
```

มองหา

```lua
'common/functions.lua'
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
'@azael_ui-acceptitems/export/server/function.server.lua'
```

![Export es_extended](/resources/azael_ui-acceptitems/export_es_extended.png "Export es_extended")

### esx_inventoryhud

ไปที่ `esx_inventoryhud/__resource.lua` หรือ `esx_inventoryhud/fxmanifest.lua`

ค้นหา

```lua
server_scripts
```

มองหา

```lua
"config.lua"
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
'@azael_ui-acceptitems/export/server/function.server.lua'
```

![Export esx_inventoryhud](/resources/azael_ui-acceptitems/export_esx_inventoryhud.png "Export esx_inventoryhud")

## การติดตั้งใน esx_inventoryhud

{{% alert theme="info" %}}
ไม่ต้องดำเนินการตามขั้นตอนนี้ หากคุณไม่ได้ใช้งานระบบส่ง กุญแจ ตามตัวอย่างรหัสด้านล่างนี้
{{% /alert %}}

ไปที่ `esx_inventoryhud/server/main.lua`

### `esx_inventoryhud:updateKey`

ค้นหา

```lua
local targetXPlayer = ESX.GetPlayerFromId(target)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
local xPlayerRequest = AZAEL.ACCEPT_ITEMS.GetPlayerRequest(sourceXPlayer.source, targetXPlayer.source, type, itemName, 1)

if xPlayerRequest.resend then
	return TriggerClientEvent('esx:showNotification', sourceXPlayer.source, '~r~Cannot~s~ give, please try ~y~again~s~')
elseif xPlayerRequest.display then
	return TriggerClientEvent('esx:showNotification', sourceXPlayer.source, 'The person is in ~y~another deal~s~')
elseif xPlayerRequest.cancel then
	return TriggerClientEvent('esx:showNotification', sourceXPlayer.source, 'The deal has been ~r~rejected~s~')
end
```

{{% alert theme="info" %}}
หากคุณใช้งาน [azael_give-objects](https://fivem.azael.dev/digishop/azael-give-objects/) ให้วางรหัสนี้ไว้ด้านบนของเงื่อนไข [AZAEL.GIVE_OBJECTS.CanPlayAnimation](../../azael_give-objects/installation/#esx_inventoryhudupdatekey)
{{% /alert %}}

## การติดตั้งใน es_extended v1.1.x

[es_extended](https://github.com/esx-framework/es_extended) เวอร์ชั่น `v1.1.x` จะใช้ระบบ `limit` หากเซิร์ฟเวอร์ของคุณใช้เวอร์ชั่นนี้อยู่ ให้คุณไปที่ `es_extended/server/main.lua` และดำเนินการติดตั้งรหัสทริกเกอร์ เพื่อส่งกิจกรรมมายังทรัพยากร `azael_ui-acceptitems` ตามขั้นตอนด้านล่างนี้

{{% alert theme="info" %}}
ตรวจสอบเวอร์ชั่นได้ที่ `es_extended/__resource.lua`
{{% /alert %}}

### `esx:giveInventoryItem`

ค้นหา

```lua
local targetXPlayer = ESX.GetPlayerFromId(target)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
local xPlayerRequest = AZAEL.ACCEPT_ITEMS.GetPlayerRequest(sourceXPlayer.source, targetXPlayer.source, type, itemName, itemCount)

if xPlayerRequest.resend then
	return TriggerClientEvent('esx:showNotification', sourceXPlayer.source, '~r~Cannot~s~ give, please try ~y~again~s~')
elseif xPlayerRequest.display then
	return TriggerClientEvent('esx:showNotification', sourceXPlayer.source, 'The person is in ~y~another deal~s~')
elseif xPlayerRequest.cancel then
	return TriggerClientEvent('esx:showNotification', sourceXPlayer.source, 'The deal has been ~r~rejected~s~')
end
```

{{% alert theme="info" %}}
หากคุณใช้งาน [azael_give-objects](https://fivem.azael.dev/digishop/azael-give-objects/) ให้วางรหัสนี้ไว้ด้านบนของเงื่อนไข [AZAEL.GIVE_OBJECTS.CanPlayAnimation](../../azael_give-objects/installation/#esxgiveinventoryitem)
{{% /alert %}}

## การติดตั้งใน es_extended v1.2.x

[es_extended](https://github.com/esx-framework/es_extended) เวอร์ชั่น `v1.2.x` จะใช้ระบบ `weigh` จะใช้ระบบ `limit` หากเซิร์ฟเวอร์ของคุณใช้เวอร์ชั่นนี้อยู่ ให้คุณไปที่ `es_extended/server/main.lua` และดำเนินการติดตั้งรหัสทริกเกอร์ เพื่อส่งกิจกรรมมายังทรัพยากร `azael_ui-acceptitems` ตามขั้นตอนด้านล่างนี้

{{% alert theme="info" %}}
ตรวจสอบเวอร์ชั่นได้ที่ `es_extended/fxmanifest.lua`
{{% /alert %}}

### `esx:giveInventoryItem`

ค้นหา

```lua
local targetXPlayer = ESX.GetPlayerFromId(target)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
local xPlayerRequest = AZAEL.ACCEPT_ITEMS.GetPlayerRequest(sourceXPlayer.source, targetXPlayer.source, type, itemName, itemCount)

if xPlayerRequest.resend then
	return sourceXPlayer.showNotification('~r~Cannot~s~ give, please try ~y~again~s~')
elseif xPlayerRequest.display then
	return sourceXPlayer.showNotification('The person is in ~y~another deal~s~')
elseif xPlayerRequest.cancel then
	return sourceXPlayer.showNotification('The deal has been ~r~rejected~s~')
end
```

{{% alert theme="info" %}}
หากคุณใช้งาน [azael_give-objects](https://fivem.azael.dev/digishop/azael-give-objects/) ให้วางรหัสนี้ไว้ด้านบนของเงื่อนไข [AZAEL.GIVE_OBJECTS.CanPlayAnimation](../../azael_give-objects/installation/#esxgiveinventoryitem-1)
{{% /alert %}}

## ยกเลิกการใช้งาน

1. เปิดไฟล์ `server.cfg` ค้นหา `ensure azael_ui-acceptitems`
2. ทำการเพิ่ม `#` ไว้ข้างหน้า `ensure azael_ui-acceptitems`

ตัวอย่าง:

```
#ensure azael_ui-acceptitems
```

[es_extended]: https://github.com/esx-framework/es_extended
