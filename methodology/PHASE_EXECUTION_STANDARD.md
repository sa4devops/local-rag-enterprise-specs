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
| **P3** ‏Workflows/Approvals/Actions | ‏F-3-Residual: دمج FR-3.11/3.12 · تثبيت بقية كتالوج الأفعال (‏OD-NM-1) · تصميم حقول Workflow owning-unit (‏owning_org_unit_id · using_units[] · step_assignee_scope) كعقد · عقدا SLA-Policy/Templates (توثيق) · ‏OD-WF-1/2 وOD-ORG-1 مقفلة ✅ · ‏OD-TPL-1/AB-4 **يبقيان مؤجلين** ولا يدخلان إلا بقرار مالك صريح · حسم انحراف canvas (‏CC-WF-1 — عقد `admin.workflows`) ببوابة G4 أو هنا | — |
| **P4** الصلاحيات المتقدمة | سياسة إعادة حساب الموروث ضمن Permission Contract + ‏Scoped-Admin وفق ADR-0037 (منح صريح؛ وراثة SELF_ONLY افتراضاً بتسجيل تدقيقي) | ‏OD-ORG-1 يحصّن ضد org→RLS |
| **P5** ملفات/RAG/OCR | ‏OD-PSC-1 و‏OD-PSC-2 (مخزن الأسرار الأول + حساسية endpoint_ref) · ضبط OD-MX-4 وOD-PSC-3 قيماً افتراضية بالتصميم (‏Ops-config) · عقد File-Portability (توثيق) | — |
| **P6** ‏Workspace/Agents/Reports | ‏OD-MX-1 (التوصية: مخفي) · ‏OD-RUN-1/2/3 · ‏OD-WS-4 مقفل ✅ · **بوابات ADR-0030-Δ الأربع قبل أي تفعيل OWUI** · ‏Event-Contract skeleton (توثيق) | — |
| **P7** التكاملات + Store | ‏Connector Contract (فصل admin_status/op_health) + معمارية Store الموقعة (توثيق) | — |
| **P8** الإنتاجية/Offline | تفصيل بنية الحزمة · ‏restore drill شرط بوابة · **قرار ADR-0036 (الخصخصة) منفَّذاً قبل أي بيانات حقيقية** · اكتمال توليد الوثائق الكامل (‏DGP) | ‏G6 تسبقها إلزاماً |

**الضمان:** مع (Baseline + تصميم تفعيل + الجدول أعلاه + بروتوكول §15) كل قرار إما **مقفل قبل البطاقات** أو **مرفوع DR** — لا مسار ثالث؛ وحرية المنفذ محصورة نصاً في §13.

## §3 Phase Exit Review — مراجعة خروج المرحلة (قاعدة مركزية واحدة، موروثة)
> **أُضيف:** 2026-07-30 — بقرار مالك: «لا يجوز الاعتماد على ذاكرة المالك أو أي مساعد لتذكّر التوصيات والقرارات والالتزامات لاحقاً». **القاعدة مركزية وتُورَّث**: تنطبق على **كل** مرحلة ودفعة — حاضرة أو مستقبلية، بما فيها المراحل التي **لا يوجد لها ملف تصميم مستقل بعد** (تُطبَّق عليها من هذا الموضع عند إنشائها أو تفعيلها؛ لا تُنشأ ملفات لأجلها ولا قوائم مراجعة موازية). هذه القاعدة **إجراء خروج** لا قالب جديد: قالب المرحلة يبقى أعمدة `phases/PHASE_MASTER_PLAN.md §2` وفق §1-1.

**المبدأ الحاكم — بثلاث عبارات ملزمة:**
```text
No silent deferral.
No memory-only obligation.
No phase closure with an unclassified remainder.
```

### §3.1 Scope Completion
- جميع المخرجات المطلوبة للمرحلة **موجودة** ومُشار إليها بمواضعها.
- جميع معايير القبول **مثبتة بدليل** (لا ادعاء بلا مرجع).
- جميع **Stop Conditions** التي ظهرت: إمّا عُولجت بدليل، أو **منعت الإغلاق** — ولا حالة ثالثة.

### §3.2 Decision Closure
- **لا قرار لازم غير محسوم** عند الإغلاق.
- كل **Owner Decision** مسجَّل في وعاء حاكم وفق `AUTHORITY.md` (المرتبة 4: `decisions/open-decisions.md` هو المرجع الملزم للمفتوح/المقفل).
- **لا قرار يعيش في تقرير أو محادثة فقط.** التقرير إحالة، لا وعاء.

### §3.3 Remainder Census — جرد المتبقي
جرد **كامل** لكل عنصر ظهر أثناء المرحلة، بالفئات: Recommendations · Observations · Deltas · Risks · Defects · Deferred work · Exceptions · Owner-only actions · External-review findings · Handoff obligations · Future-phase requirements discovered during execution.

ثم **تصنيف كل عنصر إلى واحدة من ثلاث حالات حصراً:**

| الحالة | المعنى | الشرط |
|---|---|---|
| **COMPLETE** | اكتمل داخل المرحلة | بدليل قابل للتدقيق |
| **GOVERNED TRANSFER** | لا يُنفَّذ في هذه المرحلة، ومسجَّل حاكماً | تستوفي **كل** حقول §3.4 |
| **BLOCKING REMAINDER** | يمنع الإغلاق | لا وجهة حاكمة صحيحة · أو يحتاج قراراً لازماً · أو يلزم لخروج المرحلة |

**المعادلة الإلزامية:**
```text
Total discovered remainder = COMPLETE + GOVERNED TRANSFER + BLOCKING REMAINDER
UNCLASSIFIED = 0
```

**ممنوع** اعتبار أيٍّ من هذه الكلمات معالجةً كافية بذاتها: `later` · `deferred` · `backlog` · `recommendation` · `out of scope` · `follow-up` · `to be considered`. الكلمة ليست وعاءً ولا مالكاً ولا شرط تفعيل.

### §3.4 حقول GOVERNED TRANSFER الإلزامية
لا يُعدّ عنصرٌ منقولاً حاكماً إلا بتسجيله في **وعاء حاكم مرتَّب** (يُثبَت من `AUTHORITY.md` قبل التسجيل) وباستيفاء: Stable ID · Source phase/batch · Description · Classification · Governing destination · Owning phase/batch · Owner or decision authority · Reason not executed now · Activation prerequisite · Blocking effect · Required evidence · Closure condition · Traceback to source evidence.

**التوجيه المبدئي للأوعية:** القرارات المفتوحة وقرارات المالك ⇒ `decisions/open-decisions.md` · الأعمال المؤجلة ذات المرحلة والوجهة ⇒ `decisions/DEFERRED_IMPLEMENTATION.md` · التوصيات المنهجية وانتقالات المراحل ⇒ قيد Δ في الخارطة أو الخطة المالكة · آثار الحجب ⇒ الوعاء الذي يحدده النص الحاكم للبوابة المعنية.

**قاعدة قاطعة:** وجود العنصر في وثيقة جرد أو تقرير `traceability/**` **وحده لا يُعدّ Governed Transfer** — تلك مخرجات تحليلية غير حاكمة. يبقى العنصر **BLOCKING REMAINDER** حتى يُسجَّل في وعائه الحاكم. ويجوز أن تكون وثيقة الجرد التفصيلية **وثيقة إحالة**، لا بديلاً عن التسجيل.

### §3.5 Traceability
لكل عنصر **مصدر ووجهة ودليل** · لا روابط ولا مراسي مكسورة · ولا اعتماد على وثيقة غير حاكمة دون توصيفها بذلك صراحةً.

### §3.6 Repository State
`handoff` محدَّث عند وجوب ذلك · `phases/phase-roadmap.md` و`phases/PHASE_MASTER_PLAN.md` محدَّثان عند وجوب ذلك · السجلات والفهارس **متسقة** (‏EC-3 = 100%) · **لا تغييرات غير مفسَّرة**.

### §3.7 Git and Release State
الفرع والـPR **موثَّقان** · لا merge/tag/release إلا بالسلطة المطلوبة نصاً · و**إذا كانت خطوة مالك لازمة للإغلاق فتُسجَّل خطوةً صريحة ولا تختفي** من السجل.

### §3.8 Next-phase Readiness
لا تُفتح المرحلة التالية تلقائياً · لا تُصدر عبارة الانتقال قبل اجتياز Phase Exit Review · ولا تُنفَّذ أعمال المرحلة التالية داخل الحالية إلا بتفعيل مستقل مشروع.

### §3.9 قاعدة الإغلاق
**لا يجوز إعلان Phase أو Batch مغلقة إذا بقي عنصر غير مصنَّف أو بقي `BLOCKING REMAINDER`.** ويجوز نقل عنصر إلى مرحلة لاحقة **فقط** إذا كان تنفيذه الآن خارج ملكية المرحلة الحالية، أو ممنوعاً، أو مشروطاً ببوابة لاحقة — وبشرط تسجيل **GOVERNED TRANSFER كاملاً** وفق §3.4. **النقل الحاكم لا يعني إسقاط الالتزام ولا تنفيذه المبكر.**

**تمييز إلزامي — ثلاثة معانٍ لا تُخلط:**
1. **إغلاق نطاق المرحلة** — استيفاء §3.1–§3.8 لهذه المرحلة وحدها.
2. **اكتمال المشروع كله** — حكمٌ مستقل لا يُستنتج من إغلاق مرحلة.
3. **عدم فقدان الالتزامات** — ضمانٌ مستقل يتحقق بالتسجيل الحاكم، ويبقى نافذاً بعد الإغلاق.

## بوابة الأساس (Foundation Gate) — إجراء FP-0001
1. **verify:** فحص aql الفعلي — ‏build · ‏type-check · ‏lint · ‏deps · فحص الروابط.
2. **correct:** تصحيحات محدودة موثقة (بلا توسيع نطاق).
3. **جرد Adopt/Correct/Reject:** لكل ‏Token و‏Component و‏Pattern قرار صريح (تبنٍّ/تصحيح/رفض).
4. **استخراج Design System** قابل لإعادة الاستخدام من المتبنّى.
5. **اختبارات متعددة الأنماط:** شاشات مختلفة + ‏RTL/LTR + ‏Light/Dark + وصولية.
6. **تجميد Core UI Foundation** باعتماد SA.

**لا يُعلن Core قبل اجتياز البوابة كاملة.**

**Related:** `../phases/PHASE_MASTER_PLAN.md` (§2/§4) · `../decisions/open-decisions.md` · `agent-execution-model.md` (§§12–17) · `../contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` · `../decisions/adr/ADR-0035-contracts-layer-single-source.md`
