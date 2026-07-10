# UI_V06_GATE_REVIEW.md — بوابة فحص حزمة v0.6 (Provider · Model · Run UX)

> **Version:** 1.0 — Proposed (v0.6) · **Date:** 2026-07-08 · **الموضع الهدف:** `ui/UI_V06_GATE_REVIEW.md`
> **الغرض:** بوابة قبول **إلزامية** قبل رفع حزمة v0.6 إلى `local-rag-enterprise-specs` وإصدار `v0.6-provider-model-run-ux`.
> **العلاقة:** تُستكمل مع بوابتَي v0.4 وv0.5 ولا تُغني عنهما. أي بند ❌ في A–G يمنع الرفع؛ H إجرائي للرفع نفسه.

## A) الاكتمال (4 ملفات جديدة + 12 ملفاً مُعدَّلاً Δ)
- [ ] `ui/UI_PROVIDER_MODEL_MANAGEMENT.md` موجود
- [ ] `ui/UI_RUN_EXECUTION_MODEL.md` موجود
- [ ] `ui/UI_V06_DELTA_AMENDMENTS.md` موجود (سجل الـ Δ للتتبع)
- [ ] `ui/UI_V06_GATE_REVIEW.md` (هذا الملف) موجود
- [ ] Δ مطبَّقة على 12 ملفاً: INVENTORY(v1.2) · SITEMAP · BEHAVIOR_CARDS(20–23) · COMPONENT_STATES(14–17 + §18) · ACTION_BUTTON(6.c + OD-AB-4) · FIELD_NAMING(OD-NM-1 + §5 + صف §3) · ASSUMPTIONS(A-UX-15) · INTERACTION(4 صفوف §4) · VISIBILITY(قاعدة D9 البنيوية) · ADMIN_CONSOLE(ملاحظة F) · REFERENCE_POLICY(صفّا PentAGI/RedAmon) · STITCH_REFINED_PROMPTS(**G14** + قاعدة «الثماني»)

## B) D9 والخيار A محفوظان (فحص نصي + مفهومي)
- [ ] **لا Base URL حقيقي · لا API Key · لا أسرار · لا endpoints حقيقية** في أي ملف من الحزمة أو الـ Δ (بحث أنماط: مفاتيح/عناوين/منافذ ⇒ صفر)
- [ ] secret_ref يظهر **بالاسم فقط** (تقنيع بنيوي S10 موثَّق في Provider Card وVisibility)
- [ ] تعديل المزوّد الفعلي عبر **workflow «طلب تهيئة/تعديل»** إلى Ops فقط (المواصفة §8) — لا مسار كتابة من UI إلى config
- [ ] provider.test_connection يُرجِع chip نجاح/فشل فقط
- [ ] «اكتشاف النماذج» خادمي محلي؛ **لا أزرار تنزيل/سحب** نماذج

## C) قرارات المالك المنفَّذة حرفياً
- [ ] `runs.list` و`runs.detail` موجودتان: في الجرد v1.2 (الجدولان A/B) + بطاقة السلوك 23 + المواصفة — **ولا وجود لبدائل** (agent_runs/execution_console) إلا في سطور النهي التوثيقية
- [ ] الأفعال **run · escalate · compare** مضافة كأفعال محكومة: جدول العقود 6.c كامل الحقول + OD-NM-1 المعدَّل + صف سلسلة الربط §3
- [ ] **template.create لا يزال OD غير معتمد**: لا يظهر كعقد في 6.c؛ حاضر فقط في OD-AB-4 وOD-TPL-1 بوسم «غير معتمد بقرار المالك»
- [ ] **G14 موجودة** في ملف الموجّهات المحسّنة وتغطي: runs.list/detail · Timeline · Step · Output Panel · بوابة Approval/HITL داخل الخط · retry-من-خطوة · cancel · partial · audit correlation · رابطا reports.review وadmin.audit

## D) لا terminal ولا سايبر (المنع الصريح)
- [ ] نصوص المنع حاضرة في: مواصفة التشغيل (anti-scope + §5 + §11) · بطاقة runs.detail · G14 (**terminal UI · command console · pentest dashboard · tool-hacking UI · raw command output · cybersecurity-specific UI**)
- [ ] تأكيدات G14 حاضرة نصاً: enterprise monitoring surface · no free execution · no secrets/endpoints/Base URL/API Key · **action steps are governed enterprise actions only**
- [ ] لا مفردات هجومية (recon/exploit/shell/scan-هدف) كواجهات في أي ملف؛ ذكر PentAGI/RedAmon محصور بسياسة المراجع (صور/ويكي فقط)
- [ ] السجل المُهيكل جدولٌ عبر محرك admin.logs — لا console styling

## E) النقاء
- [ ] لا أسيجة كود (ثلاث علامات اقتباس مائلة متتالية) في ملفات v0.6 الأربعة **ولا في الملفات الاثني عشر المعدَّلة**
- [ ] لا أسطر أوامر طرفية (أنماط: $ · sudo · pip · npm · docker · git · bash · curl · wget)
- [ ] أسماء ملفات ASCII · لا أصول منتجات خارجية مضمّنة

## F) لا تغيير معماري — بنيان لا استبدال
- [ ] كل Δ **إضافي** أو استبدال منصوص محدود (ترويسة الجرد · OD-NM-1 · عنوان §14→§18 · قاعدة «السبعة»→«الثماني») — لا حذف محتوى معتمد
- [ ] لا مساس بالتصاميم المرحلية P0–P8 ولا بترتيبها؛ Dual-Surface وAction Layer الواحد وws-من-P6 كما هي
- [ ] عارض التشغيل **يقرأ سلسلة correlation القائمة** — لا مخزن ثانٍ (منصوص في المواصفة وA-UX-15)
- [ ] القرارات (اعتماد/رفض/إرجاع/escalate) تبقى على queue.approval_detail — runs.detail روابط وحالات فقط
- [ ] لا dependency جديدة؛ لا وكيل coding (خارج النطاق — Backlog)

## G) التسمية والاتساق
- [ ] runs.list/runs.detail تطابق أنماط screen_id/route (§1 التسمية) والمنطقة `runs` موثَّقة القفل
- [ ] أحداث RUN_* / MODEL_* / PROVIDER_CHANGE_* بصيغة UPPER_SNAKE وحمولتها موصوفة
- [ ] operationId الجديدة (runs_start/cancel/retry/retry_step · approvals_escalate) snake_case بمساراتها
- [ ] لا خلط action_id/endpoint في الإضافات؛ المعرّفات LTR-isolated في الأمثلة
- [ ] إحالات OD الجديدة (OD-MX-1/3/4 · OD-RUN-1..3 · OD-TPL-1 · OD-AB-4) معرَّفة في مواضعها

## H) خطة الرفع والإصدار (بعد Accept — بيد المالك حصراً)
- [ ] الوجهة: `ui/` في specs — **4 ملفات جديدة + 12 ملفاً مُحدَّثاً في مواضعها** (+ اختياري: `ui/reviews/UI_EXTERNAL_PATTERNS_REVIEW_2026-07.md` كمرجع قرار الحزمة)
- [ ] commits مقترحة (5):
  - (1) `Add ui v0.6 core specs (provider-model management, run execution model)`
  - (2) `Apply ui v0.6 deltas to v0.4 docs` — الملفات السبعة (inventory v1.2 · sitemap · action-button 6.c · field-naming · assumptions A-UX-15 · admin-console F · reference-policy) + `UI_V06_DELTA_AMENDMENTS.md` كسجل
  - (3) `Apply ui v0.6 deltas to v0.5 docs` — الملفات الخمسة (behavior-cards 20–23 · component-states 14–17 · interaction · visibility · refined-prompts **G14**)
  - (4) `Add ui v0.6 gate review`
  - (5) `Update package checklist, docs structure and handoff for ui v0.6` — `PACKAGE_CHECKLIST.md → v1.5` (صفوف الأربعة الجديدة + إشارة الـ Δ) · `github-docs-structure.md` (+`ui/reviews/` إن اعتُمد رفع المراجعة) · `handoff/handoff.md` بإدخال **H-0006**
- [ ] إنشاء Release: **`v0.6-provider-model-run-ux`** — Title: *Provider, Model &amp; Run UX Package v0.6* — **Pre-release** — الوصف: إدارة مزوّدات/نماذج وفق الخيار A (D9 محفوظ حرفياً) + Model Profiles + عارض تشغيل مؤسسي (runs.list/runs.detail) + G14 + Δ إضافية على v0.4/v0.5؛ بلا كود، بلا terminal، بلا أي وظيفة سيبرانية، بلا تغيير معماري
- [ ] بعد الإصدار: تحديث `platform/docs/SPEC_SOURCE.md` إلى `v0.6-provider-model-run-ux` **فقط** (لا إصدار platform جديد)

## قرار البوابة
| النتيجة | ☐ Accept | ☐ Accept with minor edits | ☐ Reject |
|---|---|---|---|

| البند | الملف | الملاحظة | الإجراء المطلوب |
|---|---|---|---|
|  |  |  |  |

المراجِع: ____________ · التاريخ: ____________ · مرجع الجلسة/الفحص الآلي: ____________

القرار: Accepted — تمثّل الموافقةَ المالكُ بنشر الإصدار الرسمي بتاريخ 2026-07-08: https://github.com/sa4devops/local-rag-enterprise-specs/releases/tag/v0.6-provider-model-run-ux
