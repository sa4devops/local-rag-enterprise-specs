# NORMALIZATION-AND-ATOMIC-MAP — B1 (المرحلتان 2 و3)

> **مخرج traceability/تحليلي غير حاكم** — ليس داخل authority ladder ولا سلطة موازية ولا بديلاً عن الأصل الحاكم. يجمع مرحلتين في قسمين مستقلين (P3 B1 §16): **§A التطبيع** · **§B التفكيك الذري**. المدخل: `RAW-EXTRACTION-REGISTER.md`.
> **قائمة مخرجات B1 المعتمدة (تُعلن قبل الكتابة — §16):** (1) `RAW-EXTRACTION-REGISTER.md` · (2) `NORMALIZATION-AND-ATOMIC-MAP.md` · (3) `SEMANTIC-MERGE-MAP.md` · (4) `CANONICAL-ITEM-UNIVERSE.md` — **[Commit 1]**؛ (5) `RECONCILIATION-RAR-001.md` · (6) `ABSENCE-EVIDENCE-B1-RAR001.md` — [Commit 2]؛ (7) `RECONCILIATION-RAR-002.md` · (8) `ABSENCE-EVIDENCE-B1-RAR002.md` — [Commit 3]؛ (9) `RECONCILIATION-RAR-003.md` · (10) `ABSENCE-EVIDENCE-B1-RAR003.md` · (11) `B1-CHECKPOINT-REPORT.md` — [Commit 4]. **العدد الفعلي = 11 ملف .md** (سبب كل ملف = مرحلة/RAR مستقلة قابلة للتدقيق). دُمجت مرحلتا التطبيع والتفكيك في ملف واحد بقسمين حفاظاً على الحد الأدنى دون إضعاف التدقيق.

## §A — التطبيع (Normalization)
التطبيع 1:1 مع الخام (NORM-ID = raw-id مع بادئة `N-`) ما لم يُذكر خلاف. **الأنواع الستة:** REQ (مطلب) · COV (ادعاء تغطية) · SUG (اقتراح) · DQ (سؤال قرار) · REC (توصية) · STATE (وصف حالة). التغييرات التحريرية: توحيد المصطلحات (Task/Workflow/Action/Permission/Audit)، وتحويل صيغة السؤال «هل توجد X؟» إلى «إثبات وجود/غياب X عند HEAD» دون توسيع المعنى.

| النطاق (RAW-IDs) | النوع | ملاحظة التطبيع | غير المحسوم |
|---|---|---|---|
| RAR001 S11-001..005 | COV | ادعاءات حالة سابقة («توجد X») — تُطبَّع إلى «يُدَّعى وجود X؛ يلزم إثبات عند HEAD» | صحة الادعاء تُحسم بالدليل |
| RAR001 S11-006..013 | DQ→REQ | أسئلة تحقق «هل توجد X؟» تُطبَّع إلى مطلب إثبات وجود X (Contracts/Lifecycles/API/Screen-Route/Permission-Verbs/Traceability/Deferred/تعارض تسمية) | — |
| RAR001 S12-001..018 | REQ | فجوات مرشحة تُطبَّع مطالبَ قدرة (نموذج موارد · Draft/Preview/Confirm · Intent Contract · Resolution · Ambiguity · Permission-per-stage · Approval thresholds · Recurrence/TZ/Calendar · Event Trigger · Idempotency · Versioning · Run history · Notifications · Work-Queue/Inbox · Audit Catalogue · UI states · Acceptance tests · LLM Fallback) | أيها مقنَّن يُحسم بالدليل |
| RAR001 S14-001..015 | DQ | أسئلة معمارية مفتوحة — تبقى أسئلة قرار (لا تُحوَّل إلى إلزام) | تحتاج قراراً/تفسيراً |
| RAR002 S11-001..008 | REQ | خطوات Workflow «طلب إنشاء Agent» — مطلب تدفق موحّد قابل للتفكيك | هل Workflow عادية أم Capability |
| RAR002 S12-001..006 | STATE→REQ | حالات دورة حياة جانبية — تُطبَّع مطالبَ تمثيل حالة | الحد الأدنى ومالك Transitions |
| RAR002 S14-001..019 | REQ | ضوابط أمن/عزل للـAgent — مطالب سياسة/إنفاذ | أيها مقنَّن عاماً في الحوكمة |
| RAR003 S11-001..009 | REC/REQ | تقنين UI Constitution التاريخي مقابل ADR الحالي | Version Canonical |
| RAR003 S12-001..008 | COV | «الفهم الحالي» عن Open WebUI — ادعاءات تغطية | تُحسم بالدليل (ADR-0030) |
| RAR003 S12-009..014 | REQ | مطالب مراجعة/بوابات Open WebUI | Exit Criteria النهائية |
| RAR003 S12-015..024 | SUG | أمثلة Exit Criteria — مقترحات (Claude يقرر النهائية) | القائمة النهائية |
| RAR003 S14-001..013 | REQ | معايير Accessibility — مطالب قابلة للفحص | ما يدخل Governance مقابل Tests |
| RAR004 S11-001..017 | REQ | سياسات Upgrade/Rollback/Compatibility — مطالب | قاعدة الإصدار القابلة للتدقيق |
| RAR004 S12-001..011 | REQ | Impact Analysis — أنواع التبعية الواجب تغطيتها | هل Dependency Graph قانوني |
| RAR004 S14-001..009 | DQ | Code Execution Boundaries — أسئلة قرار (Process/Container/LAN/Config-only) | Runtime المؤجَّل |
| RAR005 S11-001..009 | REQ | سيناريوهات Delegation — مطالب سلوك | — |
| RAR005 S11-010..014 | STATE | تعريفات مفرَّقة (Reassignment/Delegation/Proxy/Acting/Queue-claim) — وصف تمييزي | — |
| RAR005 S12-001..017 | REQ | Escalation/SLA — أفعال وسياسات | — |
| RAR005 S14-001..007 | SUG/REQ | خيارات Override/Reopen — مقترحات + قيد «لا حذف/تعديل صامت» | حدود MVP |
| RAR006 S11-001..008 | SUG | أنماط Human-in-the-Loop مستقبلية — «لا توثَّق كلها كالتزام» | نقاط التكامل والحد الأدنى |
| RAR006 S12-001..008 | REQ | مصادر Ingestion عبر Adapter/Contract محكوم | ليست تقنيات مختارة |
| RAR006 S14-001..011 | DQ | Ordering/Replay — أسئلة معمارية | Invariants لا اختيار أداة |
| RAR007 S11-001..002 | STATE | تعريف Future Capability مقابل Deferred Implementation | القاعدة الفاصلة |
| RAR007 S12-001..009 | DQ | مواضع فحص السجل (مسارات المستودع) | — |
| RAR007 S12-010..014 | SUG | خيارات مكان السجل — مقترحات قرار | — |
| RAR007 S14-001..014 | REQ | وثائق مطلوب توليدها لاحقاً من سلسلة الحقائق المعتمدة | تُوسم Future Roadmap |
> **RAR-004..007 (132 بنداً):** ممثلوها **يُصنَّفون في B2** (لا تصنيف §10.4 في B1) — إلا إن نقلت قاعدة أدنى RAR ممثِّلاً إلى RAR-001..003 (لم يحدث: صفر مصدر 004..007 داخل مجموعات الدمج). **التفكيك الذري:** لا بند مركّب في RAR-004..007 يستوجب تفكيكاً (كلها ذرّية) — صفر atomic split جديد.

**ما لم يتغيّر:** لا توسيع معنى · لا حذف qualifier (حُفظت «لاحقاً/إن لزم/المعقولة/إن كان موجوداً») · لا تحويل توصية إلى إلزام (بقيت SUG/REC كما هي) · لا دمج هنا.

## §B — التفكيك الذري (Atomic Decomposition)
القاعدة: يُفكَّك فقط بندٌ مركّب بمطالب مستقلة **مختلفة احتمالات التغطية**. الغالبية ذرية أصلاً (بند = مفهوم واحد). التفكيكات المعتمدة (parent → children؛ children تغطي كامل معنى parent بلا إضافة/إسقاط):

| Parent NORM-ID | Atomic children (معرّفات صريحة) | عدد | سبب الاستقلال |
|---|---|---|---|
| N-RAR001-S11-002 | ATOM-RAR001-S11-002-a (Workflow) · -b (Action) · -c (Permission) · -d (Audit) | 4 | لكل أساس ملف/حالة تغطية مختلفة في المستودع |
| N-RAR001-S12-008 | ATOM-RAR001-S12-008-a (Recurrence) · -b (Timezone) · -c (Business-Calendar) | 3 | قد يُقنَّن بعضها دون بعض |
| N-RAR001-S12-011 | ATOM-RAR001-S12-011-a (Versioning) · -b (Edit) · -c (Cancel) | 3 | التزامات lifecycle منفصلة |
| N-RAR001-S14-004 | ATOM-RAR001-S14-004-a (تخزين الخطة الوسيطة) · -b (منع اعتبارها Source-of-Truth) | 2 | الثاني مقنَّن دستورياً (م1)، الأول سؤال تخزين |
| N-RAR003-S11-002 | ATOM-RAR003-S11-002-a (Brand) · -b (Tokens) · -c (Accessibility) · -d (RTL) · -e (Responsive) · -f (Offline) | 6 | تغطية مختلفة عبر `ui/` وADR |
| N-RAR002-S11-001 → S11-008 | لا تفكيك (خطوات تدفق واحد) — تُدمج في G02 (`SEMANTIC-MERGE-MAP.md`) | 0 | — |
> **إجمالي التفكيك:** **5 آباء → 18 ذرّة** (RAR-001: 4 آباء → 12 ذرّة؛ RAR-003: أبٌ واحد `S11-002` → 6 ذرّات). تُحدَّث محاسبة `CANONICAL-ITEM-UNIVERSE.md` وفقها.

**بنود لا تُفكَّك** (الفصل يغيّر المعنى): «Draft/Preview/Confirm semantics» (دلالة واحدة مترابطة) · «Row/Object/Field permissions» (تدرّج واحد) · «Ordering/Replay» (مفهومان لكن كلٌّ بند مستقل أصلاً في الخام فلا حاجة لتفكيك إضافي).

**أثر التفكيك على العدّ:** التفكيكات أعلاه تزيد عدد الذرّات فوق 257 ضمن RAR-001/003؛ يُوثَّق العدد الذرّي الفعلي وممثلوه في `CANONICAL-ITEM-UNIVERSE.md` (لا هدف عددي). لا بند خام بلا مسار: كل raw-id إمّا NORM 1:1 أو ATOM-split موثّق.
