# المرحلة 5: قوالب الأنشطة (Industry Templates)

## الهدف
تحويل «غيث» من منصة عامة إلى منصة **تتكيف بسرعة** مع أي نشاط (عمرة، فنادق، نقليات، مقاولات…)
بدون تفرع كود (Fork) وبدون كسر المسارات.

## المبدأ الحاكم
القالب = **حزمة إعدادات** + **تفعيل وحدات** + (لاحقًا) **قواعد Workflow / طباعة / تقارير**

> القالب لا يحق له إنشاء “منطق قرار” داخل مسارات خادمة. القرار يبقى في المسار القائد.

## ناتج المرحلة 5 (Deliverables)
- محرك قوالب في Backend (Templates Module)
- API Catalog + Preview + Install + Rollback
- حزمة قالب جاهزة كبداية: `umrah.v1`
- توثيق عقود وتوجيهات للمصمم

## مكان الكود
- `ghaith-api/modules/templates/*`

## مكان الحزم (Packs)
- `ghaith-api/modules/templates/packs/*.json`

## API
راجع: `TEMPLATE_CONTRACT.md`
