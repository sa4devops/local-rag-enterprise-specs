# TRACEABILITY_MATRIX.md — مصفوفة التتبع (بذرة G1)

> **Version:** 0.1 — Seed/Proposed · (Δ R1-C 2026-07-22: +ADR-0038 + دفعة R1-C) · **Date:** 2026-07-19 · **الموضع:** `traceability/TRACEABILITY_MATRIX.md`
> **Authority:** طبقة System Knowledge — كل أصل حاكم جديد/مرقّى له صف: (الأصل · نوعه · القرار الأم · من يستهلكه · حالته). مصدر تأليف لخط توليد الوثائق؛ يُحدَّث بقاعدة write-back (‏EC-10).

| الأصل | النوع | القرار/الأمر الأم | المستهلك الأول | الحالة |
|---|---|---|---|---|
| `AUTHORITY.md` | نص سلطة | م20 + أمر G0/G1 | كل الوكلاء والمستودعات الثلاثة | Proposed (G1) |
| `decisions/adr/ADR-0031..0036` | قرارات معمارية (6) | ‏Q1–Q5 + ‏DR-1/DR-2 | المنهجية · العقود · platform · aql | Proposed (G1) |
| ‏Δ ‏ADR-0017 · ‏Δ ‏ADR-0030 | تعديلان إضافيان | ‏ADR-0031 · تقرير v2.0 §F | سجل ADR · بوابات P6 | ضمن الدفعة |
| `contracts/NAMING_AND_CONTRACTS_STANDARD.md` | معيار عقود | ‏ADR-0035 | كل عقد لاحق · المولد | Proposed |
| `contracts/identity/RECORD_IDENTITY.md` | عقد هوية | ‏ADR-0032 + م17 | ‏Renderer · ws · التدقيق | Proposed |
| `contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` | قالب عقد | ‏ADR-0035 + §18 | عقود الشاشات كلها | Proposed |
| عقود البذرة: ‏run.list · ‏admin.record_types · ‏admin.actions · ‏admin.workflows | عقود شاشات (4) | ‏DR-2 + بطاقات 2/11/12/13 | ‏FP-0001/0002 ومساراتها | **Candidate** |
| `contracts/enums/ENUMS_DICTIONARY.md` | قاموس تعدادات | ‏ADR-0035 + ‏aql@eab9f99 | العقود · الواجهة · i18n | Candidate (بذرة aql) |
| `ui/UI_SCREEN_GOVERNANCE_STANDARD.md` | ‏Capstone حوكمة الشاشات | §18 + تقرير v2.0 ‏D-2 | ‏Rocket · العقود · بوابة G4 | Proposed |
| `ui/UI_COMPONENT_STATES.md` v1.1 | ترقية كتالوج (+S16–S20) | تقرير v2.0 ‏D-2-د | عقود الشاشات · التصميم | ضمن الدفعة |
| `ui/UI_SCREEN_INVENTORY.md` v1.4 | ترقية جرد (+3 أعمدة) | تقرير v2.0 ‏D-3 | العقود · ‏Rocket · البوابات | ضمن الدفعة |
| `methodology/agent-execution-model.md` v2.0 | ترقية نموذج الوكلاء (+§§12–17) | تقرير v2.0 ‏E-3 | كل وكيل تنفيذ | ضمن الدفعة |
| `methodology/PHASE_EXECUTION_STANDARD.md` | معيار مراحل | §18-د + ‏E-1/E-2 | تفعيل P0–P8 | Proposed |
| `methodology/ROCKET_OPERATING_MODEL.md` | نموذج قناة | ‏ADR-0031/0033 | دفعات Rocket · بوابة G4 | Proposed |
| `knowledge/BUSINESS_GLOSSARY.md` | معجم (بذرة) | ‏ADR-0035 (مصدر مولد) + ‏Q5 | الوثائق المولَّدة · i18n | Seed |
| `traceability/TRACEABILITY_MATRIX.md` | هذه المصفوفة | ‏EC-10 + ‏ADR-0035 | المراجعات · المولد | Seed |
| ‏Documentation Generation Pipeline (متطلب) | قدرة مؤجلة | أمر مالك G1 + ‏ADR-0035 بند 5 | ‏FP-DOCGEN ‏(P2) | Deferred-documented |
| `INDEX.md` | فهرس بشري | ‏OD-IDX-1 + ‏EC-3 | كل قارئ | ضمن الدفعة |
| إدخال handoff ‏H-G1 | سجل تسليم | م20 + منهجية §14 | الجلسة التالية | ضمن الدفعة |
| تعديلا platform: ‏AGENTS.md · ‏docs/SPEC_SOURCE.md | مواءمة توثيق تنفيذ | ‏ADR-0031/0036 + قاعدة المستويين | وكلاء platform | ضمن دفعة platform |
| Δ تصحيحات ما-قبل-الدفع (مراجعة SA): ‏README ‏v1.3 (قراءة/سلطة/ستاك) · صف README في INDEX · ‏SPEC_SOURCE (مرجع القراءة قبل/بعد الوسم) | تصحيح مراجعة | مراجعة SA لتقرير G1-A + ‏ADR-0031/0035 | القراء وكل الوكلاء | ضمن الدفعة |
| `decisions/adr/ADR-0037-scoped-administration-model.md` | قرار معماري | قرارات مالك R1 (2026-07-21) — المرجع تقرير v1.1 | العقود · ‏P4 · الواجهة | Proposed — R1-B |
| `methodology/AI_DEV_CONTROL_PLANE.md` | قدرة منهجية | قرار مالك R1 + ‏ADR-0033 (مصالحة) | الأتمتة اللاحقة · الوكلاء | Proposed — R1-B |
| `methodology/RECONCILIATION_ROADMAP.md` | خارطة مسار | قرار مالك R1 (2026-07-21) | مسار R2–R11 · المالك | Proposed — R1-B |
| دفعة R1-B (تقنين المصالحة — 15 مساراً) | دفعة تقنين | قرارات مالك R1 (2026-07-21) — المرجع تقرير v1.1 | المستودع المنشور · المؤشر الحاكم | ضمن الدفعة |
| `decisions/adr/ADR-0038-system-wide-administration-boundary.md` | قرار معماري | قرار المالك 2026-07-22 — حدّ الإدارة الشاملة | العقود · ‏P4 · شاشات الإدارة | Proposed — يُقبل بتوقيع/دمج SA في بوابة R1-C |
| دفعة R1-C (حدّ الإدارة الشاملة — 10 مسارات) | دفعة توثيقية | قرار المالك 2026-07-22 — توضيح حدّ ADR-0037 | المستودع المنشور · المؤشر الحاكم | ضمن الدفعة |


**Related:** `../decisions/adr/ADR-0035-contracts-layer-single-source.md` · `../INDEX.md` · `../methodology/agent-execution-model.md` (§16)
