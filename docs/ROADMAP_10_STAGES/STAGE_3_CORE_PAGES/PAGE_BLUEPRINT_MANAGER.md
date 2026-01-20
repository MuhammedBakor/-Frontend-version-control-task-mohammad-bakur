# Blueprint — لوحة المدير (Manager Home)

## الهدف
واجهة المدير تركّز على:
- Inbox الاعتمادات/المراجعات
- SLA/التأخير
- أداء الفريق

## شروط الدخول
- Authenticated
- Context: orgId + branchId + persona in (manager, hr_manager, dept_head)

## مناطق الصفحة (Layout zones)
1. **شريط علوي ثابت** (مثل لوحة الموظف)
2. **مؤشرات سريعة (KPIs)**
   - طلبات جديدة اليوم
   - طلبات متأخرة SLA
   - مهام متأخرة
3. **صندوق: صندوق الوارد للموافقة**
   - قائمة قصيرة + زر "عرض الكل"
4. **صندوق: تقدم المشاريع**
   - مشاريع نشطة + نسبة إنجاز
5. **صندوق: التنبيهات**

## مصادر البيانات (Endpoints)
- `GET /api/auth/options` (لإظهار الصفة/الفرع)
- `GET /api/registry/nav` (القائمة)
- `GET /api/notify/inbox` (إن وُجد)
- `GET /api/requests?scope=team&status=pending_approval`
- `GET /api/projects?scope=branch&status=active`
- `GET /api/reports/sla_summary?scope=branch`

## إجراءات حساسة تتطلب تأكيد Persona/Branch
- اعتماد/رفض أي طلب مالي/موارد بشرية/قانوني.
- طباعة خطاب/محضر/قرار.

الواجهة يجب أن ترسل Headers التأكيد (مرحلة 2):
- `X-Confirm-Persona: <activePersona>`
- `X-Confirm-Branch: <activeBranchId>`

## أخطاء متوقعة
- `CONTEXT_REQUIRED`: توجيه لاختيار الصفة/الفرع.
- `FORBIDDEN`: إخفاء الصندوق بالكامل أو رسالة صلاحيات.
