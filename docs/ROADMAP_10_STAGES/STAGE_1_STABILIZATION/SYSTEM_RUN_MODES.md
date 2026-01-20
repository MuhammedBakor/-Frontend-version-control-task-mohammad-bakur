# المرحلة 1 — الإقفال التشغيلي (Stabilization)

- **Runtime واحد فقط**: `ghaith-api/`.
- الهدف: تشغيل ثابت + توثيق تشغيل واضح.

## Dev
- `NODE_ENV=development`
- يُفضّل تفعيل: `GOVERNANCE_CHECK_ON_BOOT=true` أثناء التطوير.

## Staging
- `NODE_ENV=production`
- `GOVERNANCE_CHECK_ON_BOOT=true` للتأكد قبل النشر.
- `GOVERNANCE_STRICT=true` فقط عند الحاجة (قد يوقف الإقلاع إذا وجد مفاتيح إعدادات غير مسجلة).

## Production
- `NODE_ENV=production`
- `GOVERNANCE_CHECK_ON_BOOT=false`
- `LOG_HTTP=true` عند وجود تجميع Logs.
