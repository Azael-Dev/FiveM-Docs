---
title: การติดตั้งทรัพยากร
weight: 210
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการติดตั้ง
---

## เริ่มต้นการใช้งาน

1. ดาวน์โหลดและแตกไฟล์ลงในโฟลเดอร์ `resources` ของคุณ ชื่อของทรัพยากรจะต้องเป็น `azael_ui-itemnotify` ห้ามแก้ไขชื่อของทรัพยากรโดยเด็ดขาด เนื่องจากทรัพยากรจะไม่ทำงาน
2. เปิดไฟล์ `server.cfg` เพิ่ม `ensure azael_ui-itemnotify` ไว้ด้านล่าง [es_extended][es_extended]

## ปิดแจ้งเตือน ESX.UI

ไปที่ `es_extended/client/main.lua`

ค้นหา

```lua
ESX.UI.ShowInventoryItemNotification
```

แก้ไขเป็น

```lua
--ESX.UI.ShowInventoryItemNotification
```

{{% alert theme="info" %}}
ปิดใช้งาน `ESX.UI.ShowInventoryItemNotification` ทั้งหมดภายในไฟล์ `es_extended/client/main.lua`
{{% /alert %}}

## การติดตั้งใน es_extended v1.1.x

[es_extended](https://github.com/esx-framework/es_extended) เวอร์ชั่น `v1.1.x` จะใช้ระบบ `limit` หากเซิร์ฟเวอร์ของคุณใช้เวอร์ชั่นนี้อยู่ ให้คุณไปที่ `es_extended/server/classes/player.lua` และดำเนินการติดตั้งรหัสทริกเกอร์ เพื่อส่งกิจกรรมมายังทรัพยากร `azael_ui-itemnotify` ตามขั้นตอนด้านล่างนี้

{{% alert theme="info" %}}
ตรวจสอบเวอร์ชั่นได้ที่ `es_extended/__resource.lua`
{{% /alert %}}

### `self.setMoney`

ค้นหา

```lua
self.setMoney = function
```

มองหา

```lua
self.player.setMoney(money)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendMoney', 'set', money, self.source)
```

### `self.addMoney`

ค้นหา

```lua
self.addMoney = function
```

มองหา

```lua
self.player.addMoney(money)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendMoney', 'add', money, self.source)
```

### `self.removeMoney`

ค้นหา

```lua
self.removeMoney = function
```

มองหา

```lua
self.player.removeMoney(money)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendMoney', 'remove', money, self.source)
```

### `self.setAccountMoney`

ค้นหา

```lua
self.setAccountMoney = function
```

มองหา

```lua
TriggerClientEvent('esx:setAccountMoney', self.source, account)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendAccountMoney', 'set', acc, money, self.source)
```

### `self.addAccountMoney`

ค้นหา

```lua
self.addAccountMoney = function
```

มองหา

```lua
TriggerClientEvent('esx:setAccountMoney', self.source, account)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendAccountMoney', 'add', acc, money, self.source)
```

### `self.removeAccountMoney`

ค้นหา

```lua
self.removeAccountMoney = function
```

มองหา

```lua
TriggerClientEvent('esx:setAccountMoney', self.source, account)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendAccountMoney', 'remove', a, m, self.source)
```

### `self.addInventoryItem`

ค้นหา

```lua
self.addInventoryItem = function
```

มองหา

```lua
TriggerClientEvent('esx:addInventoryItem', self.source, item, count)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendInventoryItem', 'add', item.name, count, self.source)
```

### `self.removeInventoryItem`

ค้นหา

```lua
self.removeInventoryItem = function
```

มองหา

```lua
TriggerClientEvent('esx:removeInventoryItem', self.source, item, count)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendInventoryItem', 'remove', item.name, count, self.source)
```

### `self.setInventoryItem`

ค้นหา

```lua
self.setInventoryItem = function
```

มองหา

```lua
item.count = count
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendInventoryItem', 'set', item.name, count, self.source)
```

### `self.addWeapon`

ค้นหา

```lua
self.addWeapon = function
```

มองหา

```lua
TriggerClientEvent('esx:addInventoryItem', self.source, {label = weaponLabel}, 1)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerClientEvent('esx:addInventoryItem', self.source, {label = weaponLabel}, 1)
```

### `self.addWeaponComponent`

ค้นหา

```lua
self.addWeaponComponent = function
```

มองหา

```lua
TriggerClientEvent('esx:addWeaponComponent', self.source, weaponName, weaponComponent)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
local component = ESX.GetWeaponComponent(weaponName, weaponComponent)
if component then
    TriggerEvent('azael_ui-itemnotify:sendWeaponComponent', 'add', component.name, component.label, self.source)
end
```

### `self.removeWeapon`

ค้นหา

```lua
self.removeWeapon = function
```

มองหา

```lua
local weaponLabel
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
local weaponAmmo
```

มองหา

```lua
weaponLabel = v.label
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
weaponAmmo = v.ammo
```

มองหา

```lua
TriggerClientEvent('esx:removeInventoryItem', self.source, {label = weaponLabel}, 1)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendWeapon', 'remove', weaponName, weaponAmmo, self.source)
```

### `self.removeWeaponComponent`

ค้นหา

```lua
self.removeWeaponComponent = function
```

มองหา

```lua
TriggerClientEvent('esx:removeWeaponComponent', self.source, weaponName, weaponComponent)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
local component = ESX.GetWeaponComponent(weaponName, weaponComponent)
if component then
    TriggerEvent('azael_ui-itemnotify:sendWeaponComponent', 'remove', component.name, component.label, self.source)
end
```

## การติดตั้งใน es_extended v1.2.x

[es_extended](https://github.com/esx-framework/es_extended) เวอร์ชั่น `v1.2.x` จะใช้ระบบ `weigh` หากเซิร์ฟเวอร์ของคุณใช้เวอร์ชั่นนี้อยู่ ให้คุณไปที่ `es_extended/server/classes/player.lua` และดำเนินการติดตั้งรหัสทริกเกอร์ เพื่อส่งกิจกรรมมายังทรัพยากร `azael_ui-itemnotify` ตามขั้นตอนด้านล่างนี้

{{% alert theme="info" %}}
ตรวจสอบเวอร์ชั่นได้ที่ `es_extended/fxmanifest.lua`
{{% /alert %}}

### `self.setAccountMoney`

ค้นหา

```lua
self.setAccountMoney = function
```

มองหา

```lua
self.triggerEvent('esx:setAccountMoney', account)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendAccountMoney', 'set', accountName, money, self.source)
```

### `self.addAccountMoney`

ค้นหา

```lua
self.addAccountMoney = function
```

มองหา

```lua
self.triggerEvent('esx:setAccountMoney', account)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendAccountMoney', 'add', accountName, money, self.source)
```

### `self.removeAccountMoney`

ค้นหา

```lua
self.removeAccountMoney = function
```

มองหา

```lua
self.triggerEvent('esx:setAccountMoney', account)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendAccountMoney', 'remove', accountName, money, self.source)
```

### `self.addInventoryItem`

ค้นหา

```lua
self.addInventoryItem = function
```

มองหา

```lua
self.triggerEvent('esx:addInventoryItem', item.name, item.count)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendInventoryItem', 'add', item.name, count, self.source)
```

### `self.removeInventoryItem`

ค้นหา

```lua
self.removeInventoryItem = function
```

มองหา

```lua
self.triggerEvent('esx:removeInventoryItem', item.name, item.count)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendInventoryItem', 'remove', item.name, count, self.source)
```

### `self.setInventoryItem`

ค้นหา

```lua
self.setInventoryItem = function
```

มองหา

```lua
count = ESX.Math.Round(count)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendInventoryItem', 'set', item.name, count, self.source)
```

### `self.addWeapon`

ค้นหา

```lua
self.addWeapon = function
```

มองหา

```lua
self.triggerEvent('esx:addInventoryItem', weaponLabel, false, true)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendWeapon', 'add', weaponName, ammo, self.source)
```

### `self.addWeaponComponent`

ค้นหา

```lua
self.addWeaponComponent = function
```

มองหา

```lua
self.triggerEvent('esx:addInventoryItem', component.label, false, true)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendWeaponComponent', 'add', component.name, component.label, self.source)
```

### `self.addWeaponAmmo`

ค้นหา

```lua
self.addWeaponAmmo = function
```

มองหา

```lua
self.triggerEvent('esx:setWeaponAmmo', weaponName, weapon.ammo)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendWeaponAmmo', 'add', weaponName, ammoCount, self.source)
```

### `self.removeWeapon`

ค้นหา

```lua
self.removeWeapon = function
```

มองหา

```lua
local weaponLabel
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
local weaponAmmo
```

มองหา

```lua
weaponLabel = v.label
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
weaponAmmo = v.ammo
```

มองหา

```lua
self.triggerEvent('esx:removeInventoryItem', weaponLabel, false, true)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendWeapon', 'remove', weaponName, weaponAmmo, self.source)
```

### `self.removeWeaponComponent`

ค้นหา

```lua
self.removeWeaponComponent = function
```

มองหา

```lua
self.triggerEvent('esx:removeInventoryItem', component.label, false, true)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendWeaponComponent', 'remove', component.name, component.label, self.source)
```

### `self.removeWeaponAmmo`

ค้นหา

```lua
self.removeWeaponAmmo = function
```

มองหา

```lua
self.triggerEvent('esx:setWeaponAmmo', weaponName, weapon.ammo)
```

เพิ่มรหัสนี้ไว้ด้านล่าง

```lua
TriggerEvent('azael_ui-itemnotify:sendWeaponAmmo', 'remove', weaponName, ammoCount, self.source)
```

## ยกเลิกการใช้งาน

1. เปิดไฟล์ `server.cfg` ค้นหา `ensure azael_ui-itemnotify`
2. ทำการเพิ่ม `#` ไว้ข้างหน้า `ensure azael_ui-itemnotify`

ตัวอย่าง:
```
#ensure azael_ui-itemnotify
```

[es_extended]: https://github.com/esx-framework/es_extended
