# Stage 9 — Integrations (Contracts للمصمم)

## الهدف
شاشة تكاملات لا تقوم بالإرسال فعليًا؛ فقط:
- إدارة الكتالوج
- مشاهدة طابور الإرسال Outbound
- مشاهدة سجلات Webhooks Inbound

## صفحات مقترحة
1) Integrations Catalog
2) Outbound Queue Monitor
3) Inbound Webhooks (Evidence)

## API Reference
- `/api/integrations/catalog`
- `/api/integrations/outbound/enqueue`
- `/api/integrations/outbound/queue`
- `/api/integrations/webhooks/...` (Public)

## قواعد أمان مهمة
- Webhooks PublicRoute: لا تعتمد عليه كواجهة استخدام، يكون فقط لاستقبال مزود خارجي.
- أي عرض داخلي لسجلات الوارد يكون RBAC + Scoping.
