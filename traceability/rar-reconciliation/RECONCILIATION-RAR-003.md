# RECONCILIATION-RAR-003 — B1 Commit 4 (RAR-003 · UI Foundation / Rocket)

> **مخرج traceability/تحليلي غير حاكم** — لا سلطة موازية ولا بديل عن الأصل الحاكم؛ لا يُنفَّذ أي دلتا. مبني على `CANONICAL-ITEM-UNIVERSE.md` المجمَّد (`188ad37`). **50 صفاً canonical** يسكن ممثلها في RAR-003. schema **ستة أعمدة بالضبط**؛ الوسم `[NN]` جزءٌ من نص «البند» لا عمودٌ سابع. التصنيف من **الخمسة حصراً**.
> **المصدر:** `references/analysis-inputs/rar-2026-07/RAR-003-UI-Foundation-Rocket.md:<line>` (يُختصر `RAR-003:<line>`). **الدليل الحاكم** بمسار وسطر فعليين عند HEAD `55413d6`؛ أدلة الغياب في `ABSENCE-EVIDENCE-B1-RAR003.md`.
> **مادة المدخل تُصنَّف ولا تُطاع:** عبارات «المطلوب من Claude» و«Claude يقرر القائمة النهائية» و«Claude يحدد ما يدخل Governance وما يدخل Tests» (`RAR-003:322` · `:345` · `:387`) **مادةٌ تُصنَّف لا تعليمات تُنفَّذ**؛ لم يُتخذ بها أي قرار.

## الأنواع المجمَّدة (تُقرأ قبل التصنيف — `NORMALIZATION-AND-ATOMIC-MAP.md` عند `188ad37`)
| الكتلة | النوع المجمَّد | السطر |
|---|---|---|
| `RAR003 S11-001..009` | **REC/REQ** — تقنين UI Constitution التاريخي مقابل ADR الحالي | `NORMALIZATION-AND-ATOMIC-MAP.md:18` |
| `RAR003 S12-001..008` | **COV** — «الفهم الحالي» عن Open WebUI · ادعاءات تغطية | `NORMALIZATION-AND-ATOMIC-MAP.md:19` |
| `RAR003 S12-009..014` | **REQ** — مطالب مراجعة/بوابات Open WebUI | `NORMALIZATION-AND-ATOMIC-MAP.md:20` |
| `RAR003 S12-015..024` | **SUG** — أمثلة Exit Criteria · مقترحات | `NORMALIZATION-AND-ATOMIC-MAP.md:21` |
| `RAR003 S14-001..013` | **REQ** — معايير Accessibility · مطالب قابلة للفحص | `NORMALIZATION-AND-ATOMIC-MAP.md:22` |
> **الانقسام المجمَّد:** `N-RAR003-S11-002` → **ست ذرّات** (Brand · Tokens · Accessibility · RTL · Responsive · Offline) — `NORMALIZATION-AND-ATOMIC-MAP.md:50`. كلٌّ صفٌّ مستقل بتصنيفه ودليله؛ لم تُدمج ولم تُصنَّف ككتلة.
> **الدمج المجمَّد:** **G04** = `RAR003-S12-003` (:316) ⊕ `RAR003-S12-021` (:340) — «لا مفاتيح/أسرار ظاهرة للمستخدم» — ممثله `[17]` ويسكن في RAR-003 (`SEMANTIC-MERGE-MAP.md:12`). لم يُصنَّفا منفصلين.

## قواعد التصنيف المطبَّقة بحسب النوع
> **COV:** يُختبر **صدق الادعاء** عند HEAD — صحيح ⇒ `مقنَّن` بالاستشهاد؛ غير صحيح أو بلا سند ⇒ `مصطنع أو بلا أساس`. **لا يصير `دلتا حقيقية`** لمجرد أنه غير مُثبَت.
> **SUG:** تبنّاه المستودع ⇒ `مقنَّن` · له صف تأجيل قائم ⇒ `مؤجَّل بصف قائم` · لم يُتبنَّ ⇒ `مصطنع أو بلا أساس`. **لا يصير `دلتا حقيقية`** إلا بإثبات أن **الحاجة نفسها مستقرة في مصدر حاكم**، مع الاستشهاد — وقد طُبِّق هذا الاستثناء **مرة واحدة** (`[29]`، بسند `ADR-0030:11`).
> **REC/REQ:** صُنِّف كل بند على حدة. **REC** (توصية تُعامل كاقتراح): `[01]`,`[08]`,`[09]`,`[10]`,`[11]`,`[12]`,`[13]`,`[14]` — لأنها صيغ توصية على مادة تحريرية («قارن» · «افصل» · «أزل» · «لا تصف» · «اسمح» · «لا تفرض» · «حدِّد»). **REQ** (مطلب بالدليل): الذرّات الست `[02]..[07]` — لأنها قواعد واجبة الحفظ لا اقتراحات.
> **`تعارض يحتاج قراراً`** لا يُسند إلا بانطباق أحد محفّزات §14-هـ الأربعة مع **تسمية القرار المالك وبديلين** — ولم ينطبق على أي صف (التفصيل أسفل الجدول).

## أهلية الدليل (حالة INDEX تحكم)
`ui/UI_DESIGN_SYSTEM.md` حالته في `INDEX.md:127` **`Proposed`**، فلا يصلح **وحده** لإثبات سياسة نافذة. لكنّ `ui/UI_SCREEN_GOVERNANCE_STANDARD.md` (**`Accepted`** — `INDEX.md:138`) يجعله **ملزماً-معيارياً بالإحالة**: `:10` يدرجه في قائمة «مخالفتها عيب يُرد»، و`:68` يوجّه قبول `RTL/i18n/Light-Dark/Responsive/a11y` إلى **`DESIGN_SYSTEM §§9–11`**. لذلك **يُستشهد بهما معاً** حيثما لزم إثبات سياسة، ولا يُستشهد بـ`UI_DESIGN_SYSTEM` منفرداً.
> **ملاحظة تعارض سجلات (لا حكم):** `traceability/TRACEABILITY_MATRIX.md:16` يسجّل حالة `UI_SCREEN_GOVERNANCE_STANDARD.md` بأنها `Proposed` بينما `INDEX.md:138` يسجّلها `Accepted` بمرجع دمج ووسم. يُحسم بقاعدة `AUTHORITY.md:28` (الفهرس دليل مواضع الملفات **وحالاتها**) ⇒ صفّ المصفوفة **قديم غير محدَّث**، لا سلطة موازية. سُجِّل هنا للتدقيق ولم يُبنَ عليه تصنيف.

| البند (canonical) | المصدر | الحالة عند HEAD | الدليل | التصنيف | الوجهة |
|---|---|---|---|---|---|
| **[01]** مقارنة مبادئ UI Constitution التاريخي مع ADR الحالي | RAR-003:298 | لا وثيقة `UI Constitution` في المستودع الحاكم؛ حوكمة الواجهة قائمة بحزمة ملفات `ui/` الملزمة-معيارياً | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-001` | مصطنع أو بلا أساس | لا وجهة |
| **[02]** ذرّة Brand — حفظ قاعدة الهوية البصرية | RAR-003:299 (ATOM-a) | هوية «قيادة مؤسسية هادئة» + مبادئ الشخصية البصرية + منع نسخ هوية أي منتج مرجعي | `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:10` · `ui/UI_DESIGN_SYSTEM.md:5` · `ui/UI_REFERENCE_USAGE_POLICY.md:15` | مقنَّن | الأصل |
| **[03]** ذرّة Tokens — حفظ قاعدة رموز التصميم | RAR-003:299 (ATOM-b) | رموز بأسماء ثابتة وقيم قابلة للاستبدال بهوية الجهة؛ ألوان محجوزة للتصنيف | `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:10` · `ui/UI_DESIGN_SYSTEM.md:17` | مقنَّن | الأصل |
| **[04]** ذرّة Accessibility — حفظ قاعدة الإتاحة | RAR-003:299 (ATOM-c) | قبول a11y موجَّه إلى `DESIGN_SYSTEM §§9–11` بصيغة قابلة للاختبار؛ §9 يقنِّن خمسة معايير | `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:68` · `ui/UI_DESIGN_SYSTEM.md:111` | مقنَّن | الأصل |
| **[05]** ذرّة RTL — حفظ قاعدة الاتجاه | RAR-003:299 (ATOM-d) | `dir` بحسب اللغة · خصائص منطقية حصراً · عزل ثنائي الاتجاه إلزامي · انعكاس الأيقونات الاتجاهية | `ui/UI_DESIGN_SYSTEM.md:114` · `ui/UI_AI_WORKSPACE_MODEL.md:70` | مقنَّن | الأصل |
| **[06]** ذرّة Responsive — حفظ قاعدة الاستجابة | RAR-003:299 (ATOM-e) | قواعد الاستجابة تحفظ المقروئية والإتاحة وRTL وثبات التخطيط ثنائي اللغة · موروثة لكل نمط شاشة | `ui/UI_DESIGN_SYSTEM.md:56` · `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:42` | مقنَّن | الأصل |
| **[07]** ذرّة Offline — حفظ قاعدة العمل دون اتصال | RAR-003:299 (ATOM-f) | لا offline-write في v1 (S16 عرضٌ وإعادة محاولة فقط) · النظام air-gapped وقت التشغيل | `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:56` · `constitution.md:12` | مقنَّن | الأصل |
| **[08]** فصل Brand عن Frontend Engineering إذا لزم | RAR-003:300 | الفصل قائم: نظام التصميم يعرّف الرموز والتنفيذ «يلبسها» لاحقاً؛ ومعايير الكود طبقة مستقلة | `ui/UI_DESIGN_SYSTEM.md:4` · `methodology/coding-standards.md:22` | مقنَّن | الأصل |
| **[09]** إزالة أو Supersede إشارات Stack قديمة | RAR-003:301 | آلية الإحلال مطبَّقة: ADR-0017 موسوم `Superseded-in-scope` بقرار ADR-0031، وREADME يفسّر النطاق | `INDEX.md:30` · `decisions/adr/ADR-0031-primary-ui-client-nextjs-client-only-rocket.md:22` | مقنَّن | الأصل |
| **[10]** عدم وصف 44×44 بأنه شرط WCAG عالمي | RAR-003:302 | قاعدة المستودع **«أهداف لمس ≥40px»** بلا أي ادعاء بأنها شرط WCAG عالمي | `ui/UI_DESIGN_SYSTEM.md:111` · `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:68` | مقنَّن | الأصل |
| **[11]** السماح باستثناءات موثقة للـInline Computed Styles | RAR-003:303 | لا قاعدة تمنع الأنماط المضمّنة ولا ذكر لـReact Flow؛ فلا منعٌ يُستثنى منه | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-002` | مصطنع أو بلا أساس | لا وجهة |
| **[12]** عدم فرض منع CSS داخل Screens مطلقاً (الممنوع القيم الاعتباطية والهوية لكل شاشة) | RAR-003:304 | لا منع لـCSS في الشاشات ولا قاعدة «قيم اعتباطية» في المستودع الحاكم | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-003` | مصطنع أو بلا أساس | لا وجهة |
| **[13]** تحديد Version Canonical واحدة لوثيقة UI Constitution | RAR-003:305 | موضوع التوصية (الوثيقة التاريخية) غير موجود في المستودع؛ ونظام الإصدارات القائم يخص ملفات المستودع لا وثيقةً خارجه | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-004` | مصطنع أو بلا أساس | لا وجهة |
| **[14]** تحديد ما ينتقل إلى Code Standards وما يبقى Design Governance | RAR-003:306 | الفصل مقنَّن فعلاً: قائمة `ui/` الملزمة-معيارياً (حوكمة تصميم) مقابل `methodology/coding-standards.md` (معايير كود) | `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:10` · `methodology/coding-standards.md:22` | مقنَّن | الأصل |
| **[15]** [COV] Open WebUI ليس الواجهة النهائية | RAR-003:314 | **الادعاء صحيح:** «ليست الواجهة الدائمة» قرارٌ نافذ، والواجهة النهائية Enterprise UI خاصة | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:9` · `README.md:16` | مقنَّن | الأصل |
| **[16]** [COV] معزول عن Domain Logic | RAR-003:315 | **الادعاء صحيح:** تكامل معزول · لا DB مباشراً · لا اعتماد للمنصة على جداوله · اتجاه اعتماد أحادي | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:9` · `FLUTTER_ROLLBACK_AND_OPENWEBUI_BRIDGE_HANDOFF.md:58` | مقنَّن | الأصل |
| **[17]** [COV · ممثل G04] لا مفاتيح/أسرار ظاهرة للمستخدم (يستوعب «No user-visible keys») | RAR-003:316 · :340 | **الادعاء صحيح:** حدود D9 — لا شاشة تُظهر endpoints/secrets/مفاتيح؛ و«صفر أسرار/endpoints» وراثة عامة لكل نمط شاشة | `ui/UI_UX_ASSUMPTIONS.md:23` · `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:42` | مقنَّن | الأصل |
| **[18]** [COV] يعتمد هوية/جلسة محكومة من المنصة وفق التصميم | RAR-003:317 | **الادعاء صحيح تصميمياً:** الجسر لا يقرر صلاحيات والمنصة تعيد التحقق وتملك القرار (مبدأ العميل القابل للاستبدال) | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:9` · `decisions/adr/ADR-0029-replaceable-client-principle.md:9` | مقنَّن | الأصل |
| **[19]** [COV] Actions الحساسة تمر Server-side مع Confirmation | RAR-003:318 | **الادعاء صحيح:** الخادم مصدر التحقق والصلاحيات والتنفيذ؛ كل نداء عبر العقود المعلنة ولا صلاحيات في العميل | `decisions/adr/ADR-0031-primary-ui-client-nextjs-client-only-rocket.md:16` · `FLUTTER_ROLLBACK_AND_OPENWEBUI_BRIDGE_HANDOFF.md:58` | مقنَّن | الأصل |
| **[20]** [COV] له Decommission Plan | RAR-003:319 | **الادعاء صحيح:** شروط الخروج وتسلسله مقنَّنان (تشغيل متوازٍ → إيقاف الجديد → تصدير/هجرة → تعطيل → إبقاء التدقيق → إزالة باعتماد) | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:11` · `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:20` | مقنَّن | الأصل |
| **[21]** [COV] توجد أو يفترض وجود اختبارات Replacement/Isolation/Upgrade | RAR-003:320 | **الادعاء صحيح جزئياً وبالقدر المُدَّعى (صيغة «أو يفترض»):** REPLACEMENT_TEST_SPEC وISOLATION_TEST_SPEC قائمتان بالاسم كبوابة تفعيل؛ **لا مقابل لاختبار Upgrade** | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:28` | مقنَّن | الأصل |
| **[22]** [COV] Multi-user/session/identity/license/scale لم تثبت تشغيلياً بعد | RAR-003:321 | **الادعاء صحيح:** أربع بوابات تفعيل غير مستوفاة — صف الترخيص المعلق · قائمة فحص Scale/Identity/Sessions · digest الصورة · اجتياز الاختبارين | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:28` | مقنَّن | الأصل |
| **[23]** [مطلوب] فحص ADR والخطة الحالية | RAR-003:325 | ADR-0030 نافذ `Accepted` بقراره وحدوده وبواباته وشروط خروجه، وملحقه Δ يقيّد التفعيل | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:22` · `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:28` | مقنَّن | الأصل |
| **[24]** [مطلوب] تحديد Exit Criteria قابلة للقياس | RAR-003:326 | شرط الخروج معلَن نوعياً («الحد الأدنى من واجهة React البديلة متاح») بلا معايير مقيسة قابلة للفحص | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:11` · `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-005` | دلتا حقيقية | الأصل (ADR-0030 · DECOMMISSION_PLAN) |
| **[25]** [مطلوب] تحديد الوظائف التي يجب أن توفرها AQL UI قبل الإزالة | RAR-003:327 | «الحد الأدنى» غير مُعدَّد وظيفياً في أي مصدر حاكم داخل المستودع | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:11` · `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-006` | دلتا حقيقية | الأصل (ADR-0030 · DECOMMISSION_PLAN) |
| **[26]** [مطلوب] منع تسرب Contracts خاصة بـOpen WebUI إلى Domain | RAR-003:328 | لا اعتماد للمنصة على جداول Open WebUI الداخلية (معرفات محايدة + تسجيل فوري)؛ اتجاه الاعتماد أحادي | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:9` · `FLUTTER_ROLLBACK_AND_OPENWEBUI_BRIDGE_HANDOFF.md:58` | مقنَّن | الأصل |
| **[27]** [مطلوب] تحديد Scale/Identity/License checks قبل أول تفعيل | RAR-003:329 | الأربعة معاً شرطُ تفعيل معلن: صف الترخيص · قائمة فحص التشغيل متعدد المستخدمين (Scale/Identity/Sessions) · digest · الاختباران | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:28` | مقنَّن | الأصل |
| **[28]** [مطلوب] عدم تشغيل أو دمج Open WebUI في هذه الجولة | RAR-003:330 | scaffold موثق أولاً **ولا تشغيل قبل استيفاء بواباته**؛ ولا تفعيل تشغيلي قبل استيفاء الأربعة معاً | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:8` · `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:28` | مقنَّن | الأصل |
| **[29]** [SUG · Exit] Chat workspace في AQL يغطي الاستخدامات المطلوبة | RAR-003:334 | **الحاجة مستقرة في مصدر حاكم** (توفّر الحد الأدنى من الواجهة البديلة شرطُ خروج) لكن التغطية غير مُعدَّدة | `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:11` · `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-007` | دلتا حقيقية | الأصل (ADR-0030 · DECOMMISSION_PLAN) |
| **[30]** [SUG · Exit] SSO/session يعمل | RAR-003:335 | التنفيذ البرمجي للهوية (Local Auth + SSO/OIDC) بصف مؤجلات رسمي؛ وSSO/SAML الموسّع بصف backlog ببوابته | `decisions/DEFERRED_IMPLEMENTATION.md:9` · `phases/BACKLOG_DEFERRED_SCOPE.md:16` | مؤجَّل بصف قائم | سجل المؤجلات · backlog (بعد P1 بطلب) |
| **[31]** [SUG · Exit] Evidence presentation يعمل | RAR-003:336 | متبنّى: الاستشهادات تُحفظ مع كل رسالة، وادعاء بلا مصدر يُحجب برفض No-Guessing (fail-closed) | `phases/designs/phase-6-gateway-agents-sql-chat-reports.md:29` · `phases/designs/phase-6-gateway-agents-sql-chat-reports.md:30` | مقنَّن | الأصل |
| **[32]** [SUG · Exit] Approved actions تعمل عبر server-side bridge | RAR-003:337 | متبنّى: لا منطق أعمال في العميل والخادم مصدر التحقق والصلاحيات والتنفيذ والتدقيق | `decisions/adr/ADR-0031-primary-ui-client-nextjs-client-only-rocket.md:16` · `decisions/adr/ADR-0029-replaceable-client-principle.md:9` | مقنَّن | الأصل |
| **[33]** [SUG · Exit] Conversation history أو بديلها يعمل وفق السياسة | RAR-003:338 | آلية مزامنة/استيراد المحادثات تصميمٌ مؤجَّل بصف رسمي مربوط بخطة التخلص | `decisions/DEFERRED_IMPLEMENTATION.md:10` | مؤجَّل بصف قائم | سجل المؤجلات (مربوط بخطة التخلص) |
| **[34]** [SUG · Exit] Export/attachments المطلوبة متاحة | RAR-003:339 | متبنّى: تصدير محكوم بفحص تصنيف كل حقل/صف + وسم + audit؛ ومرفقات بميتاداتا وتصنيف وصلاحيات موروثة | `phases/designs/phase-4-advanced-permissions-feature-management.md:36` · `phases/designs/phase-5-files-rag-ocr-media.md:27` | مقنَّن | الأصل |
| **[35]** [SUG · Exit] Audit مكتمل | RAR-003:341 | متبنّى: م3 Audit شامل append-only، وكل إجراء منفّذ عبر الجسر يسجَّل في المنصة فوراً وسجلات التدقيق تبقى فيها | `constitution.md:11` · `decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md:20` | مقنَّن | الأصل |
| **[36]** [SUG · Exit] Replacement test ناجح | RAR-003:342 | اختبار الاستبدال بندٌ قائم في سجل المؤجلات الرسمي، وADR-0031 يجعله مرجع إثبات قابلية الاستبدال | `decisions/DEFERRED_IMPLEMENTATION.md:8` · `decisions/adr/ADR-0031-primary-ui-client-nextjs-client-only-rocket.md:15` | مؤجَّل بصف قائم | سجل المؤجلات |
| **[37]** [SUG · Exit] بيانات قابلة للنقل أو التصدير | RAR-003:343 | Data/File Portability بصف مؤجلات رسمي بقرار مالك، وجهته R9 → P5/P8 | `decisions/DEFERRED_IMPLEMENTATION.md:25` | مؤجَّل بصف قائم | R9 → P5/P8 |
| **[38]** Semantic HTML | RAR-003:373 | لا معيار لعناصر HTML الدلالية/الـlandmarks في حزمة الإتاحة الحاكمة | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-008` | دلتا حقيقية | R3 |
| **[39]** Keyboard access | RAR-003:374 | تنقّل لوحة مفاتيح كامل يشمل داخل البطاقات وأزرارها؛ وموروث عام لكل نمط شاشة وللصفوف في القوائم | `ui/UI_DESIGN_SYSTEM.md:111` · `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:42` | مقنَّن | الأصل |
| **[40]** Focus order | RAR-003:375 | لا قاعدة لترتيب التركيز/تسلسل الانتقال (الموجود يخص **مظهر** حلقة التركيز لا ترتيبه) | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-009` | دلتا حقيقية | R3 |
| **[41]** Visible focus | RAR-003:376 | `focus ring` واضح 2px بلون primary — معيار مقنَّن وقابل للفحص | `ui/UI_DESIGN_SYSTEM.md:111` · `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:68` | مقنَّن | الأصل |
| **[42]** Labels and descriptions | RAR-003:377 | لا قاعدة اسم/وصف قابل للقراءة الآلية للعناصر (الموجود التزام i18n لكل نص — غرضه الترجمة لا الإتاحة) | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-010` | دلتا حقيقية | R3 |
| **[43]** Error association | RAR-003:378 | لا ربط آلي بين رسالة الخطأ وحقلها (الموجود **تثبيت بصري** للأخطاء على الحقول داخل البطاقة) | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-011` | دلتا حقيقية | R3 |
| **[44]** Dialog focus trapping | RAR-003:379 | لا قاعدة لحصر التركيز داخل الحوارات/الأدراج رغم اعتماد نمطَي drawer/modal | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-012` | دلتا حقيقية | R3 |
| **[45]** Contrast | RAR-003:380 | **تباين AA حداً أدنى** + «لا معنى ينقله اللون وحده»، وقبول a11y موجَّه إلى `DESIGN_SYSTEM §§9–11` بصيغة قابلة للاختبار | `ui/UI_DESIGN_SYSTEM.md:111` · `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:68` | مقنَّن | الأصل |
| **[46]** Reduced motion | RAR-003:381 | لا قاعدة لاحترام تفضيل تقليل الحركة (الموجود سقف مدة الانتقالات ≤200ms — غرضه الطابع لا الإتاحة) | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-013` | دلتا حقيقية | R3 |
| **[47]** Screen reader announcements | RAR-003:382 | قارئ الشاشة يعلن حالة البطاقة والشارات **نصاً**، ويقرأ حالة البطاقة (S-state) في سطح المحادثة | `ui/UI_DESIGN_SYSTEM.md:111` · `ui/UI_AI_WORKSPACE_MODEL.md:70` | مقنَّن | الأصل |
| **[48]** Data table semantics | RAR-003:383 | لا دلالات جدول بيانات (رؤوس/نطاقات/عنوان) رغم أن نمط List أساس في الجرد | `ABSENCE-EVIDENCE-B1-RAR003.md#absence-b1-rar003-014` | دلتا حقيقية | R3 |
| **[49]** Accessible canvas alternatives | RAR-003:384 | الـcanvas المعقد **مؤجَّل بقرار OD-P3-2** وعقد v1 يبقى على الجدول المهيكل بديلاً؛ ومصيره يُحسم ببوابته لا صمتاً | `decisions/open-decisions.md:159` · `contracts/screens/admin.workflows.md:38` | مؤجَّل بصف قائم | OD-P3-2 (بوابته) |
| **[50]** Touch target policy المعقولة | RAR-003:385 | **أهداف لمس ≥40px** — سياسة معقولة مقنَّنة بلا ادعاء WCAG عالمي (قارن `[10]`) | `ui/UI_DESIGN_SYSTEM.md:111` · `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:68` | مقنَّن | الأصل |

## توزيع التصنيفات (50)
**مقنَّن = 31** · **مؤجَّل بصف قائم = 5** ([30],[33],[36],[37],[49]) · **دلتا حقيقية = 10** ([24],[25],[29],[38],[40],[42],[43],[44],[46],[48]) · **تعارض يحتاج قراراً = 0** · **مصطنع أو بلا أساس = 4** ([01],[11],[12],[13]). المجموع = **50** ✓ (§11 = 14 · §12 = 23 · §14 = 13).

> **ضبط خطر النوعين COV وSUG:** ثمانية بنود COV ([15]–[22]) صُنِّفت **باختبار صدق الادعاء** لا بغيابه، فلم يتحول أيٌّ منها إلى دلتا. وتسعة بنود SUG ([29]–[37]) وُزِّعت: أربعة **مؤجَّل بصف قائم** بصفوف رسمية، وأربعة **مقنَّن** بتبنٍّ فعلي، وواحد فقط **دلتا حقيقية** ([29]) بعد إثبات أن الحاجة نفسها مستقرة في `ADR-0030:11`. **صفر SUG أو COV صُنِّف دلتا بلا إثبات صريح.**
> **لماذا صفر «تعارض يحتاج قراراً»:** فُحص كل صف غير مقنَّن على المحفّزات الأربعة فلم ينطبق أيٌّ منها. أقرب مرشّح كان توجيه معايير الإتاحة السبعة بين **Governance** و**Tests**، وقد **حسمه المستودع سلفاً**: `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:68` يوجّه قبول a11y إلى `DESIGN_SYSTEM §§9–11` بصيغة قابلة للاختبار — فالوجهة محسومة والناقص **محتوى المعيار** ⇒ دلتا حقيقية لا تعارض. ومرشّح ثانٍ كان تعارض `React/Vite` مقابل `Next.js`، وقد حُسم بالإحلال المعلن (`INDEX.md:30` · `ADR-0031:22`) وبـ`README.md:24` — لا قرار مالك معلَّق.

## CANDIDATE BLOCKING (RAR-003)

**CANDIDATE BLOCKING — FP-0001 — pending final determination**

| الحقل | البيان |
|---|---|
| **canonical IDs** | `[38]` `[40]` `[42]` `[43]` `[44]` `[46]` `[48]` — سبعة معايير إتاحة |
| **المصدر** | `RAR-003:373` · `:375` · `:377` · `:378` · `:379` · `:381` · `:383` |
| **التصنيف** | دلتا حقيقية (سبعتها) |
| **الدليل** | `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:68` (Accepted) يشترط قبول a11y عبر `DESIGN_SYSTEM §§9–11` **«بصيغة قابلة للاختبار»** · `ui/UI_DESIGN_SYSTEM.md:111` (§9) يقنِّن **خمسة** معايير فقط (تباين AA · focus ring · تنقّل لوحة مفاتيح · إعلان قارئ الشاشة · لمس ≥40px) · السبعة الباقية بلا معيار — مراسي `absence-b1-rar003-008..014` |
| **الوجهة** | R3 |
| **سبب احتمال الحجب** | `FP-0001` أول حزمة أساس (Retrofit عقدي — `contracts/screens/admin.record_types.md:13`) وقبولها يجري عبر حزمة حوكمة الشاشات التي تعلن a11y **قابلاً للاختبار**؛ فمرور الحزمة ممكن بلا أي معيار لسبعةٍ من ثلاثة عشر فحصاً معلَناً — أي قبولٌ بلا أساس فحص للإتاحة |
| **البوابة المتأثرة** | `FP-0001` (وبالوراثة بوابة UI Foundation `G4` التي تشترط اجتياز الحراس بالأدلة — `ADR-0031:22`) |
| **ما يلزم للحكم النهائي** | قرار مالك يحدّد أيُّ السبعة يدخل **Governance** (معيار مقنَّن في `DESIGN_SYSTEM §9`) وأيُّها يدخل **Tests** (`methodology/testing-strategy.md`)؛ ثم تقنينه في R3. **المدخل التحليلي لا يملك حسمه** (§1). لا يُحسم قبل اكتمال B2 وحساب §13b |

**لا مرشّح حجب آخر في RAR-003** — ولا يمس أي بند `G2` أو `R6` أو `GATE-DEFINITION` بما يشكّل حجباً.
> **حدود هذا الإعلان:** مرشّح لا حكم · **لم تُطبَّق خريطة §18** · لم يُجمَّد أي مسار · **لا `NO BLOCKING DELTA` ولا `BLOCKING DELTA DETECTED`** · **§13b تبقى `PENDING`** حتى اكتمال B2.

## ثبات المدخل والقاعدة
لم تُعدَّل وثائق RAR ولم تُنفَّذ أي دلتا ولم تُلمس ملفات canonicalization الأربعة (`188ad37` — byte-identical) ولا ملفات RAR-001 وRAR-002. لا اختراع دليل: كل «مقنَّن» و«مؤجَّل» بمسار+سطر فعلي، وكل «دلتا» و«مصطنع» بمرساة في `ABSENCE-EVIDENCE-B1-RAR003.md` قابلة لإعادة التنفيذ **بالعربية والإنجليزية معاً**.
