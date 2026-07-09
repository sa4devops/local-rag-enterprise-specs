# UI_SCREEN_BEHAVIOR_CARDS.md — بطاقات سلوك الشاشات

> **Version:** 1.0 — Proposed (v0.5) · **Date:** 2026-07-07 · **الموضع الهدف:** `ui/UI_SCREEN_BEHAVIOR_CARDS.md`
> **مبنيّ فوق:** UI_SCREEN_INVENTORY (v0.4، v1.1) · UI_INTERACTION_MODEL · UI_VISIBILITY_RULES · UI_PROGRESSIVE_DISCLOSURE · UI_COMPONENT_STATES (v0.5).
> **الغرض:** لكل شاشة رئيسية بطاقة قصيرة تُحوِّل قواعد v0.5 إلى **قرارات تصميم تشغيلية** — تُلصق مباشرة داخل prompt الشاشة في Stitch.
> **قواعد قراءة:** كل بطاقة تحوي 9 حقول ثابتة. الشاشات المذكورة هي الأولوية (23 شاشة بعد Δ v0.6)؛ البقية تُستكمل عند الحاجة بنفس القالب.

---

## Global Responsive Behavior Rule

Every screen behavior card must be interpreted as responsive by default.

For every screen, the implementation must define behavior for:

- desktop screens
- laptop screens
- tablet-width screens
- mobile-width screens

Each screen must specify or preserve:

- layout resizing
- navigation behavior
- sidebar behavior
- table overflow or table-to-card transformation
- form field wrapping
- modal/drawer behavior
- action button placement
- action-card behavior
- empty/loading/error state behavior
- RTL-safe behavior

No screen may rely on desktop-only layout assumptions.

If a screen contains dense enterprise data, the responsive design must preserve readability, auditability, and access to governed actions.


## 1) `ws.main` — AI Workspace
- **افتراضياً يظهر:** topbar · sidebar مصغّر · ws.thread (فارغة أولى: قدرات المستخدم) · ws.composer (نص + إرفاق + Scope selector chip واحد) · شارة «مُولَّد» جاهزة للتفعيل عند أول مخرَج نموذج.
- **مطويّ:** كل تبويبات context panel (رؤوس فقط) · شريط الجلسات (يُفتح بنقر) · panel.audit (رأسه مخفي كلياً لغير المخوّل).
- **حسب الصلاحية:** panel.audit (رأس + محتوى) للمخوّل بـ `audit.view` فقط · مصادر Scope selector مرشّحة · اقتراحات الأفعال في بطاقات تظهر فقط لما يملك المستخدم `permission` عليه (HIDDEN-SERVER لغيره).
- **drawer:** تفاصيل استشهاد (drawer end) · معاينة سجل مرتبط (drawer end) · تفاصيل تدقيق (drawer end للمخوّل) — **واحد في كل مرة**.
- **modal:** تأكيد typed/dual للأفعال high/critical فقط · معاينة HITL للأفعال act على موصلات (P7).
- **page:** «عرض الكل في القائمة» ⇒ `run.list` · «فتح النموذج الكامل» ⇒ `run.form` · «فتح كامل السجل» ⇒ `run.detail` · فتح شاشة إدارية من بطاقة ⇒ **تبويب متصفح جديد** لا يفقد الحوار.
- **متى إلى Renderer:** نتائج >10 صفوف؛ تحرير >7 حقول؛ عرض تفصيلي كامل؛ Entity Profile.
- **يجب أن يراه Stitch:** ثلاث زوايا محادثية (فارغة أولى، بث/نبض، وضع حتمي كامل) · storyboard S3→S9 لبطاقة فعل واحدة · بطاقتا الرفض (صلاحية / أدلة غير كافية) · panel.citations بحالتين (مطويّ/مفتوح) · شارة «مُولَّد» على كل مخرَج نموذج.
- **يجب ألا يراه Stitch:** فقاعات محادثة استهلاكية · أفاتار لعوبة · «مرحباً بك في المدينة الذكية» أو أي هوية موقع تخطيط حضري · شعارات لأنظمة حقيقية · panel.audit مفتوحاً كافتراضي · «كل الاستشهادات مفتوحة».
- **الحالات المطلوبة عرضها:** default(S1) · collapsed(S2) للجلسات · loading(S4) بث · empty(S5) فارغة أولى · error(S14) فشل نموذج · permission-denied(S7) رفض فعل · audit-visible(S15) للمخوّل.

---

## 2) `run.list` — Runtime Renderer قائمة
- **افتراضياً يظهر:** header بعنوان الكيان (وهمي) + زر إنشاء (إن مسموحاً) · شريط بحث سريع · 5–7 أعمدة · صف واحد مختار · شريط ترقيم أسفل.
- **مطويّ:** الفلاتر المتقدمة (drawer end عند النقر) · column picker · row actions إضافية تحت ⋯.
- **حسب الصلاحية:** أزرار الأفعال في header وrow ⇒ HIDDEN-SERVER لغير المخوّل · صفوف خارج نطاق RLS **لا تظهر ولا تُعدّ** · حقول FLS ⇒ خلايا مقنَّعة «•••».
- **drawer:** فتح صف ⇒ drawer end (معاينة قصيرة) · فلاتر متقدمة ⇒ drawer end.
- **modal:** تصدير محكوم (خطوة نطاق + خطوة تأكيد بوسم) — modal قصير ثم صفحة حالة.
- **page:** «فتح كامل» من drawer المعاينة ⇒ `run.detail` · التحرير ⇒ `run.form`.
- **متى إلى Renderer:** هذه الشاشة **هي** Renderer — منها تُغذّى `run.detail`/`run.form`.
- **يجب أن يراه Stitch:** الجدول بحالتين (بيانات/فارغ) · drawer معاينة صف مع 3 أفعال فقط في الرأس · خلية مقنَّعة واحدة على الأقل · صف بشارة workflow state (بانتظار اعتماد مثلاً).
- **يجب ألا يراه Stitch:** 15 عموداً معاً · كل الأفعال ظاهرة في كل صف · فلاتر متقدمة داخل الرأس مباشرة · إحصائيات BI مضافة.
- **الحالات المطلوبة:** default · loading (skeleton صفوف) · empty (إرشاد بلا مبالغة) · error · permission-denied (403 مفسَّرة) · masked (خلية) · audit-visible (زر «سلسلة تدقيق الصف» للمخوّل).

---

## 3) `run.form` — Runtime Renderer نموذج
- **افتراضياً يظهر:** شريط دورة الحياة أعلى (خارج التحرير — قراءة) · القسم الأساسي مفتوح فقط · ملخص أخطاء أعلى (فارغ عند البدء) · أزرار حفظ/إلغاء أسفل.
- **مطويّ:** بقية الأقسام بعدّاد حقول · حقول متقدمة داخل القسم الأساسي إن كثرت.
- **حسب الصلاحية:** حقول بعينها HIDDEN-SERVER · حقول بحالة workflow معيّنة ⇒ read-only بسبب.
- **drawer:** «معاينة السجل السابق (نسخة)» ⇒ drawer end · «تاريخ التعديلات» ⇒ drawer end للمخوّل.
- **modal:** حفظ لفعل high/critical ⇒ modal typed/dual · تحذير «حقول حساسة سيتم تخزينها» ⇒ modal قصير.
- **page:** بعد الحفظ الناجح ⇒ إعادة توجيه لـ `run.detail` أو `run.list`.
- **متى إلى Renderer:** هذه الشاشة **هي** Renderer.
- **يجب أن يراه Stitch:** ثلاثة أقسام (واحد مفتوح، اثنان مطويان بعدّاد) · حقل مقنَّع مسبقاً «•••» · حقل شرطي مخفي حتى يتحقق شرطه · ملخص أخطاء أعلى مع حقل خاطئ.
- **يجب ألا يراه Stitch:** كل الأقسام مفتوحة · نموذج بـ 40 حقلاً على شاشة واحدة · «حفظ ونشر ومشاركة» أزراراً معاً · builder-preview كأنه صانع شاشات للمستخدم.
- **الحالات المطلوبة:** default · loading · error (S6 ملخص+حقول) · disabled (بحالة workflow) · masked · confirmation · approval (النموذج ينتقل بانتظار الاعتماد) · success · failed.

---

## 4) `run.detail` — Runtime Renderer تفاصيل
- **افتراضياً يظهر:** شارة تصنيف + شارة workflow state + مرجع تدقيق (للمخوّل) · بيانات أساسية · **3 أزرار أفعال في الرأس** (بترتيب priority من Registry) · تبويب «تفاصيل» نشط.
- **مطويّ:** بقية الأزرار في «مزيد» ⋯ · تبويبات (سجل التغييرات، المرفقات، العلاقات) مطوية · panel.audit جانبي مطويّ للمخوّل.
- **حسب الصلاحية:** أزرار خارج الصلاحية HIDDEN-SERVER · حقول مقنَّعة · panel.audit للمخوّل فقط.
- **drawer:** «سلسلة تدقيق كاملة» ⇒ drawer end للمخوّل · «معاينة نسخة سابقة» ⇒ drawer end.
- **modal:** كل فعل typed/dual · تأكيد الحذف · «إعادة توجيه إلى مسار workflow آخر» إن مسموحاً.
- **page:** التحرير ⇒ `run.form` · Entity Profile ⇒ `profile.entity` إن كان الكيان يظهر في ملف.
- **متى إلى Renderer:** هذه الشاشة **هي** Renderer.
- **يجب أن يراه Stitch:** رأس بشارتين + 3 أزرار فقط + قائمة «مزيد» تحوي 4 أفعال إضافية معطلة أحدها بسبب workflow state · panel.audit جانبي بحالة مطويّ (يظهر للمخوّل بعنوان).
- **يجب ألا يراه Stitch:** 10 أزرار في الرأس · لوحة تدقيق مفتوحة افتراضياً · تنبيهات صحة النظام في التفاصيل · «تصدير PDF/Excel» ما لم يكن صلاحية.
- **الحالات المطلوبة:** default · loading · disabled (زر بحالة) · permission-denied (على مستوى الصفحة) · masked · confirmation · approval · success · failed · audit-visible.

---

## 5) `queue.tasks` — مهامي
- **افتراضياً يظهر:** فلتر «مسندة إليّ اليوم» مفعَّل · عمود الأولوية · قائمة مضغوطة · عدّاد في التبويب.
- **مطويّ:** فلاتر متقدمة (drawer end) · تفاصيل المهمة (drawer بنقر الصف).
- **حسب الصلاحية:** المهام مرشّحة بنطاق المستخدم · إجراءات المهمة حسب صاحبها/مسؤولها.
- **drawer:** تفاصيل مهمة ⇒ drawer end (وصف/مسؤول/استحقاق/زر إتمام).
- **modal:** «إعادة إسناد» ⇒ modal قصير.
- **page:** «فتح كامل» من drawer ⇒ لا صفحة مستقلة للمهمة الواحدة (السطح drawer كافٍ) — الاستثناء إن ربطت بمشروع ⇒ `projects.main`.
- **متى إلى Renderer:** «فتح السجل المرتبط» ⇒ `run.detail`.
- **يجب أن يراه Stitch:** قائمة بـ 6 مهام بشارات (متأخرة، اليوم، غداً، هذا الأسبوع) · drawer تفاصيل واحدة · حالة فارغة إرشادية (لا مهام).
- **يجب ألا يراه Stitch:** لوحة Kanban متعددة الأعمدة (Backlog) · تعليقات ضخمة داخل الصف · إحصائيات إنتاجية.
- **الحالات المطلوبة:** default · loading · empty · error · disabled (مهمة مغلقة) · success (إتمام) · failed.

---

## 6) `queue.approvals` — اعتماداتي
- **افتراضياً يظهر:** فلتر «بانتظار قراري» مفعَّل · عمود «مقدَّم من» · عمود «الأثر المختصر» · عمود «الاستحقاق».
- **مطويّ:** فلاتر متقدمة · تعليقات thread داخل الصفوف.
- **حسب الصلاحية:** بنود مرشّحة بأدوار المعتمِد + SoD (لا يظهر بند قدَّمه المستخدم نفسه للاعتماد الذاتي).
- **drawer:** N/A — تفاصيل البند تفتح **صفحة** (سطح رسمي).
- **modal:** N/A على مستوى القائمة.
- **page:** نقر البند ⇒ `queue.approval_detail`.
- **متى إلى Renderer:** لا — البند سطح رسمي مستقل.
- **يجب أن يراه Stitch:** جدول اعتمادات بـ 5 صفوف · لا يعرض القرار داخل الصف (لا زر موافقة سريع) — يجب فتح البند.
- **يجب ألا يراه Stitch:** «موافقة سريعة» في القائمة · تعليقات مفتوحة في الصف · إشعارات دفع.
- **الحالات المطلوبة:** default · loading · empty («لا اعتمادات بانتظارك») · error · permission-denied (لا يصلها غير المعتمِدين) · disabled (بند نُقض بعد فتحه).

---

## 7) `queue.approval_detail` — تفصيل بند اعتماد
- **افتراضياً يظهر:** ملخص البند + الأثر المعلن + مقدِّم البند + السياسة المعمول بها + شريط قرارات (موافقة/رفض/إرجاع) + thread أسفل.
- **مطويّ:** تفاصيل تقنية (payload كامل للأفعال) · مرفقات · تاريخ التعديلات.
- **حسب الصلاحية:** الأزرار معطَّلة إن كان الناظر هو المقدِّم (SoD) بسبب صريح · حقول payload حساسة مقنَّعة.
- **drawer:** «سياسة الاعتماد المفصَّلة» ⇒ drawer end (للمخوّل) · «تدقيق البند» ⇒ drawer end للمخوّل.
- **modal:** «رفض» بلا تعليق ⇒ رفض النموذج + تنبيه · «موافقة على فعل critical» ⇒ modal typed.
- **page:** بعد القرار ⇒ رجوع تلقائي إلى `queue.approvals` + تحديث الحالة.
- **متى إلى Renderer:** «فتح السجل موضع القرار» ⇒ `run.detail`.
- **يجب أن يراه Stitch:** ملخص + payload مقروء (بيانات وهمية عربية) + thread فيه رسالتان + شريط قرارات · حالة SoD-معطَّل مع سبب.
- **يجب ألا يراه Stitch:** «موافقة تلقائية»/«ذكاء اقتراح» · endpoints في payload · حالة «موافقة بلا معتمِد».
- **الحالات المطلوبة:** default · loading · error · disabled (SoD) · masked (payload) · confirmation (رفض بتعليق) · success (قرار) · failed (خطأ شبكة) · audit-visible.

---

## 8) `admin.dashboard` — لوحة الأدمن
- **افتراضياً يظهر:** ≤4 بلاطات: اعتمادات معلّقة · مهام معالجة فاشلة · ملخص صحة · آخر تغييرات سياسات · بحث موحّد أعلى.
- **مطويّ:** لا تفاصيل تشغيلية عميقة في الصفحة نفسها (كلها روابط إلى شاشات مختصة).
- **حسب الصلاحية:** بلاطات بعينها HIDDEN-SERVER لدور المستخدم الفعلي (Knowledge Admin لا يرى بلاطة سياسات).
- **drawer/modal/page:** كل بلاطة رابط ⇒ الصفحة المختصة (page).
- **متى إلى Renderer:** N/A.
- **يجب أن يراه Stitch:** 4 بلاطات بأرقام وهمية معتدلة + بحث + عنوان hi-level.
- **يجب ألا يراه Stitch:** رسوم بيانية BI · «Overview» شعارات · KPIs مالية · شعارات مدن.
- **الحالات المطلوبة:** default · loading (skeleton بلاطات) · empty (بلاطة بلا أرقام) · error (بلاطة تعذّر تحميلها).

---

## 9) `admin.users` — إدارة المستخدمين
- **افتراضياً يظهر:** جدول (اسم · وحدة · دور رئيسي · حالة · آخر دخول) + شريط بحث · زر «إضافة مستخدم».
- **مطويّ:** فلاتر متقدمة · أعمدة إضافية (تاريخ الإنشاء، أدوار ثانوية) في column picker.
- **حسب الصلاحية:** الشاشة لـ `admin.users.manage` فقط · صفوف خارج نطاق admin (وحدة معينة) لا تظهر.
- **drawer:** «معاينة سريعة» عند نقر الصف.
- **modal:** «إضافة/تعطيل/إعادة تعيين كلمة» ⇒ modal قصير typed للتعطيل.
- **page:** «فتح ملف المستخدم» ⇒ `admin.user_detail`.
- **متى إلى Renderer:** N/A (Console).
- **يجب أن يراه Stitch:** 6 صفوف مستخدمين بأسماء وهمية عربية + drawer معاينة + modal «تعطيل مستخدم» بـ typed.
- **يجب ألا يراه Stitch:** كلمات مرور فعلية · مفاتيح API · تخصيصات SSO في الجدول · تاريخ IPs.
- **الحالات المطلوبة:** default · loading · empty · error · disabled (زر تعطيل لمستخدم نظام) · confirmation · success · failed · audit-visible (زر «آخر تعديلات على هذا الحساب»).

---

## 10) `admin.permissions` — مصفوفة الصلاحيات
- **افتراضياً يظهر:** مصفوفة (أدوار × موارد) مضغوطة بـ 6–8 أدوار × 8 صلاحيات ظاهرة + مفتاح ✔/✖.
- **مطويّ:** مصادر إضافية (dropdown)؛ حقول ABAC/ReBAC (شاشة `admin.policies` منفصلة).
- **حسب الصلاحية:** الشاشة لـ `admin.permissions.manage`.
- **drawer:** «تفصيل قرار خلية» (توضيح لماذا سُمح/مُنع) ⇒ drawer end للمخوّل.
- **modal:** «تغيير» ⇒ modal مصغّر بتأكيد.
- **page:** «Policy Studio» رابط منفصل ⇒ `admin.policies`.
- **متى إلى Renderer:** N/A.
- **يجب أن يراه Stitch:** مصفوفة نظيفة بألوان دقيقة (✔ رمادي داكن، ✖ فاتح) · drawer تفصيل قرار خلية · مفتاح واضح.
- **يجب ألا يراه Stitch:** مصفوفة بـ 30 عموداً معاً · «كل صلاحيات كل الأدوار في شاشة واحدة» · شعار مؤسسة أمنية.
- **الحالات المطلوبة:** default · loading · empty · error · confirmation · success · failed · audit-visible.

---

## 11) `admin.record_types` — Screen/Record-Type Builder
- **افتراضياً يظهر:** قائمة الأنواع (اسم · حالة دورة الحياة · النسخة) + زر «تعريف جديد».
- **مطويّ:** Builder نفسه صفحة مستقلة عند فتح تعريف.
- **حسب الصلاحية:** الشاشة لـ `admin.metadata.manage` · محاكاة «مَن سيرى؟» لمخوّلي admin.policies.
- **drawer:** diff بين نسختين (drawer end) · محاكاة (drawer end).
- **modal:** «اعتماد النسخة» ⇒ modal typed بشخص مختلف (SoD ظاهر).
- **page:** «فتح Builder» ⇒ صفحة Builder بشريط دورة حياة + tabs (الحقول · السياسات · التنقّل · التوثيق).
- **متى إلى Renderer:** N/A مباشرةً؛ التعريف يولّد شاشات Renderer.
- **يجب أن يراه Stitch:** قائمة أنواع وهمية بعناوين عربية · Builder بشريط حالة واحد نشط · tab «الحقول» مفتوحاً · حقلين وهميين فقط.
- **يجب ألا يراه Stitch:** كتلة WYSIWYG بصرية «drag &amp; drop» كأنها low-code استهلاكي · شعار Builder تجاري.
- **الحالات المطلوبة:** default · loading · empty · error (Validation فاشل بدورات) · disabled (تفعيل قبل اعتماد) · confirmation (اعتماد) · approval (بانتظار المعتمِد) · success · failed · audit-visible (drawer «سلسلة تعريف»).

---

## 12) `admin.actions` — Action Registry
- **افتراضياً يظهر:** قائمة الأفعال (action_id · label · risk · حالة) + فلتر target/entity + زر «تعريف فعل جديد».
- **مطويّ:** محرر عقد الفعل صفحة مستقلة عند فتح.
- **حسب الصلاحية:** الشاشة لـ `admin.actions.manage`.
- **drawer:** «مَن سيرى هذا الزر؟» simulation ⇒ drawer end.
- **modal:** «اعتماد الفعل» ⇒ modal typed.
- **page:** «فتح محرر العقد» ⇒ صفحة مستقلة بحقول العقد الـ13.
- **متى إلى Renderer:** N/A مباشرةً؛ العقد يظهر أزراراً في Renderer وبطاقات في ws.
- **يجب أن يراه Stitch:** قائمة بـ 8 أفعال بأمثلة (record.create · workflow.approve · migration.approve · connector.tool.act …) · محرر عقد لفعل واحد بحقوله الرئيسية (تبويبات: تعريف · صلاحية · تحقق · مخاطر/تأكيد · أثر · تدقيق).
- **يجب ألا يراه Stitch:** محرر تعبيرات كود · scripting IDE داخلي · «سحب-إفلات» للأثر (الأثر معلن من كتالوج).
- **الحالات المطلوبة:** default · loading · empty · error · disabled (تفعيل قبل اعتماد) · confirmation · approval · success · failed · audit-visible.

---

## 13) `admin.workflows` — تعريفات الـ Workflows
- **افتراضياً يظهر:** قائمة الـ workflows (اسم · كيان · حالة · نسخة) + زر «تعريف جديد».
- **مطويّ:** التعريف التفصيلي صفحة `admin.workflow_detail`.
- **حسب الصلاحية:** الشاشة لـ `admin.workflows.manage`؛ الاعتماد لـ `wf.approve` (SoD).
- **drawer:** «Validation report» (دورات، حالات ميتة) ⇒ drawer end · «diff نُسخ» ⇒ drawer end.
- **modal:** «اعتماد» ⇒ modal typed · «تفعيل» ⇒ modal typed للـ instances الجارية (grandfathering).
- **page:** فتح workflow ⇒ `admin.workflow_detail` (جدول حالات/انتقالات + مصفوفة اعتماد).
- **متى إلى Renderer:** N/A مباشرةً؛ الـ workflow يعمل على سجلات Renderer.
- **يجب أن يراه Stitch:** جدول workflows وهمية + تفصيل واحد بجدول حالات/انتقالات مُهيكل (بلا رسم canvas في v1) + شريط دورة حياة + tab «مصفوفة الاعتماد».
- **يجب ألا يراه Stitch:** canvas مرئي معقد بـ nodes وwires (مؤجَّل — OD-P3-2) · شعار BPM تجاري.
- **الحالات المطلوبة:** default · loading · empty · error (دورة مكتشفة) · disabled (تفعيل قبل اعتماد) · confirmation · approval · success · failed · audit-visible.

---

## 14) `admin.rag_sources` — مصادر المعرفة
- **افتراضياً يظهر:** قائمة المصادر (اسم · نوع · نطاق=وسم صلاحية · حالة · آخر فهرسة).
- **مطويّ:** تفاصيل المصدر · إعدادات chunking (drawer).
- **حسب الصلاحية:** الشاشة لـ `admin.knowledge.manage`.
- **drawer:** تفاصيل المصدر (drawer end) · «إعادة فهرسة» (drawer end بتأكيد).
- **modal:** حذف مصدر ⇒ modal typed high.
- **page:** «مراقبة الخط» ⇒ `admin.ingestion`.
- **متى إلى Renderer:** N/A.
- **يجب أن يراه Stitch:** 5 مصادر وهمية بأسماء عربية (مجلد سياسات، قاعدة عقود …) + drawer تفاصيل مصدر + مؤشر «آخر فهرسة».
- **يجب ألا يراه Stitch:** روابط URLs خارجية · مفاتيح API لمصادر · شعار خدمات cloud.
- **الحالات المطلوبة:** default · loading · empty · error · disabled (Safe Mode) · confirmation (حذف) · success · failed · audit-visible.

---

## 15) `admin.retrieval_tester` — مختبر الاسترجاع
- **افتراضياً يظهر:** حقل استعلام + مبدّل نطاق (المُجرِّب) + زر «تشغيل» + منطقة نتائج فارغة.
- **مطويّ:** إعدادات متقدمة (top-k، عتبة الكفاية) في drawer end.
- **حسب الصلاحية:** الشاشة لـ `admin.knowledge.manage` — النتائج ضمن صلاحيات المُجرِّب نفسه.
- **drawer:** تفصيل نتيجة (provenance مفصَّل، chunk نصي) ⇒ drawer end · إعدادات متقدمة (drawer end).
- **modal:** N/A.
- **page:** «تغيير ربط النموذج» ⇒ `admin.capabilities`.
- **متى إلى Renderer:** N/A.
- **يجب أن يراه Stitch:** استعلام تجريبي عربي وهمي + 5 نتائج بمحددات (صفحة/فقرة) + **لافتة قرار الكفاية** (كافٍ أخضر / غير كافٍ أصفر) بارزة أعلى النتائج + شارة «أدمن — داخل صلاحيتك».
- **يجب ألا يراه Stitch:** إجابة نموذج كاملة (هذه شاشة استرجاع لا إجابة) · مشاركة اجتماعية · «قيّم الجودة».
- **الحالات المطلوبة:** default (قبل التشغيل) · loading · empty (لا نتائج) · error · masked (مقتطف حساس) · success (كفاية) · failed (لا كفاية) · audit-visible.

---

## 16) `admin.capabilities` — ربط القدرات
- **افتراضياً يظهر:** جدول (capability · provider ref · model ref · fallback · حالة · آخر تعديل) + زر «اختبار الاتصال» لكل صف.
- **مطويّ:** خطة إعادة الفهرسة عند تغيير embedding (drawer عند التعديل).
- **حسب الصلاحية:** الشاشة لـ `admin.models.manage`؛ الاعتماد للإنتاج حسب سياسة.
- **drawer:** «خطة إعادة فهرسة» ⇒ drawer end قبل تأكيد · «تفصيل الربط» ⇒ drawer end.
- **modal:** «تغيير الربط» في الإنتاج ⇒ modal typed + شارة «يتطلب اعتماداً».
- **page:** «ربط الوكلاء» ⇒ `admin.agents`.
- **متى إلى Renderer:** N/A.
- **يجب أن يراه Stitch:** جدول بـ 6 قدرات (embedding · reranker · ocr · asr · vision-caption · chat) + chip حالة + chip اختبار اتصال (نجاح/فشل — بلا endpoint) + شارة «يتطلب اعتماداً في الإنتاج» على صف embedding.
- **يجب ألا يراه Stitch:** endpoints أو URLs أو مفاتيح · شعار مزوّدي نماذج · GPU/replicas · «إحصاءات استخدام».
- **الحالات المطلوبة:** default · loading · empty · error (فشل اتصال — رسالة عامة) · disabled (Safe Mode) · confirmation · approval (بيئة إنتاج) · success · failed · audit-visible.

---

## 17) `admin.connectors` — إدارة الموصلات
- **افتراضياً يظهر:** قائمة الموصلات (اسم وهمي · نوع · الأدوات · مستوى الخطورة · الجمهور · صحة).
- **مطويّ:** تفاصيل الموصل والأدوات (drawer).
- **حسب الصلاحية:** الشاشة لـ `admin.integrations.manage`.
- **drawer:** «تفاصيل الموصل + أدواته» ⇒ drawer end · «سياسة HITL لكل أداة» ⇒ داخل drawer.
- **modal:** «تفعيل/تعطيل» ⇒ modal typed مع تحذير الجمهور المتأثر.
- **page:** «متجر المستخدم» عرض للقراءة ⇒ `store.catalog`.
- **متى إلى Renderer:** N/A.
- **يجب أن يراه Stitch:** 4 موصلات وهمية بأدوات (كل موصل 3–5 أدوات) + شارات read/act + شارة صحة (خضراء/حمراء) + لا-أسرار في drawer.
- **يجب ألا يراه Stitch:** أسرار/tokens/endpoints · شعارات منتجات حقيقية (Jira, Slack …) · «سجل تنفيذ حي» في القائمة.
- **الحالات المطلوبة:** default · loading · empty · error (فشل صحة) · disabled (Safe Mode) · confirmation (تعطيل جمهور واسع) · success · failed · audit-visible.

---

## 18) `admin.audit` — عارض التدقيق
- **افتراضياً يظهر:** فلاتر أساسية (فاعل · فعل · تاريخ) + قائمة أحدث 50 حدثاً + شريط «ضمن نطاقك».
- **مطويّ:** فلاتر متقدمة (correlation_id · request_id · صنف حدث) في drawer end.
- **حسب الصلاحية:** الشاشة لـ `audit.view` — النتائج مرشّحة بنطاق الناظر · بند «خارج نطاقك: N» يظهر (استثناء OD-VZ-3).
- **drawer:** تفصيل الحدث + سلسلة correlation ⇒ drawer end.
- **modal:** «تصدير» ⇒ modal قصير بنطاق + تأكيد.
- **page:** حالة التصدير ⇒ صفحة حالة/تحميل.
- **متى إلى Renderer:** «فتح السجل المتأثر» ⇒ `run.detail`.
- **يجب أن يراه Stitch:** جدول 12 حدثاً عربياً · drawer تفصيل حدث بسلسلة تُظهر (proposal → validated → authorized → executed) + before/after لحقلين · فلاتر أساسية بارزة.
- **يجب ألا يراه Stitch:** SIEM بصري · رسوم بيانية للأحداث · «كشف تهديدات» · alertاً استهلاكياً.
- **الحالات المطلوبة:** default · loading · empty · error · permission-denied (على الصفحة كلها) · masked (payload حساس) · success (تصدير) · failed · audit-visible (كل صف يكشف سلسلته).

---

## 19) `admin.health` — الصحة التفصيلية
- **افتراضياً يظهر:** بلاطات لكل تبعية (اسم · حالة · آخر فحص) — المعطَّلة تظهر بلون رمادي وعلامة «disabled» صريحة.
- **مطويّ:** تفاصيل التبعية الواحدة (inline expand).
- **حسب الصلاحية:** الشاشة لـ Ops/admin مخوّل.
- **drawer:** «تاريخ الحالة» ⇒ drawer end.
- **modal:** N/A (لا أزرار lifecycle — D9).
- **page:** رابط إلى «كتالوج الأخطاء».
- **متى إلى Renderer:** N/A.
- **يجب أن يراه Stitch:** 8 بلاطات (PostgreSQL · Qdrant · OpenSearch · LLM Gateway · Ingestion Worker · Object Storage · MetricsExporter · Providers Router) — بعضها فعّال وبعضها disabled صراحة · بلاطة واحدة بحالة فشل + رسالة قصيرة.
- **يجب ألا يراه Stitch:** أزرار «إعادة تشغيل» أو «تحديث نسخة» · «uptime %» مبالغ فيه · شعار موفري cloud.
- **الحالات المطلوبة:** default · loading · error (تبعية فاشلة) · disabled (تبعية مطفأة بعلَم) · audit-visible (تاريخ الحالة للمخوّل).

---

## 20) `projects.main` — المشاريع (حاوية سياق وصلاحية) — (Δ v0.6)
- **افتراضياً يظهر:** رأس المشروع (الاسم/الوصف/عدّاد الأعضاء/شارة تصنيف أقصى) + شريط تبويبات (نظرة عامة · المحادثات · الملفات · المهام والاعتمادات · التقارير · الإعدادات) — «نظرة عامة» نشط بعدّادات وآخر نشاط + زر **«فتح في الـ Workspace»**.
- **مطويّ:** بقية التبويبات؛ تفاصيل السياسات داخل «الإعدادات».
- **حسب الصلاحية:** العضوية شرط الرؤية أصلاً (غير العضو: HIDDEN/403)؛ تبويب الإعدادات لمدير المشروع؛ محتوى كل تبويب مرشَّح بصلاحيات عناصره (ملف بتصنيف أعلى لا يظهر لعضو أدنى).
- **drawer:** إضافة/تفاصيل عضو · معاينة عنصر (ملف/مهمة).
- **modal:** أرشفة المشروع (typed).
- **page:** فتح محادثة ⇒ ws.main بجلسة مروَّسة بسياق المشروع (نطاق المعرفة الافتراضي + Model Profile الافتراضي من إعدادات المشروع) · سجل ⇒ run.detail · تقرير ⇒ reports.review · تشغيل ⇒ runs.detail.
- **متى إلى Renderer:** عناصر التبويبات تفتح أسطحها الأصلية دائماً — المشروع لا يعرض بديلاً موازياً.
- **يجب أن يراه Stitch:** الرأس + 6 تبويبات (واحد نشط) + تبويب «الإعدادات» يعرض: نطاق معرفة افتراضي · Model Profile افتراضي · قائمة Profiles المسموحة (أسماء وهمية) + زر «فتح في الـ Workspace».
- **يجب ألا يراه Stitch:** kanban ضخم · إحصاءات BI · «مشاركة عامة/رابط عام» · شعارات · أي إيحاء بأن المشروع «ذاكرة ذكاء» (هو حاوية حوكمة).
- **الحالات المطلوبة:** default · loading · empty (مشروع جديد بإرشاد) · error · permission-denied · audit-visible (سجل نشاط المشروع للمخوّل).

---

## 21) `reports.review` — مراجعة التقرير (اعتماد المحتوى) — (Δ v0.6)
- **افتراضياً يظهر:** ترويسة (القالب/النسخة/الحالة/شارة تصنيف) + قائمة الأقسام (start) + القسم المحدد بمحتواه **بشارة «مُولَّد»** واستشهاداته المرقّمة + شريط قرار المراجعة (اعتماد · إرجاع قسم للتوليد · رفض).
- **مطويّ:** تعليقات المراجعة لكل قسم (inline expand) · تاريخ النسخ (drawer).
- **حسب الصلاحية:** القرار لـ reports.review؛ قسم مصادره خارج نطاق الناظر ⇒ محتواه محجوب بعلامة «محتوى مقيّد».
- **drawer:** استشهادات القسم التفصيلية · ملخص التشغيل («عرض التشغيل» المختصر).
- **modal:** الاعتماد النهائي (typed) · اعتماد تقرير **جزئي** مع placeholder ⇒ **typed-ack** (OD-RUN-2).
- **page:** «عرض التشغيل الكامل» ⇒ runs.detail · بعد الاعتماد ⇒ نسخة نهائية للقراءة.
- **متى إلى Renderer:** فتح سجلات مصدر الاستشهاد ⇒ run.detail/profile.entity.
- **يجب أن يراه Stitch:** قسم مكتمل (مُولَّد + استشهادات + حقل تعليق) وقسم placeholder «قسم لم يُولَّد (سبب)» وشريط القرار وحالة typed-ack للجزئي.
- **يجب ألا يراه Stitch:** تحرير حر للنص المولَّد بلا أثر نسخة · تصدير بلا وسم · مشاركة خارجية · «إعادة توليد» بلا سبب مسجَّل.
- **الحالات المطلوبة:** default · loading · empty (بانتظار التوليد) · error · disabled (القرار لغير المخوّل/SoD) · approval · success · failed · audit-visible.

---

## 22) `admin.agents` — ربط الوكلاء (per-agent) — (Δ v0.6)
- **افتراضياً يظهر:** جدول الوكلاء الأربعة (chat/reasoning · report · sql-agent · validation): النموذج الحالي · fallback · آخر تعديل (مَن/متى) · شارة «يتطلب اعتماداً في الإنتاج».
- **مطويّ:** معاملات كل وكيل (تُفتح في drawer التحرير).
- **حسب الصلاحية:** admin.models.manage؛ العرض admin.models.view.
- **drawer:** تحرير ربط وكيل (معاملات ضمن حدود config) + «أثر التغيير».
- **modal:** تأكيد **typed** للحفظ في الإنتاج.
- **page:** رجوع إلى مصفوفة Routing في admin.capabilities (المصدر الموحّد).
- **متى إلى Renderer:** N/A (Console).
- **يجب أن يراه Stitch:** 4 وكلاء بأسمائهم الوظيفية فقط + drawer تحرير واحد مفتوح + شارة اعتماد-الإنتاج + حالة فشل حفظ برسالة مفسَّرة.
- **يجب ألا يراه Stitch:** أسماء/شعارات نماذج تجارية كعلامات · endpoints · معاملات GPU · «إحصاءات استهلاك».
- **الحالات المطلوبة:** default · loading · empty · error · disabled (Safe Mode) · confirmation · approval · success · failed · audit-visible.

---

## 23) `runs.detail` — تفصيل التشغيل (المرجع الكامل: UI_RUN_EXECUTION_MODEL) — (Δ v0.6)
- **افتراضياً يظهر:** الرأس (≤3 أزرار سياقية: إلغاء أثناء التشغيل / إعادة عند الفشل) + **الخط الزمني** (خطوات L0) + لوحة المخرجات بتبويبات مطوية.
- **مطويّ:** تبويبا الاستشهادات والتدقيق · تفاصيل كل خطوة (Step Drawer) · السجل المُهيكل.
- **حسب الصلاحية:** تبويب التدقيق **بلا رأس** لغير audit.view؛ كل رابط دليل يعيد فحص صلاحية الناظر على العنصر (لا توسيع وصول).
- **drawer:** Step Drawer · diff المقارنة (version.compare) · فلاتر السجل المُهيكل.
- **modal:** إلغاء (typed) · إعادة عند أثر act خارجي (typed).
- **page:** هذه الشاشة page · «فتح البند» ⇒ queue.approval_detail (**القرار هناك حصراً**) · «فتح في التدقيق» ⇒ admin.audit بفلتر correlation.
- **متى إلى Renderer:** فتح مخرَج (سجل ⇒ run.detail · تقرير ⇒ reports.review · ملف ⇒ إدارة الملفات).
- **يجب أن يراه Stitch:** فرعان متوازيان بعقدة دمج · عقدة بوابة paused برابط البند · Step Drawer بمدخل مقنَّع · Tool Call Row بحالة «مخرَج كبير — ملف» · حالة partial بملخصها · modal الإلغاء.
- **يجب ألا يراه Stitch:** **أي console/terminal/سطر أوامر** · صياغات أمنية (فحص/ثغرات/هدف) · خرائط attack-surface · progress استعراضي.
- **الحالات المطلوبة:** حالات الـ run (§2 من المواصفة) + حالات الخطوة (§6).

---

## قواعد عامة لـ Stitch (تُلصق أسفل كل بطاقة عند التوليد)
1. **بيانات وهمية عربية مؤسسية** فقط — لا أسماء منتجات ولا شعارات ولا أسماء جهات حقيقية.
2. **الافتراضي مطويّ:** ما ليس ضرورياً للقرار الرئيسي على هذه الشاشة يبدأ مطوياً أو يُنقل لسطح آخر.
3. **الحالات الست الحرجة كحد أدنى:** default · loading · empty · error · permission-denied · disabled (حيث تنطبق).
4. **لا تكرار محتوى بين page/drawer/modal لنفس الغرض** — سطح واحد لكل غرض.
5. **الهوية مقفلة:** «Governed Enterprise AI Command Center» حكومي/رسمي — **ليس** تخطيطاً حضرياً، ليس صفحة تسويقية، ليس SaaS استهلاكياً، ليس chatbot استهلاكياً، ليس low-code builder للمستخدم النهائي.
6. **مخرجات Stitch مرجع بصري فقط** — لا كودها يدخل ريبو التنفيذ.
