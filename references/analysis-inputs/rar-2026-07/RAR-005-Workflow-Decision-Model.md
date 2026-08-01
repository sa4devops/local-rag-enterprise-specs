# RAR-005 — نموذج قرارات وتعيينات سير العمل
## Workflow Decision, Assignment, Confidential Notes, Delegation & Escalation

> **نوع الوثيقة:** Request for Architectural Review (RAR)  
> **المشروع:** AQL / AQLORA Enterprise AI Platform  
> **الحالة الأولية:** Partially Covered / Not Fully Specified — Current Documentation Candidate  
> **الغرض:** حسم السلوك الوظيفي والحوكمي لقرارات Workflow دون فرض تصميم Engine  
> **قاعدة السلطة:** العقود والـADRs والمراحل الفعلية تتقدم على هذه الوثيقة  
> **قاعدة التنفيذ:** لا تعديل مستودع ولا تنفيذ Engine قبل دراسة واعتماد

---

## 1. ملخص تنفيذي

المشروع يحتوي على Workflow Builder ومفاهيم Approvals وAssignments وActions وOwning Organizational Unit وRBAC وAudit، لكن توجد تفاصيل سلوكية مهمة لم يثبت اكتمالها، مثل:

- First Decision Wins.
- التعيين لفرد أو مجموعة أو دور.
- البحث عن الموظف بالرقم الوظيفي ثم التخزين بالهوية الثابتة.
- Delegation وActing on Behalf Of.
- Escalation وSLA.
- Reassignment.
- Confidential أو Restricted Notes.
- ماذا يحدث لبقية المستلمين بعد حسم أول قرار.
- الفصل بين Comment وDecision.
- السلوك عند تزامن قرارات متعارضة.

هذه ليست تفاصيل UI فقط؛ بعضها Invariants وعقود بيانات وصلاحيات وتدقيق واختبارات قبول. المطلوب من Claude تحديد النموذج الصحيح، وليس اعتماد First Decision Wins كقاعدة عامة.

---

## 2. نية المنتج

نريد Workflow يستطيع تمثيل:

- خطوة مخصصة لموظف محدد.
- خطوة مخصصة لدور داخل وحدة تنظيمية.
- خطوة ترسل إلى Queue أو مجموعة.
- خطوة تحتاج قراراً واحداً أو عدة قرارات.
- أول قرار حاسم أو إجماع أو نسبة أو تسلسل.
- تفويض مؤقت أو خاص بمهمة.
- تصعيد بعد تجاوز SLA.
- إعادة تعيين محكومة.
- ملاحظات عامة أو داخلية أو مقيدة.
- Audit كامل للهوية والقرار والسبب والوقت والسياق.

المستخدم قد يبحث عن الموظف بالرقم الوظيفي، لكن العلاقات النهائية يجب أن تعتمد على IDs ثابتة. نقل الوحدة التنظيمية لا يغير هوية المستخدم أو Workflow أو علاقاته، وإنما يغير علاقات الملكية التنظيمية وفق النموذج المعتمد.

---

## 3. First Decision Wins — المقصود والحدود

مثال: خطوة أرسلت إلى ثلاثة أعضاء. يكفي قرار واحد. أول قرار صالح يحسم الخطوة. بعد ذلك قد يحدث أحد الآتي:

- تنتهي صلاحية القرار للبقية فوراً.
- تبقى القراءة فقط.
- يسمح بالتعليق دون القرار.
- تغلق Work Items التابعة.
- تسجل محاولة أي قرار متأخر دون تغيير النتيجة.

لكن توجد أنماط أخرى يجب عدم خلطها:

- Single Assignee.
- First Response Wins.
- Any Approve.
- Any Reject.
- All Must Approve.
- Majority.
- Quorum.
- Sequential Approval.
- Role Priority.
- Parallel Independent Decisions.
- Advisory Comments + Final Approver.

على Claude تحديد هل Decision Rule جزء من Step Definition، أم Registry، أم نوع Workflow Step، وما يدخل MVP وما يؤجل.

---

## 4. المبادئ غير القابلة للكسر

1. **Stable IDs.** لا تخزن الأسماء أو المسارات التنظيمية كهوية.
2. **Server-side authorization.** إخفاء زر في UI لا يكفي.
3. **Decision immutability after finalization** إلا Override محكوم لا يمحو التاريخ.
4. **Audit شامل** للقرار والتعيين والتفويض والتصعيد والملاحظات.
5. **Separation of Duties** عند الحاجة.
6. **LLM لا يقرر باسم شخص** إلا ضمن Automation Policy معتمدة صراحة.
7. **Race-safe semantics** للقرارات المتزامنة.
8. **Idempotency** للنقرات وإعادة الطلب.
9. **Reason/Evidence** حسب نوع القرار.
10. **Time/Timezone consistency.**
11. **Confidentiality enforced في Backend.**
12. **Assignments قابلة للتفسير.**
13. **Workflow Definition المنشور لا يتغير بأثر رجعي على Runs قائمة** إلا وفق Versioning واضح.
14. **الحالات النهائية لا تتغير بصمت.**
15. **القرار الآلي أو البشري يمر عبر Action/Permission/Audit.**

---

## 5. التعيين والهوية

طرق اختيار المستلم قد تشمل:

- الرقم الوظيفي.
- الاسم مع Disambiguation.
- User ID.
- Role.
- Organizational Unit.
- Group.
- Team.
- Manager of Record.
- Owner of Record.
- Queue.
- Expression محكومة.

لكن العقد النهائي يجب أن يخزن هوية ثابتة، مع Resolution Context عند الحاجة.

### أسئلة مطلوبة

- ماذا يحدث إذا انتقل الموظف إلى وحدة أخرى؟
- ماذا يحدث إذا غادر المؤسسة أو عطل حسابه؟
- هل Assignment Snapshot وقت إنشاء Run أم Dynamic؟
- هل Role يعاد حله وقت التنفيذ؟
- هل `owning_org_unit_id` يختلف عن Assigned Unit؟
- كيف يمنع Cross-Scope Assignment بلا صلاحية؟
- هل الرقم الوظيفي Unique على مستوى المؤسسة أو الجهة؟
- كيف يعالج أكثر من تطابق؟

---

## 6. نموذج Step يحتاج مراجعة

لا نفرض Schema، لكن نريد تقييم مفاهيم مثل:

- Assignment strategy.
- Candidate assignees.
- Decision rule.
- Completion rule.
- Allowed outcomes.
- Required reason.
- Required evidence.
- SLA.
- Escalation policy.
- Delegation policy.
- Comment policy.
- Visibility policy.
- Conflict-of-interest policy.
- Post-decision behavior.
- Notification policy.
- Override policy.

يجب الفصل بين:

- Workflow Definition.
- Workflow Version.
- Workflow Run.
- Step Run.
- Work Item.
- Assignment Record.
- Decision Record.
- Comment/Note.

Claude يحدد ما هو ضروري وما هو زائد.

---

## 7. أنماط القرار المطلوب تحليلها

| النمط | الوصف | السؤال المطلوب |
|---|---|---|
| Single Assignee | شخص واحد يحسم | هل هو Default؟ |
| First Decision Wins | أول قرار صالح يحسم | ماذا يحدث للبقية؟ |
| Any Approve | أول اعتماد يحسم، الرفض لا يحسم | متى تنتهي الخطوة؟ |
| Any Reject | أول رفض يحسم | ما أثر الاعتمادات السابقة؟ |
| All | الجميع مطلوب | ماذا عند غياب عضو؟ |
| Majority | الأغلبية | كيف تحسب Tie وQuorum؟ |
| Quorum | عدد أدنى | هل العضوية Snapshot؟ |
| Sequential | ترتيب محدد | ماذا عند Skip أو Delegation؟ |
| Advisory + Final | تعليقات ثم مسؤول نهائي | الفصل بين Comment وDecision |
| Automated Recommendation | AI يقترح والإنسان يقرر | Evidence وAudit |

على Claude اقتراح مجموعة MVP وعدم توثيق كل نمط كالتزام حالي إن لم نحتاجه.

---

## 8. Work Items وGroup Assignment

نماذج محتملة:

1. Assign to Queue؛ أول من Claims يصبح Assignee.
2. Broadcast Work Item لكل عضو.
3. Candidate Group؛ شخص واحد يقرر.
4. Committee؛ عدة قرارات.
5. Role داخل Owning Unit.
6. Dynamic Group Snapshot وقت التشغيل.
7. Dynamic Membership وقت القرار.

المطلوب حسم:

- هل Work Item كيان مستقل؟
- هل لكل مستلم Work Item أم هناك Work Item مشترك؟
- كيف تغلق العناصر بعد الحسم؟
- كيف تمنع Double Claim؟
- كيف تحفظ Traceability؟
- كيف تتعامل مع تغير أعضاء المجموعة؟

---

## 9. التزامن والسباقات

First Decision Wins يحتاج Invariant واضحاً:

- يوجد قرار نهائي واحد صالح لكل Step Run عند هذا النمط.
- أول Transaction ناجح يحسم.
- أي Request متزامن لاحق يتلقى نتيجة Deterministic.
- لا يغير Retry النتيجة.
- تسجل المحاولات المتأخرة حسب سياسة Audit.
- UI يحدث الحالة فوراً.
- Notifications لا تتكرر.

آليات ممكنة مثل Compare-and-Set أو Unique Constraint أو Transaction Lock لا يجب فرضها هنا، لكن يجب أن يحدد Claude Invariant واختبار قبول.

### مثال اختبار

```text
Given step S is open and assigned to users A and B
When A approves and B rejects concurrently
Then exactly one final decision is committed
And the losing request receives decision_already_finalized
And no downstream action runs twice
And both attempts are auditable according to policy
```

---

## 10. Confidential / Restricted Notes

مصطلح «Secret Notes» قد يكون غير مناسب قانونياً. نحتاج Visibility Model واضحاً، مثل:

- Visible to all workflow participants.
- Visible to current step participants.
- Visible to approvers only.
- Visible to owning unit.
- Visible to compliance/audit only.
- Private draft to author.
- Restricted by classification.

### أسئلة حاسمة

- هل الملاحظة جزء من Workflow أم Record؟
- هل يظهر وجودها لمن لا يملك قراءتها؟
- هل تعدل بعد الحفظ؟
- هل تدخل Export؟
- ما Retention؟
- هل Admin يرى كل شيء؟
- هل تدعم Attachments؟
- هل تستخدم كسبب قرار؟
- هل تدخل LLM Context؟
- هل تظهر في Notifications؟
- كيف تحجب في Search وReports؟

القاعدة: الإخفاء يجب أن يطبق في Backend وQuery/Export/Search، لا UI فقط.

---

## 11. Delegation وActing on Behalf Of

سيناريوهات:

- تفويض مؤقت خلال إجازة.
- تفويض لمهمة محددة.
- تفويض لنوع Workflow.
- تفويض لدور.
- No further delegation.
- Delegation requiring approval.
- Expiration.
- Revocation.
- Conflict of interest exclusion.

يجب التفريق بين:

- Reassignment: نقل المسؤولية.
- Delegation: منح صلاحية مؤقتة.
- Proxy decision: قرار بالنيابة.
- Acting role: تولي دور رسمي مؤقتاً.
- Queue claim: استلام عنصر من قائمة.

Audit يجب أن يسجل Principal وActor وOn-Behalf-Of والPolicy المستخدمة.

---

## 12. Escalation وSLA

عند تجاوز الوقت قد يحدث:

- Reminder.
- Notify manager.
- Add alternate assignee.
- Reassign.
- Mark overdue.
- Trigger path.
- Pause بسبب Dependency.
- Escalate priority.
- Open incident/task.

يجب أن تراعي السياسة:

- Business calendar.
- Timezone.
- Pause/resume.
- Holidays.
- Dependency waiting.
- Retry limits.
- Who can change SLA.
- Audit of manual override.

لا نريد كوداً حراً؛ Escalation يمر عبر Actions/Policies معتمدة.

---

## 13. Comments مقابل Decisions

يجب الفصل بين:

- Comment لا يغير الحالة.
- Recommendation غير ملزمة.
- Decision يغير Step State.
- Reason جزء من Decision.
- Evidence يدعم Decision.
- Note قد تكون مقيدة الرؤية.

بعد First Decision Wins قد يسمح للبقية بإضافة Comments، لكن يجب ألا توحي UI أن التعليق يغير القرار.

---

## 14. Override وإعادة الفتح

قد تحتاج المؤسسة إلى Reopen أو Override. الخيارات:

- منع كامل في MVP.
- Reopen بصلاحية عالية وسبب إلزامي.
- New Step Run بدلاً من تعديل القديم.
- Reversal Event يحفظ القرار السابق.
- Compensation للأفعال المنفذة.
- إشعار الأطراف.
- أثر على الخطوات اللاحقة.

لا يجوز حذف القرار السابق أو تعديله بصمت.

---

## 15. سيناريوهات الاستخدام

### UC-01 — تعيين بالرقم الوظيفي
يحل النظام الرقم إلى هوية ثابتة ويعرض الاسم والوحدة. عدم التطابق أو عدم الصلاحية يمنع الإرسال.

### UC-02 — First Decision Wins
ثلاثة مستخدمين. الأول يعتمد. الثاني يحاول الرفض لاحقاً، فيحصل على `decision_already_finalized` دون تغيير النتيجة.

### UC-03 — ملاحظة مقيدة
المراجع يضيف Note مرئية للجنة التدقيق فقط. لا تظهر للطالب ولا تدخل AI Context العام.

### UC-04 — تفويض مؤقت
الموظف يفوض نوع قرارات لمدة أسبوع. القرار يسجل باسم Actor مع On-Behalf-Of.

### UC-05 — تصعيد
بعد يومي عمل Reminder، وبعد يوم ثالث تصعيد للرئيس وفق Business Calendar.

### UC-06 — نقل وحدة تنظيمية
تتغير `parent_org_unit_id` دون كسر Workflow IDs أو العلاقات.

### UC-07 — تعارض مصالح
المستخدم resolved لكنه ممنوع من القرار على سجل يخصه.

### UC-08 — حساب معطل
Work Item ينتقل إلى حالة تحتاج Reassignment أو Queue؛ لا يختفي.

### UC-09 — قراران متزامنان
النظام يحسم واحداً فقط، ولا يكرر Downstream Action.

### UC-10 — Override
مسؤول مخول يعيد فتح القرار بسبب خطأ، مع Reason وAudit وCompensation Plan.

---

## 16. الصلاحيات المطلوبة للمراجعة

أمثلة Permission Verbs تحتاج حسم:

- View workflow.
- View restricted notes.
- Create comment.
- Make decision.
- Assign.
- Reassign.
- Delegate.
- Escalate manually.
- Override/reopen.
- Cancel.
- Export.
- View audit.
- Manage decision policy.

يجب تحديد Scope لكل فعل ومنع تضارب الصلاحيات.

---

## 17. Audit Events المحتملة

- Work item created.
- Assignment resolved.
- Assignment failed.
- Claimed.
- Released.
- Reassigned.
- Delegated.
- Delegation revoked.
- Decision submitted.
- Decision accepted.
- Decision rejected due to finalization.
- Step finalized.
- Comment added.
- Restricted note added/viewed/exported.
- SLA breached.
- Escalation executed.
- Override requested/approved/executed.
- Workflow resumed/cancelled.

Claude يقرر Catalogue النهائي ويمنع تسجيل Secret content في Logs.

---

## 18. الحالة المتوقعة داخل المستودع — تحتاج إثباتاً

المواد السابقة تشير إلى:

- Workflow Ownership موثق جزئياً.
- `owning_org_unit_id` قرار مهم.
- Workflow Builder موجود.
- LinkedRecord states أضيفت في UI.
- Permissions/Audit foundations موجودة.
- لا إثبات كافٍ على First Decision Wins وRestricted Notes.
- قد توجد Approval/Assignment semantics عامة في Phase Designs.

على Claude فحص العقود والمراحل وUI Inventory والـADRs والـDeferred Register.

---

## 19. الفجوات المحتملة — قائمة فحص

- Workflow Decision Contract.
- Assignment/Work Item Contract.
- Decision Rule Taxonomy.
- Completion Semantics.
- Concurrency Invariant.
- Comment/Note Visibility.
- Delegation Model.
- Escalation/SLA Policy.
- Identity Resolution.
- Inactive User Handling.
- Reassignment.
- Override/Reopen.
- Audit Events.
- UI States/Actions.
- Permission Verbs.
- Notifications.
- Export/Redaction.
- Retention.
- Tests.
- Phase Mapping.
- Conflict of Interest.
- Acting on Behalf Of.

---

## 20. الأسئلة المعمارية المفتوحة

1. هل Decision جزء من Workflow Engine أم Approval Bounded Context؟
2. هل Task/Work Item كيان مستقل؟
3. كيف يمثل First Decision Wins؟
4. هل Group Membership Snapshot أم Dynamic؟
5. هل Comments مستقلة عن Decisions؟
6. ما الاسم القانوني للملاحظات المقيدة؟
7. هل Admin يرى كل Restricted Note؟
8. كيف تطبق Field-level Visibility؟
9. هل Delegation عام أم Per Workflow؟
10. كيف يمثل Acting on Behalf Of؟
11. هل Escalation يغير Assignee أم يضيف؟
12. ما سلوك القرار بعد SLA؟
13. هل AI Recommendation تحفظ كEvidence؟
14. كيف يختبر التزامن؟
15. ما MVP وما Deferred؟
16. هل Reopen مسموح؟
17. كيف تتعامل مع Downstream Actions بعد Override؟

---

## 21. خارج النطاق

- تنفيذ Workflow Engine.
- دعم كل أنماط التصويت الآن.
- اختيار Queue Technology.
- كتابة UI.
- AI Auto-Approval.
- تعريف قوانين كل مؤسسة.
- تغيير الهيكل التنظيمي.
- بناء Notification System.

---

## 22. المطلوب من Claude Architecture

1. Evidence Baseline.
2. Decision Semantics Matrix.
3. Assignment Model.
4. Stable Identity/Resolution Flow.
5. Confidentiality Model.
6. Delegation/Escalation Model.
7. Concurrency Invariants.
8. Lifecycle/State Transitions.
9. Permission/Audit Matrix.
10. MVP vs Deferred List.
11. Repository Delta.
12. Owner Decisions.
13. التوقف دون تعديل.
14. بعد الاعتماد فقط: Prompt لـClaude Code لتحديث العقود والمراحل والاختبارات التوثيقية.

---

## 23. شكل مخرجات Claude

1. Executive Verdict.
2. Evidence Baseline.
3. Coverage Matrix.
4. Domain/Resource Model.
5. Decision Rule Matrix.
6. Assignment and Identity Model.
7. Confidentiality/Delegation/Escalation.
8. Concurrency Invariants.
9. Options and Trade-offs.
10. Recommended Minimal Delta.
11. Owner Decisions.
12. Deferred Items.
13. Acceptance Criteria.
14. Proposed Claude Code Prompt.
15. Stop Statement.

---

## 24. ما لا نريده

- لا جعل First Decision Wins قاعدة عامة.
- لا تخزين الاسم أو الرقم كهوية.
- لا تجاهل Concurrent Decisions.
- لا حماية بالمظهر فقط للملاحظات.
- لا خلط Delegation وReassignment وProxy.
- لا تنفيذ Engine.
- لا تعديل مستودع أثناء الدراسة.

---

## 25. معايير قبول المراجعة

تُرفض إذا:

- لم تحدد أثر القرار على بقية المستلمين.
- لم تربط الصلاحيات والتدقيق.
- لم تقدم Invariant للتزامن.
- لم تعالج Identity Resolution.
- لم تفرق بين Comments وDecisions وRestricted Notes.
- لم تحدد MVP وDeferred.
- لم تقدم Evidence من المستودع.
