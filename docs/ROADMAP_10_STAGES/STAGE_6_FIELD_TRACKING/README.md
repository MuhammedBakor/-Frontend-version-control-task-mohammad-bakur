# STAGE_6_FIELD_TRACKING

هذه المرحلة تضيف "التتبع الميداني" بشكل **Task-based** (دليل مرتبط بمهمة) بدون UX.

## ما تم تنفيذه في الكود
- Module: `field` داخل `ghaith-api/modules/field`
- APIs:
  - Geofences: `/api/field/geofences` (CRUD + disable)
  - Check-ins: `/api/field/checkins`
  - Task Runs: `/api/field/task_runs/*`
  - Reports: `/api/field/reports/summary`
- Events: `field.*`
- Settings / FeatureFlag gate

## مستندات المصمم (No UX)
- `PAGE_CONTRACTS.md`
- `DESIGNER_NOTES.md`
- `DATA_MODEL.md`
- `PRIVACY_AND_GOVERNANCE.md`
