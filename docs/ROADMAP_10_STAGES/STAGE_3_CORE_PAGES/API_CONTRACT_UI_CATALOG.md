# عقد API — UI Catalog

## 1) GET /api/ui/catalog
يعيد كتالوج الصفحات **مفلترًا** حسب صلاحيات المستخدم.

### المتطلبات
- Cookie session
- Context (orgId/branchId/persona)

### Example Response (مختصر)
```json
{
  "meta": { "version": "2026.01.19.1", "personaCount": 5, "pageCount": 11 },
  "activeContext": { "orgId": "ORG_1", "branchId": "BR_1", "persona": "employee" },
  "personas": [ { "key": "employee", "title_ar": "موظف" } ],
  "pages": [
    {
      "id": "home.employee",
      "route": "/app/home",
      "title_ar": "لوحة الموظف",
      "moduleKey": "dashboards",
      "permission": "dashboards:home:read",
      "widgets": ["kpi_strip", "my_requests", "my_tasks"],
      "data": [ { "method": "GET", "path": "/api/registry/nav" } ],
      "confirmPersona": false
    }
  ]
}
```

### أخطاء متوقعة
- `CONTEXT_REQUIRED`: يجب توجيه المستخدم لاختيار الصفة/الفرع.
- `FORBIDDEN`: المستخدم لا يملك صلاحية كافية.
- `SESSION_EXPIRED`: تسجيل دخول.

---

## 2) POST /api/ui/confirm
Endpoint اختياري (عقد) لتأكيد المستخدم قبل الأفعال عالية الخطورة.

### المتطلبات
- Cookie session
- Permission: `ui:confirm:create`

### Body
```json
{
  "action": "print",
  "entityType": "invoice",
  "entityId": "INV_123",
  "note": "اختياري"
}
```

### ملاحظة مهمة
الإنفاذ الحقيقي يتم عبر Middleware `requirePersonaConfirmation(...)` على الـ Route الحساس.
هذا الـ endpoint فقط يوفّر نمط موحّد للواجهة.
