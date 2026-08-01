# SOURCE-ELIGIBILITY-PASS — B2-FINAL-A (تمريرة أهلية المصادر)

> **مخرج traceability/تحليلي غير حاكم** — لا سلطة موازية ولا بديل عن الأصل الحاكم. يمسح **كل استشهاد في العمود الرابع** عبر الصفوف الـ260 في `RECONCILIATION-RAR-001.md`..`RECONCILIATION-RAR-007.md`، ويحكم أهلية كل مصدر مميز.
> **HEAD المنفَّذ عليه المسح:** `a2a60601b9857d9f1b6f959900a2cd97870e00e6` (‏**مُحدَّثة في B2-FINAL-A CORRECTIVE**) · **التاريخ:** 2026-07-27.
> **العدد استُخرج آلياً — لا مفترضاً:** **65 مصدراً مميزاً** في العمود الرابع (ولم يُعتمد الرقم 166 ولا أي رقم مسبق). التوزيع: **52 نافذاً** · **6 غير نافذة وحدها** · **7 مراسي أدلة غياب** (مخرجات المصالحة نفسها — لا تُثبت ذاتها، وهي صيغة مصرَّح بها في schema العمود الرابع).

## 1) قاعدة الأهلية المطبَّقة
مصدرٌ حالته `Proposed` أو `Candidate` أو تاريخي أو informative أو أي حالة غير نافذة وفق `AUTHORITY.md` **لا يثبت وحده**: التزاماً نافذاً · سياسة نافذة · تعريفاً رسمياً يُستخدم لإثبات `مقنَّن` · قراراً حاكماً · صف تأجيل حاكماً. ويجوز استعماله **سياقاً** أو **مطابقةً قريبة** أو **مقروناً بمصدر نافذ يتبنّاه صراحةً** — وعندها **يُستشهد بالمتبنّي النافذ** لا بالمصدر غير النافذ منفرداً.
**صيغة الحالة إلزامية هوياتية:** `INDEX.md → row for `path` → status `X`` — و**ممنوع** `INDEX.md:NNN` (أرقام الفهرس تنزاح مع كل دفعة؛ الإثبات في §4).

## 2) المصادر غير النافذة وحدها — وحكمها بعد التمريرة
| المصدر | الحالة | مرتبته/أهليته | صفوف تستشهد به | RAR / canonical IDs | منفرداً أم مقروناً؟ | الحكم | الإجراء المنفَّذ في FINAL-A |
|---|---|---|---|---|---|---|---|
| `ui/UI_DESIGN_SYSTEM.md` | INDEX.md → row for `ui/UI_DESIGN_SYSTEM.md` → status `Proposed` | **غير نافذ وحده** — لكن **ملزم-معياري بالتبنّي** نصاً (`ui/UI_SCREEN_GOVERNANCE_STANDARD.md:10`، ‏`Accepted`، المرتبة 8) | **12** | RAR-003 (‏`[14]`..`[29]` وغيرها) | **مقروناً** بالمتبنّي في كل صف — تحقّق آلي: صفر صف يعتمد عليه وحده | **مؤهَّل بالتبنّي** | لا تغيير في التصنيف؛ صُحِّحت صيغة حالته إلى الهوياتية |
| `ui/UI_RUN_EXECUTION_MODEL.md` | INDEX.md → row for `ui/UI_RUN_EXECUTION_MODEL.md` → status `Proposed (v0.6)` | **غير نافذ وحده** — ملزم-معياري بالتبنّي (`ui/UI_SCREEN_GOVERNANCE_STANDARD.md:10`) | **3** | RAR-002 `[05]` · RAR-005 `[34]` `[38]` | كان **منفرداً** في RAR-002 `[05]` | **مؤهَّل بالتبنّي — بعد الاقتران** | **صُحِّح `RAR-002 [05]`**: أُضيف المتبنّي `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:10` إلى العمود الرابع |
| `ui/UI_INTERACTION_MODEL.md` | INDEX.md → row for `ui/UI_INTERACTION_MODEL.md` → status `Proposed (v0.5)` | **غير نافذ وحده** — ملزم-معياري بالتبنّي (`ui/UI_SCREEN_GOVERNANCE_STANDARD.md:10`) | **2** | RAR-001 `[18]` `[21]` | كان **منفرداً** في كليهما | **مؤهَّل بالتبنّي — بعد الاقتران** | **صُحِّح الصفّان**: أُضيف المتبنّي + دليلٌ نافذ ثانٍ (`ui/UI_AI_WORKSPACE_MODEL.md`، `Current`) |
| `contracts/screens/admin.workflows.md` | INDEX.md → row for `contracts/screens/admin.workflows.md` → status `Candidate` | **غير نافذ** — مرتبة العقود تشترط **Approved** نصاً (`AUTHORITY.md:14`)، و`ADR-0035:8` يبقي مخرجات أي وكيل **Proposed حتى بوابة اعتماد العقود** | **1** (كان **6**) | كان: RAR-001 `[02]` `[10]` `[12]` `[29]` `[30]` `[36]` · بقي: RAR-003 `[49]` (مقروناً بـ`decisions/open-decisions.md:159`) | كان **منفرداً** في ستة صفوف | **غير مؤهَّل منفرداً** | **صُحِّحت الستة**: استُبدل الدليل بمصادر نافذة (الجرد الكنسي · كتالوج الحالات · ADR-0035 بند 3) وبقي العقد **سياقاً مُفصَحاً عنه** |
| `knowledge/BUSINESS_GLOSSARY.md` | INDEX.md → row for `knowledge/BUSINESS_GLOSSARY.md` → status `Proposed (G1)` | **غير نافذ وحده** — و`knowledge/**` **مُتبنّى مصدرَ تأليفٍ قانونياً** نصاً (`decisions/adr/ADR-0035-contracts-layer-single-source.md:13`، `Accepted`) | **1** | RAR-001 `[01]` | كان **منفرداً** | **الحالة الخاصة — §3** | **حُسمت في §3** |
| `traceability/TRACEABILITY_MATRIX.md` | INDEX.md → row for `traceability/TRACEABILITY_MATRIX.md` → status `Proposed (G1)` | **غير نافذ وحده** — و«سجل التتبع» **موضعٌ حاكم إلزامي** في تعريف Done (`methodology/agent-execution-model.md:103`، المرتبة 2)، و`Traceability` مصدر تأليف قانوني (`ADR-0035:13`) | **1** | RAR-001 `[14]` | كان **منفرداً** | **مؤهَّل بالتبنّي — بعد الاقتران** | **صُحِّح الصف**: أُضيف المتبنّيان النافذان قبل الوثيقة نفسها |
| `ui/UI_STITCH_PROMPTS_BY_PHASE.md` | INDEX.md → row for `ui/UI_STITCH_PROMPTS_BY_PHASE.md` → status `Current` | **غير مؤهَّل رغم `Current`** — مصنَّف **تاريخي-informative** نصاً: «**لا تُقرأ كمتطلبات**» (`ui/UI_SCREEN_GOVERNANCE_STANDARD.md:14`) | **0** (كان **2**) | كان: RAR-001 `[33]` `[34]` | كان **منفرداً** في كليهما | **غير مؤهَّل مطلقاً** | **صُحِّح الصفّان** بالجرد الكنسي والمصدر الكنسي للتسمية ⇒ **صفر ورود له في العمود الرابع** |
| `contracts/enums/ENUMS_DICTIONARY.md` | INDEX.md → row for `contracts/enums/ENUMS_DICTIONARY.md` → status `Proposed (G1)` | **غير نافذ** — نفس قاعدة العقود (`AUTHORITY.md:14`)؛ ونصُّه نفسه يوجب «**فحصاً إلزامياً في FP-0001**» لقيمه | **0** (كان **2**) | كان: RAR-001 `[18]` `[31]` | كان **منفرداً** في `[31]` ومقروناً بغير نافذ في `[18]` | **غير مؤهَّل** | **صُحِّح الصفّان** ⇒ **صفر ورود له في العمود الرابع** |
| `INDEX.md` | — (`AUTHORITY.md:28`: «**دليل مواضع الملفات وحالاتها، لا مصدر سلطة إضافياً**») | **ليس مصدر سلطة** | **0** (كان **1**) | كان: RAR-003 `[09]` | — | **غير مؤهَّل مصدرَ سلطة** | حُوِّل إلى الصيغة الهوياتية والصف مسنودٌ بـ`ADR-0031:22` النافذ |

**نتيجة §2:** **صفر صف مصنَّف `مقنَّن` يعتمد على مصدر غير نافذ منفرداً** — تحقّق آلي بعد التصحيح.

> **إضافة B2-FINAL-A CORRECTIVE:** الجدول أعلاه عالج المصادر غير النافذة **بحالتها في الفهرس**. والتمريرة التصحيحية عالجت صنفاً ثانياً لم يكن مشمولاً: مصدرٌ حالته `Accepted` **لكنه غير مرتَّب في `AUTHORITY.md`** — وهو `phases/BACKLOG_DEFERRED_SCOPE.md`. التفصيل في §6-1 و`FINAL-RECONCILIATION-TABLE.md` §5-ج.

## 3) الحالة الخاصة — حسم `SOURCE-ELIGIBILITY REVIEW REQUIRED` للصف `[01]` في `RECONCILIATION-RAR-001.md`
**البند:** «Business Glossary للمصطلحات الأربعة **موجود**» (المصدر `RAR-001:220` — نصّه: «وجود Business Glossary **أوّلي** للمصطلحات الأربعة»).
**الدليل السابق:** `knowledge/BUSINESS_GLOSSARY.md:13` منفرداً — حالته `Proposed (G1)`.

**الفحص المنفَّذ:**
1. **طبيعة الادعاء:** الادعاء **وجودُ معجم أوّليّ**، لا **نفاذُ تعريفاته**. المصدر نفسه يقول «أوّلي»، والوثيقة تُعرّف نفسها «§2 المصطلحات (**بذرة**)». فالبند **لا يتطلب نفاذاً معيارياً** ليكون صحيحاً.
2. **التحقق المادي:** المصطلحات الأربعة معرَّفة فعلاً — `Task` (`:13`) · `Schedule` (`:14`) · `Workflow` (`:15`) · `Automation` (`:16`).
3. **البحث عن متبنٍّ نافذ:** `decisions/adr/ADR-0035-contracts-layer-single-source.md:13` (‏`Accepted` — المرتبة 4) يدرج «**System Knowledge (`knowledge/**`)**» ضمن **مصادر التأليف القانونية** لخط توليد الوثائق ⇒ تبنٍّ نافذ **للمسار بوصفه مصدر تأليف**، لا لتعريفاته بوصفها سياسة.
4. **البحث عن تعارض سلطوي:** لم يُوجد — لا مصدر نافذ يعرّف المصطلحات الأربعة تعريفاً مغايراً.

**الحكم:** **بقاء التصنيف `مقنَّن` مع تصحيح وصف الأهلية** — وهي إحدى النتائج الأربع الممكنة المنصوص عليها، لأن الادعاء **لا يتطلب نفاذاً معيارياً**.
**الإجراء المنفَّذ:** العمود الثالث يُفصح الآن صراحةً أن المعجم **بذرة `Proposed (G1)`** وأن «الادعاء وجودُ معجم أوليّ لا نفاذُ تعريفاته»؛ والعمود الرابع يبدأ بالمتبنّي النافذ `decisions/adr/ADR-0035-contracts-layer-single-source.md:13` ثم الوثيقة `knowledge/BUSINESS_GLOSSARY.md:13`.
**ما لا يقرّره هذا الحكم:** لا يجعل تعريفات المعجم سياسةً نافذة، ولا يرقّي حالته، ولا يمس أي صف آخر.

## 4) إثبات صفر `INDEX.md:NNN`
- **الأمر:** `grep -rnoE 'INDEX\.md:[0-9]+' traceability/` — **النتيجة: صفر**.
- الاستشهادات المصحَّحة: **21 ورودَ `INDEX.md:NNN`** + **9 اختصارات `(:NNN)`** تشير إلى أسطر الفهرس داخل جداول الأهلية — كلها حُوِّلت إلى الصيغة الهوياتية (التفصيل في `FINAL-RECONCILIATION-TABLE.md` §5). **أحد هذه التحويلات وقع داخل خلية جدول §10.4** (‏`RAR-003 [09]`) — وهو الصفُّ الخامس عشر في diff الأعمدة 3/4، وقد أُدرج صراحةً في سجل التغييرات بعد إعادة الحساب الآلي.
- الانزياح **مُثبَت لا مُدَّعى**: الرقم **127** في الفهرس كان يعني `ui/UI_DESIGN_SYSTEM.md` في ملفَّي RAR-003 ويعني `ui/UI_ADMIN_CONSOLE_MODEL.md` في ملف RAR-004 — **رقمٌ واحد لمرجعين مختلفين**؛ و`ui/UI_DESIGN_SYSTEM.md` اليوم في السطر **138** و`ui/UI_SCREEN_GOVERNANCE_STANDARD.md` في **145**. *(كُتبت الأرقام هنا نصاً مجرَّداً عمداً — لا بصيغة استشهاد — حفاظاً على قاعدة صفر استشهاد بأرقام أسطر الفهرس.)*

## 5) جدول الأهلية الكامل — 65 مصدراً مميزاً
> العمود «صفوف» = عدد صفوف المصالحة التي تستشهد بالمصدر في العمود الرابع (بعد تصحيحات FINAL-A).

### (أ) مصادر نافذة — 52
| صفوف | المصدر | الحالة | المرتبة/الأهلية |
|---:|---|---|---|
| 66 | `decisions/DEFERRED_IMPLEMENTATION.md` | `Current` | المرتبة 4 (`AUTHORITY.md:13`) — سجل المؤجلات الرسمي |
| 29 | `constitution.md` | `Current / Accepted` | المرتبة 1 (`AUTHORITY.md:10`) |
| 25 | `methodology/RECONCILIATION_ROADMAP.md` | `Accepted — R1-B` | المرتبة 2 (`AUTHORITY.md:11`) |
| 20 | `ui/UI_SCREEN_GOVERNANCE_STANDARD.md` | `Accepted` | المرتبة 8 — **Capstone** وجدولُ الإلزام فيه هو المتبنّي النافذ |
| 19 | `decisions/adr/ADR-0035-contracts-layer-single-source.md` | `Accepted — G1-B` | المرتبة 4 |
| 19 | `ui/UI_ACTION_BUTTON_MODEL.md` | `Current` | المرتبة 8 · ملزم-معياري |
| 16 | `phases/designs/phase-4-advanced-permissions-feature-management.md` | `Accepted (v0.3)` | المرتبة 7 |
| 15 | `phases/designs/phase-7-integrations-app-store.md` | `Accepted (v0.3)` | المرتبة 7 |
| 14 | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md` | `Current` | المرتبة 4 |
| 12 | `phases/BACKLOG_DEFERRED_SCOPE.md` | `Accepted (v0.3)` | **نافذ بحدّ ذاته مقيَّد** — ‏§6 |
| 12 | `phases/designs/phase-3-workflows-approvals-actions.md` | `Accepted (v0.3)` | المرتبة 7 |
| 10 | `ui/UI_AI_WORKSPACE_MODEL.md` | `Current` | المرتبة 8 · ملزم-معياري |
| 9 | `AUTHORITY.md` | `Accepted` | نص السلطة |
| 9 | `ui/UI_FIELD_NAMING.md` | `Current` | المرتبة 8 · **المصدر الكنسي للتسمية** (`ADR-0035:9`) |
| 8 | `methodology/agent-execution-model.md` | `Current` | المرتبة 2 |
| 8 | `phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md` | `Current` | المرتبة 7 |
| 8 | `ui/UI_SCREEN_INVENTORY.md` | `Current` | المرتبة 8 · **السجل المركزي الكنسي للشاشات والمسارات** (`ADR-0035:10`) |
| 6 | `decisions/open-decisions.md` | `Current / Accepted` | المرتبة 4 — المرجع الملزم الوحيد للمفتوح/المقفل |
| 6 | `methodology/PHASE_EXECUTION_STANDARD.md` | `Accepted` | المرتبة 2 |
| 5 | `methodology/testing-strategy.md` | `Current / Accepted` | المرتبة 2 |
| 5 | `phases/designs/phase-6-gateway-agents-sql-chat-reports.md` | `Accepted (v0.3)` | المرتبة 7 |
| 5 | `ui/UI_ADMIN_CONSOLE_MODEL.md` | `Current` | المرتبة 8 · ملزم-معياري |
| 4 | `decisions/adr/ADR-0031-primary-ui-client-nextjs-client-only-rocket.md` | `Accepted — G1-B` | المرتبة 4 |
| 4 | `ui/UI_COMPONENT_STATES.md` | `Current` | المرتبة 8 · ملزم-معياري (‏S1–S20) |
| 3 | `catalogs/Feature_Technical_Architecture_Catalog.md` | `Current / Accepted` | المرتبة 3 |
| 3 | `decisions/adr/ADR-0025-…` · `ADR-0029-…` · `ADR-0037-…` (‏3 ملفات) | `Current` / `Accepted — R1-B` | المرتبة 4 |
| 3 | `methodology/Spec_Driven_Modular_Monolith_Methodology.md` | `Current / Accepted` | المرتبة 2 |
| 3 | `phases/designs/phase-5-files-rag-ocr-media.md` | `Accepted (v0.3)` | المرتبة 7 |
| 3 | `ui/UI_SCREEN_BEHAVIOR_CARDS.md` | `Current` | المرتبة 8 · ملزم-معياري |
| 3 | `FLUTTER_ROLLBACK_AND_OPENWEBUI_BRIDGE_HANDOFF.md` | `Current` | سجل تسليم |
| 2 | `decisions/adr/ADR-0027-…` · `decisions/adr/README.md` | `Current` / `Current / Accepted` | المرتبة 4 |
| 2 | `methodology/coding-standards.md` | `Current / Accepted` | المرتبة 2 |
| 2 | `phases/PHASE_MASTER_PLAN.md` · `phases/phase-roadmap.md` | `Accepted (v0.3)` / `Current / Accepted` | المرتبة 6 |
| 1 | `README.md` · `vision.md` · `architecture/README.md` · `SPECIFICATIONS_CLOSEOUT_HANDOFF.md` | `Current` / `Current / Accepted` | نافذة |
| 1 | `decisions/adr/ADR-0017-…` (`Accepted — Superseded-in-scope`) · `ADR-0018-…` · `ADR-0024-…` · `ADR-0033-…` · `ADR-0038-…` · `decisions/license-review.md` | `Current` / `Accepted` | المرتبة 4 |
| 1 | `phases/designs/phase-1-…` · `phase-8-…` · `phases/phase-0-…` | `Accepted (v0.3)` / `Accepted for Design` | المرتبتان 7 و6 |
| 1 | `ui/UI_REFERENCE_USAGE_POLICY.md` · `ui/UI_UX_ASSUMPTIONS.md` | `Current` | المرتبة 8 · ملزم-معياري |

### (ب) مصادر غير نافذة وحدها — 6
`ui/UI_DESIGN_SYSTEM.md` (12) · `ui/UI_RUN_EXECUTION_MODEL.md` (3) · `ui/UI_INTERACTION_MODEL.md` (2) · `contracts/screens/admin.workflows.md` (1) · `knowledge/BUSINESS_GLOSSARY.md` (1) · `traceability/TRACEABILITY_MATRIX.md` (1) — **كلها الآن مقرونة بمتبنٍّ نافذ أو بدليلٍ نافذ في الصف نفسه**، والتفصيل في §2.

### (ج) مراسي أدلة الغياب — 7
`ABSENCE-EVIDENCE-B1-RAR001..003.md` · `ABSENCE-EVIDENCE-B2-RAR004..007.md` — صيغةٌ **مصرَّح بها** في schema العمود الرابع («دليل حاكم بمسار وسطر · **أو مرساة غياب** · أو سلطتان متعارضتان»). **110 مرساة** فريدة: صفر يتيمة · صفر مكسورة · صفر مكرَّرة (تحقّق آلي).

## 6) ملاحظات أهلية مرفوعة إلى SA (تُسجَّل ولا تُنفَّذ في FINAL-A)
1. **`phases/BACKLOG_DEFERRED_SCOPE.md` غير مرتَّب في السلّم — عولج في B2-FINAL-A CORRECTIVE.** حالته في الفهرس `Accepted (v0.3)` وهو سجلُّ نطاقٍ مؤجَّل بقرار، لكن `AUTHORITY.md` يرتّب من `phases/` **الخارطة والخطة الأم (المرتبة 6 — `:15`)** و**التصاميم (المرتبة 7 — `:16`)** فقط، ولا يذكره؛ و«`Accepted` في الفهرس» **ليست مرتبةَ سلطة** (`AUTHORITY.md:28`).
   **ما نُفِّذ:** فُحص كل صفٍّ يستشهد به فحصاً مستقلاً (‏**12 صفاً**: 11 `مؤجَّل` + 1 `مقنَّن`).
   - **أحد عشر صفاً** ثبت لها **سندٌ مرتَّب مستقل وكافٍ** ⇒ **الحالة 1**: قُدِّم السند المرتَّب دليلاً حاكماً، وخُفِض الملف إلى **سياق مفصح عنه** بصيغة «`سياق فقط — غير حاكم مستقلاً`».
   - **صفٌّ واحد** (‏`RAR-002 [08]`) ثبت أن سنده المرتَّب `ADR-0037:11` **لا يثبت التأجيل** ⇒ **الحالة 3**: أُعيد تقييمه وانتقل من `مؤجَّل بصف قائم` إلى **`مصطنع أو بلا أساس`**.
   **النتيجة:** **صفر صف يعتمد على الملف استقلالاً** · **11 صفاً** يستشهد به سياقاً موسوماً · **صفر تعامل مع `Accepted` بوصفها مرتبة**. والملف **لم يُضَف إلى السلّم ولم تُعدَّل حالته ولا محتواه**، و`AUTHORITY.md` **لم يُعدَّل**.
   **المسألة الحوكمية** (تفويضه سجلاً حاكماً وتحت أي مرتبة ونطاق) **موحَّدة وواحدة**، ومسجَّلة `Governance observation — non-blocking for current reconciliation` في `OWNER-DECISION-PACKAGE.md` §3 — **بلا قرارٍ جديد** وبلا تكرارٍ لكل صف.

2. **تعارض سجلّي مرصود سابقاً ولم يتغيّر:** `traceability/TRACEABILITY_MATRIX.md:16` يسجّل `ui/UI_SCREEN_GOVERNANCE_STANDARD.md` بأنه `Proposed` بينما الفهرس يسجّله `Accepted` بمرجع دمج ووسم. يُحسم بقاعدة `AUTHORITY.md` (الفهرس دليل مواضع وحالات، والمصفوفة بذرة `Proposed`) — **لا قرار مالك مطلوب**، وسُجّل ملاحظةً.
3. **`contracts/**` كطبقة:** المرتبة 5 تشترط **`Approved`** نصاً (`AUTHORITY.md:14`)، ولا عقد واحد بهذه الحالة اليوم (‏4 بذور `Candidate` + 3 معايير `Proposed (G1)`). فالمرتبة 5 **خالية فعلياً** عند HEAD — واقعٌ يُسجَّل ولا يُعالَج هنا.

---

**Related:** `FINAL-RECONCILIATION-TABLE.md` · `OWNER-DECISION-PACKAGE.md` · `RECONCILIATION-RAR-001.md`..`007.md` · `AUTHORITY.md` · `INDEX.md`
