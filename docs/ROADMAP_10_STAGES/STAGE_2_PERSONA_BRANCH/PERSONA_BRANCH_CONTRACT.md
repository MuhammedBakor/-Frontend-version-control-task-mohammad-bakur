# المرحلة 2 — عقد الصفة والفرع (Persona & Branch Contract)

هذه الوثيقة **ليست UX** ولا تصميم ألوان.
هي عقد تشغيل واضح يضمن أن أي واجهة مستقبلًا (مصمم/Frontend) لا تخلط بين:
**الصفة (Persona)** و **السياق (Org/Branch)**، وأن كل حركة تُنسب بشكل صحيح في الـ Audit.

---

## 1) المصطلحات

### Persona (الصفة)
هي **هوية تشغيلية** داخل النظام (مثال: موظف / مدير / مدير عام / محاسب / قانوني).
قد يملك المستخدم أكثر من Persona.

### Context (السياق)
هو **حدود التينانت**:

- `orgId` (الشركة/المنشأة)
- `branchId` (الفرع)

> قاعدة ذهبية: **أي طلب محمي (Protected)** يجب أن يعمل داخل (orgId + branchId + persona).

---

## 2) قواعد إلزامية (Non‑Negotiable)

### قاعدة 2.1 — منع أي إجراء بدون Persona
أي Route محمي بصلاحية (RBAC) **يجب أن يرفض** إذا كانت `persona` غير محددة.

**سلوك النظام:**
- إذا لم توجد persona فعالة → يرجع خطأ `CONTEXT_REQUIRED` مع إرشاد:
  `Switch persona via POST /api/auth/persona`.

### قاعدة 2.2 — منع أي إجراء بدون Org/Branch
أي Route محمي **يجب أن يرفض** إذا لم يوجد `orgId` أو `branchId`.

**سلوك النظام:**
- إذا لم يوجد سياق فعال → يرجع `CONTEXT_REQUIRED` مع إرشاد:
  `Switch context via POST /api/auth/context`.

### قاعدة 2.3 — إظهار الصفة والسياق دائمًا في الواجهة
حتى بدون UX الآن، هذا شرط تشغيلي يجب على المصمم الالتزام به لاحقًا:

في كل شاشة محمية يجب أن يظهر دائمًا:
- الشركة/الفرع النشط
- الصفة النشطة

### قاعدة 2.4 — تأكيد الصفة قبل “الأفعال الثقيلة”
الأفعال التي تنتج أثرًا رسميًا أو قد تسبب خلطًا يجب أن تتطلب **تأكيدًا**.

أمثلة:
- طباعة مستند رسمي
- توقيع/اعتماد نهائي
- إرسال خارجي (واتساب/إيميل) عندما يُفعّل لاحقًا

**العقد:** الواجهة ترسل Headers للتأكيد:
- `X-Confirm-Persona: <activePersona>`
- `X-Confirm-Branch: <activeBranchId>`

> الهدف: منع “كنت على صفة مدير عام وأنا أحسب نفسي موظف” قبل طباعة/اعتماد.

---

## 3) API Contracts (للمصمم/الـ Frontend)

### 3.1 قراءة الوضع الحالي
`GET /api/auth/me`

يرجع:
- `activePersona`
- `activeContext.orgId/branchId`
- قائمة `roles`

### 3.2 قراءة الخيارات المتاحة للمستخدم
`GET /api/auth/options`

يرجع:
- `roles` (Personas)
- `orgs`
- `branches`
- `active` الحالي

### 3.3 تغيير السياق (Org/Branch)
`POST /api/auth/context`

Body:
```json
{ "orgId": "...", "branchId": "..." }
```

### 3.4 تغيير الصفة (Persona)
`POST /api/auth/persona`

Body:
```json
{ "persona": "role_key" }
```

> ملاحظة: Persona (في الإصدار الحالي) مرتبطة بـ Roles (role_key).

---

## 4) أخطاء متوقعة يجب على الواجهة التعامل معها

### 4.1 CONTEXT_REQUIRED (سياق/صفة مفقودة)
سيظهر في حال:
- عدم تحديد org/branch
- أو عدم تحديد persona

سلوك الواجهة:
1) توقف الإجراء
2) اعرض شاشة “اختيار السياق/الصفة”
3) بعد الاختيار… أعد تنفيذ الإجراء إذا رغبت

### 4.2 PERMISSION_DENIED
سلوك الواجهة:
- اخفاء زر/عنصر من الأساس عند عدم وجود الصلاحية
- وإذا حدثت: اعرض “ليس لديك صلاحية”

---

## 5) تعليمات للمصمم (بدون UX)

### 5.1 شاشة اختيار الصفة/السياق
يجب أن تُبنى كعنصر أساسي في القشرة (Shell) وليس داخل كل صفحة.

متطلبات:
- لا تسمح بالدخول لأي صفحة محمية إذا `activePersona` أو `activeContext` غير مكتمل
- عند تعدد الأدوار: اجعل الاختيار صريح (لا تفترض)

### 5.2 شريط الحالة (Status Bar)
يجب أن يكون دائمًا موجودًا في أعلى الواجهة (أو مكان ثابت واضح) ويعرض:
- org + branch
- persona

### 5.3 التحويل (Switch)
عند تغيير persona أو context:
- اعمل `POST /api/auth/persona` أو `POST /api/auth/context`
- ثم اعمل Refresh لـ `GET /api/auth/me`

### 5.4 التأكيد قبل الطباعة/الاعتماد
قبل “Print/Sign/Send”:
- اعرض Confirm dialog
- ثم أرسل Headers:
  - `X-Confirm-Persona`
  - `X-Confirm-Branch`

---

## 6) ما تم تطبيقه في الكود (Stage‑2 Implementation Notes)

### 6.1 Persona gate داخل RBAC
تم إلزام وجود persona في `requirePermission()`.

### 6.2 Middleware تأكيد الصفة/الفرع
تم توفير Middleware جاهز للاستخدام لاحقًا:
`requirePersonaConfirmation()`

### 6.3 Endpoint خيارات المستخدم
تم إضافة:
`GET /api/auth/options`

---

## 7) اختبار يدوي سريع (Manual Sanity)

1) سجّل دخول
2) نادِ `GET /api/auth/me` وتأكد من:
   - `activePersona != null`
   - `orgId/branchId != null`
3) غيّر persona عبر `/api/auth/persona` ثم أعد `GET /api/auth/me`
4) جرّب Route محمي بدون persona (بتصفيرها يدويًا في session) → يجب يرجع `CONTEXT_REQUIRED`
