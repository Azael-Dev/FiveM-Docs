---
title: การตั้งค่าทรัพยากร
weight: 220
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการตั้งค่า
---

## การตั้งค่า Auth

สามารถตั้งค่าได้ที่ไฟล์ `config/auth.config.js`

### `Token`

ตัวระบุ API เพื่อใช้ในการตรวจสอบสิทธิ์การใช้งานของทรัพยากร ดูได้ที่ [สินค้าที่ซื้อ](https://fivem.azael.dev/dashboard/digishop)

```js
AZAEL.SERVER.AUTH.CONFIG.Token = 'Token Key';
```

## การตั้งค่าฝั่ง Server

สามารถตั้งค่าได้ที่ไฟล์ `config/default/server.config.js`

### `Routes`

เส้นทางกิจกรรมของทรัพยากร

```js
AZAEL.SERVER.CONFIG.Routes = {
    Extended: {
        Resource: 'es_extended',
        Shared: 'esx:getSharedObject'
    }
};
```

{{% alert theme="info" %}}
ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

## การตั้งค่าฝั่ง Client

สามารถตั้งค่าได้ที่ไฟล์ `config/default/client.config.js`

### `Routes`

เส้นทางกิจกรรมของทรัพยากร

```js
AZAEL.CLIENT.CONFIG.Routes = {
    Extended: {
        Resource: 'es_extended',
        Shared: 'esx:getSharedObject'
    },

    Status: {
        Register: 'esx_status:registerStatus',
        Loaded: 'esx_status:loaded',
        Get: 'esx_status:getStatus',
        Set: 'esx_status:set'
    }
};
```

{{% alert theme="info" %}}
ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

### `Status`

สถานะ

```js
AZAEL.CLIENT.CONFIG.Status = {
    Health: {
        Enable: true,
        Name: 'health',
        Maximum: 200,
        Color: '#f4003e'
    },

    Armor: {
        Enable: true,
        Name: 'armor',
        Maximum: 100,
        Color: '#00cc99'
    }
};
```

- **Health** = พลังชีวิต
  - **Enable** = เปิดใช้งานบันทึก พลังชีวิต ไปยังฐานข้อมูล
  - **Name** = ชื่อสถานะบนฐานข้อมูล
  - **Maximum** =  พลังชีวิตสูงสุด (ค่าเริ่มต้นอยู่ที่ 200)
  - **Color** = สีของสถานะ (สนับสนุนสถานะของทรัพยากร [esx_status](https://github.com/esx-framework/esx_status))
- **Armor** = เกราะ
  - **Enable** = เปิดใช้งานบันทึก เกราะ ไปยังฐานข้อมูล
  - **Name** = ชื่อสถานะบนฐานข้อมูล
  - **Maximum** =  เกราะสูงสุด (ค่าเริ่มต้นอยู่ที่ 100)
  - **Color** = สีของสถานะ (สนับสนุนสถานะของทรัพยากร [esx_status](https://github.com/esx-framework/esx_status))

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Character`

ตัวละคร

```js
AZAEL.CLIENT.CONFIG.Character = {
    Delay: {
        Fetch: 30,
        Loop: 2
    },

    Recharge: {
        Health: {
            Disabled: true
        }
    },

    Model: [
        'mp_m_freemode_01',
        'mp_f_freemode_01'
    ]
};
```
- **Delay** = ความล่าช้า
  - **Fetch** = ความล่าช้าในการเริ่มโหลดข้อมูล เลือด เเละ เกราะ ในขณะที่เข้าสู่เซิร์ฟเวอร์
  - **Loop** = ความล่าช้าในการ Loop เพื่ออัพเดทและตรวจสอบข้อมูล
- **Recharge** = การฟื้นฟู
  - **Health** = พลังชีวิต
    - **Disabled** = ปิดใช้งาน การฟื้นฟูพลังชีวิต หากพลังชีวิตน้อยกว่า `50%`
- **Model** = รายการ Ped Models ใช้ในการตรวจสอบความถูกต้องเพื่อเริ่มโหลดข้อมูลในขณะที่เข้าสู่เซิร์ฟเวอร์ (ระบุเป็น `String` หรือ `Hash` ได้)

{{% alert theme="info" %}}
1 มีค่าเท่ากับ 1 วินาที<br>
**true** เท่ากับ ปิดใช้งาน | **false** เท่ากับ เปิดใช้งาน
{{% /alert %}}

### `Notification`

การแจ้งเตือน

```js
AZAEL.CLIENT.CONFIG.Notification = {
    Health: {
        Enable: true
    },

    Armor: {
        Enable: true
    },

    Debug: false
};
```

- **Health** = พลังชีวิต
  - **Enable** = เปิดใช้งานการเเจ้งเตือน พลังชีวิต คงเหลือในขณะที่เข้าสู่เซิร์ฟเวอร์
- **Armor** = เกราะ
  - **Enable** = เปิดใช้งานการเเจ้งเตือน เกราะ คงเหลือในขณะที่เข้าสู่เซิร์ฟเวอร์
- **Debug** = เปิดใช้งานการแสดง Debug ไปยัง `Client Console` (F8)

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}
