* หัวข้อหลัก: หลักการพื้นฐาน: Coarse vs Fine
* Air Flow คือการปรับหยาบ (Coarse) และ Spark Timing คือการปรับละเอียด (Fine)
* ทั้งสองส่วนรวมกันสร้าง Engine Torque ที่ Idle เพื่อกำหนด Idle RPM
* หัวข้อหลัก: ส่วนที่ 1 — Mechanical Idle (ต้องทำก่อนเสมอ)
* ต้องเริ่มจาก Mechanical Idle ก่อนเสมอ หาก Air Flow ไม่นิ่งจะไม่สามารถ tune idle ได้
* ทำโดยถอดสาย Solenoid หรือไม่ตั้งค่า output แล้วหมุน Throttle Stop Screw บนเครื่องอุ่นให้ได้รอบตามกำหนด
* การมี Reserve ช่วยให้ Spark Timing เพิ่ม timing ดึง RPM กลับมาได้เร็วเมื่อ Idle ดิ่งลง
* ต้องทำการ Reset TPS ที่เมนู Inputs → Sensors → Get Current Value เพื่อจำค่า voltage ของ Closed Throttle

```ตัวอย่าง
- Target 950 RPM → ตั้ง Throttle ให้เครื่องวิ่งที่ 1100-1150 RPM บนเครื่องอุ่น

```

* หัวข้อหลัก: ส่วนที่ 2 — Spark Timing Feedback (Idle RPM Error Table)
* ตั้งค่าที่ Ignition → Ignition Lock → Idle Control และเปลี่ยน Ignition Angle Mode เป็น Table
* ตาราง Idle RPM Error จะลด timing เมื่อ error เป็นลบ และเพิ่ม timing เมื่อ error เป็นบวก
* ตาราง Target Idle RPM กำหนดตาม Coolant Temperature และสามารถเพิ่มแกนแก้อุณหภูมิเป็น Table 3D ได้

```ตัวอย่าง
- error = 0 → RPM กำลัง hit target พอดี
- เครื่องเย็น 32°C → ต้องการ 1300 RPM
- เครื่องอุ่น 85°C+ → ต้องการ 950 RPM

```

* หัวข้อหลัก: ส่วนที่ 3 — PWM Solenoid Setup
* กำหนดค่าที่ Outputs → Output Config เป็น Idle PWM Solenoid หรือ Inverted ถ้าสัญญาณกลับด้าน
* Solenoid แบบ Low Side ใช้ GPO ทั่วไปคุมฝั่งกราวด์ ส่วน High Side ใช้ GPO ชนิดพิเศษคุมฝั่ง 12V
* ความถี่ใช้งานควรตั้งที่ 200-300 Hz หากไม่ทราบให้เริ่มต้นตั้งที่ 250 Hz
* หากสตาร์ทเครื่องเย็นแล้ว Duty Cycle = 0 แล้ว RPM พุ่งสูงมาก แสดงว่าต้องตั้งค่าแบบ Inverted

```ตัวอย่าง
- ตั้งความถี่ที่ 200-300 Hz หรือเริ่มที่ 250 Hz

```

* หัวข้อหลัก: ส่วนที่ 4 — Open Loop Duty Cycle Tables
* ค่า 0% คือ Solenoid ปิด ไม่มี Air flow และค่า 100% คือเปิดสุด มี Air flow สูงสุด
* บนเครื่องอุ่นต้องตั้งค่าเป็น 0 เสมอ ส่วนเครื่องเย็นเริ่มจาก 35-40% แล้วค่อยๆ taper ลงตามอุณหภูมิ
* Idle Crank Duty ช่วยเพิ่ม Air flow ช่วงกดสตาร์ทให้เครื่องยนต์ติดง่ายขึ้น
* Afterstart Duty Table ทำงานอิงตาม Engine Runtime หลังรอบเครื่องยนต์เกิน Max Crank RPM โดยคอลัมน์สุดท้ายต้องเป็น 0 เสมอ

```ตัวอย่าง
- เครื่องอุ่น → ตั้งเป็น 0 เสมอ
- เครื่องเย็น → เริ่มจาก 35-40%
- Idle Crank Duty → ตั้งค่า 80-90%
- Afterstart Duty Table → ให้ค่าสูงช่วง 0-5 วินาทีแรก และ taper ลงเป็น 0 ภายใน 20 วินาที

```

* หัวข้อหลัก: ส่วนที่ 5 — Compensation & Idle Up
* AC Idle Up ช่วยบวก Duty Cycle เพิ่มเพื่อชดเชย Torque loss จาก Compressor และตั้ง RPM Offset ได้
* Clutch Idle Up ช่วยพยุงรอบไม่ให้ร่วงฮวบเมื่อเหยียบคลัทช์ เหมาะกับ Twin/Triple Disc Clutch ที่มี Flywheel เบา
* Radiator Fan Idle Up ช่วยชดเชยแรงบิดเมื่อพัดลมไฟฟ้าทำงานและดึง Load จาก Alternator มาก
* Close Above MAP ตั้งให้ Solenoid ปิดเมื่อแรงดันเกินค่าที่กำหนดเพื่อป้องกันอาการ Boost Leak

```ตัวอย่าง
- AC Idle Up → เพิ่ม Target เป็น 1050 RPM แทน 950 RPM
- Close Above MAP → เมื่อ MAP เกิน 0 psi (100 kPa)

```

* หัวข้อหลัก: สรุปหลักการสำคัญ
* ลำดับขั้นตอนคือ Mechanical Idle ก่อน → Spark Feedback → เสียบ Solenoid → ตั้ง Cold Start Tables
* เมื่ออยู่ในสภาวะ Warm engine ระบบอากาศต้องได้ค่า 0% Duty Cycle เสมอ

```แจ้งเตือน
- ระบบหรือวิธีการคำนวณของ PID [ไม่มีในแหล่งที่มา]
- รายละเอียดและชื่อเรียกของ GPO ชนิดพิเศษสำหรับระบบ High Side [ไม่มีในแหล่งที่มา]

```
