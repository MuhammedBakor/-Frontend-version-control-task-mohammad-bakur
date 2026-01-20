# خارطة طريق غيث — 10 مراحل (بدون UX)

هذا المجلد يُستخدم كـ **مرجع تشغيل + مرجع تصميم**.

- لا يحتوي على رسومات أو ألوان أو UI جاهز.
- يحتوي على **عقود صفحات** (Page Contracts) + **قواعد تفاعل** (Interaction Rules) + **مصفوفة صلاحيات/صفات**.
- الهدف: أي مصمم/مطور واجهات يستلم لاحقًا يقدر يبني صفحات صحيحة **بدون ما يكسر حدود المسارات**.

## مبادئ إلزامية
1) **المسار القائد يقرر، والمسارات الخادمة تنفّذ** (Leader/Service)
2) **لا شاشة بلا أثر**: كل إجراء لازم ينتج (Audit + Event + Status)
3) **لا إجراء بدون سياق**: org/branch + persona
4) **لا عرض بدون صلاحية**: RBAC هو مصدر الحقيقة
5) **العقود قبل الواجهات**: أي صفحة لازم تُربط بـ API Contracts + Events + Settings

## فهرس المراحل
- STAGE_1_STABILIZATION
- STAGE_2_PERSONA_BRANCH
- STAGE_3_CORE_PAGES
- STAGE_4_CRM
- STAGE_5_TEMPLATES
- STAGE_6_FIELD_TRACKING
- STAGE_7_FINANCE_CORE
- STAGE_8_BI_KPIS
- STAGE_9_INTEGRATIONS
- STAGE_10_AI_GOVERNANCE
