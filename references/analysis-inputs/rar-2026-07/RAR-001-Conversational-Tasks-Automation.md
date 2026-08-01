# RAR-001 — إنشاء المهام والأتمتة من المحادثة
## Conversational Tasks, Schedules, Workflows & Automation

> **نوع الوثيقة:** Request for Architectural Review (RAR)  
> **المشروع:** AQL / AQLORA Enterprise AI Platform  
> **الحالة الأولية:** Partially Covered — Current Documentation Candidate  
> **الغرض:** تقديم الفكرة إلى Claude Architecture للمراجعة، لا فرض تنفيذ أو معمارية  
> **قاعدة السلطة:** المستودع الحاكم الفعلي عند `HEAD` يتقدم على هذه الوثيقة عند التعارض  
> **قاعدة التنفيذ:** لا تعديل لأي مستودع قبل عرض الدراسة وخطة التغيير واعتماد المالك

---

## 1. ملخص تنفيذي

نريد أن يستطيع المستخدم إنشاء **Task** أو **Schedule** أو **Workflow** أو **Automation** من خلال اللغة الطبيعية، انطلاقاً من محادثة أو شاشة أو سجل يملك صلاحية عليه. لا نريد أن ينفذ النموذج اللغوي العمل مباشرة، ولا أن تصبح المحادثة مساراً موازياً يتجاوز الصلاحيات أو العقود أو Action Registry. المطلوب هو تحويل الطلب الطبيعي إلى **مسودة مورد رسمي محكوم**، ثم التحقق منها وعرض Preview واضح، وبعد ذلك فقط الحفظ أو طلب الاعتماد أو التفعيل بحسب مستوى المخاطر.

الفكرة موثقة جزئياً في المواد السابقة، وتوجد مفاهيم قريبة في المشروع، لكن لم يثبت لدينا أن جميع العقود ودورات الحياة والصلاحيات والاختبارات والتتبع أصبحت مكتملة داخل المستودع. لذلك هذه الوثيقة تطلب من Claude أن يفحص الحقيقة الفعلية، يحدد الموجود والناقص، ويقرر إن كانت القدرة امتداداً لكيانات قائمة أو تحتاج نموذجاً مختلفاً.

---

## 2. نية المنتج

أمثلة لما نريد تمكينه:

- «أرسل طلباً إلى الموظف صاحب الرقم الوظيفي 18432 لتحديث بياناته».
- «أنشئ مهمة لمراجعة هذا العقد قبل يوم الخميس».
- «اطلب المعلومات من ثلاثة موظفين، ثم أخبر المدير بعد اكتمال الجميع».
- «كل صباح أعطني ملخص الأعمال المتأخرة في وحدتي».
- «عند إضافة وثيقة من هذا النوع شغّل التحقق، ثم أرسل النتيجة للمراجع».
- «إذا لم يرد الموظف خلال يومي عمل، صعّد المهمة إلى رئيس القسم».
- «حوّل ما اتفقنا عليه في هذه المحادثة إلى Workflow Draft، لكن لا تنشره قبل أن أراجعه».

الهدف أن تكون المحادثة **نقطة إدخال مبسطة** وليست مصدر حقيقة أو محرك تنفيذ مستقل.

---

## 3. لماذا نحتاج هذه القدرة

### 3.1 تقليل تعقيد الواجهات
المستخدم قد يعرف النتيجة المطلوبة لكنه لا يعرف كيفية تكوين Graph أو Trigger أو Assignment Rule. اللغة الطبيعية تقلل العبء المعرفي.

### 3.2 توحيد المدخلات
بدلاً من شاشات منفصلة لا يعرف المستخدم الفرق بينها، يمكن للمساعد تحديد النوع المناسب ثم إنشاء المورد الرسمي الصحيح.

### 3.3 دعم السياق
عند بدء الطلب من Record أو Screen، يمكن ربطه بالسجل والشاشة والوحدة التنظيمية والمالك والصلاحيات الحالية دون إعادة إدخال كل شيء.

### 3.4 إبقاء التنفيذ محكوماً
النظام لا يسمح للنموذج بكتابة SQL أو كود حر أو استدعاء موصل غير مصرح. كل أثر جانبي يمر عبر آليات معتمدة.

### 3.5 قابلية التدقيق
كل تفسير، Preview، تعديل، اعتماد، تشغيل، فشل، إلغاء أو إعادة محاولة يمكن تتبعه.

---

## 4. التعريفات الأولية التي يجب على Claude مراجعتها

هذه ليست تعريفات قانونية نهائية؛ هي نقطة بداية فقط:

| المصطلح | الفهم الأولي | السؤال المفتوح |
|---|---|---|
| Task | عمل مطلوب من شخص أو جهة، له حالة وموعد | هل هو كيان مستقل أم Work Item مشتق من Workflow؟ |
| Schedule | توقيت أو تكرار لتشغيل عمل | هل هو مورد مستقل أم Trigger داخل Automation؟ |
| Workflow | تعريف مراحل وحالات وتعيينات واعتمادات | كيف يفصل بين Definition وVersion وRun؟ |
| Automation | تشغيل آلي قائم على وقت أو حدث أو شرط | هل هو نوع Workflow أم طبقة Orchestration مستقلة؟ |
| Reminder | تنبيه مرتبط بمورد | Notification فقط أم Task خفيف؟ |
| Request | مطالبة شخص بتقديم بيانات أو قرار | Task أم Form Step أم Case؟ |

المطلوب منع ازدواج مفاهيم تؤدي الوظيفة نفسها بأسماء مختلفة.

---

## 5. المبادئ غير القابلة للكسر

على Claude أن يحدد موضع توثيقها الصحيح، لا أن ينسخها تلقائياً إلى الدستور:

1. **لا تنفيذ مباشر من اللغة الطبيعية.** يوجد تفسير ثم تحقق ثم Preview ثم تأكيد أو اعتماد.
2. **الهوية بالمعرفات الثابتة.** الرقم الوظيفي وسيلة بحث أو مرجع مؤسسي، وليس بديلاً عن الهوية الداخلية المعتمدة.
3. **الصلاحية قبل الاقتراح وقبل التنفيذ.** لا يكفي أن يستطيع المستخدم كتابة الطلب.
4. **لا كشف لبيانات غير مصرح بها في Preview أو رسائل الخطأ.**
5. **كل Action يمر عبر Action Registry أو آلية محكومة مكافئة.**
6. **كل إنشاء وتعديل ونشر وتشغيل وفشل وإلغاء يسجل في Audit.**
7. **لا نشر Workflow أو Automation تلقائياً إذا كان المشروع يفرض بوابة اعتماد.**
8. **الذكاء الاصطناعي منظم ومفسر، وليس مصدر الحقيقة.**
9. **التوقيت يراعي Timezone وتقويم العمل وسياسات العطل.**
10. **Idempotency ومنع التكرار** عند إعادة المحاولة أو إعادة إرسال الطلب.
11. **لا اعتماد على أسماء الإدارات أو مساراتها المتغيرة.** العلاقات التنظيمية بالـIDs الثابتة.
12. **Offline/Air-Gapped first.** لا افتراض لخدمات خارجية.
13. **Prompt Injection لا يغير سياسة النظام أو الصلاحيات أو الأدوات المتاحة.**
14. **التعديل على مورد قائم يحتاج Resolution دقيقاً وImpact Preview.**
15. **التنفيذ القابل للأثر يجب أن يكون قابلاً للإلغاء أو التعويض حيث يلزم.**

---

## 6. السيناريو التشغيلي العام

```text
User request from Chat / Screen / Record
→ Capture permitted context
→ Interpret intent
→ Resolve referenced people, records, units and resources
→ Select candidate resource type
→ Validate contracts, permissions and policies
→ Ask for missing information
→ Build governed draft
→ Show Preview, affected parties, data, schedule, actions and risks
→ User edits / confirms / cancels
→ Approval gate if required
→ Persist official resource
→ Execute through official services
→ Audit, notifications and run history
```

المطلوب من Claude تحديد أي أجزاء موجودة فعلياً، وأين تملك كل مسؤولية.

---

## 7. سيناريوهات الاستخدام التفصيلية

### UC-01 — إنشاء مهمة فردية
المستخدم يذكر موظفاً بالرقم الوظيفي ويحدد المطلوب والموعد. يجب حل المرجع إلى هوية ثابتة وعرض الاسم والوحدة التنظيمية قبل التأكيد.

**الحالات:** رقم غير موجود، أكثر من تطابق، حساب غير نشط، عدم صلاحية، تاريخ غير صالح، تعارض مع سياسة التعيين.

### UC-02 — طلب معلومات من عدة موظفين
قد ينتج Workflow Run واحداً أو مهاماً مترابطة. على Claude تحديد النموذج الذي يمنع تضخم السجلات ويحافظ على تتبع كل مستلم.

### UC-03 — ملخص دوري
طلب «كل صباح» يحتاج Schedule، نطاق بيانات، جهة تسليم، Timezone، وسياسة عدم الإرسال إذا لم يتغير شيء إن كانت مطلوبة.

### UC-04 — Automation قائم على حدث
«عند وصول عقد جديد شغّل الفحص». يجب أن ينتج تعريف Trigger محكوماً، لا ربطاً مباشراً من LLM إلى مصدر البيانات.

### UC-05 — تحويل محادثة إلى Workflow Draft
المحادثة قد تحتوي شروطاً واستثناءات. على النظام استخراج assumptions والأسئلة المفتوحة وعرض Diff عند التعديل.

### UC-06 — بدء الطلب من سجل
يجب حسم هل يحتفظ المورد Snapshot للسياق أم Reference فقط، وكيف يتصرف إذا تغير السجل بعد الإنشاء.

### UC-07 — تعديل أو إيقاف مورد سابق
«أوقف الملخص اليومي» أو «غيّر الموعد». يجب حل المورد المقصود بدقة، وإظهار الأثر، وتطبيق Versioning أو Audit.

### UC-08 — فشل التنفيذ
يجب وجود سياسة Retry وحدود وإشعار وحالة فشل، وعدم إعادة التنفيذ بلا نهاية.

### UC-09 — طلب عالي الأثر
مثل تحديث سجل أو إرسال معلومات حساسة. يحتاج Confirmation إضافي أو Approval أو فصل واجبات.

### UC-10 — عدم توفر النموذج
يجب ألا تختفي القدرة اليدوية الأساسية. على Claude بيان fallback المقبول.

---

## 8. تصور تجربة المستخدم — نقطة نقاش لا قرار

1. يكتب المستخدم الطلب.
2. يعرض المساعد فهمه بلغة واضحة.
3. يقترح النوع: Task / Schedule / Workflow / Automation.
4. يعرض:
   - الأشخاص أو الجهات المتأثرة؛
   - السجلات والبيانات المستخدمة؛
   - الإجراءات؛
   - التوقيت أو الحدث؛
   - الصلاحيات المطلوبة؛
   - الاعتماد المطلوب؛
   - أثر الإلغاء أو التعديل.
5. يبرز assumptions والأسئلة الناقصة.
6. يسمح بـEdit / Confirm / Cancel.
7. بعد التأكيد يعرض رقم المرجع والحالة.
8. يمكن فتح المورد في شاشته الرسمية.

على Claude أن يقرر ما إذا كان Preview مكوناً عاماً، وهل تختلف قوته حسب مستوى المخاطر.

---

## 9. نموذج البيانات والعقود المطلوب تقييمها

لا نفرض Schema، لكن نريد معرفة هل توجد أو نحتاج مفاهيم مثل:

- Intent interpretation record.
- Referenced context.
- Resolution result.
- Draft resource.
- Validation report.
- Preview snapshot.
- Confirmation/approval record.
- Task definition/work item.
- Workflow definition/version/run.
- Schedule/trigger.
- Automation rule.
- Run history.
- Idempotency key.
- Audit events.
- Failure/retry policy.

يجب تحديد المالك القانوني لكل مفهوم ومنع تخزين نفس الحقيقة في Chat وWorkflow وAutomation في آن واحد.

---

## 10. الصلاحيات والاعتماد

المراجعة يجب أن تغطي على الأقل:

- من يملك إنشاء كل نوع؟
- هل يستطيع المستخدم تعيين شخص خارج وحدته؟
- هل يسمح بإنشاء Schedule على بيانات لا يملكها وقت التنفيذ؟
- هل يعاد تقييم الصلاحية عند كل Run؟
- ما الإجراءات التي تتطلب تأكيداً فقط، وما الذي يتطلب Approval؟
- هل يستطيع المستخدم نشر Workflow أم فقط Draft؟
- كيف تعمل Scoped Administration؟
- كيف يظهر سبب الرفض دون كشف بيانات؟
- كيف تسجل Acting on Behalf Of؟

---

## 11. الحالة المتوقعة داخل المستودع — تحتاج إثباتاً

مواد المشروع السابقة تشير إلى:

- وجود Business Glossary أولي للمصطلحات الأربعة.
- وجود Workflow وAction وPermission وAudit foundations.
- وجود Agent-assisted Workflow Builder كفكرة مرتبطة.
- وضع التنفيذ الفعلي لـConversational Automation في مرحلة لاحقة.
- توصية بتجهيز العقود الآن.

على Claude فحص `HEAD` الفعلي والتحقق من:

- هل توجد Contracts للأنواع الأربعة؟
- هل توجد Lifecycles رسمية؟
- هل توجد API Operation Contracts؟
- هل توجد Screen/Route Contracts لنقاط الدخول؟
- هل توجد Permission Verbs واضحة؟
- هل توجد Traceability إلى Phase واختبارات؟
- هل توجد Deferred Entries؟
- هل توجد تعارضات تسمية بين الوثائق؟

---

## 12. الفجوات المحتملة — قائمة فحص لا حكم

- نموذج موارد موحد أو فصل واضح بين الأنواع.
- Draft / Preview / Confirm semantics.
- Intent Interpretation Contract.
- Resolution Contract للأشخاص والسجلات والوحدات.
- Ambiguity handling.
- Permission evaluation في كل مرحلة.
- Approval thresholds.
- Recurrence/Timezone/Business Calendar.
- Event Trigger abstraction.
- Idempotency وإعادة المحاولة.
- Versioning والتعديل والإلغاء.
- Run history وExecution Evidence.
- Notifications.
- ربط Work Queue وInbox.
- Audit Event Catalogue.
- UI states مثل parsing وneeds_input وpreview_ready وapproval_required وfailed.
- Acceptance tests لمنع تجاوز الصلاحيات وكشف البيانات.
- Fallback عند عدم توفر LLM.

---

## 13. العلاقة مع بقية النظام

على Claude رسم العلاقة مع:

- Workflow Module.
- Task/Work Queue.
- Action Registry.
- Permissions وScoped Administration.
- Organization وEmployee Identity.
- Records وDynamic Screens.
- Notifications.
- Audit وObservability.
- Integrations وConnectors.
- AI Gateway وModel Routing.
- Declarative Agent Builder.
- Event Readiness.
- Search وEvidence.

لا نريد إنشاء هذه القدرة كمنصة مستقلة داخل Chat UI.

---

## 14. الأسئلة المعمارية المفتوحة

1. هل Task مورد مستقل أم تجسيد مبسط لـWorkflow؟
2. ما الحد بين Schedule وAutomation Trigger؟
3. أين تخزن صياغة المستخدم الأصلية؟
4. هل تحفظ خطة LLM الوسيطة؟ وكيف تمنع اعتبارها حقيقة؟
5. ما نموذج التحقق Deterministic؟
6. كيف تربط Preview بنسخة العقود التي تحققت عليها؟
7. هل كل تعديل ينتج Version جديداً؟
8. ما الذي يمكن نشره دون Admin؟
9. كيف تعالج Cross-Org Assignment؟
10. هل نحتاج Dry Run؟
11. ما الحد الأدنى المطلوب الآن إذا كان التنفيذ مؤجلاً؟
12. هل تحتاج ADR أم Contracts فقط؟
13. كيف تعمل عند عدم توفر LLM؟
14. كيف تمنع Prompt Injection من مستند أو سجل؟
15. كيف يمثل شرط «عندما يكتمل الجميع» بشكل قابل للاختبار؟

---

## 15. خارج النطاق في هذه الجولة

- بناء UI أو Backend.
- اختيار Scheduler أو Message Broker.
- اختيار مكتبة Orchestration.
- السماح بكود حر أو SQL مولد.
- تشغيل Automation فعلي.
- إعادة تصميم Workflow Builder.
- توثيق الجرد التاريخي الكامل للميزات.
- تحديد النصوص النهائية للواجهة.

---

## 16. المطلوب من Claude Architecture

1. قراءة المستودع الحاكم وقرارات السلطة والـADRs والعقود والمراحل والـDeferred Register.
2. تقديم Evidence Baseline بمسارات ونسخ واضحة.
3. تصنيف كل جزء: Fully Covered / Partially Covered / Not Recorded / Deferred / Superseded / Rejected / Owner Decision.
4. تحديد إن كانت القدرة امتداداً لكيان موجود أو تحتاج bounded context أو contract suite جديداً.
5. تقديم Domain Concept Map للمصطلحات الأربعة.
6. تقديم Lifecycle Matrix.
7. تقديم Permission & Approval Matrix أولية.
8. تقديم Conversation-to-Governed-Resource sequence.
9. تحديد أقل تغيير توثيقي كافٍ الآن.
10. تحديد ما يؤجل إلى مرحلة التنفيذ.
11. عرض البدائل والتبعات.
12. التوقف وانتظار اعتماد المالك.
13. بعد الاعتماد فقط، كتابة Prompt مستقل لـClaude Code لتحديث المستودع.

---

## 17. شكل مخرجات Claude الإلزامي

1. Executive Verdict.
2. Evidence Baseline.
3. Coverage Matrix.
4. Architectural Interpretation.
5. Options and Trade-offs.
6. Recommended Direction.
7. Repository Impact Map.
8. Required Owner Decisions.
9. Deferred / Out-of-Scope Items.
10. Acceptance Criteria for Documentation Update.
11. Proposed Claude Code Prompt في ملحق مستقل.
12. Stop Statement يؤكد أنه لم يعدل أي مستودع.

---

## 18. ما لا نريده من Claude

- لا تنفيذ مباشر.
- لا اختراع أسماء ملفات قبل فحص البنية.
- لا اختيار تقنية لمجرد شهرتها.
- لا إنشاء Microservices أو قاعدة منفصلة.
- لا خلط Chat مع Source of Truth.
- لا اعتبار التصور الوارد هنا قراراً نهائياً.
- لا تكرار الحقيقة في عدة ملفات بلا Canonical Owner.
- لا كتابة Prompt تنفيذ قبل اعتماد الدراسة.

---

## 19. معايير قبول المراجعة

تُرفض المراجعة إذا:

- افترضت أن Chat يملك صلاحية التنفيذ.
- لم تفرق بين Task وWorkflow وAutomation.
- لم تربط الهوية والصلاحيات والتدقيق.
- اختارت تقنية قبل إثبات الحاجة.
- لم تحدد وضع القدرة: Now / Prepare Now / Later.
- أعلنت التغطية بلا Evidence.
- كتبت Prompt لـClaude Code قبل حسم قرارات المالك.
