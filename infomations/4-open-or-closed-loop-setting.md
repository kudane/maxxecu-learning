* หัวข้อหลัก: Control
* Open loop คือการใช้ base table ในการควบคุม และต้องจูนให้เหมาะสมก่อนใช้งานโหมดอื่น
* Closed loop (single mode) คือการควบคุมรอบเดินเบาอัตโนมัติ โดยใช้ อากาศ หรือ ไฟจุดระเบิด อย่างใดอย่างหนึ่ง
* Closed loop (dual mode) จะใช้ไฟจุดระเบิดควบคุมก่อน แล้วใช้อากาศช่วยเสริมเพื่อให้รอบนิ่งขึ้น
* Test mode คือการส่งค่า duty คงที่เพื่อทดสอบการทำงานของ idle valve หรือ stepper
* หัวข้อหลัก: After Start
* After start duty mode คือวิธีควบคุมลมหลังเครื่องยนต์สตาร์ทติด
* Fixed value คือการใช้ค่า duty คงที่หลังสตาร์ท ส่วน Table คือการใช้ตาราง after-start

```ตัวอย่าง
- Table → แนะนำให้ใช้ และค่าท้ายควรเป็น 0

```

* หัวข้อหลัก: Cranking / Start
* Idle crank duty คือค่า duty คงที่ระหว่างกำลังสตาร์ทเครื่อง
* Idle afterstart hold time คือเวลาค้างค่า crank duty ก่อนเปลี่ยนไปใช้ open loop
* หัวข้อหลัก: Load Compensation
* AC idle up คือการเพิ่มรอบเมื่อแอร์ทำงาน และ Clutch idle up คือการเพิ่มรอบเมื่อเหยียบคลัทช์
* Radiator fan idle up คือการเพิ่ม duty ก่อนพัดลมหม้อน้ำทำงาน เพื่อลดอาการรอบตก
* Close above MAP คือการสั่งปิด idle valve เมื่อค่า MAP สูง

```ตัวอย่าง
- Close above MAP → ปิด idle valve ที่ 0% duty

```

* หัวข้อหลัก: Closed Loop Settings
* Control deadband คือช่วง RPM ที่แกว่งเล็กน้อยแล้วระบบจะไม่ทำการปรับแต่ง
* Disable over RPM, Disable over TPS และ Disable over speed จะปิดระบบ closed loop หรือ idle control เมื่อค่าเกินกำหนด
* Activation delay คือการหน่วงเวลาก่อนที่ระบบ closed loop จะเริ่มทำงาน
* หัวข้อหลัก: Activation Conditions
* Min CLT คืออุณหภูมิน้ำขั้นต่ำ และ Min runtime คือเวลาที่เครื่องต้องทำงานก่อนเปิด closed loop
* หัวข้อหลัก: Ramp Down
* Ramp down time คือเวลาลดรอบลงแบบนุ่มหลังถอนคันเร่ง เพื่อป้องกันรอบตกดับ
* หัวข้อหลัก: PID Control
* P gain คือการตอบสนองต่อ error แบบทันที และ I gain คือการสะสม error เพื่อแก้ค่าค้าง
* D gain ทำหน้าที่ลดการแกว่งหรืออาการ overshoot
* หัวข้อหลัก: Control Range
* Range mode คือวิธีจำกัดช่วงการควบคุม โดยเลือกได้ทั้งแบบ Absolute และ Relative
* Min PID range และ Max PID range คือค่าต่ำสุดและสูงสุดที่ระบบสามารถปรับได้

```ตัวอย่าง
- Absolute → กำหนดช่วง min/max duty แบบตายตัวที่ 0–100%

```

* หัวข้อหลัก: Slow Air Follow (Dual Mode)
* Secondary air PID control คือการเลือกเปิดหรือปิดการใช้ลมช่วยควบคุม
* ในสถานะ Enabled ลมจะช่วยปรับรอบร่วมกับ ignition ส่วน Disabled ลมจะคงที่ ไม่ช่วยควบคุม
* P gain (air) คือการตอบสนองของลม และ I gain (air) คือการสะสมค่าของลม
* หัวข้อหลัก: ข้อแนะนำเพิ่มเติม
* ต้องจูน Open Loop ให้ใกล้เคียงก่อนเสมอ และระบบ Dual mode คือการใช้ไฟควบคุมเร็วบวกกับลมช่วยละเอียด
* ค่า Ramp down มีความสำคัญต่อการป้องกันอาการรอบตกดับ

```แจ้งเตือน
- ตัวเลขรอบที่เพิ่มขึ้นของ AC idle up และ Clutch idle up [ไม่มีในแหล่งที่มา]
- ค่าตัวเลขและหน่วยวัดของตัวแปรในส่วน Closed Loop Settings, Activation Conditions และ PID Control [ไม่มีในแหล่งที่มา]
- คำศัพท์ BTDC และ Feed Forward ปรากฏในเงื่อนไขการสรุปหลักแต่ไม่มีการระบุเนื้อหาขยายความในเอกสารชุดนี้ [ไม่มีในแหล่งที่มา]

```
