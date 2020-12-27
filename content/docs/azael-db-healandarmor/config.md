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
	['server_shared_obj'] = 'esx:getSharedObject',
	['server_player_load'] = 'esx:playerLoaded'
}
```

{{% alert theme="info" %}}
ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

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

### `ped_max_health`

พลังชีวิตของ Peds (ค่าปกติ เท่ากับ 200)

```lua
Config['ped_max_health'] = 200
```

{{% alert theme="info" %}}
ค่าเริ่มต้น คือ 200
{{% /alert %}}

### `ped_loaded_delay`

ความล่าช้าในการโหลด เลือด เเละ เกราะ ขณะเข้าสู่เซิร์ฟเวอร์ (วินาที)

```lua
Config['ped_loaded_delay'] = 10
```

### `enable_debug`

เปิดใช้งานการเเสดงข้อความ Debug ไปยัง Server Console

```lua
Config['enable_debug'] = false
```

* **true** = เปิดใช้งาน
* **false** = ปิดใช้งาน

### `enable_health`

เปิดใช้งานบันทึก เลือด

```lua
Config['enable_health'] = true
```

* **true** = เปิดใช้งาน
* **false** = ปิดใช้งาน

### `enable_armor`

เปิดใช้งานบันทึก เกราะ

```lua
Config['enable_armor'] = true
```

* **true** = เปิดใช้งาน
* **false** = ปิดใช้งาน
