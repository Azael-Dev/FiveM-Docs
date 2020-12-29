---
title: การติดตั้งทรัพยากร
weight: 210
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการติดตั้ง
---

## เริ่มต้นการใช้งาน

1. ดาวน์โหลดและแตกไฟล์ลงในโฟลเดอร์ `resources` ของคุณ ชื่อของทรัพยากรจะต้องเป็น `azael_give-objects` และ `azael_objects` ห้ามแก้ไขชื่อของทรัพยากรโดยเด็ดขาด เนื่องจากทรัพยากรจะไม่ทำงาน
2. เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_give-objects` ไว้ด้านล่าง [es_extended][es_extended]
3. เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_objects` ไว้ด้านล่าง `azael_give-objects`

### azael_objects
{{% alert theme="info" %}}
โฟลเดอร์ `azael_objects` คือ ทรัพยากรเกี่ยวกับ Objects (Prop) ที่เเถมให้ จำนวน 31 รายการ
{{% /alert %}}

| Model Name            | File Name              | Description              |
|---------------------- |------------------------|--------------------------|
| belt                  | belt.ydr               | เข็มขัด                    |
| card                  | card.ydr               | บัตรประจำตัว               |
| clote                 | clote.ydr              | ผ้า                       |
| corn                  | corn.ydr               | แป้งข้าวโพด               |
| cowskin               | cowskin.ydr            | หนังสัตว์ (ใหญ่)            |
| cub                   | cub.ydr                | ถ้วยใส่อาหาร               |
| diamond               | diamond.ydr            | เพชร                     |
| dish                  | dish.ydr               | จานใส่อาหาร               |
| fish                  | fish.ydr               | ปลา                      |
| g_crab                | g_crab.ydr             | ปู                        |
| gallon                | gallon.ydr             | แกลลอน                   |
| gold                  | gold.ydr               | ทองคําเเท่ง                |
| iron                  | iron.ydr               | เหล็กเเท่ง                 |
| medikit               | medikit.ydr            | กล่องปฐมพยาบาล           |
| painkiller            | painkiller.ydr         | ยาแก้ปวด                  |
| powderiron            | powderiron.ydr         | ผงเหล็ก (อยู่ในถาด)         |
| rawmeat               | rawmeat.ydr            | เนื้อสด                    |
| ricepanic             | ricepanic.ydr          | ต้นข้าว                    |
| rocksmall             | rocksmall.ydr          | ก้อนหิน                   |
| sack                  | sack.ydr               | กระสอบข้าว                |
| shell                 | shell.ydr              | หอย                     |
| skinanimal            | skinanimal.ydr         | หนังสัตว์ (เล็ก)            |
| tomato                | tomato.ydr             | มะเขือเทศ                 |
| toolbox               | toolbox.ydr            | กล่องเครื่องมือช่าง           |
| turtle                | turtle.ydr             | เต่า                      |
| vegetable             | vegetable.ydr          | กะหล่ำปลี                 |
| vegetable_pack        | vegetable_pack.ydr     | บรรจุภัณฑ์ผัก              |
| weedbag               | weedbag.ydr            | กัญชาบรรจุในถุง            |
| wheeltype             | wheeltype.ydr          | ยางรถ                    |
| woodbeak              | woodbeak.ydr           | แผ่นไม้                   |
| weed                  | weed.ydr               | ใบกัญชา                  |

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
'@azael_give-objects/export/server/extended.server.lua'
```

![Export es_extended](/resources/azael_give-objects/export_es_extended.png "Export es_extended")

### esx_inventoryhud

ไปที่ `esx_inventoryhud/__resource.lua` หรือ `esx_inventoryhud/fxmanifest.lua`

ค้นหา

```lua
client_scripts
```

มองหา

```lua
'config.lua'
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
'@azael_give-objects/export/client/inventory.client.js'
```

![Export esx_inventoryhud](/resources/azael_give-objects/export_esx_inventoryhud.png "Export esx_inventoryhud")

### dpemotes

{{% alert theme="info" %}}
ไม่ต้องดำเนินการตามขั้นตอนนี้ หากคุณไม่ได้ใช้งานทรัพยากรนี้
{{% /alert %}}

ไปที่ `dpemotes/__resource.lua` หรือ `dpemotes/fxmanifest.lua`

ค้นหา

```lua
client_scripts
```

มองหา

```lua
'Client/*.lua'
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
'@azael_give-objects/export/client/dpemotes.client.lua'
```

![Export esx_inventoryhud](/resources/azael_give-objects/export_dpemotes.png "Export esx_inventoryhud")


## การติดตั้งใน es_extended v1.1.x

[es_extended](https://github.com/esx-framework/es_extended) เวอร์ชั่น `v1.1.x` จะใช้ระบบ `limit` หากเซิร์ฟเวอร์ของคุณใช้เวอร์ชั่นนี้อยู่ ให้คุณไปที่ `es_extended/server/main.lua` และดำเนินการติดตั้งรหัสทริกเกอร์ เพื่อส่งกิจกรรมมายังทรัพยากร `azael_give-objects` ตามขั้นตอนด้านล่างนี้

{{% alert theme="info" %}}
ตรวจสอบเวอร์ชั่นได้ที่ `es_extended/__resource.lua`
{{% /alert %}}

## `esx:giveInventoryItem`

ค้นหา

```lua
local targetXPlayer = ESX.GetPlayerFromId(target)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
if not AZAEL.GIVE_OBJECTS.CanPlayAnimation(sourceXPlayer.source, targetXPlayer.source) then
	return TriggerClientEvent('esx:showNotification', sourceXPlayer.source, 'The person or you is ~y~busy~s~')
end
```

### `item_standard`

ค้นหา

```lua
targetXPlayer.addInventoryItem   (itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:giveInventoryItem', sourceXPlayer.source, targetXPlayer.source, type, itemName, true)
TriggerClientEvent('azael_give-objects:giveInventoryItem', targetXPlayer.source, sourceXPlayer.source, type, itemName, false)
```

### `item_money`

ค้นหา

```lua
targetXPlayer.addMoney   (itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:giveInventoryItem', sourceXPlayer.source, targetXPlayer.source, type, itemName, true)
TriggerClientEvent('azael_give-objects:giveInventoryItem', targetXPlayer.source, sourceXPlayer.source, type, itemName, false)
```

### `item_account`

ค้นหา

```lua
targetXPlayer.addAccountMoney   (itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:giveInventoryItem', sourceXPlayer.source, targetXPlayer.source, type, itemName, true)
TriggerClientEvent('azael_give-objects:giveInventoryItem', targetXPlayer.source, sourceXPlayer.source, type, itemName, false)
```

### `item_weapon`

ค้นหา

```lua
targetXPlayer.addWeapon(itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:giveInventoryItem', sourceXPlayer.source, targetXPlayer.source, type, itemName, true)
TriggerClientEvent('azael_give-objects:giveInventoryItem', targetXPlayer.source, sourceXPlayer.source, type, itemName, false)
```

## `esx:removeInventoryItem`

ค้นหา

```lua
local _source = source
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
if not AZAEL.GIVE_OBJECTS.CanPlayAnimation(_source) then
	return TriggerClientEvent('esx:showNotification', _source, '~r~Cannot~s~ remove item, please try ~y~again~s~')
end
```

### `item_standard`

ค้นหา

```lua
xPlayer.removeInventoryItem(itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:removeInventoryItem', xPlayer.source, type, itemName)
```

### `item_money`

ค้นหา

```lua
xPlayer.removeMoney(itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:removeInventoryItem', xPlayer.source, type, itemName)
```

### `item_account`

ค้นหา

```lua
xPlayer.removeAccountMoney(itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:removeInventoryItem', xPlayer.source, type, itemName)
```

### `item_weapon`

ค้นหา

```lua
xPlayer.removeWeapon(itemName)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:removeInventoryItem', xPlayer.source, type, itemName)
```

## `esx:onPickup`

ค้นหา

```lua
local xPlayer = ESX.GetPlayerFromId(_source)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
if not AZAEL.GIVE_OBJECTS.CanPlayAnimation(xPlayer.source) then
	return TriggerClientEvent('esx:showNotification', xPlayer.source, '~r~Cannot~s~ pickup item, please try ~y~again~s~')
end
```

### `item_standard`

ค้นหา

```lua
xPlayer.addInventoryItem(pickup.name, total)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:onPickup', xPlayer.source, pickup.type, pickup.name)
```

### `item_money`

ค้นหา

```lua
xPlayer.addMoney(pickup.count)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:onPickup', xPlayer.source, pickup.type, pickup.name)
```

### `item_account`

ค้นหา

```lua
xPlayer.addAccountMoney(pickup.name, pickup.count)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:onPickup', xPlayer.source, pickup.type, pickup.name)
```

## การติดตั้งใน es_extended v1.2.x

[es_extended](https://github.com/esx-framework/es_extended) เวอร์ชั่น `v1.2.x` จะใช้ระบบ `weigh` จะใช้ระบบ `limit` หากเซิร์ฟเวอร์ของคุณใช้เวอร์ชั่นนี้อยู่ ให้คุณไปที่ `es_extended/server/main.lua` และดำเนินการติดตั้งรหัสทริกเกอร์ เพื่อส่งกิจกรรมมายังทรัพยากร `azael_give-objects` ตามขั้นตอนด้านล่างนี้

{{% alert theme="info" %}}
ตรวจสอบเวอร์ชั่นได้ที่ `es_extended/fxmanifest.lua`
{{% /alert %}}

## `esx:giveInventoryItem`

ค้นหา

```lua
local targetXPlayer = ESX.GetPlayerFromId(target)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
if not AZAEL.GIVE_OBJECTS.CanPlayAnimation(sourceXPlayer.source, targetXPlayer.source) then
	return sourceXPlayer.showNotification('The person or you is ~y~busy~s~')
end
```

### `item_standard`

ค้นหา

```lua
targetXPlayer.addInventoryItem   (itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:giveInventoryItem', sourceXPlayer.source, targetXPlayer.source, type, itemName, true)
TriggerClientEvent('azael_give-objects:giveInventoryItem', targetXPlayer.source, sourceXPlayer.source, type, itemName, false)
```

### `item_account`

ค้นหา

```lua
targetXPlayer.addAccountMoney   (itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:giveInventoryItem', sourceXPlayer.source, targetXPlayer.source, type, itemName, true)
TriggerClientEvent('azael_give-objects:giveInventoryItem', targetXPlayer.source, sourceXPlayer.source, type, itemName, false)
```

### `item_weapon`

ค้นหา

```lua
targetXPlayer.addWeapon(itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:giveInventoryItem', sourceXPlayer.source, targetXPlayer.source, type, itemName, true)
TriggerClientEvent('azael_give-objects:giveInventoryItem', targetXPlayer.source, sourceXPlayer.source, type, itemName, false)
```

### `item_ammo`

ค้นหา

```lua
targetXPlayer.addWeaponAmmo(itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:giveInventoryItem', sourceXPlayer.source, targetXPlayer.source, type, itemName, true)
TriggerClientEvent('azael_give-objects:giveInventoryItem', targetXPlayer.source, sourceXPlayer.source, type, itemName, false)
```

## `esx:removeInventoryItem`

ค้นหา

```lua
local xPlayer = ESX.GetPlayerFromId(source)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
if not AZAEL.GIVE_OBJECTS.CanPlayAnimation(xPlayer.source) then
	return xPlayer.showNotification('~r~Cannot~s~ remove item, please try ~y~again~s~')
end
```

### `item_standard`

ค้นหา

```lua
xPlayer.removeInventoryItem(itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:removeInventoryItem', xPlayer.source, type, itemName)
```

### `item_account`

ค้นหา

```lua
xPlayer.removeAccountMoney(itemName, itemCount)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:removeInventoryItem', xPlayer.source, type, itemName)
```

### `item_weapon`

ค้นหา

```lua
xPlayer.removeWeapon(itemName)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:removeInventoryItem', xPlayer.source, type, itemName)
```

## `esx:onPickup`

ค้นหา

```lua
local pickup, xPlayer, success = ESX.Pickups[pickupId], ESX.GetPlayerFromId(source)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
if not AZAEL.GIVE_OBJECTS.CanPlayAnimation(xPlayer.source) then
	return xPlayer.showNotification('~r~Cannot~s~ pickup item, please try ~y~again~s~')
end
```

### `success`

ค้นหา

```lua
TriggerClientEvent('esx:removePickup', -1, pickupId)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('azael_give-objects:onPickup', xPlayer.source, pickup.type, pickup.name)
```

## ยกเลิกการใช้งาน

1. เปิดไฟล์ `server.cfg` ค้นหา `ensure azael_give-objects`
2. ทำการเพิ่ม `#` ไว้ข้างหน้า `ensure azael_give-objects`

ตัวอย่าง:

```
#ensure azael_give-objects
```

[es_extended]: https://github.com/esx-framework/es_extended
