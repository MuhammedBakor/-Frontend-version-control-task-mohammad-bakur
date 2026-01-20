# ملاحظات للمصمم (Stage 3)

## هدفك كمصمم
أنت لا "تخترع" شاشات من الصفر.
أنت تبني UI على عقود موجودة:
- Context (org/branch/persona)
- RBAC permissions
- Registry nav
- UI Catalog

## أول شاشة في النظام الداخلي
**Persona Selector** (مرحلة 2) ثم بعدها **Home** بحسب persona.

## لا تُنفذ هذا (ممنوع)
1. لا تجعل UI يرسل أي طلب محمي بدون persona.
2. لا تعرض زر/تحت-قائمة/صفحة إذا لا يملك المستخدم الصلاحية.
3. لا تعتمد على "ثبات" نفس persona/branch أثناء جلسة طويلة؛ ممكن يتغير.
4. لا تكتب صلاحيات داخل UI كقيم ثابتة خارج catalog/registry.

## نفذ هذا (لازم)
1. عند أول تحميل:
   - `GET /api/auth/me` (أو endpoint المستخدم الحالي إن وجد)
   - `GET /api/auth/options`
   - `GET /api/registry/nav`
   - `GET /api/ui/catalog`
2. اعرض شريط علوي ثابت:
   - الشركة/الفرع
   - persona
   - زر تبديل
3. عند كل فعل عالي الخطورة:
   - استخدم Confirmation UI
   - وأرسل Headers: `X-Confirm-Persona` + `X-Confirm-Branch`
   - ويفضل Trigger `POST /api/ui/confirm` للتدقيق (اختياري)

## معايير جودة بسيطة
- لا تزيد عن 3 نقرات للوصول للطلبات/المهام
- لا تعرض "تقرير" بدون فلتر org/branch واضح
- أي طباعة/توقيع لازم يظهر فيها persona/branch في الهيدر
