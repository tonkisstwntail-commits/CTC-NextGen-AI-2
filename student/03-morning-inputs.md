<!-- workshop-header -->
<img width="1347" height="127" alt="Coding Thailand 2026 header" src="https://github.com/user-attachments/assets/ba5cf267-f460-4fb0-b69b-c461ae061a3b" />

# 🔌 ต่อ Input 3 แบบ

วันนี้จะลองต่อให้ครบทั้ง 3 แบบ บ่ายค่อยเลือก 1 อย่างไปเทรน
> UNO Q มีสองสมอง: **sensor (Modulino)** อ่านฝั่ง MCU ส่วน **กล้อง/ไมค์ (USB)** อ่านฝั่ง Linux

---

## Input 1 — Modulino (Qwiic) — ลองครบทั้ง 7 ตัว

Modulino มี **7 ตัว** เช้านี้ลองให้ครบ **เผื่อไอเดีย** บ่ายค่อยเลือกตัวที่ทีมชอบไปเทรน
ทุกตัวเสียบ Qwiic (เสียบผิดด้านเข้าไม่ได้ ปลอดภัย) อ่าน/สั่งจากฝั่ง MCU

| # | Modulino | ทำอะไร | ใช้เป็น AI input | ไอเดีย |
|---|----------|--------|------------------|--------|
| 1 | **Movement** (IMU) | ความเร่ง x/y/z | ✅ ดีมาก | จำท่ามือ · จับการล้ม · ตรวจการสั่น |
| 2 | **Distance** (ToF) | ระยะ (มม.) | ✅ ได้ | นับคนผ่าน · gesture เลื่อนมือ |
| 3 | **Thermo** | อุณหภูมิ + ความชื้น | ✅ ได้ | เฝ้าอุณหภูมิ · แยกร้อน/ปกติ/เย็น |
| 4 | **Buttons** | ปุ่ม A/B/C | ⚠️ ใช้ติด label | กำกับ class ตอนเก็บ data |
| 5 | **Knob** | หมุน + กด | ⚠️ ใช้ปรับค่า | ปรับ threshold · เลือกโหมด |
| 6 | **Pixels** | LED RGB 8 ดวง | ❌ output | แสดงสีตาม class ที่ทำนาย |
| 7 | **Buzzer** | เล่นโทนเสียง | ❌ output | เตือนเสียงเมื่อเจอเหตุการณ์ |

**ลองยังไง (ใช้ App Lab อย่างเดียว):**
1. ต่อสาย Qwiic `UNO Q → Modulino` (ต่อหลายตัว daisy-chain ได้)
2. App Lab → **+ New** App → ไปส่วน **Sketch** (ฝั่ง Arduino/MCU)
3. ก็อปโค้ดจากไฟล์ `.ino` ใน [examples/modulino/](examples/modulino/) ตัวที่อยากลอง วางในตัวแก้ไข
   - ไลบรารี `Modulino` มีให้แล้ว — ถ้าไม่เจอ เพิ่มผ่าน **Library Manager** (ค้น "Modulino")
4. กด **Run** ▶ → App Lab build + upload ลง MCU ให้เอง
5. เปิด **Serial Monitor** ตั้ง baud **9600** → ขยับ/กด/หมุน ดูค่าขยับ

> ไม่ต้องลง Arduino IDE แยก · ตัวอย่างเป็น Sketch ฝั่ง MCU ล้วน (ฝั่ง Python ไว้ใช้ตอนบ่าย)
> ✅ **ผ่านเมื่อ:** ลองแล้วอย่างน้อย 3 ตัว และค่า/ไฟ/เสียงตอบสนองจริง
> 💡 จดไว้ว่า "ตัวไหนให้ค่าที่แยกสถานการณ์ได้ชัด" — นั่นคือตัวที่เหมาะไปเทรนบ่ายนี้

ตัวอย่างโค้ดครบทั้ง 7 ตัว + ตารางไอเดีย: [examples/modulino/README.md](examples/modulino/README.md)

### 🏆 ลองครบแล้ว? ไปต่อที่ Sensor Challenges

โจทย์เชื่อมเช้า → บ่าย ใน [examples/modulino/challenges/](examples/modulino/challenges/):
- **Challenge A** — Proximity Alarm: ของเข้าใกล้แล้ว Buzzer ร้อง (input → logic → output)
- **Challenge B** — เก็บ Movement เป็น CSV เตรียมไปเทรน Edge Impulse ตอนบ่าย

---

## Input 2 — USB Webcam (ฝั่ง Linux / Python App)

ต่างจาก Modulino — กล้องอ่านจาก **ฝั่ง Linux** เป็น **Python App** ใน App Lab

1. เสียบ webcam เข้า **powered USB hub** (hub ที่มีไฟเลี้ยง) แล้วต่อ hub เข้าบอร์ด
2. **ง่ายสุด:** App Lab → New App → เปิด example หมวด **Camera / Vision** → Run → เห็นภาพสด
3. หรือรันสคริปต์ของเรา: [examples/camera/camera_check.py](examples/camera/camera_check.py) → เอามือบังกล้องแล้วค่า brightness เปลี่ยน

> ⚠️ ตอนใช้กล้อง ให้บอร์ดอยู่บน **Wi-Fi** **อย่าต่อบอร์ดเข้าคอมโดยตรง** ไม่งั้นจะหากล้องไม่เจอ

เช็กบน shell (`>_`) ได้: `lsusb` / `ls /dev/video*` · คู่มือเต็ม: [examples/camera/README.md](examples/camera/README.md)

> ✅ **ผ่านเมื่อ:** เห็นภาพสด หรือค่า brightness ขยับเมื่อบังกล้อง

---

## Input 3 — USB Mic (ฝั่ง Linux / Python App)

ไมค์ก็อ่านจาก **ฝั่ง Linux** เหมือนกล้อง

1. เสียบ mic เข้า powered hub → เช็กบน shell: `arecord -l` (เห็น card ไมค์)
2. **ง่ายสุด:** App Lab → New App → เปิด example หมวด **Audio / Microphone** → Run → พูดแล้ว level ขยับ
3. หรือรันสคริปต์ของเรา: [examples/mic/mic_check.py](examples/mic/mic_check.py) → อัด 3 วินาที ได้ไฟล์ `test.wav`

เช็กไฟล์ที่อัดว่ามีเสียงจริง · คู่มือเต็ม: [examples/mic/README.md](examples/mic/README.md)

> ✅ **ผ่านเมื่อ:** พูดแล้ว level ขยับ หรืออัดได้ไฟล์ที่มีเสียง

---

ต่อไม่ขึ้น? เปิด [troubleshooting.md](troubleshooting.md) ข้อ 2

เสร็จเช้าแล้ว ลองคิดกันในทีม: อยากสอน AI ให้ **มอง / ฟัง / รู้สึก** อะไร? บ่ายจะได้เลือก input ไปเทรน
