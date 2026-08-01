# RAR-007 — سجل القدرات الاستراتيجية والمقترحات المستقبلية
## Strategic Capability Backlog, Future Registry & Promotion Governance

> **نوع الوثيقة:** Request for Architectural Review (RAR)  
> **المشروع:** AQL / AQLORA Enterprise AI Platform  
> **الحالة الأولية:** Governance Capability — Partially Present, Not Yet Unified  
> **الغرض:** تحديد مكان الأفكار المستقبلية وحالاتها ومسار ترقيتها دون تحويلها إلى التزامات تنفيذية  
> **قاعدة السلطة:** المستودع الحاكم الفعلي يتقدم على هذه الوثيقة  
> **قاعدة التنفيذ:** لا إنشاء سجل جديد أو تعديل AUTHORITY/INDEX قبل دراسة واعتماد

---

## 1. ملخص تنفيذي

يوجد في المشروع عدد من الأماكن التي قد تحتوي على أفكار أو قرارات أو عناصر مؤجلة، مثل:

- Deferred Implementation Register.
- Open Decisions.
- Phase Roadmaps.
- ADR Register.
- Handoffs.
- Business Glossary.
- Traceability Matrix.
- تقارير المصالحة.
- ملفات أفكار ومصادر تاريخية.

لكن لا يوجد لدينا يقين بأن هناك سجلاً موحداً يجيب عن الأسئلة التالية:

- ما الفكرة المستقبلية؟
- هل اعتمدت كاتجاه أم ما زالت مجرد اقتراح؟
- هل تحتاج تهيئة معمارية الآن؟
- هل تأجل تنفيذها إلى Phase محددة؟
- هل رفضت؟ ولماذا؟
- هل أصبحت Capability قانونية؟
- هل تحتاج ADR أو Contract أو Owner Decision؟
- ما الذي يقرأه Claude Architecture وما الذي لا يجب أن يقرأه Coding Agent؟

نريد طريقة تمنع ضياع الأفكار، وفي الوقت نفسه تمنع تضخم المواصفات أو تحول كل فكرة إلى التزام ضمن Source of Truth.

---

## 2. المشكلة الحالية

### 2.1 ضياع الأفكار
قد تبقى الفكرة في محادثة أو ملف خارجي ولا تظهر عند التنفيذ اللاحق.

### 2.2 تضخم المواصفات
نقل كل فكرة مباشرة إلى الدستور أو العقود يجعلها تبدو معتمدة وقابلة للتنفيذ.

### 2.3 تعدد مصادر الحقيقة
قد تظهر الفكرة نفسها في Roadmap وDeferred Register وتقرير خارجي وملف أفكار بصيغ مختلفة.

### 2.4 عدم وضوح الحالة
لا نعرف هل «Extension Store» فكرة، Capability مستقبلية، قرار Architecture، أم Feature في Phase 7.

### 2.5 خلط القدرة بالتقنية
قد تسجل كلمة مثل Kafka وكأنها Feature، بينما هي مجرد Option محتمل لتنفيذ حاجة لم تعتمد بعد.

### 2.6 فرض المستقبل على الحاضر
توثيق تفصيلي مفرط لقدرة بعيدة قد يؤدي إلى Over-engineering أو يقيّد Architecture دون حاجة.

---

## 3. نية الحوكمة

نريد مساراً قريباً من:

```text
Observation / Idea
→ Triage
→ Strategic Capability Candidate
→ Architectural Review عند الحاجة
→ Owner Decision
→ Approved Future Capability أو Rejected
→ Prepare-Now Requirements إن لزم
→ ADR / Contract / Phase Allocation
→ Feature Package
→ Task Cards
→ Code / Tests / Release
```

ليس كل عنصر يمر بكل المراحل، لكن يجب أن نعرف أين هو ومن يملكه وما الذي يسمح بترقيته.

---

## 4. التمييز بين أنواع السجلات

### 4.1 Idea Inbox

مادة خام غير معتمدة، قد تأتي من:

- محادثة.
- مستخدم.
- Benchmark.
- نظام منافس.
- تقرير بحث.
- ملاحظة أثناء التنفيذ.

لا يقرأها Coding Agent افتراضياً، ولا تعتبر Requirement.

### 4.2 Strategic Capability Backlog

قدرة لها مشكلة وقيمة وعلاقة بالمشروع، لكنها ليست التزام تنفيذ أو Contract نهائي.

### 4.3 Deferred Implementation

شيء معتمد أو مطلوب، لكن التنفيذ مؤجل إلى Phase أو Trigger محدد.

### 4.4 Open Decision

قرار يحتاج حسم المالك أو أدلة إضافية.

### 4.5 ADR

قرار معماري يوضح السياق والبدائل والتبعات.

### 4.6 Product Capability Catalogue

القدرات القانونية للمنتج، سواء منفذة أو مخطط لها، مع Stable IDs وروابط للعقود والمراحل.

### 4.7 Phase Roadmap

توزيع التنفيذ واعتمادياته عبر المراحل.

### 4.8 Feature Package

نطاق جاهز للتنفيذ، له قبول واعتماديات وحدود واضحة.

### 4.9 Historical Archive

مادة مرجعية غير قانونية لا يقرأها Agent التنفيذي افتراضياً.

على Claude تحديد الحدود، وربما دمج بعض السجلات إذا كان ذلك أفضل، لكن يجب منع الازدواج.

---

## 5. الجرد التاريخي للوظائف والميزات

يوجد جرد تاريخي كبير للشاشات والوظائف نوقش في مراحل سابقة. لا نريد إدراج عناصره كلها في هذه الوثيقة، ولا نقله حرفياً إلى Source of Truth.

المطلوب لاحقاً كعمل مستقل:

1. استخراج العناصر.
2. إزالة التكرار.
3. فصل Capability عن Screen وField وAction وReport.
4. مقارنة كل عنصر بالمواصفات الحالية.
5. تصنيفه: Covered / Partial / Missing / Superseded / Deferred / Rejected / Needs Decision.
6. إعطاء Stable ID فقط عند المرحلة المناسبة.
7. ربطه بالعقود والمرحلة والاختبارات.
8. إبقاء الأصل التاريخي كEvidence أو Archive.

هذا الجرد لا يساوي Strategic Backlog؛ قد يحتوي أشياء منفذة أو مكررة أو ملغاة. Claude يجب أن يحدد علاقته بـCapability Catalogue دون خلطهما.

---

## 6. الحقول المحتملة لكل فكرة أو قدرة

هذا مثال وظيفي، وليس Schema مفروضاً:

- Stable ID أو Temporary Intake ID.
- Title.
- Problem statement.
- Business value.
- Source.
- Date introduced.
- Proposer.
- Domain/Bounded Context.
- Current status.
- Decision required.
- Architecture impact.
- Security/privacy impact.
- Offline impact.
- Dependencies.
- Related capabilities.
- Duplicate/supersedes links.
- Target horizon.
- Prepare-now requirements.
- Trigger criteria.
- Owner.
- Evidence/research links.
- Defer/reject reason.
- Review date.
- Canonical destinations عند الترقية.

Claude يحدد الحد الأدنى حتى لا يتحول السجل إلى نظام Project Management ثقيل.

---

## 7. حالات مقترحة للمراجعة

- Inbox.
- Under Triage.
- Needs Research.
- Needs Owner Decision.
- Approved Future Capability.
- Prepare Now / Implement Later.
- Deferred to Phase.
- Experimental.
- Rejected.
- Superseded.
- Promoted to ADR.
- Promoted to Capability Catalogue.
- Promoted to Feature Package.
- Archived.

قد تكون هذه الحالات كثيرة. المطلوب من Claude تبسيطها مع تعريف واضح للTransitions.

---

## 8. قواعد الترقية

### 8.1 من Idea إلى Strategic Capability

تحتاج على الأقل:

- مشكلة واضحة.
- قيمة متوقعة.
- علاقة مباشرة بالمشروع.
- عدم تعارض مبدئي مع القيود.
- مصدر معروف.
- مالك أو جهة مهتمة.

### 8.2 إلى Architectural Review

عند احتمال تأثيرها على:

- Module boundaries.
- Data model.
- Identity.
- Security.
- Runtime.
- Deployment.
- Offline operation.
- Integration contracts.

### 8.3 إلى Approved Future Capability

قرار مالك واضح مع بيان أنها ليست Implementation Now.

### 8.4 إلى Prepare Now

فقط إذا كان تجاهلها الآن سيغلق طريقاً مستقبلياً أو يسبب Rework كبيراً. مثال: Event Contract Skeleton لقدرة Real-time المؤجلة.

### 8.5 إلى ADR

عندما يوجد قرار معماري حقيقي وبدائل وتبعات.

### 8.6 إلى Contract

عندما تصبح Semantics مستقرة بما يكفي.

### 8.7 إلى Feature Package

عندما يعرف النطاق والقبول والاعتماديات والمرحلة والمخاطر.

---

## 9. قواعد عدم الترقية

تبقى الفكرة أو ترفض إذا كانت:

- مجرد اسم تقنية بلا مشكلة.
- تكرر Capability موجودة.
- تتعارض مع Offline/Security دون مبرر.
- بلا قيمة أو Owner.
- تعتمد على افتراض غير مثبت.
- تسبب Over-engineering.
- سابقة لأوانها ولا تحتاج Readiness.
- تحاول تجاوز العقود أو Roadmap.
- غير قابلة للاختبار.
- اقتباساً شكلياً من منتج آخر بلا علاقة بالحاجة.

---

## 10. التعامل مع القدرات المؤجلة

كل عنصر مؤجل يجب أن يعرف:

- لماذا تأجل.
- ما الذي ينفذ الآن، إن وجد.
- ما الذي لا ينفذ الآن.
- Trigger لإعادة فتحه.
- Phase أو Horizon تقريبي.
- Dependencies.
- أثره على المعمارية الحالية.
- آخر تاريخ مراجعة.
- Owner.
- Acceptance criteria المستقبلية الأولية إن كانت معروفة.

### مثال Real-time AI

- Prepare now: Terminology وEvent Invariants.
- Do not implement: Broker وPipeline وLive UI.
- Trigger: استقرار Connectors وWorkflows ووجود Use Case وSLO.

---

## 11. الفرق بين Future Capability وDeferred Implementation

على Claude حسم قاعدة واضحة. تصور مبدئي:

- **Future Capability:** اتجاه منتج معتمد أو مرشح، لكن قد لا يكون التنفيذ مقرراً.
- **Deferred Implementation:** تنفيذ قدرة أو جزء معتمد، مؤجل بسبب ترتيب أو اعتماديات.

ليس كل Future Capability يجب أن تدخل Deferred Register. وليس كل Deferred Item يحتاج Strategic Backlog entry منفصلة.

---

## 12. مكان السجل داخل المستودع

لا نفرض مساراً. Claude يجب أن يفحص:

- `decisions/DEFERRED_IMPLEMENTATION.md`
- `decisions/open-decisions.md`
- `decisions/adr/`
- `phases/` أو `roadmap/`
- `knowledge/`
- `traceability/`
- `INDEX.md`
- `AUTHORITY.md`
- أي Capability Catalogue قائم

ثم يقرر هل الأفضل:

- توسيع Deferred Register.
- إنشاء Strategic Registry مستقل.
- إنشاء Idea Inbox خارج Tier-0.
- استخدام Structured Source مع Markdown مولد.
- دمج بعض السجلات.

المبدأ: الفكرة غير المعتمدة لا تدخل ترتيب السلطة كأنها Specification.

---

## 13. ترتيب القراءة للـAgents

يجب أن يحدد Claude Reading Matrix:

### Claude Architecture

يقرأ Strategic Backlog عند مراجعة قدرة أو Roadmap أو تعارض مستقبلي.

### Coding Agent / Claude Code

لا يقرأ Idea Inbox افتراضياً. يقرأ فقط:

- Approved task.
- Feature Package.
- Contracts.
- ADRs اللازمة.
- Deferred guards المرتبطة.

### Rocket

لا يقرأ أفكاراً غير معتمدة حتى لا يخترع شاشات أو Actions.

### Documentation Generator

يقرأ Capability Catalogue والحقائق المعتمدة، لا Raw Ideas.

### Research Agent

يكتب Findings إلى Staging أو Evidence، ولا يعتمد Capability مباشرة.

---

## 14. العلاقة مع توليد وثائق المشروع

نريد لاحقاً توليد:

- BRD.
- FRD.
- SRS.
- SDS / Architecture Description.
- Data Dictionary.
- Screen Catalogue.
- Workflow Catalogue.
- Permission Matrix.
- API Documentation.
- User Guide.
- Admin Guide.
- Operations Guide.
- Test Plan.
- Release Documentation.

لكن التوليد يجب أن يعتمد على سلسلة حقائق معتمدة:

```text
Capability
→ Requirements
→ Contracts
→ ADRs
→ Phase / Feature Package
→ Code
→ Tests
→ Release Evidence
```

Strategic Backlog لا يظهر في BRD الحالي كالتزام، إلا في قسم Future Roadmap موسوم بوضوح.

---

## 15. Traceability وعدم التكرار

نحتاج آلية تمنع:

- Duplicate IDs.
- الفكرة نفسها بأسماء متعددة.
- تضارب الحالة بين الملفات.
- Orphan ADR.
- Deferred Item بلا Owner أو Trigger.
- Capability بلا Phase.
- Feature Package بلا Requirement.
- Code بلا Contract.
- Rejected Idea تعود بلا Evidence جديد.
- Superseded Entry يبقى ظاهراً كActive.

قد تستخدم Traceability Matrix أو Validation Script أو Generator. Claude يقرر التناسب.

---

## 16. أمثلة تصنيف

### مثال A — Governed Extension Store

- Strategic Capability: نعم.
- Prepare Now: Package/Trust Architecture.
- Implement Later: Store UI وInstall/Upgrade lifecycle.
- ADR/Contract: قد يلزم.
- Phase: لاحق.

### مثال B — Kafka

- Technology option فقط.
- Reject Now كقرار Architecture.
- لا تسجل كCapability مستقلة.

### مثال C — Agent Templates

- Product Capability Candidate.
- تحتاج Product/Architecture Review.
- قد تدخل Capability Catalogue بعد الاعتماد.

### مثال D — Figma Polishing

- Tool/Process option.
- ليست Product Capability.
- Optional/Deferred Decision.

### مثال E — تغيير لون زر

- ليس Strategic Capability.
- UI Task أو Design Token Change.

### مثال F — Stable Organizational IDs

- Invariant/Architecture rule، وليس Backlog item بعد اعتماده.
- يجب أن يعيش في Contract/ADR أو Standard مناسب.

---

## 17. الأدوار والمسؤوليات

- **Owner / SA:** اعتماد أو رفض القدرة والمرحلة.
- **Claude Architecture:** تحليل وتصنيف واقتراح Canonical Destination.
- **Claude Code:** تنفيذ تحديث معتمد فقط.
- **Coding Agent:** تنفيذ Feature Package.
- **Rocket:** تنفيذ UX ضمن العقود.
- **Reviewer:** إثبات Evidence والتتبع.
- **Documentation Generator:** توليد مشتقات من Source of Truth.
- **Research Agent:** تقديم Evidence دون اعتماد قرار.
- **Repository Maintainer:** حماية Index/Authority/Validation.

---

## 18. دورة المراجعة

اقتراح للمناقشة:

- Triage عند الإدخال.
- Review عند Release Planning.
- Stale review للعناصر غير المحدثة.
- تقرير للعناصر بلا Owner أو Trigger.
- Close/Supersede بدلاً من الحذف.
- Archive للمصادر التاريخية.
- Changelog.
- Periodic duplicate detection.

Claude يقرر Cadence الملائم ولا يحول العملية إلى بيروقراطية زائدة.

---

## 19. Structured Source أم Markdown فقط

الخيارات التي يجب تقييمها:

### Option A — Markdown only

**الإيجابيات:** بسيط، واضح، Git-friendly.  
**السلبيات:** صعب التحقق الآلي وتوليد المخرجات الكبيرة.

### Option B — YAML/JSON canonical + generated Markdown

**الإيجابيات:** Validation وGeneration وIDs.  
**السلبيات:** تعقيد إضافي وحاجة إلى Tooling.

### Option C — Hybrid

ملف Markdown لكل Capability مع Front Matter منظم وIndex مولد.

لا نريد فرض Option. Claude يقرر بحسب نضج المشروع والحاجة الحالية.

---

## 20. Archive Policy

المصادر التاريخية مثل المحادثات والملفات القديمة يجب ألا تختلط مع Tier-0. نحتاج معرفة:

- أين تحفظ؟
- هل تدخل Git؟
- هل تحفظ Hash وSource metadata؟
- هل يقرأها Agent عند Reconciliation فقط؟
- كيف يشار إلى العنصر المستخرج منها؟
- كيف تمنع حذف Evidence؟
- كيف تميز Historical عن Canonical؟

قد يكون الأصل خارج Repo مع Manifest داخلي، أو داخل `archive/` منخفض السلطة. Claude يقرر.

---

## 21. الحالة المتوقعة داخل المستودع — تحتاج إثباتاً

تقارير التنفيذ تشير إلى:

- Deferred Register موجود وتمت إضافة صفوف.
- Open Decisions موجود.
- Business Glossary وTraceability Seeds موجودة.
- INDEX وAUTHORITY موجودان.
- لا دليل واضح على Strategic Capability Registry موحد.
- Capability Roadmap موجود في تقارير خارجية وقد لا يكون Canonical.
- الجرد التاريخي لم يتحول إلى Catalogue كامل.

Claude يجب أن يتحقق من actual HEAD ويحدد ما هو حي وما هو تقرير خارجي فقط.

---

## 22. الفجوات المحتملة — قائمة فحص

- Unified future capability registry.
- Status taxonomy.
- Promotion rules.
- Owner/trigger fields.
- Reading matrix.
- Link to Deferred/Open Decisions/ADR.
- Capability Catalogue boundary.
- Archive policy.
- Traceability.
- Validation/checks.
- Documentation-generation policy.
- Duplicate/supersede rules.
- Review cadence.
- Versioning.
- INDEX integration.
- Authority classification.
- Structured vs Markdown decision.

---

## 23. الأسئلة الحوكمية والمعمارية المفتوحة

1. هل نحتاج ملفاً مستقلاً أم توسيع الموجود؟
2. هل Idea Inbox داخل Repo الحاكم؟
3. ما الذي يعد Canonical؟
4. كيف نتجنب ازدواج Deferred وStrategic؟
5. متى تتحول الفكرة إلى Capability؟
6. هل Stable ID يعطى عند الإدخال أم الاعتماد؟
7. هل نستخدم Markdown أم Structured Source؟
8. من يملك التعديل؟
9. ما الذي يقرأه Coding Agent؟
10. كيف يربط بالجرد التاريخي دون نسخه كله؟
11. كيف تميز Future Vision في BRD؟
12. ما Gate الترقية؟
13. ما حالة Prepare Now؟
14. كيف تمنع Stale Decisions؟
15. هل يحتاج ADR أم Governance Standard؟
16. أين تحفظ Evidence التاريخية؟
17. كيف تمنع الفكرة من القفز مباشرة إلى Feature Package؟

---

## 24. خارج النطاق

- استخراج الجرد التاريخي كله.
- بناء تطبيق Backlog.
- اختيار Jira أو GitHub Projects.
- إعادة كتابة Roadmap.
- اعتماد كل فكرة.
- توليد BRD الآن.
- نقل المحادثات كاملة إلى Repo.
- تعديل AUTHORITY بلا دراسة.
- إنشاء Tooling معقد قبل إثبات الحاجة.

---

## 25. المطلوب من Claude Architecture

1. Evidence Baseline.
2. Registry Boundary Recommendation.
3. Canonical Data Model بالحد الأدنى.
4. Status and Transition Model.
5. Promotion Workflow.
6. Relationship Map مع Deferred/Open Decisions/ADR/Capability Catalogue.
7. Reading Matrix.
8. Archive and Historical Inventory Strategy.
9. Documentation-generation eligibility rules.
10. Structured vs Markdown recommendation.
11. Minimal Repository Delta.
12. Owner Decisions.
13. Deferred Items.
14. التوقف دون تعديل.
15. بعد الاعتماد فقط: Prompt لـClaude Code لتنفيذ التحديث التنظيمي.

---

## 26. شكل مخرجات Claude

1. Executive Verdict.
2. Evidence Baseline.
3. Current Registry Map.
4. Gap and Duplication Analysis.
5. Proposed Governance Model.
6. Status/Transition Table.
7. Promotion and Reading Matrix.
8. Archive Strategy.
9. Options and Trade-offs.
10. Recommended Minimal Delta.
11. Owner Decisions.
12. Deferred Items.
13. Acceptance Criteria.
14. Proposed Claude Code Prompt.
15. Stop Statement.

---

## 27. ما لا نريده

- لا جعل كل فكرة Specification.
- لا نسخ الجرد التاريخي مباشرة.
- لا سجل موازٍ بلا حدود.
- لا جعل Coding Agent يقرأ الأفكار غير المعتمدة.
- لا إضافة بيروقراطية ثقيلة.
- لا تعديل AUTHORITY أو INDEX قبل الدراسة.
- لا خلط Capability وFeature وTask وTool.

---

## 28. معايير قبول المراجعة

تُرفض إذا:

- لم تفرق بين Idea وCapability وDeferred وADR وFeature Package.
- لم تحدد Canonical Owner.
- أنشأت ازدواجاً مع السجلات الحالية.
- لم تحدد Reading Matrix.
- عاملت الجرد التاريخي كقائمة معتمدة.
- لم تربط الترقية بالاعتماد والتتبع.
- لم تقدم Evidence من المستودع.
