# سياسة التسجيل (Logging Policy)

## مبادئ
1) لا نطبع معلومات حساسة (tokens/passwords)
2) جميع عمليات الحساسة تُسجل في Audit/Ledger (Evidence-grade)
3) لوج HTTP اختياري ويُفعّل عبر ENV فقط

## HTTP Access Logs
- فعّل: `LOG_HTTP=true`
- الصيغة: JSON lines (مناسبة لـ ELK/Datadog)
- يتضمن: method, path, status, ms, traceId, ip

## Error Logs
- الأخطاء الحرجة يجب أن تظهر في stderr (console.error)
- لا تفصح عن معلومات المستخدم في رسالة الخطأ.

## ملاحظة للمصمم
- رسائل الخطأ في الواجهة تُبنى على `ErrorCodes` وليس على نصوص console.
