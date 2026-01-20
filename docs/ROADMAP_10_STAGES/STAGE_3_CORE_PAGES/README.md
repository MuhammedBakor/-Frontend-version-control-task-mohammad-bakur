# المرحلة 3: Core Pages — بدون UX

هذه المرحلة لا تُنتج تصميمًا ولا Frontend.
هي تُنتج **عقود صفحات** يمكن لأي مصمم/مطور واجهة أن يبني عليها بثقة بدون ما يكسر النظام.

## مخرجات المرحلة
- `PAGE_CATALOG.md`: قائمة الصفحات الرسمية + صلاحياتها + مصادر بياناتها.
- `VISIBILITY_RULES.md`: قواعد إظهار/إخفاء العناصر حسب Persona/Branch/RBAC.
- `PAGE_BLUEPRINT_EMPLOYEE.md`: Blueprint لوحة الموظف.
- `PAGE_BLUEPRINT_MANAGER.md`: Blueprint لوحة المدير.
- `PAGE_BLUEPRINT_ADMIN.md`: Blueprint لوحة الإدارة.
- `API_CONTRACT_UI_CATALOG.md`: عقد Endpoint `/api/ui/catalog`.

## تنفيذ تقني داخل الكود
- تم إضافة API جديد: `GET /api/ui/catalog`
- وتم إضافة Endpoint اختياري: `POST /api/ui/confirm`
- تم تعريف كتالوج الصفحات في: `ghaith-api/kernel/uiCatalog.js`

> أي تغيير في هذه الملفات يُعتبر تغيير عقد (Contract) ويجب أن يُراجع ويُوثَّق.
