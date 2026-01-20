# Blueprint — لوحة الموظف (Employee Home)

## الهدف
واجهة يومية للموظف تعرض:
- ماذا عليّ اليوم؟
- ما هي طلباتي؟
- ما هي مهامي؟

## شروط الدخول
- Authenticated
- Context: orgId + branchId + persona=employee

## التكوين العام (Layout zones)
1. **شريط علوي ثابت**
   - اسم الشركة/الفرع
   - الصفة النشطة
   - زر تبديل الصفة/الفرع
   - اختصار "الإشعارات"
2. **ملخص سريع (Summary Cards)**
   - عدد الطلبات المفتوحة
   - عدد المهام المتأخرة
   - آخر إشعار/تنبيه
3. **قوائم تشغيل (Worklists)**
   - طلباتي: آخر 10
   - مهامي: آخر 10
   - مشاريع/مراحل: ما يخصني (اختياري)

## مصادر البيانات (API)
- `GET /api/auth/options` (لشريط السياق)
- `GET /api/registry/nav` (القائمة حسب الصلاحيات)
- `GET /api/requests/my` أو `GET /api/requests?assignee=me&status=open` (حسب ما توفر في requests)
- `GET /api/projects/tasks?assignee=me&status!=done` (حسب ما توفر)
- `GET /api/notify/inbox` أو `GET /api/notifications/inbox` (حسب module)

## الأفعال
- فتح طلب
- فتح مهمة
- إنشاء طلب جديد (إن كانت الصلاحية موجودة)

## الأفعال الحساسة (تتطلب Confirmation)
- طباعة/توقيع/إرسال مستند: يجب استدعاء `POST /api/ui/confirm` ثم إرسال Headers التأكيد عند تنفيذ الفعل.

## حالات الخطأ
- `CONTEXT_REQUIRED`: توجيه إلى شاشة اختيار الصفة/الفرع.
- `FORBIDDEN`: لا تظهر لوحة الموظف.
