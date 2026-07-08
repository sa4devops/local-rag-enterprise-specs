# PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md — مراجعة التجميع قبل التنفيذ

> **Version:** 1.0 — Proposed (v0.7) · **Date:** 2026-07-08 · **الموضع الهدف:** `methodology/PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md`
> **الطبيعة:** مراجعة/تجميع فقط — لا كود، لا تنفيذ Phase، لا دمج/رفع GitHub ضمن هذه الوثيقة؛ كل الدمج بيد SA وفق ترتيب §3.
> **الحكم التنفيذي:** **Accept with changes** — الحالة المواصفاتية متسقة وبلا تعارضات كاسرة؛ «التغييرات» المطلوبة قبل أي تنفيذ: (١) دمج v0.5 ثم v0.6 وفق بوابتيهما، (٢) اعتماد مواصفة `architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md`، (٣) توحيد اسم حدثٍ واحد (Patch **P-4**)، (٤) ثم تحديث SPEC_SOURCE.

## §1 الإصدارات المعتمدة حالياً (Current accepted releases)
| الإصدار | الحالة | المحتوى | ZIP SHA-256 |
|---|---|---|---|
| v0.4-ui-ux-planning-package | **معتمد + مدموج ومُصدَر** (SPEC_SOURCE الحالي يشير إليه) | 12 ملف ui/ | See H-0004 / release asset record. |
| v0.5-ui-interaction-visibility-refinement | **معتمد، غير مدموج** | 7 ملفات ui/ (+ تعديل Tool-Agnostic) | cd58877f9af8f414f7b49bd82d8e4d09ee89d861092f68b03ff7e0be0da236d8 |
| v0.6-provider-model-run-ux | **معتمد (الدفعات 1–3 مكتملة)، غير مدموج** | 4 ملفات جديدة + **12 ملفاً معدَّلاً Δ مطبَّقة محلياً** + G14 + بوابة v0.6 | f45fa037d2bfb1e0d8889f6fd46f47be86555dfe6f87838782af69927542fdbd |
**فحص التعارض v0.4↔v0.5↔v0.6:** لا تعارضات كاسرة. ثلاث نقاط توفيق موثقة: (أ) موضع إعداد الأزرار (Builder مقابل admin.actions) — ملاحظة توفيقية قائمة تُثبَّت في Clarify P3؛ (ب) ازدواج اسم حدث الإقفال (PROVIDER_CHANGE_COMPLETED في v0.6 مقابل PROVIDER_CONFIG_APPLIED_BY_OPS في مواصفة v0.7) — يُحسم بـ **P-4** قبل أول دمج؛ (ج) مجموعات prompts غير المُعاد صياغتها (G2/G6/G8/G10–G12) — عمل مجدول قبل جولات Stitch الإدارية، ليس تعارضاً.

## §2 ما لم يُدمج بعد (Not merged yet)
1. **v0.5:** الملفات السبعة + تحديثاتها الوصفية (PACKAGE_CHECKLIST→v1.4 · github-docs-structure سطر تعايش الحزمتين · handoff **H-0005**).
2. **v0.6:** الملفات الأربع الجديدة + الـ 12 المعدَّلة (وفق `UI_V06_DELTA_AMENDMENTS.md` + G14) + تحديثات وصفية (PACKAGE_CHECKLIST→v1.5 · handoff **H-0006**) — بوابة `UI_V06_GATE_REVIEW.md` جاهزة.
3. **v0.7 (هذه الحزمة — مقترحة):** الملفان الجديدان (architecture/ + methodology/) + خطة Patches §9 + handoff **H-0007** + PACKAGE_CHECKLIST→v1.6.

## §3 ما يجب دمجه قبل التنفيذ (بالترتيب الإلزامي)
| # | الخطوة | البوابة/الشرط |
|---|---|---|
| 1 | دمج **v0.5** (commits بوابتها H) ثم Release بوسمها | UI_REFINEMENT_GATE_REVIEW = Accept |
| 2 | دمج **v0.6** (تطبيق الـ 12 Δ في الريبو مطابقةً لـ DELTA_AMENDMENTS + الأربعة الجديدة + P-4) ثم Release | UI_V06_GATE_REVIEW = Accept + تحقق مطابقة Δ |
| 3 | دمج **v0.7** (الملفان الجديدان + Patches P-1..P-3 وP-6 الاختياري) ثم Release **v0.7-pre-implementation-consolidation** | البنود §6 كلها ✔ |
| 4 | تحديث `platform/docs/SPEC_SOURCE.md` → **v0.7-pre-implementation-consolidation** (P-5) — **التغيير الوحيد في platform** | بعد وجود الإصدارات الثلاثة فعلاً |
> ترقيات SPEC_SOURCE الوسيطة (v0.5/v0.6) **اختيارية** إن تباعد الدمج زمنياً؛ الافتراضي هنا: ترقية واحدة نهائية لتقليل الضجيج، والقرار لـ SA.

## §4 ما يبقى مؤجلاً فعلاً (Deferred)
Design Agent مع repo · أي تعديل على **D9** · إدخال API keys/Base URL من UI · Coding Agent للمستخدم النهائي · **Terminal UI** بأي صيغة · أي وظيفة سايبر خاصة (فحص/استغلال/attack-surface) · **أي إعادة استخدام كود** من PentAGI أو RedAmon (خارج كتالوج الكود أصلاً — صور/ويكي فقط)؛ وكود Open WebUI لا يُمس إلا عبر مسار D8 المعتاد وبلا نسخ UI. **إضافةً للمؤجلات المسجلة**: OD-TPL-1 (template.create — غير معتمد) · OD-MX-3 (warm/unload يدوي) · OD-UX-3 (الوضع الداكن) · OD-AB-2 (bulk actions).

## §5 غير مؤجل لكنه **Backend-only** (الفصل الحاسم — لا خلط)
API keys · Base URL · provider endpoints · بيانات اعتماد المزوّد · حلّ الأسرار (secret resolution) · تحميل config — **كلها مطلوبة للنظام وتُنفَّذ في الـ Backend من مصادر Ops، وممنوعة من الواجهة بموجب D9 فقط**. المرجع المعياري الوحيد: `architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md`. أي Coding Agent يقرأ «ممنوع من UI» على أنه «مؤجل» يكون قد أخطأ قراءة المواصفة.

## §6 قائمة فحص ما قبل التنفيذ (Pre-implementation checklist)
- [ ] أحدث إصدار specs (v0.7) **مدموج ومُصدَر** وترتيب §3 مكتمل
- [ ] `platform/docs/SPEC_SOURCE.md` محدَّث إلى v0.7 (ولا تغيير آخر في platform)
- [ ] `architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md` موجود في الإصدار المدموج
- [ ] بوابتا v0.5 وv0.6 موثقتان بنتيجة Accept، والـ Δ في الريبو مطابقة لـ `UI_V06_DELTA_AMENDMENTS.md`
- [ ] **لا أسرار/Base URL/API Key/endpoints حقيقية في أي ملف UI أو DTO موصوف**
- [ ] لا Terminal UI ولا أي واجهة سايبرية في أي مواصفة
- [ ] لا إعادة استخدام كود من المراجع (PentAGI/RedAmon: ممنوع مطلقاً؛ OWUI: عبر D8 فقط وبلا UI)
- [ ] SHAs الحزم الثلاث مسجلة (جدول §1) ومطابقة للمرفوع
- [ ] صفوف بوابة الترخيص (م7) للستاك/الخط/الأيقونات محسومة قبل تشغيل Phase 0
- [ ] **تفعيل أي Phase يتطلب بطاقة مهمة صريحة معتمدة** — لا تنفيذ بدونها

## §7 تعليمات مُلزِمة لأي Coding Agent قبل كتابة أي سطر (تُقرأ مع methodology/agent-execution-model.md §6)
1. اقرأ `platform/docs/SPEC_SOURCE.md` أولاً، ثم محتوى إصدار specs المشار إليه **كاملاً** — المواصفات هي مصدر الحقيقة الوحيد.
2. **لا تستنتج** سلوكاً غير منصوص لأسرار/مزوّدات — المرجع الحصري `PROVIDER_MODEL_SECRET_CONFIG_SPEC.md`؛ الغموض ⇒ سؤال Clarify، لا افتراض.
3. **يُمنع** إضافة أي حقل سر/API Key/Base URL/endpoint في أي واجهة أو DTO موجَّه للواجهة (قائمة السماح §2 من المواصفة).
4. **يُمنع** إنشاء Terminal UI أو أي واجهة/ميزة سايبرية أو محاكاة console.
5. لا بدء أي Phase أو ملف تنفيذ بدون بطاقة مهمة معتمدة صراحة من SA.
6. أي تعديل على ملف قائم يتم بنمط Patch/Additive حصراً — لا إعادة كتابة كاملة ولا حذف قرارات.
7. الالتزام بالتسمية المقفلة (runs.list/runs.detail · الكتالوج المغلق + run/escalate/compare) وبكل OD كما هو مسجّل — الـ OD ليس دعوة للاجتهاد.

## §8 الإصدار التالي الموصى به
**Tag:** `v0.7-pre-implementation-consolidation` — **Pre-release** — المحتوى: الملفان الجديدان + Patches P-1..P-4 (+P-6 اختياري) + H-0007؛ الوصف: «تجميع ما قبل التنفيذ: مواصفة المزوّد/السر الخلفية + مراجعة الدمج والفصل بين المؤجل والـ Backend-only؛ بلا كود وبلا تنفيذ». بعده الخطوة 4 من §3 (SPEC_SOURCE). **لا يُنشأ الإصدار الآن** — بيد SA بعد الموافقة.

---

## §9 (ملحق) خطة الـ Patches — نمط Patch/Additive حصراً (لا تُطبَّق الآن)

### P-1 — `PACKAGE_CHECKLIST.md` (specs)
- **Change type:** Append rows (بعد تطبيق صفوف v0.5/v0.6 من دمجيهما).
- **Anchor:** آخر صف في جدول الحزم (بعد صفوف حزمة v0.6؛ وإن طُبِّق استثنائياً قبلها فبعد صفوف v0.4).
- **Patch text:**
> | architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md | v0.7 | مواصفة المزوّد/النموذج/السر (Backend — الخيار A) | معتمد-مقترح |
> | methodology/PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md | v0.7 | مراجعة التجميع قبل التنفيذ + خطة الدمج | معتمد-مقترح |
> وترقية سطر إصدار القائمة إلى **v1.6** (التسلسل: v1.4 مع v0.5 · v1.5 مع v0.6 · v1.6 مع v0.7).
- **Rationale:** بقاء القائمة مرجعاً شاملاً لبوابات الفحص. **Risk:** فقدان تتبع ملفين معياريين حاكمَين للتنفيذ.

### P-2 — `github-docs-structure.md` (specs)
- **Change type:** Insert after heading ×2.
- **Anchor 1:** آخر بند تحت قسم `architecture/` — **Patch text:**
> - `architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md` — عقد المزوّد/السر بين Config/Ops والـ Backend والواجهة (D9/الخيار A).
- **Anchor 2:** بند `methodology/agent-execution-model.md` — **Patch text (بعده):**
> - `methodology/PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md` — بوابة التجميع قبل التنفيذ وترتيب الدمج وتعليمات الوكلاء.
- **Rationale:** الخريطة تعكس البنية الفعلية. **Risk:** ملفات «يتيمة» خارج الفهرس تضعف قابلية الاكتشاف للوكلاء.

### P-3 — `handoff/handoff.md` (specs)
- **Change type:** Append section.
- **Anchor:** بعد آخر إدخال H-000x (المتوقع H-0006 بعد دمج v0.6).
- **Patch text:**
> ## H-0007 — v0.7 Pre-Implementation Consolidation (2026-07-08)
> **النطاق:** مواصفة Backend للمزوّد/السر (الخيار A، D9 ثابت) + مراجعة تجميع ودمج ما قبل التنفيذ. **المخرجات:** architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md · methodology/PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md · Patches P-1..P-6. **قرارات:** توحيد PROVIDER_CONFIG_APPLIED_BY_OPS (P-4) · الفصل «Backend-only ≠ مؤجل». **التالي:** تنفيذ ترتيب الدمج §3 ثم SPEC_SOURCE→v0.7؛ لا Phase بلا بطاقة مهمة.
- **Rationale:** استمرارية سجل التسليم. **Risk:** انقطاع خيط «مَن سلّم ماذا ولماذا» قبيل أخطر مرحلة (بدء الكود).

### P-4 — `ui/UI_PROVIDER_MODEL_MANAGEMENT.md` (ضمن مجموعة v0.6 — يُطبَّق قبل أول دمج لها)
- **Change type:** Replace exact phrase ×2 (السطران الحاليان 96 و104).
- **Anchor 1:** `PROVIDER_CHANGE_COMPLETED (إقفال Ops بمرجع)` — **Patch text:** `PROVIDER_CONFIG_APPLIED_BY_OPS (إقفال Ops بمرجع — الاسم الكنسي الموحّد مع مواصفة v0.7)`
- **Anchor 2:** `PROVIDER_CHANGE_REQUESTED · PROVIDER_CHANGE_COMPLETED.` — **Patch text:** `PROVIDER_CHANGE_REQUESTED · PROVIDER_CONFIG_APPLIED_BY_OPS.`
- **Rationale:** حدث واحد باسمين = ازدواج أبدي في كتالوج التدقيق إن دخل الدمج. **Risk:** استعلامات تدقيق ولوحات لاحقة تفوّت أحداثاً.

### P-5 — `platform/docs/SPEC_SOURCE.md` (**مؤجل — لا يُطبَّق في هذه الحزمة**)
- **Change type:** Replace exact line — **Anchor:** السطر الحامل للوسم الحالي `v0.4-ui-ux-planning-package`.
- **Patch text:** `v0.7-pre-implementation-consolidation`
- **شرط التطبيق:** فقط بعد وجود إصدارات v0.5/v0.6/v0.7 فعلياً (الخطوة 4 من §3). **Rationale:** المصدر الوحيد لرقم المواصفة. **Risk:** وكيل يبني على مواصفات قديمة.

### P-6 — `AGENTS.md` (platform) — **اختياري/موصى به، بقرار SA**
- **Change type:** Insert after heading — **Anchor:** أول قسم القواعد الملزمة في الملف.
- **Patch text:**
> - **أسرار المزوّدات:** لا حقول أسرار/Base URL/API Key في أي UI أو DTO للواجهة؛ تهيئة المزوّدات Backend/Ops-managed حصراً — المرجع `architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md`.
> - **ممنوع** أي Terminal UI أو واجهة/ميزة سايبرية.
> - قبل أي كود: SPEC_SOURCE ثم `methodology/PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md` §7.
- **Rationale:** خط دفاع أول أمام أي وكيل يعمل داخل platform. **Risk إن لم يُطبَّق:** منخفض (المنهجية تغطيه) — لذا صُنِّف اختيارياً.
