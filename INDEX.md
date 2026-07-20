# INDEX.md — الفهرس البشري الحاكم لمستودع المواصفات

> **Version:** 1.0 — Proposed (دفعة G1) · **Date:** 2026-07-19 · **الموضع:** `/INDEX.md`
> **Authority:** مصدر الفهرسة الحاكم بقرار **OD-IDX-1** (‏SA ‏2026-07-10): فهرس **بشري القراءة يدوي الصيانة** — لا index.yaml ولا manifest آلياً ولا مصدر موازياً حتى وجود مستهلك آلي فعلي وقرار جديد (‏ADR-0035 بند 7). الفهرس **دليل مواضع وحالات، لا مصدر سلطة** (‏AUTHORITY.md §2-4).
> **قاعدة الصيانة:** كل دفعة تضيف/ترقّي ملفاً تُحدّث صفه هنا في الدفعة ذاتها (بند write-back) · التغطية إلزامية 100% لكل ملفات ‏.md (‏EC-3).

| المجلد | الملف | الإصدار | الحالة | المالك النطاقي | من يقرأ |
|---|---|---|---|---|---|
| `(الجذر)` | `AUTHORITY.md` | 1.0 — Proposed (يُعتمد بتوقيع/دمج SA في بوابة G1) | Proposed (G1) | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |
| `(الجذر)` | `EXECUTION_REPORT.md` | 1.0 | Current | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |
| `(الجذر)` | `FLUTTER_ROLLBACK_AND_OPENWEBUI_BRIDGE_HANDOFF.md` | 1.0 | Current | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |
| `(الجذر)` | `PACKAGE_CHECKLIST.md` | 1.11 — (Δ 2026-07-19 دفعة G1: +قسم أصول Governance Foundatio | Current | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |
| `(الجذر)` | `PROJECT_EVOLUTION.md` | 1.0 | Current | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |
| `(الجذر)` | `README.md` | 1.3 — (Δ 2026-07-19 G1: +AUTHORITY قراءةً وإحالةَ سلطةٍ + ستاك ADR-0031) | Current / Accepted | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |
| `(الجذر)` | `SPECIFICATIONS_CLOSEOUT_HANDOFF.md` | 1.0 | Current | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |
| `architecture` | `architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md` | 1.0 — Proposed (v0.7) | Proposed (G1) | المعمارية — Specification Architect | مصمم المرحلة المعنية |
| `architecture` | `architecture/README.md` | 1.3 (v1.0-baseline: +سطر التجميد عند الوسم + مواءمة ADR-0019 | Current / Accepted | المعمارية — Specification Architect | مصمم المرحلة المعنية |
| `catalogs` | `catalogs/Feature_Technical_Architecture_Catalog.md` | 2.1 — Final (A1–A11 + قرارات ما قبل التنفيذ D1–D9 مدمجة) | Current / Accepted | المعمارية — Specification Architect | حسب تسمية تصميم المرحلة |
| `(الجذر)` | `constitution.md` | 1.2 (+م23 العميل القابل للاستبدال — دفعة إغلاق المواصفات، قر | Current / Accepted | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |
| `contracts` | `contracts/NAMING_AND_CONTRACTS_STANDARD.md` | — | Proposed (G1) | العقود — Specification Architect | كل منفذ وكل بوابة |
| `contracts/enums` | `contracts/enums/ENUMS_DICTIONARY.md` | — | Proposed (G1) | العقود — Specification Architect | كل منفذ واجهة |
| `contracts/identity` | `contracts/identity/RECORD_IDENTITY.md` | — | Proposed (G1) | العقود — Specification Architect | كل منفذ |
| `contracts/screens` | `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` | — | Proposed (G1) | العقود — Specification Architect | منفذ الشاشة وبوابتها |
| `contracts/screens` | `contracts/screens/admin.actions.md` | — | Candidate | العقود — Specification Architect | منفذ الشاشة وبوابتها |
| `contracts/screens` | `contracts/screens/admin.record_types.md` | — | Candidate | العقود — Specification Architect | منفذ الشاشة وبوابتها |
| `contracts/screens` | `contracts/screens/admin.workflows.md` | — | Candidate | العقود — Specification Architect | منفذ الشاشة وبوابتها |
| `contracts/screens` | `contracts/screens/run.list.md` | — | Candidate | العقود — Specification Architect | منفذ الشاشة وبوابتها |
| `decisions` | `decisions/DEFERRED_IMPLEMENTATION.md` | 1.0 | Current | طبقة القرارات — SA | ‏Tier-0 لكل وكيل |
| `decisions/adr` | `decisions/adr/ADR-0004-search-architecture-postgres-qdrant-opensearch.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0017-frontend-stack-react-vite-typescript.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0018-cache-queue-lock-valkey-scale-profile.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0019-object-storage-seaweedfs-production-default.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0020-observability-audit-logs-baseline.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0021-reference-aware-clean-implementation.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0022-github-development-airgapped-delivery.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0023-enterprise-ai-platform-progressive-implementation.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0024-backend-stack-python-fastapi.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0025-api-contract-rest-openapi-sse.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0026-module-boundaries-packaging-extraction.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0027-provider-capability-registry-architecture.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0028-architecture-baseline-frozen.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0029-replaceable-client-principle.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0031-primary-ui-client-nextjs-client-only-rocket.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0032-dynamic-records-hybrid-storage-uuidv7.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0033-automation-levels-git-merge-policy.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0034-development-skills-superpowers-subset.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0035-contracts-layer-single-source.md` | — | Proposed (G1) | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/ADR-0036-repo-visibility-public-temporary-private-gate.md` | — | Current | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions/adr` | `decisions/adr/README.md` | 1.3 — (Δ 2026-07-19 دفعة G1: +صفوف ADR-0031..0036 ‏Proposed  | Current / Accepted | طبقة القرارات — SA | كل وكيل عند مساس معماري |
| `decisions` | `decisions/license-review.md` | 1.2 (v1.0-architecture-baseline: صفوف SeaweedFS/MinIO/Valkey | Current / Accepted | طبقة القرارات — SA | ‏Tier-0 لكل وكيل |
| `decisions` | `decisions/open-decisions.md` | 2.4 — (Δ 2026-07-19: +فهرس دفعة G1 — Governance Foundation B | Current / Accepted | طبقة القرارات — SA | ‏Tier-0 لكل وكيل |
| `(الجذر)` | `github-docs-structure.md` | 1.7 (v1.0-baseline: ملفات ADR الفردية المزروعة تحت decisions | Current / Accepted | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |
| `handoff` | `handoff/handoff.md` | 1.1 (Δ 2026-07-11: توضيح اتفاقية الأرشفة وترتيب القراءة — تح | Current / Accepted | التسليم — كل جلسة منفِّذة | الوكيل التالي قبل أي عمل |
| `knowledge` | `knowledge/BUSINESS_GLOSSARY.md` | 0.1 — Seed/Proposed | Proposed (G1) | ‏System Knowledge — Specification Architect | المولد + المراجعات |
| `methodology` | `methodology/PHASE_EXECUTION_STANDARD.md` | 1.0 — Proposed (يُعتمد بتوقيع/دمج SA في بوابة G1) | Proposed (G1) | المنهجية — Specification Architect | كل وكيل تنفيذ |
| `methodology` | `methodology/PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md` | 1.0 — Proposed (v0.7) | Proposed (G1) | المنهجية — Specification Architect | كل وكيل تنفيذ |
| `methodology` | `methodology/ROCKET_OPERATING_MODEL.md` | 1.0 — Proposed (يُعتمد بتوقيع/دمج SA في بوابة G1) | Proposed (G1) | المنهجية — Specification Architect | كل وكيل تنفيذ |
| `methodology` | `methodology/Spec_Driven_Modular_Monolith_Methodology.md` | 2.1 — Final (A1–A11 + D1–D9 مدمجة) | Current / Accepted | المنهجية — Specification Architect | كل وكيل تنفيذ |
| `methodology` | `methodology/agent-execution-model.md` | 2.0 — (Δ 2026-07-19 دفعة G1: +§§12–17 — الأدوار الأربعة | Current | المنهجية — Specification Architect | كل وكيل تنفيذ |
| `methodology` | `methodology/coding-standards.md` | 1.2 — Final (D1–D9 مدمجة + §9 مُحدَّث وفق D12 في v1.0-archit | Current / Accepted | المنهجية — Specification Architect | كل وكيل تنفيذ |
| `methodology` | `methodology/testing-strategy.md` | 1.1 (+Provider-Equivalence وLogging-Contract) | Current / Accepted | المنهجية — Specification Architect | كل وكيل تنفيذ |
| `phases` | `phases/BACKLOG_DEFERRED_SCOPE.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Proposed (G1) | المراحل — Specification Architect | عند العمل على مرحلة |
| `phases` | `phases/PHASE_MASTER_PLAN.md` | 1.0 — Proposed (تصبح Accepted باعتماد المالك ضمن إصدار v0.3- | Proposed (G1) | المراحل — Specification Architect | عند العمل على مرحلة |
| `phases` | `phases/README.md` | 1.1 (Δ اتساق 2026-07-11: تحديث «الموجود الآن» و«الحالة الحال | Current / Accepted | المراحل — Specification Architect | عند العمل على مرحلة |
| `phases/designs` | `phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md` | 1.0 — Accepted (SA — 2026-07-10 | Current | المراحل — Specification Architect | عند تفعيل المرحلة |
| `phases/designs` | `phases/designs/phase-1-governed-core-screen-builder.md` | 1.0 — Proposed (تصبح **Accepted for Design** باعتماد v0.3) | Proposed (G1) | المراحل — Specification Architect | عند تفعيل المرحلة |
| `phases/designs` | `phases/designs/phase-2-advanced-screens-records-entity-profile.md` | 1.0 — Proposed (تصبح Accepted باعتماد v0.3) | Proposed (G1) | المراحل — Specification Architect | عند تفعيل المرحلة |
| `phases/designs` | `phases/designs/phase-3-workflows-approvals-actions.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Proposed (G1) | المراحل — Specification Architect | عند تفعيل المرحلة |
| `phases/designs` | `phases/designs/phase-4-advanced-permissions-feature-management.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Proposed (G1) | المراحل — Specification Architect | عند تفعيل المرحلة |
| `phases/designs` | `phases/designs/phase-5-files-rag-ocr-media.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Proposed (G1) | المراحل — Specification Architect | عند تفعيل المرحلة |
| `phases/designs` | `phases/designs/phase-6-gateway-agents-sql-chat-reports.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Proposed (G1) | المراحل — Specification Architect | عند تفعيل المرحلة |
| `phases/designs` | `phases/designs/phase-7-integrations-app-store.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Proposed (G1) | المراحل — Specification Architect | عند تفعيل المرحلة |
| `phases/designs` | `phases/designs/phase-8-monitoring-offline-production.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Proposed (G1) | المراحل — Specification Architect | عند تفعيل المرحلة |
| `phases` | `phases/phase-0-foundation-full-stack-skeleton.md` | 2.1 — Final (A3/A8 + D1–D9 مدمجة؛ C1–C5 وC8 مُغلقة) | Current / **Accepted for Design** (التنف | المراحل — Specification Architect | عند العمل على مرحلة |
| `phases` | `phases/phase-roadmap.md` | 1.1 (D1–D9 مدمجة) | Current / Accepted | المراحل — Specification Architect | عند العمل على مرحلة |
| `references` | `references/OSS_REFERENCE_CATALOG.md` | — | Current | المراجع — Specification Architect | بتكليف صريح |
| `superseded` | `superseded/Feature_Technical_Architecture_Catalog-v1.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded` | `superseded/Phase-0-Prompt.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded` | `superseded/Phase-1-Prompt.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded` | `superseded/README.md` | 1.0 | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded` | `superseded/Spec_Driven_Modular_Monolith_Methodology-v1.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded` | `superseded/full-architecture-study-v1.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded` | `superseded/open-decisions-v1.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded` | `superseded/phase-0-design-v1.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3` | `superseded/phase-design-package-v0.3/README.md` | 1.0 | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3` | `superseded/phase-design-package-v0.3/RESTORE_NOTE.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/methodology` | `superseded/phase-design-package-v0.3/methodology/agent-execution-model.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases` | `superseded/phase-design-package-v0.3/phases/BACKLOG_DEFERRED_SCOPE.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases` | `superseded/phase-design-package-v0.3/phases/PHASE_MASTER_PLAN.md` | 1.0 — Proposed (تصبح Accepted باعتماد المالك ضمن إصدار v0.3- | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases/designs` | `superseded/phase-design-package-v0.3/phases/designs/phase-1-governed-core-screen-builder.md` | 1.0 — Proposed (تصبح **Accepted for Design** باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases/designs` | `superseded/phase-design-package-v0.3/phases/designs/phase-2-advanced-screens-records-entity-profile.md` | 1.0 — Proposed (تصبح Accepted باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases/designs` | `superseded/phase-design-package-v0.3/phases/designs/phase-3-workflows-approvals-actions.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases/designs` | `superseded/phase-design-package-v0.3/phases/designs/phase-4-advanced-permissions-feature-management.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases/designs` | `superseded/phase-design-package-v0.3/phases/designs/phase-5-files-rag-ocr-media.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases/designs` | `superseded/phase-design-package-v0.3/phases/designs/phase-6-gateway-agents-sql-chat-reports.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases/designs` | `superseded/phase-design-package-v0.3/phases/designs/phase-7-integrations-app-store.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded/phase-design-package-v0.3/phases/designs` | `superseded/phase-design-package-v0.3/phases/designs/phase-8-monitoring-offline-production.md` | 1.0 — Proposed (Accepted باعتماد v0.3) | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded` | `superseded/pre-design-analysis-v1.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `superseded` | `superseded/system-design-v1.md` | — | Superseded | تاريخي — لا مالك نشط | محظور إلا بتكليف صريح |
| `traceability` | `traceability/TRACEABILITY_MATRIX.md` | 0.1 — Seed/Proposed | Proposed (G1) | ‏System Knowledge — Specification Architect | المراجعات + المولد |
| `ui` | `ui/UI_ACTION_BUTTON_MODEL.md` | 1.1 — (Δ v0.8: +§2.1 متغيّر العرض «inline message action» —  | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_ADMIN_CONSOLE_MODEL.md` | 1.1 — (Δ v0.8: +OD-BLD-1 أوضاع الباني الثلاثة — مقفل بقرار S | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_AI_WORKSPACE_MODEL.md` | 1.1 — (Δ v0.8: +§14 وضعا العرض محادثة/بطاقات — OD-WS-4 مقفل  | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_COMPONENT_STATES.md` | 1.1 — (Δ 2026-07-19 دفعة G1: +القسم S16–S20 «حالات البيانات/ | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_DESIGN_SYSTEM.md` | 1.0 — Proposed | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_FIELD_NAMING.md` | 1.1 — (Δ v0.8: +سلسلة «الإرجاع الموجَّه» في §3 — WORKFLOW_IT | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_GATE_REVIEW_CHECKLIST.md` | 1.0 — Proposed | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_INTERACTION_MODEL.md` | 1.0 — Proposed (v0.5) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_PROGRESSIVE_DISCLOSURE.md` | 1.0 — Proposed (v0.5) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_PROVIDER_MODEL_MANAGEMENT.md` | 1.0 — Proposed (v0.6) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_REFERENCE_USAGE_POLICY.md` | 1.1 — (Δ v0.8: +§3.1 مشاعية الأنماط المحادثية العامة — بقرار | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_REFINEMENT_GATE_REVIEW.md` | 1.0 — Proposed (v0.5) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_RUN_EXECUTION_MODEL.md` | 1.0 — Proposed (v0.6) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_SCREEN_BEHAVIOR_CARDS.md` | 1.1 — (Δ v0.8: تحديث بطاقتي 5/7 بزر «إرجاع إلى…» وفق FR-3.11 | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_SCREEN_CARDS_BY_PHASE.md` | 1.0 — Proposed | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_SCREEN_GOVERNANCE_STANDARD.md` | 1.0 — Proposed (يُعتمد بتوقيع/دمج SA في بوابة G1) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_SCREEN_INVENTORY.md` | 1.4 — (Δ v1.4/G1 2026-07-19: +ثلاثة أعمدة للجدول A — `archet | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_SITEMAP.md` | 1.0 — Proposed | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_STITCH_PROMPTS_BY_PHASE.md` | 1.1 — (Δ v0.8: تحديث G6 بشجرة org مرنة العمق وفق FR-1.Org-Ex | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_STITCH_REFINED_PROMPTS.md` | 1.0 — Proposed (v0.5) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_UX_ASSUMPTIONS.md` | 1.1 — (Δ v0.6: A-UX-15 | Current | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_V06_DELTA_AMENDMENTS.md` | 1.0 — Proposed (v0.6) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_V06_GATE_REVIEW.md` | 1.0 — Proposed (v0.6) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `ui` | `ui/UI_VISIBILITY_RULES.md` | 1.0 — Proposed (v0.5) | Proposed (G1) | حِزم UI/UX — Specification Architect | ‏Rocket/منفذ الواجهة + بوابات UI |
| `(الجذر)` | `vision.md` | 1.0 | Current / Accepted | SA (المالك) / Specification Architect | الجميع (جلسة أولى/بشر) |

**الإجمالي:** 118 ملفاً + هذا الفهرس (تغطية 100%).

**Related:** `AUTHORITY.md` · `decisions/open-decisions.md` (‏OD-IDX-1) · `PACKAGE_CHECKLIST.md`
