---
title: การใช้งาน Custom Logs
weight: 250
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับการใช้งาน **Custom Logs**
---

{{% alert theme="info" %}}
สำหรับ **Web Application** ที่ใช้ในการตรวจสอบข้อมูล ยังอยู่ระหว่างการพัฒนา 
{{% /alert %}}

## ใช้งาน Localhost
เก็บข้อมูลบันทึกกิจกรรมต่างๆไว้ภายในเครื่องเซิร์ฟเวอร์ สามารถเปิดการใช้งาน **Custom - Logs** ในการตั้งค่า [Options](../config/#options) และกำหนด **Using** เป็น **Localhost** (จำเป็นที่จะต้องติดตั้ง [MongoDB](https://www.mongodb.com/) บนเครื่องเซิร์ฟเวอร์ และใช้งานทรัพยากร [MongoDB Wrapper](https://forum.cfx.re/t/release-mongodb-wrapper-resource/149262?u=azael.dev) สำหรับ [FiveM](https://fivem.net/))

### วิธีติดตั้ง MongoDB บน Windows
<iframe width="600" height="350" src="https://www.youtube.com/embed/f8-0etb-nas" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### วิธีติดตั้ง  MongoDB Wrapper (FiveM)
1. ดาวน์โหลด [Node.js](https://nodejs.org/en/download/) และดำเนินการติดตั้งให้เรียบร้อย
2. ดาวน์โหลดทรัพยากร [MongoDB Wrapper](https://forum.cfx.re/t/release-mongodb-wrapper-resource/149262?u=azael.dev) สำหรับ [FiveM](https://fivem.net/)
3. แก้ไขชื่อโฟลเดอร์เป็น **mongodb** และนำไปวางไว้ภายในโฟลเดอร์ **resources**
4. เปิดไฟล์ `server.cfg` และดำเนินการเพิ่ม
```cfg
set mongodb_url "mongodb://localhost:27017"
set mongodb_database "your_database"
ensure mongodb
```
5. กดปุ่ม <kbd>Shift</kbd> **+** <kbd>Right Click</kbd> ที่โฟลเดอร์ **mongodb**
6. เลือก **Open PowerShell window here** เพื่อเปิดใช้งาน **PowerShell**
7. ใช้คำสั่ง `npm install` เพื่อติดตั้ง **node_modules**

## ใช้งาน HTTP Request
ส่งข้อมูลบันทึกกิจกรรมต่างๆไปยังเซิร์ฟเวอร์ที่กำหนดเอง สามารถเปิดการใช้งาน **Custom - Logs** ในการตั้งค่า [Options](../config/#options) และกำหนด **Using** เป็น **HttpRequest**

### ตัวอย่าง HTTP Request (POST)
ข้อมูลจะถูกส่งออกโดยใช้ [POST](https://en.wikipedia.org/wiki/POST_(HTTP)) และ **HTTP Response Code** จะต้องตอบกลับสถานะ `201` หรือ `200` ตาม[ตัวอย่าง API รับข้อมูล (PHP)](../custom/#ตวอยาง-api-รบขอมล-php)

##### Request Header
**Authorization** จะถูกกำหนดภายในส่วนหัวของคำขอ HTTP Request ตามกำหนดค่า [Options](../config/#options)

```
Authorization = <method> <parameter>
```

##### Request Body (JSON)
ข้อมูลจะถูกส่งออกในรูปแบบ [JSON](https://en.wikipedia.org/wiki/JSON) ดังตัวอย่างด้านล่างนี้

```json
{
    "event": "Login",
    "color": "#99CC00",
    "content": "เข้าสู่เซิร์ฟเวอร์",
    "screenshot": "https://media.discordapp.net/attachments/819858829884915753/845634322181914664/screenshot.jpg",
    "timestamp": 1621685334,
    "player": {
       "id": 1,
       "ip": "ip:192.168.1.101",
       "license": "license:c89b466e4624e53d972f5dd188fa53c34689e653",
       "discord": "discord:443334508020891658",
       "steam": "steam:1100001332e7216",
       "steam_name": "Azael Dev",
       "steam_profile": "https://steamcommunity.com/profiles/76561198818947606",
       "steam_avatar": "https://cdn.cloudflare.steamstatic.com/steamcommunity/public/images/avatars/93/93178f63ab1be3720d78340a72ca518798ca6707_full.jpg"
    }
}
```

| Name                  | Possible Values        | Description              |
|---------------------- |------------------------|--------------------------|
| event                 | string                 | ชื่อของเหตุการณ์             |
| color                 | string                 | รหัสสี                     |
| content               | string                 | เนื้อหา                    |
| screenshot            | string หรือ string ว่าง  | ภาพหน้าจอ                 |
| timestamp             | number                 | วันและเวลา (unix)          |
| player                | object                 | ข้อมูลรูปแบบวัตถุ             |
| id                    | number                 | source                   |
| ip                    | string                 | ip ที่ใช้งาน                |
| license               | string                 | ตัวระบุ rockstar           |
| discord               | string หรือ string ว่าง  | ตัวระบุ discord            |
| steam                 | string                 | ตัวระบุ steam              |
| steam_name            | string                 | ชื่อ steam                 |
| steam_profile         | string                 | ลิงก์โปรไฟล์ steam          |
| steam_avatar          | string                 | รูปโปรไฟล์ steam           |

### ตัวอย่าง API รับข้อมูล (PHP)
ใช้งานฐานข้อมูล [MongoDB](https://www.mongodb.com/) และ [MongoDB PHP Driver](https://www.mongodb.com/docs/drivers/php/)

```php
/**
* API Example (azael_dc-serverlogs)
*
* @author Azael Dev <contact@azael.dev>
* @link https://www.azael.dev
*/

// Config - Authorization (Token)
$set_token = 'your_token';

// Config - MongoDB
$uri_mongodb = 'mongodb://localhost:27017'; // Connection
$data_mongodb = 'azael_logs';               // Database

header('Access-Control-Allow-Origin: *');
header('Access-Control-Allow-Methods: POST');

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $headers = apache_request_headers();

    if (isset($headers['Authorization'])) {
        list($method, $token) = explode(' ', $headers['Authorization']);

        if ($method === 'Log' && $token === $set_token) {
            $data = json_decode(file_get_contents("php://input"), true);

            if (isset($data['event']) && isset($data['color']) && isset($data['content']) && isset($data['screenshot']) && isset($data['timestamp']) && isset($data['player'])) {
                /*  Collection */
                $col_mongodb = $data['event'];  // ชื่อ Collection ที่ใช้ในการเก็บข้อมูล (อ้างอิงจาก Event)

                /* MongoDB (PHP Driver: https://www.php.net/manual/en/set.mongodb.php) */
                $manager = new MongoDB\Driver\Manager($uri_mongodb);
                $bulk = new MongoDB\Driver\BulkWrite;
                $bulk->insert($data);
                $result = $manager->executeBulkWrite("${data_mongodb}.${col_mongodb}", $bulk);

                if ($result->getInsertedCount() >= 1) {
                    /* HTTP response status codes */
                    http_response_code(201);    // คำขอสำเร็จ (200 หรือ 201)
                } else {
                    /* HTTP response status codes */
                    http_response_code(500);    // ข้อผิดพลาดภายในเซิร์ฟเวอร์
                }
                
                exit;
            } else {
                /* HTTP response status codes */
                http_response_code(400);    // รูปแบบคำขอไม่ถูกต้อง
            }
        } else {
            /* HTTP response status codes */
            http_response_code(403);        // ไม่มีสิทธิ์เข้าถึงเนื้อหา
            exit;
        }
    } else {
        /* HTTP response status codes */
        http_response_code(404);            // ใช้ 404 แทน 401 เพื่อปิดบังเส้นทาง API
        exit;
    }
} else {
    /* HTTP response status codes */
    http_response_code(404);                // ใช้ 404 เพื่อปิดบังเส้นทาง API
    exit;
}
```
