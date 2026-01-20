# Stage 4 — Implementation Notes (Dev)

## ما تم تنفيذه فعليًا داخل الكود
- إضافة Module جديد: `ghaith-api/modules/crm`
- إضافة جداول CRM:
  - crm_customers
  - crm_contacts
  - crm_interactions
  - crm_links
- إضافة API Endpoints الأساسية (بدون UX):
  - customers CRUD (read/create/update)
  - contacts (read/create/update)
  - timeline (read)
  - linking (create)
- إضافة Events Contracts (تم توليدها عبر `scripts/generateEventContracts.js`).
- إصلاح stop-ship خطأ في `scripts/generateDocs.js` (بسبب `*/` داخل التعليق) وتم تشغيله بنجاح.

## ملاحظات تشغيل
- `scripts/systemCheck.js` يتطلب حزمة `better-sqlite3` في بيئة Node المحلية. داخل هذه بيئة التحليل قد لا تكون مثبّتة.
- **لا يوجد UX**: الصفحات هنا عقود (UI Catalog) + تعليمات للمصمم.

## حدود المرحلة (متروكة للمرحلة 9/10)
- ربط تلقائي من Events المسارات الأخرى إلى Timeline (سيكون Listener اختياري لاحقًا).
- قنوات تواصل خارجية (WhatsApp/Email) تُسجل Interaction تلقائيًا.
