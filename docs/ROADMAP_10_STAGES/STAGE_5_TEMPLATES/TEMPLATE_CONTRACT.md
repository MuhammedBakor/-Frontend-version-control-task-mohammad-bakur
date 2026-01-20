# عقد القالب (Template Contract)

## 1) JSON Schema (مبسط)

```json
{
  "key": "umrah.v1",
  "version": 1,
  "name_ar": "قالب العمرة (v1)",
  "name_en": "Umrah Template (v1)",
  "description_ar": "...",
  "description_en": "...",
  "install": {
    "featureflags": [...]
    ,"settings_overrides": [...]
  }
}
```

### featureflags item
```json
{ "key": "requests", "scope": "org", "value": 1 }
```

### settings_overrides item
```json
{ "key": "requests.sla.enabled", "type": "boolean", "scope": "org", "value": true }
```

## 2) API Contracts

### GET /api/templates/catalog
Returns available templates metadata.

### POST /api/templates/install/preview
Body:
```json
{ "template_key": "umrah.v1", "scope": "org", "reason": "optional" }
```
Returns effects array.

### POST /api/templates/install/execute
Same body as preview.

### POST /api/templates/install/rollback
Body:
```json
{ "install_id": "tpl_xxx", "reason": "optional" }
```

### GET /api/templates/installs
Returns install history for current org/branch context.

## 3) RBAC
هذا المسار قائد (Leader) — لا ينفذ قرارات تشغيلية، فقط يطبق إعدادات.

Permissions:
- `templates:catalog:read`
- `templates:install:preview`
- `templates:install:execute`
- `templates:install:rollback`

## 4) ملاحظات أمنية
- لا يوجد تثبيت بدون Context (org/branch/persona)
- لا يوجد تثبيت بدون Audit (تسجيل install + effects)