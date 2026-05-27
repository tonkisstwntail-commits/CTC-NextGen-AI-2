<!-- workshop-header -->
<img width="1347" height="127" alt="Coding Thailand 2026 header" src="https://github.com/user-attachments/assets/ba5cf267-f460-4fb0-b69b-c461ae061a3b" />

# 🎬 Anchor Demo — Gesture Wand

> ใช้เป็น demo เปิด workshop (09:15-09:30)
> **15 นาที** จาก Setup → Demo

นี่คือ demo ที่นักเรียนเห็นก่อน เพื่อให้รู้ว่า "ปลายทางที่ทีมต้องไปคืออะไร"

---

## 🎯 โจทย์ของ Demo

**Gesture Wand** — ทำให้ Modulino Movement กลายเป็นไม้กายสิทธิ์ที่รู้จักท่าทาง

**3 Classes:**
1. 🌀 **Circle** — หมุนเป็นวงกลม
2. ⚡ **Z-shape** — วาดเป็นรูป Z
3. 😴 **Still** — นิ่งๆ

**Output:**
- Modulino Pixels เปลี่ยนสีตามคลาส
- Circle → 🔵 น้ำเงิน
- Z-shape → 🟢 เขียว
- Still → ⚪ ขาว

---

## 📦 อุปกรณ์ที่ต้องเตรียม

- [ ] Arduino UNO Q
- [ ] Modulino Movement
- [ ] Modulino Pixels
- [ ] Qwiic cable ×2
- [ ] USB-C cable + Power
- [ ] Laptop + Arduino App Lab
- [ ] บัญชี Edge Impulse (ใช้ project ตั้งไว้แล้ว)

⚠️ **Pre-flight:** ทำ demo จริงรอบนี้ก่อนหน้า 1 วัน เพื่อมั่นใจว่า workflow ใช้ได้

---

## ⏱️ Demo Script (15 นาที)

### นาที 0:00-1:30 — Pre-recorded setup

> 💡 **เคล็ดลับ:** มี dataset + trained model เตรียมไว้แล้ว แต่ทำเหมือนสดเก็บใหม่ 5-10 samples เพื่อให้ดู authentic

```
[วิทยากรพูด]
"วันนี้เราจะมาทำ Gesture Wand กัน
ดูสิว่าใน 15 นาที เราสร้าง AI ที่รู้จักท่าทางได้ไหม"
```

ต่อ UNO Q → Modulino Movement → Modulino Pixels (daisy chain)
ใส่ในมือ ทำท่าเหมือนเตรียมร่ายเวทมนต์

---

### นาที 1:30-4:00 — Data Collection (Live)

เปิด Edge Impulse Studio → project "Gesture-Wand-Demo"

```
[วิทยากรพูด]
"Step 1: เก็บข้อมูล
ดู ผมจะวาดวงกลมในอากาศ 2 วินาที"
```

1. Go to **Data acquisition** tab
2. Click **Start sampling**
3. Label: `circle`, Length: 2000ms
4. Press Start → ทำท่าวงกลม → รอ data upload
5. Repeat 5 ครั้ง (ทำเร็วๆ ให้ดูง่าย)

**Key talking points ระหว่างเก็บ:**
- "เห็นไหมว่าแต่ละครั้งวงกลมไม่เหมือนเดิม 100% — นั่นคือ diversity"
- "ถ้าผมเก็บแต่วงกลมขนาดเดียว AI จะไม่รู้จักวงกลมขนาดอื่น"

ทำซ้ำกับ `z-shape` (5 ครั้ง) และ `still` (5 ครั้ง)

```
[วิทยากรพูด]
"ปกติเราจะเก็บ 50 ตัวอย่าง/คลาส
แต่ตอนนี้ผมมี dataset 50/class ที่เตรียมไว้แล้ว"
```

→ Switch ไปที่ project ที่เตรียมไว้ (มี data 50/class)

---

### นาที 4:00-7:00 — Training

```
[วิทยากรพูด]
"Step 2: Train AI ให้รู้จักท่าทาง"
```

1. Go to **Create Impulse**
2. Add processing block: **Spectral Analysis** (สำหรับ IMU)
3. Add learning block: **Classification**
4. Save Impulse
5. Spectral features → Generate features
6. NN Classifier:
   - Model size: **nano (2.4M)** ★ ย้ำให้นักเรียนเห็น
   - Training processor: **GPU**
   - Epochs: 30
7. Save & Train (รอ ~1-2 นาที)

**ระหว่างรอ train (1-2 นาที):**
- อธิบาย Confusion Matrix concept
- ถาม: "คิดว่า class ไหนจะ confuse กันมากที่สุด?"
- คาดเดา: circle อาจ confuse กับ z-shape ในตอนแรก

---

### นาที 7:00-9:00 — อ่านผล Training

แสดง training output:

```
Confusion Matrix:
              circle  z-shape  still
circle         [45]      4      1     ← 90% accuracy
z-shape         3      [42]     5     ← 84% accuracy
still           0       2     [48]    ← 96% accuracy

Validation accuracy: 90.0%
```

```
[วิทยากรพูด]
"เห็นไหม class still ทำงานดีที่สุด เพราะแยกง่าย
ส่วน circle กับ z-shape สับสนกันเล็กน้อย
นี่เป็นเรื่องปกติ — ในงานจริงเราจะ iterate ต่อ"
```

---

### นาที 9:00-11:00 — Deploy to UNO Q

1. Go to **Deployment**
2. เลือก **Arduino UNO Q**
3. Model size: nano
4. Build → รอ ~30 วินาที
5. Download

ใน Arduino App Lab:
1. Import model
2. Configure bricks:
   - Input: Modulino Movement
   - Output: Modulino Pixels (RGB)
3. Run on board

---

### นาที 11:00-14:00 — Live Demo 🎉

```
[วิทยากรพูด]
"ลุ้นกันว่าจะทำงานไหม"
```

**ทำท่าทีละท่า:**
1. นิ่งๆ → Pixels เป็นสีขาว ✓
2. วาดวงกลม → Pixels เป็นสีน้ำเงิน ✓
3. วาด Z → Pixels เป็นสีเขียว ✓

**สาธิต Edge cases (สำคัญ!):**
4. ทำท่าครึ่งๆ กลางๆ → ดูว่า model confused
5. ทำท่าเร็วมาก → ดูว่า model handle ได้ไหม
6. ส่งให้ผู้เข้าร่วม 1 คนลอง → "อันนี้ใช้ได้ไหม?"

```
[วิทยากรพูด]
"นี่คือเหตุผลที่เราเก็บข้อมูลจากหลายคน
ถ้าผมเก็บแค่ของผม → คนอื่นใช้ไม่ได้"
```

---

### นาที 14:00-15:00 — Wrap Up

```
[วิทยากรพูด]
"นี่คือ pipeline ที่ทีมจะทำในวันนี้:

  Data → Train → Deploy → Test → Iterate

แต่ละทีมจะทำ project ของตัวเอง — ไม่ใช่ gesture wand
เลือก track เลือกโจทย์ของทีมเอง"
```

→ Transition ไป Slide 11 (Pipeline Summary)

---

## 🛠️ Step-by-Step สำหรับ Backup Recording

หาก demo สด fail ใช้ video backup:

1. Record demo รอบ practice → save เป็น MP4
2. ใส่ใน `assets/anchor-demo-backup.mp4`
3. ถ้า demo สดพัง → "เอ่อ technical issue เล็กน้อย เปิด video เลยละกัน"

---

## 🎨 Sample Code Reference

### Arduino sketch สำหรับ deploy (ใน App Lab จะ generate ให้)

```cpp
#include <Modulino.h>
#include <gesture-wand_inferencing.h>  // จาก Edge Impulse export

ModulinoMovement movement;
ModulinoPixels pixels;

void setup() {
  Modulino.begin();
  movement.begin();
  pixels.begin();
}

void loop() {
  float features[NUM_FEATURES];
  // อ่าน accel จาก Modulino Movement
  collectFeatures(features);

  // Run inference
  ei_impulse_result_t result;
  run_classifier(features, &result);

  // ตอบสนอง output ตาม class
  String topClass = result.classification[0].label;
  if (topClass == "circle") {
    setPixelsColor(0, 0, 255);     // Blue
  } else if (topClass == "z-shape") {
    setPixelsColor(0, 255, 0);     // Green
  } else {
    setPixelsColor(255, 255, 255); // White
  }

  delay(100);
}
```

> ⚠️ Code นี้เป็น pseudocode สำหรับ reference — code จริงให้ใช้ที่ Arduino App Lab generate

---

## 📊 Expected Outcome

หลัง demo จบ นักเรียนควรเข้าใจ:

- ✅ Pipeline 4 ขั้นของ Edge AI
- ✅ ทำไม Edge Impulse ช่วยให้เร็วขึ้น
- ✅ UNO Q + Modulino เสียบใช้ง่าย
- ✅ Training มี config ที่ต้องระวัง (model size!)
- ✅ Test cases เผยจุดอ่อนของ model
- ✅ "ฉันก็ทำได้!"

---

## 🚨 Failure Modes & Recovery

| ปัญหา | วิธีแก้ตอน demo |
|---|---|
| UNO Q ไม่ boot | ใช้บอร์ดสำรอง / เปิด backup video |
| Wi-Fi ห้องช้า | ใช้ hotspot มือถือ |
| Edge Impulse load ไม่ขึ้น | ใช้ screenshot ที่เตรียมไว้ |
| Inference accuracy ต่ำตอน live | "เห็นไหม โลกจริงต่างจาก training — นี่คือสิ่งที่ทีมต้องเจอ" |
| Modulino Pixels ไม่ติด | ลอง re-seat Qwiic / ใช้ Buzzer แทน |

⚠️ **กฎทอง:** **อย่า panic** — ถ้า demo fail แล้วยังพูดต่อได้เป็นธรรมชาติ จะดูน่าเชื่อถือกว่า demo เริ่ดๆ ที่ดูเหมือน scripted
