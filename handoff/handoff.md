# handoff.md — سجل التسليم بين الجلسات والوكلاء

> **Version:** 1.1 (Δ 2026-07-11: توضيح اتفاقية الأرشفة وترتيب القراءة — تحسين للآلية القائمة لا نظام موازٍ) · **Status:** Current / Accepted · **Date:** 2026-07-11 (الأصل 2026-07-02) · **Authority:** ينفّذ Methodology §14.
> **القواعد:** لا تُغلق أي جلسة/مهمة/مرحلة دون تعبئة إدخال كامل هنا · يُؤرشف الإدخال السابق في `handoff/archive/` بتاريخه · الوكيل التالي **يقرأ هذا الملف قبل أي عمل** ويحترم قائمة «Do not touch» حرفياً · إن كانت المتطلبات غامضة: يسأل ولا يكتب.
> **اتفاقية التشغيل (Δ 2026-07-11):** هذا الملف هو **السجل المتجدد الوحيد** (الإدخالات H-NNNN تتراكم فيه) · عند **إغلاق كل مرحلة تنفيذية** تُؤخذ لقطة مؤرشفة باسم `handoff/archive/PHASE_N_HANDOFF-YYYY-MM-DD.md` · **ترتيب القراءة:** آخر إدخال أولاً ثم الأقدم عند الحاجة فقط — ولا يُنشأ أي نظام handoff موازٍ.

## القالب (يُنسخ لكل إدخال)
```
## Handoff H-XXXX
- date:
- phase:
- task:
- goal:
- completed:
- not completed:
- files changed:
- decisions:
- risks:
- tests: (ناجح/فاشل + الأسماء)
- next step:
- do not touch:
- notes for next agent:
```

---

## Handoff H-0002
- **date:** 2026-07-04
- **phase:** ما قبل التنفيذ — دمج قرارات D1–D9
- **task:** تحديث الحزمة إلى الإصدار 2026-07-04 (ستاك الواجهة/الخادم، التجريدات الثلاث، التخزين FS-أولاً، الخط الرقابي الأساسي، GitHub-الآن، سياسة Reference-aware)
- **goal:** حزمة متسقة بلا تعارض (لا وثيقة تقول Next.js/SvelteKit وأخرى React)
- **completed:** تحديث 13 ملفاً (انظر PACKAGE_CHECKLIST v1.1) + ADR-0017..0022 + إغلاق C1–C5 + إعادة بناء ZIP بـ SHA جديد
- **not completed (مقصود):** لا كود · لا Phase 1 · لا تحديث بصري للـ SVG (ملاحظة حاكمة في architecture/README)
- **files changed:** README · catalogs/Catalog · methodology/{Methodology, coding-standards, testing-strategy} · decisions/{open-decisions, license-review, adr/README} · phases/{phase-roadmap, phase-0} · architecture/README · PACKAGE_CHECKLIST · handoff
- **decisions:** D1–D9 مثبتة (الكتالوج §2 + open-decisions v2.1 + ADR-0017..0022)
- **risks:** تفعيل صورة اختيارية لاحقاً دون بوابة الفئة 3 — البوابة متكررة ومنصوصة في كل المواضع
- **tests:** لا كود بعد؛ أُضيف نوعا Provider-Equivalence وLogging/Error-Contract للاستراتيجية
- **next step:** تصميم **Phase 1 — Governed Core + Screen Builder** في محادثة مستقلة (بلا كود)
- **do not touch:** superseded/ · decisions/adr/ دون طلب · constitution.md (لم يتغيّر عمداً)
- **notes for next agent:** التزم بالستاك المعتمد وبسياسة Reference-aware؛ اقرأ الترتيب في README؛ لا تبدأ كوداً وأي قرار لازم غير محسوم

---

## Handoff H-0001
- **date:** 2026-07-02
- **phase:** ما قبل التنفيذ — تجهيز حزمة الوثائق النهائية
- **task:** إصدار الحزمة v2.0 المدمجة (A1–A11) الجاهزة للرفع على GitHub
- **goal:** مرجع رسمي كامل لأي AI Coding Agent قبل أي كود
- **completed:** README · vision · constitution · Methodology v2.0 · Catalog v2.0 · Open-Decisions v2.0 · Phase-0 Design v2.0 (Accepted for design) · phase-roadmap · github-docs-structure · license-review (مزروع) · adr/README (السجل الكنسي) · testing-strategy · coding-standards · architecture/README · phases/README · superseded/README · PACKAGE_CHECKLIST
- **not completed (مقصود — ليس نقصاً):** لا كود · لا تنفيذ Phase 0 · لا تصميم Phase 1 · ملفات ADR الفردية والمعماريات المستخرجة وrunbooks تُنشأ عند زرع specs (T-0.1.3) وما بعده
- **files changed:** كل محتويات `final/` (الحزمة كاملة)
- **decisions:** ADR-0001 **Accepted** · التعديلات A1–A11 مدمجة · التسمية بالرقم+الاسم (C8 مُغلق) · الترقيم الكنسي للـ ADRs في decisions/adr/README.md
- **risks:** بنود الفئة 3 (C1–C3) غير محسومة — تحجب مهمة الـ Compose فقط · تراخيص Needs Legal Review قائمة
- **tests:** لا اختبارات بعد (لا كود) — استراتيجية الاختبار معتمدة
- **next step:** تصميم **Phase 1 — Governed Core + Screen Builder** في محادثة مستقلة (Vision→Specify→Clarify→Plan→Tasks، بلا كود)؛ وبالتوازي حسم C4/C5 وC1–C3 قبل تنفيذ Phase 0
- **do not touch:** `superseded/` وكل ما يُنقل إليه (برومبتات Phase-0/1 القديمة، المخططات القديمة، نسخ v1.0) · `decisions/adr/` دون طلب صريح · constitution.md دون قرار مالك المشروع
- **notes for next agent:** اقرأ بالترتيب المحدد في README؛ نفّذ المكتوب فقط؛ أي dependency جديدة تبدأ بصف في license-review.md
## H-0003 — GitHub Bootstrap Closure

Date: 2026-07-05

Type: Organizational handoff

Status: Closed

### Summary

The GitHub bootstrap stage has been completed.

Two repositories are now established:

- `local-rag-enterprise-specs`
- `local-rag-enterprise-platform`

The specs repository is the authoritative source of truth for project documentation, architecture, methodology, decisions, phase designs, agent rules, and approved OSS references.

The platform repository is reserved for implementation code and currently contains bootstrap governance files only.

No implementation code has been written.

No Phase 0 implementation has started.

No Phase 1 design has started.

### Current releases

Specs repository:

- Current approved release: `v0.2-specs-reference-catalog`
- Previous baseline release: `v0.1-specs-baseline`

Platform repository:

- Current bootstrap release: `v0.2-platform-bootstrap`
- Previous bootstrap release: `v0.1-platform-bootstrap`

### Completed actions

- Created the specs repository.
- Uploaded the approved documentation package.
- Created specs release `v0.1-specs-baseline`.
- Added `references/OSS_REFERENCE_CATALOG.md`.
- Updated `PACKAGE_CHECKLIST.md`.
- Updated `github-docs-structure.md`.
- Created specs release `v0.2-specs-reference-catalog`.
- Created the platform repository.
- Added `README.md`.
- Added `AGENTS.md`.
- Added `docs/SPEC_SOURCE.md`.
- Added `.gitignore`.
- Added `LICENSE_NOTICE.md`.
- Updated platform references from `v0.1-specs-baseline` to `v0.2-specs-reference-catalog`.
- Created platform release `v0.2-platform-bootstrap`.

### Governance state

The current authoritative specs release is:

`v0.2-specs-reference-catalog`

The current platform bootstrap release is:

`v0.2-platform-bootstrap`

Future agents must read `docs/SPEC_SOURCE.md` in the platform repository to determine the current approved specs release.

Platform `README.md` and `AGENTS.md` should avoid duplicating release numbers where possible and should defer to `docs/SPEC_SOURCE.md` as the release pointer.

### OSS reference policy

The approved OSS reference catalog is located at:

`references/OSS_REFERENCE_CATALOG.md`

Only projects listed in that catalog may be studied by AI agents.

Projects not listed in the catalog require explicit approval before study.

OSS references are references only, not dependencies.

Direct code copying is prohibited unless explicitly approved through license review.

### Open housekeeping items

The following items are not blockers for Phase 1 design, but should be addressed in a future specs update:

- Add `LICENSE_NOTICE.md` to the specs repository.
- Expand `OSS_REFERENCE_CATALOG.md` with actual license names, risk levels, study depth, direct-dependency allowance, and copy-in allowance.
- Make `docs/SPEC_SOURCE.md` the single release pointer for future approved specs release numbers.
- Document the release cycle rule:
  approved phase design → commit to specs → create new specs release → update platform SPEC_SOURCE if needed.

### Next recommended step

Open a separate conversation for Phase 1 design only.

Recommended Phase 1 scope:

Governed Core + Screen Builder

The next conversation must remain design-only and should follow:

Vision → Specify → Clarify → Plan → Tasks

No implementation code should be written during Phase 1 design.

## H-0004 — UI/UX Planning Package v0.4 Accepted

Date: 2026-07-07

Status: Accepted for Design / Planning

Summary:

The UI/UX Planning Package v0.4 has been accepted and prepared for release.

Included in this handoff:

- `ui/UI_UX_ASSUMPTIONS.md`
- `ui/UI_SITEMAP.md`
- `ui/UI_SCREEN_INVENTORY.md`
- `ui/UI_AI_WORKSPACE_MODEL.md`
- `ui/UI_ACTION_BUTTON_MODEL.md`
- `ui/UI_ADMIN_CONSOLE_MODEL.md`
- `ui/UI_FIELD_NAMING.md`
- `ui/UI_DESIGN_SYSTEM.md`
- `ui/UI_SCREEN_CARDS_BY_PHASE.md`
- `ui/UI_STITCH_PROMPTS_BY_PHASE.md`
- `ui/UI_REFERENCE_USAGE_POLICY.md`
- `ui/UI_GATE_REVIEW_CHECKLIST.md`

Release:

`v0.4-ui-ux-planning-package`

Important rules:

- No implementation code is included in this release.
- Google Stitch outputs are prototypes/references only.
- Final implementation must follow React + Vite + TypeScript + Tailwind + shadcn/ui-style.
- The accepted UI model is Dual-Surface: AI Workspace + Runtime Renderer, both using one governed Action Layer.
- The LLM suggests actions; backend validation, permission checks, approval flow, execution, and audit remain authoritative.

## H-0005 — UI Interaction & Visibility Refinement Package v0.5 Accepted

Date: 2026-07-08

Status: Accepted for Design / Planning

Summary:

The UI Interaction & Visibility Refinement Package v0.5 has been accepted and prepared for release. It builds on top of UI/UX Planning Package v0.4 without replacing or removing any of its files.

Included in this handoff:

- `ui/UI_INTERACTION_MODEL.md`
- `ui/UI_VISIBILITY_RULES.md`
- `ui/UI_PROGRESSIVE_DISCLOSURE.md`
- `ui/UI_COMPONENT_STATES.md`
- `ui/UI_SCREEN_BEHAVIOR_CARDS.md`
- `ui/UI_STITCH_REFINED_PROMPTS.md`
- `ui/UI_REFINEMENT_GATE_REVIEW.md`

Release:

`v0.5-ui-interaction-visibility-refinement`

Important rules:

- No implementation code is included in this release.
- No architectural change; interaction, visibility, and component-state rules only.
- Builds on v0.4 — no v0.4 file modified or removed.

## H-0006 — Provider, Model & Run UX Package v0.6 Accepted

Date: 2026-07-08

Status: Accepted for Design / Planning

Summary:

The Provider, Model & Run UX Package v0.6 has been accepted and prepared for release. It adds four new specification files and applies delta amendments to twelve previously merged files (seven from v0.4, five from v0.5), replacing them with their final approved v0.6 versions. Patch P-4 (canonical event name unification: PROVIDER_CHANGE_COMPLETED → PROVIDER_CONFIG_APPLIED_BY_OPS) was applied to `ui/UI_PROVIDER_MODEL_MANAGEMENT.md` before this merge.

New files in this handoff:

- `ui/UI_PROVIDER_MODEL_MANAGEMENT.md`
- `ui/UI_RUN_EXECUTION_MODEL.md`
- `ui/UI_V06_DELTA_AMENDMENTS.md`
- `ui/UI_V06_GATE_REVIEW.md`

Files replaced with final v0.6 versions (12):

- `ui/UI_ACTION_BUTTON_MODEL.md`
- `ui/UI_ADMIN_CONSOLE_MODEL.md`
- `ui/UI_FIELD_NAMING.md`
- `ui/UI_REFERENCE_USAGE_POLICY.md`
- `ui/UI_SCREEN_INVENTORY.md`
- `ui/UI_SITEMAP.md`
- `ui/UI_UX_ASSUMPTIONS.md`
- `ui/UI_INTERACTION_MODEL.md`
- `ui/UI_VISIBILITY_RULES.md`
- `ui/UI_COMPONENT_STATES.md`
- `ui/UI_SCREEN_BEHAVIOR_CARDS.md`
- `ui/UI_STITCH_REFINED_PROMPTS.md`

Release:

`v0.6-provider-model-run-ux`

Important rules:

- No implementation code is included in this release.
- No architectural change — Dual-Surface, single Action Layer, and Workspace-from-P6 unchanged.
- D9 boundary preserved literally: no real Base URL / API Key / secrets / endpoints in any file or delta; secret_ref by name only.
- No Terminal UI, no cybersecurity-specific UI.

## H-0007 — v0.7 Pre-Implementation Consolidation (2026-07-08)
**النطاق:** مواصفة Backend للمزوّد/السر (الخيار A، D9 ثابت) + مراجعة تجميع ودمج ما قبل التنفيذ. **المخرجات:** architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md · methodology/PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md · Patches P-1..P-6. **قرارات:** توحيد PROVIDER_CONFIG_APPLIED_BY_OPS (P-4) · الفصل «Backend-only ≠ مؤجل». **التالي:** تنفيذ ترتيب الدمج §3 ثم SPEC_SOURCE→v0.7؛ لا Phase بلا بطاقة مهمة.

## H-0008 — v0.7.1 Responsive UI (توثيق لاحق — سُجِّل 2026-07-10)
**الطبيعة:** إدخال توثيقي بأثر رجعي — الإصدار صدر فعلاً (release `v0.7.1-responsive-ui` على commit c6dc18f بتاريخ 2026-07-10) دون إدخال handoff وقتها؛ يُسجَّل هنا حفاظاً على استمرارية السجل.
**النطاق:** متطلب الواجهة المتجاوبة (Responsive UI) فوق خط v0.7 المجمَّد.
**المخرجات:** Δ على 4 ملفات ui: `UI_UX_ASSUMPTIONS.md` (A-UX-16) · `UI_DESIGN_SYSTEM.md` (قسم Responsive) · `UI_SCREEN_BEHAVIOR_CARDS.md` (Global Responsive Behavior Rule) · `UI_STITCH_REFINED_PROMPTS.md` (Global Responsive Prompt Requirement).
**ملاحظات:** الوسم lightweight وبلا ZIP asset (انحراف عن نمط Option B المعمول به منذ v0.5 — مسجَّل Finding في EXECUTION_REPORT v0.8) · commit لاحق b03c9e3 (تصحيح v2.0→v2.1 في phases/README) بقي غير مُصدَر ويدخل ضمن v0.8.

## H-0009 — v0.8 Conversational & Workflow Batch (2026-07-10)
- **date:** 2026-07-10
- **phase:** ما قبل التنفيذ — دفعة تعديلات معتمدة من SA (تنفيذ وكيل مفوَّض)
- **task:** جرد 100% + تدقيق + إصلاحات FIX-9..14 + تطبيق دفعة SA (الأسطح المحادثية + سير العمل والتنظيم) + إصدار v0.8 وفق Option B
- **goal:** حزمة متسقة الفهارس، مع اعتماد السطح المحادثي المحكوم وقرارات الإرجاع/التنظيم، دون أي مساس بالقرارات المقفلة (D9 · runs.list/runs.detail · حالات النموذج الست · PROVIDER_CONFIG_APPLIED_BY_OPS · لا DDL من LLM)
- **completed:** FIX-9 (github-docs-structure v1.6) · PACKAGE_CHECKLIST v1.7 · architecture/README v1.2 · توثيق v0.7.1 (H-0008) · OD-WS-4 (وضعا عرض ws.main) · متغيّر «inline message action» · A-UX-17 (صياغة الهوية) · OD-BLD-1 (أوضاع الباني الثلاثة) · توضيح UI_REFERENCE_USAGE_POLICY · FR-3.11/FR-3.12/FR-1.Org-Ext (في DELTA_V08_FR_WORKFLOW_ORG) · OD-WF-1/OD-WF-2/OD-ORG-1 مقفلة · تحديث بطاقات queue.approval_detail/queue.tasks (+بطاقة 24 admin.org) · G6/G8 · فهرس OD · جرد الشاشات v1.3 · UI_FIELD_NAMING (WORKFLOW_ITEM_RETURNED · workflow.return_route) · EXECUTION_REPORT.md
- **not completed (مقصود):** لا كود · لا تنفيذ Phase · لم تُعالَج Findings المعلَّقة بقرار SA (حزمة v0.3 الغائبة · تسوية وسوم lightweight القديمة · ملفات platform غير SPEC_SOURCE — التفصيل في EXECUTION_REPORT)
- **files changed:** انظر جدول «الملفات المتغيرة» في `EXECUTION_REPORT.md`
- **decisions:** OD-WS-4 (ورد في دفعة SA باسم OD-WS-2 — عُدِّل الترقيم لتفادي تصادم مع قرار مدة الاحتفاظ القائم) · OD-BLD-1 · OD-WF-1 · OD-WF-2 · OD-ORG-1 — كلها مقفلة بقرار SA 2026-07-10
- **risks:** غياب ملفات تصميم Phase 1/Phase 3 يعني أن FR الجديدة محمولة في ملف delta حتى تأليف/استعادة الملفات الأم — يجب دمجها نصياً حينها
- **tests:** لا كود بعد — فحوص نقاء (لا أسيجة كود/لا أوامر/لا أسرار) مطبقة على الملفات المعدلة
- **next step:** قرار SA في Findings المعلَّقة (استعادة حزمة v0.3 أولاً) ثم تصميم Phase 1 في محادثة مستقلة
- **do not touch:** superseded/ · decisions/adr/ · constitution.md · التصاميم المرحلية وترتيبها
- **notes for next agent:** اقرأ `EXECUTION_REPORT.md` ثم `phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md` قبل أي عمل على Phase 1/Phase 3؛ المرجع النافذ للمواصفات: tag `v0.8-conversational-and-workflow`

## H-0010 — إغلاق خط الأساس المعماري v1.0-architecture-baseline (2026-07-10)
- **date:** 2026-07-10
- **phase:** إغلاق مرحلة المعمارية والمواصفات (تنفيذ وكيل مفوَّض — حزمة القرارات الستة عشر D1–D16)
- **task:** تثبيت القرارات النهائية + زرع ملفات ADR + فحص اتساق شامل + وسم `v1.0-architecture-baseline` (commits محلية + وسم محلي — **بلا دفع**)
- **goal:** معمارية مجمّدة للتنفيذ بمرجع موسوم واحد؛ أي تغيير معماري لاحق عبر ADR حصراً (م21)
- **completed:** constitution v1.1 (م21/م22) · سطر الهوية في vision/README/roadmap · agent-execution-model v1.1 (§9 مصفوفة القراءة · §10 سلّم الجاهزية · §11 قاعدتا الحراسة) · coding-standards v1.2 (D12) · جملة ما-بعد-الخط في المنهجية §20 · قاعدة اختبارات العقود للاستخراج · **13 ملف ADR**: زرع 0004/0017/0018/0019/0020/0021(معدَّل)/0022 + جديدة **0023–0028** · adr/README v1.2 (سياسة D15 كاملة + الليدجر) · open-decisions v2.3 (قسم الإغلاق + القيم التشغيلية + OD-IDX-1 مرفوض الآن) · license-review v1.2 (SeaweedFS افتراضي الإنتاج · MinIO مشروط · Valkey افتراضي التوسع · Redis مقفل · إصدارات P0 تُثبَّت في lockfiles) · إضافات Phase 0 (D14/D11/D4-موضع الواجهة/D3-خريطة التغليف) · بوابة بروفة التسليم (D13) في roadmap · تصحيح استشهاد (م2 + م16) في ملفَي الرؤية/الأزرار · سطرا قرار بوابتَي v0.5/v0.6 برابطي الإصدارين الرسميين · تحديث SPEC_SOURCE في المنصة إلى الوسم + README مؤشر واحد + حواجز AGENTS
- **not completed (مقصود):** لا دفع ولا release (بيد SA) · بصمة أصل v0.4 — **SKIPPED**: الإصدار بلا ZIP asset (لا تُخترع قيم) · Findings v0.8 المعلقة كما هي (استعادة حزمة v0.3 أولوية قبل تصميم Phase 1)
- **files changed:** أربعة commits في specs (C1–C4) + commit واحد في المنصة — التفصيل الكامل في `BASELINE_CLOSURE_REPORT.md` (خارج المستودعين)
- **decisions:** D1–D16 مثبتة بخط الأساس؛ المقفل الجديد: هوية المنصة (ADR-0023) · عقد REST+OpenAPI+SSE (ADR-0025) · موضع `/frontend` (ADR-0017) · SeaweedFS افتراضي الإنتاج (ADR-0019) · Valkey افتراضي التوسع ومسألة Redis مقفلة (ADR-0018) · سياسة التغليف والاستخراج (ADR-0026) · سياسة التجميد (ADR-0028)
- **risks:** وسم الخط محلي غير مدفوع — أي عمل قبل الدفع يبني على مرجع غير منشور؛ وملفا التصميم Phase 1/3 ما زالا غائبين (F-3)
- **tests:** لا كود — حزمة تحقق V1–V7 (مصطلحات قديمة · مؤشرات عابرة · تكافؤ ADR · الدستور · الروابط · السلبيات الحوكمية · الفهارس) — النتائج في التقرير
- **next step:** دفع main + الوسم في specs وmain في المنصة (بيد SA) ثم تصميم Phase 1 بمحادثة مستقلة ببطاقة مهمة معتمدة
- **do not touch:** superseded/ · جوهر حزم ui v0.4–v0.7 · التصاميم المرحلية وترتيبها
- **notes for next agent:** المرجع النافذ بعد الدفع: tag `v1.0-architecture-baseline`؛ اقرأ وفق مصفوفة القراءة (agent-execution-model §9) لا القراءة الشاملة. **ملاحظة عرف الإصدارات:** إصدارات 2026-07-08 الثلاثة (v0.5/v0.6/v0.7) تشترك في commit موحَّد واحد (5ede5cb) — الموافقة مُمثَّلة بنشر الإصدار الرسمي ذاته، وسطرا القرار في بوابتَي v0.5/v0.6 يوثّقان ذلك. (ترقيم هذا الإدخال H-0010 لأن H-0008/H-0009 محجوزان لتوثيق v0.7.1 ودفعة v0.8)

## H-0011 — إغلاق البقايا: استعادة حزمة v0.3 (إغلاق F-3) + نظافة ما-بعد-الأساس (2026-07-10)
- **date:** 2026-07-10
- **phase:** ما بعد خط الأساس — إغلاق البنود المتبقية الثلاثة (تنفيذ وكيل مفوَّض؛ commits محلية — بلا دفع)
- **task:** T1 سياسة `.claude/` في المستودعين · T2 حسم تكرار «Approved OSS references» في AGENTS.md · T3 استعادة حزمة v0.3 وإغلاق F-3 من أرشيف المالك المتحقَّق ببصمته
- **goal:** إغلاق Finding F-3 نهائياً بمدخل تصميم حي لمعرفات FR + أرشيف أصلٍ مجمّد، ونظافة مستودعية تمنع تسرب حالة Claude المحلية
- **completed:** **F-3 مغلقة** — الملفات العشرة (PHASE_MASTER_PLAN · BACKLOG_DEFERRED_SCOPE · تصاميم phase-1..8) مستعادة حيةً بمساراتها المعلنة **بلافتة حالة** أعلى كل ملف (مدخل ما-قبل-الأساس؛ ما استجد حتى v1.0-architecture-baseline يعلوها؛ لا تنفيذ مباشر) · **الأصل الكامل (12 ملفاً) مؤرشف مجمّداً بايتاً-بايتاً** في `superseded/phase-design-package-v0.3/` + RESTORE_NOTE ببصمة الأرشيف SHA-256: 084c26776f21a9eb6544b37cc3bef438dfc52b9befd4cb420c0419fdc2f40faa · نسخة `agent-execution-model.md` v0.3 **أرشيف-فقط** متجاوَزة بالخليفة الحية v1.1 (فرق الجوهر موثق في تقرير الجولة) · تحديثات الاتساق: agent-execution-model §5 (جملة المدخل الإلزامي) · phase-roadmap (سطر مدخلات v0.3) · PACKAGE_CHECKLIST **v1.9** + صف الأرشيف · open-decisions (سطر إغلاق F-3) · صف في superseded/README · **T1:** كتلة تجاهل `.claude/` (تتبع-المشترك/تجاهل-المحلي) في gitignore المستودعين — المجلد غائب فيهما (وقائي) · **T2:** الكتلتان متطابقتان بايتاً-بايتاً ⇒ **الفرع (a)**: بقيت القانونية في سياق سياسة المراجع واستُبدلت الثانية بسطر إحالة واحد؛ حواجز D9/اللا-طرفية/بطاقة المهمة سليمة
- **not completed (مقصود):** لا دفع (specs الآن 6 commits غير مدفوعة + الوسم؛ platform ‏3) · لا دمج بين نسختي agent-execution-model (أرشفة فقط) · لا تنفيذ ولا Phase 1
- **files changed:** specs: ‏23 ملفاً جديداً (10 حية + 13 أرشيف) + 6 معدَّلة + .gitignore جديد · platform: .gitignore + AGENTS.md — التفصيل في `RESIDUALS_CLOSURE_REPORT.md`
- **decisions:** سياسة `.claude/`: «تتبع المختار وتجاهل المحلي» · توحيد قائمة OSS بمصدر واحد (الفرع a) · التصاميم المستعادة = مدخل إلزامي وموطن تعريفي لمعرفات FR والنافذ «تصميم التفعيل»
- **risks:** لافتات الحالة تعتمد على التزام الوكلاء بقراءتها — بطاقة المهمة تبقى البوابة الفعلية؛ ‏6 commits متراكمة غير مدفوعة
- **tests:** تحقق V1–V8 (عدد الملفات/اللافتات · مراسي FR حية · تطابق الأرشيف البايتي عينياً · الفهارس · الوسم لم يتحرك · لا كود) — النتائج في التقرير
- **next step:** دفع المستودعين بيد SA ثم تصميم Phase 1 ببطاقة مهمة معتمدة — **مدخله الآن موجود**: `phases/designs/phase-1-governed-core-screen-builder.md` (v0.3) + `DELTA_V08_FR_WORKFLOW_ORG.md`
- **do not touch:** `superseded/phase-design-package-v0.3/` (مجمّد بايتاً-بايتاً) · الوسم `v1.0-architecture-baseline` (لا يتحرك)
- **notes for next agent:** عند تصميم Phase 1: ابدأ من تصميم v0.3 المستعاد + ادمج دلتا v0.8 نصياً + التزم لافتة الحالة (ما بعد v0.3 يعلو عند التعارض)

## H-0012 — تنحية تجربة Flutter ‏(AQL) + جسر Open WebUI المؤقت (2026-07-11)
- **date:** 2026-07-11
- **phase:** ما بعد خط الأساس — دفعة نظافة واتجاه واجهة بينية (فرع `chore/remove-flutter-adopt-openwebui-bridge` في المستودعين)
- **task:** جرد وإزالة كل أثر Flutter/AQL (محلياً ومن الفرعين) · تثبيت React خطاً قائماً دون إعادة فتح · ADR-0029/0030 · حزمة حوكمة الوثائق · ‏scaffold معزول لـ Open WebUI · مزامنة المؤشرات · التقرير
- **goal:** صفر إشارة Flutter نشطة، وواجهة محادثة مؤقتة محكومة بمبدأ العميل القابل للاستبدال دون أي مساس بالقرارات المقفلة
- **completed:** **جرد الفرعين: صفر إشارة Flutter/Dart/AQL** (شجرةً وتاريخاً — Not found؛ لذلك لا ADR سحبٍ لقرار لم يوجد، والتنحية موثقة هنا وفي التقرير) · **محلياً:** تجربة AQL ‏(`~/Desktop/flutter` — ‏remote ‏sa4devops/aql.git المحذوف مسبقاً بيد SA · آخر commit ‏4552bb1) أُرشفت كاملة (بما فيه تغييرات غير مرسلة) في `~/local-rag-removal-backup/aql-flutter-experiment-2026-07-11.tar.gz` ‏(sha256 ‏71fbc0366241fb73540325838368890a9bd9a03efeadcca34ddd1c11f7199f5d) ثم حُذف المسار؛ ‏SDK ‏Flutter/Dart ‏(Homebrew) وملفات الإعداد العالمية أُبقيت (لا إثبات حصرية — توصية مؤجلة) · **القرارات:** ‏ADR-0029 (العميل القابل للاستبدال؛ ترقية الدستور مشروطة باختبار الاستبدال) · ADR-0030 ‏(Open WebUI واجهة مؤقتة ضمن شرط م6 ببوابات وخروج) + فهرس الدفعة في open-decisions + صف ترخيص صورة الحاوية ‏(v0.6.5 مثبَّت · Needs Legal Review · digest إلزامي عند أول سحب) في السجل الوحيد · **الحوكمة:** سطر «منصة تطبيقات مؤسسية لا تطبيق أعمال واحداً» في README/vision فقط · قاعدة المستويين في adr/README · جدول تفصيل D8 وسلّم Platform→Products→Modules→Capabilities في coding-standards · اتفاقية handoff (لقطة PHASE_N + ترتيب قراءة) · PROJECT_EVOLUTION.md (فهرس سردي مشتق بالدليل — ليس مصدر حقيقة ثانياً) · **المنصة:** ‏scaffold معزول كامل `integrations/openwebui/` ‏(18 ملفاً · لا مجلدات فارغة · compose مثبَّت الإصدار بلا latest وبلا digest مختلق · سياسات القفل السبع · وثائق ARCHITECTURE/SECURITY_BOUNDARY/DATA_OWNERSHIP/CUSTOMIZATIONS/UPSTREAM_VERSION/DECOMMISSION_PLAN · خطط اختبار كمواصفات بلا Backend وهمي) · **الخارطة والمؤشرات:** دلتا «Open WebUI interim client» في roadmap بشروط خروج؛ ‏SPEC_SOURCE وREADME المنصة متزامنان أصلاً على المرجع القطعي `v1.0-architecture-baseline` ‏(commit ‏260780f — تحقق Phase 0)
- **not completed (مقصود):** لا تثبيت تشغيلياً ولا ادعاء تكامل (scaffold فقط) · لا وسم إصدار جديد (توصية بالإبقاء لتعليمة SA) · لا دمج في main (الفرعان مدفوعان للمراجعة) · MODULE_BOUNDARIES.md مؤجَّل (المصفوفة القانونية قائمة في المنهجية §7/§8 — قاعدة مصدر الحقيقة الواحد؛ الإنفاذ الآلي معيار قبول لأول مرحلة كود) · حذف SDK مؤجَّل
- **files changed:** التفصيل ملفاً-ملفاً في `FLUTTER_ROLLBACK_AND_OPENWEBUI_BRIDGE_HANDOFF.md`
- **decisions:** ‏ADR-0029 · ADR-0030 (كلاهما Accepted ‏2026-07-11) — ‏React baseline لم يُمس
- **risks:** بوابة الترخيص القانونية لصورة Open WebUI معلقة (لا تشغيل قبلها) · قيود branding في 0.6.6+ تمنع الترقية العمياء
- **tests:** لا كود — خطط الاختبار الثلاث (استبدال/عزل/ترقية) كمواصفات مؤجلة مربوطة بمراحلها
- **next step:** مراجعة SA للفرعين ودمجهما ثم قرار بوابة الترخيص؛ ويبقى مسار «تصميم تفعيل Phase 1» كما هو
- **do not touch:** الوسم `v1.0-architecture-baseline` · ‏superseded/** · ‏React baseline ‏(D1/ADR-0017)
- **notes for next agent:** اقرأ ADR-0029/0030 قبل أي عمل واجهات؛ الـ scaffold وثائقي — أي تشغيل يبدأ من بوابات README الخاصة به ببطاقة مهمة

## H-0013 — إغلاق مرحلة المواصفات (GATE A) — بانتظار أمر SA لـ GATE M (2026-07-11)
- **date:** 2026-07-11
- **phase:** إغلاق المواصفات — بوابة A منفَّذة كاملة؛ **بوابة M (دمج/وسم/إصدار) مقفلة حتى أمر SA الصريح: «اعتمدت — نفّذ GATE M»**
- **task:** تعديلات الإغلاق السبعة على فرعي `chore/remove-flutter-adopt-openwebui-bridge` + فحوص A2 + تقرير `SPECIFICATIONS_CLOSEOUT_HANDOFF.md` — بلا دمج
- **completed:** **A1.1 (قرار مراجعة محايد): دسترة مبدأ العميل القابل للاستبدال — المادة م23** (المبرر الكامل في ADR-0029 والتقرير؛ اختبار الاستبدال صار معيار قبول مؤجلاً) · A1.2 نموذج الهوية معمارياً (Local+SSO من اليوم الأول؛ الاختيار إعداد منصة حصراً — ملحق صف ADR-0011 + SECURITY_BOUNDARY) · A1.3 ملكية المعرفات للمنصة (محادثات/رسائل/مرفقات/مشاريع/علاقات — استبدال أي عميل بلا هجرة Backend) · A1.4 **سجل المؤجلات الرسمي** `decisions/DEFERRED_IMPLEMENTATION.md` (11 صفاً؛ أُدرج Tier-0 وفي الفهارس) · A1.5 المسح: صفر مؤجلات حرة (الجدول في التقرير) · A1.6 تطبيع بند الترخيص بالجملة المعتمدة وحدها (السجل بصفّيه + ADR-0030 + وثائق التكامل) · A1.7 خطة التخلص مكتملة (13/13 عنصراً) · فحوص A2 ‏10/10
- **not completed (مقصود — GATE M مقفل):** لا دمج · لا وسم · لا حزمة · لا Release · لا تشغيل · لا Phase 1
- **files changed:** التفصيل ملفاً-ملفاً في `SPECIFICATIONS_CLOSEOUT_HANDOFF.md` §3
- **decisions:** م23 (دستور v1.2) · ADR-0029 ‏Amended · لا مساس بأي وسم/إصدار سابق
- **risks:** قرار A1.1 قابل للنقض قبل الدمج إن رأى SA خلافه (ملفان فقط)؛ الفرعان يتقادمان إن تأخر الدمج
- **tests:** لا كود — حزمة A2 (إشارات/أسرار/روابط/تثبيت الصورة/بند الترخيص/مطابقة التقرير السابق)
- **next step:** **قراءة SA للتقرير ثم أمر «اعتمدت — نفّذ GATE M»** (أو أمر بتعديل قرار A1.1 قبله)
- **do not touch:** الوسم `v1.0-architecture-baseline` · ‏superseded/** · ‏React baseline
- **notes for next agent:** سجل المؤجلات صار Tier-0 — يُقرأ قبل أي عمل؛ لا يُنفَّذ GATE M دون أمر SA الحرفي

## H-0014 — تنفيذ GATE M بأمر SA الصريح: دمج + وسم v1.1 + إصدار (2026-07-11)
- **date:** 2026-07-11
- **phase:** إغلاق المواصفات — بوابة M (بأمر SA الحرفي: «اعتمدت — نفّذ GATE M» بعد قراءة تقرير GATE A)
- **task:** تحقق فعلي من GitHub → دمج المستودعين → وسم SPECS → حزمة → Release → تحقق شامل → ملحق الإصدار
- **completed:** تحقق ما قبل الدمج من GitHub ذاته (HEAD الفعلي: ‏specs ‏79dc987 · platform ‏4b105e3 — اعتُمدت القيم الفعلية لا المكتوبة) · **دمج SPECS** ‏`16bf80f` و**دمج PLATFORM** ‏`7e74bd3` ‏(--no-ff، ‏commits التفصيلية محفوظة، صفر تعارضات، فحوص ما بعد الدمج ناجحة) · **الوسم** `v1.1-specifications-closeout` (كائن `be25247…` → ‏`16bf80f`) مدفوعاً · **الحزمة** 550,663 بايت / 104 ملفات مطابقة للوسم · **‏SHA-256:** ‏`129b6620ffa2fddf74912492d624e6439ad9a49a9b86031a7b3e1b404c605de6` (طُوبقت بإعادة التنزيل من GitHub) · **‏Release** منشور على الوسم بالأصل والملاحظات المقررة · تحقق M6 كاملاً (v1.0 بلا مساس · لا Release/Tag في PLATFORM · لا تشغيل) · **ملحق الإصدار** §12 في `SPECIFICATIONS_CLOSEOUT_HANDOFF.md`
- **not completed (مقصود):** لا Phase 1 · لا تشغيل لأي خدمة (‏Open WebUI/Docker/SSO/مزامنة/Actions) · لا وسم/Release في PLATFORM
- **files changed:** ‏SPECIFICATIONS_CLOSEOUT_HANDOFF.md ‏(+§12) وهذا الإدخال فقط (ما بعد الوسم — توثيق لا محتوى معياري)
- **decisions:** تصديق SA على قرار A1.1 (م23) بإصدار أمر GATE M · نوع الإصدار release عادي اتباعاً لنمط v0.8 (لا Release لوسم v1.0 — الخيار موثق في §12)
- **risks:** لا مخاطر مفتوحة جديدة؛ المرجعان النافذان الآن: المعمارية `v1.0-architecture-baseline` والمواصفات المغلقة `v1.1-specifications-closeout`
- **tests:** حزمة تحقق M6 من GitHub ذاته (الدمج/الوسم/الأصل/البصمة/الروابط/سلامة v1.0)
- **next step:** **لا عمل تنفيذي — انتظار قرار SA تفعيل Phase 1** (تصميم تفعيل ببطاقة مهمة؛ المدخل: تصميم v0.3 المستعاد + دلتا v0.8)
- **do not touch:** الوسمان v1.0/v1.1 · ‏superseded/** · ‏React baseline · سجل المؤجلات إلا بقرار SA
- **notes for next agent:** اقرأ وفق Tier-0 (ومنه سجل المؤجلات)؛ مرحلة المواصفات **مقفلة** — أي تغيير معماري عبر ADR (م21)

## H-0015 — تصحيح اتساق توثيقي محدود (فئة توضيحات م21 — 2026-07-11)
- ثلاث نقاط فحص: سطر Open WebUI في README (أ: FAIL → مواءمة مع شطري م6 + إحالة ADR-0030) · عبارة الخطوة التالية (ب: README ‏FAIL → «تصميم تفعيل Phase 1» بمدخلاته الإلزامية الثلاثة والتحذير المزدوج؛ ‏roadmap ‏PASS؛ ‏phases/README صياغته قديمة — رُصد ولم يُلمس خارج القائمة البيضاء) · دلالتا المرجعين في SPEC_SOURCE ‏(ج: FAIL → فقرة توضيح قصيرة، المرساة v1.0@260780f كما هي حرفياً).
- القرار: ‏minimal documentation consistency patch completed — ‏commit واحد لكل مستودع على main مباشرة (لا مساس بأي وسم/ADR/دستور؛ ‏Phase 1 لم يبدأ).


## Handoff H-0016
- date: 2026-07-19
- phase: ‏G1 — Governance Foundation Baseline (‏G1-A: تنفيذ بلا دمج)
- task: تنفيذ البنود 1–21 من خطة تقرير v2.0 (‏sha256 ‏6ef5e106d9959ac44a628dec28fc723d42ca35ccaf98bcb4628c93959f999bfa) بأمر مالك صريح (‏G0 معتمد + قرارات Q1–Q5/DR-1/DR-2)
- goal: إيداع Governance Foundation Baseline كاملاً على فرعي عمل جاهزين للمراجعة والدمج والوسم v1.2-governance-baseline
- completed: ‏6 ملفات ADR ‏(0031–0036 ‏Proposed) · ‏Δ ‏ADR-0017/0030 · سجل adr v1.3 · ‏AUTHORITY.md · ‏INDEX.md (تغطية 100%) · طبقة contracts/ (معيار + هوية + قالب + 4 بذور Candidate + قاموس تعدادات) · ‏Capstone ‏UI_SCREEN_GOVERNANCE_STANDARD · ‏COMPONENT_STATES v1.1 ‏(+S16–S20) · ‏INVENTORY v1.4 ‏(+3 أعمدة/51 صفاً) · ‏agent-execution-model v2.0 ‏(+§§12–17) · ‏PHASE_EXECUTION_STANDARD · ‏ROCKET_OPERATING_MODEL · بذرتا knowledge/traceability · ‏open-decisions v2.4 · ‏+3 صفوف مؤجلات (مرآة Superpowers · بناء DGP · المراجعة القانونية) · ‏checklist v1.11 (تصويب v0.7.1 tag-only) · تعديلا platform ‏(AGENTS/SPEC_SOURCE)
- not completed: الدمج · الوسم v1.2-governance-baseline · ترقية ADRs إلى Accepted · دفع الفروع وفتح PRs من بيئة التنفيذ (لا اعتمادات دفع — حِزم bundles وأوامر جاهزة في تقرير التنفيذ) — كلها **G1-B بيد SA** (‏EC-12 ‏Pending Owner)
- files changed: انظر تقرير تنفيذ G1-A (قائمة كاملة ببصمات) + ‏PACKAGE_CHECKLIST §Δ G1
- decisions: لا قرارات جديدة اتُّخذت — تقنين قرارات G0 فقط؛ **صفر Decision Requests** (لم يظهر تعارض حقيقي)؛ انحرافان موثقان: ‏Archetypes ثمانية (‏Renderer-template تحقق بعمود type القائم) · جدول الجرد A ‏51 صفاً لا 52
- risks: بقاء الدفعة غير مدموجة يجمّد G2/G3؛ نص §8 القديم في أي نسخة متداولة قد يُقرأ بلا دلتا ADR-0033 — يعالجه الدمج
- tests: فحوص EC-1→EC-11 ‏scripted ناجحة (الأدلة في تقرير التنفيذ)؛ ‏EC-12 ‏Pending Owner
- next step: مراجعة SA لتقرير تنفيذ G1-A ثم الأمر: «اعتمدت G1-A — نفّذ G1-B والدمج والوسم»

## Handoff H-0017
- date: 2026-07-20
- phase: ‏G1 — Governance Foundation Baseline (‏G1-B: الدمج والترقية — جلسة GitHub موثقة بحساب SA)
- task: تنفيذ G1-B وفق برومبت v3 المعتمد بأمر المالك الصريح («اعتمدت G1-A — نفّذ G1-B والدمج والوسم»): دمج specs PR ‏#2 ثم ترقية حالات الاعتماد بهذا الـ commit
- goal: إغلاق بوابة G1 بدمج/توقيع SA وترقية أصول الدفعة من Proposed إلى Accepted تمهيداً للوسم v1.2-governance-baseline
- completed: دمج specs PR ‏#2 بإستراتيجية merge commit — ‏M1 = ‏`dd098dff9bed7a1f267ec5552b0e3366e368883d` (الأبوان `3b4c525`/`20711fe`) · ترقية الملفات الأحد عشر الحاملة لعبارة البوابة إلى «Accepted — G1-B 2026-07-20 ‏(merge M1 · ‏tag v1.2-governance-baseline)» (‏6×ADR-0031..0036 · ‏AUTHORITY · ‏Capstone · ‏PHASE_EXECUTION_STANDARD · ‏ROCKET_OPERATING_MODEL · ‏INDEX) · سجل adr ‏v1.4 (الخلايا الست Accepted) · صفوف INDEX المعنية Accepted (بذور العقود Candidate والبذرتان Seed كما هي) · خلايا Δ G1 في PACKAGE_CHECKLIST «تم — G1-B 2026-07-20» + تصويب صف README القديم من v1.2 إلى v1.3 (البند المؤجل المعلن من تقرير G1-A ‏§6-ب) · هذا الإدخال
- not completed (يُنفَّذ تالياً ضمن الجلسة ذاتها بالترتيب الملزم): الوسم v1.2-governance-baseline على main بعد دمج هذه الترقية · دمج platform PR ‏#1 · ‏micro-PR مؤشر القراءة في platform · إنشاء GitHub Release في specs حصراً
- files changed: 14 ملفاً حصراً في commit واحد: ‏6×`decisions/adr/ADR-0031..0036` · ‏`AUTHORITY.md` · ‏`ui/UI_SCREEN_GOVERNANCE_STANDARD.md` · ‏`methodology/PHASE_EXECUTION_STANDARD.md` · ‏`methodology/ROCKET_OPERATING_MODEL.md` · ‏`INDEX.md` · ‏`decisions/adr/README.md` · ‏`PACKAGE_CHECKLIST.md` · ‏`handoff/handoff.md`
- decisions: لا قرارات جديدة — تنفيذ اعتماد المالك لبوابة G1 ‏(EC-12: الدمج + الوسم + التوقيع)؛ اختيار merge commit لكل عمليات دمج هذه البوابة قرار مالك صريح باعتماد برومبت G1-B v3 ‏(§I — يُمنع squash/rebase؛ استنتاج تشغيلي لحماية سلسلة الأدلة، لا نص حوكمي قائم سابقاً)
- risks: لا مخاطر جديدة؛ الوسوم لا تُحذف — أي تصحيح بعد الدفع بوسم لاحق ‏(ADR-0033-6)
- tests: فحوص Preflight (القسم G من البرومبت) كاملة قبل أي كتابة: رؤوس D/E مطابقة حرفياً · غياب الوسم · سلالة ff · مقارنة رباعية لمحتوى الـ PRين ‏PASS · جرد عبارة البوابة = 11 ملفاً · ثم فحوص J بعد كل خطوة (بعد دمج هذه الترقية: صفر بقايا للعبارة)
- next step: إتمام الوسم ودمج platform والمؤشر ثم الـRelease ضمن جلسة G1-B ذاتها — السجل الكامل بالتقرير النهائي

## Handoff H-0018
- date: 2026-07-20
- phase: G1-C — Governance Docs Normalization (بعد تدقيق G1-B المستقل)
- task/goal: إقفال ديون التدقيق (F1–F11) وتوثيق الإغلاق النهائي لـG1 وقراري المالك.
- completed: **سجل إغلاق G1 النهائي**: M1 `dd098dff9bed7a1f267ec5552b0e3366e368883d` · M2 `a7bdcc3fa9d73b6d8bbd8543e36f94d573459ab2` · T_OBJECT `b7904c6660174dade01833d5f3036aaa4c6b5981` · T_TARGET = M2 · P1 `736b38ab54eee3b37e8c74221b7b4575128ed319` · P2 `007f57ef538f43b897181373f1f8a7462125cdc3` · Release: https://github.com/sa4devops/local-rag-enterprise-specs/releases/tag/v1.2-governance-baseline · **حكم التدقيق: ACCEPT WITH DOCUMENTATION DEBT** — تعديلات الدفعة (الملفات الستة): INDEX.md (تصويب صفوف ADR-0017/0031..0036 + إزالة انتساب (G1) الكاذب من 25 صفاً تاريخياً) · README.md v1.4 (حالة المشروع بعد إغلاق G1 + تمييز R1–R11 عن P0–P8) · PACKAGE_CHECKLIST.md v1.12 (تصويب خلية صف ADRs) · github-docs-structure.md v1.8 (+AUTHORITY.md +INDEX.md +contracts/ +knowledge/ +traceability/) · vision.md v1.1 (إحالة ترتيب السلطة إلى AUTHORITY.md) · handoff/handoff.md (هذا الإدخال H-0018)
- decisions: **قرارا مالك (2026-07-20)**: (1) مسار المصالحة **R1–R11** (أوله R1 — Current-State Baseline and Authority Verification) تمييزاً عن P0–P8 وPhase 1 — Governed Core؛ (2) **لا ترقية للعقود**: Proposed/Candidate كما هي حتى بوابة FP المختصة (`contracts/NAMING_AND_CONTRACTS_STANDARD.md §2`).
- not completed / next step: إنشاء الوسم التصحيحي `v1.2.1-governance-docs-normalization` على main بعد دمج هذا الـcommit، ثم micro-PR مؤشر القراءة في platform، ثم GitHub Release في specs حصراً — سجله النهائي في متن الـRelease وتقرير G1-C؛ وبعده: بانتظار أمر المالك الصريح لبدء R1.
- risks: v1.2 محصَّن (ADR-0033-6).
- tests: Preflight PASS + حراس H-كتلة-1.

## Handoff H-0019
- date: 2026-07-21
- phase: R1 — Requirements Reconciliation (دفعة R1-B التقنينية — جلسة GitHub موثقة بحساب SA)
- task/goal: تقنين قرارات المالك لبوابة R1-B على فرع واحد وPR رئيسي واحد (15 مساراً: 12 معدلاً + 3 جديدة) تمهيداً للتدقيق المستقل ثم الدمج والترقية والوسم والمؤشر والـRelease — إغلاق R1.
- completed (الـ15 مساراً موجزاً): **الجديدة (3):** `decisions/adr/ADR-0037-scoped-administration-model.md` (نموذج الإدارة المنطاقة) · `methodology/AI_DEV_CONTROL_PLANE.md` (قدرة Control Plane — المبادئ العشرة) · `methodology/RECONCILIATION_ROADMAP.md` (خارطة R1–R11 الرسمية). **المعدَّلة (12):** `contracts/screens/admin.workflows.md` (حقل owning_org_unit_id + قسم الإدارة المنطاقة + معيار القبول) · `contracts/NAMING_AND_CONTRACTS_STANDARD.md` (قرارا المالك: النمط المدمج + قيد التسمية القانوني) · `contracts/enums/ENUMS_DICTIONARY.md` (+scope_inheritance) · `knowledge/BUSINESS_GLOSSARY.md` (+مصطلحان) · `decisions/open-decisions.md` (+OD-ADM-1 · ملاحظة حدّية OD-ORG-1) · `decisions/DEFERRED_IMPLEMENTATION.md` (+4 صفوف R8/R9/R10) · `decisions/adr/README.md` (+صف ADR-0037 · v1.5) · `methodology/PHASE_EXECUTION_STANDARD.md` (P3 owning_org_unit_id · P4 Scoped-Admin · Foundation Gate) · `INDEX.md` (+3 صفوف · دلتا الحالات) · `PACKAGE_CHECKLIST.md` (+قسم دفعة R1-B · v1.13) · `traceability/TRACEABILITY_MATRIX.md` (+4 صفوف) · `handoff/handoff.md` (هذا الإدخال H-0019).
- decisions (تُدوَّن حرفياً — القرارات الخمسة): (1) **نمط العقود v1 المدمج داخل عقود الشاشات + فهرس أنواع موحد** — لا تفكيك لملفات مستقلة إلا عند حاجة فعلية في حزمة تطوير؛ (2) **قفل OD-ORG-1 والمنح الصريح** — الشجرة التنظيمية للتوجيه/التكليف فقط ولا تُشتق منها صلاحيات؛ الإدارة المنطاقة منحة إدارية صريحة (دور@نطاق)؛ (3) **قيم الوراثة الثلاث** `scope_inheritance` = `SELF_ONLY` افتراضاً · `SELF_AND_DESCENDANTS` صراحةً · `EXPLICIT_ORG_UNITS` — واختيار النطاق وأي تغيير عليه يُسجَّلان في سجل التدقيق؛ (4) **الوسم المعتمد** `v1.3-r1-requirements-reconciliation` (مرشح حتى انتقال الحكم بمؤشر platform)؛ (5) **الاحتفاظ بمسار R1–R11 بخارطة رسمية** منفصلة تماماً عن P0–P8.
- decisions (تُدوَّن حرفياً — القواعد السبع للأدمن المحدود، ADR-0037): (1) التقاطع الرباعي: الصلاحية = الدور × النطاق التنظيمي × الشاشة/المورد × القدرة؛ غياب أي بُعد = لا صلاحية؛ (2) المنح الإداري الصريح لا الاشتقاق التلقائي — OD-ORG-1 يبقى مقفلاً؛ (3) وراثة النطاق `scope_inheritance` بالافتراضي `SELF_ONLY`، وSELF_AND_DESCENDANTS/EXPLICIT_ORG_UNITS صراحةً، مع تسجيل الاختيار وتغييره تدقيقياً؛ (4) التسمية القانونية `owning_org_unit_id` حصراً في الوثائق الحية؛ (5) الإنفاذ والترشيح في الخادم حصراً — الواجهة عرض لا مصدر أمان؛ (6) الصلاحية الإدارية لا تمنح قراءة بيانات سجلات الإدارة (RLS/FLS مستقلة)؛ (7) معيار القبول الملزم (مثال المشتريات/HR): الأدمن المنطاق يرى ويدير نطاقه الممنوح فقط بلا تسرب لشاشات غير ممنوحة ولا قراءة بيانات إدارته.
- not completed (مقصود — بانتظار الجزء 2 بعد H-HALT): لا دمج للـPR الرئيسي · لا ترقية · لا وسم · لا micro-PR مؤشر platform · لا Release · لا Phase/FP.
- next step: بعد دمج SA للـPR الرئيسي وتدقيقه المستقل: طلب دمج مستقل لترقية بوابة R1-B إلى Accepted، ثم الوسم `v1.3-r1-requirements-reconciliation` على الناتج (مرشح)، ثم micro-PR مؤشر platform (بدمجه ينتقل الحكم)، ثم Release في specs يسجل ويثبت — السجل النهائي بتقرير R1-B.
- risks: v1.2 وv1.2.1 محصّنان قطعياً (وسوماً وReleases) — لا حذف/نقل/تعديل؛ اسم الوسم claimed لا published حتى انتقال الحكم.
- tests: Preflight PASS + حراس كتلة H (EXPECTED_MAIN · صفر بقايا للرموز النائبة تاريخاً وتعويضَ شِل · صفر تسريب v1.3-r1 خارج handoff · جرد عبارة البوابة = 10 · owning_org_unit_id≥2 · صفر owning_unit_id · SELF_ONLY/EXPLICIT_ORG_UNITS · R11 · Foundation Gate).
- do not touch: v1.2-governance-baseline · v1.2.1-governance-docs-normalization (وسوماً/أهدافاً/Releases) · constitution.md · AUTHORITY.md · H-0016..H-0018.

## Handoff H-0020
- date: 2026-07-22
- phase: R1-C — System-Wide Administration Boundary (دفعة توثيقية واحدة — جلسة GitHub موثقة بحساب SA)
- task/goal: توضيح حدّ ADR-0037 بقرار مالك محسوم — تمثيل الأدمن الشامل داخل النموذج — عبر ADR-0038 على فرع واحد وcommit واحد وPR رئيسي واحد (10 مسارات: 1 جديد + 9 معدَّلة) تمهيداً للتدقيق المستقل ثم الدمج والترقية والوسم والمؤشر والـRelease.
- completed (10 مسارات موجزاً): **الجديد (1):** `decisions/adr/ADR-0038-system-wide-administration-boundary.md` (حدّ الإدارة الشاملة). **المعدَّلة (9):** `decisions/adr/ADR-0037-scoped-administration-model.md` (سطر «مُوضَّح بـ ADR-0038» فقط) · `decisions/adr/README.md` (+صف ADR-0038 · v1.6) · `contracts/enums/ENUMS_DICTIONARY.md` (ملاحظة حدّ الشامل على scope_inheritance) · `knowledge/BUSINESS_GLOSSARY.md` (+مصطلح الإدارة الشاملة) · `contracts/screens/admin.workflows.md` (جملة حدّ الإدارة الشاملة في قسم الإدارة المنطاقة) · `INDEX.md` (+صف ADR-0038 · الإجمالي 122 · دلتا الحالات) · `PACKAGE_CHECKLIST.md` (+قسم دفعة R1-C · v1.14) · `traceability/TRACEABILITY_MATRIX.md` (+صفان) · `handoff/handoff.md` (هذا الإدخال H-0020).
- decisions (تُدوَّن حرفياً): (1) **الإدارة الشاملة دور مستقل قائم بذاته** (System-Wide Administrator) لا قيمة في تعداد `scope_inheritance` ولا تُمنح عبر نموذج الإدارة المنطاقة؛ (2) **لا قيمة رابعة في التعداد** — يبقى بثلاث قيم ويسري على المنح المنطاقة فقط؛ يُمنع أي قيمة تعني «كل الوحدات»؛ (3) **لا تصعيد ضمني** — لا يتحول المنطاق إلى شامل بتراكم المنح؛ (4) **الصلاحية الإدارية ≠ قراءة البيانات** للنوعين؛ (5) **الإنفاذ الخادمي حصراً** للنوعين؛ (6) كون الدور شاملاً يستوفي البُعد التنظيمي وحده — الشاشة والقدرة تبقيان بُعدين صريحين؛ (7) منح الدور الشامل قرار استثنائي صريح مسجَّل بالتدقيق عند المنح وكل تعديل/سحب.
- not completed (مقصود — بانتظار الجزء 2 بعد H-HALT): لا دمج للـPR الرئيسي · لا ترقية · لا وسم · لا micro-PR مؤشر platform · لا Release · لا Phase/FP · لا R2–R11.
- next step: ترقية ADR-0038 إلى Accepted بطلب دمج مستقل، ثم الوسم `v1.3.1-system-wide-admin-boundary` على الناتج (مرشح)، ثم micro-PR مؤشر platform (بدمجه ينتقل الحكم)، ثم Release في specs يسجل ويثبت — والتفصيل التنفيذي لنوعَي المنح = مسار R4 → بوابة P4.
- risks: v1.2 وv1.2.1 وv1.3-r1-requirements-reconciliation محصَّنة قطعياً (وسوماً وReleases) — لا حذف/نقل/تعديل؛ اسم الوسم claimed لا published حتى انتقال الحكم.
- tests: Preflight PASS + حراس كتلة H (EXPECTED_MAIN=10 · صفر بقايا للرموز النائبة تاريخاً وتعويضَ شِل · صفر تسريب لاسم وسم R1-C خارج handoff · جرد عبارة البوابة = 6 · ADR-0038 في ADR-0037 · System-Wide في ADR-0038 · SELF_ONLY≥1 · git diff --check).
- do not touch: v1.2-governance-baseline · v1.2.1-governance-docs-normalization · v1.3-r1-requirements-reconciliation (وسوماً/أهدافاً/Releases) · constitution.md · AUTHORITY.md · H-0016..H-0019.

## Handoff H-0021
> **مُصحَّح 2026-07-25 (يتجاوز النص الذي نشره commit `5bb7dc0`).** commit `5bb7dc0` باقٍ في تاريخ Git بلا إعادة كتابة؛ هذه الصيغة تتجاوز ادعاءاته غير الدقيقة.
- date: 2026-07-25
- phase: R2 — Historical Drafts Delta Reconciliation (تفعيل R2) + **أرشفة حزمة RAR المتحقَّق منها** — دفعة P3 · **P3 غير مكتملة · المصالحة معلّقة · §13b PENDING** (L1 · فرع + PR بلا دمج)
- task/goal: تفعيل R2 (خارطة v1.1) + **أرشفة حزمة RAR** بمسار SA المعتمد + MANIFEST + تغطية EC-3 + **تصحيح سجل commit 5bb7dc0** + تعليق §13b. مصالحة RAR (§10.4) **لم تبدأ** في هذه الجولة.
- base SHA: `52fbde1f027f0ffcd3e9376e7f3fdc1216068515` (= origin/main).
- **هوية الوسم (تصحيح §9):** `v1.3.1-system-wide-admin-boundary` = **annotated tag object** `ba6db35bb1b801191b2bddc4b11f6a965a2093f2`؛ و**peeled commit** `v1.3.1^{}` = `52fbde1f027f0ffcd3e9376e7f3fdc1216068515` = **baseline/main HEAD نفسه**. الوسم يشير إلى HEAD، **وليس سلفاً مختلفاً عنه** — وبذلك يُصحَّح الوصف السابق الذي جعل الوسمَ سابقاً للـHEAD.
- completed: تفعيل R2 + ترقية `RECONCILIATION_ROADMAP.md` v1.1 (Δ مُصحَّح) · **أرشفة الملفات الثمانية بايتياً** في `references/analysis-inputs/rar-2026-07/` + `MANIFEST.md` (ترويسة المجلد؛ تحذير اللاحاكمية الحرفي + بصمات فردية ومجمّعة قابلة لإعادة الإنتاج؛ المجلد **9 ملفات بالضبط**) · تغطية EC-3 لـ9 ملفات في `INDEX.md` (122→131 + الفهرس = **132**؛ **صفر غير مغطى**؛ بتجاوز مالك محدود مؤرَّخ) · هذا التصحيح.
- **الحقيقة المصححة (تتجاوز commit 5bb7dc0):** (1) حزمة RAR **موجودة كمدخل تحليلي تاريخي**؛ (2) لم تتوفر نسخة دائمة منها داخل filesystem/Git الذي فحصته جولة Claude Code السابقة؛ (3) تقرير البحث السابق كان صحيحاً **فقط ضمن المواقع المفحوصة**؛ (4) لم يُثبت ذلك التقرير أنها لم توجد أو لم تُسلَّم تاريخياً؛ (5) استُعيدت من مكتبة ملفات ChatGPT بتاريخ 2026-07-25؛ (6) تُحقِّق من الملفات الثمانية (اسم · حجم · بصمات فردية ومجمّعة) قبل الأرشفة؛ (7) **لا يمكن إثبات** أن البايتات المسترجعة هي عين بايتات جلسة 2026-07-22 (لا رقم/تاريخ إصدار داخلي)؛ (8) حكمُ «عدم التسليم» في 5bb7dc0 **متجاوَز** ولا يُعامل حكماً نافذاً — دون استبداله بادعاء تاريخي جديد غير مثبت.
- **§13b (تجاوز مالك مؤقت مؤرَّخ 2026-07-25):** `PENDING — TO BE DETERMINED FROM THE COMPLETED RAR RECONCILIATION TABLE`. معناها: (1) تجاوز إجرائي مؤقت **لا حكم نهائي ثالث دائم**؛ (2) **لا يجوز** إعلان `NO BLOCKING DELTA` ولا `BLOCKING DELTA DETECTED` (هذا نفيٌ لهما لا إعلانٌ لأحدهما)؛ (3) لا يُستنتج من غياب الفحص؛ (4) الحكم النهائي يُحسب من جدول المصالحة المكتمل؛ (5) **لا يجمّد تلقائياً** P4/P6/P8/P9/P10/P12 (مقايضة واعية مقصودة)؛ (6) قد تُنتج المصالحة لاحقاً blocking delta تمسّ مساراً سبق فتحه، وعندها تُطبَّق §18 من لحظة الإثبات؛ (7) أمر الجولة الحالية **لا يخوّل** بدء أو تنفيذ أي مسار لاحق؛ (8) أي dependency صريح مستقل على إغلاق P3 يبقى نافذاً.
- **الجملة الختامية (قرار SA مؤرَّخ 2026-07-25 يتجاوز أي جملة سابقة من 5bb7dc0):** الإغلاق المخفَّض السابق **متجاوَز**؛ حزمة RAR **استُعيدت وتُحقِّق منها وأُرشِفت**؛ مصالحة RAR **لم تبدأ وما زالت معلّقة**؛ §13b **PENDING**؛ **P3 غير مكتملة**؛ PR #9 يبقى **مفتوحاً وغير جاهز للدمج**؛ **لا merge/tag/release/P4** من هذه الجولة.
- not completed: **مصالحة RAR (§10.4) لم تبدأ** · لا استخراج/تصنيف §11/§12/§14 · لا merge · لا tag · لا release · لا P4 · لا تعديل deferred register / agent-execution-model / سياسة INDEX-EC3.
- decisions: تجاوزات مالك مؤرَّخة (2026-07-25) ضمن أمر SA التصحيحي: (1) اعتماد مسار الأرشفة `references/analysis-inputs/rar-2026-07/`؛ (2) `MANIFEST.md` = ترويسة المجلد (تفسير مالكي لـ§10.3b)؛ (3) تعديل `INDEX.md` بالحد الأدنى لـEC-3؛ (4) §13b PENDING مؤقت. لا ADR جديد · لا قرار معماري.
- next step: أمر SA لبدء مصالحة RAR (§10.4) على نفس الفرع/الـPR، ثم حساب §13b النهائي من الجدول المكتمل.
- tests: EC-3 = **132/132 · 0 غير مغطى** · byte-identity 8/8 · aggregate MATCH (`294e8cd6…`) · لا بوابات آلية (مُعاد التحقق 2026-07-25) · `git diff --check` نظيف · لا أسرار · لا آثار macOS في الأرشيف.
- do not touch: constitution.md · AUTHORITY.md · decisions/adr/** · contracts/** · superseded/** · ui/** · phases/** · catalogs/** · decisions/DEFERRED_IMPLEMENTATION.md · methodology/agent-execution-model.md · سياسة INDEX/EC-3 · الوسوم v1.0..v1.3.1 · H-0016..H-0020. (INDEX.md عُدِّل هذه الجولة بتجاوز مالك محدود لـEC-3 فقط.)

## Handoff H-0022
> **Phase Completion Assurance — شق P3 Closure Inventory.** يُقرأ بعد `H-0021` ولا ينسخه: `H-0021` صحيحٌ في تاريخه (2026-07-25) لكنه **متقادم** — كان يعلن «المصالحة لم تبدأ · §13b PENDING»، وقد اكتملت المصالحة (260/260) وحُسمت §13b منذ ذلك التاريخ. **لا إعادة كتابة لأي مدخل سابق.**
- date: 2026-07-30
- phase: P3 — Phase Exit Review · **P3 Closure Inventory** (‏Remainder Census + تسجيل حاكم) — L1 · فرع PR #9 نفسه بلا دمج
- task/goal: جرد كل التزامات P3 من المستودع الفعلي، وتصنيفها ثلاثياً، وتسجيل كل `GOVERNED TRANSFER` في **وعائه الحاكم** — تنفيذاً لقرار المالك: «لا يجوز الاعتماد على ذاكرة المالك أو أي مساعد لتذكّر التوصيات والقرارات والالتزامات لاحقاً». **لا تنفيذ لأي التزام** في هذه الدفعة.
- base SHA: `52fbde1f027f0ffcd3e9376e7f3fdc1216068515` (= `origin/main`) · **PR #9 head قبل الدفعة:** `f6ec1f33ed98fe02229e5614e7707a5c8d93c557`.
- **القاعدة المركزية (شق مستقل):** `methodology/PHASE_EXECUTION_STANDARD.md` **§3 Phase Exit Review** أُنشئت في **PR مستقل** على فرع مستقل من `main` (‏`docs/phase-exit-review-standard`) — لأن ملفاتها (`methodology/PHASE_EXECUTION_STANDARD.md` · `phases/**`) **خارج مجموعة ملفات PR #9 كلياً** (تقاطع = صفر، وهما متطابقان بايتياً بين `main` ورأس PR #9). **لم يُلمس أي ملف من PR #9 في ذلك الشق، ولم يُلمس أي ملف من ذلك الشق هنا.**
- completed: `traceability/rar-reconciliation/P3-CLOSURE-INVENTORY.md` (جرد تفصيلي **غير حاكم** — وثيقة إحالة) · تسجيل حاكم في `decisions/open-decisions.md` (v2.5 → **v2.6**: «فهرس ترحيل إغلاق P3» + `OD-GOV-1..3` مفتوحة + تأكيدات ترحيل على `OD-P3-2` والحدّ المؤسسي) · صف جديد في `decisions/DEFERRED_IMPLEMENTATION.md` (حماية مسار أرشيف RAR في `agent-execution-model` §9) · قيد Δ في `methodology/RECONCILIATION_ROADMAP.md` (v1.1 → **v1.2**) · تغطية EC-3.
- **نتيجة Remainder Census:** `Total = 25` = `COMPLETE 9` + `GOVERNED TRANSFER 13` + `BLOCKING REMAINDER 3` · **`UNCLASSIFIED = 0`** · المعادلة متوازنة.
- **`BLOCKING REMAINDER` — يمنع إغلاق P3 (3):** (1) **§18 لم تُنفَّذ** — تطبيق خريطة الحجب على `FP-0001` بأمر مستقل؛ (2) **الدلتا السبعة** `RAR-003 [38] [40] [42] [43] [44] [46] [48]` — وعاء أثر حجبها هو مخرج §18 نفسه، ووجهتها التقنينية `R3` غير مُفعَّلة؛ (3) **تسجيل النطاق المتأثِّر** بـ`FP-0001` (تسمّيه الحزمة `P12` ولا ملف بهذا الرقم في المستودع). **لا يجوز إعلان إغلاق P3 مع بقاء أيٍّ منها.**
- **خطوات المالك الصريحة اللازمة للإغلاق (لا تختفي من السجل):** (1) إصدار **أمر §18** المستقل وتنفيذه ومراجعته؛ (2) **دمج PR القاعدة العامة** (‏`docs/phase-exit-review-standard`) في `main` — قيدٌ مسجَّل لأن §3 معيار الخروج نفسه ولا ينفذ قبل الدمج (المرتبة 2)؛ (3) بعدهما وبعد بلوغ `BLOCKING REMAINDER = 0`: **قرار إغلاق P3 → قرار الدمج → الوسم → الإصدار** — كلها **سلطة مالك حصراً**.
- **تجاوز مالك مسجَّل (‏B1 §20) — توسعة `GATE-DEFINITION`:** أُضيف `GATE-DEFINITION` نطاقاً مرشحاً للحجب ثم حكماً نهائياً بتجاوز مالك صريح مؤرَّخ. **يُسجَّل هنا لأول مرة في وعاء حاكم** (كان مسجَّلاً في `B1-CHECKPOINT-REPORT` غير الحاكم ووصف PR #9 فقط). نتيجته النهائية: **`لا حجب` على `GATE-DEFINITION`** — سقط المرشح إلى ملاحظة توثيقية + قيد مؤجَّل. **لا ADR لهذه التوسعة.**
- **تحفّظ الأرشيف المحلي (قيد تدقيق):** `out/P3/**` وZIP الأدلة التصحيحية المحلي **خارج Git · غير متعقبَين · لا يراهما مدقق بعيد**، ولا يُعوَّضان بالمخرجات المتعقبة. أي تعقّب لأي جزء منهما يحتاج **قرار مالك صريح**؛ وإدخال ZIP أو ملفات محلية إلى Git يبقى محظوراً. **لا يُقرأ غيابُهما اكتمالاً.**
- **متبقّي خارج P3 (مسجَّل لا مُنفَّذ):** متبقّي جولتَي **P1** و**P2** الحوكميّتين يعيش **حصراً في تقارير محلية غير متعقبة**، ومنه **`P2 — OWNER_DECISION_PACKAGE`** المنتظِر قرار مالك بشأن مساحة الأسماء. **لا يخص P3 ولا يمنع إغلاقها**، ومالكُه **دفعة مخوَّلة مستقلة** تطبّق `PHASE_EXECUTION_STANDARD.md` §3 على P1 و P2. جردُه الكامل **لم يُنفَّذ هنا**.
- **`GOVERNED TRANSFER` (13) — أوعيتها:** `decisions/open-decisions.md` (الحدّ المؤسسي · `OD-P3-2` · `OD-GOV-1` · `OD-GOV-2` · `OD-GOV-3`) · `decisions/DEFERRED_IMPLEMENTATION.md` (توصية `agent-execution-model` §9) · `methodology/RECONCILIATION_ROADMAP.md` قيد Δ (‏39 دلتا باقية بوجهاتها · 32 صف `RAR-004` مدخلاتِ جاهزية R10 · قيد إغلاق P3) · وهذا المدخل `H-0022` (تجاوز `GATE-DEFINITION` · خطوات المالك · تحفّظ الأرشيف المحلي · متبقّي P1/P2 · الـdependency). **وجودُ أي عنصر في `traceability/**` وحده لا يُعدّ نقلاً حاكماً.**
- **تصحيح نطاق مقابل `H-0021`:** قائمة «do not touch» في `H-0021` كانت قيد **تلك** الجولة وتضمّنت `decisions/DEFERRED_IMPLEMENTATION.md` و`phases/**`. **أمر المالك الصادر 2026-07-30 يخوّل صراحةً**: تسجيل عنصر في سجل المؤجلات (وفق قاعدته «لا يُضاف إليه عنصر إلا بقرار جديد من SA»)، وتعديل `phases/**` **في الشق العام على فرعه المستقل فقط**. لا تعارض صامتاً.
- not completed: **§18 لم تُطبَّق** · الدلتا السبعة **لم تُعالَج** · `FP-0001` لم يُعدَّل · **Gate Criteria لم تُعدَّل** · `OD-P3-2` **لم يُغلق** · `OD-GOV-1..3` **لم تُحسم** · لا قرار `tenant`/`org_unit` · `AUTHORITY.md` **لم يُعدَّل** · لا ADR جديد · `superseded/**` لم يُلمس · لم تُنشأ ملفات P9–P12 · لم تبدأ R3 ولا R4 ولا R10 ولا P4 ولا P5 · **P3 لم تُغلق** · لا merge ولا tag ولا release · لا فرع ولا PR جديد في هذا الشق.
- decisions: لا قرار معماري ولا ADR. تسجيلٌ حاكم فقط لعناصر كانت تعيش في تقارير غير حاكمة؛ و`OD-GOV-1..3` **مفتوحة** لا محسومة. `AUTHORITY.md` لم يُمسّ — ولذلك بقي `GOV-OBS-01` قيداً مفتوحاً بدل حلّه.
- tests: EC-3 = **156/156 · صفر غير مغطى** (‏155 → 156 بإضافة ملف الجرد) · معادلة الجرد متوازنة (`25 = 9 + 13 + 3` · `UNCLASSIFIED = 0`) · صفر تقاطع ملفات بين الشق العام وPR #9 · مراسي الغياب **111** وصفر مرجع مكسور (بلا تغيير) · البصمات الأربع لخط الأساس المجمَّد `188ad379d04b07ca9e1b4eeee38dc68ecca29914` **byte-identical** (بلا تغيير) · جدول §10.4 **260** والتوزيع **116/80/46/18/0** بلا تغيير · `git diff --check` نظيف · worktree نظيف بعد الدفع · لا أسرار · لا آثار macOS · لا ZIP ولا ملف محلي دخل Git.
- next step: **أمر §18 المستقل** على النطاق الممسوس `FP-0001` (‏`handoff/handoff.md` H-0021 بند 6 · `B1-CHECKPOINT-REPORT.md:87`)، **بالتوازي مع** قرار المالك في دمج PR القاعدة العامة. **بعدهما فقط** يُعاد تقييم إغلاق P3 وفق `PHASE_EXECUTION_STANDARD.md` §3.
- do not touch: constitution.md · AUTHORITY.md · decisions/adr/** · contracts/** · superseded/** · ui/** · catalogs/** · methodology/agent-execution-model.md · `references/analysis-inputs/rar-2026-07/**` · جداول المصالحة السبعة وتصنيفاتها ووجهاتها · `FINAL-B-13B-DETERMINATION.md` · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.3.1 · H-0016..H-0021.

## Handoff H-0023
> **تنفيذ §18 — أثر حجب فعلي محدود على `FP-0001`.** يُقرأ بعد `H-0022` ولا ينسخه: `H-0022` صحيحٌ في تاريخه (2026-07-30) لكن بندَه «`BLOCKING REMAINDER` — يمنع إغلاق P3 (3)» **متجاوَزٌ الآن** بصدور أمر §18 وتنفيذه. **لا إعادة كتابة لأي مدخل سابق.**
- date: 2026-07-30
- phase: P3 — **§18 GOVERNED NARROW-FREEZE EXECUTION** — L1 · فرع PR #9 نفسه بلا دمج
- task/goal: تنفيذ **§18** على النطاق الممسوس `FP-0001` بعد ثبوت `§13b: DETERMINED — BLOCKING DELTA DETECTED`، وتسجيل أثر الحجب ومكوّناته الأربعة في أوعية حاكمة. **لا معالجة لأي دلتا · لا كتابة لأي معيار · لا إغلاق لـP3.**
- base SHA: **`origin/main` = `7611ed9531660f5f4762f3e6a60f05cdf0f419b4`** (بعد دمج **PR #10** — `docs/phase-exit-review-standard` — فصار `PHASE_EXECUTION_STANDARD.md` **§3 Phase Exit Review** نافذاً على `main`؛ الأب الأول `52fbde1f…` والثاني `e999c01c…`) · **رأس PR #9 قبل الدفعة:** `f70e41138b49c247880cf1ed95e1606d4d22a3e1`.
- **خطية الفرع (قيد نافذ):** **لم يُدخَل `main` إلى فرع PR #9** · لا merge commit · لا rebase · لا force-push · لا نسخ لتغييرات PR #10 · وكل commit جديد **بأبٍ واحد**. تقاطع الملفات بين شقّ PR #10 (`methodology/PHASE_EXECUTION_STANDARD.md` · `phases/**`) وهذه الدفعة = **صفر**. **وراثة §3 تتحقق عند دمج PR #9 لاحقاً إلى `main`**، و§18 **لا تحتاج** استهلاك نص §3 داخل ancestry الفرع كي تُنفَّذ (التبعية مسجَّلة في `H-0022` وقيد Δ الخارطة).
- **قرار المالك المنفَّذ:** **`ACTUAL NARROW FREEZE`** — تجميد فعلي **محدود** لقبول بوابة `FP-0001` وكل اعتماد قائم على اجتيازها، **دون** تجميد المشروع ولا أي مرحلة P ولا أي مسار R ولا التحليل ولا العمل التحضيري ولا مسار رفع الحجب.
- completed: **§18 نُفِّذت** — `decisions/open-decisions.md` (v2.6 → **v2.7**: قسم «سجل أثر الحجب §18 — بوابة `FP-0001`» + **`OD-FP-0001-FREEZE`** بحالة **`ACTIVE`** + جدول الدلتا السبعة بحقولها التسعة) · `decisions/DEFERRED_IMPLEMENTATION.md` (صف جديد لتقنين المعايير السبعة — وجهته **R3**) · `methodology/RECONCILIATION_ROADMAP.md` (v1.2 → **v1.3** قيد Δ) · `traceability/rar-reconciliation/SECTION-18-BLOCKING-EFFECT.md` (**غير حاكم** — وثيقة إحالة) · تحديث `P3-CLOSURE-INVENTORY.md` · تغطية EC-3 (**156 → 157**) · هذا المدخل.
- **المكوّنات الأربعة المسجَّلة:** (1) **Blocking Effect:** `FP-0001 = BLOCKED` · بوابة **`FAIL-CLOSED`** · نوع الأثر **`ACTUAL NARROW FREEZE`** · تفعيل **2026-07-30** · حالة **`ACTIVE`**؛ (2) **الدلتا السبعة** `RAR-003 [38][40][42][43][44][46][48]` بمصادرها ومراسيها ووجهتها الثابتة **R3** واختبارها ودليل إغلاقها وأثر بقائها؛ (3) **النطاق المتأثِّر:** «بوابة `FP-0001` نفسها وكل قبول أو إعلان جاهزية أو اعتماد لاحق يشترط اجتيازها» — **بلا استخدام `P12`** (لا ملف ولا مرحلة بهذا الرقم؛ `phases/designs/**` ينتهي عند `phase-8`) ولا اختراع مرحلة؛ (4) **شروط الرفع السبعة** — ولم يُرفع شيء.
- **الوعاء الحاكم — سنده:** `PHASE_EXECUTION_STANDARD.md` §3.4 يوجب أن يكون وعاء أثر الحجب هو «الوعاء الذي يحدده النص الحاكم للبوابة المعنية»؛ ونصّ بوابة الأساس **لا يسمّي وعاءً**، فحدّده أمر المالك ضمن `decisions/open-decisions.md` (المرتبة 4) وسجل المؤجلات وقيد الخارطة (المرتبة 2) وهذا المدخل (المرتبة 9). **لم يُنشأ وعاء حاكم جديد · `AUTHORITY.md` لم تُمسّ · نص بوابة `FP-0001` و`Gate Criteria` لم يُمسّا** (الأثر **مشتقٌّ** من الخطوة 5 ومن «لا يُعلن Core قبل اجتياز البوابة كاملة»، لا استثناءٌ منهما).
- **نصّ §18 ذاته:** **غير موجود في المستودع** — كل ما فيه إحالات إليه بوصفه خطوة لاحقة مشروطة؛ ومضمون الخريطة صدر عن المالك في **أمر 2026-07-30**. **لم يُخترع منه شيء**، ولم يُستعمل §18 الوارد في وثائق `RAR` (وهو «الأسئلة المعمارية المفتوحة» — **غير حاكم ومحظور تنفيذه** بنص `MANIFEST.md:73`).
- **نتيجة Remainder Census بعد §18:** `Total = 26` = **`COMPLETE 11`** + **`GOVERNED TRANSFER 15`** + **`BLOCKING REMAINDER 0`** · **`UNCLASSIFIED = 0`** · المعادلة متوازنة. (قبل الدفعة: `25 = 9 + 13 + 3`.) `P3-CI-01` و`P3-CI-03` ⇒ **`COMPLETE`** · `P3-CI-02` ⇒ **`GOVERNED TRANSFER`** · وأُضيف **`P3-CI-26`** (رفع أثر §18 لاحقاً) **`GOVERNED TRANSFER`** حتى لا يعيش التزام الرفع في الذاكرة.
- **`BLOCKING REMAINDER = 0` لا يعني إغلاق P3:** إغلاق P3 **قرار مالك مستقل لم يُتخذ** ولم يُؤذَن به في هذا الأمر؛ ويبقى `P3-CI-13` (‏merge/tag/release) **حاجباً لأي إعلان اكتمال**، و`OD-FP-0001-FREEZE` **`ACTIVE`**، و`OD-GOV-1..3` **مفتوحة**.
- **`OD-GOV-3` (لم يُنفَّذ — إثبات مسجَّل):** مخرجات المصالحة **ليست حالياً** ضمن Reading Sets التي يستهلكها المنفِّذ؛ **قد لا يرى** منفِّذُ تقنين الدلتا هذه الدلتا؛ **معالجة `OD-GOV-3` تسبق** التنفيذ الفعلي لمسار التقنين؛ **§18 لا تعالج الفجوة**؛ **والعمل التحضيري لإصلاحها مسموح** رغم التجميد. **لم تبدأ R3.**
- **الطبيعة التاريخية المجمَّدة — لم تُمسّ:** `FINAL-B-13B-DETERMINATION.md` · `FINAL-RECONCILIATION-TABLE.md` · `RECONCILIATION-RAR-001..007.md` **byte-identical**؛ جدول §10.4 = **260**؛ التوزيع = **`116/80/46/18/0`**؛ خط الأساس المجمَّد `188ad379d04b07ca9e1b4eeee38dc68ecca29914` لم يُعَد فتحه؛ حكم §13b **لم يُعَد حسابه ولم يتغيّر**. **ورفع الأثر لاحقاً ليس إعادة كتابة للتاريخ** — يرفع الأثر ولا يُبطل الحكم.
- not completed: **الدلتا السبعة لم تُعالَج** · **المعايير السبعة لم تُكتب** · `FP-0001` لم يُعدَّل · **Gate Criteria لم تُعدَّل** · Reading Sets لم تُصلَح و`OD-GOV-3` لم يُنفَّذ · **لم تبدأ R3** ولا R4 ولا P4 ولا R10 · لم تُنشأ ملفات P9–P12 · `OD-P3-2` لم يُغلق · `OD-GOV-1..3` لم تُحسم · لا قرار `tenant`/`org_unit` · `AUTHORITY.md` لم يُعدَّل · لا ADR جديد · `superseded/**` لم يُلمس · **P3 لم تُغلق** · **لا merge ولا tag ولا release** · لا فرع ولا PR جديد.
- decisions: قرار مالك واحد منفَّذ — **`ACTUAL NARROW FREEZE`** على `FP-0001` (مسجَّل `OD-FP-0001-FREEZE`). لا قرار معماري ولا ADR. **لم يُحسم أيٌّ من `OD-GOV-1..3` ولا `OD-P3-2`.**
- tests: `origin/main` = `7611ed9…` وPR #10 `MERGED` · §3 نافذة على `main` (‏`## §3 Phase Exit Review` موجود) · الفرع **لم يستوعب `main`** (`git merge-base --is-ancestor origin/main HEAD` = خطأ ⇒ غير مستوعَب) · commit الدفعة **بأبٍ واحد** · `git rev-list --merges origin/main..HEAD` = **0** · معادلة الجرد متوازنة (`26 = 11 + 15 + 0` · `UNCLASSIFIED = 0`) · جدول §10.4 **260** والتوزيع **116/80/46/18/0** بلا تغيير · بصمات `FINAL-B` و`FINAL-TABLE` و`RECONCILIATION-RAR-001..007` **مطابقة قبل/بعد** · `AUTHORITY.md` و`methodology/PHASE_EXECUTION_STANDARD.md` **مطابقان** · EC-3 = **157/157 · صفر غير مغطى** · مراسي الغياب **111** وصفر مرجع مكسور · `git diff --check` نظيف · worktree نظيف بعد الدفع · PR #9 **`OPEN — NOT MERGED`** · لا وسم جديد ولا إصدار جديد · لا أسرار · لا آثار macOS · لا ZIP ولا ملف محلي دخل Git.
- next step: **قرار مالك** — إمّا (أ) **أمر تفعيل `R3`** لتقنين المعايير السبعة (ويسبقه أو يرافقه حسمُ `OD-GOV-3` حتى تصل الدلتا إلى المنفِّذ)، وإمّا (ب) **إعادة تقييم إغلاق P3** وفق `PHASE_EXECUTION_STANDARD.md` §3 مع بقاء `OD-FP-0001-FREEZE` **`ACTIVE`**. **رفع التجميد لا يقع إلا بالشروط السبعة المسجَّلة وبدليل حاكم.**
- do not touch: constitution.md · AUTHORITY.md · decisions/adr/** · contracts/** · superseded/** · ui/** · catalogs/** · phases/** · methodology/agent-execution-model.md · **methodology/PHASE_EXECUTION_STANDARD.md** (نصّ البوابة و§3 — شقّ PR #10) · `references/analysis-inputs/rar-2026-07/**` · جداول المصالحة السبعة وتصنيفاتها ووجهاتها · `FINAL-B-13B-DETERMINATION.md` · `FINAL-RECONCILIATION-TABLE.md` · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.3.1 · H-0016..H-0022.

## Handoff H-0024
> **معالجة `OD-GOV-3` — إيصال مصدر المصالحة والدلتا إلى Reading Set منفِّذ `R3` + استكمال تتبّعية §18.** يُقرأ بعد `H-0023` ولا ينسخه: `H-0023` صحيحٌ في تاريخه، لكن بندَه «`OD-GOV-3` (لم يُنفَّذ — إثبات مسجَّل)» (‏`:493`) **متجاوَزٌ الآن**. **لا إعادة كتابة لأي مدخل سابق.**
- date: 2026-07-31
- phase: P3 — **OD-GOV-3 READING-SET DELIVERY AND §18 TRACEABILITY COMPLETION** — L1 · فرع PR #9 نفسه بلا دمج
- task/goal: إيصال **مصدر المصالحة والدلتا** إلى مجموعة القراءة التي يستهلكها منفِّذ `R3`، وإغلاق `OD-GOV-3` إن ثبت الوصول؛ + ثلاثة تصحيحات توثيقية: تجميع حقول §3.4 لـ`P3-CI-02` و`P3-CI-26`، وتدقيق إحالات الخطوتين 1 و5، وتسجيل `GOV-OBS-03`. **لا بدء لـR3 · لا معالجة لأي دلتا · لا رفع للتجميد · لا إغلاق لـP3.**
- base SHA: **`origin/main` = `7611ed9531660f5f4762f3e6a60f05cdf0f419b4`** (بلا تغيير) · **رأس PR #9 قبل الدفعة:** `bdd5929825e5050d7cb8b39ffcdae8e07e81c3cf`.
- **خطية الفرع (قيد نافذ):** **لم يُدخَل `main` إلى فرع PR #9** · لا merge commit · لا rebase · لا force-push · commit الدفعة **بأبٍ واحد** هو `bdd5929…`. تقاطع ملفات هذه الدفعة مع شقّ PR #10 (`methodology/PHASE_EXECUTION_STANDARD.md` · `phases/**`) = **صفر** — فلم يُمسّ أيٌّ منهما.
- **الجذر المكتشَف (‏Root cause):** مصفوفة القراءة `methodology/agent-execution-model.md` §9 (`:56`..`:63`) لها **ثلاثة صفوف**: Tier-0 (`:59`) · «لكل مرحلة» (`:60`) · «لكل مهمة» (`:61`). وصفُّ «لكل مرحلة» مُفتاحُه **مرحلة**، بينما `methodology/RECONCILIATION_ROADMAP.md:5` ينصّ على أن مسار R «**منفصل تماماً** عن مراحل تطوير المنتج P0–P8»؛ ولا ذكر لأي «مسار R» في `agent-execution-model.md`. ⇒ **منفِّذ `R3` يسقط من المصفوفة** فلا يستهلك إلا Tier-0 + بطاقة المهمة، ومصدر المصالحة خارج كليهما.
- **أقل تغيير صحيح حاكمياً (المنفَّذ):** أُنشئ قسم **«مجموعة قراءة مسار `R3`»** داخل `decisions/open-decisions.md` (المرتبة 4) — **وهو ملف Tier-0 إلزامي** بنص `agent-execution-model.md:59` ⇒ الوصول مضمون **لكل** منفِّذ محتمل **بلا تعديل مصفوفة القراءة**. القسم يحمل **12 إحالة قابلة للحل** (6 حاكمة + 6 إحالات تحليلية) و**6 حدود ملزمة**، **بلا نسخ أي محتوى مصالحة**.
- **لماذا لم تُعدَّل `agent-execution-model.md`:** ممنوع بنص **حاكم** مزدوج — `decisions/DEFERRED_IMPLEMENTATION.md:26` (المرتبة 4) و`handoff/handoff.md:499` (المرتبة 9)؛ وشرط تفعيل تعديله مسجَّل في `P3-CI-08` = «دفعة مخوَّلة تملك `methodology/**`». **فبقي بلا مساس**، والوصول تحقَّق عبر Tier-0.
- completed: `decisions/open-decisions.md` (v2.7 → **v2.8**: «مجموعة قراءة مسار `R3`» + «سجل إغلاق `OD-GOV-3`» + «سجل `GOV-OBS-03`» + «استكمال حقول §3.4» + صفّ `GOV-OBS-03` في فهرس الترحيل + `OD-GOV-3` ⇒ **مُعالَج**) · `traceability/rar-reconciliation/SECTION-18-BLOCKING-EFFECT.md` (**غير حاكم** — +§9 جدولا §3.4 · +§10 إحالات الخطوتين · +§11 `GOV-OBS-03`) · `traceability/rar-reconciliation/P3-CLOSURE-INVENTORY.md` (`P3-CI-09` ⇒ `COMPLETE` · **`P3-CI-27` جديد**) · هذا المدخل.
- **`OD-GOV-3` ⇒ مُعالَج/مغلق.** سجل الإغلاق كامل الحقول في `decisions/open-decisions.md` → «سجل إغلاق `OD-GOV-3`»: Root cause · Reading Set المتأثرة · المراجع المضافة · المستهلك المتوقع · Evidence · Commit SHA · Verification method · Closure date · **Residual risks** · تأكيد أن `R3` لم تبدأ.
- **`GOV-OBS-03` (جديد — مفتوح):** نصّ §18 المرجعي **غير موجود** بينما تحيل إليه نصوص حاكمة ونُفِّذ أثره بأمر مالك 2026-07-30. **واكتُشف أن للرمز «§18» ثلاثة مدلولات متمايزة**: (1) خريطة الحجب — نصُّها مفقود؛ (2) **حوكمة الشاشات** — قائمة ومُغطّاة بجدول EC-4 في `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:58`..`:74` ببندين فرعيين `§18-د` و`§18-هـ`، **و`§18-د` يُحيل إلى `methodology/PHASE_EXECUTION_STANDARD.md`** وهو الملف نفسه الذي يستضيف بوابة `FP-0001`؛ (3) §18 داخل `RAR` — **محظورة** بنص `MANIFEST.md:73`. الأثر: `ambiguity / wrong-source execution` · **Mitigated for P3** · المطلوب: قرار حوكمي مستقل (إنشاء/استعادة/إعادة تسمية). **ولم يُنشأ النص المفقود.**
- **حقول §3.4:** التدقيق كشف **أربع فجوات** — `P3-CI-02`: Stable ID · Source phase/batch · **Owner or decision authority** (الجرد كان يكتب «مالك (R3 بأمر تفعيل)» فيخلط **المسار المالك** بـ**سلطة القرار**)؛ و`P3-CI-26`: Source phase/batch. **صُحِّحت الأربع في الوعاء الحاكم** `decisions/open-decisions.md` لا في `traceability/**` ⇒ `P3-CI-02` = **13/13** · `P3-CI-26` = **13/13**.
- **إحالات الخطوتين 1 و5:** بوابة الأساس في `methodology/PHASE_EXECUTION_STANDARD.md` — **الخطوة 1** «verify» و**الخطوة 5** «اختبارات متعددة الأنماط … وصولية». **لا مراسٍ ثابتة في الملف** (`grep '{#'` بلا نتيجة)، **وأرقام الأسطر تختلف بين المرجعين**: على الفرع `bdd5929` العنوان `:29` والخطوة 1 `:30` والخطوة 5 `:34` وقاعدة الإقفال `:37`؛ وعلى `origin/main` `7611ed9` هي `:95` · `:96` · `:100` · `:103`. فاعتُمد **النص الحرفي مرساةً مستقرة** مع ذكر السطر لكل مرجع. **مضمون البوابة والاختبارات لم يُمسّ.**
- **ملاحظتان مسجَّلتان لم تُصحَّحا (خارج صلاحية الدفعة):** (1) **مرجع مكسور اليوم على الفرع** — `FINAL-B-13B-DETERMINATION.md:122` يستشهد بـ`AUTHORITY.md:9` وهو سطر فاصل جدول `|---|---|---|---|`؛ والصف الصحيح للمرتبة 2 هو `AUTHORITY.md:11`. **الملف مجمَّد وعلى قائمة `do not touch`** فلم يُمسّ. (2) `P3-CLOSURE-INVENTORY.md:68` يدّعي استيفاء الحقول الثلاثة عشر بينما جدوله `:70` له **أحد عشر عموداً** (بلا Classification وبلا Required evidence)، و`P3-CI-02` معدودٌ ضمن الخمسة عشر بلا صفٍّ في ذلك الجدول.
- **نتيجة Remainder Census:** `Total = 27` = **`COMPLETE 12`** + **`GOVERNED TRANSFER 15`** + **`BLOCKING REMAINDER 0`** · **`UNCLASSIFIED = 0`** · المعادلة متوازنة. (قبل الدفعة: `26 = 11 + 15 + 0`.) `P3-CI-09` ⇒ `COMPLETE` · **`P3-CI-27`** (`GOV-OBS-03`) ⇒ `GOVERNED TRANSFER`.
- **`BLOCKING REMAINDER = 0` لا يعني إغلاق P3** ولا رفع التجميد ولا جاهزية `FP-0001`: الإغلاق **قرار مالك مستقل لم يُتخذ**؛ و`P3-CI-13` (merge/tag/release) يبقى **حاجباً لأي إعلان اكتمال**؛ و`OD-FP-0001-FREEZE` يبقى **`ACTIVE`**؛ و`OD-GOV-1` و`OD-GOV-2` و`GOV-OBS-03` **مفتوحة**.
- **الطبيعة التاريخية المجمَّدة — لم تُمسّ:** `FINAL-B-13B-DETERMINATION.md` (blob `806ebc47…`) · `FINAL-RECONCILIATION-TABLE.md` (blob `d8be1b85…`) · `RECONCILIATION-RAR-001..007.md` **byte-identical قبل/بعد**؛ جدول §10.4 = **260**؛ التوزيع = **`116/80/46/18/0`**؛ خط الأساس `188ad379…` لم يُعَد فتحه؛ حكم §13b **لم يُعَد حسابه**؛ مراسي الغياب **111** بلا تغيير.
- not completed: **لم تبدأ R3** · **الدلتا السبعة لم تُعالَج** · **المعايير السبعة لم تُكتب** · `ui/UI_DESIGN_SYSTEM.md` §9 **لم يُمسّ** · `FP-0001` و`Gate Criteria` لم يُعدَّلا · **التجميد لم يُرفع** · `methodology/agent-execution-model.md` **لم يُمسّ** (‏§9 ما زالت بلا صفٍّ لمسارات R) · `P3-CI-08` لم يُنفَّذ · `OD-GOV-1` و`OD-GOV-2` و`OD-P3-2` لم تُحسم · نص §18 المفقود **لم يُنشأ** · `AUTHORITY.md` لم تُمسّ · `superseded/**` لم يُلمس · لا ADR · **P3 لم تُغلق** · **لا merge ولا tag ولا release** · لا فرع ولا PR جديد.
- decisions: لا قرار مالك جديد. `OD-GOV-3` **عولج تنفيذياً** بالمسار الذي يوصل الدلتا عبر وعاء Tier-0 قائم — **دون** اختيار «إدراج مخرَج جامع في Reading Set» بتعديل §9، لأن ذلك محظور بنصٍّ حاكم. **ولم يُمنح `GOV-OBS-03` رقماً في سلسلة `OD-GOV-*`** — منحُ الرقم فعلٌ حوكمي لم يأذن به الأمر.
- tests: `origin/main` = `7611ed9…` بلا تغيير · PR #9 **`OPEN — NOT MERGED`** · رأس الفرع قبل = `bdd5929…` / بعد = **`e6c5b345702ad4c6c9e479f7bf1183fd9a0ecc88`** (ثُبِّت بجولة تصحيح لاحقة — H-0025) · commit **بأبٍ واحد** · `git rev-list --merges origin/main..HEAD` = **0** · `git merge-base --is-ancestor origin/main HEAD` = خطأ ⇒ `main` **غير مستوعَب** · كل مرجع في مجموعة القراءة **يُحَل فعلياً** · لا إحالة دائرية · لا مجموعة قراءة ثانية متعارضة · §3.4 = **13/13** لكلٍّ من `P3-CI-02` و`P3-CI-26` · معادلة الجرد متوازنة (`27 = 12 + 15 + 0` · `UNCLASSIFIED = 0`) · جدول **260** والتوزيع **116/80/46/18/0** بلا تغيير · بصمات `FINAL-B` و`FINAL-TABLE` و`RECONCILIATION-RAR-001..007` **مطابقة** · `AUTHORITY.md` و`methodology/PHASE_EXECUTION_STANDARD.md` و`methodology/agent-execution-model.md` **مطابقة** · EC-3 = **157/157** (لا ملف جديد) · مراسي الغياب **111** · `git diff --check` نظيف · worktree نظيف بعد الدفع · لا وسم ولا إصدار · لا أسرار · لا آثار macOS.
- next step: **قرار مالك** — إمّا (أ) **أمر تفعيل `R3`** لتقنين المعايير السبعة (الطريق إليه صار سالكاً: مجموعة القراءة قائمة، والشرط 2 من شروط الرفع مُستوفى تنفيذياً)، وإمّا (ب) **إعادة تقييم إغلاق P3** وفق `PHASE_EXECUTION_STANDARD.md` §3 مع بقاء `OD-FP-0001-FREEZE` **`ACTIVE`**، وإمّا (ج) **دفعة مخوَّلة تملك `methodology/**`** تنفّذ `P3-CI-08` وتضيف صفَّ مسارات R إلى §9. **ورفع التجميد لا يقع إلا بالشروط السبعة كاملةً وبدليل حاكم.**
- do not touch: constitution.md · AUTHORITY.md · decisions/adr/** · contracts/** · superseded/** · ui/** · catalogs/** · phases/** · **methodology/agent-execution-model.md** · **methodology/PHASE_EXECUTION_STANDARD.md** · `references/analysis-inputs/rar-2026-07/**` · جداول المصالحة السبعة وتصنيفاتها ووجهاتها · `FINAL-B-13B-DETERMINATION.md` · `FINAL-RECONCILIATION-TABLE.md` · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.3.1 · **H-0016..H-0023**.

## Handoff H-0025
> **جولة تصحيح حوكمي ضيقة — قبل إصدار أمر تفعيل `R3`.** يُقرأ بعد `H-0024` ولا ينسخه: `H-0024` صحيحٌ في تاريخه، وهذه الجولة **تُثبّت دليله** وتصحّح عبارةً مضلِّلة وتسجّل عيباً مكتشَفاً. **لا إعادة كتابة لأي مدخل سابق.** **لا تغيير في أي حالة حاكمة.**
- date: 2026-07-31
- phase: P3 — **OD-GOV-3 CLOSURE-EVIDENCE FIXATION · §3.4 REFERENCE CORRECTION · P3-CI-28 REGISTRATION** — L1 · فرع PR #9 نفسه بلا دمج
- task/goal: (1) تثبيت `Commit SHA` في سجل إغلاق `OD-GOV-3` بدل الـplaceholder؛ (2) تصحيح العبارة الموحية بأن جدول الجرد يعرض حقول §3.4 الثلاثة عشر؛ (3) تسجيل **`P3-CI-28`**. **لا بدء لـR3 · لا معالجة للمعايير السبعة · لا رفع للتجميد.**
- base SHA: **`origin/main` = `7611ed9531660f5f4762f3e6a60f05cdf0f419b4`** (بلا تغيير) · **رأس PR #9 قبل الدفعة:** `e6c5b345702ad4c6c9e479f7bf1183fd9a0ecc88`.
- **خطية الفرع:** أبٌ واحد هو `e6c5b34…` · بلا merge ولا rebase ولا amend ولا force-push · **`main` لم يُدخَل**.
- **(1) تثبيت دليل الإغلاق:** كان الحقل يحمل **قيمة placeholder غير محلولة** (رمزاً نائباً بين قوسين زاويين) **ويزعم** أن الـSHA «يُثبَّت في H-0024 عند الدفع» — وH-0024 نفسه كان يحمل الرمز النائب ذاته، فالإحالة كانت **زعماً غير محقَّق**. *(لا يُكتب الرمز النائب حرفياً هنا كي لا يُنتج تطابقاً كاذباً في فحوص الـplaceholders اللاحقة.)* ثُبِّت الآن في الموضعين بالـSHA الفعلي **`e6c5b345702ad4c6c9e479f7bf1183fd9a0ecc88`** — وهو commit إغلاق `OD-GOV-3` (أبوه `bdd5929…`)، **لا** SHA جولة التصحيح، **ولا** إحالة ذاتية. وصُحِّحت العبارة بأقل تعديل.
- **(2) تصحيح §3.4:** `P3-CLOSURE-INVENTORY.md` §4 كان يقول «الحقول الثلاثة عشر الإلزامية … **مستوفاة لكل صف**» ثم يعدّدها — وهو موحٍ بأن الجدول يعرضها، بينما أعمدته **أحد عشر** (ينقصها **Classification** و**Required evidence**). صار النص ينصّ صراحةً على أن الجرد **يعرّف العنصر وحالته**، وأن الاستيفاء التفصيلي 13/13 في `SECTION-18-BLOCKING-EFFECT.md` **§9.1** و**§9.2**، وأن ذلك **إحالة توثيقية لا تنقل سلطة إلى `traceability/**`**. **بلا أعمدة جديدة وبلا تكرار الحقول الثلاثة عشر داخل الجرد.**
- **(3) `P3-CI-28` (جديد · `GOVERNED TRANSFER`):** `FINAL-B-13B-DETERMINATION.md:122` يستشهد بـ`AUTHORITY.md:9` لإثبات المرتبة 2، لكن `AUTHORITY.md:9` **سطر فاصل جدولي** (`|---|---|---|---|`)؛ والصف الصحيح **`AUTHORITY.md:11`**. **الادّعاء الموضوعي صحيح والمكسور هو الاستشهاد وحده**، وهو مكسور **اليوم على الفرع** لا بعد الدمج فقط. **لم يُصحَّح**: `FINAL-B` مجمَّد وعلى قائمة `do not touch`، و`AUTHORITY.md` ممنوع تعديله. الوعاء الحالي: هذا المدخل + صفّه في الجرد. الوجهة: **دفعة مخوَّلة لاحقة بأمر مالك**. شرط الإغلاق: تصويب `:9` ⇒ `:11` بدليل، أو قبول صريح موثَّق. **غير حاجب** لـP3 ولا لـ`FP-0001` ولا لتفعيل `R3`.
- **فحص placeholders الحاكم (decisions/** · methodology/** · handoff/**):** أربعة تطابقات إضافية **فُحصت وصُنِّفت غير عيوب**: `decisions/adr/README.md:14` (`ADR-XXXX-kebab-title.md` — **نمط تسمية**) · `handoff/handoff.md:9` (`## Handoff H-XXXX` — **ترويسة قالب**) · `SPECIFICATIONS_CLOSEOUT_HANDOFF.md:7` و`:38` (**جملة نتيجة مسح** تعدّد الرموز: «صفر TODO/FIXME/Future-Work/TBD/Coming-Soon»). **صفر placeholder غير محلول داخل سجل نافذ أو قرار معلن مغلق.**
- **نتيجة Remainder Census:** `Total = 28` = **`COMPLETE 12`** + **`GOVERNED TRANSFER 16`** + **`BLOCKING REMAINDER 0`** · **`UNCLASSIFIED = 0`** · `P3-CI-01`..`P3-CI-28` بلا فجوات. (قبل الجولة: `27 = 12 + 15 + 0`.)
- **الحالات التي لم تتغيّر:** `OD-GOV-3` = **CLOSED** · `GOV-OBS-03` = **OPEN** · `P3-CI-27` = `GOVERNED TRANSFER` · `P3-CI-28` = `GOVERNED TRANSFER` · **`FP-0001` = `BLOCKED`** · **`OD-FP-0001-FREEZE` = `ACTIVE`** · **R3 = NOT STARTED** · **P3 = OPEN** · **الدلتا السبعة = NOT REMEDIATED**.
- **الطبيعة التاريخية المجمَّدة — لم تُمسّ:** `FINAL-B-13B-DETERMINATION.md` (blob `806ebc47…`) · `FINAL-RECONCILIATION-TABLE.md` (blob `d8be1b85…`) · `RECONCILIATION-RAR-001..007.md` · `AUTHORITY.md` · `methodology/PHASE_EXECUTION_STANDARD.md` · `methodology/agent-execution-model.md` · `methodology/RECONCILIATION_ROADMAP.md` · `ui/**` · `INDEX.md` — **byte-identical**؛ الجدول **260** · التوزيع **`116/80/46/18/0`** · خط الأساس `188ad379…` · المراسي **111** · EC-3 **157/157**.
- not completed: **لم تبدأ R3** · المعايير السبعة لم تُصَغ ولم تُنفَّذ · `ui/UI_DESIGN_SYSTEM.md` §9 لم يُمسّ · التجميد لم يُرفع · `FINAL-B` و§13b لم يُعادا · استشهاد `AUTHORITY.md:9` **لم يُصحَّح** (مسجَّل `P3-CI-28`) · `GOV-OBS-03` لم يُحسم · `P3-CI-08` لم يُنفَّذ · `OD-GOV-1` و`OD-GOV-2` و`OD-P3-2` لم تُحسم · **P3 لم تُغلق** · لا merge ولا tag ولا release.
- decisions: لا قرار مالك جديد. تسجيلٌ وتصحيحُ إحالات فقط.
- tests: parent count = **1** · merge commits = **0** · `main` غير مستوعَب · الملفات المعدَّلة **ثلاثة فقط** · الملفات المجمَّدة **byte-identical** · **صفر placeholder غير محلول** · `P3-CI-01..28` بلا فجوات · المعادلة `28 = 12 + 16 + 0` · `UNCLASSIFIED = 0` · SHA إغلاق `OD-GOV-3` = `e6c5b345702ad4c6c9e479f7bf1183fd9a0ecc88` · عبارة §3.4 متسقة مع §9.1/§9.2 · الجدول **260** · التوزيع **116/80/46/18/0** · خط الأساس `188ad37` · `FP-0001` = `BLOCKED` · التجميد `ACTIVE` · R3 = NOT STARTED · `git diff --check` نظيف · worktree نظيف · لا وسم ولا إصدار.
- next step: **المستودع جاهز لإصدار أمر تفعيل `R3`** من حيث التتبّعية والأدلة — مجموعة القراءة قائمة وواصلة عبر Tier-0، ودليل إغلاق `OD-GOV-3` مثبَّت، وصفر placeholder غير محلول. **والتفعيل نفسه قرار مالك لم يُتخذ**؛ ولا يبدأ إلا بأمر صريح (`RECONCILIATION_ROADMAP.md:5`).
- do not touch: constitution.md · AUTHORITY.md · decisions/adr/** · contracts/** · superseded/** · ui/** · catalogs/** · phases/** · methodology/** · `references/analysis-inputs/rar-2026-07/**` · جداول المصالحة السبعة وتصنيفاتها ووجهاتها · `FINAL-B-13B-DETERMINATION.md` · `FINAL-RECONCILIATION-TABLE.md` · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.3.1 · **H-0016..H-0024**.

## Handoff H-0026
> **جولة تفعيل مسار `R3` — تخصيص ومعايير قبول فقط.** يُقرأ بعد `H-0025` ولا ينسخه: `H-0025` صحيحٌ في تاريخه وقد أنهى بأن «المستودع جاهز لإصدار أمر تفعيل `R3`»، **وقد صدر الأمر ونُفِّذ نطاقُه التخصيصي هنا**. **لا إعادة كتابة لأي مدخل سابق.** **ولا تغيير في حالة `FP-0001` ولا في التجميد ولا في جرد `P3`.**
- date: 2026-07-31
- phase: **R3 — Accessibility Specification & Acceptance-Criteria Design (‏`ACTIVE — SPECIFICATION ONLY`)** — L1 · فرع PR #9 نفسه بلا دمج
- task/goal: تنفيذ **أمر المالك الصريح** «‏OWNER ACTIVATION ORDER — R3 (specification and acceptance-criteria design only)»: (1) تسجيل تفعيل `R3` حاكمياً في وعائيه المأذونين؛ (2) تخصيص **المعايير السبعة** بمعرّفات ثابتة وحقول كاملة؛ (3) تصميم **مصفوفة اختبارات القبول**؛ (4) نموذج حوكمة «Labels and Descriptions»؛ (5) تصنيف حقول ميتاداتا الشاشات الديناميكية بأدلة؛ (6) شروط رفع التجميد وإغلاق `R3`. **لا معالجة · لا تقنين · لا رفع تجميد · لا إغلاق.**
- base SHA: **`origin/main` = `7611ed9531660f5f4762f3e6a60f05cdf0f419b4`** (بلا تغيير) · **رأس PR #9 قبل الدفعة (‏commit البداية في أمر المالك):** `00c358712be9d5d952b64b82edfa2ac9d9154193`.
- **خطية الفرع:** أبٌ واحد هو `00c3587…` · بلا merge ولا rebase ولا amend ولا force-push · **`main` لم يُدخَل** ولا merge commit.
- completed:
  - **تفعيل `R3` مسجَّل حاكمياً** — `decisions/open-decisions.md` → **«سجل تفعيل مسار `R3`»** (‏`R3-ACT-01`، المرتبة 4) + هذا المدخل (المرتبة 9). الحالة النافذة: **`ACTIVE — SPECIFICATION ONLY`**.
  - **سبعة معايير بمعرّفات ثابتة** `R3-A11Y-01`..`R3-A11Y-07` — مساحةُ أسماءٍ أُثبت آلياً خلوُّ المستودع وكل الفروع منها، وتتبع النمط البيتي `<FAMILY>-<AREA>-<zero-padded-n>`. لكل معيار: الهدف · المتطلب المعياري · النطاق · السلوك المطلوب والمحظور · المكوّنات المنطبِقة · أثر الواجهات الديناميكية والمولَّدة بالـAI · RTL/LTR · Light/Dark · اختبارات آلية ويدوية · الدليل المطلوب · شروط النجاح والفشل · الاستثناءات · وجهة المعالجة · سلطة القرار.
  - **مصفوفة اختبارات** `R3-A11Y-T-001`..`R3-A11Y-T-046` (‏**46** — آلي 29 · يدوي 17) بعشرة حقول لكل اختبار، مع `RUN-MATRIX` إلزامية (‏`ar`/`en` × Light/Dark × `FIXED`/`META`/`AIGEN`) وجدول تغطية للأبعاد الستة عشر المطلوبة.
  - **نموذج حوكمة «Labels and Descriptions»** بأقسامه الأربعة: (A) الضوابط الثابتة · (B) الشاشات المُدارة بالميتاداتا · (C) التوليد بمعونة الـAI بثمانية ضوابط ملزمة أساسُها `OD-BLD-1` و`ADR-0029` و`OD-RAR-05` · (D) النص السياقي محدود الجلسة. **والخلاصة: النموذج اللغوي ليس السلطة الدائمة لميتاداتا الإتاحة.**
  - **تصنيف ثلاثة عشر حقلاً** لميتاداتا الشاشات الديناميكية بدليل `file:line` لكل تصنيف: **`GOVERNED` = 3** (بتحفّظ) · **`PARTIAL` = 3** · **`MISSING` = 6** · **`CONFLICTING` = 1**. الاستنتاج: **لا عقد حقلٍ في المستودع** (`contracts/fields/` مؤجَّل والمجلد غير موجود).
  - **شروط رفع التجميد وإغلاق `R3`** — عشرون شرطاً تراكمياً، **تفصيلاً للشروط السبعة القائمة لا استبدالاً لها**، مع النصّ صراحةً على أن **اكتمال التخصيص وحده لا يرفع التجميد**.
  - **وعاء تتبّع `R3` منفصل** أُنشئ: `traceability/r3-accessibility/` بملفَّين غير حاكمين — **خارج `P3-CLOSURE-INVENTORY.md` كلياً**.
  - **تغطية EC-3** لملفَّي `R3` في `INDEX.md` (‏156 → 158 ملفاً + الفهرس) ⇒ **EC-3 = 159/159 · صفر غير مغطى**.
  - **تعارضٌ حوكمي مرفوع إلى المالك بلا حسم:** ميثاق `R3` في `methodology/RECONCILIATION_ROADMAP.md:11` = «Contracts Coverage Expansion»، وتقنينُ الإتاحة أُلحق بـ`R3` بنصوص المرتبة 4 **دون تعديل صفّ الخارطة** ⇒ `R3` تحمل حِملين غير متجانسين. **ولم يُعدَّل `RECONCILIATION_ROADMAP.md`.**
- not completed: **لم تُعالَج الدلتا السبعة** · **لم تُقنَّن المعايير** و`ui/UI_DESIGN_SYSTEM.md` **§9 لم يُمسّ** · **لا معيار `PASS`** · لم يُنفَّذ ولا بُني أيُّ اختبار · **لم يُرفع التجميد** و`OD-FP-0001-FREEZE` يبقى **`ACTIVE`** · **`FP-0001` يبقى `BLOCKED`** · **`R3` لم تُغلق** · **`P3` لم تُغلق** · لم يُنشأ عقد حقلٍ · لم يُبنَ الباني ولا عُدِّل · لم يُحسم تعارض ميثاق `R3` ولا تعارض الوضع الداكن (`OD-UX-3`) ولا تعارض `UI_SCREEN_GOVERNANCE_STANDARD.md:68` · `GOV-OBS-03` و`P3-CI-28` و`OD-GOV-1` و`OD-GOV-2` و`OD-P3-2` **لم تُحسم** · `P3-CI-08` لم يُنفَّذ · لم يُعَد `FINAL-B` ولا §13b · لا merge ولا tag ولا release.
- files changed: **خمسة** — `decisions/open-decisions.md` (‏v2.9 · +سجل التفعيل +إحالة أمامية في مجموعة القراءة) · `handoff/handoff.md` (هذا المدخل) · `INDEX.md` (‏+صفّان وتحديث الإجمالي) · **جديد** `traceability/r3-accessibility/R3-ACCESSIBILITY-SPECIFICATION.md` · **جديد** `traceability/r3-accessibility/R3-ACCESSIBILITY-TEST-MATRIX.md`. **و`traceability/rar-reconciliation/P3-CLOSURE-INVENTORY.md` لم يُعدَّل** — لأن لا تصنيفَ عنصرٍ تغيَّر ولا عنصرَ `P3` جديداً نشأ.
- decisions: **قرار مالك واحد** = تفعيل `R3` للتخصيص فقط. لا ADR · لا قرار معماري · لا إعادة ترقيم لأي `OD` قائم · لا تغيير لحالة أي `OD` آخر · `AUTHORITY.md` لم تُمسّ · **ولم تُنشأ طبقة سلطة جديدة** — وعاءا `R3` **غير حاكمين** صراحةً.
- risks: (1) **ميثاق `R3` لا يعكس شقّ الإتاحة** في المرتبة 2 — مرفوع للمالك، وأثره **غير حاجب** لهذه الدفعة. (2) **`ui/UI_DESIGN_SYSTEM.md` §9 هو الوجهة المسمّاة في ثلاثة نصوص حاكمة، ولم يُمسّ** — فالتقنين يحتاج **أمراً مستقلاً**، وحتى وقوعه يبقى الشرط الأول من شروط الرفع غيرَ مستوفى. (3) **ستة حقول ميتاداتا `MISSING` وواحد `CONFLICTING`** ⇒ `R3-A11Y-03` غير قابل للتنفيذ الكامل قبل إنشاء **عقد حقلٍ** (يمسّ المرتبة 5). (4) **فجوات إنفاذ** في `testing-strategy.md` و`UI_GATE_REVIEW_CHECKLIST.md` و`UI_COMPONENT_STATES.md` — لو قُنِّنت §9 وحدها لبقيت بلا نقطة إنفاذ. (5) **تعارض الوضع الداكن** قائم قبل `R3` ويؤثر في عمود Dark من `RUN-MATRIX`.
- tests: parent count = **1** · merge commits = **0** · `main` غير مستوعَب · الملفات المعدَّلة/المضافة **خمسة فقط** · الملفات المجمَّدة (`FINAL-B-13B-DETERMINATION.md` · `FINAL-RECONCILIATION-TABLE.md` · `AUTHORITY.md` · `constitution.md` · `methodology/**` · `ui/**` · `contracts/**` · `phases/**` · `catalogs/**` · `decisions/adr/**` · `superseded/**` · `references/**` · `traceability/rar-reconciliation/**`) **byte-identical** · الجدول **260** · التوزيع **`116/80/46/18/0`** · خط الأساس `188ad37` · المراسي **111** · معادلة جرد `P3` **`28 = 12 + 16 + 0`** · `UNCLASSIFIED = 0` · **صفر `P3-CI-*` جديد** · `P3-CI-01..28` بلا فجوات · EC-3 **159/159** · صفر `placeholder` غير محلول · `R3-A11Y-01..07` بلا فجوات · `R3-A11Y-T-001..046` بلا فجوات · `FP-0001` = **`BLOCKED`** · التجميد **`ACTIVE`** · **لا معيار `PASS`** · `R3` = **`ACTIVE — SPECIFICATION ONLY`** · `P3` = **مفتوحة** · `git diff --check` نظيف · worktree نظيف · **لا وسم ولا إصدار**.
- next step: **المستودع جاهز لإصدار أمر `R3` مستقل للمعالجة (‏remediation)**. وترتيبُ ما بعده كما تقتضيه الشروط: (1) **اعتماد المالك للمعايير السبعة**؛ (2) **أمر تقنين** يملأ `ui/UI_DESIGN_SYSTEM.md` §9 بالصيغة القابلة للاختبار؛ (3) **أمر إنشاء عقد الحقل** (المرتبة 5) لأن `R3-A11Y-03` معلَّق عليه؛ (4) بناء الاختبارات وتنفيذها بأدلة؛ (5) المعالجة؛ (6) فحوص بوابة `FP-0001`؛ (7) الرفع بقرار مالك. **ولا شيء من ذلك مأذون به في هذه الدفعة.** وقد يقرّر المالك دمج (2) و(3) في أمرٍ واحد.
- do not touch: constitution.md · AUTHORITY.md · decisions/adr/** · contracts/** · superseded/** · ui/** · catalogs/** · phases/** · methodology/** · `references/analysis-inputs/rar-2026-07/**` · `traceability/rar-reconciliation/**` كاملاً (بما فيه `P3-CLOSURE-INVENTORY.md` وجداول المصالحة السبعة وتصنيفاتها ووجهاتها) · `FINAL-B-13B-DETERMINATION.md` · `FINAL-RECONCILIATION-TABLE.md` · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.3.1 · **H-0016..H-0025**.

## Handoff H-0027
> **‏P3 — Phase Exit Review وإعداد الإغلاق.** يُقرأ بعد `H-0026` ولا ينسخه: `H-0026` صحيحٌ في تاريخه وقد أنهى بأن «المستودع جاهز لإصدار أمر `R3` مستقل للمعالجة»، **وهذه الجولة لا تنفّذ معالجة** — بل تُجري **مراجعة خروج `P3`** وتُعدّ سجل الإغلاق. **لا إعادة كتابة لأي مدخل سابق.** **ولا تغيير في `FP-0001` ولا في التجميد ولا في `R3` ولا في أي مخرج مجمَّد.**
- date: 2026-08-01
- phase: **P3 — Phase Exit Review and Closure Preparation** — L1 · فرع PR #9 نفسه **بلا دمج**
- task/goal: إجراء **Phase Exit Review** الرسمي لـ`P3` وفق `methodology/PHASE_EXECUTION_STANDARD.md` **§3.1–§3.9**، وتسجيل قرار المالك بإغلاق **نطاق** `P3` في وعائه الحاكم. **لا merge · لا tag · لا release · لا تفعيل `R4` · لا تعديل `R3` · لا رفع تجميد · لا فكّ حجب `FP-0001`.**
- base SHA: **`origin/main` = `7611ed9531660f5f4762f3e6a60f05cdf0f419b4`** (بلا تغيير · **غير مستوعَب في الفرع**) · **رأس PR #9 قبل الدفعة:** `8a5b2f6ba66462042c988987bf056e541e1095b0`.
- **خطية الفرع:** أبٌ واحد هو `8a5b2f6…` · بلا merge ولا rebase ولا amend ولا force-push · **`main` لم يُدخَل** · `git rev-list --merges origin/main..HEAD` = **0** · الفرع **25 commit** فوق نقطة الافتراق `52fbde1f…` قبل هذه الدفعة.

**قيد تنفيذي حاكم على هذه المراجعة (‏مصدر §3):** `methodology/PHASE_EXECUTION_STANDARD.md` **§3.1–§3.9 غير موجودة في شجرة فرع PR #9** — الملف على الفرع **39 سطراً** وينتهي عند «بوابة الأساس»، وعلى `origin/main` **105 أسطر**. فقُرِئت §3 **من `origin/main`** (المرتبة 2 نافذة بعد دمج PR #10 في `7611ed9…`). **وهذا ليس عيباً في الفرع:** فرع PR #9 أُنشئ **قبل** PR #10، وتقاطع ملفات الشقّين = **صفر** (تحقّق: الفرع لم يمسّ `methodology/PHASE_EXECUTION_STANDARD.md` ولا `phases/**` في أيٍّ من commitاته الخمسة والعشرين). **ووراثة §3 تتحقق عند دمج PR #9.**

**نتيجة المراجعة — §3.1 إلى §3.9:**

| البند | النتيجة | الدليل |
|---|---|---|
| **§3.1 Scope Completion** | **PASS** | المصالحة مكتملة **260/260** (تحقّق آليّ مستقل: `53+25+50+37+38+27+30 = 260`، وكل صف **ستة أعمدة** — مجموعة أعداد الأعمدة = `{6}`) · التوزيع **`116/80/46/18/0`** (تحقّق آليّ مستقل بعدّ العمود الخامس) · §13b **`DETERMINED — BLOCKING DELTA DETECTED`** بنطاق `FP-0001` حصراً و**`33+7+6 = 46`** — **محفوظ بلا مساس** · لا عمل `P3` غير محسوم خارج النقل الحاكم |
| **§3.2 Decision Closure** | **PASS** | `OD-RAR-01..09` **مقفلة** · `OD-GOV-3` **مغلق** بدليل `e6c5b345…` · قرار المالك `ACTUAL NARROW FREEZE` مسجَّل `OD-FP-0001-FREEZE` · تفعيل `R3` مسجَّل `R3-ACT-01` · **وقرار إغلاق نطاق `P3` سُجِّل الآن في الوعاء الحاكم** `decisions/open-decisions.md` → **`OD-P3-CLOSURE`** (لا في تقرير). القرارات المفتوحة الباقية (`OD-GOV-1` · `OD-GOV-2` · `OD-P3-2` · `GOV-OBS-03`) **ليست لازمة لإغلاق نطاق `P3`** ومسجَّلة منقولةً حاكمياً بوجهات ومالكين وشروط تفعيل |
| **§3.3 Remainder Census** | **PASS** | **`Total 28 = COMPLETE 13 + GOVERNED TRANSFER 15 + BLOCKING REMAINDER 0`** · **`UNCLASSIFIED = 0`** · `P3-CI-01..28` **بلا فجوات** (تحقّق آليّ) · **التغيير الوحيد عن `28 = 12 + 16 + 0`:** `P3-CI-15` ⇒ **`COMPLETE`** (أدناه). **ولم يُنشأ أي عنصر `P3` جديد** لـ`R3` ولا Issue #11 ولا Rocket ولا Visual Baseline ولا Design System ولا عقود الشاشات ولا Enterprise UI Governance |
| **§3.4 Governed Transfer** | **PASS** | `P3-CI-02` = **13/13** · `P3-CI-26` = **13/13** — **الحقول مستوفاة في الوعاء الحاكم** `decisions/open-decisions.md` («استكمال حقول §3.4» + `OD-FP-0001-FREEZE` + جدول الدلتا السبعة)، **لا في `traceability/**`** (القاعدة القاطعة في §3.4 محترَمة؛ و`SECTION-18-BLOCKING-EFFECT.md` §9.1/§9.2 **فهرس تجميع وإحالة لا وعاء**). **وقرار المالك المسجَّل:** النقل الحاكم **كافٍ لإغلاق نطاق `P3`** مع بقاء الالتزامَين **غير منفَّذين** |
| **§3.5 Traceability and Evidence** | **PASS** | مراسي الغياب: **111 تعريفاً** · **111 مُشاراً إليها** · **صفر مكسورة** · **صفر مكرَّرة** (تحقّق آليّ) · **صفر `placeholder` غير محلول** في سجل نافذ (المطابقات الباقية أنماط تسمية وترويسة قالب ورمز `<FAMILY>-<AREA>-<n>` وجُمَل نتائج مسح — مُصنَّفة غير عيوب في H-0025) · **الأدلة المجمَّدة byte-identical** (أدناه) · العدّادات والتوزيعات التاريخية **بلا تغيير** · **EC-3 = 159/159 · صفر غير مغطى** للشجرة الحالية (تحقّق آليّ مستقل: **159** ملف `.md` متعقَّب · **158** صفاً في `INDEX.md` + الفهرس نفسه · **صفر** ملف خارج الفهرس · **صفر** صفّ بلا ملف) |
| **§3.6 Repository and Roadmap State** | **PASS — `NO UPDATE REQUIRED`** | التفصيل والدليل أدناه |
| **§3.7 Git and Release State** | **PASS** | PR #9 **`OPEN — NOT MERGED`** · الحالة أدناه · **merge/tag/release خطوات مالك حصراً** مسجَّلة صريحةً في `P3-CI-13` و`OD-P3-CLOSURE` (د) — **ولا تختفي من السجل** |
| **§3.8 Next-stage Readiness** | **PASS** | **`R4` لم تُفعَّل ولا تُفعَّل هنا** · **لا عبارة انتقال صدرت** · لم تُنفَّذ أعمال مرحلة تالية داخل هذه · شرطُ الاستمرار المسجَّل: التفعيل **بأمر مالك صريح** (`methodology/RECONCILIATION_ROADMAP.md:5`) |
| **§3.9 Closure Semantics** | **PASS** | القاعدة مسجَّلة حرفيّاً في الوعاء الحاكم `OD-P3-CLOSURE` (ب) — والتمييز الثلاثي (إغلاق نطاق ≠ اكتمال مشروع ≠ عدم فقدان الالتزامات) **مطبَّق نصاً** |

- **§3.3 — التغيير الوحيد في التصنيف: `P3-CI-15` ⇒ `COMPLETE`.** شرط إغلاقه المسجَّل كان «**دمج القاعدة + اجتياز §3 عليها**» وأثرُه المسجَّل «**حاجب لإعلان إغلاق `P3`**». **وقد تحقّق الشقّان:** PR #10 **مدموج** و§3 **نافذة على `main`** (`origin/main` = `7611ed9…` — تحقّق حيّ)، **واجتياز §3 واقعٌ في هذا المدخل نفسه**. **فلا يجوز إبقاؤه `GOVERNED TRANSFER`** وقد استُوفي شرطه — وإبقاؤه كذلك كان سيترك بنداً **أثرُه المسجَّل حاجبٌ لإعلان الإغلاق** مفتوحاً عند الإغلاق. **ولم ينتقل أي بند آخر، ولم يُحذف بند، ولم يُدمج بندان.**
- **§3.4 — قرار المالك المسجَّل:** `P3-CI-02` و`P3-CI-26` **منقولان حاكمياً بنجاح لأغراض نطاق `P3`** لأن التزاميهما **مصنَّفان** وحقولهما **13/13** ولهما **مسار مالك مسمّى (`R3`)** وهما **محفوظان لـ`R3`**. **وهذا لا ينفّذ التزاميهما ولا يُسقطهما ولا يُضعفهما** — يبقيان `GOVERNED TRANSFER` وتبقى الدلتا السبعة **`NOT REMEDIATED`**.
- **§3.6 — تقييم ملفَّي الخارطة (‏`NO UPDATE REQUIRED`) بدليل، لا بمجرد وجودهما:**
  1. **لا صلة موضوعية:** `phases/phase-roadmap.md` و`phases/PHASE_MASTER_PLAN.md` يحكمان **ترتيب مراحل المنتج `P0`–`P8` ونطاقها العام** (المرتبة 6). وفحصٌ آليّ عليهما أرجع **صفر** ورود لـ`RAR` أو «مصالحة» أو `reconciliation` أو `FP-0001` أو `Phase Exit`. ودفعة `P3` الحوكمية **ليست** مرحلة منتج: مسار `R` «**منفصل تماماً** عن مراحل `P0`–`P8`» (`methodology/RECONCILIATION_ROADMAP.md:5`)، والتمييز مسجَّل أصلاً في `P3-CI-03` و`P3-CLOSURE-INVENTORY.md` §6. **فإغلاق نطاق `P3` لا يغيّر ترتيب مرحلة منتج ولا نطاقها.**
  2. **الربط المطلوب موجود سلفاً على `main`:** PR #10 (`e999c01`) أضاف بنفسه **سطر Phase Exit Review إلى كلا الملفين** — «**Phase Exit Review (قاعدة مركزية):** لا تُعلن أي مرحلة من هذه الخارطة مغلقة … قبل اجتياز Phase Exit Review في `../methodology/PHASE_EXECUTION_STANDARD.md` §3» و«**Phase Exit Review مشترك** … **لا قائمة مراجعة موازية في هذه الوثيقة ولا في التصاميم**». **فالنصّ الحاكم نفسه ينهى عن قائمة موازية فيهما** ⇒ أي إضافة هنا **مخالفة** لا استيفاء.
  3. **حجّة تقنية مانعة:** الملفان **لم يُمسّا في أيٍّ من commitات الفرع الخمسة والعشرين**، ونسختهما على الفرع **أقدم** من نسخة `main` (تنقصها إضافة PR #10). فتعديلهما هنا يعني الكتابة فوق **النسخة الأقدم** وخلقَ **تعارض دمج** يهدّد سطر PR #10 على `main`. **وبتركهما بلا مساس يبقى الدمج نظيفاً وتُورَث نسخة `main` كما هي.**
  4. **السلطة:** لا سلطة في أمر هذه الجولة لتعديل المرتبة 6، وأمرُ الجولة ينصّ صراحةً على عدم تعديلهما لمجرد وجودهما.
  ⇒ **`NO UPDATE REQUIRED`** — لكلٍّ من `phases/phase-roadmap.md` و`phases/PHASE_MASTER_PLAN.md`. **ولم يُمسّا.**
- **§3.7 — حالة Git وPR (قراءة حيّة من `origin` وGitHub):** PR #9 = **`OPEN`** · `mergeable` = **`MERGEABLE`** · `mergeStateStatus` = **`CLEAN`** · `mergedAt` = **`null`** · القاعدة `main` · **head** = `8a5b2f6…` قبل الدفعة · نقطة الافتراق `52fbde1f…` · **25 commit** فوقها · **صفر merge commit** · **`main` غير مستوعَب** · worktree **نظيف**. **ولم يقع في هذه الجولة:** merge · rebase · amend · force-push · tag · release.
- **إفصاح إلزامي — توسعة نطاق مسجَّلة غير حاجبة على PR #9 (‏قرار المالك 4):** يحمل PR #9 **محتوى تفعيل `R3`** في commitه الأخير `8a5b2f6…` — خمسة ملفات: `decisions/open-decisions.md` (سجل `R3-ACT-01`) · `handoff/handoff.md` (H-0026) · `INDEX.md` (+صفّان) · **وملفّان جديدان** `traceability/r3-accessibility/R3-ACCESSIBILITY-SPECIFICATION.md` و`…/R3-ACCESSIBILITY-TEST-MATRIX.md`. **وهذا محتوى مسار `R3` لا مسار `P3`.** قرار المالك: **يُقبل توسعةَ نطاقٍ مسجَّلة غير حاجبة** — **يُفصح عنه هنا** · **لا يُحذف ولا يُنقل ولا يُعاد تأسيسه ولا يُعدَّل ولا يُعاد كتابته** · **ولا يُضاف عملُ `R3` جديد إلى PR #9**. **ولم يُمسّ أيٌّ من الملفين في هذه الجولة**، ولم يُنشأ لهما عنصر `P3-CI-*`.
- **‏GitHub Issue #11 — خارج نطاق `P3` (قرار المالك 5):** **لم يُضَف** إلى `P3-CLOSURE-INVENTORY.md` · **لم يُعدَّل** · **لم يُصنَّف** بنداً حاكمَ النقل جديداً. **ولم يُقرأ محتواه بوصفه مصدر التزام على `P3`.**
- completed: `decisions/open-decisions.md` (‏v2.9 → **v3.0**: «سجل قرار إغلاق نطاق `P3`» — **`OD-P3-CLOSURE`** + قاعدة دلالة الإغلاق §3.9 + الحالات النافذة + **خطوات المالك المتبقية**) · `traceability/rar-reconciliation/P3-CLOSURE-INVENTORY.md` (**غير حاكم** — Δ إغلاق: `P3-CI-15` ⇒ `COMPLETE` + المعادلة `28 = 13 + 15 + 0` + إفصاح توسعة `R3` + EC-3 للشجرة الحالية) · هذا المدخل.
- **الأدلة المجمَّدة — لم تُمسّ (تحقّق ببصمات الـblob قبل/بعد):** خط الأساس المجمَّد **`188ad379d04b07ca9e1b4eeee38dc68ecca29914`** والبصمات الأربع **byte-identical**: `RAW-EXTRACTION-REGISTER.md` (`6f74480e…`) · `CANONICAL-ITEM-UNIVERSE.md` (`2a8f959a…`) · `NORMALIZATION-AND-ATOMIC-MAP.md` (`1b9aa8ec…`) · `SEMANTIC-MERGE-MAP.md` (`0f5a841f…`). و`FINAL-B-13B-DETERMINATION.md` · `FINAL-RECONCILIATION-TABLE.md` · `RECONCILIATION-RAR-001..007.md` · `ABSENCE-EVIDENCE-B1/B2-*` · `OWNER-DECISION-PACKAGE.md` · `B1-CHECKPOINT-REPORT.md` · `SOURCE-ELIGIBILITY-PASS.md` **لم يمسّها أيُّ commit منذ `f6ec1f3` (B2-FINAL-B)** — تحقّق: `git diff --name-only f6ec1f3..HEAD` **لا يحوي أيّاً منها**. و`AUTHORITY.md` · `methodology/**` · `contracts/**` · `ui/**` · `phases/**` · `superseded/**` · `references/**` **byte-identical**.
- not completed: **الدلتا السبعة لم تُعالَج ولم تُقنَّن** · `ui/UI_DESIGN_SYSTEM.md` **§9 لم يُمسّ** · **لا معيار `PASS`** · لم يُبنَ ولم يُنفَّذ أيُّ اختبار · **التجميد لم يُرفع** و`OD-FP-0001-FREEZE` يبقى **`ACTIVE`** · **`FP-0001` يبقى `BLOCKED`** · **`R3` لم تُغلق** ولم تُعدَّل ملفّاتها · **`R4` لم تُفعَّل** · `GOV-OBS-03` و`P3-CI-28` و`OD-GOV-1` و`OD-GOV-2` و`OD-P3-2` **لم تُحسم** · `P3-CI-08` لم يُنفَّذ · تعارض ميثاق `R3` (`RECONCILIATION_ROADMAP.md:11`) **لم يُحسم** · Issue #11 **لم يُمسّ** · لم يُعَد `FINAL-B` ولا §13b · `AUTHORITY.md` و`methodology/**` و`phases/**` **لم تُمسّ** · **لا merge ولا tag ولا release**.
- files changed: **ثلاثة** — `decisions/open-decisions.md` · `handoff/handoff.md` · `traceability/rar-reconciliation/P3-CLOSURE-INVENTORY.md`. **ولم يُنشأ ملف جديد** — ولذلك `INDEX.md` **لم يُعدَّل** وتغطية **EC-3 = 159/159 بلا تغيير**.
- **وعاء المراجعة — إثبات عدم الحاجة إلى ملف جديد (‏قيد «التفضيل للتمديد»):** §3 **إجراء خروج لا قالب جديد** بنصّها (`origin/main:30`)، وتنهى عن «قوائم مراجعة موازية». والأوعية القائمة تكفي وتغطي الأدوار الثلاثة: **القرار** ⇒ `decisions/open-decisions.md` (المرتبة 4 — المرجع الملزم للمفتوح/المقفل، §3.2) · **سجل المراجعة** ⇒ `handoff/handoff.md` (المرتبة 9 — §3.6 «`handoff` محدَّث عند وجوب ذلك»، وH-0022 سبق أن حمل جرداً بالشكل نفسه) · **الجرد التفصيلي** ⇒ `P3-CLOSURE-INVENTORY.md` (غير حاكم — وثيقة إحالة). **فلا وعاء ناقص ⇒ لا ملف جديد**، وبذلك لا يتغيّر `INDEX.md` ولا EC-3.
- decisions: **قرار مالك واحد** = **إغلاق نطاق `P3`** (‏`OD-P3-CLOSURE`) بقراراته الخمسة المسجَّلة. لا ADR · لا قرار معماري · لا إعادة ترقيم لأي `OD` قائم · لا تغيير لحالة أي `OD` آخر · `AUTHORITY.md` لم تُمسّ · **ولم تُنشأ طبقة سلطة جديدة**.
- risks: (1) **`P3` مغلقة النطاق بينما `FP-0001` `BLOCKED` والتجميد `ACTIVE`** — بقرار مالك صريح؛ والضمانة أن **`P3-CI-02` و`P3-CI-26` يبقيان `GOVERNED TRANSFER` بحقول كاملة** فلا يسقط الالتزام. (2) **إغلاق النطاق قد يُقرأ خطأً اكتمالاً للمشروع** — مُعالَج بقاعدة §3.9 المسجَّلة حرفيّاً في الوعاء الحاكم. (3) **وراثة §3 لا تتحقق نصاً على الفرع قبل الدمج** — مسجَّلة قيداً تنفيذياً هنا وفي `H-0023:485`. (4) **توسعة نطاق `R3` على PR #9** — مُفصح عنها ومقبولة غير حاجبة بقرار مالك. (5) **`GOV-OBS-03` و`P3-CI-28` و`OD-GOV-1/2` و`OD-P3-2` تبقى مفتوحة بعد الإغلاق** — منقولةً حاكمياً لا مُسقَطة، وهذا نصّ §3.9-3.
- tests: `origin/main` = **`7611ed9531660f5f4762f3e6a60f05cdf0f419b4`** (مطابق للمتوقع) · PR #9 head قبل الدفعة = **`8a5b2f6ba66462042c988987bf056e541e1095b0`** (مطابق) · الفرع = **`docs/r2-activation-rar-reconciliation`** (مطابق) · **25 commit** فوق نقطة الافتراق (مطابق) · **صفر merge commit** (مطابق) · **`main` غير مستوعَب** (مطابق) · PR #9 **`OPEN — NOT MERGED`** · parent count = **1** · بلا rebase/amend/force-push · **260** صفاً (تحقّق آليّ) · التوزيع **`116/80/46/18/0`** (تحقّق آليّ) · كل صف **6 أعمدة** · §13b **DETERMINED** بـ`33+7+6=46` · البصمات الأربع **byte-identical** · صفر مساس بمخرج مجمَّد منذ `f6ec1f3` · مراسي الغياب **111/111 · صفر مكسورة · صفر مكرَّرة** · **صفر `placeholder` غير محلول** · EC-3 = **159/159 · صفر غير مغطى** · المعادلة **`28 = 13 + 15 + 0`** · **`UNCLASSIFIED = 0`** · **`BLOCKING REMAINDER = 0`** · `P3-CI-01..28` بلا فجوات · `P3-CI-02` و`P3-CI-26` = **13/13** · `FP-0001` = **`BLOCKED`** · التجميد **`ACTIVE`** · `R3` = **`ACTIVE — SPECIFICATION ONLY`** · `phases/**` و`methodology/**` و`AUTHORITY.md` **byte-identical** · `git diff --check` نظيف · worktree نظيف بعد الدفع · **لا وسم ولا إصدار**.
- next step: **خطوات المالك حصراً — ولا شيء منها مأذون به في هذه الجولة:** (1) **دمج PR #9**؛ (2) **الوسم (tag)**؛ (3) **الإصدار (release)**؛ (4) **تفعيل `R4`** بأمر صريح. وبالتوازي — وبأوامر مستقلة — يبقى مسار `R3` قائماً: اعتماد المعايير السبعة ⇒ **أمر تقنين** يملأ `ui/UI_DESIGN_SYSTEM.md` §9 ⇒ **أمر إنشاء عقد الحقل** (المرتبة 5) ⇒ بناء الاختبارات وتنفيذها ⇒ المعالجة ⇒ فحوص بوابة `FP-0001` ⇒ **رفع التجميد بقرار مالك**. **ورفع التجميد لا يقع بإغلاق `P3` ولا بانقضاء وقت ولا صمتاً.**
- do not touch: constitution.md · AUTHORITY.md · decisions/adr/** · contracts/** · superseded/** · ui/** · catalogs/** · **phases/** (بما فيه `phase-roadmap.md` و`PHASE_MASTER_PLAN.md` — `NO UPDATE REQUIRED`)** · methodology/** · `references/analysis-inputs/rar-2026-07/**` · **`traceability/r3-accessibility/**`** (محتوى `R3` — توسعة مسجَّلة لا تُمسّ) · جداول المصالحة السبعة وتصنيفاتها ووجهاتها · `FINAL-B-13B-DETERMINATION.md` · `FINAL-RECONCILIATION-TABLE.md` · خط الأساس المجمَّد `188ad37` · **‏GitHub Issue #11** · الوسوم v1.0..v1.3.1 · **H-0016..H-0026**.

## Handoff H-0028
> **‏R3 — Governing Transfer Preparation.** يُقرأ بعد `H-0027` ولا ينسخه: `H-0027` صحيحٌ في تاريخه وقد أُغلق **نطاق `P3`** ووُسم `v1.4-p3-rar-reconciliation-closure`؛ **وهذه الجولة جولةُ نقلٍ حاكم فقط** — لا تصحيحَ لملفَّي `R3`، ولا تقنينَ إتاحة، ولا معالجة، ولا بناءَ اختبارات. **لا إعادة كتابة لأي مدخل سابق.** **ولا تغيير في `FP-0001` ولا في التجميد ولا في جرد `P3` ولا في أي مخرج مجمَّد.**
- date: 2026-08-02
- phase: **R3 — Governing Transfer Preparation** — فرع جديد `docs/r3-governing-transfer` من `origin/main` مباشرة · **PR غير مدموج**
- task/goal: نقلُ ثلاثة قرارات مالك معتمدة من مصدرها التاريخي (‏`GitHub Issue #11`) إلى **أوعيتها الحاكمة**، وتسجيلُ **سند استمرار** Accessibility Sub-track استثناءً تنفيذياً محدوداً. **لا merge · لا tag · لا release · لا rebase · لا amend · لا force-push · لا رفع تجميد · لا فكّ حجب `FP-0001` · لا تفعيل `R4` · لا إغلاق `Issue`.**
- base SHA: **`origin/main` = `04bdbb32ab610b4f33df7332fe010da6f099ef2c`** · **الوسم** `v1.4-p3-rar-reconciliation-closure` (كائن وسم `a490ad2810f4b43d07a5600bfc6dd4d7489c2312` ⇒ **هدفه** `04bdbb32…` = `main`) · **صفر commit بعد الوسم على `main`** · **عدد الوسوم = 16**.
- **خطية الفرع:** أُنشئ من `origin/main` مباشرة · **ثلاثة commits** كلٌّ **بأبٍ واحد** · **صفر merge commit** · بلا rebase ولا amend ولا force-push.

**تصحيح نطاق مقابل `H-0027` — لا تعارض صامتاً:** قائمة «do not touch» في `H-0027` كانت قيد **تلك** الجولة وتضمّنت `ui/**` و`contracts/**`. **وأمر المالك الصادر 2026-08-02 يخوّل صراحةً** تعديل **ثلاثة ملفات بعينها**: `ui/UI_COMPONENT_STATES.md` · `ui/UI_FIELD_NAMING.md` · `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md`. **وما عداها من `ui/**` و`contracts/**` يبقى محظوراً**، وعلى رأسه `ui/UI_DESIGN_SYSTEM.md` و`ui/UI_ACTION_BUTTON_MODEL.md` — **ولم يُمسّا**.

**مطابقة المصدر قبل النقل — `GitHub Issue #11`:**

| القرار | `Comment ID` | `created_at` | `updated_at` | `SHA-256` (بداية الجولة = قبل النقل) |
|---|---|---|---|---|
| **`OD-R3-UI-1`** | `5156528819` | `2026-08-02T08:26:18Z` | `2026-08-02T08:26:18Z` | `df92080cad347046ce935bf30cc5f08e2cd5bdab976ba8f27e5a3bdcccbeb843` |
| **`OD-R3-UI-2`** | `5156530178` | `2026-08-02T08:26:33Z` | `2026-08-02T08:26:33Z` | `e79b5ab4f69f7c9a7c1244bc452e89981a2616be6bf0e0ec345ff90cc1d31e9d` |
| **`OD-R3-UI-3`** | `5156531912` | `2026-08-02T08:26:51Z` | `2026-08-02T08:26:51Z` | `78ec5c6a19daec7a22ce48354fed479f8c7d47448fdf688dad8a4827eb160edd` |

`updated_at = created_at` في الثلاثة ⇒ **لا تعديل بعد اعتماد المالك**. وأُعيد الحساب **مباشرةً قبل تنفيذ النقل** فطابق **بايتاً ببايت** ⇒ **لا تغيير في المصدر أثناء التنفيذ**. والبصمة على **جسم التعليق كما تُرجعه `GitHub REST API` (`.body`) بلا محرف سطر مُضاف**. **و`Issue #11` لم يُمسّ.**

**الـcommits الثلاثة:**

| # | `commit` | الأب | الرسالة | الملفات |
|---|---|---|---|---|
| **1** | `5eed4b52eb1e1d379c3cabd773331ac9aed7744a` | `04bdbb32ab610b4f33df7332fe010da6f099ef2c` | `docs(r3): record bounded accessibility sub-track authorization` | `decisions/open-decisions.md` · `INDEX.md` |
| **2** | `826a51eac971e379b065cba8f21caa1d023c34c1` | `5eed4b52eb1e1d379c3cabd773331ac9aed7744a` | `docs(ui): transfer approved surface, naming, and disabled-state rules` | `ui/UI_COMPONENT_STATES.md` · `ui/UI_FIELD_NAMING.md` · `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` · `INDEX.md` |
| **3** | **هذا المدخل** — أبوه `826a51eac971e379b065cba8f21caa1d023c34c1` | `826a51eac971e379b065cba8f21caa1d023c34c1` | `docs(r3): record governing-transfer preparation and handoff` | `decisions/open-decisions.md` · `handoff/handoff.md` · `INDEX.md` |

- **حالة النقل:** **`OWNER APPROVED · DURABLY RECORDED · GOVERNING TRANSFER PREPARED · EFFECTIVE UPON MERGE`**. **ولا تُستعمل `TRANSFERRED` قبل الدمج** — الأوعية الثلاثة **لا تنفذ** حتى الدمج في `main`.
- completed: `decisions/open-decisions.md` (‏v3.0 → **v3.2**: +**`OD-R3-SCOPE-1`** سند استمرار Accessibility Sub-track — استثناء تنفيذي محدود + تطبيق قاعدة «توسّع Enterprise UI Governance لا يوسّع شروط رفع التجميد» + **«سجل النقل الحاكم — قرارات واجهة `R3`»** بمصدره وبصماته وأوعيته و`commit` SHAs) · `ui/UI_COMPONENT_STATES.md` (‏v1.1 → **v1.2**: أنماط `S8` الأربعة الإلزامية — نقل `OD-R3-UI-1`) · `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` (‏v1.0 → **v1.1**: §3 `surfaces[]` مغلق التعداد + §3.2 حقول السطح + §3.3 القواعد الثماني — نقل `OD-R3-UI-2` و`OD-R3-UI-3`) · `ui/UI_FIELD_NAMING.md` (‏v1.1 → **v1.2**: الاسم الدلالي المحكوم مقابل النص الظاهر — نقل مبدأ `OD-R3-UI-3`) · `INDEX.md` (تحديث **أربعة صفوف** فقط) · هذا المدخل.
- **`OD-R3-SCOPE-1` — حدوده المسجَّلة:** **لا يعدّل `methodology/RECONCILIATION_ROADMAP.md`** · **لا يدّعي أن الإتاحة جزء أصليّ من ميثاق `R3`** · **لا يعيد تعريف `R3`** · **لا يُنشئ مسار `R` جديداً** · **لا يضيف شرطاً إلى `OD-FP-0001-FREEZE`** · **لا يحلّ تعارض المرتبتين 2 و4**. وظيفتُه الوحيدة **السماح باستمرار العمل الحالي على الدلتا السبعة** `RAR-003 [38] [40] [42] [43] [44] [46] [48]`، **وينتهي عند إغلاقها**. والتسوية النهائية لاسم `R3` ونطاقه تبقى **`AUTHORITY CONFLICT — SEPARATE OWNER ACTION`** وتُراجَع **ديناً حوكمياً في `Phase Exit Review`**.
- not completed: **ملفّا `R3` لم يُمسّا** (`traceability/r3-accessibility/R3-ACCESSIBILITY-SPECIFICATION.md` · `…-TEST-MATRIX.md`) — **لا تصحيح لهما في هذه الجولة** · **الدلتا السبعة لم تُعالَج ولم تُقنَّن** (`NOT REMEDIATED`) · `ui/UI_DESIGN_SYSTEM.md` **§9 لم يُمسّ** · **لا معيار `PASS`** · لم يُبنَ ولم يُنفَّذ أيُّ اختبار · **التجميد لم يُرفع** (`OD-FP-0001-FREEZE` = **`ACTIVE`**) · **`FP-0001` = `BLOCKED`** · **شروط الرفع لم تُعدَّل ولم يُعَد عدُّها** · **`R3` لم تُغلق** (`ACTIVE — SPECIFICATION ONLY`) · **`R4` لم تُفعَّل** · `GOV-OBS-03` و`P3-CI-28` و`OD-GOV-1` و`OD-GOV-2` و`OD-P3-2` **لم تُحسم** · `P3-CI-08` لم يُنفَّذ · **تعارض ميثاق `R3` لم يُحسم** · **`Issue #11` لم يُمسّ ولم يُغلق** · لم يُعَد `FINAL-B` ولا §13b · **لا merge ولا tag ولا release**.
- files changed: **ستة عبر الجولة كلها** — `decisions/open-decisions.md` · `ui/UI_COMPONENT_STATES.md` · `ui/UI_FIELD_NAMING.md` · `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` · `handoff/handoff.md` · `INDEX.md`. **ولم يُنشأ ملف جديد** ⇒ **لا صفّ جديد في `INDEX.md`** والإجمالي **158 ملفاً + الفهرس** بلا تغيير · **EC-3 = 159/159 بلا تغيير**.
- decisions: **قرار مالك واحد جديد** = **`OD-R3-SCOPE-1`** (سند استمرار — استثناء تنفيذي محدود). و**ثلاثة قرارات مالك سابقة نُقلت** إلى أوعيتها (`OD-R3-UI-1/2/3`) **بلا تعديل دلالاتها**. لا ADR · لا قرار معماري · لا إعادة ترقيم لأي `OD` قائم · لا تغيير لحالة أي `OD` آخر · `AUTHORITY.md` و`constitution.md` و`methodology/**` **لم تُمسّ** · **ولم تُنشأ طبقة سلطة جديدة**.
- risks: (1) **قراءة النقل نفاذاً قبل الدمج** — مُعالَج بقاعدة لفظية ملزمة: `EFFECTIVE UPON MERGE`، و**لا تُستعمل `TRANSFERRED` قبل الدمج**. (2) **قراءة `OD-R3-SCOPE-1` حسماً لتعارض السلطة** — مُعالَج بنصّ صريح: التسوية النهائية **`AUTHORITY CONFLICT — SEPARATE OWNER ACTION`**. (3) **قراءة توسّع حوكمة الواجهة شرطَ رفعٍ جديداً** — مُعالَج بقاعدة §(ج) من سجل السند: أي شرط جديد **يحتاج قرار مالك يعدّل سجل التجميد نفسه**. (4) **تناقض ظاهريّ مع `do not touch` في `H-0027`** — مُعالَج بفقرة «تصحيح نطاق» أعلاه، والتخويل **محصور في ثلاثة ملفات بعينها**. (5) **بقاء ملفَّي `R3` غير متسقين مع القواعد المنقولة** — مقصود: **التصحيح خارج نطاق هذه الجولة** ومسجَّل هنا حتى لا يعيش في الذاكرة.
- tests: `origin/main` = **`04bdbb32ab610b4f33df7332fe010da6f099ef2c`** (مطابق) · الوسم `v1.4-p3-rar-reconciliation-closure` ⇒ هدفه **`04bdbb32…`** (مطابق) · **صفر commit** بعد الوسم على `main` · **عدد الوسوم = 16** (قبل/بعد) · **ثلاثة commits** · `parent count = 1` لكلٍّ · `git rev-list --merges origin/main..HEAD` = **0** · `git diff --check` **نظيف** · **صفر تعديل على `traceability/**`** · الأدلة المجمَّدة **byte-identical** (‏`FINAL-B-13B-DETERMINATION.md` `806ebc47…` · `FINAL-RECONCILIATION-TABLE.md` `d8be1b85…` · `P3-CLOSURE-INVENTORY.md` `cac1ba06…` · `SECTION-18-BLOCKING-EFFECT.md` `b587f20c…` · `R3-ACCESSIBILITY-SPECIFICATION.md` `251f1039…` · `R3-ACCESSIBILITY-TEST-MATRIX.md` `eb32cb9e…`) · `AUTHORITY.md` (`5b639cf4…`) و`constitution.md` (`79d51ddf…`) و`methodology/RECONCILIATION_ROADMAP.md` (`a093beba…`) و`methodology/PHASE_EXECUTION_STANDARD.md` (`f052d1d7…`) و`ui/UI_DESIGN_SYSTEM.md` (`d0a6262d…`) و`ui/UI_ACTION_BUTTON_MODEL.md` (`6d827562…`) **byte-identical** · جرد `P3` **`28 = 13 + 15 + 0`** · **`UNCLASSIFIED = 0`** · `FP-0001` = **`BLOCKED`** · التجميد **`ACTIVE`** · `R3` = **`ACTIVE — SPECIFICATION ONLY`** · **`R4` غير مفعَّلة** · **صفر معيار `PASS`** · **صفر `placeholder` غير محلول** · `INDEX.md` **مطابق للشجرة** (‏158 صفاً + الفهرس · صفر ملف خارج الفهرس · صفر صفّ بلا ملف) · worktree نظيف بعد الدفع · **لا وسم ولا إصدار**.
- next step: **قرار مالك في الـPR** (‏دمج أو رفض) — **والنفاذ يبدأ عند الدمج فقط**. وبعده، **بأوامر مستقلة**: تصحيح ملفَّي `R3` وفق القواعد المنقولة (`R3-A11Y-02` · `R3-A11Y-T-010` · `R3-A11Y-01` · `R3-A11Y-05` · `R3-A11Y-T-001`) ⇒ **أمر تقنين** يملأ `ui/UI_DESIGN_SYSTEM.md` §9 ⇒ **أمر إنشاء عقد الحقل** (المرتبة 5) ⇒ بناء الاختبارات وتنفيذها ⇒ المعالجة ⇒ فحوص بوابة `FP-0001` ⇒ **رفع التجميد بقرار مالك**. **وتبقى تسوية اسم `R3` ونطاقه قراراً مالكياً مستقلاً.** **ولا شيء من ذلك مأذون به في هذه الجولة.**
- do not touch: constitution.md · AUTHORITY.md · methodology/** · phases/** · `traceability/rar-reconciliation/**` (بما فيه `P3-CLOSURE-INVENTORY.md`) · **الآثار التاريخية المجمَّدة** · decisions/adr/** · catalogs/** · **`ui/UI_DESIGN_SYSTEM.md`** · **`ui/UI_ACTION_BUTTON_MODEL.md`** · **`traceability/r3-accessibility/**`** · **‏GitHub Issue #11** · أي ملف في `aql` · **أي وسم أو إصدار** · **أي سجل تفعيل `R4`** · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.4 · **H-0016..H-0027**.

## Handoff H-0029
> **‏R3 — Non-Governing Specification Correction Package.** يُقرأ بعد `H-0028` ولا ينسخه: `H-0028` صحيحٌ في تاريخه وقد **أعدّ** النقل الحاكم لـ`OD-R3-UI-1/2/3`، **ثم دُمج الـPR #12 بقرار المالك** فصارت القواعد **نافذة** على `main`؛ **وهذه الجولة تُصحّح ملفَّي `R3` غير الحاكمين ليَرِثا تلك القواعد النافذة — لا غير.** **لا إعادة كتابة لأي مدخل سابق.** **ولا تغيير في `FP-0001` ولا في التجميد ولا في جرد `P3` ولا في أي مخرج مجمَّد.**
- date: 2026-08-02
- phase: **R3 — Non-Governing Specification Correction** — فرع جديد `docs/r3-spec-correction` من `origin/main` مباشرة · **PR غير مدموج**
- task/goal: مواءمة `traceability/r3-accessibility/R3-ACCESSIBILITY-SPECIFICATION.md` و`…-TEST-MATRIX.md` مع **قواعد الواجهة المنقولة النافذة** — **سبعة تصحيحات لا ثامن لها**. **لا تقنين · لا معالجة · لا بناء اختبارات ولا تنفيذها · لا معيار `PASS` · لا merge · لا tag · لا release · لا rebase · لا amend · لا force-push · لا رفع تجميد · لا فكّ حجب `FP-0001` · لا إغلاق `R3` · لا تفعيل `R4`.**

**‏Owner Authorization — 2026-08-02 (تسجيل إلزامي · إذن مؤقت منتهٍ):** أصدر المالك إذناً يرفع **مؤقتاً ولأغراض هذه الجولة فقط** القيدَ المنشور في `H-0028` («do not touch: `traceability/r3-accessibility/**`»). **حدوده المسجَّلة:** مرتبطٌ **حصراً** بنقطة الأساس **`a8ef8d9e990195f364fb81465856f3176d323dd6`** · محصورٌ في **ملفَّي `R3` أعلاه** + التحديثات التابعة في `INDEX.md` و`handoff/handoff.md` · **لا يرفع القيد دائماً** · **لا يأذن بأي ملف آخر في `traceability/**` ولا بـ`ui/**` ولا بـ`contracts/**`** · **لا تقنين ولا معالجة ولا بناء/تنفيذ اختبارات ولا إعلان `PASS`** · **لا يرفع `OD-FP-0001-FREEZE`** ولا يفكّ حجب `FP-0001` · **لا يغلق `R3`** ولا يفعّل `R4` · **لا دمج ولا وسم ولا إصدار**. **وينتهي تلقائياً** عند إعداد الـPR غير المدموج لهذه الجولة، أو عند اختلاف نقطة الأساس، أو عند ظهور تعارض سلطوي أو حاجة إلى ملف غير مأذون. ⇒ **وبإعداد الـPR في هذه الجولة يعود القيد على `traceability/r3-accessibility/**` نافذاً كما كان.**
- base SHA: **`origin/main` = `a8ef8d9e990195f364fb81465856f3176d323dd6`** — **merge commit** أبواه `04bdbb32ab610b4f33df7332fe010da6f099ef2c` و`1f3b1dbc76817fd2194186f0a5dbd0f156c6191c` (دمج PR #12) · **عدد الوسوم = 16** · الوسم الأحدث `v1.4-p3-rar-reconciliation-closure`.
- **خطية الفرع:** أُنشئ من `origin/main` مباشرة · **commit واحد بأبٍ واحد** · **صفر merge commit** · بلا rebase ولا amend ولا force-push.

**تغيّرٌ حاكمٌ يُسجَّل ولا يُفترض:** بدمج **PR #12** تحقّق شرطُ `EFFECTIVE UPON MERGE` المسجَّل في `decisions/open-decisions.md` §(د)، فصار `OD-R3-UI-1` و`OD-R3-UI-2` و`OD-R3-UI-3` **نافذةً** في أوعيتها الحاكمة. **ومصدر القواعد في هذه الجولة هو النصّ المنشور على `main` حصراً** — لا `Issue #11` ولا ملخّص محادثة ولا `handoff` قديم ولا تقرير سابق. والأوعية المقروءة: `ui/UI_COMPONENT_STATES.md` (‏Δ v1.2 — أنماط `S8`) · `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` (‏§3.1–§3.3 — `surfaces[]`) · `ui/UI_FIELD_NAMING.md` (‏Δ v1.2 — الاسم الدلالي المحكوم). **ولم يُمسّ أيٌّ منها.**

**التصحيحات السبعة — لا ثامن:**

| # | الموضع | ما تغيّر | المرجع الحاكم |
|---|---|---|---|
| **1** | `SPEC` → `R3-A11Y-02` المتطلب (ج) | **قاعدة منع التركيز المطلقة** ⇒ **وراثة الحالة المعلَنة**: `S7` (‏`HIDDEN-SERVER`) · `S8:NATIVE` · `S8:ARIA_FOCUSABLE` · `S8:READ_ONLY` · `S8:LOCKED` — **ولا يُقبل `S8` بلا نمط**؛ و`S9` و`S10` **بدلالاتهما دون تغيير** | `ui/UI_COMPONENT_STATES.md` Δ v1.2 §1 و§2 و§3 · `SCREEN_CONTRACT_TEMPLATE.md` §3.3-6/7 |
| **2** | `MATRIX` → `T-010` | معيار «صفر عنصر مخفي/معطَّل استقبل التركيز» ⇒ **اختبار مطابقة النمط المعلَن**؛ و**الفشل عند مخالفة النمط لا عند استقبال التركيز مطلقاً**. **المعرّف والنوع بلا تغيير · ولم يُنشأ اختبار جديد** | كما أعلاه |
| **3** | `SPEC` → `R3-A11Y-01` المتطلب (أ) و(ب) | إعادة صياغة على **`surfaces[].type`**: `h1` **لـ`PAGE` وحده** ولا تُفرض على `DIALOG`/`DRAWER`/`INLINE_PANEL`/`TRANSIENT` · **مناطق الإطار الأربع تخصّ Application Shell لا كلَّ سطح** (وقواعد الإطار القائمة **لم تُضعَّف ولم تُحذف**) · ومتطلبات الاسم/العنوان/التركيز/الإعلان **بحسب نوع السطح والعقد**. **ولم يُضَف نوع سطح جديد** | `SCREEN_CONTRACT_TEMPLATE.md` §3.1 القواعد 2 و3 · §3.3-5 |
| **4** | `SPEC` → `R3-A11Y-02` (د)(ز) والنطاق والسلوك المحظور · `R3-A11Y-06` أثر RTL · `MATRIX` → `T-013` | **توحيد المفردات المهجورة** (`page`/`modal`/`drawer`/`inline`/`toast`/«سطح ثانوي») على التعداد المغلق **`PAGE`/`DIALOG`/`DRAWER`/`INLINE_PANEL`/`TRANSIENT`** · وقواعد الدخول والعودة صارت على **`focus_return_target`** ∈ { `AUTO_TRIGGER` · `<control_id>` · `<action_id>` } — **لا قيمة `null`**، **وهدفٌ بديل صريح في العقد** إن كان الضابط المطلق قد يزول | `SCREEN_CONTRACT_TEMPLATE.md` §3.1 (خريطة التحويل) · §3.2 · §3.3-3/4 |
| **5** | `SPEC` → `R3-A11Y-05` المتطلب (د) و(ح) والنطاق والمكوّنات | `modal`/`drawer` ⇒ **`DIALOG`/`DRAWER`**، وحصرُ التركيز والعودة **على `DIALOG` و`DRAWER` القابلَين للإغلاق وفق العقد**؛ **و`TRANSIENT` لا يحصر التركيز**، **ولا يُعمَّم الحصر على `INLINE_PANEL`**. **والاستثناء القائم (‏`queue.approval_detail`) لم يُمسّ — byte-identical** | `SCREEN_CONTRACT_TEMPLATE.md` §3.1 القاعدتان 4 و5 · §3.3-3 |
| **6** | `SPEC` → `R3-A11Y-01` المتطلب (أ-1) | **التطابق الحرفي مع عنوان الجرد** ⇒ **الاسم الدلالي المحكوم**: `screen_id`/`screen_name` مرجعُ المعنى، والنص الظاهر من **`presentation_label_key`**، **ويجوز اختلافه أسلوبياً** ولا يجوز أن يغيّر المعنى التجاري/القانوني ولا ربط الـAPI ولا الصلاحية ولا دلالة التدقيق، **والاسم المتاح قابل للتتبّع إلى `screen_id`**. **وقاعدة الاشتقاق النصي للاسم المحكوم لم تُغيَّر** | `ui/UI_FIELD_NAMING.md` Δ v1.2 §1 و§2 القواعد 1 و2 و5 · `SCREEN_CONTRACT_TEMPLATE.md` §3.2 |
| **7** | `MATRIX` → `T-001` | **المقارنة النصّية الحرفية بعنوان الجرد** ⇒ فحصُ **اسم متاح صالح لكل سطح** + **مطابقة المصدر لـ`accessible_name_source`** + **استعمال `presentation_label_key`** + **التتبّع إلى `screen_id`**؛ **ولا يُشترط تطابق حرفي**، **والفشل عند تغيُّر المعنى المحكوم أو انقطاع التتبّع**. **المعرّف بلا تغيير** | كما أعلاه |

- **إفصاح نطاقي — ما لم يُمسّ عمداً داخل الملفَّين:** صفوف `T-029`..`T-034` (‏`R3-A11Y-05`) **لم تُعدَّل**: لا تحوي أياً من الرموز الخمسة المهجورة (`page`/`modal`/`drawer`/`inline`/`toast`)، وإنما لفظَ «نافذة» نثراً عربياً؛ **وتعديلها كان سيتجاوز مجموعة التصحيحات السبعة** فامتُنع عنه. **والربط الدلالي قائم** بنصّ `R3-A11Y-05` (ح) المصحَّح. وكذلك **§9 من الوثيقة الأم لم يُمسّ** — فهو سجلٌ تاريخيّ لجولة `v1.0`، وحدودُ هذه الجولة مسجَّلة في ترويسة `v1.1`.
- completed: `traceability/r3-accessibility/R3-ACCESSIBILITY-SPECIFICATION.md` (‏v1.0 → **v1.1** — التصحيحات 1 و3 و4 و5 و6) · `traceability/r3-accessibility/R3-ACCESSIBILITY-TEST-MATRIX.md` (‏v1.0 → **v1.1** — التصحيحات 2 و4 و7) · `INDEX.md` (**صفّان محدَّثان فقط** — لا صفّ جديد) · هذا المدخل.
- not completed: **الدلتا السبعة لم تُعالَج ولم تُقنَّن** (`NOT REMEDIATED`) · `ui/UI_DESIGN_SYSTEM.md` **§9 لم يُمسّ** · **لا معيار `PASS`** وحالة السبعة تبقى **`SPECIFIED — NOT CODIFIED — NOT REMEDIATED — NOT TESTED`** · **لم يُبنَ ولم يُنفَّذ أيُّ اختبار** (‏`DESIGNED — NOT BUILT — NOT EXECUTED`) · **التجميد لم يُرفع** (`OD-FP-0001-FREEZE` = **`ACTIVE`**) · **`FP-0001` = `BLOCKED`** · **شروط الرفع لم تُعدَّل ولم يُعَد عدُّها** · **`R3` لم تُغلق** (`ACTIVE — SPECIFICATION ONLY`) · **`R4` لم تُفعَّل** · **`UI-4` و`UI-5` لم يُنفَّذا** · `GOV-OBS-03` و`P3-CI-28` و`OD-GOV-1` و`OD-GOV-2` و`OD-P3-2` **لم تُحسم** · **تعارض ميثاق `R3` لم يُحسم** · **`Issue #11` لم يُمسّ** · **`ui/**` و`contracts/**` و`methodology/**` و`decisions/**` لم تُمسّ** · **لا merge ولا tag ولا release**.
- files changed: **أربعة** — `traceability/r3-accessibility/R3-ACCESSIBILITY-SPECIFICATION.md` · `traceability/r3-accessibility/R3-ACCESSIBILITY-TEST-MATRIX.md` · `INDEX.md` · `handoff/handoff.md`. **ولم يُنشأ ملف جديد** ⇒ **لا صفّ جديد في `INDEX.md`** · الإجمالي **158 ملفاً + الفهرس** بلا تغيير · **EC-3 = 159/159 بلا تغيير**.
- decisions: **لا قرار مالك جديد** · لا ADR · لا قرار معماري · **لا `OD` أُنشئ ولا أُعيد ترقيمه ولا تغيّرت حالته** · `decisions/open-decisions.md` **لم يُمسّ** · **ولم تُنشأ طبقة سلطة جديدة**. وهذه الجولة **تصحيحُ محتوىً في وثيقتين غير حاكمتين** — **وجودُ القاعدة فيهما لا يُعدّ تقنيناً ولا `GOVERNED TRANSFER`** (`methodology/PHASE_EXECUTION_STANDARD.md` §3.4).
- risks: (1) **قراءة التصحيح تقنيناً** — مُعالَج بترويسة `v1.1` في الملفَّين وبالقاعدة القاطعة في صدر الوثيقة الأم: المخرج **تحليلي غير حاكم**، والتقنين يبقى في `ui/UI_DESIGN_SYSTEM.md` §9 **بأمر مستقل**. (2) **قراءة اشتقاق سلوكٍ جديد لأنماط `S8`** — مُعالَج بالنقل الحرفي/بالإحالة الدقيقة إلى `ui/UI_COMPONENT_STATES.md` Δ v1.2 دون زيادة. (3) **بقاء «نافذة» نثراً في `T-029`..`T-034`** — مُفصح عنه أعلاه بوصفه التزاماً بحدود التصحيحات السبعة لا سهواً. (4) **انتهاء الإذن المؤقت** — مسجَّل أعلاه: بإعداد الـPR يعود حظر `traceability/r3-accessibility/**` نافذاً. (5) **قراءة الدمج شرطاً مستوفى** — النفاذ يبدأ **عند الدمج فقط**، والـPR **غير مدموج**.
- tests: (‏نتائج فحوص ما بعد التعديل مثبَّتة في وصف الـPR وفي تقرير الجولة) — **أربعة ملفات معدَّلة فقط** · **commit واحد بأبٍ واحد** = `a8ef8d9e…` · **صفر merge commit** · `git diff --check` **نظيف** · `R3-A11Y-01..07` **سبعة بلا فجوات ولا تكرار تعريفي** · `R3-A11Y-T-001..046` **ستة وأربعون بلا فجوات** · **صفر معيار `PASS`** · **صفر `placeholder` جديد** · **EC-3 = 159/159** بلا صفّ جديد · `INDEX.md` **مطابق للشجرة** · جرد `P3` **`28 = 13 + 15 + 0`** · **`UNCLASSIFIED = 0`** · `FP-0001` = **`BLOCKED`** · التجميد **`ACTIVE`** · `R3` = **`ACTIVE — SPECIFICATION ONLY`** · **`R4` غير مفعَّلة** · الأدلة المجمَّدة **byte-identical** · `ui/**` و`contracts/**` و`methodology/**` و`AUTHORITY.md` و`constitution.md` و`decisions/**` **byte-identical** · **عدد الوسوم = 16** · **صفر تعديل** على `T-007` و`RUN-MATRIX` و`AIGEN` و`META` · **الاستثناء في `R3-A11Y-05` byte-identical**.
- next step: **قرار مالك في الـPR** (‏دمج أو رفض) — **والنفاذ يبدأ عند الدمج فقط**. وبعده، **بأوامر مستقلة**: **أمر تقنين** يملأ `ui/UI_DESIGN_SYSTEM.md` §9 بصيغة قابلة للاختبار ⇒ **أمر إنشاء عقد الحقل** (المرتبة 5) ⇒ بناء الاختبارات وتنفيذها ⇒ المعالجة ⇒ فحوص بوابة `FP-0001` ⇒ **رفع التجميد بقرار مالك**. **وتبقى تسوية اسم `R3` ونطاقه قراراً مالكياً مستقلاً.** **ولا شيء من ذلك مأذون به في هذه الجولة.**
- do not touch: constitution.md · AUTHORITY.md · methodology/** · phases/** · `traceability/rar-reconciliation/**` (بما فيه `P3-CLOSURE-INVENTORY.md`) · **الآثار التاريخية المجمَّدة** · decisions/** (بما فيه `open-decisions.md` و`adr/**`) · catalogs/** · **`ui/**`** · **`contracts/**`** · **‏GitHub Issue #11** · أي ملف في `aql` · **أي وسم أو إصدار** · **أي سجل تفعيل `R4`** · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.4 · **H-0016..H-0028** · **و`traceability/r3-accessibility/**` — يعود محظوراً بانتهاء الإذن المؤقت عند إعداد الـPR**.

## Handoff H-0030
> **‏R3 — Corrective Commit inside PR #13 (‏Review Defects).** يُقرأ بعد `H-0029` **ولا يعيد كتابته**: `H-0029` صحيحٌ في تاريخه وقد أعدّ حزمة التصحيح السبعة؛ **ثم كشفت مراجعةٌ مستقلة ثلاثة عيوب فيها**، وهذه الجولة **تصحّحها بـcommit واحد فوق `f2faf7af…` داخل الـPR نفسه**. **قاعدة السجل المتجدد** (`handoff.md` §الاتفاقية) تمنع إعادة كتابة مدخل سابق **وقد صار `H-0029` مدفوعاً في PR #13** ⇒ **استُعمل المعرّف التالي `H-0030`**. **ولا تغيير في `FP-0001` ولا في التجميد ولا في جرد `P3` ولا في أي مخرج مجمَّد.**
- date: 2026-08-02
- phase: **R3 — Non-Governing Specification Correction · دفعة تصحيح المراجعة** — **الفرع نفسه** `docs/r3-spec-correction` · **PR #13 نفسه — غير مدموج · لم يُنشأ فرع ولا PR جديد**
- task/goal: معالجة **ثلاثة عيوب** كشفتها المراجعة المستقلة على الحزمة، بـ**أربعة تصحيحات** في ملفَّي `R3` غير الحاكمين. **لا توسيع نطاق · لا تقنين · لا معالجة · لا بناء اختبارات ولا تنفيذها · لا معيار `PASS` · لا merge · لا tag · لا release · لا amend · لا rebase · لا force-push.**
- base SHA: **`origin/main` = `a8ef8d9e990195f364fb81465856f3176d323dd6`** (بلا تغيير) · **أساس هذه الدفعة:** `f2faf7afed2a554131d4a33cb670bdfd5defeba3` (‏commit `H-0029`).
- **خطية الفرع:** **commitان اثنان فقط فوق `main`** · كلٌّ **بأبٍ واحد** · **صفر merge commit** · بلا rebase ولا amend ولا force-push.

**‏Owner Authorization — 2026-08-02 (إذن محدود ثانٍ · مسجَّل):** أذن المالك بإضافة **commit تصحيحي واحد فقط** إلى PR #13، محصوراً في **`R3-ACCESSIBILITY-SPECIFICATION.md` · `R3-ACCESSIBILITY-TEST-MATRIX.md` · `INDEX.md` · `handoff/handoff.md`** — **ولا يسمح بأي تعديل آخر**. **وينتهي عند دفع commit التصحيح وعودة PR #13 إلى حالة جاهزة للمراجعة** ⇒ **وقد انتهى بدفع هذه الدفعة**، فعاد حظر `traceability/r3-accessibility/**` نافذاً.

**العيوب الثلاثة التي كشفتها المراجعة المستقلة:**

| # | العيب | طبيعته |
|---|---|---|
| **1** | **معادلة جرد `P3` متقادمة** في ترويسة الوثيقة الأم و§1: **`28 = 12 + 16 + 0`** — وهي معادلة ما قبل `Phase Exit Review`؛ والحالة الحاكمة النافذة **`28 = 13 + 15 + 0`** منذ انتقال `P3-CI-15` إلى `COMPLETE` (‏`H-0027`). **نصٌّ متقادم مورَّث من `v1.0`، لا خطأ أحدثته حزمة التصحيح** |
| **2** | **قاعدة مخترَعة لـ`INLINE_PANEL`**: `R3-A11Y-02` (د) بصيغة `v1.1` ألزم بنقل التركيز إلى **كل** `INLINE_PANEL` — **ولا سند لذلك في العقد الحاكم**، الذي يوجب إدارة التركيز والعودة على **`DIALOG`/`DRAWER` القابلَين للإغلاق** وينصّ أن **`TRANSIENT` لا يحصر التركيز**، **ولا يحمل قاعدة عامة لـ`INLINE_PANEL`**. **عيبٌ أحدثته حزمة التصحيح — استنتاجٌ يتجاوز النصّ** |
| **3** | **أثرُ العيب 2 في المصفوفة**: `T-013` بصيغة `v1.1` افترض انتقال التركيز إلى كل `INLINE_PANEL`. **وبالمراجعة نفسها ظهر أثرٌ مماثل في `T-002`**: بقي يفحص المناطق الأربع **بلا تقييدها بـ`Application Shell`**، خلافاً لقاعدة `R3-A11Y-01` (ب) المصحَّحة في `v1.1` — **عدم توريث مكتمل** |

**التصحيحات الأربعة المنفَّذة:**

| # | الموضع | ما تغيّر | السند |
|---|---|---|---|
| **1** | `SPEC` → الترويسة + §1 «جرد `P3`» | **`28 = 12 + 16 + 0`** ⇒ **`28 = 13 COMPLETE + 15 GOVERNED TRANSFER + 0 BLOCKING REMAINDER`** · **`UNCLASSIFIED = 0`**، مع نصٍّ صريح أن المعادلة **لم تتغيّر بسبب جولة `R3`** بل تعكس **حالة `P3` الحاكمة بعد `Phase Exit Review` وإغلاق `P3`**. **نقلٌ عن المصدر لا تعديلٌ له — و`P3-CLOSURE-INVENTORY.md` لم يُمسّ** | `H-0027` · `OD-P3-CLOSURE` · `P3-CLOSURE-INVENTORY.md` |
| **2** | `SPEC` → `R3-A11Y-02` (د) | فُكّ البند إلى **(د-1)** فتح `DIALOG`/`DRAWER` ينقل التركيز **وفق عقد الشاشة** · **(د-2)** الإغلاق يعيده إلى **`focus_return_target`** (لا `null`) · **(د-3)** **`INLINE_PANEL` لا ينتقل إليه التركيز إلا بإعلان صريح في عقد الشاشة**، **ولا يُستنتَج سلوكٌ من النوع وحده** · **(د-4)** **`TRANSIENT` لا يحصر التركيز ولا يستقبل انتقالاً تلقائياً لمجرد ظهوره**. **ولم يُضَف حقل عقدٍ جديد** | `SCREEN_CONTRACT_TEMPLATE.md` §3.1 القاعدتان 4 و5 · §3.2 · §3.3-3/4 |
| **3** | `MATRIX` → `T-013` | يختبر **دائماً** `DIALOG` و`DRAWER` القابلَين للإغلاق و**`focus_return_target`** لهما · و`INLINE_PANEL` **يدخل شرطياً فقط بإعلان العقد** ويُختبر بما أعلنه وحده · **ولا `Focus Return` مفروض عليه بدون إعلان** · **و`TRANSIENT` خارج اختبار الحصر والاستعادة** · **وغيابُ انتقال التركيز إلى `INLINE_PANEL` غير معلَن ليس فشلاً**. **المعرّف والنوع بلا تغيير** | كما أعلاه |
| **4** | `MATRIX` → `T-002` | الفحص **على مستوى `Application Shell` المنطبِق وحده** · **ولا تُفرض المناطق الأربع داخل كل سطح** ولا على `DIALOG`/`DRAWER`/`INLINE_PANEL`/`TRANSIENT` · **وغيابُ منطقة Shell في تكوين منطبِق فشلٌ**. **المعرّف والنوع بلا تغيير · ولم يُنشأ `Applicability Model` ولم تُعدَّل `RUN-MATRIX`** | `R3-A11Y-01` (ب) المصحَّح · `ui/UI_DESIGN_SYSTEM.md:29`/`:32` · `SCREEN_CONTRACT_TEMPLATE.md` §3.1 القاعدة 2 |

- **الجولة لم توسّع النطاق:** **صفر ملف خامس** · **لا معيار ولا اختبار أُنشئ أو حُذف** (‏سبعة معايير · **46** اختباراً) · **`T-001` و`T-007` و`T-010` byte-identical** مع `f2faf7af…` · **`RUN-MATRIX` وأبعادها و`META`/`AIGEN` و`Rendering Mode` و`Authoring Origin` بلا مساس** · **حالة المعايير `SPECIFIED — NOT CODIFIED — NOT REMEDIATED — NOT TESTED` بلا تغيير** · **شروط رفع التجميد بلا تغيير ولم يُعَد عدُّها** · **الاستثناء في `R3-A11Y-05` byte-identical** · **`ui/**` و`contracts/**` و`decisions/**` و`methodology/**` و`phases/**` و`traceability/rar-reconciliation/**` و`AUTHORITY.md` و`constitution.md` byte-identical** · **`Issue #11` لم يُمسّ** · **لا وسم ولا إصدار (‏16 وسماً)**.
- completed: `traceability/r3-accessibility/R3-ACCESSIBILITY-SPECIFICATION.md` (‏v1.1 → **v1.2** — التصحيحان 1 و2) · `traceability/r3-accessibility/R3-ACCESSIBILITY-TEST-MATRIX.md` (‏v1.1 → **v1.2** — التصحيحان 3 و4) · `INDEX.md` (**صفّان محدَّثان** — لا صفّ جديد) · هذا المدخل.
- not completed: **الدلتا السبعة لم تُعالَج ولم تُقنَّن** · `ui/UI_DESIGN_SYSTEM.md` **§9 لم يُمسّ** · **لا معيار `PASS`** · **لم يُبنَ ولم يُنفَّذ أيُّ اختبار** · **التجميد `ACTIVE`** · **`FP-0001` `BLOCKED`** · **`R3` لم تُغلق** (`ACTIVE — SPECIFICATION ONLY`) · **`R4` لم تُفعَّل** · `GOV-OBS-03` و`P3-CI-28` و`OD-GOV-1/2` و`OD-P3-2` **لم تُحسم** · **تعارض ميثاق `R3` لم يُحسم** · **تعارض الوضع الداكن (§8-ب) لم يُحسم** · **`PR #13` لم يُدمج**.
- files changed: **أربعة عبر الجولة كلها** — `traceability/r3-accessibility/R3-ACCESSIBILITY-SPECIFICATION.md` · `traceability/r3-accessibility/R3-ACCESSIBILITY-TEST-MATRIX.md` · `INDEX.md` · `handoff/handoff.md`. **ولم يُنشأ ملف جديد** ⇒ **لا صفّ جديد في `INDEX.md`** · **EC-3 = 159/159 بلا تغيير**.
- decisions: **لا قرار مالك جديد** · لا ADR · **لا `OD` أُنشئ ولا تغيّرت حالته** · `decisions/open-decisions.md` **لم يُمسّ** · **ولم تُنشأ طبقة سلطة جديدة**. والوثيقتان تبقيان **مخرجاً تحليلياً غير حاكم** — **ووجود القاعدة فيهما لا يُعدّ تقنيناً ولا `GOVERNED TRANSFER`** (`methodology/PHASE_EXECUTION_STANDARD.md` §3.4).
- risks: (1) **قراءة تحديث معادلة `P3` تعديلاً للجرد** — مُعالَج بنصّ صريح: نقلٌ عن `P3-CLOSURE-INVENTORY.md` **الذي لم يُمسّ**، وليس أثراً لجولة `R3`. (2) **قراءة `INLINE_PANEL` الشرطي إنشاءً لحقل عقدٍ** — مُعالَج: **لا حقل جديد**، والشرط هو **إعلان العقد القائم**. (3) **قراءة `T-002` إنشاءً لـ`Applicability Model`** — مُعالَج بنصّ الترويسة: لم يُنشأ نموذج انطباق ولم تُعدَّل `RUN-MATRIX`. (4) **تعدّد مداخل `H` لجولة واحدة** — مقصود ومسجَّل: قاعدة عدم إعادة كتابة مدخل مدفوع.
- tests: **commitان فوق `main`** · commit التصحيح **بأبٍ واحد** = `f2faf7afed2a554131d4a33cb670bdfd5defeba3` · **صفر merge commit** · `git diff --check` **نظيف** · **أربعة ملفات فقط** عبر الجولة · معادلة `P3` = **`13 + 15 + 0`** و**`UNCLASSIFIED = 0`** · **`T-002` مقيَّد بـ`Application Shell`** · **`INLINE_PANEL` بلا انتقال تركيز تلقائي** · **`T-013` يعكس القيد نفسه** · **`T-001`/`T-007`/`T-010` byte-identical** · **`RUN-MATRIX` بلا تغيير** · **46 اختباراً بلا فجوات** · **صفر معيار `PASS`** · التجميد **`ACTIVE`** · `FP-0001` **`BLOCKED`** · `R3` **`ACTIVE — SPECIFICATION ONLY`** · **`R4` غير مفعَّلة** · **16 وسماً** · **لا وسم ولا إصدار** · **PR #13 `OPEN — NOT MERGED`**.
- next step: **قرار مالك في PR #13** (‏دمج أو رفض) — **والنفاذ يبدأ عند الدمج فقط**. وبعده وبأوامر مستقلة: **أمر تقنين** يملأ `ui/UI_DESIGN_SYSTEM.md` §9 ⇒ **أمر إنشاء عقد الحقل** ⇒ بناء الاختبارات وتنفيذها ⇒ المعالجة ⇒ فحوص بوابة `FP-0001` ⇒ **رفع التجميد بقرار مالك**.
- do not touch: constitution.md · AUTHORITY.md · methodology/** · phases/** · `traceability/rar-reconciliation/**` · **الآثار التاريخية المجمَّدة** · decisions/** · catalogs/** · **`ui/**`** · **`contracts/**`** · **‏GitHub Issue #11** · أي ملف في `aql` · **أي وسم أو إصدار** · **أي سجل تفعيل `R4`** · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.4 · **H-0016..H-0029** · **و`traceability/r3-accessibility/**` — يعود محظوراً بانتهاء الإذن المحدود عند دفع هذه الدفعة**.

## Handoff H-0031
> **‏R3 — Accessibility §9 Codification.** يُقرأ بعد `H-0030` **ولا يعيد كتابته ولا يحذفه**: `H-0029` و`H-0030` صحيحان في تاريخهما، **ثم دُمج PR #13 بقرار المالك** فتغيّرت الحالة التاريخية على النحو المسجَّل أدناه؛ **وهذه الجولة تقنينٌ حاكمٌ لمعايير الإتاحة السبعة في `ui/UI_DESIGN_SYSTEM.md` §9 — لا غير.** **ولا تغيير في `FP-0001` ولا في التجميد ولا في جرد `P3` ولا في أي مخرج مجمَّد.**
- date: 2026-08-02
- phase: **R3 — Accessibility §9 Codification** — فرع جديد `docs/r3-accessibility-section-9-codification` من `origin/main` مباشرة · **PR مستقل غير مدموج**
- task/goal: **تقنين** المعايير السبعة **`R3-A11Y-01`..`R3-A11Y-07`** داخل `ui/UI_DESIGN_SYSTEM.md` **§9** بصيغة **حاكمة · دقيقة · قابلة للاختبار · قابلة للنجاح أو الفشل · غير وصفية**، وتسجيلُ الواقعة وأثرِها في وعائها الحاكم. **لا معالجة · لا بناء اختبارات ولا تنفيذها · لا معيار `PASS` · لا `UI-4` ولا `UI-5` · لا Screen Contracts ولا `run.list` ولا `admin.actions` · لا Rocket ولا Visual Baseline · لا إعادة فتح `P3` ولا PR #12 ولا PR #13 · لا merge ولا tag ولا release ولا rebase ولا amend ولا force-push · لا رفع تجميد ولا فكّ حجب `FP-0001` ولا إغلاق `R3` ولا تفعيل `R4`.**
- base SHA: **`origin/main` = `765c4504a8e813e031ae0c9fb8b5eaad95f85da2`** — **merge commit** أبواه `a8ef8d9e990195f364fb81465856f3176d323dd6` و`0c339e739b60068b827bf301a78914576fb43371` (‏دمج **PR #13**) · **عدد الوسوم = 16** · الوسم الأحدث `v1.4-p3-rar-reconciliation-closure`.
- **خطية الفرع:** أُنشئ من `origin/main` مباشرة · **commit واحد بأبٍ واحد — أبوه `765c4504a8e813e031ae0c9fb8b5eaad95f85da2`** (‏وهو **الأساس** لا commit هذه الجولة؛ وSHA الـcommit مثبَّت في وصف الـPR بعد الدفع) · **صفر merge commit** · بلا rebase ولا amend ولا force-push.

**قرار الحالة التاريخية — يُسجَّل ولا يُفترض، ولا يُمحى منه سابق:**

| البند | الحالة النافذة عند هذه الجولة | الدليل |
|---|---|---|
| **PR #13** | **`MERGED`** | `gh pr view 13` ⇒ `state = MERGED` · `mergedAt = 2026-08-02T12:23:27Z` |
| **merge commit** | **`765c4504a8e813e031ae0c9fb8b5eaad95f85da2`** | `git rev-parse origin/main` = القيمة نفسها · `git log --oneline -1 origin/main` = `Merge pull request #13 from sa4devops/docs/r3-spec-correction` |
| **العبارات السابقة `OPEN` · `NOT MERGED` · «PR #13 لم يُدمج»** | **`HISTORICAL / STALE EVIDENCE`** — صحيحةٌ في تاريخها، **غيرُ نافذةٍ اليوم** | `H-0030` (سطر `tests`: «PR #13 `OPEN — NOT MERGED`») · `H-0029` (`PR غير مدموج`) — **ولم يُعدَّل أيٌّ منهما ولم يُحذف** |
| **`R3-ACCESSIBILITY-SPECIFICATION.md` · `R3-ACCESSIBILITY-TEST-MATRIX.md`** | **موجودان على `origin/main`** — **ويظلّان `Non-Governing` داخل `traceability/**`** | `git ls-tree origin/main traceability/r3-accessibility/` ⇒ الملفّان · `INDEX.md` ⇒ صفّاهما `Non-governing` · `methodology/PHASE_EXECUTION_STANDARD.md` §3.4 |
| **مستواهما السلطوي** | **لم يُرفع** · **ولم يُنقل محتواهما بوصفه حاكماً تلقائياً** | صياغة §9 استندت إلى **الأوعية الحاكمة الأعلى** (`ui/**` الملزمة · `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` · `decisions/open-decisions.md`)، والملفّان **لم يُمسّا** في هذه الجولة |

> **قاعدة قراءة ملزمة:** استُعملت `traceability/r3-accessibility/**` **استخراجاً للمعايير وربطاً تاريخياً فقط**. **ولم تُنسخ سلطتها**، ولم تُقرأ سنداً حاكماً، ولا يُقرأ التقنينُ ترقيةً لها. **والوعاء الحاكم للقواعد هو `ui/UI_DESIGN_SYSTEM.md` §9 حصراً.**

**ما قُنِّن — سبع قواعد لا ثامنة لها:**

| # | المعرّف | الاسم | الموضع |
|---|---|---|---|
| 1 | **`R3-A11Y-01`** | Semantic Structure | `ui/UI_DESIGN_SYSTEM.md` §9.2 |
| 2 | **`R3-A11Y-02`** | Focus Order | §9.3 |
| 3 | **`R3-A11Y-03`** | Labels and Descriptions | §9.4 |
| 4 | **`R3-A11Y-04`** | Error Association | §9.5 |
| 5 | **`R3-A11Y-05`** | Dialog Focus Trapping | §9.6 |
| 6 | **`R3-A11Y-06`** | Reduced Motion | §9.7 |
| 7 | **`R3-A11Y-07`** | Data Table Semantics | §9.8 |

لكل قاعدة **أحد عشر حقلاً**: معرّف · متطلب معياري · نطاق · سلوك مطلوب · سلوك محظور · **شرط نجاح** · **شرط فشل** · أسطح ومكوّنات منطبِقة · دليل مطلوب · استثناء · إحالات. ويسبقها **§9.0** (الإطار: قابلية الفشل · حياد الأدوات · عدم الادّعاء الشامل · **نطاق مسارات الإنتاج الثلاثة** · قاعدة الاستثناء · قاعدة الدليل · **قواعد منع الخلط**)، و**§9.1** (البنود الستة القائمة محفوظة نافذة بشرطَي نجاح وفشل)، وتليها **§9.9** (جدول تلخيص) و**§9.10** (أثر التقنين على التجميد — تسجيلٌ لا رفع).

- **ما حُفظ ولم يُضعَّف:** البنود الستة القائمة في §9 (تباين AA · حلقة تركيز 2px · تنقّل لوحة مفاتيح كامل · إعلان الحالة والشارات نصاً · أهداف لمس ≥40px · لا معنى باللون وحده) **نُقلت إلى §9.1 بلا حذف ولا إضعاف**، **مع نصّ قاطع** أنها **لا تُستعمل بديلاً** عن السبعة: **حلقة التركيز ليست ترتيب التركيز**، **وإمكان التنقّل ليس صحة التسلسل**، **ومفتاح i18n ليس اسماً متاحاً**، **و`placeholder` ليس `label`**.
- completed: `ui/UI_DESIGN_SYSTEM.md` (‏v1.0 → **v1.1** — §9 وحدها أُعيدت صياغةً، وسطرُ الترويسة/الإصدار وحده تحديثاً تابعاً؛ **لا قسم آخر عُدِّل**) · `decisions/open-decisions.md` (‏v3.2 → **v3.3** — +**`OD-R3-CODIFY-1`** سجل التقنين + أثره على شروط الرفع **بلا تعديل ولا إعادة عدّ** + **إحدى عشرة فجوةً/مسألةً مسجَّلة لا مَحسومة**) · `INDEX.md` (**ثلاثة صفوف محدَّثة** — لا صفّ جديد) · هذا المدخل.
- not completed: **لم تُنفَّذ أي معالجة إتاحة** ولم يُعدَّل كود تطبيق ولا مكوّن UI · **لم يُبنَ ولم يُنفَّذ أيُّ اختبار** (`R3-A11Y-T-001`..`046` تبقى **`DESIGNED — NOT BUILT — NOT EXECUTED`**) · **لا معيار `PASS`** · **لم يُنشأ عقد حقلٍ** (`contracts/fields/` مؤجَّل) · **التجميد لم يُرفع** (`OD-FP-0001-FREEZE` = **`ACTIVE`**) · **`FP-0001` = `BLOCKED`** · **شروط الرفع لم تُعدَّل ولم يُعَد عدُّها ولم يُضَف إليها شرط** · **`R3` لم تُغلق ولم يُعَد تعريفها** · **`R4` لم تُفعَّل** · **`UI-4` و`UI-5` لم يُنشآ** · **Screen Contracts لم تُمسّ** (`run.list` · `admin.actions` · `admin.record_types` · `admin.workflows` · القالب) · **Rocket وVisual Baseline خارج النطاق ولم يُمسّا** · `GOV-OBS-03` و`P3-CI-28` و`OD-GOV-1` و`OD-GOV-2` و`OD-P3-2` **لم تُحسم** · **تعارض ميثاق `R3` لم يُحسم** · **تعارض الوضع الداكن لم يُحسم** · **`P3` لم تُعَد فتحاً** ولا PR #12 ولا PR #13 · **`Issue #11` لم يُمسّ** · **لا merge ولا tag ولا release**.
- files changed: **أربعة** — `ui/UI_DESIGN_SYSTEM.md` · `decisions/open-decisions.md` · `INDEX.md` · `handoff/handoff.md`. **ولم يُنشأ ملف جديد** ⇒ **لا صفّ جديد في `INDEX.md`** · الإجمالي **158 ملفاً + الفهرس** بلا تغيير · **EC-3 = 159/159 بلا تغيير**.
- decisions: **قرار مالك واحد جديد مسجَّل** = **`OD-R3-CODIFY-1`** (تقنين المعايير السبعة — `CODIFIED — EFFECTIVE UPON MERGE`). **لا ADR · لا قرار معماري · لا `OD` قائم أُعيد ترقيمه ولا تغيّرت حالته** · `AUTHORITY.md` و`constitution.md` و`methodology/**` و`contracts/**` و`traceability/**` و`superseded/**` و`decisions/adr/**` و`catalogs/**` و`phases/**` **لم تُمسّ** · **ولم تُنشأ طبقة سلطة جديدة**.
- risks: (1) **قراءة التقنين رفعاً للتجميد** — مُعالَج بـ§9.10 وبقسم (ب) من `OD-R3-CODIFY-1`: شرطٌ واحد تراكمي، **والرفع بقرار مالك صريح بعد استيفاء الشروط كاملةً**. (2) **قراءة التقنين إعلانَ `PASS`** — مُعالَج بنصّ صريح في §9.10-1: **إنشاء قاعدةٍ قابلة للقياس لا نتيجةُ قياس**. (3) **قراءة النفاذ قبل الدمج** — مُعالَج بقاعدة **`EFFECTIVE UPON MERGE`**: §9 **لا تنفذ** حتى الدمج في `main`. (4) **قراءة `traceability/**` مصدراً حاكماً** — مُعالَج بقاعدة القراءة أعلاه وبنصّ §9.0 و`OD-R3-CODIFY-1`: **الملفّان `Non-Governing` ولم يُمسّا ولم تُرفع سلطتهما**. (5) **قراءة فجوات §(د) شروطَ رفعٍ جديدة** — مُعالَج بتنبيه ملزم: **تسجيلُ فجوةٍ ليس إضافةَ شرط**. (6) **قراءة §9.1 بديلاً عن السبعة** — مُعالَج بقاعدة قاطعة في §9.1 وبقواعد منع الخلط في §9.0. (7) **بقاء `traceability/r3-accessibility/**` على الحالة `NOT CODIFIED`** — **مقصود ومُفصَح عنه**: تصحيح وثيقةٍ غير حاكمة **خارج نطاق هذه الجولة** ويحتاج أمراً مستقلاً؛ **والحالة النافذة حاكمياً** مسجَّلة في `OD-R3-CODIFY-1`. (8) **توتّر وسم حالة `R3`** — `R3-ACT-01` يسجّلها `ACTIVE — SPECIFICATION ONLY` وقد أُذن لاحقاً بالتقنين بأمر مالك مستقل: **مُسجَّل ولم يُحسم**، **ولم يُعدَّل السجل السابق**، وإعادةُ الوسم **قرار مالك مستقل** (`OD-R3-CODIFY-1` §(د) البند 11). (9) **قراءة §9.1 القائمة قيداً مطلقاً** على العناصر المعطَّلة — مُعالَج بقاعدتَي التخصيص وعدم تكرار العدّ في §9.0 (7) و(8).
- tests: (‏التفصيل في وصف الـPR وتقرير الجولة) — `origin/main` = **`765c4504a8e813e031ae0c9fb8b5eaad95f85da2`** (مطابق للأساس المعلَن) · **PR #13 = `MERGED`** · **أربعة ملفات معدَّلة فقط** · **commit واحد بأبٍ واحد أبوه `765c4504…`** و`git rev-list --merges origin/main..HEAD` = **0** (‏**يُثبَّتان بعد الدفع** — وSHA الـcommit في وصف الـPR) · `git diff --check` **نظيف** · **المعرّفات السبعة `R3-A11Y-01`..`07` موجودة في §9 · بلا تكرار تعريفي · بلا فجوات** · **لكل قاعدة `شرط النجاح` و`شرط الفشل`** · **صفر معيار `PASS`** · **صفر عبارة عامة غير قابلة للفشل بوصفها بوابة** · **البنود الستة القائمة محفوظة** · **صفر ذكر لأداة بعينها** (‏لا Playwright ولا Axe ولا Lighthouse ولا خدمة خارجية) · **صفر تعديل** على `traceability/**` و`contracts/**` و`methodology/**` و`phases/**` و`catalogs/**` و`superseded/**` و`decisions/adr/**` و`AUTHORITY.md` و`constitution.md` وبقية `ui/**` · جرد `P3` **`28 = 13 + 15 + 0`** · **`UNCLASSIFIED = 0`** · `FP-0001` = **`BLOCKED`** · التجميد **`ACTIVE`** · **`R4` غير مفعَّلة** · **عدد الوسوم = 16** · **لا وسم ولا إصدار** · `INDEX.md` **مطابق للشجرة** (‏158 صفاً + الفهرس · صفر ملف خارج الفهرس · صفر صفّ بلا ملف) · **صفر `placeholder` غير محلول**.
- next step: **قرار مالك في الـPR** (‏دمج أو رفض) — **والنفاذ يبدأ عند الدمج فقط**. وبعده وبأوامر مستقلة: **تصحيح `traceability/r3-accessibility/**`** لتعكس وقوع التقنين ⇒ **إدراج §9 المقنَّنة في Reading Sets** ⇒ **أمر إنشاء عقد الحقل** (المرتبة 5) ⇒ **بند إتاحة في `ui/UI_GATE_REVIEW_CHECKLIST.md`** ونوع اختبار إتاحة في `methodology/testing-strategy.md` وحدٌّ أدنى في §8 من قالب عقد الشاشة ⇒ **بناء الاختبارات وتنفيذها** ⇒ **المعالجة** ⇒ فحوص بوابة `FP-0001` ⇒ **رفع التجميد بقرار مالك**. **وهذا ترتيبٌ تشغيليّ مقترَح لا قائمةُ شروطٍ للرفع**: شروط رفع `OD-FP-0001-FREEZE` **مغلقة على المنصوص عليه** في سجل التجميد وتفصيلِه في `R3-ACT-01`، **وما ورد هنا من فجوات إنفاذٍ ليس شرطاً مضافاً** (`OD-R3-CODIFY-1` §(د)). **وتبقى تسوية اسم `R3` ونطاقه وحسمُ تعارض الوضع الداكن قرارَين مالكيَّين مستقلَّين.** **ولا شيء من ذلك مأذون به في هذه الجولة.**
- do not touch: constitution.md · AUTHORITY.md · methodology/** · phases/** · contracts/** · **`traceability/**` بكاملها** (بما فيها `r3-accessibility/**` و`rar-reconciliation/**` و`P3-CLOSURE-INVENTORY.md`) · superseded/** · **الآثار التاريخية المجمَّدة** · decisions/adr/** · catalogs/** · **بقية `ui/**` عدا `UI_DESIGN_SYSTEM.md`** · **ملفات UI-4 وUI-5** · **Rocket files** · **Visual Baseline files** · **‏GitHub Issue #11** · أي ملف في `aql` · **أي وسم أو إصدار** · **أي سجل تفعيل `R4`** · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.4 · **H-0016..H-0030**.

## Handoff H-0032
> **‏R3 — PR #14 Pre-Merge Reconciliation.** يُقرأ بعد `H-0031` **ولا يعيد كتابته ولا يحذفه**: `H-0031` صحيحٌ في تاريخه وقد قنّن §9؛ **وهذه الجولة تُغلق ملاحظات المراجعة السابقة للدمج على الفرع نفسه — لا غير.** **ليست جولة تقنين جديدة، ولا `UI-4` ولا `UI-5`، ولا إعادة تصميم لـ§9.** **ولا تغيير في `FP-0001` ولا في التجميد ولا في جرد `P3` ولا في أي مخرج مجمَّد.**
- date: 2026-08-03
- phase: **R3 — PR #14 Pre-Merge Reconciliation** — **الفرع نفسه** `docs/r3-accessibility-section-9-codification` · **PR #14 نفسه — غير مدموج · لم يُنشأ فرع ولا PR جديد**
- task/goal: تنفيذ **ستة تصحيحات** (`C1`..`C6`) بأمر مالك، **بلا توسيع نطاق**. **لا تقنين جديد · لا قاعدة أُضيفت أو حُذفت · لا شرط نجاح أو فشل عُدِّل · لا معالجة · لا بناء اختبارات · لا معيار `PASS` · لا merge ولا tag ولا release ولا rebase ولا amend ولا force-push · لا رفع تجميد ولا فكّ حجب `FP-0001` ولا تفعيل `R4` ولا `ADR` ولا `OD` جديد.**
- base SHA: **`origin/main` = `765c4504a8e813e031ae0c9fb8b5eaad95f85da2`** (بلا تغيير — أُعيد التحقق) · **أساس هذه الدفعة:** `c26a01ce04f38528dc0e91cfb7fbe20130a69a93` (‏commit `H-0031`) · **PR #14 = `OPEN`** غير مدموج، رأسه مطابق قبل التصحيح · **عدد الوسوم = 16**.
- **خطية الفرع:** **commitان اثنان فقط فوق `main`** · كلٌّ **بأبٍ واحد** · **صفر merge commit** · بلا rebase ولا amend ولا force-push.

**‏Owner Correction Order — 2026-08-03 (تسجيل إلزامي):** «‏OWNER CORRECTION ORDER — PR #14 Pre-Merge Reconciliation». **وهو نفسه قرارُ المالك المطلوب لتوثيق الاستثناء التنفيذي المحدود** ⇒ **لا يلزم `Decision Request` جديد**. **ومحصورٌ في الملفات الأربعة القائمة في PR #14** + تحديث وصف الـPR.

**التصحيحات الستة:**

| # | التصحيح | ما تغيّر | الموضع |
|---|---|---|---|
| **C1** | **إغلاق توتّر `R3-ACT-01`** | التوتّر **لم يعد مسألةً معلَّقة**: `R3-ACT-01` **صحيحٌ عند صدوره** · وأمرُ تقنين §9 **استثناءٌ تنفيذي محدود ومؤرَّخ** · نطاقه **§9 وملفات PR #14 وحدها** · **`R3-ACT-01` لا يُوسَم `Superseded`** وبقية قيوده **نافذة** · والعبارات المانعة لتعديل `ui/UI_DESIGN_SYSTEM.md` تصير **`HISTORICAL / STALE EVIDENCE` عند الدمج ولهذه الجولة وحدها**. **وحُذفت المسألة من قائمة الفجوات** | `OD-R3-CODIFY-1` §(هـ) + صفّ `R3` |
| **C2** | **تصحيح الادّعاء السلطوي** | **حالة `ui/UI_DESIGN_SYSTEM.md` تبقى `Proposed` ولم تُرقَّ**. وأُبدلت كلُّ صيغةٍ توحي بأن الدمج يجعل المرتبة 8 حاكمةً للقواعد السبع بصيغةٍ دقيقة: **الدمج ينشر §9 مرجعاً منشوراً ضمن حالة `Proposed`، والترقيةُ قرارُ مالك مستقل** | §9.0 · §9.10-5 · ترويسة الملف · `OD-R3-CODIFY-1` · `INDEX.md` · وصف الـPR |
| **C3** | **تصحيح وصف المراجعة** | «‏Independent adversarial review» ⇒ **`Structured self-review using a separate review agent`** — **مراجعة ذاتية منظمة بوكيل مراجعة منفصل داخل الجلسة نفسها**: التقطت **عيوباً حقيقية**، **لكنها ليست مراجعة مستقلة خارجية ولا تحلّ محلّ مراجعة المالك** | وصف الـPR + هذا المدخل |
| **C4** | **تسجيل واقعة `replace_all`** | سُجِّلت بوصفها **دليلاً على فجوة الحماية القائمة**: التسرّب **وقع** · **كُشف قبل الـcommit** · **أُعيدت §4 مطابقةً لـ`origin/main`** · **الضمانة الحالية بشرية لا آلية** · والمعالجة الآلية **ضمن مسارها المخطط** (`G2` · حماية الفروع · `CODEOWNERS` · `CI`) **خارج هذه الجولة**. **ولا شرط رفعٍ ولا شرط سابق للدمج ولا أمر `CI` ولا توسّع إلى `G2`** | `OD-R3-CODIFY-1` §(و) + الفجوة 11 |
| **C5** | **فحوص قابلة لإعادة الإنتاج** | نُشر في وصف الـPR قسم **`Reproducible Verification Commands`** بالأوامر الحرفية ومخرجاتها المختصرة (‏baseline · الملفات المعدَّلة · حصر التعديل في §9 والترويسة · عدّ المعرّفات · Pass/Fail · `git diff --check` · التجميد · المسارات المحظورة · حالة العقود). **ولم يُنشأ script ولا CI** | وصف الـPR |
| **C6** | **تسجيل تبعية العقود** | **§9 قُنِّن بنجاح**، وتطبيقُ بعض قواعده على العقود القائمة **سيُظهر failures** لأن: العقود الأربعة **لا تستخدم `surfaces[]`** · `contracts/fields/` **غير موجود** · **لا إعلان تعاقدي كافٍ للترتيب المتوقَّع** · `accessible_name_source` **ليس على حبيبة العنصر**. **وهذه تبعياتُ المعالجة التالية لا أسبابٌ لرفض التقنين** · **ولا يُعلَن `PASS` قبل حلّها وبناء الاختبارات وتنفيذها** · **ولا تُوصف بحلقةٍ مستحيلة ولا بشرط رفعٍ جديد** | وصف الـPR + تقرير الجولة (‏والفجوات 1 و4 و8 و9 قائمة) |

- **حالة العقود عند هذا الأساس (مثبَتة لا مفترَضة):** **أربعة عقود** (`admin.actions` · `admin.record_types` · `admin.workflows` · `run.list`) · **صفرٌ منها يحتوي `surfaces[]`** (الورود الوحيد في **القالب** `SCREEN_CONTRACT_TEMPLATE.md`) · **`contracts/fields/` غير موجود**. **ولم يُعدَّل أيُّ ملف في `contracts/**`.**
- completed: `decisions/open-decisions.md` (‏v3.3 → **v3.4** — +§(هـ) حكم الاستثناء المحدود · +§(و) واقعة `replace_all` · تصحيح الصياغة السلطوية · حذف مسألة وسم `R3` من الفجوات وإحلال فجوة الحماية محلّها) · `ui/UI_DESIGN_SYSTEM.md` (‏تدقيق الصياغة السلطوية في §9.0 و§9.10 والترويسة والعنوانين — **بلا مساس بأي قاعدة ولا شرط نجاح أو فشل**) · `INDEX.md` (**ثلاثة صفوف محدَّثة** — لا صفّ جديد) · هذا المدخل.
- not completed: **لا تقنين جديد ولا إعادة تصميم لـ§9** · **`contracts/**` لم تُمسّ** · **`methodology/**` و`AUTHORITY.md` و`traceability/**` لم تُمسّ** · **`R3-ACT-01` لم يُعدَّل** ولم يُعَد كتابةُ تاريخه · **لم تُنفَّذ معالجة** ولم يُبنَ اختبار · **لا معيار `PASS`** · **التجميد `ACTIVE`** · **`FP-0001` `BLOCKED`** · **`R4` غير مفعَّلة** · **`UI-4` و`UI-5` لم يُنشآ** · **حالة `ui/UI_DESIGN_SYSTEM.md` لم تُرقَّ** · **الفجوات 1–10 قائمة** · **تعارض ميثاق `R3` وتعارض الوضع الداكن لم يُحسما** · **PR #14 لم يُدمج**.
- files changed: **ثلاثة في هذه الدفعة** — `decisions/open-decisions.md` · `ui/UI_DESIGN_SYSTEM.md` · `INDEX.md` — **+ `handoff/handoff.md` (هذا المدخل)** ⇒ **الأربعة نفسها عبر PR #14 كله**. **ولم يُنشأ ملف جديد** ⇒ **لا صفّ جديد في `INDEX.md`** · **EC-3 = 159/159 بلا تغيير**.
- decisions: **لا `OD` جديد ولا `ADR`** — عُدِّل **`OD-R3-CODIFY-1` وحده** بموجب أمر المالك. **ولم تُنشأ طبقة سلطة جديدة**، ولم يتغيّر تصنيف أي ملف، **ولم تُرقَّ حالة أي ملف**.
- risks: (1) **قراءة الاستثناء إلغاءً لـ`R3-ACT-01`** — مُعالَج بالبند 4 من §(هـ): **لا يُوسَم `Superseded`** وبقية قيوده نافذة. (2) **قراءة الدمج ترقيةً لحالة الملف** — مُعالَج بـ§9.0 «قيد سلطوي دقيق» و§9.10-5 وصفّ `INDEX`. (3) **قراءة واقعة `replace_all` أمرَ إنشاء `CI`** — مُعالَج بنصّ §(و): **لا أمر ولا شرط**، والمسار المخطط خارج الجولة. (4) **قراءة تبعية العقود رفضاً للتقنين أو حلقةً مستحيلة** — مُعالَج بـ`C6`: **تبعياتُ معالجةٍ تالية** لا أسباب رفض. (5) **قراءة المراجعة الذاتية مراجعةً مستقلة** — مُعالَج بـ`C3`: **لا تحلّ محلّ مراجعة المالك ولا مراجعٍ مستقل خارجي**.
- tests: (‏الأوامر الحرفية ومخرجاتها في وصف الـPR — قسم `Reproducible Verification Commands`) — `origin/main` = **`765c4504…`** (لم يتحرك) · **PR #14 `OPEN`** ورأسه قبل التصحيح **`c26a01ce…`** (مطابق) · **أربعة ملفات عبر الـPR كله** · **commitان بأبٍ واحد لكلٍّ** · `git rev-list --merges origin/main..HEAD` = **0** · `git diff --check` **نظيف** · **`R3-A11Y-01`..`07` سبعة بلا تكرار تعريفي** · **Pass/Fail لكل قاعدة (7/7)** · **صفر معيار `PASS`** · **سجل التجميد وشروطه السبعة byte-identical** · **`contracts/**` و`methodology/**` و`traceability/**` و`AUTHORITY.md` و`constitution.md` و`phases/**` و`catalogs/**` و`superseded/**` و`decisions/adr/**` وبقية `ui/**` byte-identical** · **العقود = 4 · صفرٌ منها بـ`surfaces[]` · `contracts/fields/` غير موجود** · **EC-3 = 159/159** · جرد `P3` **`28 = 13 + 15 + 0`** · **16 وسماً** · **لا وسم ولا إصدار**.
- next step: **قرار مالك في PR #14** (‏دمج أو رفض) — **والنفاذ يبدأ عند الدمج فقط، والدمج لا يرقّي حالة الملف**. وبعده وبأوامر مستقلة: تصحيح `traceability/r3-accessibility/**` · إدراج §9 في Reading Sets · **قرار ترقية حالة `ui/UI_DESIGN_SYSTEM.md`** · **أمر إنشاء عقد الحقل** و`surfaces[]` في العقود الأربعة · بند إتاحة في `ui/UI_GATE_REVIEW_CHECKLIST.md` ونوع اختبار في `methodology/testing-strategy.md` وحدٌّ أدنى في §8 من قالب العقد · بناء الاختبارات وتنفيذها · المعالجة · فحوص بوابة `FP-0001` · **رفع التجميد بقرار مالك**. **وهذا ترتيبٌ تشغيليّ لا قائمةُ شروطِ رفعٍ** — الشروط مغلقة على المنصوص عليه. **ولا شيء من ذلك مأذون به في هذه الجولة.**
- do not touch: constitution.md · AUTHORITY.md · methodology/** · phases/** · **contracts/**** · **traceability/** بكاملها** · superseded/** · **الآثار التاريخية المجمَّدة** · decisions/adr/** · catalogs/** · **بقية `ui/**` عدا `UI_DESIGN_SYSTEM.md`** · **ملفات UI-4 وUI-5** · **Rocket files** · **Visual Baseline files** · **‏GitHub Issue #11** · أي ملف في `aql` · **أي وسم أو إصدار** · **أي سجل تفعيل `R4`** · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.4 · **H-0016..H-0031** · **و`R3-ACT-01` — لا يُعاد كتابة تاريخه؛ حكمُ الأمر اللاحق مسجَّل في `OD-R3-CODIFY-1` §(هـ)**.

## Handoff H-0033
> **‏GOV — Agent-Authorized Merge Governance Amendment.** جولةُ **حوكمةٍ مستقلة** على **فرع جديد من `origin/main` مباشرةً** — **لا علاقة لها بـPR #14 ولا تمسّه ولا تدمجه.** **ليست جولة `R3` ولا إتاحة ولا تقنين §9.** **يُقرأ بعد `H-0030` ولا يعيد كتابته ولا يحذفه.**
> **فجوة ترقيم مقصودة ومُفصَح عنها:** **`H-0031` و`H-0032` محجوزان لـPR #14** (غير مدموج عند تحرير هذا المدخل) — فاستُعمل **`H-0033`** **منعاً للتصادم**، لا سهواً. **ولا يُعاد ترقيمه لاحقاً.**
- date: 2026-08-03
- phase: **GOV — Merge Governance Amendment** — فرع `docs/gov-owner-authorized-merge-agent` من `origin/main` مباشرةً · **PR مستقل غير مدموج**
- task/goal: تنفيذ **أمر المالك** «‏OWNER ORDER — Agent-Authorized Merge Governance Amendment»: استبدال قاعدة «الدمج البشري بواسطة SA حصراً» بنموذج **Owner-Authorized Independent Merge Agent**، بفصلٍ صريح بين **قرار الدمج** و**تنفيذه** و**هوية المنفِّذ** و**هوية المراجع** و**بيانات الاعتماد التقنية** — **مع تشديد فصل الأدوار لا تخفيفه**. **لا معالجة · لا اختبارات · لا عقود · لا `ui/**` · لا merge ولا tag ولا release ولا rebase ولا amend ولا force-push · لا رفع تجميد ولا فكّ حجب `FP-0001` ولا تفعيل `R4` ولا مساس بـPR #14.**
- base SHA: **`origin/main` = `765c4504a8e813e031ae0c9fb8b5eaad95f85da2`** · **عدد الوسوم = 16** · **PR #14 = `OPEN`** ورأسه **`52d88d0ea9b642f5b04def30a416f0a595bdaa10`** (‏**تُحقِّق منه ولم يُمسّ**).
- **خطية الفرع:** أُنشئ من `origin/main` مباشرةً · **commit واحد بأبٍ واحد أبوه `765c4504…`** · **صفر merge commit** · بلا rebase ولا amend ولا force-push.

**‏Owner Order — 2026-08-03 (تسجيل إلزامي):** «‏OWNER ORDER — Agent-Authorized Merge Governance Amendment». **وهو نفسه سندُ الاستثناء الانتقالي** ⇒ **لا يلزم `Decision Request` جديد** ولا `ADR` جديد.

**ما تغيّر — القاعدة القديمة ⇐ الجديدة:**

| # | القديم (`SUPERSEDED — 2026-08-03`) | الجديد (`EFFECTIVE UPON MERGE`) |
|---|---|---|
| **1** | ‏ADR-0033-1 «‏L1 … **والدمج بشري (SA)**» | المنفِّذ **لا يدمج عمله**؛ والتنفيذ بشري **أو** بـMerge Agent مفوَّض |
| **2** | ‏ADR-0033-3 «المسارات المحمية — **دمج بشري دائماً في L≤2**» | **لا auto-merge غير مشروط أبداً** · ‏Human Manual Merge **أو** Owner-Authorized Agent Merge بشروط بند 10 |
| **3** | `agent-execution-model` §2-7 «الدمج/الرفع **بيد SA حصراً**» | **قرار** الدمج للمالك · **تنفيذه** وفق §18 |
| **4** | `agent-execution-model` §8 «الدمج والوسوم **بيد SA في كل مستوى دون L3**» | الدمج كما أعلاه · **والوسوم والإصدارات لم تُمسّ** |
| **5** | `agent-execution-model` §14 «‏L1 … **والدمج بشري**» | المستوى يحكم **الأتمتة غير المشروطة** لا **هوية المنفِّذ** |
| **6** | ‏ADR-0033-7 فصل الأدوار | **`RETAINED + EXTENDED`** — **نافذ ومُشدَّد**، لم يُضعَّف |

**النصوص القديمة محفوظة حرفياً** في جدول «النصوص المستبدَلة» داخل ADR-0033 — **ولم يُحذف قرار ولا سجل سابق**، ولم يُعدَّل أيُّ مدخل `handoff` سابق.

- completed: `decisions/adr/ADR-0033-automation-levels-git-merge-policy.md` (‏**`Accepted` ⇒ `Accepted (Amended)`** — دلتا البنود 1 و3 و7 + **البنود الجديدة 8–14** + جدول النصوص المستبدَلة + **الاستثناء الانتقالي** + تحديث Context/Alternatives/Rationale/Consequences/Migration/Status/Related) · `methodology/agent-execution-model.md` (‏**v2.0 ⇒ v2.1** — **+§18 فصل أدوار دورة الدمج** بأربعة أدوار وسبع قواعد قاطعة + دلتا §2-7 و§8 و§12 و§14) · `decisions/open-decisions.md` (‏v3.2 ⇒ **v3.3-GOV** — +**`OD-GOV-MERGE-1`** بتسعة أقسام: القرار · المقابلة النصية · جدول الأدوار · الشروط السبعة · **الاستثناء الانتقالي** · قيود عدم الفعل · أثر `L1`/`L2` · تسجيل PR #14 · **أوعية فُحصت ولم تُعدَّل**) · `decisions/adr/README.md` (‏v1.6 ⇒ **v1.7** — صفّ ADR-0033 وحده) · `INDEX.md` (**خمسة صفوف محدَّثة** — لا صفّ جديد) · هذا المدخل.
- not completed: **`PR #14` لم يُمسّ ولم يُدمج ولم يُعدَّل** · **`ui/**` لم تُمسّ** (ومنها `UI_DESIGN_SYSTEM.md` §9) · **`contracts/**` لم تُمسّ** · **`AUTHORITY.md` و`constitution.md` و`traceability/**` و`phases/**` و`catalogs/**` و`superseded/**` لم تُمسّ** · **بقية `decisions/adr/**` لم تُمسّ** · **لا ADR جديد** · **لا معالجة ولا اختبارات ولا معيار `PASS`** · **التجميد `ACTIVE`** · **`FP-0001` `BLOCKED`** · **شروط الرفع بلا تعديل ولا إعادة عدّ** · **`R3` لم تُغلق** · **`R4` غير مفعَّلة** · **`UI-4` و`UI-5` لم يُنشآ** · **لا وسم ولا إصدار (16 وسماً)** · **لا `CI` ولا حماية فروع ولا `CODEOWNERS`** · **تعارض ميثاق `R3` وتعارض الوضع الداكن لم يُحسما**.
- files changed: **ستة** — `decisions/adr/ADR-0033-automation-levels-git-merge-policy.md` · `decisions/adr/README.md` · `methodology/agent-execution-model.md` · `decisions/open-decisions.md` · `INDEX.md` · `handoff/handoff.md`. **ولم يُنشأ ملف جديد** ⇒ **لا صفّ جديد في `INDEX.md`** · الإجمالي **158 + الفهرس** بلا تغيير · **EC-3 = 159/159 بلا تغيير**.
- decisions: **قرار مالك واحد جديد مسجَّل** = **`OD-GOV-MERGE-1`** (`AMENDED — EFFECTIVE UPON MERGE`) + **تعديل ADR-0033 في موضعه** بنمط سابقة **ADR-0029** (`Accepted (Amended)`) — **لا ADR جديد · لا وسم `Superseded` على ADR-0033 · لا طبقة سلطة جديدة · لا `OD` قائم أُعيد ترقيمه أو غُيّرت حالته**.
- risks: (1) **قراءة التعديل إذناً عاماً بالأتمتة** — مُعالَج بجدول أنماط الدمج الثلاثة: **Owner-Authorized Agent Merge ≠ Autonomous Merge**، والأخير **ممنوع** على المسارات الحساسة. (2) **قراءته تخفيفاً لفصل الأدوار** — مُعالَج ببند 7 `RETAINED + EXTENDED` و§18.2 القواعد السبع. (3) **قراءته ترقيةً إلى `L2`** — مُعالَج بـ§(ز): **لا يستهلك شرط الانتقال ولا يعجّله**، و`L2` لم يُبلَغ. (4) **قراءة الحساب التقني دليلَ تنفيذٍ يدويٍّ من المالك** — مُعالَج ببندي 9 و12 و§18.2-5. (5) **منح وكيلٍ الموافقةَ لنفسه** — مُعالَج ببند 13 (صلاحيات مغلقة) و§(د)-2. (6) **قراءة الاستثناء الانتقالي سابقةً عامة** — مُعالَج بحدوده الستة: **ينتهي فور دمج أو رفض هذا الـPR** ولا يطبَّق على PR #14. (7) **قراءة النفاذ قبل الدمج** — مُعالَج بـ`EFFECTIVE UPON MERGE` في ثلاثة مواضع. (8) **تفاعل تسلسلي مع PR #14** — **مُثبَت بالفحص ومرفوع للمالك** في `OD-GOV-MERGE-1` §(ح)-3: ‏`git merge-tree --write-tree` يُرجع **ثلاثة تعارضات محتوى** (`INDEX.md` · `decisions/open-decisions.md` · `handoff/handoff.md`)؛ فدمجُ أيٍّ من الـPRين يجعل الآخر غير قابل للدمج آلياً، وحلُّ التعارض **يغيّر رأس الآخر فيُبطل الـSHA المثبَّت** ⇒ **يحتاج أمر مالك جديداً أو تحديثاً صريحاً للتفويض**. **ولم يُحسم بافتراض.** (9) **مراجعة PR #14 الحالية ليست مستقلة** (‏`Structured self-review` بنصّ الـPR نفسه) ⇒ **شرط §(د)-3 غير مستوفٍ له** — **مسجَّل حالةً لا شرطَ رفعٍ جديداً**.
- tests: (‏الأوامر ومخرجاتها في وصف الـPR) — `origin/main` = **`765c4504…`** (مطابق للأساس) · **PR #14 `OPEN` ورأسه `52d88d0e…` بلا تغيير ولم يُمسّ** · **ستة ملفات معدَّلة فقط** · **commit واحد بأبٍ واحد** و`git rev-list --merges origin/main..HEAD` = **0** · `git diff --check` **نظيف** · **`ui/**` و`contracts/**` و`traceability/**` و`phases/**` و`catalogs/**` و`superseded/**` و`AUTHORITY.md` و`constitution.md` وبقية `decisions/adr/**` byte-identical مع `origin/main`** · **سجل `OD-FP-0001-FREEZE` وشروطه byte-identical** · **`R3-ACT-01` byte-identical** · **صفر ADR جديد** · **صفر ملف جديد** · **EC-3 = 159/159** · جرد `P3` **`28 = 13 + 15 + 0`** · **16 وسماً · لا وسم ولا إصدار**.
- next step: **قرار مالك في هذا الـPR** (‏دمج أو رفض) — **والنفاذ يبدأ عند الدمج فقط**. ودمجُه جائزٌ بـ**الاستثناء الانتقالي** بيد **وكيل دمج مستقل لم يكتب هذا الـPR ولم يدفع إلى فرعه**، بعد **مراجعة مستقلة** و**بوابات** و**تثبيت Head SHA**. **[Δ تصحيح 2026-08-03]:** جرت مراجعة مستقلة على `8b741729…` بحكم **`REQUEST CHANGES`**، ونُفِّذت تصحيحاتها في **commit جديد ⇒ الرأس تغيّر** ⇒ **يلزم أمرُ مالكٍ جديد يثبّت الرأس النهائي ومراجعةٌ مستقلة جديدة قبل أي دمج** (‏ADR-0033 بند 11)؛ **والرأس القديم لم يُعتمد للدمج**. وبعده وبأمر مالك مستقل: **جلسة Merge Agent مستقلة لـPR #14** تتحقق من بقاء الرأس `52d88d0e…` ومن **مراجعة مستقلة** (‏**غير مستوفاة حتى تاريخه**) ومن الفحوص الاثني عشر، **ثم تُحسم مسألة التعارض التسلسلي بقرار مالك**. **ولا شيء من ذلك مأذون به في هذه الجولة.**
- do not touch: **‏PR #14 وفرعه `docs/r3-accessibility-section-9-codification`** · constitution.md · AUTHORITY.md · **`ui/**` بكاملها** · **`contracts/**`** · **`traceability/**` بكاملها** · phases/** · catalogs/** · superseded/** · **بقية `decisions/adr/**` عدا ADR-0033 و`README.md`** · **بقية `methodology/**` عدا `agent-execution-model.md`** · **الآثار التاريخية المجمَّدة** · **ملفات UI-4 وUI-5** · **Rocket files** · **Visual Baseline files** · **‏GitHub Issue #11** · أي ملف في `aql` · **أي وسم أو إصدار** · **أي سجل تفعيل `R4`** · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.4 · **H-0016..H-0030** · **و`R3-ACT-01` — لا يُعاد كتابة تاريخه**.

**‏Δ 2026-08-03 — جولة تصحيح بعد مراجعة مستقلة (‏ضمن `H-0033` — لا مدخل جديد):**
> **السند:** «‏OWNER CORRECTION ORDER — PR #15 Independent Review Findings» (2026-08-03). **نفس الفرع ونفس الـPR** · **commit جديد فوق الرأس** · **بلا `amend` ولا `rebase` ولا `force-push`** · **بلا فرع أو PR جديد** · **بلا دمج**.

| ‏ID | الملاحظة الحاجبة | التصحيح |
|---|---|---|
| **`C1`** | عدد شروط الدمج متناقض: بند 10 = **ستة** · §(د) = **سبعة** · `adr/README.md` ينسب «السبعة» إلى ADR-0033 | اعتُمد **سبعة مجتمعة (AND)**: أُضيف **`(ز)` تسجيل أثر الدمج بالأبعاد الأربعة** إلى بند 10، وبقي **بند 12** تفصيلاً للمحتوى والتنفيذ · ووُحِّد العدّ في **ستة أوعية + وصف الـPR** |
| **`C2`** | نسبة عبارة «كل قرار حاكم» إلى النص السابق وهي **غير موجودة فيه**، ووصف إضافة `methodology/**` بأنها «تثبيت لا توسيع» | حُذف الادّعاء · `methodology/**` **إضافةٌ وتوسيعٌ مقصود** بأمر المالك · ونُصَّ أن السابق «**وكل قرار تجاري**» · وحُفظ النص السابق **حرفياً كاملاً** في جدول النصوص المستبدَلة |
| **`C3`** | الاستثناء الانتقالي **لا يسمّي PR #15** ولا يَرِد رأسه في أي وعاء | ثُبِّت حرفياً: `sa4devops/local-rag-enterprise-specs` · **`PR #15`** · **`8b741729…`** · `main` · +**قاعدة الرأس النهائي** · +عدم الانطباق على **PR #14** و**أي PR لاحق يعدّل السياسة** و**أي وكيل كتب/عدّل PR #15** · +**ثلاثة محفزات انقضاء** |
| **`N1`** | قوائم المسارات الحساسة غير متطابقة · `handoff/**` في وعاء واحد | **ADR-0033 بند 3 = القائمة الكنسية الوحيدة**؛ وغيرُها **إحالة لا تعريف** · و`handoff/**` **حماية إضافية في سياق PR #14 وحده** لا جزءٌ من القائمة العامة · **ولم تُوسَّع القائمة** |

**أثر سلطوي مسجَّل:** وكيلُ المراجعة الذي نفّذ التصحيح **صار كاتبَ محتوى** (‏§18.1 صفّ Review Agent · §18.2-1) ⇒ **فقَدَ أهليةَ مراجعة هذه الدفعة ولا يدمجها**. **المطلوب قبل أي دمج: مراجعة مستقلة جديدة + أمر مالك جديد يثبّت الرأس النهائي.**

**بلا تغيير:** التجميد **`ACTIVE`** · `FP-0001` **`BLOCKED`** · شروط الرفع **بلا تعديل ولا إعادة عدّ** · `R3` لم تُغلق · **`R4` غير مفعَّلة** · جرد `P3` **`28 = 13 + 15 + 0`** · **16 وسماً** · **PR #14 لم يُمسّ** ورأسه **`52d88d0e…`** · **ستة ملفات فقط** · **لا ملف جديد ولا محذوف**.

## Handoff H-0034
> **‏GOV — PR #14 Merge Execution Provenance (‏Post-Merge Audit Record).** جولةُ **توثيقٍ بعد الدمج فقط** على **فرع جديد من `origin/main` مباشرةً**. **ليست** جولة `R3` ولا إتاحة ولا تعديل §9 ولا `UI-4`/`UI-5` ولا عقود ولا تعديل سياسة دمج ولا رفع تجميد ولا مراجعة/إعادة فتح لـPR #14. **يُقرأ بعد `H-0033` ولا يعيد كتابته ولا يحذفه.**
> **‏`H-0031` و`H-0032` و`H-0033` لم تُمسّ ولم تُعدَّل** — وهذا المدخل **الرقم التسلسلي التالي الفعلي** بعد تحقُّقٍ من السجل لا بافتراض.
- date: 2026-08-03
- phase: **GOV — Merge Audit Record** — فرع `docs/pr14-merge-audit-record` من `origin/main` مباشرةً · **PR مستقل غير مدموج**
- task/goal: استكمال **أثر دمج PR #14** الواجب بموجب **`ADR-0033` بند 12** ونموذج **Owner-Authorized Independent Merge Agent**: تسجيل **الأبعاد الأربعة** و`Merge SHA` وخط الأساس الجديد وهوية المراجعة المستقلة ونطاقها، **والنصّ صراحةً على أن الحساب التقني ليس دليلَ تنفيذٍ يدويٍّ من المالك**. **توثيق فقط — لا سياسة جديدة ولا ADR جديد ولا OD جديد.**
- base SHA: **`origin/main` = `d2c93d2c16b03d406a6b6fe70c0b0771687c9ff5`** · **عدد الوسوم = 16** · **PR #14 = `MERGED`**.

**‏Owner Order — 2026-08-03 (تسجيل إلزامي):** «‏OWNER MERGE ORDER — PR #14» (أمر الدمج) · ثم «‏OWNER ORDER — Complete PR #14 Merge Audit Record» (أمر هذا التوثيق).

**واقعة الدمج — تسجيل حرفي:**

```text
PR = #14  ("R3 — Codify Accessibility Requirements in UI Design System §9")
Authorization Principal = Owner
Execution Actor = Owner-Authorized Independent Merge Agent
Technical Credential = GitHub token for account sa4devops used by the agent environment
Review Actor = Independent Engineering Review Session
Review Date = 2026-08-03
Reviewed Head SHA = 0020dfb6de7f383b3468518691a7b29da0cf7f1e
Review Result = APPROVE / NO BLOCKING FINDINGS
Review Artifact Identifier = Not persisted outside the review conversation
Authorized Head SHA = 0020dfb6de7f383b3468518691a7b29da0cf7f1e
Base SHA Before Merge = 0c199d76f732357ac948fe6c6e50171e9250a04c
Merge SHA = d2c93d2c16b03d406a6b6fe70c0b0771687c9ff5
New Governing Baseline = origin/main @ d2c93d2c16b03d406a6b6fe70c0b0771687c9ff5
Merge Method = merge commit
Merge Result = SUCCESS
```

**نصٌّ قاطع — الحساب التقني:** الدمج **نُفِّذ بواسطة Merge Agent مفوَّض**، **لا يدوياً بواسطة المالك**. و**ظهور `sa4devops` في GitHub** (‏`mergedBy`) هو **هوية بيانات الاعتماد التقنية** لبيئة الوكيل — **وليس دليلاً على أن المالك ضغط زرّ الدمج بنفسه**، ويُمنع قراءتُه كذلك.

**استقلال وكيل الدمج:** جلسة **مستقلة** · **لم يكتب محتوى PR #14** · **لم يحلّ تعارضاته** · **لم يدفع أي commit إلى فرعه** · **لم يعدّل رأسه** · قرأ المستودع والـPR **مباشرةً** · **ولم يمنح الموافقة لنفسه** (التفويض من المالك).

**تغيّر الرأس عن المسجَّل في `OD-GOV-MERGE-1` §(ح):** كان الرأس المتوقَّع `52d88d0e…`؛ ودمجُ PR #15 نقل PR #14 إلى `DIRTY` كما تنبّأ §(ح)-3، فجرت **جولة حلّ تعارض منفصلة** أنتجت merge commit أبواه `52d88d0e…` و`0c199d76…` ⇒ الرأس صار **`0020dfb6…`** و**بطَل الـSHA القديم** (بند 11)، **فصدر أمر مالك جديد يثبّت الرأس الجديد**. **ولم يُدمج أي رأس غير مثبَّت** · **ولم يُستعمل الاستثناء الانتقالي §(هـ)** (محصور بـPR #15 ومنقضٍ).

- completed: `decisions/open-decisions.md` (‏**v3.4 ⇒ v3.5** — +**«(ك) سجل أثر تنفيذ الدمج — PR #14»** داخل `OD-GOV-MERGE-1` بستة أقسام فرعية: الأبعاد الأربعة · نصّ الحساب التقني · استيفاء استقلال الوكيل · هوية المراجعة ونطاقها ونقص التتبّع · أثر تغيّر الرأس · ما لم يتغيّر — **والأقسام (أ)..(ي) لم تُمسّ**) · `handoff/handoff.md` (**+`H-0034`** — هذا المدخل) · `INDEX.md` (**صفّان محدَّثان فقط** — `decisions/open-decisions.md` و`handoff/handoff.md` — **بلا ملف جديد ⇒ بلا صفّ جديد**).
- not completed: **`ui/**` لم تُمسّ** — ومنها **`UI_DESIGN_SYSTEM.md` §9** · **`decisions/adr/**` لم تُمسّ** ومنها **`ADR-0033`** · **`methodology/**` لم تُمسّ** ومنها **`agent-execution-model.md`** · **`contracts/**` و`traceability/**` و`AUTHORITY.md` و`constitution.md` و`phases/**` و`catalogs/**` و`superseded/**` لم تُمسّ** · **لا ADR جديد ولا OD جديد** · **لا تعديل لسياسة الدمج ولا لشروطها السبعة** · **لا معالجة ولا اختبارات ولا معيار `PASS`** · **لم يُرفع التجميد** · **لم يُفكّ حجب `FP-0001`** · **لم تُفعَّل `R4`** · **`R3` لم تُغلق** · **`UI-4` و`UI-5` لم يُنشآ** · **لا وسم ولا إصدار** · **لم يُعَد فتح PR #14 ولم يُراجَع ولم يُعدَّل** · **لم يبدأ أي Workstream لاحق**.
- files changed: **ثلاثة** — `decisions/open-decisions.md` · `handoff/handoff.md` · `INDEX.md`. **ولم يُنشأ ملف جديد** ⇒ **لا صفّ جديد في `INDEX.md`** · الإجمالي **158 + الفهرس** بلا تغيير · **EC-3 = 159/159 بلا تغيير**.
- decisions: **لا قرار جديد.** هذا **استكمالُ أثرٍ إلزامي** لقرارٍ قائم (`OD-GOV-MERGE-1`) بموجب **ADR-0033 بند 12** و**§(د)-7** — **ولا OD جديد ولا ADR جديد ولا حالة `OD` قائم غُيّرت ولا قرار أُعيد ترقيمه**.
- risks: (1) **قراءة هذا السجل ترقيةً لحالة `ui/UI_DESIGN_SYSTEM.md`** — مُعالَج بالنصّ: الحالة تبقى **`Proposed`**، والدمج **نشر §9 داخلها ولم يرقِّها**، والترقية **قرار مالك مستقل**. (2) **قراءة الدمج إعلانَ `PASS` للإتاحة** — مُعالَج: **لا معيار أُعلن `PASS`**، والتقنين **إنشاءُ قاعدةٍ قابلة للقياس لا قياسٌ**. (3) **قراءة `sa4devops` دليلَ تنفيذٍ يدويٍّ من المالك** — مُعالَج بنصّ قاطع في وعاءين (‏`OD-GOV-MERGE-1` §(ك-2) وهذا المدخل). (4) **قراءة الدمج رفعاً للتجميد** — مُعالَج: **التجميد `ACTIVE`** و**`FP-0001` `BLOCKED`** وشروط الرفع **بلا مساس**؛ وتقنين §9 **يستوفي الشرط (1) وحده من سبعة تراكمية ولا يرفع شيئاً**. (5) **نقص تتبّع المراجعة المستقلة** — **مسجَّل صراحةً** (‏`Review Artifact Identifier = Not persisted outside the review conversation`) **ولم يُخترع له معرّف**؛ ومعالجتُه قرارٌ مالكٍ مستقل. (6) **قراءة هذه الجولة إذناً ببدء الجولة التالية** — مُعالَج: **لا Workstream بدأ**.
- tests: `origin/main` = **`d2c93d2c…`** (مطابق للأساس · **لا commit أحدث**) · merge commit **أبواه `0c199d76…` و`0020dfb6…`** · **PR #14 = `MERGED`** · **ثلاثة ملفات معدَّلة فقط** · **commit واحد بأبٍ واحد** و`git rev-list --merges origin/main..HEAD` = **0** · `git diff --check` **نظيف** · **`ui/**` و`decisions/adr/**` و`methodology/**` و`contracts/**` و`traceability/**` و`AUTHORITY.md` و`constitution.md` byte-identical مع `origin/main`** · **سجل `OD-FP-0001-FREEZE` وشروطه byte-identical** · **`Merge SHA` و`Head SHA` وخط الأساس الجديد حاضرة حرفياً في `open-decisions.md` و`handoff.md`** · **الأبعاد الأربعة مسجَّلة في الوعاءين** · **EC-3 = 159/159** · **16 وسماً · لا وسم ولا إصدار**.
- next step: **قرار مالك في هذا الـPR** (دمج أو رفض). و**دمجُه لا يجوز بوكيل التنفيذ نفسه** الذي كتب هذه الدفعة (‏`agent-execution-model` §18.2-1 · `OD-GOV-MERGE-1` §(ج) صفّ Execution Agent) ⇒ يلزمه **مراجعة مستقلة** و**أمر مالك يثبّت الرأس** و**وكيل دمج مستقل**. **ولا شيء بعد ذلك مأذون به في هذه الجولة.**
- do not touch: constitution.md · AUTHORITY.md · **`ui/**` بكاملها** ومنها **`UI_DESIGN_SYSTEM.md` §9** · **`contracts/**`** · **`traceability/**`** · **`decisions/adr/**` بكاملها** ومنها **`ADR-0033`** · **`methodology/**` بكاملها** ومنها **`agent-execution-model.md`** · phases/** · catalogs/** · superseded/** · **شروط التجميد و`FP-0001` و`R4`** · **أي معيار Accessibility** · **أي نص من نصوص PR #14 المدموجة** · **`H-0016`..`H-0033`** · **`R3-ACT-01`** · **أي وسم أو إصدار** · **‏GitHub Issue #11** · خط الأساس المجمَّد `188ad37` · **ملفات UI-4 وUI-5**.

> **⚠ حكمٌ لاحق على الدلتا التالية — يُقرأ قبلها ولا يُحذف منها شيء:** النموذج الوارد أدناه (`MERGE_AUDIT_RECORD_ONLY` · `TRANSITIONAL SELF-CLOSING CASE`) **`SUPERSEDED — NEVER IN FORCE`** — بقي على **فرع PR #16 وحده**، **ولم يُدمج إلى `main` قط**، **ولم يصبح سياسة نافذة** ولا لحظةً واحدة، و**استُبدل قبل النفاذ** بالنموذج المبسَّط في **ADR-0033 بند 12** (‏Δ 2026-08-04 أدناه). **يُقرأ ما يلي تاريخاً لا قاعدةً نافذة.**

**‏Δ 2026-08-03 — إغلاق تعاقب تسجيل أثر الدمج (‏ضمن `H-0034` — لا مدخل جديد):**
> **السند:** «‏OWNER CORRECTION ORDER — PR #16 Merge-Audit Recursion Closure» (2026-08-03). **نفس الفرع `docs/pr14-merge-audit-record` ونفس الـPR #16** · **commit جديد فوق الرأس `0a2c434c…`** · **بلا `amend` ولا `rebase` ولا `force-push`** · **بلا فرع أو PR جديد** · **بلا دمج**.
> **لا يُعاد كتابة تاريخ هذا المدخل:** كل ما سُجِّل أعلاه **صحيحٌ كما وقع** — وهذا **إلحاقُ دلتا** يوضّح ما استجدّ بأمر المالك، **ولا يُعدَّل به سطرٌ سابق**.

**المشكلة المُثبَتة:** تطبيق **ADR-0033 بند 12** حرفياً على دفعات تسجيل الأثر يولّد **حلقة لا تنتهي**: دمجُ PR #14 ⇒ **PR #16** لتسجيله ⇒ دمجُ PR #16 ⇒ **PR #17** ⇒ دمجُ PR #17 ⇒ **PR #18** … **وقد ظهرت الحلقة فعلاً عند إعداد PR #16**.

**قرار المالك:** اعتماد فئة ضيقة **`MERGE_AUDIT_RECORD_ONLY`** — ‏PR لا يحتوي إلا تسجيل أثر دمجٍ سابق ولا يعدّل مواصفات منتج ولا عقوداً ولا معمارية ولا سياسات (عدا التصحيح الانتقالي الأدنى المغلق للحلقة). **ولا يُطلب لها PR مستودعي لاحق**؛ ويُغلق أثرُها بـ**ثمانية أدلة مجتمعة**: أمر مالك مثبِّت الرأس · مراجعة مستقلة على الرأس نفسه · Merge Agent مستقل · **GitHub PR immutable timeline** · `Merge SHA` ووالداه · **تقرير Merge Agent منشوراً داخل الـPR بعد الدمج** · الأبعاد الأربعة · نصّ «الحساب التقني ليس تنفيذاً يدوياً من المالك».

**بند 12 لم يُلغَ:** **نافذٌ كاملاً على كل دفعة عادية** — والاستثناء **في موضع التسجيل لا في وجوبه**.

**تصنيف PR #16:** **`MERGE_AUDIT_RECORD_ONLY — TRANSITIONAL SELF-CLOSING CASE`** — لأنه يسجّل أثر دمج PR #14 **ويضيف التصحيح الأدنى** المانع للتكرار ⇒ **عند دمجه لا يحتاج `PR #17`**. **وينقضي هذا الوصف بدمجه أو رفضه أو سحب الأمر**، بينما **القاعدة العامة للفئة تبقى نافذة**.

**حدود الاستثناء — مسجَّلة:** لا ينطبق على PRs تنفيذية/معمارية/تعاقدية · لا على `ui/**` ولا `methodology/**` ولا `contracts/**` ولا كود المنتج · **لا يعفي دفعة عادية** · **لا يسمح لوكيل التنفيذ بدمج عمله** · **لا يلغي المراجعة المستقلة** ولا يقبل `Structured self-review` · **لا يسمح بتغيّر الرأس بعد أمر المالك** · **لا auto-merge غير مشروط** · **لا تخفيف للمسارات المحمية** · **وصفُ الـPR ليس مصدر سلطة عام** · **GitHub أثرُ تنفيذٍ لا وعاءُ قرار**.

**تصحيح نطاق مسجَّل — لا يُطوى:** سطر `do not touch` أعلاه في `H-0034` أدرج `decisions/adr/**` و`methodology/**` ضمن غير الممسوس، **وقد وقع مساسٌ بهما في هذه الدلتا بأمر مالك لاحق صريح** — **`ADR-0033` (+البند 15) و`agent-execution-model.md` (+§18.2-8) و`decisions/adr/README.md` (صفّ ADR-0033)**. **وهذا استثناءٌ بأمرٍ مالكٍ جديد لهذه الجولة وحدها، لا إبطالٌ للقيد السابق** — ويبقى القيد نافذاً لما عداه. **والسطر السابق لم يُعدَّل، والتصحيح مسجَّل هنا صراحةً.**

- ملفات هذه الدلتا: **ستة** — `decisions/adr/ADR-0033-automation-levels-git-merge-policy.md` (‏**+البند 15** · الحالة ⇒ **التعديل الثاني**) · `methodology/agent-execution-model.md` (‏**v2.1 ⇒ v2.2** · **+§18.2-8**) · `decisions/adr/README.md` (‏**v1.7 ⇒ v1.8** — صفّ ADR-0033 وحده) · `decisions/open-decisions.md` (‏**v3.5 ⇒ v3.6** · **+§(ل)** بخمسة أقسام فرعية — **والأقسام (أ)..(ك) لم تُمسّ**) · `handoff/handoff.md` (هذه الدلتا) · `INDEX.md` (**صفوف قائمة محدَّثة — بلا صفّ جديد**).
- ما لم يتغيّر: **`ui/**` ومنها §9** · **`contracts/**`** · **`traceability/**`** · **`AUTHORITY.md`** · **`constitution.md`** · **بقية `decisions/adr/**` وبقية `methodology/**`** · **التجميد `ACTIVE`** · **`FP-0001` `BLOCKED`** · **`R4` غير مفعَّلة** · **`R3` لم تُغلق** · **لا معيار `PASS`** · **لا ADR جديد ولا OD جديد** · **لا ملف جديد ولا محذوف** · **16 وسماً · لا وسم ولا إصدار** · **EC-3 = 159/159**.
- next step: **بلا تغيير عن أعلاه** — **مراجعة مستقلة** + **أمر مالك يثبّت الرأس الجديد** + **وكيل دمج مستقل**. **ولا يجوز لوكيل التنفيذ الذي كتب هذه الدفعة دمجُها** (‏§18.2-1). **ولم يبدأ أي Workstream لاحق.**

**‏Δ 2026-08-04 — تبسيط إتمام أثر الدمج (‏ضمن `H-0034` — لا مدخل جديد):**
> **السند:** «‏OWNER EXECUTION ORDER — PR #16 Final Merge Governance Simplification» (2026-08-04). **نفس الفرع `docs/pr14-merge-audit-record` ونفس الـPR #16** · **commit جديد فوق الرأس `0497250a…`** · **بلا `amend` ولا `rebase` ولا `force-push`** · **بلا فرع أو PR جديد** · **بلا دمج**.
> **لا يُعاد كتابة تاريخ هذا المدخل:** كلُّ ما سُجِّل أعلاه — **بما فيه دلتا 2026-08-03** — **يبقى كما كُتب**، وهذا إلحاقُ دلتا يوضّح ما استجدّ.

**‏(1) حكمُ نموذج إغلاق الحلقة السابق:**

```text
MERGE_AUDIT_RECORD_ONLY:
SUPERSEDED — NEVER IN FORCE
```

| الحقيقة | الحكم |
|---|---|
| ظهر على **فرع PR #16 وحده** (‏commit `0497250a…`) | **لم يُدمج إلى `main` قط** |
| **لم يصبح سياسة نافذة** ولا لحظةً واحدة | **`SUPERSEDED — NEVER IN FORCE`** |
| استُبدل **قبل النفاذ** بالنموذج المبسَّط | **ADR-0033 بند 12 المُعاد صياغته** |

**حُذف من المسودة قبل الدمج:** البند 15 المقترح · فئةُ دفعات التوثيق · الوصف الانتقالي ذاتي الإغلاق · **الاعتماد على GitHub PR body/timeline حاملاً دائماً للأثر** · **اشتراطُ PR توثيقي بعد الدمج**. **وكلُّ ورودٍ متبقٍّ لهذا الاسم محصورٌ في `H-0034` بوصفه تاريخاً موسوماً `SUPERSEDED — NEVER IN FORCE` — ولا يُقرأ قاعدةً نافذة في أي وعاء.** ‏**ودلتا 2026-08-03 أعلاه تُقرأ بهذا الحكم.**

**‏(2) القرار المعماري النافذ:** المعلومات **الحاكمة** تُسجَّل **قبل الدمج** في `decisions/open-decisions.md` و`handoff/handoff.md` · و**الوقائع التقنية** (الرأس المدموج · `Merge SHA` · الأبوان · التاريخ · الشجرة) **لا تُكرَّر** لأن **Git يملكها** — و**الرأس النهائي المدموج هو الأب الثاني للـMerge Commit** (`git show -s --format='%P' <MERGE_SHA>`) · و**واقعة التنفيذ** تُثبَت بـ**رسالة Merge Commit** بوصفها **إيصالَ تنفيذٍ لا وعاءَ سلطة**. ⇒ **لا تحديثَ مستودعياً بعد الدمج · لا PR لاحق · `PR #17` غير مطلوب.**

**‏(3) السجل الحاكم السابق للدمج — PR #16:**

```text
Authorization Principal      = Owner
Owner Order Reference        = OWNER EXECUTION ORDER — PR #16 Final Merge Governance Simplification
Owner Order Date             = 2026-08-04
PR                           = #16
Permitted Scope              = decisions/adr/ADR-0033-automation-levels-git-merge-policy.md
                               decisions/adr/README.md
                               methodology/agent-execution-model.md
                               decisions/open-decisions.md
                               handoff/handoff.md
                               INDEX.md
                               PR #16 title and description
Required Review Actor        = Independent Review Session (did not author or modify this PR)
Required Review Result       = APPROVE
Authorized Execution Actor   = Owner-Authorized Independent Merge Agent
                               (third session: not the author, not the reviewer)
Expected Technical Credential = GitHub token for account sa4devops used by the agent environment
Credential Statement         = The technical account sa4devops is NOT evidence of manual Owner execution
Merge Method                 = merge commit
Pending Merge SHA            = assigned automatically by Git
```

**‏(4) نصّ رسالة Merge Commit المتوقَّع — مثبَّتٌ حرفياً:**

```text
Merge PR #16 — GOV — Record PR #14 Merge Provenance and Simplify Merge Audit Completion

Governance record: OD-GOV-MERGE-1 · H-0034
Executed by Owner-Authorized Independent Merge Agent.
Technical account sa4devops is not evidence of manual Owner execution.
```

**قواعد المطابقة:** توحيدُ نهايات الأسطر إلى **`LF`** · حذفُ **المسافات الطرفية** من كل سطر · حذفُ **الأسطر الفارغة الزائدة** في البداية والنهاية. **ولا يُسمح باختلاف الكلمات ولا ترتيب الأسطر** ⇒ **الاختلاف بعد التطبيع = `MERGE RECEIPT MISMATCH` ⇒ لا دمج.** **ولا يُضاف `Authorized head` إلى الرسالة.**

**‏(5) استثناء دورة التصحيح على بند 11:** تغيُّرُ الرأس الناتجُ **حصراً** عن معالجة ملاحظات مراجعةٍ مستقلة **داخل نطاق الأمر نفسه وبلا ملفات أو موضوعات جديدة** ⇒ **لا أمر مالك جديداً**، بشرط **مراجعة مستقلة كاملة للرأس الجديد** و**عدم دمج رأسٍ لم يحصل هو نفسه على `APPROVE`**. **وبند 11 نافذ بكامل أثره فيما عدا ذلك.**

**‏(6) الاكتفاء الذاتي:** **لا اعتماد حاكم على GitHub ولا أي خدمة خارجية** — أدواتُ عملٍ أثناء التطوير فقط. **ووحدة التاريخ الحاكم المحمولة هي المستودع الكامل متضمناً `.git`**: شجرةُ الملفات تكفي **لقراءة الحالة الحالية**، وإعادةُ بناء **تاريخ الدمج والوقائع التقنية** **تلزمها `.git`**. **والنسخة المسلَّمة على الفلاش يجب أن تحتوي مستودعات المشروع كاملةً مع تاريخها** · **والنسخُ والتنصيبُ لا يتطلبان تعديل ملفات ولا إضافة بيانات حوكمة** · **أحجام تقريبية مقيسة من المالك 2026-08-04:** الشجرة **≈ 3.3 MB** · المستودع الكامل **≈ 7.2 MB** · الفرق **≈ 4 MB** · **ولا مبرر لإسقاط `.git`**. **ولا Bundle ولا Script ولا دليل تنصيب في هذه الجولة.**

- ملفات هذه الدلتا: **ستة** — `decisions/adr/ADR-0033-automation-levels-git-merge-policy.md` (**حذف البند 15 المقترح** · **بند 11** +استثناء دورة التصحيح · **بند 12** مُعاد صياغته · **بند 10-(ز)** موائم · **+حدود المراجع المستقل** · **+الاكتفاء الذاتي**) · `methodology/agent-execution-model.md` (**§18.2-8** مُستبدَل · **+§18.2-9** و**§18.2-10** · تشديد صفّ Review Agent في §18.1) · `decisions/adr/README.md` · `decisions/open-decisions.md` (**§(ل) مُستبدَل بالكامل** — والأقسام (أ)..(ك) لم تُمسّ) · `handoff/handoff.md` (هذه الدلتا) · `INDEX.md` (**صفوف قائمة — بلا صفّ جديد**). **وعنوان ووصف PR #16 حُدِّثا.**
- ما لم يتغيّر: **`ui/**` ومنها §9** · **`contracts/**`** · **`traceability/**`** · **`AUTHORITY.md`** · **`constitution.md`** · **بقية `decisions/adr/**` وبقية `methodology/**`** · **شروط بند 10 السبعة** · **التجميد `ACTIVE`** · **`FP-0001` `BLOCKED`** · **`R4` غير مفعَّلة** · **`R3` لم تُغلق** · **لا معيار `PASS`** · **لا ADR جديد ولا OD جديد** · **لا ملف جديد ولا محذوف** · **16 وسماً · لا وسم ولا إصدار** · **EC-3 = 159/159**.
- next step: **مراجعة مستقلة** على الرأس الجديد (جلسة لم تشارك في التنفيذ) ⇒ **`APPROVE`** ⇒ **Merge Agent مستقل** (جلسة ثالثة ليست المؤلف ولا المراجع) يطابق نصّ الإيصال **قبل** التنفيذ ثم يدمج. **ولا يجوز لوكيل التنفيذ الذي كتب هذه الدفعة مراجعتُها ولا دمجُها.** **ولم يبدأ أي Workstream لاحق.**

## Handoff H-0035
> **‏R3 — Priority Screen Contracts Expansion.** يُقرأ بعد `H-0034` ولا ينسخه: `H-0034` صحيحٌ في تاريخه وقد سجّل أثر دمج PR #14 ثم بُسِّط إتمامُ أثر الدمج بدمج PR #16؛ **وهذه الجولة دفعةٌ تعاقدية تنفّذ مخرج `R3` المسجَّل: توسيع تغطية عقود الشاشات ذات الأولوية.** **لا إعادة كتابة لأي مدخل سابق.** **ولا تغيير في `FP-0001` ولا في التجميد ولا في جرد `P3` ولا في أي مخرج مجمَّد.**
- date: 2026-08-04
- phase: **R3 — Priority Screen Contracts Expansion** — فرع جديد `docs/r3-priority-screen-contracts` من `origin/main` مباشرة · **PR #17 غير مدموج**
- task/goal: مواءمة **عقدَي الشاشات ذوَي الأولوية** `contracts/screens/run.list.md` و`contracts/screens/admin.actions.md` مع **`contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` v1.1**، مع **حفظ حالتهما `Candidate`** و**عدم ادّعاء ترقيتهما إلى `Approved`**. **لا merge · لا tag · لا release · لا rebase · لا amend · لا force-push · لا رفع تجميد · لا فكّ حجب `FP-0001` · لا تفعيل `R4` · لا إغلاق `R3` · لا اختبارات ولا CI.**
- base SHA: **`origin/main` = `e81ea775d119971e2efed2646c5b006df1706388`** — **مطابقٌ حرفياً** للـSHA المثبَّت في أمر المالك · **عدد الوسوم = 16 بلا تغيير**.
- **خطية الفرع:** أُنشئ من `origin/main` مباشرة · كل commit **بأبٍ واحد** · **صفر merge commit** · بلا rebase ولا amend ولا force-push.

**التحقق من الأساس قبل أي كتابة — نتائجه:**

| الفحص | النتيجة |
|---|---|
| `origin/main` = ‏`EXPECTED_MAIN_SHA` | **مطابق** — `e81ea775d119971e2efed2646c5b006df1706388` |
| **PR #16 مدموج** | **نعم** — رأسه `4992f0d837512d93295319678031a3731f151afa` **سلفٌ لـ`origin/main`** |
| **رؤوس PR غير مدموجة** | **صفر** — جُرِدت **أربعة عشر** رأساً بـ`git ls-remote origin 'refs/pull/*/head'`، و**كلها أسلافٌ لـ`origin/main`** بـ`git merge-base --is-ancestor` ⇒ **لا رأس يمسّ العقدين ولا القالب** |
| **التجميد** | **`OD-FP-0001-FREEZE` = `ACTIVE`** |
| **`FP-0001`** | **`BLOCKED`** |
| **`R4`** | **غير مفعَّلة** |
| **`contracts/fields/`** | **غير موجود** — والمجلد **لم يُنشأ**، ولا مرجعٌ إلزامي معلَّق إليه |

- **V1 — نطاق `R3`:** تعديل العقدين **يطابق المخرج المسجَّل** في `methodology/RECONCILIATION_ROADMAP.md:11` («توسيع عقود الشاشات ذات الأولوية … المخرج: عقود Candidate إضافية»). **ولا نصّ أعلى رتبة يمنع تحديث عقد `Candidate`.** ولم يُعالَج في هذه الجولة **تعارض ميثاق `R3`** الخاص بالإتاحة ولا `UI-4` — يبقيان كما هما.
- **V2 — مسار اعتماد العقود:** **التعارض مثبَتٌ بالقراءة**: `contracts/NAMING_AND_CONTRACTS_STANDARD.md` §2 («بتوقيع SA **أو** بوابة FP معتمدة») ⇄ `SCREEN_CONTRACT_TEMPLATE.md` «دورة الاعتماد» («عبر بوابة FP … **بتوقيع SA**»). **لم يُحسم · لم يُرقَّ عقد · الحالة `Candidate` محفوظة · وسُجِّل تبعيةً لاحقة لاعتماد العقود لا مانعاً عن تحديث عقود `Candidate`** — الوعاء `decisions/open-decisions.md` → `OD-R3-CONTRACTS-1` §(ب).
- **V3 — `contracts/fields/`:** **غائب** ⇒ ما لا وعاء له سُجِّل **`DOWNSTREAM DEPENDENCY`** (`DD-RL-1` · `DD-AC-1`) **ولم يُخترع حقلٌ ولا عقدٌ صامتاً**.
- completed: `contracts/screens/run.list.md` (‏0.1 ⇒ **0.2**: §3-أ `surfaces[]` بستة أسطح · §3-ب سلوك كل سطح · §3-ج التعامد · §3-د الترتيب المنطقي المعلَن · §3-هـ أنماط `S8` · §4 إعلان الحالات نصاً · §5 (د)/(هـ) · §7-أ ثماني تبعيات) · `contracts/screens/admin.actions.md` (‏0.1 ⇒ **0.2**: §3-أ `surfaces[]` بستة أسطح · §3-ب · §3-ج · §3-د · §3-هـ · §4 · §5-أ الفصل بين `action_id` والنص الظاهر · §7-أ ثماني تبعيات) · `decisions/open-decisions.md` (‏v3.6 ⇒ **v3.7**: +`OD-R3-CONTRACTS-1` بخمسة أقسام فرعية — **والأقسام السابقة لم تُمسّ**) · `handoff/handoff.md` (هذا المدخل) · `INDEX.md` (**صفوف قائمة محدَّثة — بلا صفّ جديد**).
- **`surfaces[]` — الإعلان الناتج:** `run.list` = **`PAGE` ×1 · `DRAWER` ×3 · `DIALOG` ×1 · `TRANSIENT` ×1** · `admin.actions` = **`PAGE` ×2 · `DRAWER` ×2 · `DIALOG` ×2**. **كلها من التعداد المغلق الخماسي** — **ولم يُخترع نوع سطح**، و**`WIZARD_STEP` و`COMMAND_SURFACE` و`AGENT_CONVERSATION_SURFACE` بقيت مؤجَّلة ولم تُستعمل**. و**كل سطح يحمل سنداً مشتقّاً منه** في جدول «سند اشتقاق كل سطح» — **لا تأليف موازٍ**.
- **خريطة التحويل:** **صفر ورودٍ** للأسماء النثرية القديمة (`page` · `modal` · `drawer` · `inline` · `toast`) في العقدين — **لا في الإعلان ولا في السند ولا في بقية الأقسام**.
- not completed: **الحالتان تبقيان `Candidate`** — **لا ترقية ولا ادّعاء ترقية** · **المرتبة 5 تبقى خالية فعلياً** و`OD-GOV-2` **مفتوح بلا مساس** · **`ui/UI_DESIGN_SYSTEM.md` §9 لم يُمسّ** و**لا معيار `R3-A11Y-01`..`07` أُعلن `PASS`** · **`contracts/fields/` لم يُنشأ** · **`SCREEN_CONTRACT_TEMPLATE.md` و`NAMING_AND_CONTRACTS_STANDARD.md` لم يُمسّا** · **`admin.record_types.md` و`admin.workflows.md` لم يُمسّا** · **لا `UI-4` ولا `UI-5`** · **لا Rendering Topology ولا Authoring Provenance** · **`Action Registry` لم يُوسَّع** · **التجميد لم يُرفع** · **`FP-0001` = `BLOCKED`** · **`R4` لم تُفعَّل** · **`R3` لم تُغلق** · **تعارض مسار اعتماد العقود لم يُحسم** · `GOV-OBS-03` و`OD-GOV-1` و`OD-GOV-2` و`OD-P3-2` و`P3-CI-28` **بلا مساس** · **لا اختبار بُني ولا نُفِّذ** · **لا وسم ولا إصدار**.
- files changed: **خمسة** — `contracts/screens/run.list.md` · `contracts/screens/admin.actions.md` · `decisions/open-decisions.md` · `handoff/handoff.md` · `INDEX.md`. **ولم يُنشأ ملف جديد ولم يُحذف** ⇒ **لا صفّ جديد في `INDEX.md`** والإجمالي **158 ملفاً + الفهرس** بلا تغيير · **EC-3 = 159/159**.
- decisions: **قرار مالك واحد جديد** = **`OD-R3-CONTRACTS-1`** (سجل توسيع عقود الشاشات ذات الأولوية + السجل الحاكم السابق للدمج). **لا ADR · لا قرار معماري · لا إعادة ترقيم لأي `OD` قائم · لا تغيير لحالة أي `OD` آخر · ولم تُنشأ طبقة سلطة جديدة.**
- risks: (1) **قراءة الدلتا ترقيةً ضمنية للعقود** — مُعالَج بنصّ صريح في ترويسة كل عقد وفي §(أ) و§(د) من السجل: **الحالة `Candidate` والمرتبة 5 خالية**. (2) **قراءة إعلان `surfaces[]` استيفاءً لمعايير §9** — مُعالَج بحدٍّ صريح في §5 و§8 من العقدين: **بنودُ قبولٍ للعقد لا نتيجةَ قياس، ولا معيار `PASS`**. (3) **قراءة التبعيات المسجَّلة شروطَ رفعٍ جديدة** — مُعالَج بقاعدة قاطعة في §(ج): **تسجيلُ تبعيةٍ ليس إضافةَ شرط رفع**، وشروط `OD-FP-0001-FREEZE` **مغلقة على المنصوص عليه**. (4) **الخلط بين `PR #17` هذا و«`PR #17` غير مطلوب» في `OD-GOV-MERGE-1` §(ل-1)** — مُعالَج بتنبيهٍ ترقيميّ صريح في §(هـ): **ذاك PR توثيقيّ لاحق سقط وجوبُه، وهذا دفعةٌ تعاقدية عادية تخضع لبند 12 كاملاً، والتوافق محضُ تسلسلٍ من GitHub**. (5) **قراءة `admin.actions` شاشتين لوجود سطحَي `PAGE`** — مُعالَج بنصّ §3-ج: **الهوية `screen_id` واحدة**، و**المسار الثاني غير مسجَّل في الجرد** ومسجَّل تبعيةً `DD-AC-3` بلا اختراع مسار.
- tests: `origin/main` = **`e81ea775d119971e2efed2646c5b006df1706388`** (مطابق) · **أربعة عشر رأس PR كلها أسلاف لـ`origin/main`** ⇒ صفر رأس غير مدموج · `git diff --check` **نظيف** · **صفر تعديل خارج القائمة البيضاء الخماسية** · **صفر ورود** للأسماء النثرية القديمة للأسطح في العقدين · **كل `type:` من التعداد المغلق الخماسي** (‏`PAGE`/`DIALOG`/`DRAWER`/`TRANSIENT` — و`INLINE_PANEL` غير مستعمل) · **صفر قيمة `null`** في حقول الأسطح · **`focus_return_target` معلَن لكل `DIALOG` و`DRAWER`** (‏سبعة أسطح) وغير معلَن حيث لا يوجبه القالب · **`status: Candidate`** في العقدين · **صفر ادّعاء `Approved`** · **صفر ورود** لـ`rendering_topology`/`authoring_origin`/`provenance_ref` بوصفها محاور · `ui/**` و`traceability/**` و`AUTHORITY.md` و`constitution.md` و`methodology/**` و`decisions/adr/**` وبقية `contracts/**` **byte-identical مع `origin/main`** · جرد `P3` **`28 = 13 + 15 + 0`** · `FP-0001` = **`BLOCKED`** · التجميد **`ACTIVE`** · `R3` = **`ACTIVE — SPECIFICATION ONLY`** · **`R4` غير مفعَّلة** · **صفر معيار `PASS`** · `INDEX.md` **مطابق للشجرة** (‏158 صفاً + الفهرس · صفر ملف خارج الفهرس · صفر صفّ بلا ملف) · **لا وسم ولا إصدار**.
- **المراجعة:** جلسةُ التنفيذ أجرت **`Structured self-review`** فقط — **وهي ليست مراجعة مستقلة** ولا تستوفي `ADR-0033` بند 10-(ج) ولا `OD-GOV-MERGE-1` §(د)-3.
- next step: **مراجعة مستقلة** على الرأس النهائي (جلسة لم تكتب ولم تعدّل هذه الدفعة) ⇒ **`APPROVE`** ⇒ **Merge Agent مستقل** (جلسة ثالثة ليست المؤلف ولا المراجع) يطابق **نصّ إيصال الدمج المثبَّت** في `OD-R3-CONTRACTS-1` §(هـ) **قبل** التنفيذ ثم يدمج، ثم **تحقُّق قراءةً فقط بعد الدمج** بلا أي تحديث مستودعي لاحق (‏ADR-0033 بند 12-(هـ) البندان 6 و7). **ولا يجوز لوكيل التنفيذ الذي كتب هذه الدفعة مراجعتُها ولا دمجُها.** **ولم يبدأ أي Workstream لاحق.**
- do not touch: constitution.md · AUTHORITY.md · methodology/** · phases/** · ui/** (‏ومنها `UI_DESIGN_SYSTEM.md` §9) · decisions/adr/** · catalogs/** · traceability/** · `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` · `contracts/NAMING_AND_CONTRACTS_STANDARD.md` · `contracts/screens/admin.record_types.md` · `contracts/screens/admin.workflows.md` · `contracts/identity/**` · `contracts/enums/**` · **`contracts/fields/**` (غير موجود — لا يُنشأ)** · أي ملف في `aql` · **أي وسم أو إصدار** · **أي سجل تفعيل `R4`** · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.4 · **H-0016..H-0034**.

**‏Δ 2026-08-04 — جولة تصحيح بعد المراجعة المستقلة (‏ضمن `H-0035` — لا مدخل جديد):**
> **السند:** «‏**OWNER CORRECTION ORDER — PR #17 Required Review Corrections**» (2026-08-04). **نفس الفرع `docs/r3-priority-screen-contracts` ونفس الـPR #17** · **commit جديد فوق الرأس `01b9f2e5…`** · **بلا `amend` ولا `rebase` ولا `force-push`** · **بلا فرع أو PR جديد** · **بلا دمج**.
> **لا يُعاد كتابة تاريخ هذا المدخل:** كلُّ ما سُجِّل أعلاه **يبقى كما كُتب**، وهذا إلحاقُ دلتا يوضّح ما استجدّ.

**نتيجة المراجعة المستقلة على الرأس السابق:** **`REQUEST CHANGES`** على الرأس **`01b9f2e5436747b50865b8a5ca28fa29686769ea`** بأربع ملاحظات، بُلِّغت عبر أمر المالك.

| ‏ID | الملاحظة | التصحيح |
|---|---|---|
| **`C1`** | ‏`run.list`: هدفان متنافسان لعودة التركيز — `AUTO_TRIGGER` في `surfaces[]` مقابل `record.search` في النثر | `drawer_row_preview` و`drawer_row_audit_chain` يعلنان **`focus_return_target: record.search`** بنيوياً (نوع `<action_id>` لفعلٍ قائم في §2)، وأُزيل النثر المتعارض؛ والسطحان الباقيان `AUTO_TRIGGER` بتعليل عدم الزوال |
| **`C2`** | ‏`admin.actions`: احتمال زوال ضابط `drawer_definition_audit_chain` بلا معالجة §3.2 | **إثبات عدم الزوال بالدليل** بدل هدفٍ غير لازم: ضوابط الأسطح الأربعة على `page_action_contract_editor` لا على صفّ القائمة (‏`UI_COMPONENT_STATES` §10 «Admin Definition Card» · بطاقة 12 لا تُسند إلى القائمة إلا المحاكاة)، **ولا فعل حذفٍ معلَناً** — القاعدة 6 في §3-ب |
| **`C3`** | ‏`run.list`: تناقض `S19` بين §3-ب و§4/`DD-RL-4` | **أُزيل `S19` من `transient_action_feedback`** — سطحُ نتيجةٍ بعد الإقرار لا سطحُ كتابةٍ قيد النقل؛ و`S19`/`S20` تبقيان `DOWNSTREAM DEPENDENCY` |
| **`C4`** | ‏`run.list`: «الأسطح الثلاثة» بينما المسمّى سطحان | صُحِّح إلى **«السطحان»** — **بلا إضافة سطح ثالث** |

- ملفات هذه الدلتا: **خمسة** — `contracts/screens/run.list.md` (‏`C1`/`C3`/`C4`) · `contracts/screens/admin.actions.md` (‏`C2`) · `decisions/open-decisions.md` (‏**+§(و)** داخل `OD-R3-CONTRACTS-1` — والأقسام (أ)..(هـ) لم تُمسّ) · `handoff/handoff.md` (هذه الدلتا) · `INDEX.md` (صفوف قائمة — بلا صفّ جديد). **ووصف PR #17 حُدِّث.**
- **الأثر السلطوي:** **الرأس السابق `01b9f2e5…` لم يعد مؤهلاً للدمج** · **الرأس الجديد يحتاج مراجعة مستقلة كاملة** ولا تُسجَّل نتيجتُها قبل وقوعها · **استثناء دورة التصحيح منطبق** (‏ADR-0033 بند 11) فلا يلزم أمر مالك جديد، و**نطاق التفويض ونصّ إيصال الدمج في `OD-R3-CONTRACTS-1` §(هـ) نافذان بلا تعديل** · **ولا يجوز لوكيل التنفيذ الذي كتب وصحَّح هذه الدفعة مراجعتُها ولا دمجُها**.
- ما لم يتغيّر: **العقدان `Candidate` `v0.2`** · **`surfaces[]` لم تتوسّع** (ستة + ستة) · **لا سطح ولا `action_id` ولا حقل ولا حالة `S` ولا نوع سطح جديد** · **لا `<control_id>`** · **تعارض `filter`/`define`/`edit` لم يُحسم** · **`contracts/fields/` لم يُنشأ** · **القالب و`ui/**` ومنها §9 و`methodology/**` و`decisions/adr/**` و`traceability/**` لم تُمسّ** · **لا `UI-4` ولا `UI-5`** · **التجميد `ACTIVE`** · **`FP-0001` `BLOCKED`** · **`R4` غير مفعَّلة** · **`R3` لم تُغلق** · **16 وسماً · لا وسم ولا إصدار** · **EC-3 = 159/159**.
- next step: **مراجعة مستقلة كاملة على الرأس الجديد** ⇒ **`APPROVE`** ⇒ **Merge Agent مستقل** (جلسة ثالثة) يطابق نصّ الإيصال المثبَّت **قبل** التنفيذ ثم يدمج، ثم **تحقُّق قراءةً فقط بعد الدمج**. **ولم يبدأ أي Workstream لاحق.**

---

## Handoff H-0036
> **‏R3 — `BATCH_A` Remaining Candidate Contract Alignment.** يُقرأ بعد `H-0035` ولا ينسخه ولا يعيد كتابته: `H-0035` صحيحٌ في تاريخه وقد سجّل مواءمة عقدَي `run.list` و`admin.actions` (‏PR #17، **مدموج** الآن)؛ **وهذه الجولة دفعةٌ تعاقدية تالية تنفّذ المخرج نفسه على العقدين المتبقّيين.** **لا تغيير في `FP-0001` ولا في التجميد ولا في جرد `P3` ولا في أي مخرج مجمَّد.**
> **تحقُّق ترقيم:** ‏`H-0036` **غير مستعمَل** في السجل عند تحرير هذا المدخل — تحقُّقاً من الملف لا افتراضاً؛ و`H-0016`..`H-0035` **لم تُمسّ**.

- date: 2026-08-05
- phase: **R3 — Remaining Contracts · `BATCH_A`** — فرع جديد `docs/r3-batch-a-contract-alignment` من `origin/main` مباشرة · **PR #18 غير مدموج**
- task/goal: مواءمة **عقدَي الشاشات المرشَّحين المتبقّيين** `contracts/screens/admin.record_types.md` و`contracts/screens/admin.workflows.md` مع **`contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` v1.1** على **نمط PR #17 نفسه**، مع **حفظ حالتهما `Candidate`** و**عدم ادّعاء ترقيتهما إلى `Approved`**. **لا merge · لا tag · لا release · لا rebase · لا amend · لا force-push · لا حذف فرع · لا تعديل إعدادات مستودع ولا CI · لا رفع تجميد · لا فكّ حجب `FP-0001` · لا تفعيل `R4`/`R5` · لا إغلاق `R3` · لا اختبارات ولا CI.**
- base SHA: **`origin/main` = `48fcdfd93eebf68abde85d664d107de7cbeda502`** — **مطابقٌ حرفياً** للـSHA المثبَّت في أمر المالك.
- **خطية الفرع:** أُنشئ من `origin/main` مباشرة · كل commit **بأبٍ واحد** · **صفر merge commit** · بلا rebase ولا amend ولا force-push.

**التحقق من الأساس قبل أي كتابة — نتائجه:**

| الفحص | النتيجة |
|---|---|
| `origin/main` = ‏`EXPECTED_ORIGIN_MAIN_SHA` | **مطابق** — `48fcdfd93eebf68abde85d664d107de7cbeda502` |
| **PR #17 مدموج** ورأسه = `EXPECTED_PR17_MERGED_HEAD` | **مطابق** — `6c965377bb35611ba72499bb200b94cef027ea21` · و**Merge Commit** له = `48fcdfd9…` = `origin/main` |
| **رؤوس PR غير مدموجة** | **صفر** — جُرِدت **خمسة عشر** رأساً بـ`git ls-remote origin 'refs/pull/*/head'`، و**كلها أسلافٌ لـ`origin/main`** بـ`git merge-base --is-ancestor` ⇒ **لا رأس يمسّ العقدين ولا القالب** · و`gh pr list --state open` = **صفر** |
| **التجميد** | **`OD-FP-0001-FREEZE` = `ACTIVE`** |
| **`FP-0001`** | **`BLOCKED`** |
| **`R4`** | **`NOT_ACTIVATED`** |
| **`contracts/fields/`** | **غير موجود** — والمجلد **لم يُنشأ**، ولا مرجعٌ إلزامي معلَّق إليه |
| **`contracts/screens/admin.workflow_detail.md`** | **غير موجود قبل الدفعة وبعدها** — **لم يُنشأ** |

- **V1 — نطاق `R3`:** تعديل العقدين **يطابق المخرج المسجَّل** في `methodology/RECONCILIATION_ROADMAP.md:11` («توسيع عقود الشاشات ذات الأولوية … المخرج: عقود Candidate إضافية»). **ولا نصّ أعلى رتبة يمنع تحديث عقد `Candidate`.**
- **V2 — مسار اعتماد العقود:** التعارض **قائمٌ ومسجَّلٌ أصلاً** في `OD-R3-CONTRACTS-1` §(ب) — **يُحال ولا يُكرَّر ولا يُحسم**؛ ومسجَّلٌ عقدياً `DD-RT-APPROVAL-PATH` و`DD-WF-APPROVAL-PATH`. **لم يُرقَّ عقد · الحالة `Candidate` محفوظة.**
- **V3 — تنازع إسناد أفعال الـWorkflow:** **مثبَتٌ بالقراءة** بين ثلاثة نصوص في المرتبة نفسها (‏الجرد B ⇄ بطاقة 13 ⇄ `UI_ADMIN_CONSOLE_MODEL` §4-D). **لم يُحسم**؛ **أُبقيت الأسطح المشتقّة من بطاقة 13** بأمر المالك، **وسُجِّل `DD-WF-ALLOC`** — الوعاء `decisions/open-decisions.md` → `OD-R3-CONTRACTS-2` §(ب)-1.
- completed: `contracts/screens/admin.record_types.md` (‏0.1 ⇒ **0.2**: §3-أ `surfaces[]` بسبعة أسطح + جدول السند · §3-ب سلوك كل سطح + سبع قواعد · §3-ج التعامد · §3-د الترتيب المنطقي المعلَن · §3-هـ أنماط `S8` · §4-أ تصريح `S16`–`S20` · §5 (هـ)/(و)/(ز) · §7-أ سبع تبعيات) · `contracts/screens/admin.workflows.md` (‏0.1 ⇒ **0.2**: §3-أ `surfaces[]` بسبعة أسطح + جدول السند + «ما ليس سطحاً» · §3-ب · §3-ج · §3-د · §3-هـ · §4-أ · §5 (هـ)..(ح) · §6 حالة `CC-WF-1/2/3` · §7-أ إحدى عشرة تبعية — **وقسم الإدارة المنطاقة ADR-0037 محفوظٌ بنصّه**) · `decisions/open-decisions.md` (‏v3.7 ⇒ **v3.8**: +`OD-R3-CONTRACTS-2` بخمسة أقسام فرعية — **والأقسام السابقة ومنها `OD-R3-CONTRACTS-1` لم تُمسّ**) · `handoff/handoff.md` (هذا المدخل) · `INDEX.md` (**صفوف قائمة محدَّثة — بلا صفّ جديد**).
- **`surfaces[]` — الإعلان الناتج:** `admin.record_types` = **`PAGE`×2 · `DRAWER`×3 · `DIALOG`×2 = سبعة** · `admin.workflows` = **`PAGE`×1 · `DRAWER`×3 · `DIALOG`×3 = سبعة**. **كلها من التعداد المغلق الخماسي** — **ولم يُخترع نوع سطح**، و**`WIZARD_STEP` و`COMMAND_SURFACE` و`AGENT_CONVERSATION_SURFACE` بقيت مؤجَّلة ولم تُستعمل**، و**`INLINE_PANEL` غير مستعمل**. و**كل سطح يحمل سنداً مشتقّاً منه** في جدول «سند اشتقاق كل سطح» — **لا تأليف موازٍ**.
- **خريطة التحويل:** **صفر ورودٍ** للأسماء النثرية القديمة (`page` · `modal` · `drawer` · `inline` · `toast`) **بوصفها وسوم أسطح** في العقدين — **لا في الإعلان ولا في السند ولا في بقية الأقسام**.
- **`admin.workflow_detail`:** **شاشةٌ شقيقة لا سطح** — منصوصٌ عليه حرفياً في عقد `admin.workflows` §3 و§3-أ: «‏**Opening a workflow navigates to `admin.workflow_detail`; it is not counted as a surface of `admin.workflows`.**» **ولم يُنشأ ملفُ عقدٍ لها، ولم تُنشأ بطاقة سلوك 25، ولم يُعدَّل الجرد** — مسجَّلٌ تبعيةً `DD-WF-DETAIL-SCREEN`.
- not completed: **الحالتان تبقيان `Candidate`** — **لا ترقية ولا ادّعاء ترقية** · **المرتبة 5 تبقى خالية فعلياً** و`OD-GOV-2` **مفتوح بلا مساس** · **لا عقد شاشة جديد** · **`contracts/screens/admin.workflow_detail.md` لم يُنشأ** · **`ui/**` لم تُمسّ** ومنها `UI_SCREEN_INVENTORY.md` و`UI_SCREEN_BEHAVIOR_CARDS.md` و`UI_DESIGN_SYSTEM.md` §9 · **لا معيار `R3-A11Y-01`..`07` أُعلن `PASS`** · **`contracts/fields/` لم يُنشأ** · **`contracts/enums/**` و`contracts/identity/**` لم تُمسّ** · **`SCREEN_CONTRACT_TEMPLATE.md` و`NAMING_AND_CONTRACTS_STANDARD.md` و`run.list.md` و`admin.actions.md` لم تُمسّ** · **لا إعادة تسمية `action_id`** · **`OD-P3-1` و`OD-P3-2` و`CC-WF-1` و`CC-WF-2` و`CC-WF-3` و`CC-RT-1..3` بلا حسم** · **لا `UI-4` ولا `UI-5`** · **التجميد لم يُرفع** · **`FP-0001` = `BLOCKED`** · **`R4` = `NOT_ACTIVATED`** و`R5` لم تُفعَّل · **`R3` لم تُغلق** · `GOV-OBS-03` و`OD-GOV-1` و`P3-CI-28` **بلا مساس** · **لا اختبار بُني ولا نُفِّذ** · **لا وسم ولا إصدار**.
- files changed: **خمسة** — `contracts/screens/admin.record_types.md` · `contracts/screens/admin.workflows.md` · `decisions/open-decisions.md` · `handoff/handoff.md` · `INDEX.md`. **ولم يُنشأ ملف جديد ولم يُحذف** ⇒ **لا صفّ جديد في `INDEX.md`** والإجمالي **158 ملفاً + الفهرس** بلا تغيير · **EC-3 = 159/159**.
- decisions: **قرار مالك واحد جديد** = **`OD-R3-CONTRACTS-2`** (سجل مواءمة عقود المرشَّح المتبقّية + السجل الحاكم السابق للدمج). **لا ADR · لا قرار معماري · لا إعادة ترقيم لأي `OD` قائم · لا تغيير لحالة أي `OD` آخر · ولم تُنشأ طبقة سلطة جديدة.**
- risks: (1) **قراءة الدلتا ترقيةً ضمنية للعقود** — مُعالَج بنصّ صريح في ترويسة كل عقد وفي §(أ) و§(د) من السجل: **الحالة `Candidate` والمرتبة 5 خالية**. (2) **قراءة ورود اسم `admin.workflow_detail` إيحاءً بوجود عقدٍ لها** — مُعالَج بنصّ §(د)-2 من السجل وبقاعدة القراءة في §3 من عقد `admin.workflows`: **إحالةٌ إلى شاشةٍ شقيقة وتبعيةٍ لاحقة، والملف غير موجود**. (3) **قراءة إبقاء أسطح الاعتماد/التفعيل حسماً لتنازع الإسناد** — مُعالَج بـ§(ب)-1 و`DD-WF-ALLOC`: **إبقاءٌ بأمر المالك لهذه المواءمة، لا قرارَ ملكية**. (4) **قراءة `AUTO_TRIGGER` في `admin.workflows` إغفالاً لشرط الهدف البديل** — مُعالَج بالقاعدة 6 في §3-ب: **بيانُ سببٍ صريح** (لا فعل قراءةٍ ثابتاً في §2 · و`<control_id>` خارج الأنواع الثمانية) **وتسجيلُ `DD-WF-FOCUS-RETURN`** بدل اختراع معرّف. (5) **قراءة التبعيات المسجَّلة شروطَ رفعٍ جديدة** — مُعالَج بقاعدة قاطعة في §(ج): **تسجيلُ تبعيةٍ ليس إضافةَ شرط رفع**. (6) **قراءة تصريح `S16`/`S17` المضاف تصويباً صامتاً** — مُعالَج بـ«ملاحظة اكتمال» في §4-أ من العقدين: **إكمالُ تصريحٍ من المصفوفة الحاكمة نفسها، بلا مساسٍ بها**.
- tests: `origin/main` = **`48fcdfd93eebf68abde85d664d107de7cbeda502`** (مطابق) · رأس **PR #17** = `6c965377…` (مطابق) · **خمسة عشر رأس PR كلها أسلاف لـ`origin/main`** ⇒ صفر رأس غير مدموج · **صفر PR مفتوح** · `git diff --check` **نظيف** · **صفر تعديل خارج القائمة البيضاء الخماسية** · **صفر ورود** للأسماء النثرية القديمة للأسطح في العقدين · **كل `type:` من التعداد المغلق الخماسي** · **صفر قيمة `null`** في حقول الأسطح · **`focus_return_target` معلَن لكل `DIALOG` و`DRAWER`** (‏أحد عشر سطحاً) وغير معلَن حيث لا يوجبه القالب (‏ثلاثة أسطح `PAGE`) · **`status: Candidate`** في العقدين · **صفر ادّعاء `Approved`** · **صفر ورود** لـ`rendering_topology`/`authoring_origin`/`provenance_ref` بوصفها محاور · **`contracts/screens/admin.workflow_detail.md` غير موجود** · `ui/**` و`traceability/**` و`AUTHORITY.md` و`constitution.md` و`methodology/**` و`decisions/adr/**` و`phases/**` و`catalogs/**` وبقية `contracts/**` **byte-identical مع `origin/main`** · جرد `P3` **`28 = 13 + 15 + 0`** · `FP-0001` = **`BLOCKED`** · التجميد **`ACTIVE`** · `R3` = **`ACTIVE — SPECIFICATION ONLY`** · **`R4` `NOT_ACTIVATED`** · **صفر معيار `PASS`** · `INDEX.md` **مطابق للشجرة** (‏158 صفاً + الفهرس · صفر ملف خارج الفهرس · صفر صفّ بلا ملف) · **لا وسم ولا إصدار**.
- **المراجعة:** جلسةُ التنفيذ أجرت **`Structured self-review`** فقط — **وهي ليست مراجعة مستقلة** ولا تستوفي `ADR-0033` بند 10-(ج) ولا `OD-GOV-MERGE-1` §(د)-3.
- next step: **مراجعة مستقلة** على الرأس النهائي (جلسة لم تكتب ولم تعدّل هذه الدفعة) ⇒ **`APPROVE`** ⇒ **Merge Agent مستقل** (جلسة ثالثة ليست المؤلف ولا المراجع) يطابق **نصّ إيصال الدمج المثبَّت** في `OD-R3-CONTRACTS-2` §(هـ) **قبل** التنفيذ ثم يدمج، ثم **تحقُّق قراءةً فقط بعد الدمج** بلا أي تحديث مستودعي لاحق (‏ADR-0033 بند 12). **ولا يجوز لوكيل التنفيذ الذي كتب هذه الدفعة مراجعتُها ولا دمجُها.** **ولم يبدأ أي Workstream لاحق، ولم تُفتح دفعةٌ لـ`admin.workflow_detail`.**
- do not touch: constitution.md · AUTHORITY.md · methodology/** · phases/** · ui/** (‏ومنها `UI_SCREEN_INVENTORY.md` و`UI_SCREEN_BEHAVIOR_CARDS.md` و`UI_DESIGN_SYSTEM.md` §9) · decisions/adr/** · catalogs/** · traceability/** · aql/** · `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` · `contracts/NAMING_AND_CONTRACTS_STANDARD.md` · `contracts/screens/run.list.md` · `contracts/screens/admin.actions.md` · **`contracts/screens/admin.workflow_detail.md` (غير موجود — لا يُنشأ)** · `contracts/identity/**` · `contracts/enums/**` · **`contracts/fields/**` (غير موجود — لا يُنشأ)** · **أي وسم أو إصدار** · **أي سجل تفعيل `R4` أو `R5`** · **إعدادات المستودع وحماية الفروع وCI** · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.4 · **H-0016..H-0035**.

## Handoff H-0037
> **‏R3 — `DD-WF-ALLOC` Determination · Behavior Card 25 · Contract Ripple Alignment.** يُقرأ بعد `H-0036` **ولا ينسخه ولا يعيد كتابته**: `H-0036` صحيحٌ في تاريخه وقد سجّل مواءمة عقدَي `admin.record_types` و`admin.workflows` مع القالب v1.1 (‏PR #18) **مع إبقاء تنازع إسناد أفعال الـWorkflow مسجَّلاً غير محسوم**؛ **وهذه الجولة تحسم ذلك التنازع بقرار مالك وتستهلكه ارتداداً**. **لا تغيير في `FP-0001` ولا في التجميد ولا في جرد `P3` ولا في أي مخرج مجمَّد.**
> **تحقُّق ترقيم:** ‏`H-0037` **غير مستعمَل** في السجل عند تحرير هذا المدخل — تحقُّقاً من الملف لا افتراضاً؛ و`H-0016`..`H-0036` **لم تُمسّ**.

- date: 2026-08-06 (‏**تاريخ التنفيذ**) · **تاريخ القرار الحاكم: 2026-08-05** — ولذلك تحمل أسطر الـΔ في الأوعية تاريخَ القرار
- phase: **R3 — Workflow Surface Allocation · `DD-WF-ALLOC`** — فرع جديد `docs/r3-wf-alloc-card25` من `BASE_SHA` مباشرة · **PR غير مدموج**
- task/goal: تنفيذ **قرار المالك `OD-R3-WF-ALLOC-1`**: تخصيص `wf.approve`/`wf.activate`/`wf.rollback` إلى **`admin.workflow_detail`** · **توزيع الصلاحيتين بلا جمع ولا اختراع** · إنشاء **بطاقة السلوك 25** بالطقم العشري ومعرّفات أسطحها السبعة داخل نقاطها (**استثناء محصور ببطاقة 25 وحدها**) · مواءمة **بطاقة 13** · **ارتداد عقد `admin.workflows`** (`0.2 ⇒ 0.3`، **`Candidate` بلا تغيير**). **لا merge · لا tag · لا release · لا rebase · لا amend · لا force-push · لا حذف فرع · لا تعديل إعدادات مستودع ولا CI · لا رفع تجميد · لا فكّ حجب `FP-0001` · لا تفعيل `R4`/`R5` · لا إغلاق `R3` · لا اختبارات ولا CI.**
- base SHA: **`origin/main` = `0d46d71d372e0f5458a0621578b743a6139c7bbb`** — **مطابقٌ حرفياً** للـSHA المثبَّت في أمر المالك، و`HEAD` عند إنشاء الفرع **مطابقٌ له قبل أي تعديل**.
- **خطية الفرع:** أُنشئ من `BASE_SHA` مباشرة · **commit واحد ذرّي** بأبٍ واحد · **صفر merge commit** · بلا rebase ولا amend ولا force-push.
- **نموذج الدفعة:** **`ONE_ATOMIC_COMMIT`** — سجلّ القرار وبطاقة 25 ومواءمة بطاقة 13 وارتداد العقد والفهرس والـhandoff **في commit واحد**. **ويُمنع أي commit جزئي** (سجلّ القرار وحده، أو `ui/**` وحدها، أو ارتداد العقد وحده) لأنه يترك SHA وسيطة غير متسقة مع بقية الأوعية.

**التحقق من الأساس قبل أي كتابة — نتائجه:**

| الفحص | النتيجة |
|---|---|
| `origin/main` = ‏`BASE_SHA` | **مطابق** — `0d46d71d372e0f5458a0621578b743a6139c7bbb` |
| `git status --short` قبل التعديل | **فارغ** |
| `HEAD` بعد إنشاء الفرع وقبل أي تعديل | **مطابق لـ`BASE_SHA`** |
| **التجميد** | **`OD-FP-0001-FREEZE` = `ACTIVE`** — بلا مساس |
| **`FP-0001`** | **`BLOCKED`** — بلا مساس |
| **`R3`** | **`ACTIVE — SPECIFICATION ONLY`** — **لم تُغلق** |
| **`R4` / `R5`** | **`NOT_ACTIVATED`** — بلا مساس |
| **`contracts/screens/admin.workflow_detail.md`** | **غير موجود قبل الدفعة وبعدها** — **لم يُنشأ** |
| **نمط تأكيد rollback** | **صفر ورود** لنصٍّ حاكم يربط `typed`/`dual`/`simple` بـrollback في `ui/**` و`contracts/**` و`phases/**` و`decisions/**` و`catalogs/**` و`methodology/**` |

- completed: `ui/UI_SCREEN_BEHAVIOR_CARDS.md` (‏1.1 ⇒ **1.2**: +بطاقة 25 · مواءمة أربع نقاط في بطاقة 13 وقائمة حالاتها · الترويسة 24 ⇒ 25 شاشة) · `ui/UI_ADMIN_CONSOLE_MODEL.md` (‏1.1 ⇒ **1.2**: شقّ §4-D بندين) · `ui/UI_SCREEN_CARDS_BY_PHASE.md` (‏1.0 ⇒ **1.1**: شقّ صفّ Phase 3 صفّين — **`Proposed` بلا تغيير**) · `contracts/screens/admin.workflows.md` (‏0.2 ⇒ **0.3**: الترويسة · §2 · §3 · §3-أ · §3-ب · §3-ج · §3-د · §3-هـ · §4 · §4-أ · §5 · §7-أ · §8 · Related) · `decisions/open-decisions.md` (‏3.8 ⇒ **3.9**: +`OD-R3-WF-ALLOC-1` بتسعة أقسام فرعية + **إلحاق** سطرين مؤرَّخين بـ`OD-R3-CONTRACTS-2`) · `handoff/handoff.md` (هذا المدخل) · `INDEX.md` (**ستة صفوف قائمة محدَّثة — بلا صفّ جديد**).
- **`surfaces[]` — الأثر:** ‏`admin.workflows` = **`PAGE`×1 · `DRAWER`×2 · `DIALOG`×1 = أربعة** (كان **سبعة**). الخارجة إلى بطاقة 25: `drawer_version_diff` · `dialog_workflow_approval` · `dialog_workflow_activation`. **والباقية أربعة**: `page_definitions_list` · `drawer_validation_report` · `drawer_definition_audit_chain` (يستوفي `S15` للقائمة — **لم يُنقل**) · `dialog_version_conflict` (يستوفي `S20` على القائمة — **لم يُنقل**).
- **بطاقة 25 — المعرّفات السبعة داخل نقاطها:** `page_workflow_detail` (جديد) · `drawer_version_diff` (منقول) · `drawer_workflow_detail_audit_chain` (جديد — استيفاء مستقل لـ`S15`) · `dialog_workflow_approval` (منقول · `typed`) · `dialog_workflow_activation` (منقول · `typed`) · `dialog_workflow_rollback` (جديد · **تأكيد صريح بلا وسم نمط**) · `dialog_workflow_detail_version_conflict` (جديد — استيفاء مستقل). **بلا حقل حادي عشر وبلا تغيير لأسماء النقاط العشر**، و**الإدراج استثناءٌ محصورٌ ببطاقة 25 وحدها** — منصوصٌ عليه حرفياً في `OD-R3-WF-ALLOC-1` §(ح).
- not completed: **`contracts/screens/admin.workflow_detail.md` لم يُنشأ** · **العقد يبقى `Candidate`** ولا ترقية ولا ادّعاء ترقية · **المرتبة 5 تبقى خالية فعلياً** و`OD-GOV-2` مفتوح · **`ui/UI_SCREEN_INVENTORY.md` لم يُمسّ** · **`OD-P3-1` و`OD-P3-2` (ومعه `CC-WF-1`) و`OD-P3-3` بلا حسم** · **لا سياسة instances عند rollback** · **`CC-WF-2`/`CC-WF-3` بوجهتهما `R5`** · **`DD-WF-ACTION-CATALOG` و`DD-WF-STATUS-LIFECYCLE` و`DD-WF-CONTROL-ID` و`DD-WF-FIELDS` و`DD-WF-APPROVAL-PATH` و`DD-WF-A11Y-ENFORCEMENT` و`DD-RT-SIBLING-SCREENS` مفتوحة** · **`DD-WF-FOCUS-RETURN` تحوّل ولم يُغلق** · **لا معيار `R3-A11Y-01`..`07` أُعلن `PASS`** · **`contracts/fields/` لم يُنشأ** · **`contracts/enums/**` و`contracts/identity/**` والقالب لم تُمسّ** · **لا `UI-4` ولا `UI-5`** · **لا Rendering Topology ولا Authoring Provenance** · **لا Rocket/aql** · **التجميد لم يُرفع** · **`FP-0001` = `BLOCKED`** · **`R4` = `NOT_ACTIVATED`** و`R5` لم تُفعَّل · **`R3` لم تُغلق** · **لا اختبار بُني ولا نُفِّذ** · **لا وسم ولا إصدار ولا دمج**.
- files changed: **سبعة** — `ui/UI_SCREEN_BEHAVIOR_CARDS.md` · `ui/UI_ADMIN_CONSOLE_MODEL.md` · `ui/UI_SCREEN_CARDS_BY_PHASE.md` · `contracts/screens/admin.workflows.md` · `decisions/open-decisions.md` · `handoff/handoff.md` · `INDEX.md`. **ولم يُنشأ ملف جديد ولم يُحذف** ⇒ **لا صفّ جديد في `INDEX.md`** والإجمالي **158 ملفاً + الفهرس** بلا تغيير · **EC-3 = 159/159**.
- decisions: **قرار مالك واحد جديد** = **`OD-R3-WF-ALLOC-1`** (‏`RESOLVED BY OWNER DECISION`) — يحسم `DD-WF-ALLOC` وحده. **لا ADR · لا قرار معماري · لا إعادة ترقيم لأي `OD` قائم · لا تغيير لحالة أي `OD` آخر · ولم تُنشأ طبقة سلطة جديدة.**
- risks: (1) **قراءة إدراج المعرّفات داخل بطاقة 25 قاعدةً عامة** — مُعالَج بنصّ `F1` حرفياً في `OD-R3-WF-ALLOC-1` §(ح) وفي ترويسة ملف البطاقات: **استثناء محصور ببطاقة 25 وحدها**. (2) **قراءة سلسلتَي التدقيق وحوارَي نزاع الإصدار تكراراً محظوراً** — مُعالَج بالمبدأ في §(ج): **استيفاء حالةٍ مستقلٌّ عبر شاشتَي `Builder`**. (3) **قراءة انتقال الـgrandfathering إذناً باشتقاق سلوك rollback أو بحسم `OD-P3-3`** — مُعالَج بقيدٍ صريح في §(ز) وفي بطاقة 25 («لا سياسة instances»). (4) **اشتقاق نمط تأكيدٍ لـrollback من أحد الأفخاخ الثلاثة** — مُعالَج بجدول الأفخاخ في §(و) وبفحصٍ مُثبَت بصفر ورود. (5) **قراءة شقّ صفّ Phase 3 تفعيلاً للمرحلة** — مُعالَج بنصّ الترويسة: **`Proposed` بلا تغيير ولا صياغة تفعيل**. (6) **قراءة حسم `DD-WF-ALLOC` إغلاقاً لـ`DD-WF-FOCUS-RETURN`** — مُعالَج بعلّةٍ محدَّثة في §7-أ من العقد وفي §(ط)-8: **يتحوّل ولا يُغلق**.
- tests: راجع تقرير الدفعة — بوابات `G0` · `G0-b` · `G1` · `G1-b` · `G2`..`G13` بمخرجاتها، والبيانات القرائية الثمانية ومنها **`ZERO EC-11`**.
- **المراجعة:** جلسةُ التنفيذ أجرت **`Structured self-review`** فقط — **وهي ليست مراجعة مستقلة** ولا تستوفي `ADR-0033` بند 10-(ج) ولا `OD-GOV-MERGE-1` §(د)-3.
- next step: **مراجعة مستقلة** على الرأس النهائي (جلسة لم تكتب ولم تعدّل هذه الدفعة) ⇒ **`APPROVE`** ⇒ **Merge Agent مستقل** (جلسة ثالثة ليست المؤلف ولا المراجع) **بأمر مالك صريح منفصل**. **ولا يجوز لوكيل التنفيذ الذي كتب هذه الدفعة مراجعتُها ولا دمجُها.** **ولم تُفتح دفعةٌ لعقد `admin.workflow_detail`** — تأليفُه يبقى محجوباً حتى دمج بطاقة 25 وأمرِ مالك مستقل.
- do not touch: constitution.md · AUTHORITY.md · methodology/** · phases/** · **`ui/UI_SCREEN_INVENTORY.md` (قراءةً فقط — لا يُمسّ)** · `ui/UI_DESIGN_SYSTEM.md` §9 · بقية `ui/**` خارج الثلاثة المأذونة · decisions/adr/** · catalogs/** · traceability/** · aql/** · `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` · `contracts/NAMING_AND_CONTRACTS_STANDARD.md` · `contracts/screens/run.list.md` · `contracts/screens/admin.actions.md` · `contracts/screens/admin.record_types.md` · **`contracts/screens/admin.workflow_detail.md` (غير موجود — لا يُنشأ)** · `contracts/identity/**` · `contracts/enums/**` · **`contracts/fields/**` (غير موجود — لا يُنشأ)** · **أي وسم أو إصدار** · **أي سجل تفعيل `R4` أو `R5`** · خط الأساس المجمَّد `188ad37` · الوسوم v1.0..v1.4 · **H-0016..H-0036**.

**‏Δ 2026-08-06 — جولة تصحيح داخل PR #19: استكمال سجلّ ما قبل الدمج (‏`ADR-0033` بند 11) — لا مدخل handoff جديد**

- **ما اكتُشف:** مراجعةُ حوكمةٍ مستقلة كشفت **نقصاً في سجلّ ما قبل الدمج**: الدفعة لم تُثبِّت حقولَ أثر الدمج السابقة للدمج ولا نصَّ رسالة الـMerge Commit المتوقَّعة، فلم تستوفِ **`ADR-0033` بند 10-(ز) وبند 12** ولا **`methodology/agent-execution-model.md` §18.2-8**.
- **ما استُكمل:** أُلحق **§(ي)** داخل `OD-R3-WF-ALLOC-1` يحمل **السجل الحاكم السابق للدمج لـPR #19** بحقوله كاملةً + **نصّ رسالة الـMerge Commit المتوقَّعة مثبَّتاً حرفياً** + **قواعد المطابقة** نفسها المستعملة في سجلّ PR #18 (‏توحيد نهايات الأسطر إلى `LF` · حذف المسافات الطرفية · حذف الأسطر الفارغة الزائدة في البداية والنهاية · لا اختلاف في الكلمات ولا في ترتيب الأسطر · **أي اختلاف بعد التطبيع ⇒ `MERGE RECEIPT MISMATCH` ⇒ لا دمج**). **ولا يُضاف `Authorized head` إلى الرسالة** — الرأس النهائي يُثبَت من **الأب الثاني للـMerge Commit**.
- **مصادقة المالك على الانحراف:** صادق المالك على **التعديل المحدود لصفّ `DD-WF-DETAIL-SCREEN`** في §7-أ من عقد `admin.workflows` — لأن النصّ السابق كان سيصبح **كاذباً داخل الدفعة نفسها** بعد إنشاء بطاقة السلوك 25. **`DEVIATION_RATIFIED=YES` · `PROCEDURAL_EXCEPTION=ACCEPTED_THIS_ROUND_ONLY` · `GENERAL_PRECEDENT=NO` · `REWORK_ON_FUNCTIONAL_CONTENT=NO`.** والقيودُ نافذة بلا تخفيف: **العقد لم يُنشأ · تأليفُه يحتاج أمر مالك مستقلاً · بطاقة 25 ترفع مانعَ غياب مصدر الاشتقاق فقط ولا تأذن بالتأليف · ولم يُنشأ معرّف ولا صلاحية ولا مسار ولا توسّع في النطاق**. **وفي الجولات اللاحقة يجب على المنفّذ `STOP` عند اكتشاف تعارضٍ حاكمٍ غير مغطّى ما لم يمنحه الأمرُ تفويضاً صريحاً ومحدوداً بالتصحيح.**
- **أثر التصحيح على أهلية الرأس:** **الرأس السابق `291365262dd8818ec3976d2dc950ce29d02f7313` لم يعد مؤهلاً للدمج** بعد صدور commit التصحيح. **والرأس الجديد يحتاج مراجعةً مستقلة كاملة**، **ولا تأذن نتيجةُ أي مراجعة سابقة بدمجه** (‏`ADR-0033` بند 11 + استثناء دورة التصحيح: **لا يُدمج رأسٌ لم يحصل هو نفسه على `APPROVE`**).
- **فصل الأدوار:** **Merge Agent يجب أن يكون جلسةً مستقلة لم تؤلّف الحزمة ولا محتوى الـPR ولا هذا التصحيح، ولم تراجعه** (‏`agent-execution-model` §18.2-1). **ووكيلُ التنفيذ الذي كتب الدفعة والتصحيح لا يراجعهما ولا يدمجهما.**
- **نموذج الـcommit بعد التصحيح:** الـcommit الوظيفي الأصلي **يبقى ذرّياً واحداً**، ويُضاف **commit تصحيحي حاكم واحد فقط** ⇒ **`EXPECTED_PR_COMMIT_COUNT=2`**. **بلا amend ولا rebase ولا force-push ولا squash ولا حذف فرع ولا PR جديد.**
- **نطاق التصحيح المغلق:** ثلاثة ملفات فقط — `decisions/open-decisions.md` · `handoff/handoff.md` · `INDEX.md`. **ولم يُمسّ `ui/**` ولا `contracts/**` ولا `methodology/**` ولا `decisions/adr/**`، ولم تُمسّ بطاقتا السلوك 13 و25 ولا عقد `admin.workflows`، ولم يُنشأ `Decision ID` ولا `Handoff ID` جديد، ولا ملف جديد ولا حذف.**
- **الحالة الحاكمة بلا مساس:** **لا دمج · لا وسم · لا إصدار · ولا إغلاق لـ`R3` في هذه الجولة** · **`FP-0001` `BLOCKED`** · **التجميد `ACTIVE` وشروط الرفع بلا تعديل ولا إعادة عدّ** · **`R4`/`R5` `NOT_ACTIVATED`** · `INDEX.md` **بلا صفّ جديد وبلا تغيير في الإجمالي** (‏158 + الفهرس · **EC-3 = 159/159**).
