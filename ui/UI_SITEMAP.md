# UI_SITEMAP.md — خريطة أسطح الواجهة

> **Version:** 1.0 — Proposed · **Date:** 2026-07-06 · **الموضع الهدف:** `ui/UI_SITEMAP.md`
> **مفتاح السمات لكل قسم:** UF = user-facing · AD = admin-only · OP = operational · CFG = configuration · ST = يحتاج تصميم Stitch مستقل (رقم المجموعة G — تُفصَّل الـ prompts في `UI_STITCH_PROMPTS_BY_PHASE.md`) · WS = يمكن أن يظهر كسطح داخل AI Workspace بدل صفحة مستقلة.
> **مبدأ حاكم (Dual-Surface):** عمليات السجلات (إنشاء/تعديل/بحث/حذف…) **ليست صفحات لكل نوع** — سطحها الحتمي هو Runtime Renderer الموحّد، وسطحها المحادثي Action Cards داخل الـ Workspace، وكلاهما يستدعي نفس `action_id`.

## نظرة شجرية مختصرة
- **/login** → Auth
- **/workspace** → AI Workspace (P6، الرئيسية الافتراضية بعدها)
- **/me/** → Work Queue: tasks · approvals · notifications · reports · connections (الرئيسية قبل P6)
- **/me/runs** → تشغيلاتي (P6+، يمتد P7): قائمة وتفصيل التشغيلات المحكومة — سمة UF، مراقبة فقط، Dual ✖ (Δ v0.6)
- **/projects** → المشاريع
- **/app/{entity}** → Runtime Renderer (list/form/detail لأي كيان مولّد)
- **/entity/{key}** → Entity Profile
- **/store** → App Store (P7)
- **/reports/{id}/review** → مراجعة التقارير الرسمية (P6)
- **/admin/** → Admin Console (الأقسام 8–15 أدناه)
- **/ops · /about** → تشغيل وقراءة (P8)

## 1) Public / Auth — UF ✔ · AD ✖ · OP ✖ · CFG ✖ · ST: G2 · WS: لا (يسبق الجلسة)
`auth.login` (+حالات: خطأ اعتماد، حساب مقفل، جلسة منتهية — **حالات ضمن الشاشة لا صفحات**) · `auth.first_login` (تغيير كلمة أول دخول). لا استعادة ذاتية عبر بريد في المسار الأول (بيئة مغلقة — إعادة التعيين إدارية).

## 2) User AI Workspace (P6) — UF ✔ · ST: G3 (الصدفة) + G4 (البطاقات/النتائج) · WS: هو الحاوية
صفحة واحدة `ws.main` بمكوّنات (وليست صفحات): منطقة المحادثة · شريط الجلسات · **Context/Scope selector** (نطاق المعرفة: إدارتي/مصادر محددة — ضمن الصلاحية فقط) · Action Cards (معاينة→تأكيد) · **Citations panel** · السجلات المرتبطة · مرفقات ورفع ملف · انطلاق تقرير · إنشاء مهمة/طلب اعتماد · **SQL answer panel** (الاستعلام ظاهر) · حالات أولى مصممة: رفض صلاحية / معلومات غير كافية (No-Guessing) / خطأ منفّذ · **Audit-trace side panel** (بصلاحية العرض فقط).

## 3) User Work Queue (P3) — UF ✔ · ST: G8 · WS: تندمج كتبويبات/لوحات داخل ws من P6 وتبقى صفحاتها قائمة
`queue.tasks` · `queue.approvals` · `notif.center` · `projects.main`. هذه **رئيسية المستخدم قبل P6** (A-UX-5).

## 4) Tasks / Approvals (تفاصيل القرار) — UF ✔ · ST: ضمن G8 · WS: بطاقة مختصرة تفتح التفصيل
`queue.approval_detail` صفحة **رسمية** (قرار مدقَّق + thread النقاش) — لا تُختزل داخل الدردشة لأن القرار الرسمي يحتاج سطحاً ثابتاً قابلاً للمراجعة. تفاصيل المهمة = درج داخل `queue.tasks` (ليست صفحة).

## 5) Reports — UF ✔ · ST: ضمن G4 (بطاقات التوليد) + شاشة مراجعة ضمن G8-رسمي · WS: التوليد يبدأ من ws
`reports.list` (تقاريري وحالاتها) · `reports.review` (مراجعة قسمية بالاستشهادات + اعتماد/إرجاع — **صفحة مستقلة رسمية**). لا صفحة «إنشاء تقرير» — الإنشاء Action Card.

## 6) Notifications — UF ✔ · ST: ضمن G8 · WS: جرس + لوحة داخل ws
`notif.center` (+thread لكل بند داخل اللوحة). التفضيلات قسم داخل المركز لا صفحة.

## 7) Business Runtime Surfaces (السطح الحتمي) — UF ✔ · ST: **G13 قوالب فقط** (list/form/detail/profile) · WS: تُفتح كوجهات من البطاقات
`run.list` /app/{entity} · `run.form` (new/edit) · `run.detail` (+لوحة audit جانبية بصلاحية) · `profile.entity`. **قالب واحد لكل نمط يلبس كل الكيانات** — لا تصميم لكل نوع سجل (A-UX-3). كل زر فيها من Action Registry نفسه.

## 8) Admin Console Shell — AD ✔ · CFG · ST: G5 · WS: لا
`admin.dashboard` + التنقّل الصلاحي + بحث إداري موحّد. أقسام 9–15 تعيش داخله.

## 9) Security &amp; Access — AD ✔ · CFG · ST: G6 · WS: لا
`admin.users` · `admin.user_detail` · `admin.org` · `admin.roles` · `admin.permissions` (المصفوفة الأساسية P1) · `admin.policies` (ABAC/ReBAC/SoD Studio — P4) · `admin.classification` (P4) · `admin.security_policies` (جلسات/قفل/تصدير — P4) · `admin.features` (Feature Mgmt + مدخل Safe Mode المحمي — P4).

## 10) Record / Metadata / Action Configuration — AD ✔ · CFG · ST: G7 · WS: لا
`admin.record_types` (Screen/Record-Type Builder — P1→P2) · `admin.fields` (**تبويب داخل الـ Builder** لا صفحة مستقلة) · `admin.actions` (Action Registry — P3) · `admin.navigation` (P1) · `admin.migrations` (**Migration Review/الاعتماد** — P1، شاشة حرجة) · `admin.generation_docs` (توثيق التوليد — P2).

## 11) Workflow Configuration — AD ✔ · CFG · ST: G8-admin · WS: لا
`admin.workflows` (القائمة+دورة الحياة) · `admin.workflow_detail` (التعريف/الحالات/الانتقالات + الاعتماد قبل التفعيل). مصفوفة الاعتماد الافتراضية = تبويب إعدادات هنا (OD-P3-1).

## 12) RAG / Knowledge Admin (P5) — AD ✔ · CFG+OP · ST: G9 · WS: لا
`admin.rag_sources` · `admin.ingestion` (مراقبة/إعادة معالجة) · `admin.okf` · `files.manager` (إدارة الملفات وتصنيفها — إدارية؛ رفع المستخدم يتم من ws/renderer).

## 13) Provider &amp; Model Admin — AD ✔ · CFG · ST: G10 · WS: لا
`admin.capabilities` (capability→provider/model + fallback — P5) · `admin.agents` (per-agent bindings — P6). **حدود D9:** لا endpoints/secrets/GPU هنا إطلاقاً.

## 14) Integrations / App Store — مزدوج · ST: G11 · WS: بطاقات استدعاء داخل ws
User-facing (P7): `store.catalog` · `store.connections` (ربط/إلغاء حساباتي). Admin: `admin.connectors` (تعريف/تفعيل/جمهور — بلا أسرار) · بوابة HITL للمعاينة/الموافقة تظهر **كسطح داخل ws وqueue.approvals** لا كصفحة مستقلة.

## 15) Audit &amp; Operations — AD/OP قراءة · ST: G12 · WS: لا
`admin.audit` (P1) · `admin.logs` (P1، بقناع) · `admin.health` (P0/P1) · `admin.error_catalog` (P1) · `admin.config_profiles` (**قراءة فقط** — D9) · `ops.status` (P8: نسخ/إصدارات/صحة موصلات) · `about.licenses` (P8).

## 16) Deferred / Future — خارج المسار الأول
Dark mode (OD-UX-3) · تجربة موبايل كاملة · لوحات BI · Monitoring dashboards (رهن OD-P8-1) · قنوات Email/SMS وتفضيلاتها · تخصيص ثيمات.
