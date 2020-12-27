---
title: การตั้งค่าทรัพยากร
weight: 220
description: >
  คำแนะนำทีละขั้นตอนเกี่ยวกับวิธีการตั้งค่า
---

## การตั้งค่าฝั่ง Server

สามารถตั้งค่าได้ที่ไฟล์ `config.server.lua`

### `identifier_license`

เปิดใช้งาน ตรวจสอบ R* License แทน Steam

```lua
Config['identifier_license'] = false
```

- **true** = ใช้ตัวระบุ R* License
- **false** = ใช้ตัวระบุ Steam

{{% alert theme="info" %}}
หากเปิดใช้งาน ตรวจสอบ R* License จำเป็นที่จะต้องใช้งาน es_extended เวอร์ชั่น 1.2.0 ขึ้นไป (ไม่แนะนำให้ใช้งาน R* License)
{{% /alert %}}

### `remove_command`

คำสั่งที่ใช้ในการตรวจสอบเเละดำเนินการลบข้อมูลของผู้เล่น

```lua
Config['remove_command'] = 'wlremoveall'
```

### `remove_set_day`

ผู้เล่นที่ไม่เชื่อมต่อกับเซิร์ฟเวอร์ติดต่อกันตามจำนวนวันที่ระบุ

```lua
Config['remove_set_day'] = 30
```

{{% alert theme="info" %}}
จะถูกลบข้อมูลบัญชีออกจากฐานข้อมูลของเซิร์ฟเวอร์ หลังจากที่ใช้คำสั่งที่กำหนดในการตั้งค่า <a href="#remove_command">remove_command</a>
{{% /alert %}}

### `remove_delay`

ดีเลย์ในการลบข้อมูลผู้เล่นต่อ 1 รายการ (มิลลิวินาที)

```lua
Config['remove_delay'] = 1500
```

### `webhook_remove_logs`

ลิงก์ Discord Webhook สำหรับเก็บบันทึกการลบข้อมูลของผู้เล่น

```lua
Config['webhook_remove_logs'] = 'Webhook URL'
```

### `database_list`

ตาราง เเละ คอลัมน์ ฐานข้อมูลเซิร์ฟเวอร์ เพื่อใช้ในการลบข้อมูลของผู้เล่น

```lua
Config['database_list'] = {
	{
		['table_data'] = 'addon_account_data',				-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'owner'						-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'addon_inventory_items',			-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'owner'						-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'billing',							-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'identifier'				-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'datastore_data',					-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'owner'						-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'owned_properties',				-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'owner'						-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'owned_vehicles',					-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'owner'						-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'rented_vehicles',					-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'owner'						-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'society_moneywash',				-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'identifier'				-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'users',							-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'identifier'				-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'user_licenses',					-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'owner'						-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	},

	{
		['table_data'] = 'vehicle_sold',					-- ชื่อของตารางในฐานข้อมูล
		['column_identifier'] = 'soldby'					-- ชื่อของคอลัมน์ที่เก็บตัวระบุ
	}
}
```
