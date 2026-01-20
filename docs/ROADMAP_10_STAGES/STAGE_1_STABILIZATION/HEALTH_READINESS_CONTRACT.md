# عقد الصحة والجاهزية (Health/Readiness)

## لماذا؟
- Health = هل الخدمة تعمل؟
- Readiness = هل الخدمة جاهزة لاستقبال الترافيك؟

## Endpoints
- `GET /api/health/live` (Public)
  - سريع جدًا
  - لا يلمس قاعدة البيانات
- `GET /api/health/ready` (Public)
  - يفحص قاعدة البيانات
  - يفحص تهيئة Settings Registry
- `GET /api/health/details` (Auth)
  - تفاصيل أكثر + إحصاءات

## قواعد تشغيلية
- Nginx/Load balancer يجب أن يستخدم:
  - live لإثبات الحياة
  - ready لبدء توجيه الترافيك

## ملاحظة للمصمم
- لا تعتمد واجهة المستخدم على هذه endpoints لعرض بيانات تشغيلية للمستخدم.
- واجهة المستخدم تعتمد على dashboard/reports المصرّح بها.
