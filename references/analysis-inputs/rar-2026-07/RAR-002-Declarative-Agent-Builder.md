# RAR-002 — منشئ الوكلاء التصريحي للمستخدم
## Declarative Agent Builder for Governed AI Workers

> **نوع الوثيقة:** Request for Architectural Review (RAR)  
> **المشروع:** AQL / AQLORA Enterprise AI Platform  
> **الحالة الأولية:** Not Fully Specified — Current Product/Architecture Review Candidate  
> **الغرض:** عرض نية المنتج وأسئلة المراجعة دون فرض Schema أو Runtime أو تقنية  
> **قاعدة السلطة:** المستودع الحاكم الفعلي عند `HEAD` يتقدم على هذه الوثيقة  
> **قاعدة التنفيذ:** Claude Architecture يدرس ويقترح؛ Claude Code لا يعدل إلا بعد اعتماد المالك

---

## 1. ملخص تنفيذي

نريد تمكين المستخدم غير التقني من إنشاء **AI Worker / Agent** محكوم عبر واجهة مبسطة تعتمد على اللغة الطبيعية، مع إخفاء العقد والرسوم والموصلات والتعقيد التشغيلي. يقدم المستخدم تعليمات العمل، ويختار مصادر معرفة مصرحاً بها، ويفعّل Skills جهزها الأدمن مسبقاً، ثم يجرب النتيجة في Test Panel قبل طلب النشر أو الاعتماد.

الفكرة واضحة من ناحية UX، لكن لم يثبت بعد هل هي:

- واجهة مبسطة فوق قدرات موجودة؛
- مورد Domain جديد باسم Agent Definition؛
- Template/Profile داخل AI Workspace؛
- طبقة فوق Workflow Builder؛
- أو قدرة يجب إعادة تعريفها بشكل مختلف.

المطلوب من Claude أن يحدد المالك المعماري الصحيح، والعقود اللازمة، وعلاقة Agent بالـWorkflow والـAutomation والـRAG والـAction Registry والـProvider/Capability Registry، وأن يمنع تحول Prompt المستخدم إلى سياسة أمنية أو صلاحية تنفيذ.

---

## 2. نية المنتج

المستخدم يستطيع:

1. كتابة **Instructions** بلغة طبيعية.
2. إضافة **Knowledge Sources** من مصادر معتمدة.
3. تفعيل **Skills / Tools** جاهزة ضمن صلاحياته.
4. اختيار طريقة الاستدعاء أو Trigger إذا كان ذلك مسموحاً.
5. التجربة في **Test Panel** أو Dry Run.
6. البدء من **Template** معتمد.
7. حفظ Draft.
8. إرسال طلب اعتماد أو نشر وفق دوره.
9. رؤية الحالة والنسخة والمالك والاعتماديات.
10. تعطيل Agent أو إنشاء Version جديدة وفق السياسة.

المستخدم لا يرى:

- API keys.
- Secret values.
- SQL.
- System prompts الداخلية.
- Connector internals.
- صلاحيات غير ممنوحة.
- Model infrastructure details.

---

## 3. لماذا نحتاج هذه القدرة

### 3.1 تمكين الأقسام
الأقسام تستطيع تكوين مساعدين مخصصين دون انتظار فريق التطوير لكل حالة صغيرة.

### 3.2 إعادة استخدام القدرات
المعرفة والـSkills والـTemplates المعتمدة تستخدم عبر عدة Agents.

### 3.3 تقليل تعقيد Workflow Builder
المستخدم الذي لا يحتاج التحكم بكل Node لا يجب إجباره على Canvas معقد.

### 3.4 فصل النية عن التنفيذ
المستخدم يصف المطلوب، والنظام يحول الوصف إلى Runtime Policy محكومة.

### 3.5 الحوكمة والتدقيق
كل Agent يصبح مورداً معروفاً له مالك وVersion وحالة وصلاحيات وAudit.

### 3.6 قابلية الاختبار
Test Panel يسمح باكتشاف السلوك قبل النشر.

---

## 4. الفرق المطلوب حسمه بين Agent Builder وWorkflow Builder

التصور الأولي:

| البعد | Declarative Agent Builder | Workflow Builder |
|---|---|---|
| الجمهور | مستخدم غير تقني أو Power User | Admin / Process Designer |
| المدخل | Instructions + Knowledge + Skills | Nodes + States + Edges + Conditions |
| الواجهة | نموذج مبسط، بلا Graph افتراضياً | Canvas أو محرر متقدم |
| الناتج | Agent Definition محكوم | Workflow Definition / Version |
| التحكم | مقيد بما جهزه الأدمن | أوسع وفق الدور |
| النشر | طلب اعتماد أو نشر محدود | نشر إداري محكوم |
| التنفيذ | عبر Runtime Policy وRegistries | عبر Workflow Engine |

لكن هذا ليس قراراً نهائياً. على Claude تحديد:

- هل Agent يستطيع استدعاء Workflow معتمد؟
- هل Agent نفسه ينشئ Workflow؟
- هل بعض Agents مجرد Configurations لنفس Runtime؟
- هل Agent Builder مجرد View مبسط لنفس Metadata؟
- ما الذي لا ينبغي أن يفعله Agent Builder أبداً؟

---

## 5. المبادئ غير القابلة للكسر

1. **لا امتياز من Prompt.** النص لا يمنح صلاحية.
2. **Skills تأتي من Registry معتمد.** المستخدم يفعّل subset مما تسمح به سياساته.
3. **Knowledge selection تخضع لصلاحيات المصدر وObject/Row/Field Security.**
4. **لا أسرار في الواجهة أو تعريف Agent.**
5. **رفع ملف لا يعني السماح الدائم باستخدامه.** يخضع للتصنيف والاحتفاظ والفحص.
6. **الصلاحيات يعاد تقييمها وقت التنفيذ** حيث يلزم.
7. **Prompt Injection لا يغير System Policy أو Tool Scope.**
8. **الكتابة إلى النظام تمر عبر Actions محكومة وتأكيد أو اعتماد.**
9. **الإجابات المؤسسية تستند إلى Evidence.**
10. **Offline/Air-Gapped first.**
11. **Provider-agnostic.** لا يرتبط تعريف Agent بمزود أو نموذج واحد.
12. **Versioning وAudit** للتعليمات والمعرفة والSkills والاختبارات والنشر.
13. **الاسم والوصف ليسا هوية.** الموارد بالـIDs الثابتة.
14. **Agent ليس مستخدماً بشرياً تلقائياً.** يجب حسم Runtime Principal وDelegation.
15. **لا نشر تلقائي من مخرج LLM.**
16. **Memory ليست حقيقة معتمدة.** الحقائق من DB/Evidence وفق سياسة المشروع.
17. **تعطيل Skill أو Source يجب أن يؤثر فوراً وفق السياسة.**
18. **Agent لا يتجاوز Owning Org Unit أو Scoped Administration.**

---

## 6. مكونات UX المراد تقييمها

### 6.1 Identity and Status

- اسم Agent.
- وصف مختصر.
- المالك.
- `owning_org_unit_id` أو النموذج القانوني المعتمد.
- الحالة: Draft / In Review / Published / Disabled / Archived.
- النسخة.
- آخر تعديل.
- مصدر Template إن وجد.

### 6.2 Instructions

مساحة كتابة موجهة بلغة الأعمال، مع:

- أمثلة.
- قيود.
- صياغة الهدف.
- ما يجب وما لا يجب فعله.
- اقتراحات تحسين اختيارية.
- تحذير عند الغموض أو التعارض.

السؤال: هل تخزن كنص فقط، أم تتحول أيضاً إلى Structured Constraints؟

### 6.3 Knowledge

- Add Knowledge.
- اختيار مصدر معتمد: ملفات، Collections، Records، Connectors، Folders، مواقع داخلية.
- عرض نطاق الوصول.
- عرض حالة Ingestion/Indexing.
- تحذير للمصادر الحساسة.
- إزالة Binding دون حذف الأصل.
- بيان Freshness وسياسة التحديث.

### 6.4 Skills / Tools

قائمة جاهزة قد تشمل:

- Search records.
- Retrieve documents.
- Generate report.
- Request information.
- Send notification.
- Create task.
- Start approved workflow.
- Call approved connector.
- Export document.

كل Skill يجب أن يظهر الوصف والأثر والبيانات التي يصل إليها ومتطلبات التأكيد أو الاعتماد.

### 6.5 Test Panel

- Chat تجريبي مرتبط بنسخة Draft.
- Dry Run للأفعال ذات الأثر.
- إظهار الأدوات المقترحة دون تنفيذ عند الحاجة.
- Evidence.
- أسباب الرفض أو الحجب.
- Test traces بسياسة احتفاظ.
- Test Cases محفوظة.
- مقارنة السلوك بين Versions.

### 6.6 Publish / Request Approval

- Diff عن النسخة المنشورة.
- Knowledge وSkills التي تغيرت.
- المخاطر.
- الجهات المتأثرة.
- صلاحيات مطلوبة.
- نتائج الاختبار.
- قرار Approve / Reject / Return for Changes.

هذه المكونات نقطة بداية فقط. Claude يقرر الهيكل الصحيح ولا يفرض Layout حرفياً.

---

## 7. نموذج مورد مبدئي للنقاش — ليس Schema معتمداً

```yaml
agent_definition:
  id: stable-id
  version: version
  name: display-name
  owner_user_id: stable-id
  owning_org_unit_id: stable-id
  status: draft|in_review|published|disabled|archived
  instructions:
    user_intent: text
    structured_constraints: []
  knowledge_bindings:
    - source_id: stable-id
      access_mode: read
      retrieval_policy_id: stable-id
  skill_bindings:
    - capability_id: stable-id
      enabled: true
      policy_id: stable-id
  invocation_policy:
    allowed_channels: []
  runtime_policy_id: stable-id
  approval_policy_id: stable-id
  audit_metadata: {}
```

المثال يوضح المفاهيم فقط. لا نريد فرض أسماء الحقول أو JSON Blob إذا كانت المعمارية الحالية أفضل بنموذج آخر.

---

## 8. Translation / Compilation Layer

الفكرة التي تحتاج مراجعة:

```text
User Agent Definition
→ Validate ownership and policy
→ Resolve knowledge bindings
→ Resolve allowed skills
→ Compile runtime policy
→ Build bounded prompt/context
→ Execute via AI Gateway
→ Enforce tool calls server-side
→ Retrieve evidence
→ Require confirmation/approval for side effects
→ Record audit and trace
```

الأسئلة:

- هل Compile ينتج Artifact ثابتاً لكل Version؟
- هل Runtime يعيد بناء الخطة عند كل تشغيل؟
- كيف نثبت أن Skills ما زالت مسموحة؟
- ماذا يحدث إذا تغير Connector أو Source؟
- هل يحتاج Agent Dependency Graph؟
- هل يمكن Agent استدعاء Agent آخر؟ وهل يجب تأجيله؟
- أين تقع مسؤولية Model Routing؟
- كيف نمنع Instructions من إعادة تعريف System Policy؟
- هل Prompt النهائي Artifact قابل للمراجعة أم يولد ديناميكياً؟

---

## 9. الهوية التنفيذية والصلاحيات

هذه من أهم نقاط المراجعة:

### 9.1 Creator Identity
من أنشأ Agent ومن يملكه.

### 9.2 Runtime Principal
من ينفذ فعلياً:

- باسم المستخدم الحالي؟
- Service Principal؟
- Delegated Identity؟
- Agent Identity محدودة؟

### 9.3 Authorization Time
هل تتحقق الصلاحيات:

- وقت إنشاء Binding؟
- وقت النشر؟
- عند كل Run؟
- قبل كل Tool Call؟

### 9.4 Scope

- المؤسسة.
- الوحدة التنظيمية.
- السجل.
- الصف.
- الحقل.
- Connector Scope.
- Action Scope.

على Claude تقديم نموذج واضح يمنع Privilege Escalation ويشرح Acting on Behalf Of.

---

## 10. Agent Templates

نرى حاجة محتملة إلى:

- قوالب مؤسسية معتمدة.
- قوالب خاصة بالوحدة.
- Clone as Draft.
- Versioned Template.
- Required Skills.
- Optional Knowledge slots.
- Test Suite مرفقة.
- Deprecation.
- Migration guidance.
- Usage analytics محكومة.

الأسئلة:

- هل Template كيان مستقل أم Agent Version مصنف؟
- هل النسخ تورث التحديث أم تنسخ فقط؟
- كيف تمنع تحديث Template من كسر Agents المنشورة؟
- هل القالب يمنح صلاحيات؟ يجب ألا يفعل.

---

## 11. طلب إنشاء Agent من الأدمن

سيناريو مطلوب عندما لا يملك المستخدم صلاحية الإنشاء أو يحتاج Skills غير متاحة:

1. المستخدم يكتب الهدف.
2. يحدد المعرفة المطلوبة.
3. يحدد ما يود أن يفعله Agent.
4. النظام يحلل الطلب دون إنشاء فعلي.
5. يرسل Request إلى Admin/Approver.
6. الأدمن يراجع المخاطر والـSkills والSources.
7. يقبل أو يعدل أو يرفض مع السبب.
8. عند القبول ينشأ Draft مملوكاً وفق السياسة.

على Claude تقرير هل هذه Workflow عادية أم Capability مستقلة.

---

## 12. دورة الحياة المحتملة

```text
Draft
→ Validation Failed / Ready for Test
→ In Review
→ Approved
→ Published
→ Disabled
→ Archived
```

حالات جانبية محتملة:

- Dependency Missing.
- Knowledge Updating.
- Policy Conflict.
- Degraded.
- Revoked.
- Pending Revalidation.

نطلب من Claude تحديد الحد الأدنى، ومن يملك Transitions، والفرق بين Disable وArchive وRevoke.

---

## 13. سيناريوهات الاستخدام التفصيلية

### UC-01 — Agent بحث داخلي
يختار المستخدم مجموعة عقود ويطلب تلخيص الالتزامات مع Evidence، دون Actions كتابية.

### UC-02 — Agent يطلب معلومات
يستخدم Skill معتمدة لإنشاء Task، لكنه يعرض Preview قبل الإرسال.

### UC-03 — قالب موارد بشرية
الأدمن ينشر Template، والمستخدم ينسخه ويقيد المعرفة بنطاق وحدته.

### UC-04 — طلب Agent من الأدمن
المستخدم لا يملك Create/Publish، فيقدم Request رسمياً.

### UC-05 — رفض صلاحية
Agent يرفض الوصول إلى Record غير مصرح دون كشف تفاصيل حساسة.

### UC-06 — تغير مصدر معرفة
Source أزيل أو تغيرت صلاحياته. يظهر Agent Degraded أو Binding Invalid.

### UC-07 — Skill عالية الأثر
Skill تحديث سجل تحتاج Human Confirmation في كل Run أو Approval وفق السياسة.

### UC-08 — Template Update
يجب تحديد أثر التحديث على النسخ.

### UC-09 — Revocation
اكتشاف مشكلة في Skill يؤدي إلى تعطيلها في كل Agents المرتبطة، مع Audit وإشعار.

### UC-10 — Offline Runtime
النموذج الأساسي غير متاح، فيتحول إلى Provider بديل معتمد أو يرفض بوضوح.

---

## 14. الأمن والعزل

المراجعة يجب أن تعالج:

- Institution/Tenant isolation إن كان موجوداً.
- Org-unit scoped administration.
- Creator vs Runtime Principal.
- Least privilege.
- Connector scopes.
- Row/Object/Field permissions.
- Secret handling.
- Prompt Injection from knowledge.
- Tool output sanitization.
- Data exfiltration prevention.
- Outbound network restrictions.
- File scanning/classification.
- Audit and non-repudiation.
- Rate/usage quotas.
- Model/provider policy.
- Session memory vs verified facts.
- Test sandbox boundaries.
- Sensitive output redaction.
- Cross-agent data leakage.

---

## 15. العلاقة مع بقية المشروع

على Claude توضيح العلاقة مع:

- AI Workspace / Chat.
- Workflow Builder.
- Conversational Tasks & Automation.
- Provider/Capability Registry.
- Action Registry.
- Connectors.
- RAG/Evidence.
- Permissions.
- Audit.
- Templates.
- Dynamic Screens.
- Notifications.
- Model Routing.
- Offline Deployment.

---

## 16. الحالة المتوقعة داخل المستودع — تحتاج إثباتاً

المواد التاريخية تشير إلى:

- Workflow Builder موجود جزئياً.
- Agent-assisted Workflow Builder مذكور.
- Declarative end-user UX موصوف في ملف مستقل.
- Provider/Capability Registry اتجاه معماري قائم.
- Contracts Layer وBusiness Glossary وUI Governance أضيفت.
- Rocket يحتوي شاشات تجريبية لكنه ليس Source of Truth.
- لا إثبات كافٍ على Agent Contract أو Agent Lifecycle كامل.

Claude يجب أن يفحص actual HEAD ولا يعتمد على هذا الملخص.

---

## 17. الفجوات المحتملة — قائمة فحص

- Agent Definition Contract.
- Agent Template Contract.
- Knowledge Binding Contract.
- Skill/Capability Binding Contract.
- Runtime Identity/Delegation.
- Compile/Validation Model.
- Draft/Test/Publish Lifecycle.
- Test Case/Result Model.
- Dependency Versioning.
- Approval Policy.
- Agent Request Workflow.
- Screen وRoute Contracts.
- Audit Event Catalogue.
- Error/Degraded States.
- Traceability إلى Phase.
- Offline Provider Fallback.
- Isolation وPrompt Injection Acceptance Tests.
- Relationship to Memory وEvidence.
- Revocation semantics.
- Agent dependency impact analysis.

---

## 18. الأسئلة المعمارية المفتوحة

1. هل Agent مورد Domain أم UI Configuration؟
2. هل يحتاج Bounded Context جديداً؟
3. هل ينفذ باسم المستخدم أم Service Principal؟
4. هل يمكن أن يعمل مجدولاً دون مستخدم حاضر؟
5. ما الفرق بين Agent وAssistant وWorker وWorkflow؟
6. هل Templates تورث أم تنسخ؟
7. كيف يمثل Dependency Compatibility؟
8. هل Test Panel يستخدم بيانات حقيقية أم Fixtures؟
9. هل إضافة Knowledge تحتاج Approval؟
10. كيف يعرض أثر Skill؟
11. كيف يمنع Skill معطلة من Tool Call فوراً؟
12. هل تحتاج ADR أم Contract Suite؟
13. ما الذي يوثق الآن وما يؤجل؟
14. كيف يتعايش مع Open WebUI المؤقت؟
15. متى يسمح لـRocket بتصميم الشاشة؟
16. هل Agent يمكنه استدعاء Workflow منشور فقط؟
17. هل Instructions تحتاج Structured Policy منفصلة؟

---

## 19. خارج النطاق

- بناء Agent Runtime.
- اختيار LangGraph أو أي Framework.
- بناء UI.
- Agent-to-Agent.
- Memory طويلة الأمد بلا سياسة.
- Marketplace عام للقوالب.
- Fine-tuning.
- External SaaS dependency.
- Autonomous unrestricted agents.
- نشر Agent فعلي.

---

## 20. المطلوب من Claude Architecture

1. Evidence Baseline من المستودع.
2. Terminology Decision: Agent/Worker/Assistant.
3. Domain Ownership Decision.
4. Resource and Lifecycle Model.
5. Security/Identity Model.
6. Translation Layer Responsibilities.
7. UX-to-Contract Traceability.
8. Template and Request Model Recommendation.
9. Current / Prepare Now / Later separation.
10. Minimal Repository Delta.
11. Deferred Capabilities.
12. Test Obligations.
13. Owner Decisions.
14. التوقف دون تعديل.
15. بعد الاعتماد فقط: Prompt لـClaude Code لتوثيق القرار.

---

## 21. شكل مخرجات Claude

1. Executive Verdict.
2. Evidence Baseline.
3. Coverage Matrix.
4. Agent vs Workflow Boundary.
5. Identity and Security Model.
6. Options and Trade-offs.
7. Recommended Architecture Direction.
8. Repository Impact Map.
9. Owner Decisions.
10. Deferred Items.
11. Acceptance Criteria.
12. Proposed Claude Code Prompt.
13. Stop Statement.

---

## 22. ما لا نريده

- لا اعتبار Prompt سياسة أمنية.
- لا ربط Agent بمزود LLM واحد.
- لا إنشاء Graph مخفي دون Contract واضح.
- لا تنفيذ قبل اعتماد العقود.
- لا نسخ نموذج Microsoft أو غيره حرفياً.
- لا إضافة Secrets أو API Keys إلى الواجهة.
- لا جعل Template يمنح صلاحيات.
- لا تعديل مستودع في مرحلة الدراسة.

---

## 23. معايير قبول المراجعة

تُرفض إذا:

- لم تفرق بين المنشئ والهوية المنفذة.
- لم تعالج Revocation للKnowledge/Skills.
- تجاهلت Workflow وAutomation وAction Registry.
- اقترحت Runtime قبل تعريف الحدود.
- لم تعالج Prompt Injection وLeast Privilege.
- لم تحدد ما هو Now وما هو Deferred.
- لم تقدم Evidence.
