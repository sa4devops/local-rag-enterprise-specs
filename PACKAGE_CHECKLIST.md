# PACKAGE_CHECKLIST.md — Final GitHub Package Checklist

> **Version:** 1.10 (… + إغلاق F-3 + **دفعة تنحية Flutter وجسر Open WebUI المؤقت**) · **Status:** Current · **Date:** 2026-07-11
>  **Purpose:** خريطة الحزمة النهائية: كل ملف، مساره، حالته، جاهزيته للرفع، وما يلزم قبل **التنفيذ** (لا قبل الرفع).

| الملف | المسار داخل GitHub | الحالة | جاهز للرفع؟ | يحتاج قراراً قبل التنفيذ؟ |
|---|---|---|---|---|
| README.md | `/README.md` | **v1.2** — سطر الهوية + حالة المشروع عند خط الأساس v1.0 | ✅ | لا |
| vision.md | `/vision.md` | v1.0 + سطر الهوية المعتمدة (v1.0-baseline) | ✅ | لا |
| constitution.md | `/constitution.md` | **v1.1** — +م21 (خط الأساس المعماري) +م22 (القدرات المستقبلية التزامات) — v1.0-baseline | ✅ | لا |
| PACKAGE_CHECKLIST.md | `/PACKAGE_CHECKLIST.md` | **v1.8** — مضاف إليه v0.7.1 + دفعة v0.8 + إغلاق خط الأساس v1.0 | ✅ | لا |
| github-docs-structure.md | `/github-docs-structure.md` | **v1.7** — FIX-9 (v0.8) + ملفات ADR الفردية المزروعة (v1.0-baseline) | ✅ | لا |
| Feature_Technical_Architecture_Catalog.md | `/catalogs/…` | **v2.1** — D1–D9 مدمجة (§2 + §3.1/3.3/3.8 + §5 + §15) | ✅ | لا |
| Spec_Driven_Modular_Monolith_Methodology.md | `/methodology/…` | **v2.1** — عقود shared + §16/§17 + D8 | ✅ | لا |
| coding-standards.md | `/methodology/coding-standards.md` | **v1.2** — §9 وفق D12 (معايير الحكم + سجل المراجع) | ✅ | تثبيت إصدارات Python/Node عند بدء التنفيذ |
| testing-strategy.md | `/methodology/testing-strategy.md` | **v1.1** — +Provider-Equivalence +Logging/Error-Contract | ✅ | لا |
| open-decisions.md | `/decisions/open-decisions.md` | **v2.3** — +قسم إغلاق خط الأساس (قرارات مُغلقة بمراجع ADR · قيم تشغيلية · OD-IDX-1) | ✅ | هو ذاته سجل بوابات التنفيذ |
| license-review.md | `/decisions/license-review.md` | **v1.2** — SeaweedFS افتراضي الإنتاج · MinIO مشروط · Valkey افتراضي التوسع · Redis مقفل · إصدارات P0 في lockfiles · سياسة D12 | ✅ | **نعم:** إقرار صفوف الستاك قبل أول كود؛ الفئة 3 عند تفعيل صورة اختيارية |
| adr/README.md | `/decisions/adr/README.md` | **v1.2** — سياسة D15 كاملة + السجل الكنسي **ADR-0001..0028** + روابط الملفات المزروعة | ✅ | لا |
| phase-roadmap.md | `/phases/phase-roadmap.md` | **v1.1** — بوابات P0/P5 محدّثة + بند D1–D9 | ✅ | لا |
| phases/README.md | `/phases/README.md` | v1.0 (قواعد المجلد — غير متأثرة) | ✅ | لا |
| phase-0-foundation-full-stack-skeleton.md | `/phases/…` | **v2.1 — Accepted for Design** (C1–C5 مُغلقة؛ FR-0.4/0.9/0.11/0.13 + FR-0.19) | ✅ | **قبل تنفيذها:** صفوف ترخيص الستاك فقط (لا بوابة فئة 3 على P0.4) |
| handoff.md | `/handoff/handoff.md` | H-0001..**H-0010** (آخرها: H-0010 إغلاق خط الأساس v1.0) | ✅ | لا |
| architecture/README.md | `/architecture/README.md` | **v1.3** — +سطر التجميد عند الوسم + مواءمة ADR-0019/0026 (v1.0-baseline) | ✅ | لا |
| Full_Stack_Architecture.svg (+Agent/Deployment) | `/architecture/diagrams/…` | معتمد مفهومياً؛ **التحديث البصري لاحقاً** (النص يحكم الفروق) | ✅ | لا |
| superseded/README.md + 11 أرشيفاً | `/superseded/…` | v1.0 — تاريخية موسومة | ✅ | لا تُستخدم إطلاقاً |
| OSS_REFERENCE_CATALOG.md | `/references/OSS_REFERENCE_CATALOG.md` | v1.0 — Approved OSS reference catalog for AI agents | ✅ | يحتاج تدقيق ترخيص قبل أي استخدام مباشر |
| PHASE_MASTER_PLAN.md | `/phases/PHASE_MASTER_PLAN.md` | v1.0 — Accepted Phase Master Plan ضمن v0.3 — **⚠️ غير موجود في الريبو (Finding F-3 — EXECUTION_REPORT v0.8)؛ رفعه بقرار SA** | ⚠️ | لا — تصميم فقط |
| Phase Design Documents 1–8 | `/phases/designs/phase-1…8-*.md` | v1.0 — Accepted Phase Design Package ضمن v0.3 — **⚠️ غير موجودة في الريبو (Finding F-3)؛ ولا يوجد tag v0.3** | ⚠️ | لا — كل Phase تُفعّل لاحقاً بجلسة مستقلة |
| BACKLOG_DEFERRED_SCOPE.md | `/phases/BACKLOG_DEFERRED_SCOPE.md` | v1.0 — Deferred scope ضمن v0.3 — **⚠️ غير موجود في الريبو (Finding F-3)** | ⚠️ | لا |
| agent-execution-model.md | `/methodology/agent-execution-model.md` | **v1.1** — +§9 مصفوفة القراءة +§10 سلّم الجاهزية +§11 قاعدتا الحراسة (v1.0-baseline) | ✅ | لا |
| UI/UX Planning Package | `/ui/*.md` | v1.0 — Accepted UI/UX Planning Package ضمن v0.4 | ✅ | لا — تصميم/تخطيط فقط، ومخرجات Stitch لاحقاً prototypes/references |
| ui/UI_INTERACTION_MODEL.md | `/ui/UI_INTERACTION_MODEL.md` | v1.0 — Accepted UI Interaction & Visibility Refinement Package ضمن v0.5 | ✅ | لا |
| ui/UI_VISIBILITY_RULES.md | `/ui/UI_VISIBILITY_RULES.md` | v1.0 — Accepted UI Interaction & Visibility Refinement Package ضمن v0.5 | ✅ | لا |
| ui/UI_PROGRESSIVE_DISCLOSURE.md | `/ui/UI_PROGRESSIVE_DISCLOSURE.md` | v1.0 — Accepted UI Interaction & Visibility Refinement Package ضمن v0.5 | ✅ | لا |
| ui/UI_COMPONENT_STATES.md | `/ui/UI_COMPONENT_STATES.md` | v1.0 — Accepted UI Interaction & Visibility Refinement Package ضمن v0.5 | ✅ | لا |
| ui/UI_SCREEN_BEHAVIOR_CARDS.md | `/ui/UI_SCREEN_BEHAVIOR_CARDS.md` | v1.0 — Accepted UI Interaction & Visibility Refinement Package ضمن v0.5 | ✅ | لا |
| ui/UI_STITCH_REFINED_PROMPTS.md | `/ui/UI_STITCH_REFINED_PROMPTS.md` | v1.0 — Accepted UI Interaction & Visibility Refinement Package ضمن v0.5 | ✅ | لا |
| ui/UI_REFINEMENT_GATE_REVIEW.md | `/ui/UI_REFINEMENT_GATE_REVIEW.md` | v1.0 — بوابة قبول حزمة v0.5 | ✅ | لا |
| ui/UI_PROVIDER_MODEL_MANAGEMENT.md | `/ui/UI_PROVIDER_MODEL_MANAGEMENT.md` | v1.0 — Accepted Provider, Model & Run UX Package ضمن v0.6 (+ Patch P-4 مطبَّق) | ✅ | لا |
| ui/UI_RUN_EXECUTION_MODEL.md | `/ui/UI_RUN_EXECUTION_MODEL.md` | v1.0 — Accepted Provider, Model & Run UX Package ضمن v0.6 | ✅ | لا |
| ui/UI_V06_DELTA_AMENDMENTS.md | `/ui/UI_V06_DELTA_AMENDMENTS.md` | v1.0 — سجل Δ v0.6 للتتبع | ✅ | لا |
| ui/UI_V06_GATE_REVIEW.md | `/ui/UI_V06_GATE_REVIEW.md` | v1.0 — بوابة قبول حزمة v0.6 | ✅ | لا |
| **Δ v0.6 على ملفات سابقة** | 12 ملفاً (v0.4 ×7 + v0.5 ×5) | مُستبدلة بنسخها النهائية المعتمدة بعد v0.6 — تفاصيل التغييرات في `ui/UI_V06_DELTA_AMENDMENTS.md` | ✅ | لا |
| architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md | `/architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md` | v0.7 — مواصفة المزوّد/النموذج/السر (Backend — الخيار A) | ✅ | لا |
| methodology/PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md | `/methodology/PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md` | v0.7 — مراجعة التجميع قبل التنفيذ + خطة الدمج | ✅ | لا |
| **Δ v0.7.1 Responsive UI** | 4 ملفات ui (ASSUMPTIONS A-UX-16 · DESIGN_SYSTEM · SCREEN_BEHAVIOR_CARDS · STITCH_REFINED_PROMPTS) | مدموجة في الريبو (commit c6dc18f) وصدر لها release v0.7.1-responsive-ui — **يوثَّق هنا لأول مرة (كان ناقصاً)** | ✅ | لا |
| phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md | `/phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md` | **v1.0 — v0.8**: نصوص FR-3.11/FR-3.12/FR-1.Org-Ext المعتمدة + OD-WF-1/2 وOD-ORG-1 المقفلة — تُدمج في تصميمَي Phase 1/Phase 3 عند توفرهما | ✅ | لا |
| **Δ v0.8 Conversational & Workflow** | 10 ملفات معدَّلة (ASSUMPTIONS A-UX-17 · AI_WORKSPACE §14 · ACTION_BUTTON §2.1 · ADMIN_CONSOLE OD-BLD-1+org · REFERENCE_POLICY · SCREEN_BEHAVIOR_CARDS · SCREEN_INVENTORY v1.3 · FIELD_NAMING · STITCH_PROMPTS G6/G8 · open-decisions) | تفاصيل التغييرات في `EXECUTION_REPORT.md` | ✅ | لا |
| EXECUTION_REPORT.md | `/EXECUTION_REPORT.md` | v1.0 — تقرير تنفيذ دفعة v0.8 (جرد/تدقيق/إصلاحات/بصمات) | ✅ | لا |
| **Δ v1.0 Architecture Baseline Closure** | 14 ملفاً معدَّلاً (constitution م21/م22 · README v1.2 · vision · agent-execution-model v1.1 · coding-standards v1.2 · Methodology §20 · testing-strategy · roadmap · phase-0 · architecture/README v1.3 · open-decisions v2.3 · license-review v1.2 · handoff H-0010 · بوابتا v0.5/v0.6 + تصحيح م2+م16) | تفاصيل الجولة في `BASELINE_CLOSURE_REPORT.md` (خارج المستودع — بيد SA) | ✅ | لا |
| ADR-0004 · ADR-0017 · ADR-0018 · ADR-0019 · ADR-0020 · ADR-0021 · ADR-0022 (ملفات مزروعة) | `/decisions/adr/ADR-00XX-*.md` | v1.0 — زرع الأرقام القائمة بملفات كاملة الحقول العشرة (مع تكميلات D8/D9c/D10/D11/D12/D13/D14 المعتمدة) | ✅ | لا |
| ADR-0023 · ADR-0024 · ADR-0025 · ADR-0026 · ADR-0027 · ADR-0028 (جديدة) | `/decisions/adr/ADR-002X-*.md` | v1.0 — الهوية · ستاك الخادم · عقد REST+OpenAPI+SSE · التغليف والاستخراج · سجلات المزوّدات · سياسة التجميد — كلها Accepted بتاريخ 2026-07-10 | ✅ | لا |
| superseded/phase-design-package-v0.3/ | `/superseded/phase-design-package-v0.3/` | أرشيف الأصل الكامل لحزمة v0.3 (12 ملفاً مجمّدة بايتاً-بايتاً + RESTORE_NOTE ببصمة ZIP) — إغلاق F-3؛ النسخ الحية للملفات العشرة في phases/ بلافتة حالة | ✅ | لا — أرشيف تاريخي |
| ADR-0029 · ADR-0030 (Δ 2026-07-11) | `/decisions/adr/ADR-0029…-0030….md` | v1.0 — مبدأ العميل القابل للاستبدال (ترقية الدستور مشروطة باختبار الاستبدال) · Open WebUI واجهة محادثة مؤقتة (بوابات + خروج) — Accepted | ✅ | تفعيل الواجهة المؤقتة: اعتماد صف ترخيص الصورة أولاً |
| PROJECT_EVOLUTION.md | `/PROJECT_EVOLUTION.md` | v1.0 — فهرس سردي يشير للمصادر الرسمية؛ ليس مصدر حقيقة ثانياً | ✅ | لا |
| FLUTTER_ROLLBACK_AND_OPENWEBUI_BRIDGE_HANDOFF.md | `/FLUTTER_ROLLBACK_AND_OPENWEBUI_BRIDGE_HANDOFF.md` | v1.0 — تقرير الدفعة (جرد/نسخ أمان/تصنيفات الحالة الست) | ✅ | لا |


**تُنشأ لاحقاً (ليست نقصاً):** ملفات المعمارية المستخرجة · ملفات ADR الفردية · handoff/archive · runbooks · prototypes/design-notes الناتجة من Google Stitch بعد مراجعتها.

**خلاصة الجاهزية:** لا قرار يمنع **الرفع**. قبل **التنفيذ**: إقرار صفوف ترخيص الستاك المعتمد فقط. **بوابة compose (فئة 3)** تنطبق حصراً عند **تفعيل** صورة اختيارية (Valkey / MinIO أو SeaweedFS / خادم مراقبة). قبل **مرحلة الوسائط**: OCR/PDF-tooling/ffmpeg/أوزان النماذج. قبل **الإنتاج/التوزيع**: فئة 4 كاملة.
