# محرك القوالب — الفكرة والتنفيذ

## لماذا القوالب؟
القالب هو الطريقة الوحيدة لجعل «غيث» يخدم أنشطة مختلفة **بدون**:
- تفرع كود (Fork)
- نسخ وحدات
- كسر الحدود المعمارية

## تعريف القالب
القالب = Package يطبق **تغييرات قابلة للتدقيق** على نفس المنصة عبر:
1) Feature Flags
2) Settings Overrides
3) (لاحقًا) Seed Workflows/Print/Reports

> ممنوع على القالب أن يكتب مباشرة في جداول “المنطق التشغيلي” لمسار آخر (مثل إنشاء قضايا/فواتير/طلبات). القالب يضبط **الإعداد** فقط.

## مكان القوالب
القوالب محفوظة كملفات JSON داخل:
`ghaith-api/modules/templates/packs/*.json`

## كيف يتم التطبيق؟
1) `POST /api/templates/install/preview` يرجع “قائمة التأثيرات” (effects)
2) `POST /api/templates/install/execute`:
   - يسجل Install Record
   - يسجل Snapshot لكل تغيير داخل `templates_install_effects`
   - يطبق التغيير في:
     - `featureflags`
     - `settings_overrides`

## التراجع (Rollback)
`POST /api/templates/install/rollback`:
- يعيد القيم السابقة (أو يحذف override إن لم يكن موجود سابقًا)
- يحدّث حالة install إلى `ROLLED_BACK`

## الضمانات (Guarantees)
- كل شيء Evidence-grade: Install + Effects
- لا Cross-tenant: scope يعتمد على org/branch من الـ Context
- لا تغيير صامت: publish events عند install/rollback
