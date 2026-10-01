# การเชื่อมต่อ (Export)

Hyper_Thief **ไม่มี export ของตัวเอง** (สแกนทั้งเซิร์ฟแล้ว: 0 export, ไม่มี resource ไหนเรียกใช้) ระบบทำงานโดยเรียก export ของ resource อื่น และเปิด event ให้ Hyper_Inventory ยิงกลับ

## Export ที่ Hyper_Thief เรียกใช้

| Resource | Export | ฝั่ง | ใช้ทำอะไร |
| --- | --- | --- | --- |
| Hyper_Inventory | `OpenStashExternal(playerId, opts)` | server | เปิดตู้ "ปล้น: ชื่อเหยื่อ" จากกระเป๋าเหยื่อ |
| Hyper_Inventory | `RefreshStash(playerId, id, items)` | server | อัปเดตตู้หลังย้ายของ |
| Hyper_Inventory | `CloseInventory()` | client | ปิดตู้เมื่อเหยื่อออก/ศพหมดเวลา |
| Hyper_Notifyall | `sendNotify(option)` | client | การ์ดแจ้งเตือนมุมขวาบน |
| Hyper_Notifyall | `progressBar(option)` / `stopProgressBar()` | client | หลอดโหลด 3.5 วินาที |
| Hyper_Check | `AssertEventTrigger(src, event)` | server | ตรวจ event ก่อนทำงาน |
| Hyper_Check | `RegisterTrustedEvent(event, res)` | server | ลงทะเบียน 2 net event |
| Hyper_Discordlogs | `CreateLog(data)` | server | log หมวด `thief`, `thief_sec` |

## ตัวอย่าง: เปิดหน้าต่างปล้น

```lua
exports["Hyper_Inventory"]:OpenStashExternal(source, {
    id = "hyperthief_" .. targetServerId,
    label = L("stash_label", Framework.GetName(victim)),
    slots = 999,
    items = buildVictimItems(victim),
    events = {
        take = "Hyper_Thief:stashTake",
        store = "Hyper_Thief:stashStore",
        close = "Hyper_Thief:stashClose",
    },
})
```

Hyper_Inventory ยิง `take` / `store` กลับมาพร้อม `(robberSrc, name, count, itype)` — `itype` เป็น `item`, `weapon` หรือ `account` แล้ว Hyper_Thief ย้ายของเองและเรียก `RefreshStash`

## Event ของ Hyper_Thief

| Event | ชนิด | ทิศทาง | หน้าที่ |
| --- | --- | --- | --- |
| `Hyper_Thief:server:rob` | net (trusted) | client → server | ขอปล้นเป้าหมาย |
| `Hyper_Thief:server:setState` | net (trusted) | client → server | แจ้งยกมือ/คุกเข่า/เลิก |
| `esx:onPlayerDeath` | net | client → server | ตั้งสถานะศพ (ไม่เชื่อ data จาก client) |
| `Hyper_Thief:stashTake` / `stashStore` / `stashClose` | server | Hyper_Inventory → Hyper_Thief | ย้ายของ / ปิดตู้ |
| `Hyper_Thief:notify` / `forceClose` / `policeAlert` | client | server → client | แจ้งเตือน / ปิดตู้ / blip ตำรวจ |

{% hint style="warning" %}
`esx:onPlayerDeath` ถูก Hyper_Thief ลงทะเบียนเป็น net event — resource อื่นที่ฟัง event นี้ฝั่ง server (เช่น Hyper_Ranking) ต้องไม่เชื่อ data ที่ client ส่งมา
{% endhint %}

## ต่อกับระบบแจ้งตำรวจภายนอก

ใส่ชื่อ event ใน `Config.Police.externalEvent` แล้ว Hyper_Thief จะยิง `TriggerEvent(externalEvent, "thief", coords)` ฝั่ง server แทน blip ในตัว
