# المرحلة 4: CRM Core

## هدف المرحلة
تأسيس **كيان العميل** داخل غيث بحيث يصبح:
- مرجعًا واحدًا لكل عميل/شركة/مورد/وكيل
- مرتبطًا بالطلبات/المشاريع/القضايا/الوثائق بدون تداخل منطقي
- جاهزًا للتوسع لاحقًا (تحصيل، حملات، واتساب...)

## ناتج المرحلة
1) Module جديد: `crm` داخل `ghaith-api/modules/crm`
2) جداول CRM الأساسية:
   - `crm_customers`
   - `crm_contacts`
   - `crm_interactions`
   - `crm_links`
3) APIs جاهزة (بدون UX):
   - Customers CRUD
   - Contacts CRUD (بحد أدنى)
   - Timeline
   - Linking
4) Events مملوكة للمسار:
   - `crm.customer.created/updated`
   - `crm.contact.created/updated`
   - `crm.interaction.logged`
   - `crm.link.created`
5) إدراج صفحات CRM داخل UI Catalog (Stage 3) كعقد للمصمم.

## ملفات التوثيق
- `CRM_ENTITY_BLUEPRINT.md`
- `API_CONTRACT.md`
- `TIMELINE_AND_LINKING.md`
- `DESIGNER_NOTES.md`
