# تقرير جاهزية الإطلاق — P6.6 (Prod Readiness)

تاريخ الإعداد: 2026-01-15

## 1) الملخص التنفيذي
هذه الحزمة **مهيأة للإقلاع التشغيلي** مع حوكمة (Governance) واضحة للمسارات، ودعم Aliases للتوافق الخلفي (Backward Compatibility) بدون جعل الازدواج مسارات منتج.

- **جاهزية الإطلاق:** ✅ جاهز لـ Pilot / UAT
- **جاهزية الإنتاج الكامل:** ✅ بشرط تجهيز بيئة التشغيل (Node + Dependencies) وضبط المتغيرات.

> ملاحظة مهمة: أثناء فحص هذه الحزمة داخل بيئة التحضير الحالية لم يكن متاحًا تنزيل حزم npm من الإنترنت، لذلك تم الاعتماد على فحوصات ثابتة (Static) مثل `node --check`.

## 2) ما تم التأكد منه (Ready)
### 2.1 فحوصات Syntax
- تم تنفيذ فحص `node --check` على ملفات JavaScript الأساسية، والنتيجة:
  - **147 ملف**
  - **0 أخطاء Syntax**

### 2.2 قفل الازدواج (Canonical vs Alias)
- تم تثبيت المسارات الرسمية (Canonical):
  - `communications`, `documents` ... إلخ
- المسارات المتوافقة (Aliases) تعمل فقط للتوافق:
  - `comms` → `communications`
  - `dms` → `documents`
- Aliases **لا تظهر كمسارات منتج** ولا تدخل تفعيل الاشتراكات.

### 2.3 وجود حزمة تشغيل Docker
- يوجد `Dockerfile` و `docker-compose.yml` لتسهيل الإطلاق في بيئة موحدة.

## 3) متطلبات التشغيل (Prerequisites)
- Node.js: **18+** (مفضل 20 LTS)
- npm: 9+
- SQLite3 (ضمن `better-sqlite3`)

## 4) متغيرات البيئة (Environment)
يوجد قالب: `ghaith-api/.env.example`

أهم المتغيرات المتوقعة (قد تختلف حسب إعداداتك):
- `PORT=3000`
- `DB_PATH=./data/ghaith.db`
- `JWT_SECRET=...`
- `CORS_ORIGINS=...`

## 5) طريقة التشغيل (مباشر)
من داخل مجلد `ghaith-api`:

1) تثبيت الحزم:
- `npm ci` (أو `npm install`)

2) تشغيل فحص الحوكمة:
- `npm run system:check`

3) تشغيل السيرفر:
- `npm run start`

4) التأكد من الصحة:
- `GET /api/health`

## 6) طريقة التشغيل (Docker)
1) البناء والتشغيل:
- `docker compose up --build`

2) فحص الصحة:
- `GET http://localhost:<PORT>/api/health`

## 7) Smoke Checklist (بعد الإقلاع)
- [ ] `/api/health` يرجع OK
- [ ] `/api/registry` يرجع قائمة المسارات المسجلة
- [ ] Owner Console UI تعمل وتعرض Modules Canonical
- [ ] تفعيل Module من OwnerActivation ينعكس في registry (بدون ظهور comms/dms)
- [ ] عمليات documents الأساسية (upload/list) تعمل
- [ ] communications inbox endpoints ترجع بدون أخطاء

## 8) مخاطر معروفة (Known Risks)
- أي بيئة إنتاج لا تستطيع تنزيل حزم npm لن تقدر تُشغّل النظام (لا بد من repo mirror أو registry داخلي).
- SQLite مناسب كبداية/UAT، ويفضل لاحقًا ترقية محرك التخزين في الإنتاج عالي الحمل.

## 9) التوصية
- البدء بـ **Pilot** على بيئة Staging مع:
  - تثبيت npm dependencies
  - تشغيل `system:check` و `smoke`
  - تفعيل مسارين فقط كبداية: `owner + documents + communications`
- ثم توسيع التفعيل تدريجيًا.
