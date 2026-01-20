# تعليمات للمصمم — قوالب الأنشطة

> هذه المرحلة **بدون UX** حاليًا، لكن هذه التعليمات تضمن أن الواجهة المستقبلية تُبنى صح.

## 1) صفحات الواجهة المطلوبة (اقتراح UI Catalog)

### (A) صفحة: كتالوج القوالب
**Purpose:** عرض القوالب المتاحة + وصفها + نسخة القالب + أزرار “معاينة/تثبيت”.

**Data Source:**
- `GET /api/templates/catalog`

**UI Rules:**
- لا تعرض زر “تثبيت” إلا إذا المستخدم يملك `templates:install:execute`.
- اعرض “نطاق التثبيت” كاختيار: `org` أو `branch` (إذا كان `templates.install.allow_branch_scope=true`).

### (B) صفحة: معاينة تأثير القالب (Dry-Run)
**Purpose:** قبل التثبيت، نعرض “ما الذي سيتغير” (feature flags + settings overrides).

**Data Source:**
- `POST /api/templates/install/preview`

**UI Rules:**
- اعرض التأثيرات على شكل جدول:
  - type (featureflag/setting_override)
  - key
  - scope
  - previous_value → new_value

### (C) صفحة: سجل التثبيتات
**Purpose:** تاريخ القوالب المثبتة + من ثبّت + متى + خيار rollback.

**Data Source:**
- `GET /api/templates/installs`

**UI Rules:**
- لا تعرض زر “Rollback” إلا إذا المستخدم يملك `templates:install:rollback`.
- عند الضغط rollback لازم يظهر مربع سبب (Reason) قبل الإرسال.

## 2) قواعد مهمة

### (A) لا يوجد “تغيير مباشر في وحدات”
التثبيت يغيّر فقط:
- `featureflags`
- `settings_overrides`

### (B) كل تثبيت/تراجع لازم يظهر في Audit + Event
لا تسوّي أي “تثبيت صامت”.

### (C) عرض السياق بوضوح
دائمًا اعرض في رأس الصفحة:
- الشركة (org)
- الفرع (branch)
- الصفة (persona)

## 3) أخطاء متوقعة (Error Contracts)

- `CONTEXT_REQUIRED`: المستخدم لم يحدد org/branch/persona.
- `SCOPE_ID_REQUIRED`: حاول تثبيت على branch بدون branch.
- `TEMPLATE_KEY_MISMATCH` / `ENOENT`: قالب غير موجود.

## 4) لا تتجاوز الحدود
أي محاولة من الواجهة لتغيير “منطق أعمال” القالب (مثل إنشاء workflows مباشرة من الواجهة) **ممنوع** في هذه المرحلة. فقط تثبيت/معاينة/تراجع.
