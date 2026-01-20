# Privacy & Governance — STAGE_6_FIELD_TRACKING

## مبادئ
1) لا يوجد "تتبع دائم" داخل غيث.
2) أي جمع للموقع يجب أن يكون مرتبطًا بمهمة/طلب/أمر عمل (Task/WorkOrder).
3) تقليل البيانات: نحتفظ بالأدلة اللازمة فقط.
4) قابلية التدقيق: كل إدخال يجب أن يكون Evidence-grade.
5) لا قرارات داخل المسار: Field Tracking خادم (Service) ويُنتج أدلة وتقارير فقط.

## إعدادات حاكمة
- `field.tracking.mode = task` (إجبار)
- `field.geofence.enforce`: عند تفعيله، أي Check-in مع إحداثيات يجب أن يقع داخل أحد Geofences النشطة.
- `field.photos.enabled`: يسمح بإرفاق صورة من خلال documents (photo_document_id).
- `field.privacy.retention_days`: يحدد مدة الاحتفاظ بالسجلات الخام.

## قواعد أثبات (Legal Evidence)
- كل سجل Check-in يجب أن يحمل:
  - `occurred_at` + `created_at`
  - `user_id` + `persona_key`
  - `org_id` + `branch_id`
  - (اختياري) `task_id` و/أو `project_id`
- الطباعة/التصدير لاحقًا يجب أن يَعرض الصفة والفرع بشكل صريح.

## محاذير
- لا يتم تخزين مسار حركة (polyline) ولا عينات مستمرة.
- يمنع ربط التتبع الميداني بغير عمل مُسند (بدون task_id) إلا إذا كانت السياسة تسمح (حالياً: غير مُفعّل افتراضيًا).
