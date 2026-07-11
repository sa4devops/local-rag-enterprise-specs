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
