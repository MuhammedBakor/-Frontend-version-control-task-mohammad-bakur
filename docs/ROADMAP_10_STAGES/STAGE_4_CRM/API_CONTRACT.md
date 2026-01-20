# Stage 4 — CRM Core (API Contract)

## قاعدة عامة
- كل الطلبات تتطلب: **Auth + Scope + Persona**.
- جميع endpoints تحت:
  - `/api/crm/*` (Canonical)
  - `/api/modules/crm/*` (Module prefix)

## 1) Customers
### GET /api/crm/customers
- Permission: `crm:customer:read`
- Response: `{ ok, customers: [...] }`

### POST /api/crm/customers
- Permission: `crm:customer:create`
- Body:
  - name (required)
  - status (optional)
  - customer_type (optional)
  - tags (optional string[])
  - meta (optional object)
- Returns: `{ ok, id }`

### GET /api/crm/customers/:id
- Permission: `crm:customer:read`

### PATCH /api/crm/customers/:id
- Permission: `crm:customer:update`
- Partial update.

## 2) Contacts
### GET /api/crm/customers/:id/contacts
- Permission: `crm:contact:read`

### POST /api/crm/contacts
- Permission: `crm:contact:create`
- Body: customer_id + name + optional fields

### PATCH /api/crm/contacts/:id
- Permission: `crm:contact:update`

## 3) Timeline
### GET /api/crm/customers/:id/timeline
- Permission: `crm:customer:read`
- Returns merged list of interactions + links sorted by `ts` desc.
- Controlled by setting: `crm.timeline.max_items`.

### POST /api/crm/customers/:id/interactions
- Permission: `crm:interaction:create`
- Body:
  - channel (required)
  - direction (optional)
  - subject/body (optional)
  - occurred_at (optional)

## 4) Linking
### POST /api/crm/customers/:id/links
- Permission: `crm:link:create`
- Body:
  - entity_type (required)
  - entity_id (required)
  - note (optional)

## 5) Errors
- `CONTEXT_REQUIRED`: org/branch/persona missing
- `NOT_FOUND`: customer/contact not found
- `VALIDATION_ERROR`: schema validation
