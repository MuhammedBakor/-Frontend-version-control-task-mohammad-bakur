# Stage 4 — Timeline & Linking Rules

## 1) Timeline (Customer Timeline)
- الـ Timeline يجمع نوعين حاليًا:
  1) Interactions (crm_interactions)
  2) Links (crm_links)
- ترتيب العناصر: Desc by `ts`.
- الحد الأقصى: Setting `crm.timeline.max_items`.

## 2) Linking (بدون كسر الحدود)
- الربط لا ينشئ أو يعدّل كيان المسار الآخر.
- الربط هو **Reference فقط**: `entity_type + entity_id`.
- أي واجهة مستخدم تعرض تفاصيل الكيان المرتبط يجب أن تفتح صفحة المسار القائد (requests/projects/legal...) وتلتزم بصلاحياته.

## 3) توسعة مستقبلية (بدون تعديل UX الآن)
- لاحقًا نضيف Listener اختياري يلتقط أحداث من المسارات الأخرى (events) ويحوّلها إلى Timeline Items.
- هذا يكون كـ "Service" لا كمنطق قرار داخل CRM.
