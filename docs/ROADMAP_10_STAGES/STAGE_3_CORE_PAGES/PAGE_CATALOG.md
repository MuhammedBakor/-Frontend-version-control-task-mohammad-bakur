# المرحلة 3: كتالوج الصفحات (Page Catalog) — بدون UX

هذا الملف هو **عقد واجهات** للمصمم/الواجهة الأمامية.
لا يحتوي أي تصميم، لكنه يحدد:
- ما الصفحات الموجودة.
- من يراها (Persona + Permission).
- ما هي مصادر بياناتها (Endpoints) وما هي الأفعال الحساسة التي تتطلب تأكيد.

## مبادئ غير قابلة للتفاوض

1) **لا صفحة داخلية بدون Persona**
- أي صفحة داخلية (Authenticated) تتطلب Persona نشطة.
- عند غياب Persona: يتم إظهار شاشة اختيار الصفة/الفرع.

2) **الفرع/الشركة جزء من هوية الشاشة**
- يجب أن يظهر في الهيدر دائمًا: الشركة + الفرع + Persona النشطة.
- أي تبديل للفرع أو الشركة يعيد تحميل البيانات.

3) **المنيو مبني على Registry وليس على كود الواجهة**
- الواجهة تبني التنقل من `/api/registry/nav` و`/api/registry/modules`.
- لا تُ hardcode مسارات داخل الواجهة.

4) **كل فعل حساس يحتاج تأكيد Persona/Branch**
- أي عملية: طباعة/توقيع/إرسال خارجي/اعتماد مالي
  يجب أن تستخدم تأكيد عبر Headers:
  - `X-Confirm-Persona`
  - `X-Confirm-Branch`

5) **الصفحة ليست مجرد عرض — لها عقد بيانات واضح**
- كل صفحة لها:
  - Data endpoints
  - Widgets (مكونات منطقية)
  - Actions

## مصدر الكتالوج الرسمي

الكتالوج الرسمي موجود في الباكند (Stage 3):
- `ghaith-api/kernel/uiCatalog.js`

والواجهة تجلبه عبر:
- `GET /api/ui/catalog`

> هذا الـ endpoint يرجع كتالوج **مفلتر حسب صلاحيات المستخدم**.

## الصفحات الأساسية (Minimum Viable Pages)

> ملاحظة: الأسماء هنا “Contracts” ويمكن للمصمم تغيير النصوص/الأيقونات بدون كسر العقد.

### A) صفحات عامة داخلية (Global Internal)

1) **Home / Dashboard**
- Route: `/app/home`
- Personas: employee, manager, admin
- Permission: `dashboards:read`
- Data:
  - `GET /api/dashboards/summary`
  - `GET /api/requests/stats`
- Widgets: kpis, quick_actions
- Sensitive actions: لا

2) **Requests Inbox**
- Route: `/app/requests`
- Permission: `requests:read`
- Data:
  - `GET /api/requests?scope=inbox`
  - `GET /api/requests/types`
- Widgets: inbox_table, filters
- Sensitive actions: `approve`, `escalate` (تتطلب Confirm)

3) **My Tasks / Projects Tasks**
- Route: `/app/projects/tasks`
- Permission: `projects:tasks:read`
- Data:
  - `GET /api/projects/tasks?scope=my`
  - `GET /api/projects/milestones`
- Widgets: task_board, milestones_strip
- Sensitive actions: تغيير حالة/تعديل SLA (Confirm)

4) **Documents Library**
- Route: `/app/documents`
- Permission: `documents:read`
- Data:
  - `GET /api/documents`
  - `GET /api/dms/folders`
- Widgets: folder_tree, document_grid
- Sensitive actions: مشاركة/تصدير/حذف (Confirm)

5) **Reports**
- Route: `/app/reports`
- Permission: `reports:read`
- Data:
  - `GET /api/reports/catalog`
  - `GET /api/reports/run?...`
- Widgets: report_catalog, report_runner
- Sensitive actions: تصدير PDF/Excel (Confirm)

6) **Settings (Admin/Owner)**
- Route: `/app/settings`
- Permission: `settings:write`
- Data:
  - `GET /api/settings`
  - `PATCH /api/settings`
- Widgets: settings_registry, feature_flags
- Sensitive actions: تعديل إعدادات تشغيلية (Confirm)

## صفحات حسب Persona

### Persona: Employee
- Dashboard: تركيز على “مهامي، طلباتي، حضوري، مستنداتي”.
- ممنوع: أي صفحات إدارة عامة.

### Persona: Manager
- Dashboard: “فريقي، موافقات، مؤشرات تأخير، SLA”.
- مسموح: تقارير فرع/فريق.

### Persona: Admin
- Dashboard: “إدارة المستخدمين/العضويات/الإعدادات/التقارير العليا”.

## نمط بناء الصفحة (Layout Contract)

كل صفحة داخلية يجب أن تتبع نفس المكونات المنطقية (بدون تصميم):

1) Header ثابت:
- org + branch + persona
- زر تبديل persona
- زر تبديل الفرع

2) Left Nav:
- يبنى من `/api/registry/nav`

3) Content:
- Widgets حسب كتالوج الصفحة

4) Footer (اختياري):
- رقم إصدار registryVersion

## أخطاء واجب دعمها في الواجهة

- `CONTEXT_REQUIRED`: يجب توجيه المستخدم لشاشة اختيار الصفة/الفرع.
- `FORBIDDEN`: عرض رسالة صلاحيات.
- `SESSION_EXPIRED`: إعادة تسجيل الدخول.

