# عقد البيئة (ENV Contract)

هذا العقد يحدد المتغيرات المعتمدة لتشغيل غيث.

## ملف البيئة
- انسخ: `ghaith-api/.env.example` إلى `ghaith-api/.env`

## مفاتيح أساسية
- `PORT`: منفذ السيرفر.
- `NODE_ENV`: `development` أو `production`.
- `TRUST_PROXY`: عند التشغيل خلف Nginx/Proxy.

## الحوكمة
- `GOVERNANCE_CHECK_ON_BOOT`:
  - true: يشغّل فحص حوكمة عند الإقلاع (أبطأ لكنه يكشف مشاكل).
- `GOVERNANCE_STRICT`:
  - true: يوقف الإقلاع إذا وجد Settings غير مسجلة أو 타입 غير متطابق.

## التسجيل (Logs)
- `LOG_HTTP`:
  - true: يسجل كل طلب HTTP بصيغة JSON lines.

## ملاحظة للمصمم
- المصمم لا يحتاج أي ENV.
- أي سلوك في الواجهة لازم يُبنَى على:
  - صلاحيات (RBAC)
  - سياق org/branch
  - persona
وليس على ENV.
