# Stage 7 — Finance Core (Contracts للمصمم)

## الهدف
واجهة مالية قابلة للبناء لاحقًا بدون تغيير في الـ API.

## الصفحات المقترحة
1) دليل الحسابات (COA)
2) القيود اليومية (Journal Entries)
3) الفترات (Periods)
4) ميزان المراجعة (Trial Balance)

## قواعد إلزامية
- لا يتم إنشاء/تعديل أي شيء بدون org/branch/persona
- كل عملية حفظ تعرض نتيجة واضحة (ok, id)
- في حال نقص صلاحية: 403 ...

## API Reference
كلها تحت:
- `/api/finance/accounting/*`

### COA
- GET `/api/finance/accounting/coa`
- POST `/api/finance/accounting/coa/upsert`

### Periods
- GET `/api/finance/accounting/periods`
- POST `/api/finance/accounting/periods/upsert`

### Journal
- GET `/api/finance/accounting/journal`
- POST `/api/finance/accounting/journal`
- GET `/api/finance/accounting/journal/:id`

### Trial Balance
- GET `/api/finance/accounting/trial_balance`
