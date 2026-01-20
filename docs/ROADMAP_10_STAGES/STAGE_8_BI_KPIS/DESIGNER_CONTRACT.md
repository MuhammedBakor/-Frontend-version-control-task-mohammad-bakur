# Stage 8 — BI & KPIs (Contracts للمصمم)

## الهدف
لوحات مؤشرات Read-only تعتمد على:
- كتالوج KPI
- Query API

## الصفحات المقترحة
1) كتالوج المؤشرات
2) تنفيذ استعلام KPI (فلاتر + تاريخ + مقارنة فروع)
3) تصدير (PDF/Excel) — التصميم فقط، التنفيذ في reports لاحقًا

## API Reference
- `/api/bi/kpis/catalog`
- `/api/bi/kpis/query`

## قواعد الفلاتر
- org/branch/persona إلزامي
- أي KPI يحدد `filters_allowed` من الكتالوج (في هذه النسخة: تصمم الشكل وتخلي التحقق على الـ API)
