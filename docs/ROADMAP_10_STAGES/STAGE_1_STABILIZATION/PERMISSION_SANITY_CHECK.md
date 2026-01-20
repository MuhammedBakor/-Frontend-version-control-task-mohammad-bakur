# فحص الصلاحيات (Permission Sanity)

## القاعدة
أي Route داخل النظام يجب أن يكون أحد التالي:
- `requirePermission(...)`
- أو `publicRoute(reason)` (نادرًا وبمبرر)

## تطبيق فعلي
النظام يشغّل Gate عند الإقلاع عبر:
- `assertRouterPermissionCoverage(...)`

## What Designer Must Assume
- الواجهة لا تفترض أي شيء.
- كل عنصر (زر/قائمة/إجراء) لازم يرتبط بـ Permission معلن.
