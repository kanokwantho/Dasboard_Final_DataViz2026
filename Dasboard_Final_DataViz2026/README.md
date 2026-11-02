# Thailand & Global Digital Risk Dashboard
### Global Context to Local Impact — Interactive HTML Dashboard

ระบบแดชบอร์ดเชิงโต้ตอบสำหรับติดตามและวิเคราะห์ความเสี่ยงดิจิทัล ข่าวบิดเบือน และภัยคุกคามจากปัญญาประดิษฐ์ (AI/Deepfake) พัฒนาขึ้นตามข้อกำหนดทางเทคนิคในเอกสาร **Dashboard Handoff Specification** โดยประมวลผลจากชุดข้อมูลจริงที่เตรียมไว้ใน Jupyter Notebook `Cyber_Threat_AI_Disinformation_Analysis_FINAL.ipynb`

---

## 📸 ภาพตัวอย่างแดชบอร์ด (Screenshots ทั้ง 3 หน้า)

| หน้าที่ | ชื่อหน้า | ภาพตัวอย่าง |
|---|---|---|
| **Page 1** | 🇹🇭 **Thailand Cyber Fraud & Scam Tracker** | ![Page 1](screenshot_page1.png) |
| **Page 2** | 🌍 **Global Disinformation & Narrative Watch** | ![Page 2](screenshot_page2_tall.png) |
| **Page 3** | 🤖 **Emerging AI Risks & Deepfake Incident Watch** | ![Page 3](screenshot_page3_tall.png) |

---

## 🚀 วิธีเปิดใช้งานแดชบอร์ด (How to Run)

แดชบอร์ดถูกออกแบบให้เป็น **Standalone Interactive HTML** ที่มีความยืดหยุ่นสูง สามารถเปิดใช้งานได้ 2 รูปแบบ:

### วิธีที่ 1: ดับเบิ้ลคลิกเปิดไฟล์ `index.html` โดยตรง (Zero-Setup)
- สามารถดับเบิ้ลคลิกไฟล์ `index.html` ในโฟลเดอร์เพื่อเปิดบน Web Browser (Chrome, Edge, Safari, Firefox) ได้ทันที
- ระบบมีสคริปต์ `data/bundled_data.js` ที่ฝังข้อมูลจริงที่ประมวลผลแล้วไว้ ทำให้สามารถแสดงผลกราฟและ KPI ได้ทันที แม้ไม่มี Web Server และไม่ติดข้อจำกัด CORS ของ Browser

### วิธีที่ 2: รันผ่าน Local HTTP Server (แนะนำสำหรับการทดสอบการ Fetch ข้อมูลสด)
เปิด Terminal หรือ PowerShell ในโฟลเดอร์นี้ แล้วรันคำสั่ง:
```bash
# ด้วย Python
python -m http.server 8000

# หรือด้วย Node.js
npx serve
```
จากนั้นเปิด Browser ไปที่ `http://localhost:8000`

---

## 📂 โครงสร้างไฟล์ในโครงการ (Project Structure)

```text
Dasboard_Final_DataViz2026/
├── index.html                           # ไฟล์แดชบอร์ดหลัก (HTML5 + CSS3 + Vanilla JS)
├── README.md                            # คู่มือการใช้งานและเอกสารกำกับความถูกต้อง
├── screenshot_page1.png                 # ภาพบันทึกหน้าจอ Page 1
├── screenshot_page2_tall.png            # ภาพบันทึกหน้าจอ Page 2
├── screenshot_page3_tall.png            # ภาพบันทึกหน้าจอ Page 3
└── data/                                # โฟลเดอร์ชุดข้อมูลจริง
    ├── weekly_panel.csv                 # ข้อมูลรายสัปดาห์คดีออนไลน์และข่าวปลอมไทย (409 แถว)
    ├── thai_dashboard_master.csv        # ข้อมูลสรุปรายสัปดาห์ที่ทำความสะอาด Outlier แล้ว
    ├── acsc_weekly.csv                  # สถิติคดีศูนย์ปราบปรามอาชญากรรมทางเทคโนโลยี (ACSC)
    ├── data_dictionary.csv              # คำอธิบายคอลัมน์ของข้อมูลชุดไทย
    ├── euvsdisinfo_base.csv             # ฐานข้อมูลตรวจสอบข่าวบิดเบือนสหภาพยุโรป (ดิบ)
    ├── euvsdisinfo_disinformation.csv   # กรองเฉพาะ class == disinformation (10,682 แถว)
    ├── AIID_Excel_Export-20261026.xlsx  # ฐานข้อมูลเหตุการณ์ AI ต้นฉบับจาก AIID
    ├── ai_incidents.csv                 # เหตุการณ์ AI ที่สกัดจาก Sheet 'Incidents' (1,775 แถว)
    ├── ai_yearly_eda.csv                # สรุปรายปีเหตุการณ์ AI และ Deepfake Keyword Proxy
    ├── ai_risk_summary.csv              # เมทริกซ์แจกแจงรายปี x 8 Risk Domains
    ├── bundled_data.json                # ข้อมูล JSON รวมสำหรับส่งต่อ API
    └── bundled_data.js                  # สคริปต์โหลดข้อมูลทันทีเพื่อรองรับการเปิดแบบ file://
```

---

## 📊 รายละเอียดฟังก์ชันทั้ง 3 หน้า

### 🇹🇭 Page 1: Thailand Online Cyber Fraud & Scam Tracker
เน้นเชื่อมโยงความเสียหายจากคดีออนไลน์ (ACSC) กับแนวโน้มข่าวปลอม (AFNC)
1. **KPI Cards (สัปดาห์ล่าสุดที่มีข้อมูลจริง: 18–24 ต.ค. 2026)**
   - **Total Financial Damage:** ฿333.00 ล้านบาท (333,000,000 บาท)
   - **Online Reported Cases:** 6,220 คดี (เฉลี่ย 53,537 บาท/คดี) จาก `acsc_cases_cleaned`
   - **Fake + Distorted Share:** 68.0% (ข่าวเท็จ 23 เรื่อง, ข่าวบิดเบือน 11 เรื่อง จาก 50 เรื่องที่ตรวจสอบ)
2. **Weekly Dual-Axis Chart:**
   - แกนซ้าย (Bar): มูลค่าความเสียหายรายสัปดาห์ (หน่วยล้านบาท)
   - แกนขวา (Line): จำนวนข่าวเท็จหมวดการเงิน (`afnc_false_finance`)
   - จุดข้อมูลเรียงตาม `week_start` จากอดีตถึงปัจจุบัน สัปดาห์ที่ไม่รายงานหรือติด Suspect จะเว้นวรรค (ไม่เติม 0)
3. **Monthly Fake News by Category (Stacked Bar):**
   - รวมยอดรายเดือนของข่าวปลอมหมวดสุขภาพ, การเงิน และนโยบายรัฐ
   - มีปุ่มสลับมุมมองระหว่าง **[จำนวนเรื่อง]** และ **[สัดส่วน 100%]**
   - มีข้อความกำกับชัดเจนว่าเกิดจากการรวมผลรวมรายสัปดาห์ ไม่ใช่ข่าวรายเดือนดิบ
4. **Data Quality Alert Panel:**
   - แจ้งเตือนสัปดาห์ 16–22 ส.ค. 2026 ที่ติด flag `Suspect` (คดี 79,311 คดี / ความเสียหาย 2,775 ล้านบาท สูงผิดปกติ 13 เท่า) ซึ่งถูกแยกออกจากตัวแปร `*_cleaned`
   - แจ้งเตือนสัปดาห์ 30 พ.ค. – 6 มิ.ย. 2026 ที่มีระยะเวลาคาบเกี่ยว 8 วัน (overlapping period)
   - ชี้แจงช่วงก่อน พ.ย. 2025 ที่ยังไม่มีการแถลงข่าวของ ACSC

---

### 🌍 Page 2: Global Disinformation & Narrative Watch
ติดตามความเคลื่อนไหวของข่าวบิดเบือนระดับโลกจากฐานข้อมูล EUvsDisinfo (กรอง `class == "disinformation"`)
1. **KPI Cards:**
   - **Disinformation Debunks:** 6,182 กรณีตรวจสอบไม่ซ้ำ (`debunk_id`) จากทั้งหมด 10,682 บทความ
   - **Debunked Domains:** 1,315 โดเมนแหล่งที่มาที่ไม่ซ้ำ
2. **Top 15 Keywords in Disinformation (Horizontal Bar):**
   - จัดอันดับคำสำคัญยอดนิยม เช่น `war in ukraine` (1,949), `anti-russian` (1,423), `west` (1,376), `conspiracy theory` (1,277), `nato` (1,092), `crimea` (1,038) ฯลฯ
3. **Article Language Distribution (Donut Chart):**
   - แสดงสัดส่วนภาษาของบทความ: Russian (50.1%), Arabic (32.2%), English (4.0%), Spanish (2.3%), German (2.0%), French (1.5%), อื่น ๆ (7.9%)
4. **Top Debunked Domains Table:**
   - ตารางแสดงอันดับโดเมนที่ปรากฏบ่อยที่สุด: `arabic.rt.com`, `ria.ru`, `ru.armeniasputnik.am`, `sputnik.by`, `russian.rt.com` ฯลฯ
   - รองรับช่องค้นหาโดเมน, จัดเรียงลำดับ และการแบ่งหน้า (Pagination 10 รายการต่อหน้า)
   - แสดงถ้อยคำกำกับตามหลักวิชาการ: *"โดเมน/แหล่งที่ปรากฏในรายการบทความที่ EUvsDisinfo จัดเป็น disinformation ไม่ใช่การตัดสินโดยพลการ"*

---

### 🤖 Page 3: Emerging AI Risks & Deepfake Incident Watch
วิเคราะห์แนวโน้มอุบัติการณ์ความเสี่ยงจาก AI และ Deepfake จากฐานข้อมูล AI Incident Database (AIID)
1. **Disclaimer Banner (คำเตือนด้านระเบียบวิธีวิจัย):**
   - แจ้งเตือนอย่างเด่นชัดว่าตัวชี้วัด Deepfake คำนวณจากกฎการตรวจจับคำสำคัญ (Keyword Regex: `deepfake|synthetic media|voice clone|face swap`) ไม่ใช่การพิสูจน์ยืนยันทางนิติวิทยาศาสตร์
2. **KPI Cards:**
   - **Total AI Incidents:** 1,775 เหตุการณ์สะสม (2015 – ต.ค. 2026)
   - **Deepfake Keyword Share:** 31.8% (565 เหตุการณ์ที่ตรวจพบคำสำคัญ Deepfake/Synthetic)
   - **2026 YTD Incidents:** 288 เหตุการณ์ (ตัดยอด 26 ต.ค. 2026 เป็นข้อมูลไม่ครบปี)
3. **AI Incidents by Year and Risk Domain (Stacked Column Chart):**
   - แสดงการกระจายตัวของเหตุการณ์ AI ในแต่ละปีตาม 8 Risk Domains จริง:
     - `Malicious Actors & Misuse` (พุ่งสูงชัดเจนในปี 2024–2025)
     - `AI system safety, failures, and limitations`
     - `Discrimination and Toxicity`
     - `Misinformation`
     - `Privacy & Security`
     - `Human-Computer Interaction`
     - `Socioeconomic & Environmental Harms`
     - `Uncategorized`
   - คลิกเปิด/ปิด Series ใน Legend ได้อิสระ
4. **Impact by Sector of Deployment (Horizontal Bar Chart):**
   - แสดงการกระจายตัวตามภาคส่วนที่มีการระบุข้อมูลจริง เช่น `information and communication`, `Arts, entertainment and recreation`, `transportation and storage` ฯลฯ
   - มีปุ่มสลับมุมมอง **[All AI Incidents]** เทียบกับ **[Deepfake Keyword Only]**
5. **Latest AI Incident Feed & Modal:**
   - แสดงการ์ดเหตุการณ์ AI ล่าสุด เรียงจากใหม่ไปเก่า
   - มีแถบค้นหาเหตุการณ์แบบ Real-time ตามชื่อ, ระบบ, ผู้พัฒนา, และผู้ติดตั้งใช้งาน
   - ปุ่ม **View Details** สำหรับเปิดหน้าต่าง Modal เพื่ออ่านรายละเอียดเหตุการณ์ฉบับเต็ม

---

## 🛡️ การตรวจสอบ Schema และการอัปโหลดไฟล์ (Data Upload & Schema Report)

ผู้ใช้งานสามารถกดปุ่ม **Upload Data** บนแถบ Header เพื่อนำเข้าไฟล์ข้อมูลของตนเอง:
- รองรับไฟล์ทั้งนามสกุล `.csv` (ผ่าน Papa Parse) และ `.xlsx` (ผ่าน SheetJS)
- **ระบบ Auto-Detection:** ตรวจสอบโครงสร้าง Headers อัตโนมัติ:
  - หากพบ `week_start` หรือ `acsc_cases` -> จัดเข้า **Page 1 (Thailand)**
  - หากพบ `debunk_id` หรือ `class` -> จัดเข้า **Page 2 (EUvsDisinfo)**
  - หากพบ `Incident ID` หรือ Sheet `Incidents` -> จัดเข้า **Page 3 (AIID)**
- **Schema Checklist:** แสดงรายการคอลัมน์ที่ตรวจพบ พร้อมเครื่องหมายถูกสีเขียว (✓) หรือแจ้งเตือนสีแดง (✗) และจำนวนแถวที่ประมวลผลได้
- ปุ่ม **"นำข้อมูลเข้าสู่แดชบอร์ด"** จะปรับปรุงกราฟและ KPI ทุกตัวบนหน้าเว็บแบบ Reactive ทันที

---

## 🔍 สรุปการตรวจสอบ Field จริง และข้อจำกัดที่พบ (Schema Findings & Data Limitations)

ตามข้อกำหนดใน Section 6 และ Section 10 ของเอกสาร Handoff ทางผู้พัฒนาได้สรุปสถานะของ Fields จริงดังนี้:

| ชุดข้อมูล | Field ที่ตรวจพบและใช้งานจริง | Field ที่ไม่พบ / มีข้อจำกัด | แนวทางการจัดการตามหลัก Data Integrity |
|---|---|---|---|
| **Thai Weekly Panel** | `week_start`, `week_end`, `afnc_*`, `acsc_reported`, `acsc_cases`, `acsc_loss_baht`, `acsc_flag` | ข้อมูล ACSC มีรายงานเฉพาะ พ.ย. 2025 – ต.ค. 2026 | **ไม่เติม 0 ในสัปดาห์ที่ไม่มีรายงาน** เพื่อป้องกันไม่ให้ค่าเฉลี่ยความเสียหายต่อคดีผิดเพี้ยน |
| **Thai Weekly Panel** | `acsc_flag` สัปดาห์ 16–22 ส.ค. 2026 ระบุ `Suspect` | ไม่มีข้อมูลประเภทคดีรายระเบียน | แยกสัปดาห์ Suspect ออกจาก `*_cleaned` และแสดงข้อความเตือนใน Alert Panel |
| **EUvsDisinfo** | `debunk_id`, `article_id`, `article_language`, `article_domain`, `debunk_date`, `class`, `keywords` | บางระเบียนไม่มีการระบุภาษา | เติมภาษาที่ขาดเป็น `Unspecified` เพื่อคงจำนวนรวมของบทความไว้ครบถ้วน |
| **EUvsDisinfo** | กรอง `class == "disinformation"` | โดเมนเป็น Hostname ไม่ใช่ URL เต็ม | นับโดเมนระดับ Hostname และระบุถ้อยคำว่าเป็นแหล่งที่ปรากฏในฐานข้อมูล |
| **AIID** | `Incident ID`, `date`, `year`, `title`, `description`, `developer`, `deployer`, `Risk Domain`, `Implicated Systems` | `Sector of Deployment` มีการระบุเพียงส่วนน้อย (558 ระเบียนเป็นค่าว่าง/Unspecified) | **ห้ามสร้างข้อมูล Sector ขึ้นเอง** แสดงเฉพาะหมวดที่มีการระบุจริง และใส่หมายเหตุกำกับสัดส่วน Unspecified |

---

## 🛠️ เทคโนโลยีที่ใช้ (Tech Stack)

- **Frontend:** Vanilla HTML5, CSS3 (Modern Flexbox/Grid, Glassmorphism, CSS Custom Properties)
- **Charts:** Chart.js v4.4.1 (Dual-Axis Mixed Bar/Line, Stacked Column, Donut, Horizontal Bar)
- **Parsers:** Papa Parse v5.4.1 (CSV streaming parser), SheetJS xlsx v0.18.5 (Excel binary parser)
- **Typography:** Google Fonts: `Prompt` (ภาษาไทย/อังกฤษ) และ `Inter` (ตัวเลขสถิติและรหัส)
- **Zero-Dependency Icons:** Inline SVG (คมชัดทุกความละเอียดและทำงานได้แม้ออฟไลน์)
