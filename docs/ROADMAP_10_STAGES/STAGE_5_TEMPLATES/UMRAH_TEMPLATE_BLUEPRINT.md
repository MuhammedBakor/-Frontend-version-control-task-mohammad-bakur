# قالب العمرة (Umrah Template) — Blueprint

## الهدف التشغيلي
تهيئة النظام ليعمل كمنصة عمرة بسرعة عبر:
- تفعيل الوحدات الأساسية
- ضبط إعدادات افتراضية تقلل العمل اليدوي

## ما الذي يفعله القالب حاليًا (v1)

### 1) Feature Flags
يفعل:
- requests
- documents
- notify
- reports
- crm

### 2) Settings Overrides (Org Scope)
- `requests.sla.enabled = true`
- `requests.autoassign.enabled = true`
- `crm.enabled = true`
- `crm.timeline.max_items = 200`

## ما الذي لن يفعله القالب (ممنوع)
- إنشاء طلبات/فواتير/قضايا جاهزة داخل بيانات التشغيل
- تعديل منطق وحدات أخرى

## خطوط التوسع (v2)
بعد اعتماد v1، يمكن إضافة:
- Seed Workflows في مسار workflows (عبر API رسمية)
- قوالب طباعة للخطابات/الفواتير (documents/templates)
- تقارير جاهزة موجهة لنشاط العمرة