# เทคโนโลยีและโครงสร้าง

โค้ด Lua 1,684 บรรทัดใน 16 ไฟล์ ส่วนใหญ่อยู่ฝั่ง server (`core/server/main.lua` 658 บรรทัด) ฝั่ง client ทำแค่รับปุ่ม เล่นอนิเมชัน และขอปล้น

## ลำดับการปล้น

1. เหยื่อกด X/Y → ตั้ง state bag `hyperthief_state` และแจ้ง server ผ่าน `Hyper_Thief:server:setState`
2. ผู้ปล้นกด G → client เช็คอาวุธในมือ + หาคนใกล้สุด → หลอดโหลด 3.5 วินาที
3. ยิง `Hyper_Thief:server:rob` → server ตรวจ อาชีพ · ตำรวจออนไลน์ · โซนห้าม · ระยะ · สถานะเหยื่อ · ไอเทมกันปล้น · การปล้นซ้อน
4. ผ่านทั้งหมด → `exports.Hyper_Inventory:OpenStashExternal` เปิดตู้ `hyperthief_<id>` + แจ้งเหยื่อ + แจ้งตำรวจ
5. ทุกครั้งที่ลากของ → event `take` / `store` เช็คระยะและสถานะซ้ำ ย้ายของจริง เขียน log แล้ว `RefreshStash`

## ความปลอดภัย

* **Server ตัดสินทุกอย่าง:** ระยะวัดจากพิกัด ped ฝั่ง server ทั้งตอนเปิดและทุกครั้งที่ย้ายของ จำนวนถูกตัดให้ไม่เกินของที่มีจริง
* **คนฆ่ามาจาก server:** จำ last-damager จาก `weaponDamageEvent` และ `explosionEvent` (รัศมี 12 เมตร อายุ 15 วินาที) ไม่อ่าน `killerServerId` ที่ client ส่งมา
* **กันแกล้งตาย:** เข้าสถานะศพถี่กว่า 10 วินาที = ปฏิเสธ + log ตรวจซ้ำหลัง 2 วินาที ถ้าเลือด ≥ 190 ถอนสถานะศพและปิดตู้ผู้ปล้น
* **ห้ามทับสถานะศพ:** ศพที่ยังไม่หมดเวลาส่ง handsup มาล้างสิทธิ์คนฆ่าไม่ได้
* **Hyper_Check:** 2 net event ลงทะเบียนเป็น trusted event และไฟล์ client 3 ไฟล์ส่งผ่าน Code Vault
* **เคลียร์สถานะ:** ผู้เล่นออกเกม → ล้างตารางทุกตัวและปิดตู้ฝั่งที่ค้างอยู่

## โครงไฟล์

| โฟลเดอร์ | ไฟล์ |
| --- | --- |
| `config/` | general, items, locale (21 ข้อความ), log, security, shared |
| `config/framework/esx/` | bridge client / server / shared — เปลี่ยน framework แก้ที่นี่ที่เดียว |
| `core/` | client/main.lua, server/main.lua, shared/common.lua, shared/version.lua |
| `utils/` | utils.client.lua (notify), utils.server.lua (log + webhook) |
