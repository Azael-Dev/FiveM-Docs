---
title: การตั้งค่าทรัพยากร
weight: 220
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการตั้งค่า
---

## การตั้งค่าฝั่ง Server

สามารถตั้งค่าได้ที่ไฟล์ `config.server.js`

### `command`

คำสั่งที่ใช้ในการประกาศสำหรับผู้ดูแลระบบ

```js
const command = 'anm';
```

{{% alert theme="info" %}}
ใช้คำสั่งได้ผ่าน Chat, F8 หรือ Server Console ใช้ [ACE Permissions](https://forum.cfx.re/t/basic-aces-principals-overview-guide/90917?u=azael.dev) ในการตรวจสอบสิทธิ์การใช้งานคำสั่ง
{{% /alert %}}

### `display`

เวลาในการเเสดงข้อความที่ประกาศ (วินาที)

```js
const display = 30;
```

### `announceAdmin`

หัวข้อประกาศข้อความจากผู้ดูแลระบบ

```js
const announceAdmin = 'ผู้ดูแลระบบ';
```

### `announceAutomate`

หัวข้อประกาศข้อความอัตโนมัติ

```js
const announceAutomate = 'ประกาศ';
```

### `enableAutomate`

เปิดใช้งานประกาศข้อความโดยอัตโนมัติ

```js
const enableAutomate = true;
```

* **true** = เปิดใช้งาน
* **false** = ปิดใช้งาน

### `automateDelay`

ดีเลย์ในการประกาศข้อความโดยอัตโนมัติ (นาที)

```js
const automateDelay = 5;
```

### `automateLists`

ข้อความที่ต้องการประกาศโดยอัตโนมัติ

```js
const automateLists = [
    'ยินดีต้อนรับ ขอให้สนุกกับการสวมบทบาท',
    'ติดตามข่าวสารและกิจกรรมต่างๆ ได้ที่กลุ่มชุมชนของเรา',
    'หากพบผู้กระทำความผิด โปรดแจ้งผู้ดูแลระบบ'
];
```

## การตั้งค่าฝั่ง Client

สามารถตั้งค่าได้ที่ไฟล์ `config.client.js`

### `imageEnable`

เปิดใช้งานรูปภาพ

```js
const imageEnable = true;
```

* **true** = เปิดใช้งาน
* **false** = ปิดใช้งาน

### `imageName`

ชื่อไฟล์รูปภาพพร้อมนามสกุลไฟล์

```js
const imageName = 'logo.png'; 
```

### `delayFadeIn`

ความล้าช้า FadeIn (มิลลิวินาที)

```js
const delayFadeIn = 1000;
```

### `delayFadeOut`

ความล้าช้า fadeOut (มิลลิวินาที)

```js
const delayFadeOut = 1000;
```
