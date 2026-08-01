# RAR-006 — جاهزية معالجة الأحداث الحية بالذكاء الاصطناعي
## Real-time AI, Event Processing & Live Operational Views Readiness

> **نوع الوثيقة:** Request for Architectural Review (RAR)  
> **المشروع:** AQL / AQLORA Enterprise AI Platform  
> **الحالة الأولية:** Architecture Readiness Only — Deferred Implementation  
> **الغرض:** تهيئة المعمارية للمستقبل دون تنفيذ Pipeline أو اختيار تقنية الآن  
> **قاعدة السلطة:** المستودع الحاكم الفعلي يتقدم على هذا التصور  
> **قاعدة التنفيذ:** لا Broker ولا Streaming ولا Live UI ولا تعديل Repo قبل الدراسة والاعتماد

---

## 1. ملخص تنفيذي

هذه القدرة **ليست للتنفيذ الآن**. نريد تسجيلها كقدرة مستقبلية محكومة وضمان أن العقود والحدود الحالية لا تمنع تنفيذها لاحقاً. التصور المستقبلي هو استقبال بيانات حية، توحيدها، تحليلها بقواعد أو نماذج ذكاء اصطناعي، إنتاج تنبيه أو توصية أو تصنيف، عرضها في Dashboard أو Map أو Timeline، ثم تمرير أي إجراء عبر Action Registry وWorkflow والصلاحيات والتدقيق.

المواد السابقة أشارت إلى أن Real-time AI/Event Readiness غير موثقة بما يكفي. وجود SSE أو Queue في جزء آخر من المشروع لا يعني وجود Event Architecture. المطلوب الآن قد يقتصر على:

- Event terminology.
- Event Contract skeleton.
- Schema versioning.
- Idempotency.
- Correlation/Causation.
- Replay readiness.
- فصل Domain/Integration/Audit events.
- Bounded-context note أو Integration hooks.
- Deferred entry واضحة.

لا نريد اختيار Kafka أو RabbitMQ أو NATS أو أي تقنية، ولا نريد تحويل Modular Monolith إلى Microservices أو Event Sourcing.

---

## 2. نية المنتج المستقبلية

```text
مصادر بيانات حية
→ استقبال وتوحيد البيانات
→ تحقق وإثراء مصرح
→ قواعد وتحليل ونماذج AI
→ تنبيه / توصية / تصنيف / كشف نمط
→ عرض حي: Dashboard / Map / Timeline / Status
→ قرار بشري أو آلي محكوم
→ Action عبر Registry / Workflow
→ إرسال النتيجة إلى نظام آخر أو المصدر
→ Audit وObservability كاملان
```

أمثلة مستقبلية:

- مراقبة تدفق عمليات واكتشاف التأخير.
- خريطة حية لحوادث أو أصول.
- تحديث Dashboard عند وصول أحداث.
- اقتراح إجراء عند تجاوز Threshold.
- تصنيف حدث وربطه بسجل أو شخص.
- فتح Task أو Case أو Workflow من حدث.
- إرسال نتيجة معتمدة إلى النظام المصدر.
- عرض حالة الأنظمة والموصلات لحظياً.

---

## 3. لماذا نسجل الجاهزية الآن

1. منع تصميم APIs وRecords بطريقة لا تقبل Event Correlation لاحقاً.
2. توحيد Identity وTimestamps وSchema Evolution.
3. ضمان أن Action Registry وWorkflow يستطيعان استقبال Triggers مستقبلاً.
4. منع ربط الواجهة بمزود أو Transport محدد.
5. حماية Audit والتفسير وProvenance.
6. الفصل المبكر بين Operational Event وAudit Event وDomain Event.
7. إدراج Idempotency وReplay في العقود المستقبلية.
8. معرفة ما يجب تأجيله صراحة لمنع Over-engineering.
9. دعم إعادة النتائج إلى الأنظمة المصدر بصورة محكومة.
10. عدم إغلاق طريق Live Operational Views.

---

## 4. المبادئ الوظيفية غير القابلة للكسر

1. **Technology-agnostic Event Contract.**
2. **Stable Event Identity.**
3. **Schema Versioning.**
4. **Event Time وIngestion Time** عند الحاجة.
5. **Source Identity وProvenance.**
6. **Correlation وCausation IDs.**
7. **Idempotent Consumers وActions.**
8. **Replay readiness** أو على الأقل عدم منعها.
9. **Ordering assumptions صريحة.**
10. **لا ادعاء Exactly Once** بلا دليل تقني واختبارات.
11. **Audit منفصل عن Operational Events** مع روابط واضحة.
12. **Permissions وData Classification.**
13. **Human in the Loop** للأفعال ذات الأثر حسب السياسة.
14. **Actions تمر عبر Registry.**
15. **لا كتابة مباشرة من LLM.**
16. **Failure وDead-letter semantics** على مستوى المتطلبات، لا الأداة.
17. **Observability.**
18. **Offline deployment compatibility.**
19. **Provider/tool neutrality.**
20. **Retention وPrivacy policies.**
21. **Backpressure وDegradation** يؤخذان في الاعتبار لاحقاً.
22. **لا تحويل كل CRUD إلى Event Sourcing.**

---

## 5. أنواع الرسائل والأحداث المطلوب تمييزها

على Claude تحديد Glossary وحدود بين:

- Domain Event.
- Integration Event.
- Operational Event.
- Audit Event.
- Notification Event.
- Command / Action Request.
- Telemetry / Metric.
- AI Inference Result.
- Alert.
- Recommendation.
- State Snapshot.
- Workflow Trigger.

لا نريد تسمية كل شيء Event. الفرق بين «حدث وقع» و«أمر مطلوب» و«سجل تدقيق» جوهري.

---

## 6. Event Envelope مبدئي للنقاش — ليس Schema معتمداً

```yaml
event:
  event_id: stable-id
  event_type: namespaced-type
  schema_version: version
  source_id: stable-id
  occurred_at: timestamp
  ingested_at: timestamp
  subject:
    type: entity-type
    id: stable-id
  correlation_id: stable-id
  causation_id: stable-id|null
  classification: policy-label
  payload: type-specific
  integrity:
    hash: optional
  trace:
    trace_id: optional
```

المثال يوضح الأسئلة فقط:

- ما الحد الأدنى المشترك؟
- هل Subject دائماً Entity؟
- كيف تمثل Source وTenant/Institution؟
- كيف تمنع Payload غير محكومة؟
- هل تحتاج Integrity Metadata؟
- ما الذي يعد PII أو Sensitive؟
- هل Schema Version على Envelope أم Payload أم كليهما؟

---

## 7. دورة استقبال الحدث

```text
Receive
→ Authenticate source
→ Validate envelope and schema
→ Classify and authorize
→ Deduplicate
→ Persist or stage according to policy
→ Enrich from authorized sources
→ Route to rules/processors
→ Produce result / alert / recommendation
→ Human review or governed action
→ Record outcome and audit
```

على Claude تحديد ما يلزم توثيقه الآن وما يؤجل للImplementation Phase.

---

## 8. AI Processing Pipeline

الذكاء الاصطناعي يجب أن يكون خطوة قابلة للرصد، لا صندوقاً أسود:

1. Event accepted and validated.
2. Enrichment from authorized records.
3. Rule/filter evaluation.
4. Model route selection.
5. Bounded context construction.
6. Inference.
7. Output validation.
8. Evidence/provenance attachment.
9. Confidence/uncertainty policy.
10. Recommendation/alert creation.
11. Human review أو Action policy.
12. Outcome feedback.
13. Audit/metrics.

### أسئلة حاسمة

- هل AI Result Event مستقل؟
- هل نحفظ Model/Version/Prompt Template؟
- كيف نتعامل مع Non-determinism عند Replay؟
- هل Replay يعيد Inference أم يستخدم Archived Result؟
- كيف تمنع Payload من Prompt Injection؟
- كيف تطبق Permissions عند Enrichment؟
- ماذا إذا لم يحقق النموذج Offline زمن الاستجابة المطلوب؟
- كيف توثق Confidence دون اعتباره حقيقة؟

---

## 9. Live Operational Views

المقصود Views تعرض حالة حية أو شبه حية، مثل:

- Dashboard.
- Map.
- Timeline.
- Table.
- Cards.
- Status board.
- Alert queue.

المتطلبات الوظيفية التي يجب التفكير فيها:

- Current state.
- Freshness وLast Update.
- Degraded/Stale/Disconnected states.
- Reconnect/Resume.
- Drill-down إلى Record وEvidence.
- Permissions على كل Item/Field.
- Uncertainty display.
- No side effect from visual control دون Action/Permission.
- Filtering by org unit/record type/source.
- Consistent color semantics.
- Audit عند اتخاذ إجراء من View.
- Mobile/responsive behavior لاحقاً.

لا نريد فرض WebSocket أو SSE أو Polling. Claude يحدد ما هو Contract وما هو Implementation Detail.

---

## 10. Alerts وRecommendations وActions

يجب الفصل بين:

| المفهوم | المعنى |
|---|---|
| Observation | حقيقة أو قيمة واردة من مصدر |
| Alert | حالة تستحق الانتباه وفق Rule/Policy |
| Recommendation | اقتراح قابل للقبول أو الرفض |
| Decision | اعتماد بشري أو آلي محكوم |
| Action | أمر ذو أثر يمر عبر Registry |
| Task/Workflow | متابعة رسمية متعددة الخطوات |

التسلسل يمنع الانتقال المباشر من مخرج Model إلى تحديث خارجي.

---

## 11. Human in the Loop

أنماط مستقبلية:

- View only.
- Acknowledge.
- Accept/Reject recommendation.
- Edit before action.
- Approval workflow.
- Two-person rule.
- Auto-action within safe threshold.
- Rollback/compensation.

لا نريد توثيق كل هذه الأنماط كالتزام. المطلوب تحديد نقاط التكامل والحد الأدنى للجاهزية.

---

## 12. مصادر Ingestion المحتملة

- Connector polling.
- Webhook داخل الشبكة.
- File drops.
- Manual event.
- Internal domain events.
- Message bus لاحقاً.
- Database CDC لاحقاً.
- Device/IoT gateway لاحقاً.

هذه ليست تقنيات مختارة. كل مصدر يجب أن يدخل عبر Adapter/Contract ويخضع للهوية والHealth والصلاحيات والتدقيق.

---

## 13. Idempotency وDeduplication

يجب أن تعرف المعمارية لاحقاً:

- Event identity.
- Source-provided key.
- Deduplication window.
- Duplicate payload with same ID.
- Same logical event with different IDs.
- Retry behavior.
- Idempotent action execution.
- Correlation with Workflow Run.
- Audit of duplicates.

لا نحتاج تنفيذ Store الآن، لكن نحتاج ألا تمنع العقود ذلك.

---

## 14. Ordering وReplay

### Ordering

- هل الترتيب مطلوب per source أم per subject؟
- ماذا يحدث عند Out-of-order Event؟
- هل يوجد Sequence Number؟
- كيف تعرض Live View بيانات متأخرة؟

### Replay

- لماذا يعاد التشغيل؟
- من يملك الصلاحية؟
- ما النطاق الزمني؟
- كيف تمنع Side Effects المكررة؟
- هل AI Inference يعاد؟
- كيف تميز Replay عن Live Processing؟
- كيف تسجل Audit؟

المطلوب Invariants، لا اختيار أداة.

---

## 15. Failure وDegradation

حالات مستقبلية:

- Source unavailable.
- Invalid schema.
- Unauthorized source.
- Duplicate.
- Processor failed.
- Model unavailable.
- Action failed.
- Downstream system unavailable.
- Backlog growing.
- Live view stale.

يجب أن تكون الحالات ظاهرة وقابلة للرصد، مع Retry/Quarantine/Manual Review concepts عند الحاجة.

---

## 16. العلاقة مع Modular Monolith

لا نريد القفز إلى Microservices. Claude يجب أن يوضح كيف يمكن:

- تعريف Event Contracts داخل Modular Monolith.
- استخدام In-process events أو Outbox أو Queue abstraction لاحقاً عند الحاجة.
- الحفاظ على Module boundaries.
- جعل Extraction ممكناً لاحقاً دون تنفيذه الآن.
- عدم جعل Event Bus dependency لكل عملية بسيطة.
- عدم تحويل النظام إلى Event Sourcing.

قد يكون القرار الصحيح هو توثيق Interfaces وInvariants فقط.

---

## 17. العلاقة مع بقية المشروع

- Records/Entity DB.
- Integrations/Connectors.
- Workflow/Tasks.
- Action Registry.
- AI Gateway/RAG.
- Audit/Observability.
- Notifications.
- UI Live Views.
- Permissions.
- Extension Store.
- Offline Deployment.
- Backup/Restore.
- Data Retention.
- Organization/Stable IDs.

على Claude توضيح أين توجد نقاط الربط دون تنفيذها.

---

## 18. سيناريوهات مستقبلية لاختبار الجاهزية

### UC-01 — Event يفتح Workflow
Connector يرسل Event. Rule يقرر فتح Workflow. Idempotency تمنع فتح نسختين.

### UC-02 — AI Recommendation
Event يمر بنموذج، ينتج Recommendation، والإنسان يعتمد قبل إرسال Action للنظام المصدر.

### UC-03 — Live Map
Markers تظهر حسب صلاحيات المستخدم مع Freshness. عند انقطاع المصدر تظهر Degraded ولا تعرض البيانات القديمة كأنها حية.

### UC-04 — Replay
بعد إصلاح Rule، تعاد معالجة أحداث دون تكرار Side Effects.

### UC-05 — Schema Evolution
Source يرسل v2. Consumer يتوافق أو يرفض بوضوح، لا يفشل بصمت.

### UC-06 — Sensitive Event
Payload حساس لا يدخل كاملاً إلى LLM، ويطبق Redaction/Authorized Enrichment.

### UC-07 — Burst
ارتفاع مفاجئ يسبب Backpressure/Degradation معروفاً، لا إسقاطاً صامتاً.

### UC-08 — Offline Model Unavailable
تتوقف مرحلة AI أو تتحول إلى Rule-only، مع حالة واضحة.

### UC-09 — Return to Source
بعد اعتماد التوصية، يرسل Action إلى النظام المصدر مع Correlation وAudit.

---

## 19. الحد الأدنى المطلوب الآن — على Claude تقييمه

قد يشمل:

- Business Glossary.
- Event Contract Template/Skeleton.
- Naming/Versioning rule.
- Idempotency/Correlation invariants.
- Distinction between Audit/Domain/Integration.
- Deferred Register entry.
- Phase mapping.
- Bounded-context note.
- Action/Workflow integration hooks.
- Live View states requirements.
- Test obligations deferred.
- Explicit no-technology-choice statement.

Claude قد يرى أن بعض هذه العناصر مبكر؛ عليه بيان السبب.

---

## 20. الحالة المتوقعة داخل المستودع — تحتاج إثباتاً

تقارير سابقة أشارت إلى:

- Real-time غير مسجل بما يكفي.
- SSE موجود كوسيلة نقل لسيناريو آخر، لا Event Architecture.
- Valkey/Queues قد تكون أساساً تقنياً لكنها ليست قراراً لهذه القدرة.
- Deferred Entry تمت إضافتها أو اقتراحها.
- Event Contract مذكور ضمن العقود المرغوبة، وقد لا يكون ملفاً كاملاً.
- التنفيذ لاحق في مراحل ترتبط بالAutomation/Integrations/Operations.

Claude يجب أن يثبت الوضع الفعلي من `HEAD`.

---

## 21. الفجوات المحتملة — قائمة فحص

- Terminology.
- Event Envelope.
- Schema Registry/Versioning policy.
- Source registration.
- Idempotency.
- Ordering.
- Replay.
- Retention.
- Classification.
- AI Result Provenance.
- Alert/Recommendation/Action separation.
- Human in the Loop.
- Live View states.
- Failure/Quarantine concept.
- Observability.
- Phase/Deferred mapping.
- Acceptance criteria.
- Offline behavior.
- Portability.
- Correlation with Workflow and Actions.
- Return-to-source contract.

---

## 22. الأسئلة المعمارية المفتوحة

1. هل نحتاج Bounded Context للأحداث الآن أم Contracts مشتركة فقط؟
2. من يملك Event Contract؟
3. ما نوع Event ID؟ لا نفترض.
4. هل Subject دائماً Entity؟
5. ما الفرق بين Command وEvent؟
6. كيف يرتبط Audit؟
7. ما Replay Policy للAI؟
8. هل تحفظ Inference Artifacts؟
9. ما الحد الأدنى لـLive View Contract؟
10. هل Event Payload يدخل RAG؟
11. كيف تمنع Duplicate Actions؟
12. هل Outbox Requirement ضروري الآن؟
13. متى يستحق ADR كامل؟
14. ما Phase الصحيح؟
15. ما Trigger الذي ينقل القدرة من Readiness إلى Implementation؟
16. كيف تدار Sensitive Events؟
17. ما علاقة Event Contract بـConnector Contract؟

---

## 23. ما لا نريد فعله الآن

- اختيار Kafka أو RabbitMQ أو NATS أو Pulsar.
- بناء Broker.
- بناء Streaming Pipeline.
- اختيار CEP Engine.
- تنفيذ Live Dashboards.
- Event Sourcing.
- Microservices.
- CDC.
- Data Lake.
- MLOps Platform.
- كتابة Consumers.
- تحديد SLA أرقام بلا قياس.
- ادعاء Real-time بزمن محدد.

---

## 24. المطلوب من Claude Architecture

1. Evidence Baseline.
2. Future Capability Verdict.
3. Minimal Readiness Artifacts.
4. Event Taxonomy.
5. Invariants.
6. Integration Map.
7. Do Now / Prepare Now / Later / Reject Now table.
8. No-Technology-Lock statement.
9. Trigger criteria for future ADR and implementation.
10. Repository Delta.
11. Owner Decisions.
12. Deferred Items.
13. التوقف دون تعديل.
14. بعد الاعتماد فقط: Prompt لـClaude Code لإضافة التوثيق والDeferred references، لا تنفيذ Pipeline.

---

## 25. شكل مخرجات Claude

1. Executive Verdict.
2. Evidence Baseline.
3. Coverage Matrix.
4. Event Taxonomy and Boundaries.
5. Readiness Invariants.
6. Integration Map.
7. Options and Trade-offs.
8. Recommended Minimal Delta.
9. Trigger Criteria.
10. Owner Decisions.
11. Deferred Items.
12. Acceptance Criteria.
13. Proposed Claude Code Prompt.
14. Stop Statement.

---

## 26. ما لا نريده

- لا اختيار Broker.
- لا تحويل إلى Microservices.
- لا اعتبار SSE Event Architecture.
- لا تنفيذ Pipeline.
- لا خلط Audit وEvent وAction.
- لا توثيق تفاصيل مستقبلية غير لازمة.
- لا تعديل Repo أثناء الدراسة.

---

## 27. معايير قبول المراجعة

تُرفض إذا:

- اختارت تقنية.
- تجاهلت Replay وIdempotency.
- لم تفرق بين Event وCommand وAudit.
- أوصت بالتنفيذ الآن.
- لم تسجل القدرة مؤجلة بوضوح.
- لم تحدد Trigger للعودة إليها.
- لم تقدم Evidence من المستودع.
