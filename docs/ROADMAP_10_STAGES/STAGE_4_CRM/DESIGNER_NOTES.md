# تعليمات للمصمم — STAGE_4_CRM (CRM Core)

## 1) مبادئ غير قابلة للتفاوض
1) كل صفحة تبدأ بعرض: **الشركة/الفرع/الصفة** (Context Banner) بشكل واضح.
2) كل عنصر UI (زر/تاب/قائمة) مربوط بصلاحية RBAC ويختفي إن لم تتوفر.
3) أي إجراء "مؤثر" (إنشاء/تعديل/ربط/تواصل) يجب أن يمر عبر **تأكيد الصفة** (Persona Confirm) وفق Stage 2 + Stage 3.
4) CRM هنا **مسار قائد** داخل نطاق "تعريف العميل" فقط، لكنه **لا يقرر** عن مسارات أخرى.

## 2) الصفحات المطلوبة (بدون تنفيذ UI الآن)
- **/crm** (قائمة العملاء)
  - جدول + بحث + فلتر (status/type/tags)
  - زر "عميل جديد" (يتطلب confirmPersona)
- **/crm/customers/:id** (ملف عميل)
  - Header: الاسم + الحالة + tags
  - Tabs:
    1) Timeline
    2) Contacts
    3) Links
- **/crm/customers/:id/actions** (إجراءات)
  - Log Interaction
  - Create Contact
  - Create Link

## 3) شكل Timeline (اقتراح تصميم)
- عناصر timeline نوعان:
  - Interaction: channel + direction + subject + body + occurred_at + actor_user_id
  - Link: entity_type + entity_id + note + created_at
- كل عنصر يظهر كـ Card بسيط مع أيقونة حسب النوع.

## 4) Linking UX
- عند إنشاء Link:
  - Dropdown entity_type (requests/projects/legal/finance/documents/other)
  - حقل entity_id
  - note اختياري
- عند عرض Link:
  - زر "فتح" يفتح صفحة المسار القائد المناسبة (إن توفرت route عندكم لاحقًا)
  - لا تُعرض تفاصيل الكيان المرتبط داخل CRM إلا إذا تم جلبها من المسار القائد بصلاحياته.

## 5) بيانات الحقول (Labels عربية أولًا)
- العميل:
  - الاسم
  - النوع
  - الحالة
  - الوسوم
  - بيانات إضافية (JSON) — للمشرف فقط إن لزم
- جهة الاتصال:
  - الاسم
  - الجوال
  - البريد
  - المسمى/الدور
  - ملاحظات
- التفاعل:
  - القناة
  - الاتجاه
  - الموضوع
  - الوصف
  - وقت الحدث

