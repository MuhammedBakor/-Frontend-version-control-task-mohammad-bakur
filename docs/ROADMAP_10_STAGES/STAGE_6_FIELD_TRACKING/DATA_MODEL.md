# Data Model — STAGE_6_FIELD_TRACKING

## الفلسفة
- تتبع **مرتبط بمهمة** (Task-based) وليس تتبع مستمر.
- كل سجل يحمل: `org_id + branch_id + user_id + persona_key` لضمان الدقة القانونية.

## كيانات
### 1) field_geofences
يُستخدم لتحديد "نطاق عمل" اختياري للتأكيد (Enforcement).

حقول أساسية:
- `id`
- `org_id, branch_id`
- `name`
- `center_lat, center_lng, radius_m`
- `active`
- `meta_json`

### 2) field_checkins
سجل دليل/إثبات للزيارة/الحضور الميداني.

الأنواع (kind):
- `CHECKIN` دخول
- `CHECKOUT` خروج
- `PING` نقطة إثبات وسطية
- `NOTE` ملاحظة ميدانية

حقول أساسية:
- `task_id` اختياري (لكن **موصى به دائمًا**)
- `project_id` اختياري
- `lat/lng/accuracy_m/address_text`
- `photo_document_id` (عبر مسار Documents)
- `note`
- `occurred_at`

### 3) field_task_runs
تشغيل مهمة ميدانية (Start/End) يسهّل تقارير الإنجاز واحتساب الوقت.

حالات (status):
- `ACTIVE`
- `DONE`
- `CANCELED`
