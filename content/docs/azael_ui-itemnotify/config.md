---
title: การตั้งค่าทรัพยากร
weight: 220
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

### `ammo`

ชื่อที่ใช้ในการแสดงแทน ลูกกระสุน

```lua
Config['ammo'] = 'Ammo'
```

### `money`

ชื่อที่ใช้ในการแสดงแทน เงินสด

```lua
Config['money'] = 'Cash'
```

### `bank`

ชื่อที่ใช้ในการแสดงแทน เงินในธนาคาร

```lua
Config['bank'] = 'Bank Money'
```

### `black_money`

ชื่อที่ใช้ในการแสดงแทน เงินผิดกฏหมาย

```lua
Config['black_money'] = 'Dirty Money'
```

## การตั้งค่าฝั่ง Client

สามารถตั้งค่าได้ที่ไฟล์ `config.client.lua`

### `esx_routers`

เส้นทางกิจกรรมของทรัพยากร ESX Framework หาก es_extended เซิร์ฟเวอร์ของคุณ มีการแก้ไขชื่อกิจกรรมของทรัพยากร เพื่อป้องกันโปรแกรมโกงต่างๆ

```lua
Config['esx_routers'] = {
	['client_shared_obj'] = 'esx:getSharedObject'
}
```

{{% alert theme="info" %}}
ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

### `timeout`

เวลาในการแสดง UI (วินาที)

```lua
Config['timeout'] = 3
```

### `maximum`

จำนวนคิวในการแสดง UI สูงสุด

```lua
Config['maximum'] = 3
```

### `position`

ตำแหน่งในการแสดง UI

```lua
Config['position'] = 'bottomRight'
```

* **bottomCenter** = กลางล่าง
* **bottomRight** = ขวาล่าง

### `inventory_image`

เปิดใช้งานรูปภาพจากกระเป๋า

```lua
Config['inventory_image'] = false
```

* **true** = ช้งานรูปภาพจากกระเป๋า
* **false** = ใช้งานรูปภาพของทรัพยากร

### `inventory_link`

ที่อยู่ไฟล์รูปภาพจากกระเป๋าที่ใช้งาน

```lua
Config['inventory_link'] = 'esx_inventoryhud/html/img/items'
```

### `text_add`

ข้อความ เพิ่ม

```lua
Config['text_add'] = '<i class="fas fa-plus"></i>'
```

### `text_set`

ข้อความ ตั้ง

```lua
Config['text_set'] = '<i class="fas fa-plus"></i>'
```

### `text_remove`

ข้อความ ลบ

```lua
Config['text_remove'] = '<i class="fas fa-minus"></i>'
```
