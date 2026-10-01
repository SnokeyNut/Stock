# รวมร้าน · ระบบสต๊อก

เว็บ Phase 1 สำหรับหลายร้าน/หลายสาขา ใช้ GitHub Pages สำหรับหน้าเว็บ และ Supabase PostgreSQL + Auth สำหรับข้อมูลจริง

## ใช้งาน

https://SnokeyNut.github.io/Stock/

1. เข้าสู่ระบบ → สร้างบัญชี → ยืนยันอีเมล
2. สร้างองค์กร เพิ่มร้าน สาขา ผู้ขาย ประเภท และสินค้า
3. เลือกสาขา แล้วรับสินค้า เบิกสินค้า นับสต๊อก และสร้างใบสั่งซื้อ
4. ผู้ขาย → ดูรายการสั่งซื้อวันนี้ → คัดลอกข้อความ ปรับ Template ได้ในจัดการข้อมูล

ข้อมูลของแต่ละองค์กรแยกด้วย RLS และตรวจ membership ที่ backend ไม่มี service-role key ในเว็บไซต์

## ไฟล์ใน repository

- `index.html` — เว็บที่ build แล้ว รวม React, CSS และ favicon พร้อมเปิดบน GitHub Pages โดยไม่ต้องเชื่อมบริการ hosting ภายนอก
- `ruamran-stock-source.zip` — codebase TypeScript/React ต้นฉบับ พร้อม lockfile, database types, migrations และ tests ดาวน์โหลดแตกไฟล์เพื่อพัฒนาต่อ
- `.nojekyll` — ให้ GitHub Pages เสิร์ฟไฟล์โดยตรง

## พัฒนาต่อ

แตก source archive แล้วเปิดโฟลเดอร์ `inventory-app`

```sh
npm ci
npm run dev
npx tsc --noEmit
node --experimental-strip-types tests/inventory.test.mjs
npm run build:pages
```

อัปโหลด `pages-dist/index.html` ที่ได้แทน `index.html` ใน repository นี้ GitHub Pages จะเผยแพร่เวอร์ชันใหม่ โดยยังย้อนกลับผ่าน commit history ได้

Supabase project: `pjahviamqmnfpnidydhe` กำหนด Auth Site URL และ redirect URLs ให้ตรงกับ `https://SnokeyNut.github.io/Stock/` สำหรับการยืนยันอีเมลในเว็บจริง

AI อ่านบิล/รูปเบิก, POS, Recipe/BOM, Food Cost และ Usage Variance เป็น Coming Soon ไม่มีการส่ง LINE อัตโนมัติ

เว็บเดิมของบัญชี `siamsukicnx` และ Supabase project เดิมไม่ถูกแก้ไข ไม่ได้ย้ายข้อมูลเก่าเข้า Phase 1 อัตโนมัติ
