# ฟีเจอร์หลัก

ปล้นได้ 3 สถานะ ล้วงได้ 3 ชนิดของ (ไอเทม · อาวุธ · เงิน) และยัดของคืนใส่เหยื่อได้ ทุกค่าด้านล่างมาจาก `config/*.lua`

| ฟีเจอร์ | รายละเอียด | ค่าใน config |
| --- | --- | --- |
| ปล้นคนยกมือ | เหยื่อกด X ยกมือ | `RobHandsUpPlayer = true` |
| ปล้นคนคุกเข่า | เหยื่อกด Y คุกเข่า | `RobKneelPlayer = true` |
| ปล้นศพ | ปล้นได้ภายใน 150 วินาทีหลังตาย เฉพาะคนที่ฆ่า | `DeathBodyTime = 150`, `OnlyKillerCanRobDeadPlayer = true` |
| อาวุธที่ใช้จี้ | 6 ชนิด: KNIFE, DAGGER, BOTTLE, MACHETE, SWITCHBLADE, GOLFCLUB | `WeaponsUsedForRobbery` |
| ระยะปล้น | 2.5 เมตร server วัดพิกัดเอง | `MaxDistance = 2.5` |
| หลอดโหลดก่อนปล้น | 3.5 วินาที ล็อกเดิน/ยิง กด X ยกเลิกได้ | `Progress.time = 3500` |
| หน้าต่างปล้น | ตู้ฝั่งขวาของ Hyper_Inventory ชื่อ "ปล้น: ชื่อเหยื่อ" 999 ช่อง | `OpenStashExternal` |
| ของที่ล้วงได้ | ไอเทม, อาวุธ, เงินสด/เงินดำ (ห้ามเงินธนาคาร) | `AllowStealWeapon`, `AllowStealAccount` |
| Blacklist | ห้ามล้วง `water`, `id_card`, `WEAPON_BAT`, `bank` · ห้ามยัด `id_card`, `bank` | `AllowedList.take / put` |
| ยัดของใส่เหยื่อ | ลากของจากกระเป๋าผู้ปล้นไปฝั่งเหยื่อ | event `store` |
| อาชีพที่ปล้นได้ | ค่าเริ่มต้น `unemployed` | `AllowJobsForRobbery` |
| ต้องมีตำรวจออนไลน์ | ตั้งจำนวนต่ออาชีพได้ (ค่าเริ่มต้นปิด) | `OnlineJobsNeedForRobbing` |
| โซนห้ามปล้น | จุด + รัศมี (ค่าเริ่มต้นว่าง) | `BlockZone` |
| ไอเทมกันปล้น | เหยื่อถือไอเทมนี้ = ปล้นไม่ได้ (ค่าเริ่มต้นว่าง) | `ProtectionItems` |
| ป้ายเหนือหัว | `[Rob]` เหนือคนที่ปล้นได้ในระยะ 3 เมตร | `ShowIndicator`, `IndicatorDistance = 3.0` |
| แจ้งตำรวจ | blip 180 วินาที cooldown 30 วินาทีต่อผู้ปล้น หรือส่งเข้า event ภายนอก | `Config.Police` |
| Log | ส่ง Hyper_Discordlogs หมวด `thief` และ `thief_sec` + webhook สำรอง | `Config.Log` |

**กันปล้นซ้อน:** เหยื่อ 1 คนถูกปล้นได้ทีละ 1 คน และหน้าต่างปิดเองเมื่อศพหมดเวลา เหยื่อออกเกม หรือตรวจพบว่าแกล้งตาย
