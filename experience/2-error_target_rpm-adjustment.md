หลักการปรับ target rpm error 

กรณี closed loop สามารถทำได้ดังนี้

1) ใช้ ign ช่วย โดยการปรับค่า P/D Gain(Dual Mode) ให้สังเกตว่า target rpm error อยู่ที่เท่าไหร่แล้วให้ใส่ค่า P Pain ไปครึ่งหนึ่ง ดูต่อว่า target rpm error เปลี่ยนแปลงหรือไม่ ถ้าไม่เปลี่ยนเข้าใกล้ rpm target ให้ใส่ D Gain ให้เท่ากับ target rpm error หรือน้อยกว่านิดหน่อย จากนั้นทำซ้ำจนไม่มีความต่างแล้ว

2) เมื่อทำข้อ 1 แล้ว target rpm error ยังไม่ดีให้ ให้ปรับใช้ slow air flow โดยให้สังเกตเพียงแค่ว่า ถ้า target rpm error เกินให้เพิ่ม I Gain ที่ละนิด มันจะต้องลดลง ถ้าไม่ลดลงให้เพิ่ม P Gain เพื่อเพิ่มระยะเปิดปิด จากนั้นสังเกตทำซ้ำจนไม่เปลี่ยนแปลง

สรุป

closed loop P/I/D
- P Gain ใส่ค่าครึ่งหนึ่งของ target rpm error หรือ 1/4 ค่อยๆ ขยับ (เพราะมันช่วยเพิ่มหรือลดตามค่า target rpm error ถ้าใส่ P เท่ากับ target rpm error มันจะขยับทันทีเกิน target rpm error ทำให้ไฟวิ่งไล่รอบมากเกินไป)
- D Gain ใส่ค่าเท่ากับ target rpm error หรือ น้อยกว่านิดหน่อย (D มากเกินไปรอบ target rpm error จะค้างไม่วิ่งลดลงมาที่ target rpm ไปขัดขวาง P Gain ให้ทำงานช้า)

slow air flow
- P Gain ใส่ค่าเท่ากับ target rpm error หรือ น้อยกว่านิดหน่อย
- I Gain ใส่ค่าครึ่งหนึ่งของ target rpm error หรือ 1/4 ค่อยๆ ขยับ  (เพราะมันช่วยเพิ่มหรือลดตามค่า target rpm error ถ้าใส่ I เท่ากับ target rpm error มันจะขยับทันทีเกิน target rpm error ไปทำให้ไม่สมูทนั้นเอง)
