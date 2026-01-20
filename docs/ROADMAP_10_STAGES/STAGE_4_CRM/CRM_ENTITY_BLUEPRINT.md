# Stage 4 — CRM Core (Blueprint)

> الهدف: تعريف كيان "العميل" ككيان تجاري حقيقي داخل غيث، وربطه بكل مسارات النظام بدون تداخل منطقي.

## 1) الكيانات (Entities)

### 1.1 Customer (crm_customers)
- **id**: معرف ثابت.
- **org_id / branch_id**: نطاق المؤسسة/الفرع (الفرع اختياري).
- **name**: اسم العميل.
- **status**: ACTIVE / INACTIVE / ARCHIVED.
- **customer_type**: individual / company / vendor / agent / other.
- **tags_json**: مصفوفة Tags.
- **meta_json**: بيانات إضافية (JSON) تُستخدم لاحقًا حسب الأنشطة (عمرة/نقليات/مقاولات/قانوني...)

### 1.2 Contact (crm_contacts)
- جهة اتصال مرتبطة بعميل واحد.
- الحقول: name / phone / email / role_title / notes.

### 1.3 Interaction (crm_interactions)
- سجل تواصل زمني.
- **channel**: whatsapp/email/phone/meeting/system/other.
- **direction**: IN/OUT.
- **subject/body**: محتوى مختصر للتوثيق.
- **occurred_at**: وقت حدوث التفاعل.

### 1.4 Link (crm_links)
- ربط العميل بكيانات من مسارات أخرى **بدون** نقل منطق الأعمال.
- **entity_type**: نص يُعرّف المسار/الكيان (requests/projects/legal/finance/documents/other).
- **entity_id**: معرف الكيان.
- **note**: سبب الربط.

## 2) Lifecycle
- Customer:
  - ACTIVE: قابل للتعامل.
  - INACTIVE: مُعطّل (لا يُحذف).
  - ARCHIVED: أرشفة (للتاريخ).

## 3) مبدأ عدم التداخل
- CRM لا يقرر شيئًا نيابة عن أي مسار.
- CRM يقدم:
  - ملف العميل
  - Timeline
  - روابط
- القرارات (اعتماد/رفض/إقفال) تظل داخل مسارها القائد.
