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
	['server_status_add'] = 'esx_status:add'
}
```

{{% alert theme="info" %}}
ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

### `item`

ชื่อของ ชุดดำน้ำลึก, ชุดดำน้ำตื้น และ ถังออกซิเจน ที่ตรงกับรายการในฐานข้อมูล ตาราง items คอลัมน์ name

```lua
Config['item'] = {
	['scuba_gear'] = 'scuba_gear',							-- ชื่อ ชุดดำน้ำลึก ในฐานข้อมูล
	['scuba_oxygen_tank'] = 'scuba_oxygen_tank',			-- ชื่อ ถังออกซิเจน ในฐานข้อมูล
	['snorkelling_gear'] = 'snorkelling_gear'				-- ชื่อ ชุดดำน้ำตื้น ในฐานข้อมูล
}
```

### `use_scuba_gear_in_water`

สามารถใช้งาน ชุดดำน้ำลึก ใต้น้ำ

```lua
Config['use_scuba_gear_in_water'] = false
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `use_scuba_oxygen_tank_in_water`

สามารถใช้งาน ถังออกซิเจน เพื่อเติม ออกซิเจน ใต้น้ำ

```lua
Config['use_scuba_oxygen_tank_in_water'] = false
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `use_snorkelling_gear_in_water`

สามารถใช้งาน ชุดดำน้ำตื้น ใต้น้ำ

```lua
Config['use_snorkelling_gear_in_water'] = false
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `scuba_oxygen_add`

จำนวน ออกซิเจน ที่ได้รับหากใช้งานไอเทม ถังออกซิเจน จำนวน 1 ถัง

```lua
Config['scuba_oxygen_add'] = 500000
```

{{% alert theme="info" %}}
ค่าสูงสุดอยู่ที่ 1,000,000 ตามที่ [esx_status](https://github.com/esx-framework/esx_status) กำหนด
{{% /alert %}}

## การตั้งค่าฝั่ง Client

สามารถตั้งค่าได้ที่ไฟล์ `config.client.lua`

### `esx_routers`

เส้นทางกิจกรรมของทรัพยากร ESX Framework หาก es_extended เซิร์ฟเวอร์ของคุณ มีการแก้ไขชื่อกิจกรรมของทรัพยากร เพื่อป้องกันโปรแกรมโกงต่างๆ

```lua
Config['esx_routers'] = {
	['client_shared_obj'] = 'esx:getSharedObject',
	['client_re_loadout'] = 'esx:restoreLoadout',
	['client_player_load'] = 'esx:playerLoaded',
	['client_player_skin'] = 'esx_skin:getPlayerSkin',
	['client_status_loaded'] = 'esx_status:loaded',
	['client_status_register'] = 'esx_status:registerStatus',
	['client_status_get'] = 'esx_status:getStatus',
	['client_status_remove'] = 'esx_status:remove',
	['client_status_set'] = 'esx_status:set'
}
```

{{% alert theme="info" %}}
ห้ามแก้ไขการตั้งค่าในส่วนนี้โดยเด็ดขาด หากคุณไม่เข้าใจว่าสิ่งนี้คืออะไร เพราะอาจจะทำให้ทรัพยากรเกิดข้อผิดพลาดได้
{{% /alert %}}

### `esx_status_max`

ค่าสูงสุดที่กำหนดไว้ในทรัพยากร [esx_status](https://github.com/esx-framework/esx_status)

```lua
Config['esx_status_max'] = 1000000
```

{{% alert theme="info" %}}
ค่าสูงสุดอยู่ที่ 1,000,000 ตามที่ [esx_status](https://github.com/esx-framework/esx_status) กำหนด
{{% /alert %}}

### `scuba_oxygen_remove`

จำนวน ออกซิเจน ที่ลดลงต่อ 1 วินาที ในขณะที่ใช้งาน ชุดดำน้ำลึก

```lua
Config['scuba_oxygen_remove'] = 1000
```

### `snorkelling_depth`

ชุดดำน้ำตื้น สามารถดำน้ำได้ไม่เกินระยะที่กำหนด

```lua
Config['snorkelling_depth'] = 10
```

{{% alert theme="info" %}}
ตรวจสอบจาก Coords Z
{{% /alert %}}

### `snorkelling_timer`

ชุดดำน้ำตื้น สามารถดำน้ำได้กี่วินาที (วินาที)

```lua
Config['snorkelling_timer'] = 30
```

### `snorkelling_timer_recovery`

ชุดดำน้ำตื้น หากขึ้นมาเหนือน้ำ จะฟื้นฟูเวลาในการดำน้ำตามค่าที่ระบุ (วินาที)

```lua
Config['snorkelling_timer_recovery'] = 1
```

### `object`

Prop สำหรับ ชุดดำน้ำลึก และ ชุดดำน้ำตื้น

```lua
Config['object'] = {
	['scuba'] = {										    -- Prop ชุดดำน้ำลึก
		['enable'] = true,								    -- เปิดใช้งาน Prop ชุดดำน้ำลึก
		['mask'] = 'p_michael_scuba_mask_s',			    -- ชื่อ หน้ากาก (Object Name)
		['tank'] = 'p_michael_scuba_tank_s',				-- ชื่อ ถังออกซิเจน (Object Name)
		['light'] = true									-- เปิดใช้งาน ไฟฉาย ชุดดำน้ำลึก หรือไม่?
	},
	['snorkelling'] = {									    -- Prop ชุดดำน้ำตื้น
		['enable'] = true,								    -- เปิดใช้งาน Prop ชุดดำน้ำตื้น
		['mask'] = 'p_d_scuba_mask_s'					    -- ชื่อ หน้ากาก (Object Name)
	}
}
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `animation`

Animation ในขณะที่ใช้งาน ชุดดำน้ำลึก และ ชุดดำน้ำตื้น

```lua
Config['animation'] = {
	['dict_clothing'] = 'clothingtie',
	['anim_clothing'] = 'try_tie_negative_a',
	['delay_clothing'] = 1200
}
```

### `skin_color_random`

สีแบบสุ่ม สำหรับ ชุดดำน้ำลึก และ ชุดดำน้ำตื้น

```lua
Config['skin_color_random'] = {
	['scuba_enable'] = true,							    -- เปิดใช้งาน สุ่มสี ชุดดำน้ำลึก
	['scuba_male'] = {									    -- รหัสสี ชุดดำน้ำลึก แบบสุ่ม (ชาย)
		['color_min'] = 0,								    -- รหัสสี น้อย ที่สุด
		['color_max'] = 25,								    -- รหัสสี มาก ที่สุด
		['color_position'] = {							    -- ตำแหน่ง สุ่มสี ชุดดำน้ำลึก (ชาย)
			'tshirt_2', 'torso_2', 'pants_2', 'shoes_2'
		}
	},
	['scuba_female'] = {								    -- รหัสสี ชุดดำน้ำลึก แบบสุ่ม (หญิง)
		['color_min'] = 0,								    -- รหัสสี น้อย ที่สุด
		['color_max'] = 25,								    -- รหัสสี มาก ที่สุด
		['color_position'] = {							    -- ตำแหน่ง สุ่มสี ชุดดำน้ำลึก (หญิง)
			'tshirt_2', 'torso_2', 'pants_2', 'shoes_2'
		}
	},
	['snorkelling_enable'] = true,						    -- เปิดใช้งาน สุ่มสี ชุดดำน้ำตื้น
	['snorkelling_male'] = {							    -- รหัสสี ชุดดำน้ำตื้น แบบสุ่ม (ชาย)
		['color_min'] = 0,								    -- รหัสสี น้อย ที่สุด
		['color_max'] = 6,								    -- รหัสสี มาก ที่สุด
		['color_position'] = {							    -- ตำแหน่ง สุ่มสี ชุดดำน้ำตื้น (ชาย)
			'pants_2'
		}
	},
	['snorkelling_female'] = {							    -- รหัสสี ชุดดำน้ำตื้น แบบสุ่ม (หญิง)
		['color_min'] = 0,								    -- รหัสสี น้อย ที่สุด
		['color_max'] = 11,								    -- รหัสสี มาก ที่สุด
		['color_position'] = {							    -- ตำแหน่ง สุ่มสี ชุดดำน้ำตื้น (หญิง)
			'tshirt_2', 'torso_2', 'decals_2', 'pants_2'
		}
	}
}
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `skin_color_scuba_agencies`

สี ชุดดำน้ำลึก สำหรับ หน่วยงาน Ambulance และ Police

```lua
Config['skin_color_scuba_agencies'] = {
	['enable'] = true,									    -- เปิดใช้งาน กำหนดสี ชุดดำน้ำลึก หน่วยงาน
	['ambulance'] = {
		['name'] = 'ambulance',							    -- ชื่อ หน่วยงาน Ambulance
		['color'] = 0,									    -- รหัสสี ชุดดำน้ำลึก หน่วยงาน Ambulance
		['color_position'] = {							    -- ตำแหน่ง สี ชุดดำน้ำลึก หน่วยงาน Ambulance
			'tshirt_2', 'torso_2', 'pants_2', 'shoes_2'	    -- ตำแหน่ง สี ชุดดำน้ำลึก หน่วยงาน Ambulance
		}
	},
	['police'] = {
		['name'] = 'police',							    -- ชื่อ หน่วยงาน Police
		['color'] = 0,									    -- รหัสสี ชุดดำน้ำลึก หน่วยงาน Police
		['color_position'] = {							    -- ตำแหน่ง สี ชุดดำน้ำลึก หน่วยงาน Police
			'tshirt_2', 'torso_2', 'pants_2', 'shoes_2'	    -- ตำแหน่ง สี ชุดดำน้ำลึก หน่วยงาน Police
		}
	}
}
```

- **true** = เปิดใช้งาน
- **false** = ปิดใช้งาน

### `skin`

Skin ชุดดำน้ำลึก และ ชุดดำน้ำตื้น

```lua
Config['skin']= {
	['scuba'] = {										    -- Skin ชุดดำน้ำลึก (Scuba)
		['male'] = {									    -- Skin ผู้ชาย
			['hair_1'] = 0,			['hair_2'] = 0,
			['hair_color_1'] = 0,	['hair_color_2'] = 0,
			['tshirt_1'] = 15,		['tshirt_2'] = 0,
			['ears_1'] = -1,		['ears_2'] = 0,
			['torso_1'] = 243,		['torso_2'] = 0,
			['decals_1'] = 0,		['decals_2']= 0,
			['mask_1'] = 0, 		['mask_2'] = 0,
			['arms'] = 31,			['arms_2'] = 0,
			['pants_1'] = 94,		['pants_2'] = 0,
			['shoes_1'] = 67,		['shoes_2'] = 0,
			['helmet_1'] = -1,		['helmet_2'] = 0,
			['bags_1'] = -1,		['bags_2'] = 0,
			['glasses_1'] = -1,		['glasses_2'] = 0,
			['chain_1'] = 0,		['chain_2'] = 0,
			['bproof_1'] = 0, 		['bproof_2'] = 0
		},

		['female'] = {									    -- Skin ผู้หญิง
			['hair_1'] = 0,			['hair_2'] = 0,
			['hair_color_1'] = 0,	['hair_color_2'] = 0,
			['tshirt_1'] = 15,		['tshirt_2'] = 0,
			['ears_1'] = -1,		['ears_2'] = 0,
			['torso_1'] = 251,		['torso_2'] = 0,
			['decals_1'] = 0,		['decals_2'] = 0,
			['mask_1'] = 0, 		['mask_2'] = 0,
			['arms'] = 36,			['arms_2'] = 0,
			['pants_1'] = 97,		['pants_2'] = 0,
			['shoes_1'] = 70,		['shoes_2'] = 0,
			['helmet_1']= -1,		['helmet_2'] = 0,
			['bags_1'] = -1,		['bags_2']	= 0,
			['glasses_1'] = -1,		['glasses_2'] = 0,
			['chain_1'] = 0,		['chain_2'] = 0,
			['bproof_1'] = 0,		['bproof_2'] = 0
		}
	},

	['snorkelling'] = {									    -- Skin ชุดดำน้ำตื้น (Snorkelling)
		['male'] = {									    -- Skin ผู้ชาย
			['hair_1'] = 0,			['hair_2'] = 0,
			['hair_color_1'] = 0,	['hair_color_2'] = 0,
			['tshirt_1'] = 15, 		['tshirt_2'] = 0,
			['ears_1'] = -1, 		['ears_2'] = 0,
            ['torso_1'] = 15, 		['torso_2'] = 0,
            ['decals_1'] = 0,  		['decals_2'] = 0,
            ['mask_1'] = 0, 		['mask_2'] = 0,
            ['arms'] = 15,			['arms_2'] = 0,
            ['pants_1'] = 54, 		['pants_2'] = 0,
            ['shoes_1'] = 67,		['shoes_2'] = 0,
            ['helmet_1'] = 8, 		['helmet_2'] = 0,
            ['bags_1'] = 43, 		['bags_2'] = 0,
			['glasses_1'] = -1, 	['glasses_2'] = 0,
			['chain_1'] = 0, 		['chain_2'] = 0,
            ['bproof_1'] = 0,  		['bproof_2'] = 0
		},

		['female'] = {									    -- Skin ผู้หญิง
			['hair_1'] = 0,			['hair_2'] = 0,
			['hair_color_1'] = 0,	['hair_color_2'] = 0,
			['tshirt_1'] = 15, 		['tshirt_2'] = 0,
			['ears_1'] = -1, 		['ears_2'] = 0,
            ['torso_1'] = 15, 		['torso_2'] = 0,
            ['decals_1'] = 0,  		['decals_2'] = 0,
            ['mask_1'] = 0, 		['mask_2'] = 0,
            ['arms'] = 15,			['arms_2'] = 0,
            ['pants_1'] = 15, 		['pants_2'] = 0,
            ['shoes_1'] = 70,		['shoes_2'] = 0,
            ['helmet_1'] = -1, 		['helmet_2']	= 0,
            ['bags_1'] = 43, 		['bags_2'] = 0,
			['glasses_1'] = -1, 	['glasses_2'] = 0,
			['chain_1'] = 0, 		['chain_2'] = 0,
            ['bproof_1'] = 0,  		['bproof_2'] = 0
		}
	}
}
```

### `pNotify`

การเเจ้งเตือน pNotify สำหรับ ชุดดำน้ำลึก และ ชุดดำน้ำตื้น

```lua
Config['pNotify'] = {									    -- การแจ้งเตือน pNotify
	['enable'] = false,									    -- เปิดใช้งาน
	['type'] = 'error',									    -- ประเภท (alert, success, error, warning, info)
	['timeout'] = 3000,									    -- เวลาที่เเสดง (1000 เท่ากับ 1 วินาที)
	['layout'] = 'bottomCenter',						    -- ตำแหน่งที่แสดง (top, topLeft, topCenter, topRight, center, cenerLeft, centerRight, bottom, bottomLeft, bottomCenter, bottomRight)
	['queue'] = 'global'								    -- ชื่อคิว (ตั้งค่าเป็น "global" โดยค่าเริ่มต้น)
}
```

* **true** = เปิดใช้งาน
* **false** = ปิดใช้งาน
