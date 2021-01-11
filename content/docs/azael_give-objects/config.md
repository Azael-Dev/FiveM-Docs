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

### `Commands`

คำสั่งการใช้งาน ผู้เล่นสามารถใช้คำสั่งนี้ได้หากพบข้อผิดพลาดบางอย่าง

```js
AZAEL.SERVER.CONFIG.Commands = {
    Fixing: {
        Name: 'fixbuggive',
        Restricted: false
    }
};
```

- **Name**
    - **fixbuggive** = คำสั่งที่ใช้งาน
- **Restricted**
    - **true** = [ACE Permissions](https://forum.cfx.re/t/basic-aces-principals-overview-guide/90917?u=azael.dev) เท่านั้นที่ใช้คำสั่งได้
    - **false** = ทุกคน สามารถใช้คำสั่งได้

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

### `Types`

ประเภทข้อมูลที่ใช้ในการค้นหา วัตถุ ภายในการตั้งค่า

```js
AZAEL.CLIENT.CONFIG.Types = {
    'item_standard': AZAEL.CLIENT.OBJECT.CONFIG.Item,
    'item_money': AZAEL.CLIENT.OBJECT.CONFIG.Money,
    'item_account': AZAEL.CLIENT.OBJECT.CONFIG.Money,
    'item_weapon': AZAEL.CLIENT.OBJECT.CONFIG.Weapon,
    'item_ammo': AZAEL.CLIENT.OBJECT.CONFIG.Ammo,
    'item_key': AZAEL.CLIENT.OBJECT.CONFIG.Item,
    'item_keyhouse': AZAEL.CLIENT.OBJECT.CONFIG.Item
};
```

- **item_standard** = ไอเทมทั่วไป
- **item_money** = เงินสด
- **item_account** = เงินผิดกฎหมาย
- **item_weapon** = อาวุธ
- **item_ammo** = กระสุน
- **item_key** = กุญแจ ยานพาหนะ
- **item_keyhouse** = กุญแจ บ้าน

### `Blacklists`

รายการที่ไม่เเสดง วัตถุ หรือ รูปภาพ ในขณะที่ เก็บ, ทิ้ง, ส่ง, รับ

```js
AZAEL.CLIENT.CONFIG.Blacklists = {
    Enable: {
        Pickup: true,
        Remove: true,
        Give: true,
    },

    Items: [
        'black_money',
        'marijuana',
        'weed'
    ]
};
```
- **Enable** = เปิดใช้งาน ไม่เเสดง วัตถุ หรือ รูปภาพ
    - **Pickup** = ขณะที่ เก็บ
    - **Remove** = ขณะที่ ทิ้ง
    - **Give** = ขณะที่ ส่ง และ รับ
- **Items** = รายการ ไอเทม ที่จะไม่เเสดง

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Animations`

ภาพเคลื่อนไหว ในขณะที่ เก็บ, ทิ้ง, ส่ง, รับ

```js
AZAEL.CLIENT.CONFIG.Animations = {
    Pickup: {
        A: {
            Dict: 'weapons@first_person@aim_rng@generic@projectile@sticky_bomb@',
            Anim: 'plant_floor',
            Delay: 500
        },

        B: {
            Dict: 'reaction@intimidation@1h',
            Anim: 'intro',
            Delay: 1000
        },

        Pocket: {
            Enable: true
        }
    },

    Remove: {
        A: {
            Dict: 'reaction@intimidation@1h',
            Anim: 'outro',
            Delay: 1000
        },

        B: {
            Dict: 'weapons@first_person@aim_rng@generic@projectile@sticky_bomb@',
            Anim: 'plant_floor',
            Delay: 1000
        },

        Pocket: { 
            Enable: true
        }
    },

    Give: {
        Request: {
            A: {
                Dict: 'reaction@intimidation@1h',
                Anim: 'outro',
                Delay: 1000
            },
    
            B: {
                Dict: 'mp_common',
                Anim: 'givetake1_a',
                Delay: 1000
            }
        },
    
        Receive: {
            A: {
                Dict: 'mp_common',
                Anim: 'givetake1_b',
                Delay: 1000
            },
    
            B: {
                Dict: 'reaction@intimidation@1h',
                Anim: 'intro',
                Delay: 1000
            },
    
            Wait: 1500
        },

        Pocket: {
            Enable: true 
        }
    },

    TimeOut: 3000 
};
```

- **Pickup** = ภาพเคลื่อนไหว ขณะที่ เก็บ
    - **A** = ภาพเคลื่อนไหว 1
        - **Dict** = พจนานุกรม
        - **Anim** = ชื่อ
        - **Delay** = ความล้าช้า (มิลลิวินาที)
    - **B** = ภาพเคลื่อนไหว 2
        - **Dict** = พจนานุกรม
        - **Anim** = ชื่อ
        - **Delay** = ความล้าช้า (มิลลิวินาที)
    - **Pocket** = เก็บเข้าตัวละคร (ภาพเคลื่อนไหว 2)
        - **Enable** = เปิดใช้งาน ภาพเคลื่อนไหว เก็บเข้าตัวละคร
- **Remove** = ภาพเคลื่อนไหว ขณะที่ ทิ้ง
    - **A** = ภาพเคลื่อนไหว 1
        - **Dict** = พจนานุกรม
        - **Anim** = ชื่อ
        - **Delay** = ความล้าช้า (มิลลิวินาที)
    - **B** = ภาพเคลื่อนไหว 2
        - **Dict** = พจนานุกรม
        - **Anim** = ชื่อ
        - **Delay** = ความล้าช้า (มิลลิวินาที)
    - **Pocket** = เอาออกจากตัวละคร (ภาพเคลื่อนไหว 1)
        - **Enable** = เปิดใช้งาน ภาพเคลื่อนไหว เอาออกจากตัวละคร
- **Give** = ภาพเคลื่อนไหว ขณะที่ ส่ง และ รับ
    - **Request** = ภาพเคลื่อนไหว ขณะที่ ส่ง
        - **A** = ภาพเคลื่อนไหว 1
            - **Dict** = พจนานุกรม
            - **Anim** = ชื่อ
            - **Delay** = ความล้าช้า (มิลลิวินาที)
        - **B** = ภาพเคลื่อนไหว 2
            - **Dict** = พจนานุกรม
            - **Anim** = ชื่อ
            - **Delay** = ความล้าช้า (มิลลิวินาที)
    - **Receive** = ภาพเคลื่อนไหว ขณะที่ ส่ง
        - **A** = ภาพเคลื่อนไหว 1
            - **Dict** = พจนานุกรม
            - **Anim** = ชื่อ
            - **Delay** = ความล้าช้า (มิลลิวินาที)
        - **B** = ภาพเคลื่อนไหว 2
            - **Dict** = พจนานุกรม
            - **Anim** = ชื่อ
            - **Delay** = ความล้าช้า (มิลลิวินาที)
        - **Wait** = เวลาที่รอ ผู้ส่ง เล่นภาพเคลื่อนไหว (มิลลิวินาที)
    - **Pocket** = เอาออกจากตัวละคร (Request - ภาพเคลื่อนไหว 1) เเละ เก็บเข้าตัวละคร (Receive - ภาพเคลื่อนไหว 2)
        - **Enable** = เปิดใช้งาน ภาพเคลื่อนไหว เอาออกจากตัวละคร เเละ เก็บเข้าตัวละคร
- **TimeOut** = หากไม่สามารถโหลด ภาพเคลื่อนไหว ได้ จะข้ามขั้นตอนภายในเวลาที่กำหนด (มิลลิวินาที)

{{% alert theme="info" %}}
1000 มิลลิวินาที มีค่าเท่ากับ 1 วินาที<br>
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Objects`

เวลาที่แสดง วัตถุ และ รูปภาพ

```js
AZAEL.CLIENT.CONFIG.Objects = {
    Enable: true,

    Time: {
        Pickup: 1000,
        Remove: 500,
        Request: 500,
        Receive: 500,
    },

    TimeOut: 3000
};
```
- **Enable** = เปิดใช้งาน แสดงวัตถุ
- **Time** = เวลาที่แสดง วัตถุ (มิลลิวินาที)
    - **Pickup** = ขณะที่ เก็บ
    - **Remove** = ขณะที่ ทิ้ง
    - **Request** = ขณะที่ ส่ง
    - **Receive** = ขณะที่ รับ
- **TimeOut** = หากไม่สามารถโหลด วัตถุ ได้ จะข้ามขั้นตอนภายในเวลาที่กำหนด (มิลลิวินาที)

{{% alert theme="info" %}}
1000 มิลลิวินาที มีค่าเท่ากับ 1 วินาที <br>
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Images`

แสดงรูปภาพ หากไม่พบวัตถุ ในการตั้งค่า

```js
AZAEL.CLIENT.CONFIG.Images = {
    Enable: true,

    Inventory: {
        Enable: true,
        Path: 'html/img/items',
    },

    Custom: [
        'cash',
        'money',
        'black_money',
        'key',
        'keyhouse'
    ],

    Bone: 28422,
    Width: 0.1,
    Height: 0.2,
    Distance: 50,

    Debug: true
};
```

- **Enable** = เปิดใช้งาน แสดงรูปภาพ หากไม่พบวัตถุ ในการตั้งค่า
- **Inventory** = รูปภาพ จาก กระเป๋า
    - **Enable** = เปิดใช้งาน รูปภาพ จาก กระเป๋า
    - **Path** = ที่อยู่ไฟล์รูปภาพ ของ กระเป๋า ที่ใช้งาน (ไม่ต้องระบุชื่อของทรัพยากร)
- **Bone** = [รหัสกระดูก](https://wiki.gtanet.work/index.php?title=Bones) แนบรูปภาพ
- **Width** = ความกว้าง ของรูปภาพ
- **Height** = ความสูง ของรูปภาพ
- **Distance** = ระยะที่มองเห็นรูปภาพ
- **Debug** = เปิดใช้งาน เเสดงข้อมูลการโหลดรูปภาพ ใน F8 ขณะเข้าเกม

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Sounds`

เสียงประกอบ

```js
AZAEL.CLIENT.CONFIG.Sounds = {
    Enable: true,
    ID: -1,
    Name: 'PICK_UP',
    Ref: 'HUD_FRONTEND_DEFAULT_SOUNDSET',
    P3: false
};
```

- **Enable** = เปิดใช้งาน เสียงประกอบ
- **ID** = รหัสเสียงประกอบ
- **Name** = ชื่อเสียงประกอบ
- **Ref** = ชื่อชุดเสียงประกอบ

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}


### `Events`

กิจกรรมต่างๆ

```js
AZAEL.CLIENT.CONFIG.Events = {
    Inventory: {
        Open: {
            Enable: true,
            Event: 'esx_inventoryhud:openInventory',
            Delay: 500
        },

        Close: {
            Enable: true,
            Event: 'esx_inventoryhud:closeInventory',
            Delay: 300
        }
    },

    Emote: {
        Cancel: {
            Enable: true,
            Event: 'dpemotes:cancelEmote',
            Delay: 100
        }
    }
};
```

- **Inventory** = กระเป๋า
    - **Open** = เปิดกระเป๋า เมื่อเล่นภาพเคลื่อนไหวเสร็จ
        - **Enable** = เปิดใช้งาน เปิดกระเป๋า เมื่อเล่นภาพเคลื่อนไหวเสร็จ
        - **Event** = ชื่อกิจกรรม เปิดกระเป๋า
        - **Delay** = ความล้าช้าในการ เปิดกระเป๋า
    - **Close** = ปิดกระเป๋า เมื่อเริ่มเล่นภาพเคลื่อนไหว
        - **Enable** = เปิดใช้งาน ปิดกระเป๋า เมื่อเริ่มเล่นภาพเคลื่อนไหว
        - **Event** = ชื่อกิจกรรม ปิดกระเป๋า
        - **Delay** = ความล้าช้าในการ ปิดกระเป๋า
- **Emote** = [dpemotes](https://forum.cfx.re/t/dpemotes-1-7-390-emotes-walkingstyles-keybinding-dances-expressions-and-shared-emotes/843105?u=azael.dev)
    - **Cancel** = ยกเลิกกิจกรรม ก่อนเริ่มเล่นภาพเคลื่อนไหว
        - **Enable** = เปิดใช้งาน ยกเลิกกิจกรรม ก่อนเริ่มเล่นภาพเคลื่อนไหว
        - **Event** = ชื่อกิจกรรม ก่อนเริ่มเล่นภาพเคลื่อนไหว
        - **Delay** = ความล้าช้าในการ ยกเลิกกิจกรรม

{{% alert theme="info" %}}
1000 มิลลิวินาที มีค่าเท่ากับ 1 วินาที<br>
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Controls`

การควบคุม ในขณะที่เล่นภาพเคลื่อนไหว

```js
AZAEL.CLIENT.CONFIG.Controls = {
    Enable: true,

    List: {
        0: {
            Group: 0,
            Control: 0,
            Enable: true
        },

        1: {
            Group: 0,
            Control: 1,
            Enable: true
        },

        2: {
            Group: 0,
            Control: 2,
            Enable: true
        },

        3: {
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
สามารถดูรายรหัส การควบคุม ได้ที่ [FiveM Controls](https://docs.fivem.net/docs/game-references/controls/#controls)
{{% /alert %}}

## การตั้งค่า Objects

- **item_standard** (ไอเทมทั่วไป) สามารถตั้งค่าได้ที่ไฟล์ `config/object/item.config.js`
- **item_money** (เงินสด) และ **item_account** (เงินผิดกฎหมาย) สามารถตั้งค่าได้ที่ไฟล์ `config/object/money.config.js`
- **item_weapon** (อาวุธ) สามารถตั้งค่าได้ที่ไฟล์ `config/object/weapon.config.js`
- **item_ammo** (กระสุน) สามารถตั้งค่าได้ที่ไฟล์ `config/object/ammo.config.js`

### `รายละเอียด`

ค้นหาชื่อ Model ของวัตถุภายในเกมได้ที่ [mWojtasik.dev](https://mwojtasik.dev/tools/gtav/objects) หรือ [Pleb Masters](https://forge.plebmasters.de/objects)

```js
'bread': {
    Model: 'v_ret_247_bread1',
    Bone: 57005,
    Position: {
        X: 0.13,
        Y: 0.050,
        Z: 0.001
    },
    Rotation: {
        X: 240.0,
        Y: 175.0,
        Z: 25.0
    }
},
```

- **bread** = ชื่อไอเทม ในฐานข้อมูล
    - **Model** = ชื่อวัตถุ
    - **Bone** = [รหัสกระดูก](https://wiki.gtanet.work/index.php?title=Bones)
    - **Position** = ตำแหน่ง วัตถุ
        - **X** = ตำแหน่ง X
        - **Y** = ตำแหน่ง Y
        - **Z** = ตำแหน่ง Z
    - **Rotation** = การหมุน วัตถุ
        - **X** = การหมุน X
        - **Y** = การหมุน Y
        - **Z** = การหมุน Z
