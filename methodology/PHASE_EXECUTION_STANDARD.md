# PHASE_EXECUTION_STANDARD.md — معيار تنفيذ المراحل (صفحة تقنين)

> **Version:** 1.0 — Accepted — G1-B 2026-07-20 (merge dd098dff9bed7a1f267ec5552b0e3366e368883d · tag v1.2-governance-baseline) · **Date:** 2026-07-19 · **الموضع:** `methodology/PHASE_EXECUTION_STANDARD.md`
> **Authority:** المرتبة 2 (`AUTHORITY.md`) — **تقنين رقيق فوق أصل قوي، لا قالب موازٍ**: أعمدة `phases/PHASE_MASTER_PLAN.md §2` هي القالب، وتصاميم المراحل الثمانية قائمة وترث `§4 Common Phase Baseline`، وقاعدة «تصميم التفعيل عند التفعيل» نافذة برأس كل ملف.

## §1 القواعد الأربع الملزمة
1. **القالب:** أعمدة PMP §2 (‏inputs/outputs/enablement/out-of-scope/exit/risks/open-decisions) هي البنية الإلزامية لأي مرحلة حاضرة أو مستقبلية — لا قالب آخر.
2. **حقلان إلزاميان يُضافان لكل مرحلة عند تفعيلها** (في تصميم التفعيل): **FP-Ordering** (ترتيب حزم الميزات داخل المرحلة — دون تجميد تفاصيل الحزم المستقبلية) و**Decision-Closure Checklist** (سطر المرحلة من §2 أدناه محدَّثاً بلحظة التفعيل من سجل `open-decisions`).
3. **لا بطاقة مهمة تصدر قبل اجتماع ثلاثة:** تصميم تفعيل معتمد + إغلاق قائمة قرارات المرحلة (أو رفع بنودها Decision Requests) + عقود شاشات الحزمة **Approved**.
4. **تسليم المرحلة = عمود Enablement مستوفى + ‏write-back مكتمل** (‏agent-execution-model §16) — لا إغلاق بغيرهما.

## §2 قوائم الإغلاق المرجعية P0–P8 (لقطة G1 — تُحدَّث من السجل عند كل تفعيل)
> يغلقها **Specification Architect قبل توليد بطاقات المرحلة** حتى لا يواجه وكيل التنفيذ قراراً واحداً؛ المصدر الحي: `decisions/open-decisions.md` + عمود Open decisions في PMP.

| Phase | ‏Decision-Closure قبل بطاقاتها | ملاحظات |
|---|---|---|
| **P0** الأساس التقني | صفوف ترخيص الستاك (فئة 2) + كون Baseline الحوكمة (G1) معتمداً | لا شاشات مستخدم |
| **P1** ‏Governed Core + Builder | **F-3-Residual:** دمج ما يمس P1 من `DELTA_V08` (‏FR-1.Org-Ext) في تصميم التفعيل ووسم الجزء المدمج Superseded · التقيد بـ**ADR-0032** في نموذج البيانات (+حسم موضع توليد UUIDv7) · حسم Clarify التسعة: ‏OD-IX-1..3 · ‏OD-VZ-1..3 · ‏OD-PD-1..3 · عقود شاشات P1 ‏Approved (‏auth.* · ‏run.* · ‏admin.record_types …) · ‏OD-BLD-1 مقفل ✅ | أثقل قائمة — محددة بالكامل |
| **P2** سجلات متقدمة + Entity Profile | عقود شاشاتها + امتداد enums/الحقول من P1 · **بوابة FP-DOCGEN** (بناء خط توليد الوثائق — ‏ADR-0035 بند 5) تقع في نافذة هذه المرحلة | لا OD معلق خاص بها بالسجل |
| **P3** ‏Workflows/Approvals/Actions | ‏F-3-Residual: دمج FR-3.11/3.12 · تثبيت بقية كتالوج الأفعال (‏OD-NM-1) · تصميم حقول Workflow owning-unit (‏owning_unit_id · using_units[] · step_assignee_scope) كعقد · عقدا SLA-Policy/Templates (توثيق) · ‏OD-WF-1/2 وOD-ORG-1 مقفلة ✅ · ‏OD-TPL-1/AB-4 **يبقيان مؤجلين** ولا يدخلان إلا بقرار مالك صريح · حسم انحراف canvas (‏CC-WF-1 — عقد `admin.workflows`) ببوابة G4 أو هنا | — |
| **P4** الصلاحيات المتقدمة | سياسة إعادة حساب الموروث ضمن Permission Contract | ‏OD-ORG-1 يحصّن ضد org→RLS |
| **P5** ملفات/RAG/OCR | ‏OD-PSC-1 و‏OD-PSC-2 (مخزن الأسرار الأول + حساسية endpoint_ref) · ضبط OD-MX-4 وOD-PSC-3 قيماً افتراضية بالتصميم (‏Ops-config) · عقد File-Portability (توثيق) | — |
| **P6** ‏Workspace/Agents/Reports | ‏OD-MX-1 (التوصية: مخفي) · ‏OD-RUN-1/2/3 · ‏OD-WS-4 مقفل ✅ · **بوابات ADR-0030-Δ الأربع قبل أي تفعيل OWUI** · ‏Event-Contract skeleton (توثيق) | — |
| **P7** التكاملات + Store | ‏Connector Contract (فصل admin_status/op_health) + معمارية Store الموقعة (توثيق) | — |
| **P8** الإنتاجية/Offline | تفصيل بنية الحزمة · ‏restore drill شرط بوابة · **قرار ADR-0036 (الخصخصة) منفَّذاً قبل أي بيانات حقيقية** · اكتمال توليد الوثائق الكامل (‏DGP) | ‏G6 تسبقها إلزاماً |

**الضمان:** مع (Baseline + تصميم تفعيل + الجدول أعلاه + بروتوكول §15) كل قرار إما **مقفل قبل البطاقات** أو **مرفوع DR** — لا مسار ثالث؛ وحرية المنفذ محصورة نصاً في §13.

**Related:** `../phases/PHASE_MASTER_PLAN.md` (§2/§4) · `../decisions/open-decisions.md` · `agent-execution-model.md` (§§12–17) · `../contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` · `../decisions/adr/ADR-0035-contracts-layer-single-source.md`
