# Hyper_Thief

ระบบปล้นผู้เล่นของเซิร์ฟ Hyper (ESX) — ถืออาวุธระยะประชิด เข้าใกล้เป้าหมายในระยะ 2.5 เมตร กด **G** แล้วกระเป๋าของเหยื่อจะเปิดเป็นตู้ฝั่งขวาของ Hyper_Inventory ลากของออกหรือยัดของเข้าได้ทันที

![หน้าต่างปล้น](.gitbook/assets/01_rob_stash.png)

เป้าหมายที่ปล้นได้มี 3 สถานะ: **ยกมือ (X)**, **คุกเข่า (Y)** และ **นอนตาย** (ปล้นศพได้ภายใน 150 วินาที เฉพาะคนที่ฆ่า) ทุกการตัดสินใจ — ระยะ อาชีพ โซนห้ามปล้น ใครเป็นคนฆ่า และการย้ายของ — ทำที่ฝั่ง server ทั้งหมด

{% hint style="info" %}
Hyper_Thief ไม่มีหน้า NUI ของตัวเอง หน้าต่างปล้นคือตู้ของ **Hyper_Inventory** (`OpenStashExternal`) ส่วนหลอดโหลดและการ์ดแจ้งเตือนมาจาก **Hyper_Notifyall**
{% endhint %}

| รายการ | ค่า |
| --- | --- |
| เวอร์ชัน | 1.0.0 |
| Framework | ESX (`es_extended`) — bridge แยกไว้ใน `config/framework/esx/` |
| Dependencies | es_extended, Hyper_Inventory, Hyper_Notifyall |
| เชื่อมเสริม | Hyper_Check (trusted event + Code Vault), Hyper_Discordlogs (หมวด `thief`, `thief_sec`) |
| ไฟล์ client | ส่งผ่าน Hyper_Check Code Vault ไม่ cache บนเครื่องผู้เล่น |

## ปุ่มลัด

| ปุ่ม | คำสั่ง | ทำอะไร |
| --- | --- | --- |
| G | `hyperthief_rob` | เริ่มปล้นเป้าหมายที่ใกล้ที่สุด |
| Y | `hyperthief_kneel` | คุกเข่า (เปิด/ปิด) |
| X | `hyperthief_handsup` | ยกมือ (เปิด/ปิด) |

ผู้เล่นเปลี่ยนปุ่มเองได้ใน Settings → Key Bindings → FiveM
