# P6.5 — No Hidden Components (Inventory + SystemCheck Fix)

## الهدف
تنفيذ مبدأ **"لا يوجد شيء مخفي"** داخل حزمة غيث:

1) أي جزء موجود في الملف لازم يكون:
   - إما **مشغّل (Active)** ضمن الـ Runtime.
   - أو **معلن عنه صراحةً** بأنه **مؤرشف/مرجعي (Archived/Reference)** مع سبب واضح.
   - أو **محذوف/مستبعد** إذا تعذّر دمجه.

## التغيير المحقق
### 1) جرد شامل داخل الحزمة (Module Inventory)
تم إضافة مولّد جرد يقرأ:

- ما هو الـ Runtime الحقيقي (ghaith-api/server.js)
- وما هي الـ Modules الموجودة فعليًا داخل `ghaith-api/modules`
- وما الذي تم تركه كـ `legacy_root_pack` (مؤرشف)

الملفات الناتجة:
- `ghaith-api/docs/MODULE_INVENTORY.json`
- `ghaith-api/docs/MODULE_INVENTORY.md`

تشغيله:
```bash
cd ghaith-api
npm run inventory
```

### 2) إصلاح SystemCheck (منع أخطاء تمنع التشغيل)
تم إزالة/تصحيح أجزاء كانت تسبب أخطاء تنفيذ داخل `ghaith-api/scripts/systemCheck.js`.

## ملاحظة مهمة
وجود `legacy_root_pack` داخل الحزمة ليس "إخفاء" — لكنه **أرشيف مرجعي**.
الجرد يصرّح به ويعرض محتواه بالكامل، والـ Runtime لا يشغّله.
