# جاهزية الإنتاج (Prod Readiness) — غيث

هذه قائمة فحص عملية قبل النشر على بيئة الإنتاج.

## 1) التشغيل والاعتمادية
- [ ] تشغيل API عبر: `npm run system:check` ثم `npm start`.
- [ ] تشغيل Smoke Test: `npm run smoke`.
- [ ] فحص Health: `/api/health` يرجع 200.
- [ ] تفعيل restart policy (Nginx/Systemd/Docker).

## 2) الأمان
- [ ] تفعيل HTTPS عبر Nginx (TLS) + HSTS حسب الحاجة.
- [ ] ضبط CORS Origins في `ghaith-api/config/index.js` (لا تفتح *).
- [ ] تأكيد Cookie Settings (secure, httpOnly, sameSite=None) حسب الدومين.
- [ ] مراجعة RBAC Coverage (Permission Gate) بدون استثناءات.

## 3) البيانات والنسخ الاحتياطي
- [ ] مسار SQLite محفوظ على Volume مستقل (`ghaith-api/data/ghaith.db`).
- [ ] نسخ احتياطي دوري (daily) + اختبار استرجاع.

## 4) الحوكمة (Governance)
- [ ] لا توجد Events schema = unknown.
- [ ] Settings PATCH ذري (Atomic) ولا يقبل جزئيًا.
- [ ] Audit لكل: create/update/delete/approve/override.
- [ ] تفعيل `GOVERNANCE_STRICT=true` بعد تنظيف بيانات settings في الإنتاج.

## 5) المراقبة والتنبيهات
- [ ] Logging مركزي + TraceId.
- [ ] تنبيهات توقف الخدمة/ارتفاع الموارد (CPU/RAM/Disk).
- [ ] مراقبة Outbox Worker/Retry Loop.

## 6) التشغيل عبر Docker (اختياري)
- [ ] `docker-compose up -d` يعمل.
- [ ] Healthcheck PASS.

---

## ملاحظات إصدار P6.9 (إغلاق نواقص إضافية)

- تم إضافة كود خطأ: `CONTEXT_REQUIRED` وتطبيق شرط وجود سياق نشط (org/branch) على كل Route محمي (باستثناء صلاحيات `system:*`).
- تم إضافة API للـ Ledger للقراءة والمراجعة: `GET /api/ledger` (يتطلب `ledger:txn:read`).
- تم توسعة Audit API ليعرض ويفلتر حسب: `actorRole` و `actorPersona` و `orgId` و `branchId`.

