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

### `Keys`

ชื่อที่ใช้แสดงแทน กุญแจ

```js
AZAEL.SERVER.CONFIG.Keys = {
    'item_key': 'กุญแจยานพาหนะ',
    'item_keyhouse': 'กุญแจบ้าน'
};
```

- **item_key** = ประเภท กุญแจยานพาหนะ
    - **กุญแจยานพาหนะ** = ชื่อที่ใช้ในการแสดง
- **item_keyhouse** = ประเภท กุญแจบ้าน
    - **กุญแจบ้าน** = ชื่อที่ใช้ในการแสดง

### `Currencies`

ชื่อที่ใช้แสดงแทน เงิน

```js
AZAEL.SERVER.CONFIG.Currencies = {
    Money: 'Cash',
    BlackMoney: 'Dirty Money'
};
```

- **Money** = ประเภท เงินสด
    - **Cash** = ชื่อที่ใช้ในการแสดง
- **BlackMoney** = ประเภท เงินผิดกฎหมาย
    - **Dirty Money** = ชื่อที่ใช้ในการแสดง

### `Blacklists`

รายการที่ไม่เเสดง UI เเละ ยอมรับการแลกเปลี่ยนโดยอัตโนมัติ

```js
AZAEL.SERVER.CONFIG.Blacklists = {
    Enable: true,

    Items: [
        'black_money',
        'marijuana',
        'weed'
    ]
};
```

- **Enable** = เปิดใช้งาน ไม่เเสดง UI
- **Items** = รายการ ไอเทม ที่จะไม่เเสดง UI

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
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
    }
};
```

{{% alert theme="info" %}}
ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

### `Dialogs`

กล่องข้อความ UI

```js
AZAEL.CLIENT.CONFIG.Dialogs = {
    Timer: 15,
    Distance: 5
};
```

- **Timer** = เวลาในการเเสดง UI การแลกเปลี่ยนจะถูกยกเลิกโดยอัตโนมัติเมื่อหมดเวลา  (ระบุเป็น วินาที)
- **Distance** = ยกเลิก UI การแลกเปลี่ยน เมื่อ ผู้ส่ง อยู่ห่างจาก ผู้รับ เกินระยะที่กำหนด

### `Images`

รูปภาพ

```js
AZAEL.CLIENT.CONFIG.Images = {
    Inventory: {
        Enable: true,
        Path: 'esx_inventoryhud/html/img/items'
    }
};
```

- **Inventory** = กระเป๋า
    - **Enable** = เปิดใช้งานรูปภาพ จาก กระเป๋า
    - **Path** = ที่อยู่ไฟล์รูปภาพ จาก กระเป๋า ที่ใช้งาน

{{% alert theme="info" %}}
หากปิดใช้งานรูปภาพจากกระเป๋า จะเป็นการใช้งานรูปภาพของทรัพยากรภายในโฟลเดอร์ `html/images`
{{% /alert %}}

### `Events`

กิจกรรมต่างๆ

```js
AZAEL.CLIENT.CONFIG.Events = {
    Inventory: {
        Close: {
            Enable: true,
            Event: 'esx_inventoryhud:closeInventory',
            Delay: 300
        }
    }
};
```

- **Inventory** = กระเป๋า
    - **Close** = ปิดกระเป๋า ผู้ส่ง เเละ ผู้รับ เมื่อกล่องข้อความ UI แสดง
        - **Enable** = เปิดใช้งาน ปิดกระเป๋า ผู้ส่ง เเละ ผู้รับ เมื่อกล่องข้อความ UI แสดง
        - **Event** = ชื่อกิจกรรม ปิดกระเป๋า
        - **Delay** = ความล้าช้าในการ ปิดกระเป๋า

{{% alert theme="info" %}}
1000 มิลลิวินาที มีค่าเท่ากับ 1 วินาที<br>
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Messages`

ข้อความ และ การเเจ้งเตือนต่างๆ

```js
AZAEL.CLIENT.CONFIG.Messages = {
    DrawText: {
        Enable: true,
        Font: 'sarabun',
        Size: 0.4,
        Position: {
            X: 0.5,
            Y: 0.8
        }
    },

    pNotify: {
        Enable: true,
        Type: 'error',
        Timeout: 3000,
        Layout: 'bottomCenter',
        Queue: 'global'
    }
};
```

- **DrawText** = เเสดงข้อความนับถอยหลัง สำหรับ ผู้ส่ง
    - **Enable** = เปิดใช้งาน เเสดงข้อความนับถอยหลัง สำหรับ ผู้ส่ง
    - **Font** = แบบ อักษร (โฟลเดอร์ `stream`)
    - **Size** = ขนาด อักษร
    - **Position** = ตำแหน่ง ข้อความ
        - **X** = ตำแหน่ง X
        - **Y** = ตำแหน่ง Y
- **pNotify** = เเจ้งเตือน [pNotify][pNotify] เมื่อ ผู้ส่ง อยู่นอกระยะที่กำหนด
    - **Enable** = เปิดใช้งาน เเจ้งเตือน [pNotify][pNotify]
    - **Type** = ประเภท (`alert`, `success`, `error`, `warning`, `info`)
    - **Timeout** = เวลาที่เเสดง (มิลลิวินาที)
    - **Layout** = ตำแหน่งที่แสดง (`top`, `topLeft`, `topCenter`, `topRight`, `center`, `cenerLeft`, `centerRight`, `bottom`, `bottomLeft`, `bottomCenter`, `bottomRight`)
    - **Queue** = ชื่อคิว `เป็น global โดยค่าเริ่มต้น`

{{% alert theme="info" %}}
1000 มิลลิวินาที มีค่าเท่ากับ 1 วินาที<br>
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Controls`

การควบคุม ในขณะที่เเสดงกล่องข้อความ UI

```js
AZAEL.CLIENT.CONFIG.Controls = { 
    Enable: true,

    List: {
        0: {
            Group: 0,
            Control: 249,
            Enable: true
        }
    }
};
```

- **Enable** = เปิดใช้งาน การควบคุม ในขณะที่เล่นภาพเคลื่อนไหว
- **List** = รายการ
    - **Group** = รหัส กลุ่ม
    - **Control** = รหัส การควบคุม
    - **Enable** = เปิดใช้งาน ปิดการควบคุม

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน<br>
สามารถดูรหัส การควบคุม ได้ที่ [FiveM Controls](https://docs.fivem.net/docs/game-references/controls/#controls)
{{% /alert %}}

[pNotify]: https://forum.cfx.re/t/release-pnotify-in-game-js-notifications-using-noty/20659?u=azael.dev