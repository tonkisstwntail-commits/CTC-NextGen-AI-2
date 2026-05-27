<!-- workshop-header -->
<img width="1347" height="127" alt="Coding Thailand 2026 header" src="https://github.com/user-attachments/assets/ba5cf267-f460-4fb0-b69b-c461ae061a3b" />

# 🚀 GitHub Setup Guide

> คู่มือนี้ใช้อ้างอิง flow ปัจจุบันของ repo นี้: เก็บ team template ไว้ในโฟลเดอร์ `templates/team-repo-template/`

---

## Step 1: สร้าง Repo บน GitHub

### Option A: สร้างใหม่จาก scratch

1. ไป https://github.com/new
2. **Repository name:** `coding-thailand-edge-ai-workshop`
3. **Description:** "Day 1 materials — Coding Thailand 2026 Edge AI Workshop"
4. **Public** ✓
5. **Initialize:** ☐ ไม่ต้องติ๊ก (เราจะ push เอง)
6. กด **Create repository**

### Option B: ใช้ repo ที่มีอยู่แล้วเป็นฐาน

ถ้ามี workshop repo อยู่แล้ว ให้ push เพิ่มเติมจากเครื่องที่ใช้อยู่เข้า repo เดิมได้เลย

---

## Step 2: Push Repo จากเครื่องที่ใช้อยู่

```bash
# เข้า folder
cd coding-thailand-edge-ai-workshop

# Init git
git init
git add .
git commit -m "init: Edge AI Workshop Day 1 materials"

# เชื่อม remote
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/coding-thailand-edge-ai-workshop.git

# Push
git push -u origin main
```

---

## Step 3: เลือกวิธีแจก Team Template

### วิธีที่ใช้ได้ทันทีใน repo นี้

ให้นักเรียนสร้าง repo ใหม่ของทีม แล้วคัดลอกไฟล์จาก `templates/team-repo-template/` ไปใส่ repo ของตัวเอง

ข้อดี:
- ใช้ได้ทันที ไม่ต้องแยก repo ใหม่
- โครงสร้างทีมอยู่ใน repo เดียวกับ workshop materials

### ถ้าอยากได้ปุ่ม "Use this template" จริง

แยก `templates/team-repo-template/` ออกเป็น repo ใหม่ แล้วค่อยตั้ง repo นั้นเป็น GitHub template repository:

1. สร้าง repo ใหม่สำหรับ template ทีมโดยเฉพาะ
2. copy ไฟล์จาก `templates/team-repo-template/` ไปใส่
3. ใน GitHub → repo นั้น → **Settings**
4. หน้า General → ติ๊ก ☑ **Template repository**
5. Save

วิธีนี้เหมาะถ้าจะใช้ workshop นี้หลายรอบและอยากให้ onboarding เร็วขึ้น

---

## Step 4: ตั้ง Branch Protection (Optional)

ป้องกัน main branch ถูกแก้ตรงๆ:

1. Settings → Branches → Add rule
2. Branch name: `main`
3. ☑ Require pull request before merging
4. ☑ Require approvals: 1
5. Save

> ⚠️ สำหรับ workshop ไม่บังคับ — แต่ดีถ้าอยากสอน PR workflow เต็มรูปแบบ

---

## Step 5: เปิด GitHub Discussions (แนะนำ)

ให้นักเรียนถาม-ตอบกันได้:

1. Settings → General → Features
2. ☑ Discussions
3. Save

---

## Step 6: เตรียม URL ให้ทีม

ก่อนวัน workshop ส่งให้นักเรียนรู้ล่วงหน้า:

```
🔗 Workshop Repo:
https://github.com/YOUR_USERNAME/coding-thailand-edge-ai-workshop

📋 Team Repo Template:
ใน workshop ทีมจะเปิดโฟลเดอร์ templates/team-repo-template/
แล้วสร้าง repo ของตัวเองชื่อ edge-ai-team-XX (เช่น edge-ai-team-01)
```

---

## Step 7: Sample Team Repo (Optional แต่แนะนำ)

สร้าง demo team repo เป็นตัวอย่าง:

```bash
# สร้าง repo ว่างก่อน
gh repo create demo-team --public --clone

# จากนั้น copy ไฟล์ใน templates/team-repo-template ไปใส่ demo-team
```

แล้วทำ:
- Commit ตัวอย่าง 3-5 ครั้ง (แสดง commit message format ที่ดี)
- กรอก Worksheet W1-W4 ตัวอย่าง
- ใส่ผลลัพธ์สมมุติ V1 vs V2

→ นักเรียนเห็นเป็น reference ได้ทันที

---

## Step 8: Pre-Workshop Checklist

ก่อนถึงวัน Workshop:

- [ ] Repo ขึ้น GitHub แล้ว
- [ ] ตกลงแล้วว่าจะใช้ subfolder template หรือ template repo แยก
- [ ] Discussions เปิด ☑
- [ ] URL ส่งให้ทีมแล้ว
- [ ] Demo team repo มีตัวอย่าง
- [ ] ทุก TA clone repo ลงเครื่อง
- [ ] ทดสอบ flow: เปิด team-repo-template → สร้าง repo ทีมใหม่ → push commit แรกได้

---

## ⚙️ Optional: GitHub Classroom

ถ้าสะดวกใช้ GitHub Classroom (เหมาะกับ workshop ใหญ่ >20 ทีม):

1. ไป https://classroom.github.com
2. Create organization → Create classroom
3. Create assignment → ใช้ repo template
4. ได้ลิงก์ assignment สำหรับนักเรียน
5. นักเรียนกดลิงก์ → ระบบสร้าง repo ของแต่ละทีมอัตโนมัติ

**ข้อดี:** จัดการได้ดี + เห็น progress ของทุกทีมในที่เดียว
**ข้อเสีย:** ต้องตั้ง org ก่อน + นักเรียนต้องอยู่ใน account ที่ join classroom

---

## 📋 Workshop Day Flow (GitHub-focused)

### 09:30-09:45 — Setup ทีม

ลำดับที่ควรพาทีมทำ:

- ไปที่ URL workshop repo
- เปิดโฟลเดอร์ `templates/team-repo-template`
- สร้าง repo ใหม่ชื่อ `edge-ai-team-XX` แบบ public
- คัดลอกไฟล์ template ไปใส่ repo ทีม
- Clone ลง laptop ตามคำสั่งใน `docs/04-git-basics.md`

### ตลอดวัน — Cadence ของ Commit

แนะนำให้ครูตั้ง "Commit Time" ทุก ~30 นาที:
- 11:00 — Commit Worksheet W1
- 11:30 — Commit Data Collection log
- 13:30 — Commit V1 results
- 14:30 — Commit Prediction Log
- 15:30 — Commit V2 + comparison

### 16:30 — Final push
ทุกทีมต้อง final push ก่อนเลิก พร้อม tag `day1-final`:
```bash
git tag day1-final
git push origin day1-final
```

---

## 🎯 Tips จาก Workshop ก่อนๆ

1. **Username convention:** บอกนักเรียนตั้งชื่อ team-repo ให้ match กับ team number เพื่อง่ายต่อการ grade
2. **TA Watch List:** ให้ TA แต่ละคน Watch repo ของทีมที่ดูแล จะได้รู้เมื่อมี commit ใหม่
3. **Grading Day:** ใช้ `git log` + `gh pr list` + เปิด repo ดู → ใช้ Rubric ที่อยู่ใน `docs/03-rubric.md`
4. **Public vs Private:** Public ดีกว่า เพราะทีมเห็นของกันและกัน → เป็นแรงผลักดัน

---

## 🆘 ปัญหาที่อาจเจอ

### นักเรียนไม่มี GitHub account
→ เตรียม instruction sign up ล่วงหน้า + เผื่อ 15 นาทีใน schedule

### Push ไม่ขึ้น (HTTPS)
→ GitHub ตอนนี้ต้องใช้ Personal Access Token แทน password
→ แนะนำให้ใช้ GitHub CLI: `gh auth login`

### นักเรียนเผลอ commit dataset ใหญ่
→ มี .gitignore ใน team template แล้ว แต่ย้ำตอน Git 101

### ทีม merge conflict
→ มีใน troubleshooting guide แล้ว

---

## 📚 References

- [GitHub Docs - Template Repos](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository)
- [GitHub Classroom](https://classroom.github.com)
- [GitHub CLI](https://cli.github.com/)
