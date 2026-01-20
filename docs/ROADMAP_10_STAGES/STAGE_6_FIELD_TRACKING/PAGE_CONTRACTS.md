# Page Contracts — STAGE_6_FIELD_TRACKING

> الهدف: إعطاء المصمم/المطور واجهة تصميمية واضحة بدون تنفيذ UX الآن.

## 1) لوحة الميدان (Field Dashboard)
**Route (UI):** `/field`

**Data Sources (API):**
- `GET /api/field/reports/summary?from&to` (permission: `field:report:read`)
- `GET /api/field/task_runs?status=ACTIVE` (permission: `field:taskrun:read`)

**Widgets:**
- Today check-ins by kind (CHECKIN/CHECKOUT/PING/NOTE)
- Active task runs (who, task_id, started_at)
- Quick actions: Start task run, Log check-in

**Hard Guards:**
- Must show: org/branch/persona
- Hide widgets if permission not present

## 2) سجل check-ins
**Route:** `/field/checkins`

**Data Sources:**
- `GET /api/field/checkins?user_id&task_id&from&to&limit` (permission: `field:checkin:read`)
- optional: resolve `photo_document_id` via documents module when UX exists

**Columns:**
- occurred_at
- user
- kind
- task_id / project_id (if present)
- lat/lng (compact)
- note

**Actions:**
- View details (no edit in v1)

## 3) تشغيلات المهام (Task Runs)
**Route:** `/field/task-runs`

**Data Sources:**
- `GET /api/field/task_runs?task_id&project_id&user_id&from&to` (`field:taskrun:read`)
- `POST /api/field/task_runs/start` (`field:taskrun:create`)
- `POST /api/field/task_runs/end` (`field:taskrun:create`)

**Form Contracts:**
- Start: { task_id, project_id?, start_checkin_id?, started_at? }
- End: { id, end_checkin_id?, ended_at?, status? }

**Hard Guards:**
- No start/end without active persona
- Reason prompts are not required here (not approvals), لكن أي تغيير يسجل بالـ Audit عبر EventBus/ledger

## 4) الجيوفينس (Geofences)
**Route:** `/field/geofences`

**Data Sources:**
- `GET /api/field/geofences` (`field:geofence:read`)
- `POST /api/field/geofences` (`field:geofence:create`)
- `PATCH /api/field/geofences/:id` (`field:geofence:update`)
- `POST /api/field/geofences/:id/disable` (`field:geofence:disable`)

**Model:**
- name, center_lat, center_lng, radius_m, active, meta

**Hard Guards:**
- Disable requires reason
- Geofence enforcement is controlled by setting `field.geofence.enforce`
