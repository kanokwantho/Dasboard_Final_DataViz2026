# Thailand & Global Digital Risk Dashboard

## วิธีเปิดใช้งาน
1. ดาวน์โหลด `index.html` แล้วเปิดด้วย Chrome, Edge หรือ Firefox รุ่นปัจจุบัน
2. Dashboard ฝังข้อมูลจาก `processed.zip` ไว้ใน HTML แล้ว จึงไม่จำเป็นต้องแตก ZIP หรือเชื่อมต่อ backend
3. ใช้เมนูด้านซ้ายเพื่อเปลี่ยน 3 หน้า: Thailand Cyber Fraud, Global Disinformation และ AI Risks & Deepfake
4. ใช้ตัวกรองในแต่ละหน้าเพื่อเปลี่ยนช่วงเวลา/หมวด แล้วกด Export เพื่อดาวน์โหลดข้อมูลที่กรองแล้ว
5. ปุ่ม Upload CSV / JSON รองรับการแทนที่ไฟล์สรุปเดิม โดยใช้ชื่อไฟล์ตามที่ export จาก Notebook เช่น `thai_dashboard_master.csv`, `eu_monthly.csv`, `ai_yearly.csv`

## ข้อมูลที่ฝังอยู่
ข้อมูลใน HTML มาจาก `processed.zip` ที่ผู้ใช้แนบมา ณ วันที่ใน `dashboard_metadata.json` มีไฟล์ CSV/JSON ที่ใช้สร้าง KPI, charts, tables และ data-quality notes

## ข้อจำกัดที่แสดงใน Dashboard
- EUvsDisinfo: monthly article/debunk aggregates สิ้นสุดช่วงข้อมูลปี 2023; โดเมนและ publisher ที่แสดงเป็น Top 10 เท่านั้น ไม่ใช่จำนวนโดเมนทั้งหมด
- Thailand: ACSC มีข้อมูลเฉพาะสัปดาห์ที่มีการรายงาน; missing ไม่ถูกเติมเป็นศูนย์; สัปดาห์ Suspect และช่วงทับซ้อนถูกตัดออกจาก cleaned analysis
- AIID: ปี 2026 เป็นข้อมูลบางส่วน; deepfake/synthetic เป็น keyword-based candidates ไม่ใช่การยืนยันโดยผู้เชี่ยวชาญ
- AI Sector: ไม่มีตาราง Sector summary ใน processed.zip จึงแสดงเป็น empty state ไม่สร้างค่าขึ้นเอง
- AI incident feed: ตาราง feed ใช้ review sample 30 แถว ไม่ใช่ Incident Database ทั้งหมด
- Freedom on the Net มีอยู่ใน ZIP แต่ยังไม่อยู่ในขอบเขต 3 หน้าหลัก

## หมายเหตุด้านเทคนิค
- เป็นไฟล์ HTML เดียว ใช้ HTML/CSS/JavaScript และ SVG สำหรับกราฟ ไม่ต้องติดตั้ง Python หรือมี backend
- สามารถแก้ไข source ได้โดยเปิด `index.html` ด้วย code editor
- Upload ใช้ CSV/JSON รายไฟล์; การแทนที่ ZIP โดยตรงยังไม่รองรับ
