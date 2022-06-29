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
    Active: {
        Identifier: 'steam'
    },

    Kick: { 
        Player: {
            Enable: true,
            Reason: 'บุคคลอื่นกำลังใช้งานตัวระบุ {0} พยายามเชื่อมต่อกับเซิร์ฟเวอร์'
        },

        Target: {
            Reason: 'บุคคลอื่นกำลังใช้งานตัวระบุ {0} เชื่อมต่อกับเซิร์ฟเวอร์อยู่ในขณะนี้'
        },

        Identifier: {
            Reason: 'ไม่พบตัวระบุ {0} โปรดลองเชื่อมต่อกับเซิร์ฟเวอร์ใหม่อีกครั้ง'
        }
    }
};
```

- **Active** = ใช้งาน
    - **Identifier** = ตัวระบุที่ใช้ในการตรวจสอบ (steam, license, live, discord, fivem, license2, ip)
- **Kick** = เตะออกจากเซิร์ฟเวอร์
    - **Player** = ผู้เล่นที่อยู่ภายในเซิร์ฟเวอร์
        - **Enable** = เปิดใช้งาน เตะผู้เล่นออกจากเซิร์ฟเวอร์ หากมีบุคคลอื่นใช้ตัวระบุเดียวกันเชื่อมต่อ
        - **Reason** = เหตุผลในการเตะออกจากเซิร์ฟเวอร์
    - **Target** = ผู้เล่นที่พยายามเชื่อมต่อกับเซิร์ฟเวอร์
        - **Reason** = เหตุผลในการเตะออกจากเซิร์ฟเวอร์
    - **Identifier** = ไม่พบตัวระบุของผู้เล่น
        - **Reason** = เหตุผลในการเตะออกจากเซิร์ฟเวอร์

{{% alert theme="info" %}}
**true** เท่ากับ เปิดใช้งาน | **false** เท่ากับ ปิดใช้งาน
{{% /alert %}}

### `Logs`

บันทึก สำหรับทรัพยากร [azael_dc-serverlogs](https://fivem.azael.dev/digishop/azael-dc-serverlogs/)

```js
AZAEL.SERVER.CONFIG.Logs = {
    Send: {
        Enable: true
    },

    Event: {
        Name: 'azael_dc-serverlogs:sendToDiscord'
    },

    Webhook: {
        Name: 'ActiveIdentifiers'
    }
};
```

- **Send** = ส่งบันทึก
    - **Enable** = เปิดใช้งาน ส่งบันทึก
- **Event** = เหตุการณ์
    - **Name** = ชื่อของเหตุการณ์ (เวอร์ชันเก่าจะใช้ `azael_discordlogs:sendToDiscord`)
- **Webhook** = Webhook
    - **Name** = ชื่อของ Webhook ที่กำหนดไว้ใน [การตั้งค่า Events](../../azael_dc-serverlogs/config/#events) ของทรัพยากร [azael_dc-serverlogs](https://fivem.azael.dev/digishop/azael-dc-serverlogs/)