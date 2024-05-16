# # Day4 - **Query Optimization - พัฒนา SQL ที่เขียนให้มีประสิทธิภาพที่ดีขึ้น | EP.3 SQL Series 1.1**

- ใช้ Preview ก่อนที่จะ SELECT * FROM 
- เวลาเรา Query จะมีการทำงานไม่เหมือนกัน → Postgres (C) or BigQuery
- Postgres ที่เป็น RDBMS ซึ่งเบื้องหลังเขียนด้วยซีก็จะทำงานคนละแบบเวลาที่เรา Select
- BigQuery ของข้างในจะเป็น Data model อยู่ที่ว่าเราจะ design มันออกมาเป็นยังไง → Star schema , snowflake or design ในระดับ type ของคอลัมน์ เช่น int fast more than str
- Query ที่ดี (อ่านรู้เรื่อง) กับ Query ที่ performance ดีอาจจะต่างกัน
- In BigQuery Bad Practice ที่ไม่ควรทำ

```sql
SELECT * FROM `table`
SELECT * FROM `table` LIMIT 1
```

```sql
SELECT
	* EXCEPT(customer_id, agent_code, order_description)
FROM `orders`
```
- สามารถใช้ EXCEPT เพื่อบอกว่าเราไม่อยากได้คอลัมน์อะไรบ้าง อย่าใช้ LIMIT 1 เพราะไม่ช่วยในการลด processing time และขนาด แค่ช่วยในเรื่องการนำมาแสดง
- view table ทุกครั้งที่รันจะไปรัน query เพื่อหยิบของจาก table อื่นอีกที
- กรณีที่อยากใช้ view ก็คือกรณีที่เราไม่ต้องการดู data บ่อยๆเพราะต้อง query เอาเท่านั้น
- หรือ data มีการอัพเดทบ่อยๆ แล้วเราไม่อยากเก็บ data ให้ซ้ำซ้อนสองที่
- ในกรณีที่ data น้อยๆ การใช้ String จะไม่มีผลเยอะ แต่จะเยอะในกรณีขนาด GB แนะนำให้ใช้ INT64
