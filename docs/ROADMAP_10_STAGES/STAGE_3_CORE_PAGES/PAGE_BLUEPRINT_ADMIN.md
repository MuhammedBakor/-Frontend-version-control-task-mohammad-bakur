# Blueprint — لوحة الإدارة (Admin / Owner)

## الهدف
واجهة الإدارة هي "لوحة قيادة" للنظام:
- إدارة المستخدمين والعضويات
- إدارة التفعيل/الاشتراكات/الحدود
- مراقبة الصحة والتدقيق

## شروط الدخول
- Authenticated
- Context: orgId + branchId + persona in (admin, owner)

## مناطق الصفحة
1. **شريط علوي ثابت**
2. **System Health**
   - Live/Ready status
   - آخر أخطاء Telemetry
3. **Governance**
   - Event contracts status (مؤشر)
   - Permission gate status (مؤشر)
4. **الكيانات الأساسية**
   - Users / Roles / Context Access
   - Feature Flags
   - Settings

## مصادر البيانات (Endpoints)
- `GET /api/health/details` (محمي)
- `GET /api/audit?limit=...`
- `GET /api/telemetry/...`
- `GET /api/registry/modules`
- `GET /api/settings`
- `GET /api/org/...`

## الأفعال الحساسة (تتطلب Confirm)
- تغيير صلاحيات/أدوار/سياقات
- تغيير إعدادات مالية/ضريبية
- نشر قالب/تفعيل مسار

## أخطاء متوقعة
- `FORBIDDEN` → لا تظهر أي عناصر إدارة إذا ما عنده صلاحية.
