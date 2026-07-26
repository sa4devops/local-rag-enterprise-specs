# RECONCILIATION-RAR-001 — B1 Commit 2 (RAR-001 · Conversational Tasks & Automation)

> **مخرج traceability/تحليلي غير حاكم** — لا سلطة موازية ولا بديل عن الأصل الحاكم؛ لا يُنفَّذ أي دلتا. مبني على `CANONICAL-ITEM-UNIVERSE.md` المجمَّد (`188ad37`). **53 صفاً canonical** يسكن ممثلها في RAR-001. schema **ستة أعمدة بالضبط** (البند · المصدر · الحالة عند HEAD · الدليل · التصنيف · الوجهة)؛ الوسم `[NN]` جزءٌ من نص «البند» لا عمودٌ سابع. التصنيف من **الخمسة حصراً**.
> **المصدر:** `references/analysis-inputs/rar-2026-07/RAR-001-Conversational-Tasks-Automation.md:<line>` (يُختصر `RAR-001:<line>`). **الدليل الحاكم** بمسار وسطر فعليين عند HEAD `188ad37`؛ أدلة الغياب في `ABSENCE-EVIDENCE-B1-RAR001.md`.

| البند (canonical) | المصدر | الحالة عند HEAD | الدليل | التصنيف | الوجهة |
|---|---|---|---|---|---|
| **[01]** Business Glossary للمصطلحات الأربعة موجود | RAR-001:220 | معجم أعمال يعرّف Task/Schedule/Workflow/Automation | `knowledge/BUSINESS_GLOSSARY.md:13` | مقنَّن | الأصل (Glossary) |
| **[02]** أساس Workflow | RAR-001:221 | عقد شاشة workflows (Candidate) | `contracts/screens/admin.workflows.md:19` | مقنَّن | الأصل |
| **[03]** أساس Action | RAR-001:221 | كتالوج أفعال مغلق + نموذج أزرار | `ui/UI_ACTION_BUTTON_MODEL.md:18` | مقنَّن | الأصل |
| **[04]** أساس Permission | RAR-001:221 | م2 default-deny + Permission Registry | `constitution.md:10` | مقنَّن | الأصل |
| **[05]** أساس Audit | RAR-001:221 | م3 Audit append-only | `constitution.md:11` | مقنَّن | الأصل |
| **[06]** Agent-assisted Workflow Builder كفكرة | RAR-001:222 | OD-BLD-1 (أوضاع الباني) مقفل | `decisions/open-decisions.md:100` | مقنَّن | الأصل |
| **[07]** تنفيذ Conversational Automation في مرحلة لاحقة | RAR-001:223 | مُرحَّل (P6 chat + P3 workflow) | `phases/PHASE_MASTER_PLAN.md:38` | مؤجَّل بصف قائم | P6/P3 |
| **[08]** توصية تجهيز العقود الآن | RAR-001:224 | الحد الأدنى من العقود يُنشأ الآن + 4 بذور | `decisions/adr/ADR-0035-contracts-layer-single-source.md:26` | مقنَّن | الأصل |
| **[09]** Contracts للأنواع الأربعة | RAR-001:228 | جزئي: task.create + admin.workflows؛ Schedule/Automation غائبة | `ui/UI_ACTION_BUTTON_MODEL.md:67` · `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-001` | دلتا حقيقية | R3 |
| **[10]** Lifecycles رسمية | RAR-001:229 | workflow lifecycle فقط؛ الأنواع الأخرى غائبة | `contracts/screens/admin.workflows.md:22` · `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-002` | دلتا حقيقية | R3 |
| **[11]** API Operation Contracts | RAR-001:230 | نمط REST/OpenAPI معرَّف؛ لا عقود عمليات للأنواع | `decisions/adr/ADR-0025-api-contract-rest-openapi-sse.md:7` · `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-003` | دلتا حقيقية | R3 |
| **[12]** Screen/Route Contracts لنقاط الدخول | RAR-001:231 | عقود شاشات (workflows) + مساحة عمل محادثة | `contracts/screens/admin.workflows.md:19` | مقنَّن | الأصل |
| **[13]** Permission Verbs واضحة | RAR-001:232 | نمط `{resource}.{scope}.{operation}` + Registry | `ui/UI_FIELD_NAMING.md:13` | مقنَّن | الأصل |
| **[14]** Traceability إلى Phase واختبارات | RAR-001:233 | مصفوفة تتبّع بذور → FP → مراحل | `traceability/TRACEABILITY_MATRIX.md:14` | مقنَّن | الأصل |
| **[15]** Deferred Entries | RAR-001:234 | سجل المؤجلات الرسمي | `decisions/DEFERRED_IMPLEMENTATION.md:4` | مقنَّن | الأصل |
| **[16]** تعارضات تسمية بين الوثائق | RAR-001:235 | مصدر تسمية كنسي واحد؛ تعارض G-namespace مساره P4 | `ui/UI_FIELD_NAMING.md:10` | مقنَّن | الأصل (P4 للتعارض) |
| **[17]** نموذج موارد موحد أو فصل واضح | RAR-001:241 | غير مقنَّن | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-004` | دلتا حقيقية | R3 |
| **[18]** Draft/Preview/Confirm semantics | RAR-001:242 | حالات + بطاقة معاينة/تأكيد | `contracts/enums/ENUMS_DICTIONARY.md:16` · `ui/UI_INTERACTION_MODEL.md:52` | مقنَّن | الأصل |
| **[19]** Intent Interpretation Contract | RAR-001:243 | غير مقنَّن | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-005` | دلتا حقيقية | R3 |
| **[20]** Resolution Contract للأشخاص/السجلات/الوحدات | RAR-001:244 | غير مقنَّن | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-006` | دلتا حقيقية | R3 |
| **[21]** Ambiguity handling | RAR-001:245 | استيضاح حقلاً-حقلاً في بطاقة الحوار | `ui/UI_INTERACTION_MODEL.md:73` | مقنَّن | الأصل |
| **[22]** Permission evaluation في كل مرحلة | RAR-001:246 | م2 default-deny قبل كل استرجاع/فعل | `constitution.md:10` | مقنَّن | الأصل |
| **[23]** Approval thresholds | RAR-001:247 | confirmation none/simple/typed/dual مشتق من الخطورة | `ui/UI_ACTION_BUTTON_MODEL.md:18` | مقنَّن | الأصل |
| **[24]** Recurrence | RAR-001:248 | غير مقنَّن | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-007` | دلتا حقيقية | R5 |
| **[25]** Timezone (جدولة) | RAR-001:248 | غير مقنَّن | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-008` | دلتا حقيقية | R5 |
| **[26]** Business Calendar | RAR-001:248 | غير مقنَّن | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-009` | دلتا حقيقية | R5 |
| **[27]** Event Trigger abstraction | RAR-001:249 | غير مقنَّن | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-010` | دلتا حقيقية | R10 |
| **[28]** Idempotency وإعادة المحاولة | RAR-001:250 | تنفيذ idempotent بمفتاح + run.retry | `ui/UI_ACTION_BUTTON_MODEL.md:21` | مقنَّن | الأصل |
| **[29]** Versioning | RAR-001:251 | عمود «نسخة» + ADR-0032 | `contracts/screens/admin.workflows.md:19` | مقنَّن | الأصل |
| **[30]** التعديل (Edit) | RAR-001:251 | شريط دورة حياة التعريف | `contracts/screens/admin.workflows.md:19` | مقنَّن | الأصل |
| **[31]** الإلغاء (Cancel) | RAR-001:251 | حالات archived/rejected | `contracts/enums/ENUMS_DICTIONARY.md:16` | مقنَّن | الأصل |
| **[32]** Run history وExecution Evidence | RAR-001:252 | runs.list/runs.detail + OD-RUN-1..3 | `decisions/open-decisions.md:85` | مقنَّن | الأصل |
| **[33]** Notifications | RAR-001:253 | مركز إشعارات (G8) + WORKFLOW_ITEM_RETURNED | `ui/UI_STITCH_PROMPTS_BY_PHASE.md:50` | مقنَّن | الأصل |
| **[34]** ربط Work Queue وInbox | RAR-001:254 | My Tasks + approvals inbox (G8) | `ui/UI_STITCH_PROMPTS_BY_PHASE.md:48` | مقنَّن | الأصل |
| **[35]** Audit Event Catalogue (موحّد) | RAR-001:255 | audit_event لكل عقد؛ لا كتالوج موحّد | `ui/UI_FIELD_NAMING.md:23` · `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-011` | دلتا حقيقية | R3 |
| **[36]** UI states (parsing/needs_input/preview_ready/approval_required/failed) | RAR-001:256 | عائلة حالات المكوّنات + حالات البطاقة | `contracts/screens/admin.workflows.md:22` | مقنَّن | الأصل |
| **[37]** Acceptance tests (منع تجاوز الصلاحيات/كشف البيانات) | RAR-001:257 | مبدأ م2 + استراتيجية الاختبار | `methodology/testing-strategy.md:1` · `constitution.md:10` | مقنَّن | الأصل |
| **[38]** Fallback عند عدم توفر LLM (G03 يضم +:298) | RAR-001:258 | م11: fallback معرَّف + validation لا تفشل مفتوحة | `constitution.md:19` | مقنَّن | الأصل |
| **[39]** Task مورد مستقل أم تجسيد Workflow؟ | RAR-001:286 | لا حسم حاكم لعلاقة Task↔Workflow | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-012` | تعارض يحتاج قراراً | SA (R3 pending decision) |
| **[40]** الحد بين Schedule وAutomation Trigger؟ | RAR-001:287 | لا حسم حاكم (النوعان غير مقنَّنين) | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-013` | تعارض يحتاج قراراً | SA (R3 pending decision) |
| **[41]** أين تخزن صياغة المستخدم الأصلية؟ | RAR-001:288 | لا حسم حاكم لآلية التخزين | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-014` | تعارض يحتاج قراراً | SA (R3 pending decision) |
| **[42]** تخزين خطة LLM الوسيطة؟ | RAR-001:289 | لا حسم حاكم لآلية التخزين | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-015` | تعارض يحتاج قراراً | SA (R3 pending decision) |
| **[43]** منع اعتبار خطة LLM حقيقة | RAR-001:289 | م1: الـLLM ليس مصدر حقيقة | `constitution.md:9` | مقنَّن | الأصل |
| **[44]** نموذج التحقق Deterministic؟ | RAR-001:290 | لا حسم حاكم | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-016` | تعارض يحتاج قراراً | SA (R3 pending decision) |
| **[45]** ربط Preview بنسخة العقود المتحقَّق عليها؟ | RAR-001:291 | لا حسم حاكم (معاينة بلا ربط نسخة) | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-017` | تعارض يحتاج قراراً | SA (R3 pending decision) |
| **[46]** هل كل تعديل ينتج Version جديداً؟ | RAR-001:292 | ADR-0032 يعرّف التخزين؛ سياسة versioning-per-edit غير مقنَّنة | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-018` | تعارض يحتاج قراراً | SA (R3 pending decision) |
| **[47]** ما الذي يُنشر دون Admin؟ | RAR-001:293 | م14 + OD-BLD-1 (لا builder للمستخدم النهائي) | `constitution.md:22` · `decisions/open-decisions.md:100` | مقنَّن | الأصل |
| **[48]** Cross-Org Assignment؟ | RAR-001:294 | نموذج الإدارة المنطاقة (ADR-0037)؛ تفصيل التعيين العابر لاحق | `decisions/adr/ADR-0037-scoped-administration-model.md:7` | مؤجَّل بصف قائم | R4/R5 |
| **[49]** هل نحتاج Dry Run؟ | RAR-001:295 | لا حسم حاكم لـDry-Run تنفيذ الأتمتة | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-019` | تعارض يحتاج قراراً | SA (R3 pending decision) |
| **[50]** الحد الأدنى المطلوب الآن إذا كان التنفيذ مؤجلاً؟ | RAR-001:296 | سلّم الجاهزية السداسي (Architecture-ready) | `methodology/agent-execution-model.md:65` | مقنَّن | الأصل |
| **[51]** ADR أم Contracts فقط؟ | RAR-001:297 | سياسة D15 (متى يلزم ADR) | `decisions/adr/README.md:9` | مقنَّن | الأصل |
| **[52]** منع Prompt Injection من مستند/سجل (G01 يضم +RAR-002:414) | RAR-001:299 | م1 + validation fail-closed (P6)؛ لا عقد حقن مخصَّص بعد | `constitution.md:9` · `phases/PHASE_MASTER_PLAN.md:38` | مؤجَّل بصف قائم | P6 |
| **[53]** تمثيل «عندما يكتمل الجميع» قابلاً للاختبار؟ | RAR-001:300 | لا حسم حاكم لدلالة join | `ABSENCE-EVIDENCE-B1-RAR001.md#absence-b1-rar001-020` | تعارض يحتاج قراراً | SA (R5 pending decision) |

## توزيع التصنيفات (53) — [مُحدَّث بعد استعادة نوع DQ المجمَّد]
**مقنَّن = 30** · **مؤجَّل بصف قائم = 3** ([07]·[48]·[52]) · **دلتا حقيقية = 11** ([09],[10],[11],[17],[19],[20],[24],[25],[26],[27],[35]) · **تعارض يحتاج قراراً = 9** ([39],[40],[41],[42],[44],[45],[46],[49],[53]) · **مصطنع أو بلا أساس = 0**. المجموع = 53 ✓ (= canonical universe housing لـRAR-001).

### تصحيح: محفّزات §14-هـ الأربعة (لا محفّزان)
العبارة السابقة التي حصرت §14-هـ في «تعارض سلطات/تفسيرات» **خاطئة وأُسقطت**. التصنيف «تعارض يحتاج قراراً» ينطبق بأيٍّ من المحفّزات الآتية:
1. **تعارض سلطتين حاكمتين** (نصّان حاكمان يقرّران خلاف بعضهما).
2. **تعارض تفسيرين حاكمين** (نصٌّ واحد يحتمل قراءتين نافذتين).
3. **owner intent غير محسوم** — سؤال قرار لم يفصل فيه المالك بعد. *(المحفّز المُسقَط في `ce61506`، وهو المنطبق على الصفوف التسعة.)*
4. **تعارض نطاقين** يحتاج قراراً — اختيار أحد النطاقين يغيّر التزامات نافذة.

### القاعدة الحاكمة: نوع DQ المجمَّد لا يتحول دلتا بالغياب
`NORMALIZATION-AND-ATOMIC-MAP.md:14` (مجمَّد عند `188ad37`) يقرّر لـ**RAR001 S14-001..015**: النوع **DQ** — «أسئلة معمارية مفتوحة — **تبقى أسئلة قرار (لا تُحوَّل إلى إلزام)** · تحتاج قراراً/تفسيراً». وبالمقابل يُظهر السطر 12 أن ما أُريد تحويله نوعاً وُسم صراحةً `DQ→REQ` (RAR001 S11-006..013) — ولا تحويل مماثل لـS14.
> **قاعدة (١):** البند الذي نوعه المجمَّد **DQ** وصيغته سؤال قرار أو اختيار بين بدائل، ولا يحسمه المستودع الحاكم، **يبقى «تعارض يحتاج قراراً»**. لا يتحول إلى «دلتا حقيقية» إلا بقرار مالك يثبت الالتزام ويحدد الخيار أو السلوك المطلوب.
> **قاعدة (٢):** `absence evidence` يثبت **غياب الحسم الحاكم**، لكنه **لا يثبت أن الإجابة المطلوبة «نعم»**، ولا يحوّل السؤال تلقائياً إلى مطلب تنفيذي. الغياب شرطُ **إبقاء** سؤال القرار لا شرطُ ترقيته إلزاماً.
> **قاعدة (٣) — استثناء الدليل الموجب:** يُصنَّف صف DQ «مقنَّن» فقط بدليل حاكم **مباشر وصريح** بمسار وسطر فعليين يحسم **الخيار أو السلوك محل السؤال نفسه**. لا يُقبل: تشابه مصطلحات · استنتاج ضمني · مطابقة تقريبية · نص عام لا يجيب السؤال. **لم يُستوفَ هذا الاستثناء في أيٍّ من الصفوف التسعة** (المطابقات القريبة التي فُحصت واستُبعدت موثَّقة داخل مراسي `absence-b1-rar001-012..020`).
> **الوجهة:** صيغة `SA (RN pending decision)` تعني: **SA صاحب القرار** · المرحلة **ليست التزاماً بعد** · لا يدخل البند backlog تنفيذياً بوصفه دلتا مستقرة قبل القرار.
> **قاعدة §4 (تصحيح سابق — سارٍ):** العمود الرابع لا يستشهد بأي ملف تحت `references/analysis-inputs/**` (مادة غير حاكمة، عمود المصدر فقط) — دليل حاكم أو مرساة غياب أو سلطتان متعارضتان حصراً.

### قاعدة إنفاذ إلزامية قبل Commit 3 (تسري على RAR-002 · RAR-003 · B2)
**أي بند مصنَّف في normalization بوصفه `DQ` لا يجوز تحويله في reconciliation إلى «دلتا حقيقية» لمجرد غياب التقنين.** غياب الحسم يثبت **بقاء سؤال القرار**. التحويل إلى دلتا يتطلب **قرار مالك صريحاً** أو **دليلاً حاكماً** يثبت أن الالتزام نفسه مستقر وأن الناقص هو التقنين فقط.

## CANDIDATE BLOCKING (RAR-001)
**لا مرشح حجب في RAR-001.** الدلتا الحقيقية (11) توجَّه إلى R3/R5/R10، والتعارضات التسعة موضع قرارها **SA** ولا تدخل مرحلةً بوصفها التزاماً قبل القرار؛ **لا بند يمس G2 · R6 · FP-0001 · GATE-DEFINITION** بما يشكّل حجباً. (B1 لا يحسب §13b النهائي؛ candidate ≠ final — §13b تبقى `PENDING`.)

## ثبات المدخل والقاعدة
لم تُعدَّل وثائق RAR ولم تُنفَّذ أي دلتا ولم تُلمس ملفات canonicalization الأربعة (`188ad37`). لا اختراع دليل: كل «مقنَّن» بمسار+سطر فعلي، وكل «دلتا» بمرساة في `ABSENCE-EVIDENCE-B1-RAR001.md` قابلة لإعادة التنفيذ.
