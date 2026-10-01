# การตั้งค่า (Config)

| ไฟล์ | โหลดที่ | ใช้ทำอะไร |
| --- | --- | --- |
| `config/config.general.lua` | shared | เงื่อนไขการปล้น, อาวุธ, อาชีพ, โซน, ป้าย, ปุ่ม, หลอดโหลด, อนิเมชัน, ตำรวจ |
| `config/config.items.lua` | shared | ไอเทมกันปล้น, blacklist/whitelist ล้วง-ยัด, เปิด/ปิดปล้นอาวุธและเงิน |
| `config/config.locale.lua` | shared | ข้อความแจ้งเตือน 21 ข้อความ |
| `config/config.shared.lua` | shared | path รูปไอเทม, เปิด/ปิดการเชื่อม Hyper_Notifyall / Discordlogs / Hyper_Check |
| `config/config.log.lua` | server | log ผ่าน Hyper_Discordlogs + webhook สำรอง |
| `config/config.security.lua` | server | ค่าตรวจการตาย (DeathGuard) — client มองไม่เห็น |

## ค่าที่ปรับบ่อย

```lua
Config.MaxDistance = 2.5               -- ระยะปล้น (เมตร)
Config.DeathBodyTime = 150             -- ปล้นศพได้กี่วินาที
Config.OnlyKillerCanRobDeadPlayer = true

Config.WeaponsUsedForRobbery = {
    "WEAPON_KNIFE", "WEAPON_DAGGER", "WEAPON_BOTTLE",
    "WEAPON_MACHETE", "WEAPON_SWITCHBLADE", "WEAPON_GOLFCLUB",
}

Config.AllowJobsForRobbery = { ["unemployed"] = true }
Config.OnlineJobsNeedForRobbing = { -- ['police'] = 1,
}
Config.BlockZone = { -- { coords = vector3(0.0, 0.0, 0.0), radius = 15.0 },
}
```

## หลอดโหลดและตำรวจ

```lua
Config.Progress = { enable = true, time = 3500, layout = "bottomCenter", canCancel = true, cancelKey = 73, freeze = true }

Config.Police = {
    alert = true, jobName = "police", cooldown = 30,
    blip = { sprite = 459, color = 1, scale = 1.0, time = 180 },
    label = "มีการปล้นผู้เล่น",
    externalEvent = "", -- ใส่ชื่อ event ถ้าใช้ระบบแจ้งตำรวจภายนอก
}
```

## Blacklist ไอเทม

```lua
Config.AllowedList = {
    take = {
        items = { type = "blacklist", list = { "water", "id_card" } },
        weapons = { type = "blacklist", list = { "WEAPON_BAT" } },
        accounts = { type = "blacklist", list = { "bank" } },
    },
    put = {
        items = { type = "blacklist", list = { "id_card" } },
        weapons = { type = "blacklist", list = {} },
        accounts = { type = "blacklist", list = { "bank" } },
    },
}
```

`type = "whitelist"` = อนุญาตเฉพาะชื่อในลิสต์

## DeathGuard (server-only)

| ค่า | ค่าเริ่มต้น | ความหมาย |
| --- | --- | --- |
| `damageWindow` | 15 วินาที | อายุของ last-damager ที่ยังนับเป็นคนฆ่า |
| `explosionRadius` | 12.0 เมตร | รัศมีระเบิดที่นับว่าโดน |
| `markCooldown` | 10 วินาที | เข้าสถานะศพถี่กว่านี้ = ผิดปกติ |
| `reverifyDelay` | 2 วินาที | รอแล้วตรวจซ้ำว่าตายจริง |
| `aliveHealth` | 190 | เลือดเท่านี้ขึ้นไป = ยังไม่ตาย |
