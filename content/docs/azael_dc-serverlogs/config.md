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

### `Options`

ตัวเลือกฟังก์ชั่นต่างๆ

```js
AZAEL.SERVER.CONFIG.Options = {
    Event: {
        Name: 'azael_dc-serverlogs:sendToDiscord'
    },

    Discord: {
        Enable: true,

        Image: {
            URL: 'https://i.imgur.com/GxQpZzJ.png'
        },
    
        Request: {
            Count: 30
        },

        Queue: {
            Command: 'logq'
        },
    
        Limit: {
            Enable: false
        }
    },

    Custom: {
        Enable: false,  
        Using: 'Localhost',

        Localhost: {
            Resource: {
                Name: 'mongodb'
            },
            
            Collection: {
                Name: 'azael_logs'
            }
        },

        HttpRequest: {
            Host: {
                Name: 'example.com',
                Path: '/api/logs/',
                Port: 80
            }
        }
    },

    Hardware: {
        Enable: true
    },

    Screenshot: {
        Enable: true
    },

    Debug: {
        Enable: false
    }
};
```

- **Event** = เหตุการณ์
    - **Name** = ชื่อของเหตุการณ์ (เวอร์ชันเก่าจะใช้ `azael_discordlogs:sendToDiscord`)
- **Discord** = Discord - Webhooks
    - **Enable** = เปิดใช้งาน ส่งคำขอ ไปยัง Discord - Webhooks
    - **Image** = ภาพประจำตัว
        - **URL** = ที่อยู่รูปภาพ
    - **Request** = คำขอการใช้งาน [Discord API](https://discord.com/developers/docs/intro)
        - **Count** = จำนวน คำขอ Webhooks ที่ต้องการส่งไปยัง Discord ภายใน 1 นาที ต่อ 1 ช่อง (แนะนำไม่เกิน 30 คำขอ เพื่อป้องกัน [Rate Limit](https://discord.com/developers/docs/topics/rate-limits#rate-limits))
    - **Queue** = คิวคำขอ
        - **Command** = คำสั่ง ตรวจสอบคิวคำขอ Webhooks ที่ยังรอดำเนินการส่งไปยัง Discord (สามารถใช้คำสั่งผ่าน Server Console หรือ Live Console ของระบบ txAdmin)
    - **Limit** = จำกัด
        - **Enable** = เปิดใช้งาน ไม่ส่งคำขอ Webhooks หากเกินอัตราจำกัดการใช้งาน [Discord API](https://discord.com/developers/docs/intro)
- **Custom** = Custom - Webhooks
    - **Enable** = เปิดใช้งาน ส่งคำขอ ไปยัง Custom - Webhooks
    - **Using** = ใช้งาน `Localhost` หรือ `HttpRequest` (Localhost เก็บข้อมูลไว้ภายในเครื่องเซิร์ฟเวอร์ | HttpRequest ส่งข้อมูลไปเก็บไว้ภายนอกเครื่องเซิร์ฟเวอร์)
    - **Localhost** = เก็บข้อมูลไว้ภายในเครื่องเซิร์ฟเวอร์ (หากใช้งาน จำเป็นที่จะต้องติดตั้ง [MongoDB](https://www.mongodb.com/try/download/community) บนเครื่องเซิร์ฟเวอร์ และ ทรัพยากร [MongoDB](https://github.com/alcoholiclobster/fivem-mongodb) สำหรับ FiveM)
        - **Resource** = ทรัพยากร (Database)
            - **Name** = ชื่อของ ทรัพยากร ที่ใช้งาน (รองรับ [MongoDB](https://github.com/alcoholiclobster/fivem-mongodb) เท่านั้น)
        - **Collection** = MongoDB - Collection (Table)
            - **Name** = ชื่อ Collection ที่ใช้ในการเก็บข้อมูล
    - **HttpRequest** = ส่งข้อมูลไปเก็บไว้ภายนอกเครื่องเซิร์ฟเวอร์ (ใช้งาน POST และ ข้อมูลจะถูกส่งออกในรูปแบบ JSON)
        - **Host** = โฮสที่ใช้สำหรับเก็บข้อมูล
            - **Name** = ชื่อ Host หรือ Domain (IP Address หรือ example.com)
            - **Path** = เส้นทางของแอปพลิเคชัน (/api/logs/index.php)
            - **Port** = Port ที่ใช้งาน (HTTP: 80 | HTTPS: 443)
- **Hardware** = Hardware - Tokens (แสดงข้อมูลที่ช่อง เข้าสู่เซิร์ฟเวอร์ หรือ Login ในรูปแบบ JSON Array)
    - **Enable** = เปิดใช้งาน แสดงข้อมูล Hardware - Tokens ของผู้เล่น เมื่อเข้าสู่เซิร์ฟเวอร์            
- **Screenshot** = ภาพหน้าจอ
    - **Enable** = เปิดใช้งาน บันทึกภาพหน้าจอ (หากเปิดใช้งาน จำเป็นที่จะต้องติดตั้งทรัพยากร [screenshot-basic](https://github.com/citizenfx/screenshot-basic))
- **Debug** = ข้อผิดพลาด
    - **Enable** = เปิดใช้งาน แสดงข้อความ Debug ไปยัง Server Console

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Messages`

ข้อความแชท

```js
AZAEL.SERVER.CONFIG.Messages = {
    Blacklist: {
        Enable: true
    },

    Remove: {
        Enable: true
    },

    Kick: { 
        Enable: true,
        Reason: 'ใช้คำที่ไม่ได้รับอนุญาตในกล่องข้อความแชท'
    },
    
    Word: [
        'lynxmenu.com',
        'lynxcollective.ltd',
        'eulencheats.com',
        'discord.gg'
    ]
};
```

- **Blacklist** = ไม่อนุญาต (คำที่ไม่อนุญาต)
    - **Enable** = เปิดใช้งาน ตรวจสอบคำที่ไม่อนุญาต
- **Remove** = ลบข้อความแชท
    - **Enable** = เปิดใช้งาน ลบข้อความแชท หากมีคำที่ไม่อนุญาตออกจากช่องแแชทของผู้เล่นทุกคน
- **Kick** = เตะออกจากเซิร์ฟเวอร์
    - **Enable** = เปิดใช้งาน เตะผู้เล่นที่ใช้คำที่ไม่อนุญาตออกจากเซิร์ฟเวอร์
    - **Reason** = เหตุผลในการเตะออกจากเซิร์ฟเวอร์
- **Word** = คำที่ไม่อนุญาต

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Colors`

สีกล่องข้อความ

```js
AZAEL.SERVER.CONFIG.Colors = {
    0: '#FFFFFF',
	1: '#FF4444',
	2: '#99CC00',
	3: '#FFBB33',
	4: '#0099CC',
    5: '#33B5E5',
	6: '#AA66CC',
	7: '#99AAB5',
	8: '#CC0000',
	9: '#CC0068'
};
```

{{% alert theme="info" %}}
สนับสนุนการใช้งานแบบ string, number หรือ ^0 (สำหรับการระบุรหัสสีที่รหัสทริกเกอร์)
{{% /alert %}}

### `Screenshots`

เหตุการณ์ที่กำหนดให้ บันทึกภาพหน้าจอ และ อัพโหลดไปยัง [Discord - Webhooks](https://support.discord.com/hc/th/articles/228383668-Intro-to-Webhooks) (Logout หรือ ออกจากเซิร์ฟเวอร์ ไม่สามารถใช้งานได้)

```js
AZAEL.SERVER.CONFIG.Screenshots = {
    'Dead': 'Discord Webhook URL - Dead Screenshots'        // ฝากภาพ-สาเหตุการตาย
};
```

- **Discord** = Discord
    - **Webhook** = URL สำหรับ ฝากภาพหน้าจอ
- **Event** = เหตุการณ์ที่อนุญาตให้ บันทึกภาพหน้าจอ

{{% alert theme="info" %}}
[วิธีการสร้าง Discord Webhook](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks)
{{% /alert %}}

### `Events`

เหตุการณ์ทั้งหมด

```js
AZAEL.SERVER.CONFIG.Events = {
    'Login': 'Discord Webhook URL - Login',                 // เข้าสู่เซิร์ฟเวอร์
    'Logout': 'Discord Webhook URL - Logout',               // ออกจากเซิร์ฟเวอร์
    'Chat': 'Discord Webhook URL - Chat',                   // ข้อความแชท
    'Dead': 'Discord Webhook URL - Dead'                    // สาเหตุการตาย
};
```

{{% alert theme="info" %}}
ไม่ต้องกำหนดค่าต่างๆในส่วนนี้ หากคุณไม่ได้ เปิดการใช้งาน Discord - Webhooks ในการตั้งค่า [Options](#options)<br>
บรรทัดสุดท้ายจะต้องไม่มีเครื่องหมาย <kbd>,</kbd> เพราะอาจจะทำให้เกิดข้อผิดพลาดได้
{{% /alert %}}

## การตั้งค่าฝั่ง Client

สามารถตั้งค่าได้ที่ไฟล์ `config/default/client.config.js`

### `Character`

ตัวละคร

```js
AZAEL.CLIENT.CONFIG.Character = {
    Model: [
        'mp_m_freemode_01',
        'mp_f_freemode_01'
    ]
};
```

- **Model** = รายการ Ped Models ใช้ในการตรวจสอบความถูกต้อง สำหรับบันทึกภาพหน้าจอของผู้เล่นในขณะที่เข้าสู่เซิร์ฟเวอร์ (ระบุเป็น `String` หรือ `Hash` ได้)

### `Deaths`

เสียชีวิต

```js
AZAEL.CLIENT.CONFIG.Deaths = {
    Log: {
        Disable: false
    },

    Zone: [
        /* Boxing - International Airport */
        {
            X: -1096.59,
            Y: -3007.87,
            Z: 13.94,
            Radius: 170
        }
    ]
};
```

- **Log** = บันทึก (Log)
    - **Disable** = ปิดใช้งาน บันทึกเสียชีวิต (Log) ในพื้นที่ที่กำหนด
- **Zone** = พื้นที่ (สามารถเพิ่มพื้นที่ได้)
    - **{...}** = [Objects](https://www.w3schools.com/js/js_objects.asp)
        - **X** = ตำแหน่ง X
        - **Y** = ตำแหน่ง Y
        - **Z** = ตำแหน่ง Z
        - **Radius** = รัศมี

{{% alert theme="info" %}}
**true** เท่ากับ ปิดใช้งาน | **false** เท่ากับ เปิดใช้งาน
{{% /alert %}}

### `Weapons`

รายการ อาวุธ สำหรับ สาเหตุการตาย

```js
AZAEL.CLIENT.CONFIG.Weapons = {                             // อาวุธ
    // Melee - ระยะประชิด
    'WEAPON_DAGGER': {                                      // ชื่อ หรือ แฮช
        Label: 'Antique Cavalry Dagger',                    // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_BAT': {                                         // ชื่อ หรือ แฮช
        Label: 'Baseball Bat',                              // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_BOTTLE': {                                      // ชื่อ หรือ แฮช
        Label: 'Broken Bottle',                             // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_CROWBAR': {                                     // ชื่อ หรือ แฮช
        Label: 'Crowbar',                                   // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_UNARMED': {                                     // ชื่อ หรือ แฮช
        Label: 'Fist',                                      // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_FLASHLIGHT': {                                  // ชื่อ หรือ แฮช
        Label: 'Flashlight',                                // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_GOLFCLUB': {                                    // ชื่อ หรือ แฮช
        Label: 'FlasGolf Clubhlight',                       // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_HAMMER': {                                      // ชื่อ หรือ แฮช
        Label: 'Hammer',                                    // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_HATCHET': {                                     // ชื่อ หรือ แฮช
        Label: 'Hatchet',                                   // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_KNUCKLE': {                                     // ชื่อ หรือ แฮช
        Label: 'Brass Knuckles',                            // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_KNIFE': {                                       // ชื่อ หรือ แฮช
        Label: 'Knife',                                     // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_MACHETE': {                                     // ชื่อ หรือ แฮช
        Label: 'Machete',                                   // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_SWITCHBLADE': {                                 // ชื่อ หรือ แฮช
        Label: 'Switchblade',                               // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_NIGHTSTICK': {                                  // ชื่อ หรือ แฮช
        Label: 'Nightstick',                                // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_WRENCH': {                                      // ชื่อ หรือ แฮช
        Label: 'Pipe Wrench',                               // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_BATTLEAXE': {                                   // ชื่อ หรือ แฮช
        Label: 'Battle Axe',                                // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_POOLCUE': {                                     // ชื่อ หรือ แฮช
        Label: 'Pool Cue',                                  // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    'WEAPON_STONE_HATCHET': {                               // ชื่อ หรือ แฮช
        Label: 'Stone Hatchet',                             // ป้าย
        Type: 'Melee'                                       // ประเภท
    },

    // Bullet - กระสุน
    'WEAPON_PISTOL': {                                      // ชื่อ หรือ แฮช
        Label: 'Pistol',                                    // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_PISTOL_MK2': {                                  // ชื่อ หรือ แฮช
        Label: 'Pistol Mk II',                              // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_COMBATPISTOL': {                                // ชื่อ หรือ แฮช
        Label: 'Combat Pistol',                             // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_APPISTOL': {                                    // ชื่อ หรือ แฮช
        Label: 'AP Pistol',                                 // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_STUNGUN': {                                     // ชื่อ หรือ แฮช
        Label: 'Stun Gun',                                  // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_PISTOL50': {                                    // ชื่อ หรือ แฮช
        Label: 'Pistol .50',                                // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_SNSPISTOL': {                                   // ชื่อ หรือ แฮช
        Label: 'SNS Pistol',                                // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_SNSPISTOL_MK2': {                               // ชื่อ หรือ แฮช
        Label: 'SNS Pistol Mk II',                          // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_HEAVYPISTOL': {                                 // ชื่อ หรือ แฮช
        Label: 'Heavy Pistol',                              // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_VINTAGEPISTOL': {                               // ชื่อ หรือ แฮช
        Label: 'Vintage Pistol',                            // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_FLAREGUN': {                                    // ชื่อ หรือ แฮช
        Label: 'Flare Gun',                                 // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_MARKSMANPISTOL': {                              // ชื่อ หรือ แฮช
        Label: 'Marksman Pistol',                           // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_REVOLVER': {                                    // ชื่อ หรือ แฮช
        Label: 'Heavy Revolver',                            // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_REVOLVER_MK2': {                                // ชื่อ หรือ แฮช
        Label: 'Heavy Revolver Mk II',                      // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_DOUBLEACTION': {                                // ชื่อ หรือ แฮช
        Label: 'Double Action Revolver',                    // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_RAYPISTOL': {                                   // ชื่อ หรือ แฮช
        Label: 'Up-n-Atomizer',                             // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_CERAMICPISTOL': {                               // ชื่อ หรือ แฮช
        Label: 'Ceramic Pistol',                            // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_NAVYREVOLVER': {                                // ชื่อ หรือ แฮช
        Label: 'Navy Revolver',                             // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_MICROSMG': {                                    // ชื่อ หรือ แฮช
        Label: 'Micro SMG',                                 // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_SMG': {                                         // ชื่อ หรือ แฮช
        Label: 'SMG',                                       // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_SMG_MK2': {                                     // ชื่อ หรือ แฮช
        Label: 'SMG Mk II',                                 // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_ASSAULTSMG': {                                  // ชื่อ หรือ แฮช
        Label: 'Assault SMG',                               // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_COMBATPDW': {                                   // ชื่อ หรือ แฮช
        Label: 'Combat PDW',                                // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_MACHINEPISTOL': {                               // ชื่อ หรือ แฮช
        Label: 'Machine Pistol',                            // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_MINISMG': {                                     // ชื่อ หรือ แฮช
        Label: 'Mini SMG',                                  // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_RAYCARBINE': {                                  // ชื่อ หรือ แฮช
        Label: 'Unholy Hellbringer',                        // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_PUMPSHOTGUN': {                                 // ชื่อ หรือ แฮช
        Label: 'Pump Shotgun',                              // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_PUMPSHOTGUN_MK2': {                             // ชื่อ หรือ แฮช
        Label: 'Pump Shotgun Mk II',                        // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_SAWNOFFSHOTGUN': {                              // ชื่อ หรือ แฮช
        Label: 'Sawed-Off Shotgun',                         // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_ASSAULTSHOTGUN': {                              // ชื่อ หรือ แฮช
        Label: 'Assault Shotgun',                           // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_BULLPUPSHOTGUN': {                              // ชื่อ หรือ แฮช
        Label: 'Bullpup Shotgun',                           // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_MUSKET': {                                      // ชื่อ หรือ แฮช
        Label: 'Musket',                                    // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_HEAVYSHOTGUN': {                                // ชื่อ หรือ แฮช
        Label: 'Heavy Shotgun',                             // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_DBSHOTGUN': {                                   // ชื่อ หรือ แฮช
        Label: 'Double Barrel Shotgun',                     // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_AUTOSHOTGUN': {                                 // ชื่อ หรือ แฮช
        Label: 'Sweeper Shotgun',                           // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_ASSAULTRIFLE': {                                // ชื่อ หรือ แฮช
        Label: 'Assault Rifle',                             // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_ASSAULTRIFLE_MK2': {                            // ชื่อ หรือ แฮช
        Label: 'Assault Rifle Mk II',                       // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_CARBINERIFLE': {                                // ชื่อ หรือ แฮช
        Label: 'Carbine Rifle',                             // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_CARBINERIFLE_MK2': {                            // ชื่อ หรือ แฮช
        Label: 'Carbine Rifle Mk II',                       // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_ADVANCEDRIFLE': {                               // ชื่อ หรือ แฮช
        Label: 'Advanced Rifle',                            // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_SPECIALCARBINE': {                              // ชื่อ หรือ แฮช
        Label: 'Special Carbine',                           // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_SPECIALCARBINE_MK2': {                          // ชื่อ หรือ แฮช
        Label: 'Special Carbine Mk II',                     // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_BULLPUPRIFLE': {                                // ชื่อ หรือ แฮช
        Label: 'Bullpup Rifle',                             // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_BULLPUPRIFLE_MK2': {                            // ชื่อ หรือ แฮช
        Label: 'Bullpup Rifle Mk II',                       // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_COMPACTRIFLE': {                                // ชื่อ หรือ แฮช
        Label: 'Compact Rifle',                             // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_MG': {                                          // ชื่อ หรือ แฮช
        Label: 'MG',                                        // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_COMBATMG': {                                    // ชื่อ หรือ แฮช
        Label: 'Combat MG',                                 // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_COMBATMG_MK2': {                                // ชื่อ หรือ แฮช
        Label: 'Combat MG Mk II',                           // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_GUSENBERG': {                                   // ชื่อ หรือ แฮช
        Label: 'Gusenberg Sweeper',                         // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_SNIPERRIFLE': {                                 // ชื่อ หรือ แฮช
        Label: 'Sniper Rifle',                              // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_HEAVYSNIPER': {                                 // ชื่อ หรือ แฮช
        Label: 'Heavy Sniper',                              // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_HEAVYSNIPER_MK2': {                             // ชื่อ หรือ แฮช
        Label: 'Heavy Sniper Mk II',                        // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_MARKSMANRIFLE': {                               // ชื่อ หรือ แฮช
        Label: 'Marksman Rifle',                            // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_MARKSMANRIFLE_MK2': {                           // ชื่อ หรือ แฮช
        Label: 'Marksman Rifle Mk II',                      // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    'WEAPON_MINIGUN': {                                     // ชื่อ หรือ แฮช
        Label: 'Minigun',                                   // ป้าย
        Type: 'Bullet'                                      // ประเภท
    },

    // Explosion - แรงระเบิด
    'WEAPON_RPG': {                                         // ชื่อ หรือ แฮช
        Label: 'RPG',                                       // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_GRENADELAUNCHER': {                             // ชื่อ หรือ แฮช
        Label: 'Grenade Launcher',                          // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_GRENADELAUNCHER_SMOKE': {                       // ชื่อ หรือ แฮช
        Label: 'Grenade Launcher Smoke',                    // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_RAILGUN': {                                     // ชื่อ หรือ แฮช
        Label: 'Railgun',                                   // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_HOMINGLAUNCHER': {                              // ชื่อ หรือ แฮช
        Label: 'Homing Launcher',                           // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_COMPACTLAUNCHER': {                             // ชื่อ หรือ แฮช
        Label: 'Compact Grenade',                           // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_RAYMINIGUN': {                                  // ชื่อ หรือ แฮช
        Label: 'Widowmaker',                                // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_PASSENGER_ROCKET': {                            // ชื่อ หรือ แฮช
        Label: 'Passenger Rocket',                          // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_AIRSTRIKE_ROCKET': {                            // ชื่อ หรือ แฮช
        Label: 'Airstrike Rocket',                          // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_STINGER': {                                     // ชื่อ หรือ แฮช
        Label: 'Stinger (Vehicle)',                         // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_GRENADE': {                                     // ชื่อ หรือ แฮช
        Label: 'Grenade',                                   // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_STICKYBOMB': {                                  // ชื่อ หรือ แฮช
        Label: 'Sticky Bomb',                               // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_SMOKEGRENADE': {                                // ชื่อ หรือ แฮช
        Label: 'Tear Gas',                                  // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_EXPLOSION': {                                   // ชื่อ หรือ แฮช
        Label: 'Explosion',                                 // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_HELI_CRASH': {                                  // ชื่อ หรือ แฮช
        Label: 'Helicopter Crash',                          // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_VEHICLE_ROCKET': {                              // ชื่อ หรือ แฮช
        Label: 'Vehicle Rocket',                            // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_PROXMINE': {                                    // ชื่อ หรือ แฮช
        Label: 'Proximity Mines',                           // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    'WEAPON_PIPEBOMB': {                                    // ชื่อ หรือ แฮช
        Label: 'Pipe Bombs',                                // ป้าย
        Type: 'Explosion'                                   // ประเภท
    },

    // Gas - แก๊สพิษ
    'WEAPON_BZGAS': {                                       // ชื่อ หรือ แฮช
        Label: 'BZ Gas',                                    // ป้าย
        Type: 'Gas'                                         // ประเภท
    },

    // Vehicle - ยานพาหนะ
    'WEAPON_RAMMED_BY_CAR': {                               // ชื่อ หรือ แฮช
        Label: 'ยานพาหนะ',                                  // ป้าย
        Type: 'Vehicle'                                     // ประเภท
    },

    'WEAPON_RUN_OVER_BY_CAR': {                             // ชื่อ หรือ แฮช
        Label: 'ยานพาหนะ',                                  // ป้าย
        Type: 'Vehicle'                                     // ประเภท
    },

    // Animal - สัตว์
    'WEAPON_ANIMAL': {                                      // ชื่อ หรือ แฮช
        Label: 'สัตว์',                                       // ป้าย
        Type: 'Animal'                                      // ประเภท
    },

    'WEAPON_COUGAR': {                                      // ชื่อ หรือ แฮช
        Label: 'เสือภูเขา',                                    // ป้าย
        Type: 'Animal'                                      // ประเภท
    },

    // Fall - ตกจากที่สูง
    'WEAPON_FALL': {                                        // ชื่อ หรือ แฮช
        Label: 'ตกจากที่สูง หรือ ขาดอาหาร',                     // ป้าย
        Type: 'Fall'                                        // ประเภท
    },

    // Burn - เผา
    'WEAPON_MOLOTOV': {                                     // ชื่อ หรือ แฮช
        Label: 'Molotov Cocktail',                          // ป้าย
        Type: 'Burn'                                        // ประเภท
    },

    'WEAPON_PETROLCAN': {                                   // ชื่อ หรือ แฮช
        Label: 'Jerry Can',                                 // ป้าย
        Type: 'Burn'                                        // ประเภท
    },

    'WEAPON_FIREWORK': {                                    // ชื่อ หรือ แฮช
        Label: 'Firework Launcher',                         // ป้าย
        Type: 'Burn'                                        // ประเภท
    },

    // Burn - จมน้ำ
    'WEAPON_DROWNING': {                                    // ชื่อ หรือ แฮช
        Label: 'จมน้ำ',                                      // ป้าย
        Type: 'Drown'                                       // ประเภท
    },

    'WEAPON_DROWNING_IN_VEHICLE': {                         // ชื่อ หรือ แฮช
        Label: 'จมน้ำ (ภายในยานพาหนะ)',                      // ป้าย
        Type: 'Drown'                                       // ประเภท
    }
};
```
