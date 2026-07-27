# ABSENCE-EVIDENCE-B2-RAR005 — B2-B (RAR-005 · Workflow Decision Model)

> **مخرج traceability/تحليلي غير حاكم** — لا سلطة موازية ولا بديل عن الأصل الحاكم. حزمة أدلة غياب **قابلة لإعادة التنفيذ** تسند صفوف `RECONCILIATION-RAR-005.md`. كل حالة بمرساة HTML صريحة بأحرف صغيرة. **HEAD المنفَّذ عليه البحث:** `4bb60ab80356c3dd68918ad676d707fc065c9c85` · **تاريخ البحث:** 2026-07-27.
> **نطاق مشترك مستثنى من «الحاكم»:** `references/analysis-inputs/**` (مدخل تحليلي غير حاكم خارج authority ladder) · `traceability/rar-reconciliation/**` (مخرجات المصالحة نفسها — لا تُثبت ذاتها) · `superseded/**` (تاريخي منسوخ — محظور إلا بتكليف صريح، `AUTHORITY.md:22`). **المسارات المشمولة:** كل ملف `.md` متعقَّب خارج المستثنى — **100 ملفاً** من أصل 145 عند HEAD (`git ls-files '*.md' | grep -vE '<المستثنى>' | wc -l`).
> **الأمر القياسي:** `grep -rInE "<terms>" . --include='*.md' | grep -viE 'references/analysis-inputs/|traceability/rar-reconciliation/|superseded/'`
>
> ### قاعدتان إلزاميتان مطبَّقتان في كل حالة أدناه
> **(أ) ثنائية اللغة —** كل حزمة نُفِّذت **بأمرين منفصلين**: مصطلحات إنجليزية ومقابلها العربي، ونتيجتاهما مسجَّلتان معاً. نتيجة صفرية بلغة واحدة **لا تثبت الغياب**. *(السابقة الموجِبة في هذه الحزمة: `absence-b2-rar005-000` و`-001` — نتيجة إنجليزية **صفر** بينما أرجع العربي مطابقات، إحداها هي الصف القائم الذي غيّر تصنيف خمسة عشر صفاً.)*
> **(ب) الأسطر الكاملة —** المستودع يحوي أسطراً طويلة تجمع عدة التزامات مفصولة بـ`·` أو `؛`. **كل فحص أدناه قرأ السطر بتمامه** — لا مقتطف مقصوص ولا معاينة محدودة الأحرف. الأسطر الجامعة التي قُرئت كاملةً ووُثِّق ذلك: `phases/designs/phase-3-workflows-approvals-actions.md:12` و`:15` · `phases/designs/phase-4-advanced-permissions-feature-management.md:12` · `ui/UI_SCREEN_BEHAVIOR_CARDS.md:100` و`:103` و`:124` · `ui/UI_ACTION_BUTTON_MODEL.md:89` · `ui/UI_RUN_EXECUTION_MODEL.md:87` · `phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md:20` و`:22` · `ui/UI_ADMIN_CONSOLE_MODEL.md:70` · `methodology/PHASE_EXECUTION_STANDARD.md:20`.
>
> **ممنوع** وصف مطابقة بأنها «الوحيدة» ما لم يُرجع الأمر الموثَّق ذلك العدد بالضبط.

> **أهلية المصادر (قاعدة نافذة — حالة `INDEX.md` تحكم):** لم يُستشهد أدناه بمصدرٍ حالته `Proposed`/`Candidate` لإثبات نفاذ التزام. المصادر `Proposed` التي وردت ذُكرت **سياقاً أو مطابقةً قريبة** مع الإفصاح عن حالتها: `knowledge/BUSINESS_GLOSSARY.md` = `Proposed (G1)` (INDEX.md → row for `knowledge/BUSINESS_GLOSSARY.md` → status `Proposed (G1)`) · `contracts/screens/admin.workflows.md` = `Candidate` (INDEX.md → row for `contracts/screens/admin.workflows.md` → status `Candidate` — ورتبة العقود تشترط **Approved**، `AUTHORITY.md:14`) · `ui/UI_RUN_EXECUTION_MODEL.md` = `Proposed (v0.6)` (INDEX.md → row for `ui/UI_RUN_EXECUTION_MODEL.md` → status `Proposed (v0.6)`) — ويُستشهد به **مقروناً** بـ`ui/UI_SCREEN_GOVERNANCE_STANDARD.md:10` (`Accepted`) الذي يصنّفه **ملزم-معيارياً** نصاً، فالناسخ النافذ هو المستشهَد به.
> **أرقام أسطر `INDEX.md` أدناه وفي `RECONCILIATION-RAR-005.md` مأخوذة من `INDEX.md` بعد صفَّي هذه الدفعة** (أي كما ستقرأ عند HEAD الجديد) — لا قبلها.

---

<a id="absence-b2-rar005-000"></a>
### ABSENCE-B2-RAR005-000 — حصر الذِكر الحاكم لمؤقتات SLA والتصعيد المتقدم
- **الغرض:** تحديد ما إذا كانت سياسة SLA/التصعيد مقنَّنة أم محجوزة بصفوف قائمة — وهو الأساس الذي تُبنى عليه صفوف §12.
- **السؤال:** هل يقنِّن المستودع مؤقتات SLA أو تصعيداً مُشغَّلاً بالوقت، أم يحجزها بصفٍّ قائم؟
- **المصطلحات (EN):** `SLA timer` · `advanced escalation` · `escalation policy` · `SLA policy`. **(AR):** `مؤقتات SLA` · `تصعيد متقدم` · `سياسة SLA` · `عقد SLA`.
- **الأمر (EN):** `grep -rInE 'SLA timer|advanced escalation|escalation policy|SLA policy' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'مؤقتات SLA|تصعيد متقدم|سياسة SLA|عقد SLA' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 3**
- **المطابقات الثلاث — كلها صفوف حجز لا تقنين:**
  - `phases/designs/phase-3-workflows-approvals-actions.md:15` — **Out of Scope** لـP3، والسطر كامله: «أي تنفيذ/صياغة عبر LLM (P6) · قنوات إشعار خارجية email/SMS (Backlog — الطبقة مجرّدة) · **مؤقتات SLA وتصعيد متقدم (Backlog)** · تكاملات خارجية (P7) · مصفوفات SoD/ABAC الكاملة (P4 — هنا SoD الأساسي للاعتمادات).»
  - `phases/BACKLOG_DEFERRED_SCOPE.md:23` — صف نطاق مؤجَّل بقرار: «SLA/تصعيد متقدم للworkflows | **الأساسي (تذكيرات استحقاق) يكفي أولاً** | بعد P3 | تصميم مصغّر».
  - `knowledge/BUSINESS_GLOSSARY.md:20` — تعريف SLA وإحالته إلى «عقد SLA-Policy (P3 — توثيق)». **حالته `Proposed (G1)`** ⇒ سياقٌ لا إثبات نفاذ.
- **صفٌّ قائم ثالث لا يُرجعه هذا الأمر (وجد ببحث مستقل):** `methodology/RECONCILIATION_ROADMAP.md:13` — **R5** «Workflow/Org & SLA Contracts Detail | إغلاق حقول الملكية وusing/step-scope + **عقدا SLA-Policy/Templates** + حسم CC-WF-2/3 | حزمة عقود Workflow | P3»؛ ويؤكده `methodology/PHASE_EXECUTION_STANDARD.md:20` (المرتبة 2، `Accepted`) الذي يدرج «**عقدا SLA-Policy/Templates (توثيق)**» ضمن قائمة إغلاق قرارات P3.
- **ما يثبته هذا:** سياسة SLA/التصعيد **محجوزة بصفوف فعلية قائمة** (لا بعبارة «لاحقاً» ولا بتوصية مستقبلية): تأجيل التنفيذ (`phases/designs/phase-3-workflows-approvals-actions.md:15` + `phases/BACKLOG_DEFERRED_SCOPE.md:23`) وملكية التوثيق (R5 + قائمة إغلاق P3). لذلك تُصنَّف بنود §12 غير المقنَّنة **`مؤجَّل بصف قائم`** لا `دلتا حقيقية`.
- **لا تعارض بين الصفوف:** `phases/designs/phase-3-workflows-approvals-actions.md:15` يؤجّل **التنفيذ** (مؤقتات وتصعيد متقدم)، و`methodology/PHASE_EXECUTION_STANDARD.md:20` يوجب **التوثيق** (عقدا SLA) ضمن إغلاق P3 — وثيقةٌ تسبق تنفيذاً، لا سلطتان متعارضتان. سُجّل الفحص هنا لأنه المرشّح الوحيد الذي كان يمكن أن يُقرأ تعارضاً.

<a id="absence-b2-rar005-001"></a>
### ABSENCE-B2-RAR005-001
- **البنود [02] و[03] و[04]:** التفويض بحسب **مهمة محددة** · بحسب **نوع Workflow** · بحسب **دور**.
- **السؤال:** هل يقنِّن المستودع نطاقاً للتفويض أدقّ من «علاقة محدودة المدة»؟
- **المصطلحات (EN):** `delegate scope` · `delegation scope` · `per-task delegation` · `delegate a role`. **(AR):** `تفويض لمهمة` · `تفويض لنوع` · `تفويض لدور` · `نطاق التفويض`.
- **الأمر (EN):** `grep -rInE 'delegate scope|delegation scope|per.task delegation|delegate a role' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'تفويض لمهمة|تفويض لنوع|تفويض لدور|نطاق التفويض' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 1**
- **لماذا لا يثبت الموجود البنود:** آلية التفويض المقنَّنة الوحيدة هي علاقة ReBAC: `phases/designs/phase-4-advanced-permissions-feature-management.md:12` (السطر كاملاً: «… · ReBAC: منح علاقات (owner/manager-of/**delegate بمدة**) · التصنيف الخماسي على screen/field/record مع إنفاذ في الاستعلام والواجهة والتصدير · …») و`:27` (FR-4.2: «علاقات مُعلنة بمنح **محدودة المدة والقنوات**، وتُلغى بانتهاء العلاقة»). محدِّدا النطاق المقنَّنان هما **المدة** و**القناة** — لا بندٌ بعينه ولا نوع workflow ولا دور. فالمطالب الثلاثة صالحة وغير مقنَّنة، **ولا صف قائم يحجزها** (فُحص `decisions/DEFERRED_IMPLEMENTATION.md` كاملاً — 26 سطراً — و`phases/BACKLOG_DEFERRED_SCOPE.md` كاملاً — 25 سطراً — فلا صف تفويض في أيٍّ منهما) ⇒ **دلتا حقيقية**.
- **مطابقة قريبة فُحصت واستُبعدت:**
  - `EXECUTION_REPORT.md:25` — **قريبة:** المطابقة العربية الوحيدة التي أرجعها الأمر: «… تُحيل إلى إصدارات specs سابقة — **خارج نطاق التفويض** (PHASE 5 = `docs/SPEC_SOURCE.md` فقط) …» (قُرئ السطر كاملاً). **مستبعَدة:** «التفويض» هنا **تكليف وكيل التنفيذ** في دفعة عمل، لا تفويض صلاحية داخل workflow. **لا تثبت البنود.**

<a id="absence-b2-rar005-002"></a>
### ABSENCE-B2-RAR005-002
- **البند [05]:** No further delegation — منع التفويض المتسلسل.
- **السؤال:** هل يقيّد المستودع قدرة المفوَّض إليه على إعادة التفويض؟
- **المصطلحات (EN):** `no further delegation` · `sub-delegation` · `chain of delegation`. **(AR):** `منع التفويض` · `تفويض متسلسل` · `لا تفويض إضافي`.
- **الأمر (EN):** `grep -rInE 'no further delegation|sub.delegation|chain of delegation' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'منع التفويض|تفويض متسلسل|لا تفويض إضافي' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** FR-4.2 يمنح علاقة محدودة المدة ولا يقول شيئاً عمّا إذا كان المفوَّض إليه يملك منحها بدوره. وأقرب مبدأ — `decisions/adr/ADR-0038-system-wide-administration-boundary.md:14` («**لا تصعيد ضمني:** لا يتحول الأدمن المنطاق إلى شامل بتراكم المنح المنطاقة مهما بلغ عددها») — يمنع **تراكم المنح الإدارية** لا **إعادة التفويض**؛ نطاقه الأدمن المنطاق مقابل الشامل، لا سلسلة تفويض بند workflow. فالقيد صالح وغير مقنَّن ولا صف قائم يحجزه ⇒ **دلتا حقيقية**.

<a id="absence-b2-rar005-003"></a>
### ABSENCE-B2-RAR005-003
- **البند [06]:** Delegation requiring approval — إخضاع التفويض نفسه لاعتماد.
- **السؤال:** هل يقنِّن المستودع اعتماداً مسبقاً لفعل التفويض؟
- **المصطلحات (EN):** `delegation approval` · `approve delegation` · `redelegat`. **(AR):** `اعتماد التفويض` · `إعادة التفويض` · `الموافقة على التفويض`.
- **الأمر (EN):** `grep -rInE 'no further delegation|sub.delegat|delegation approval|redelegat' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'تفويض متسلسل|إعادة التفويض|تفويض الفرعي|اعتماد التفويض' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** **الآلية** العامة قائمة ولا تُغني: `ui/UI_ACTION_BUTTON_MODEL.md:19` يجعل `approval_required` (‏none \| policy-ref \| hitl) **حقلاً إلزامياً** في عقد كل فعل محكوم، فأي فعل يمكن إخضاعه لاعتماد بالسياسة. لكن **لا فعل تفويض أصلاً**: كتالوج الأفعال المغلق (`ui/UI_FIELD_NAMING.md:43`) يضم `assign` و`grant` و`revoke` **ولا يضم `delegate`**، وقاعدة الملف نصاً «أي فعل جديد يُضاف بقرار في الـ Registry» و«**ممنوع** … مرادفات». فلا عقد يُعلَّق عليه الاعتماد ⇒ المطلب صالح وغير مقنَّن ⇒ **دلتا حقيقية**.
- **مطابقة قريبة فُحصت واستُبعدت:**
  - `decisions/open-decisions.md:61` — **قريبة:** «مصفوفات الاعتماد + SoD التفصيلية | 5 | سياسات في platform_db | لا | لا | مع P3/P4 كإعدادات | حسب المؤسسة | **قابلة للضبط من الأدمن**» (قُرئ السطر كاملاً). **مستبعَدة:** تصنّف **محتوى** مصفوفة الاعتماد إعداداً إدارياً (فئة 5)، ولا تُنشئ فعل تفويض ولا تحجزه بتأجيل. **لا تثبت البند** — لكنها تبيّن أن *أيّ* شرط اعتماد يصبح إعداداً بمجرد وجود الفعل.

<a id="absence-b2-rar005-004"></a>
### ABSENCE-B2-RAR005-004
- **البند [12]:** تعريف **Proxy decision: قرار بالنيابة**.
- **السؤال:** هل يعرف المستودع اتخاذ قرار اعتماد بالنيابة عن شخص آخر؟
- **المصطلحات (EN):** `proxy decision` · `decide on behalf` · `on-behalf-of decision`. **(AR):** `قرار بالنيابة` · `يقرر نيابة` · `اتخاذ القرار نيابة`.
- **الأمر (EN):** `grep -rInE 'proxy decision|decide on behalf|on.behalf.of decision' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'قرار بالنيابة|يقرر نيابة|اتخاذ القرار نيابة' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** سطح القرار الرسمي مقنَّن بثلاثة خيارات فقط (موافقة/رفض/إرجاع — `ui/UI_SCREEN_BEHAVIOR_CARDS.md:124`)، وصلاحية التوجيه محصورة نصاً بـ**المكلَّف الحالي** («لا أطراف سابقة ولا مراقبون» — `phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md:38`)، والقرار يُعطَّل على المقدِّم بـSoD (`ui/UI_SCREEN_BEHAVIOR_CARDS.md:126`). فلا سند لمفهوم «قرار بالنيابة» في المستودع ⇒ **مصطنع أو بلا أساس** بقاعدة `STATE` (وصفٌ بلا سند). *(حكمٌ على البند مقيساً بالمستودع الحاكم عند HEAD — لا نفيٌ لصلاحية المفهوم في أنظمة أخرى.)*
- **مطابقة قريبة فُحصت واستُبعدت:**
  - `ui/UI_FIELD_NAMING.md:32` — **قريبة:** سلسلة «فعل موصل كاتب» تحمل الحقل **`on_behalf_of`** ضمن حقولها الأساسية (قُرئ السطر كاملاً). **مستبعَدة:** الحقل يوثّق **تنفيذ** نداء موصل باسم مستخدم نهائي عبر حساب خدمة (FR-7.4: «سجل تفويض لكل مستخدم (مَن نُفِّذ باسمه) — لا فعل باسم مجهول»)، أي إسنادُ فعلٍ لا **اتخاذ قرار** بدلاً عن معتمِد. **لا تثبت البند.**

<a id="absence-b2-rar005-005"></a>
### ABSENCE-B2-RAR005-005
- **البند [13]:** تعريف **Acting role: تولي دور رسمي مؤقتاً**.
- **السؤال:** هل يعرف المستودع دوراً رسمياً يُتولّى مؤقتاً (بالوكالة)؟
- **المصطلحات (EN):** `acting role` · `interim role` · `temporary role`. **(AR):** `دور مؤقت` · `القائم بالأعمال` · `تولي دور` · `دور بالوكالة`.
- **الأمر (EN):** `grep -rInE 'acting role|interim role|temporary role' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'دور مؤقت|القائم بالأعمال|تولي دور|دور بالوكالة' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** الأدوار في المستودع تُسند وتُنزع بفعلين محكومين (`role.assign` بفحص SoD وحدث `ROLE_ASSIGNED` وفشلٍ `SOD_VIOLATION` — `ui/UI_ACTION_BUTTON_MODEL.md:74`) بلا أي بُعد زمني؛ والبُعد الزمني مقنَّن على **العلاقات** (ReBAC `delegate بمدة`) لا على **الأدوار**. فتعريف «الدور المؤقت» بلا سند ⇒ **مصطنع أو بلا أساس**.
- **مطابقة قريبة فُحصت واستُبعدت:**
  - `decisions/adr/ADR-0038-system-wide-administration-boundary.md:14` — **قريبة:** «**لا تصعيد ضمني:** لا يتحول الأدمن المنطاق إلى شامل بتراكم المنح المنطاقة مهما بلغ عددها. النوعان منحان متمايزان لا يلتقيان.» **مستبعَدة:** تنفي **الانتقال الضمني بين نوعَي منح إداري**، لا تُعرّف تولياً مؤقتاً لدور. **لا تثبت البند** — لكنها تؤكد أن اكتساب دورٍ لا يقع إلا بمنح صريح.

<a id="absence-b2-rar005-006"></a>
### ABSENCE-B2-RAR005-006
- **البند [14]:** تعريف **Queue claim: استلام عنصر من قائمة**.
- **السؤال:** هل يعرف المستودع «استلام» عنصر من قائمة مشتركة (نموذج سحب) بدل الإسناد المسبق (نموذج دفع)؟
- **المصطلحات (EN):** `queue claim` · `claim an item` · `self-assign` · `pull from queue`. **(AR):** `استلام من قائمة` · `سحب من القائمة` · `إسناد ذاتي`.
- **الأمر (EN):** `grep -rInE 'queue claim|claim an item|self.assign|pull from queue' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'استلام من قائمة|سحب من القائمة|إسناد ذاتي' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** نموذج الطوابير المقنَّن **دفعٌ لا سحب**: `queue.tasks` افتراضه فلتر «**مسندة إليّ** اليوم» (`ui/UI_SCREEN_BEHAVIOR_CARDS.md:96`) و`queue.approvals` بنوده «مرشّحة بأدوار المعتمِد + SoD» (`ui/UI_SCREEN_BEHAVIOR_CARDS.md:112`) — أي عرضٌ مرشَّح لبنودٍ **مسندة سلفاً**، لا بركة عناصر تُستلَم. ويؤكده أن كتالوج الأفعال المغلق (`ui/UI_FIELD_NAMING.md:43`) يضم `assign` **ولا يضم `claim`**، مع منع المرادفات نصاً. فالتعريف بلا سند ⇒ **مصطنع أو بلا أساس**.
- **مطابقات قريبة فُحصت واستُبعدت:**
  - `methodology/ROCKET_OPERATING_MODEL.md:22` — **قريبة:** «كل «Fixed/تم» من الأداة = **Claimed** حتى اجتياز البوابات بالأدلة». **مستبعَدة:** «Claimed» هنا **ادعاءٌ غير مُثبَت** في حوكمة أدوات التوليد، لا استلام عنصر عمل. **لا تثبت البند.**
  - `handoff/handoff.md:424` · `:436` — **قريبة:** «اسم الوسم claimed…». **مستبعَدة:** حجز اسم وسم Git. **لا تثبت البند.**

<a id="absence-b2-rar005-007"></a>
### ABSENCE-B2-RAR005-007
- **البند [16]:** Notify manager — إشعار المدير عند تجاوز الوقت.
- **السؤال:** هل يقنِّن المستودع إشعار المدير بوصفه فعل تصعيد؟
- **المصطلحات (EN):** `notify manager` · `manager notification` · `escalate to manager`. **(AR):** `إشعار المدير` · `إبلاغ المدير` · `تنبيه المدير`.
- **الأمر (EN):** `grep -rInE 'notify.*manager|manager notification|escalate.*manager' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'إشعار المدير|إبلاغ المدير|تنبيه المدير' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** المكوّنان قائمان منفصلين — علاقة `manager-of` ضمن ReBAC (`phases/designs/phase-4-advanced-permissions-feature-management.md:12`) ومحرّك إشعارات لأحداث النظام (`phases/designs/phase-3-workflows-approvals-actions.md:31` — FR-3.6: «أحداث النظام (تكليف/اعتماد/انتقال/استحقاق) تولّد إشعارات») — **ولا نص يربطهما بمحفّز زمني**. والحدث المقنَّن هو «استحقاق» لا «تجاوز استحقاق». يسكن الصف القائم (`absence-b2-rar005-000`) ⇒ **مؤجَّل بصف قائم**.

<a id="absence-b2-rar005-008"></a>
### ABSENCE-B2-RAR005-008
- **البند [17]:** Add alternate assignee — إضافة مكلَّف بديل.
- **السؤال:** هل يقنِّن المستودع إضافة مكلَّف بديل (بالإضافة إلى الأصلي) عند تجاوز الوقت؟
- **المصطلحات (EN):** `alternate assignee` · `substitute assignee` · `escalation path`. **(AR):** `مكلَّف بديل` · `مسؤول بديل` · `مسار بديل`.
- **الأمر (EN):** `grep -rInE 'alternate assignee|substitute assignee|trigger path|escalation path' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'مكلَّف بديل|مسؤول بديل|مسار تصعيد|مسار بديل' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** المقنَّن **نقلُ** التكليف لا **إضافةُ** مكلَّف ثانٍ: FR-3.12 (`phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md:19`) يجيز «إرجاع/إعادة إسناد البند إلى أي عضو مؤهل» — بديلٌ **يحلّ محلّ** الأصلي، ووجهةٌ واحدة (`returned_to`). ولا تعدد مكلَّفين متزامنين في أي نص. يسكن الصف القائم ⇒ **مؤجَّل بصف قائم**.

<a id="absence-b2-rar005-009"></a>
### ABSENCE-B2-RAR005-009
- **البند [20]:** Trigger path — مسار يُشغَّل بتجاوز الوقت.
- **السؤال:** هل يوجد محفّز زمني يفتح مساراً بديلاً في الـworkflow؟
- **المصطلحات (EN):** `time-based trigger` · `timer trigger` · `scheduled trigger` · `on timeout`. **(AR):** `محفّز زمني` · `مشغّل بالوقت` · `عند تجاوز الوقت` · `عند انقضاء`.
- **الأمر (EN):** `grep -rInE 'time.based trigger|timer trigger|scheduled trigger|on timeout' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'محفّز زمني|مشغّل بالوقت|عند تجاوز الوقت|عند انقضاء' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** المحفّزات المقنَّنة للانتقال **صلاحية + شرط + حالة صحيحة** (FR-3.3 — `phases/designs/phase-3-workflows-approvals-actions.md:28`)، والشروط معلنة «على قيم الحقول والنطاق» (`:12`) — لا بُعد زمني. والاستخدام الوحيد للـqueue زمنياً هو **تذكير** استحقاق (FR-3.8) لا فتح مسار. يسكن الصف القائم ⇒ **مؤجَّل بصف قائم**.

<a id="absence-b2-rar005-010"></a>
### ABSENCE-B2-RAR005-010
- **البنود [21] و[26] و[28]:** Pause بسبب Dependency · Pause/resume · Dependency waiting.
- **السؤال:** هل يقنِّن المستودع إيقاف/استئناف عدّاد المهلة أو انتظاراً على تبعية؟
- **المصطلحات (EN):** `SLA clock` · `clock pause` · `stop the clock` · `dependency wait`. **(AR):** `إيقاف المؤقت` · `تعليق المهلة` · `إيقاف العدّاد` · `انتظار تبعية`.
- **الأمر (EN):** `grep -rInE 'SLA clock|clock pause|stop the clock' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'إيقاف المؤقت|تعليق المهلة|إيقاف العدّاد' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البنود:** لا عدّاد مهلة أصلاً ليُوقَف (`absence-b2-rar005-000`). يسكن الصف القائم ⇒ **مؤجَّل بصف قائم**.
- **مطابقة قريبة فُحصت واستُبعدت:**
  - `ui/UI_RUN_EXECUTION_MODEL.md:21` — **قريبة:** الحالة `paused_awaiting_approval` («بوابة اعتماد/HITL فُتحت»). **مستبعَدة:** إيقافٌ للـ**تشغيل** بانتظار قرار بشري، لا إيقاف لعدّاد مهلة بسبب تبعية؛ ولا مهلة مرتبطة بها. **لا تثبت البنود.** *(المصدر `Proposed (v0.6)` — ملزم-معياري بإحالة `ui/UI_SCREEN_GOVERNANCE_STANDARD.md:10`؛ استُعمل مطابقةً قريبة لا إثباتاً.)*

<a id="absence-b2-rar005-011"></a>
### ABSENCE-B2-RAR005-011
- **البند [22]:** Escalate priority — رفع الأولوية.
- **السؤال:** هل يقنِّن المستودع رفع أولوية بندٍ بوصفه أثراً للتصعيد؟
- **المصطلحات (EN):** `raise priority` · `priority escalation` · `bump priority`. **(AR):** `رفع الأولوية` · `تصعيد الأولوية` · `زيادة الأولوية`.
- **الأمر (EN):** `grep -rInE 'raise priority|priority escalation|bump priority' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'رفع الأولوية|تصعيد الأولوية|زيادة الأولوية' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** المكوّنان قائمان ولا يلتقيان: **عمود الأولوية** في `queue.tasks` (`ui/UI_SCREEN_BEHAVIOR_CARDS.md:96`)، و**فعل تصعيد** مقنَّن بعقد كامل. لكن أثر فعل التصعيد معلَنٌ نصاً بأنه **رفع البند لمستوى أعلى بالمصفوفة** لا رفع أولويته. يسكن الصف القائم ⇒ **مؤجَّل بصف قائم**.
- **مطابقة قريبة فُحصت واستُبعدت:**
  - `ui/UI_ACTION_BUTTON_MODEL.md:89` — **قريبة:** عقد `approval.escalate` كاملاً (قُرئ السطر بتمامه): «approval.escalate | approvals.escalate (SoD: ≠ المقدِّم) | تعليق إلزامي | **typed** | **يرفع البند لمستوى أعلى بالمصفوفة** | api: approvals_escalate ⇦ POST /api/v1/approvals/{id}/escalate | APPROVAL_ESCALATED | high | لا». **مستبعَدة لسببين:** (١) أثره **مستوى الاعتماد** لا **الأولوية**؛ (٢) محفّزه **بشريٌّ يدوي** من سطح البند لا انقضاء مهلة. **لا تثبت البند** — لكنها تحدد بدقة أين ينتهي المقنَّن ويبدأ المؤجَّل: التصعيد **اليدوي** مقنَّن، و«التصعيد المتقدم» (المُشغَّل بالوقت) هو المؤجَّل بـ`phases/designs/phase-3-workflows-approvals-actions.md:15`.

<a id="absence-b2-rar005-012"></a>
### ABSENCE-B2-RAR005-012
- **البند [23]:** Open incident/task — فتح حادثة أو مهمة عند التصعيد.
- **السؤال:** هل يقنِّن المستودع توليد مهمة أو حادثة بمحفّز زمني؟
- **المصطلحات (EN):** `open incident` · `incident ticket` · `auto-create task`. **(AR):** `فتح حادثة` · `إنشاء مهمة تلقائياً` · `تذكرة`.
- **الأمر (EN):** `grep -rInE 'open incident|incident ticket|auto.create task' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'فتح حادثة|إنشاء مهمة تلقائياً|تذكرة' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** التوليد التلقائي مقنَّن بمحفّز **انتقالٍ** لا بمحفّز **زمن**: FR-3.8 (`phases/designs/phase-3-workflows-approvals-actions.md:33`) «Tasks: CRUD + تكليف + حالات + استحقاق + **توليد تلقائي من انتقال مُعلَّم** + تذكير استحقاق (queue)» (قُرئ السطر كاملاً). ولا كيان «حادثة» في المستودع إطلاقاً. يسكن الصف القائم ⇒ **مؤجَّل بصف قائم**.

<a id="absence-b2-rar005-013"></a>
### ABSENCE-B2-RAR005-013
- **البنود [24] و[25] و[27]:** Business calendar · Timezone · Holidays.
- **السؤال:** هل يقنِّن المستودع تقويم عمل أو منطقة زمنية أو عطلاً رسمية لحساب المهل؟
- **المصطلحات (EN):** `business calendar` · `working hours` · `holiday` · `timezone` · `time zone` · `TZ`. **(AR):** `تقويم عمل` · `أيام العطل` · `العطل الرسمية` · `المنطقة الزمنية` · `توقيت`.
- **الأمر (EN):** `grep -rInE 'business calendar|working hours|holiday|Holiday|timezone|time zone|TZ' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'تقويم عمل|أيام العطل|العطل الرسمية|المنطقة الزمنية|توقيت' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 8**
- **لماذا لا يثبت الموجود البنود:** المطابقات العربية الثماني كلها لكلمة **«توقيت»** بمعنى **زمن التحديث/فئة التوقيت** لا المنطقة الزمنية — مثل `decisions/open-decisions.md:6` («تصنيف كل قرار إلى **فئة توقيت** واضحة…») و`methodology/Spec_Driven_Modular_Monolith_Methodology.md:142` («كل ملف من §5 له مالك و**توقيت** تحديث…»). فصفرٌ فعليٌّ للمفهوم في اللغتين. يسكن الصف القائم ⇒ **مؤجَّل بصف قائم**.

<a id="absence-b2-rar005-014"></a>
### ABSENCE-B2-RAR005-014
- **البند [29]:** Retry limits — حدود إعادة المحاولة ضمن سياسة المهلة.
- **السؤال:** هل يقنِّن المستودع سقفاً لإعادة المحاولة في سياق SLA؟
- **المصطلحات (EN):** `retry limit` · `max retries` · `retry_limit` · `backoff`. **(AR):** `حد المحاولات` · `عدد المحاولات` · `سقف الإعادة`.
- **الأمر (EN):** `grep -rInE 'retry limit|max retries|retry_limit|backoff' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 2**
- **الأمر (AR):** `grep -rInE 'حد المحاولات|عدد المحاولات|سقف الإعادة' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند:** المطابقتان الإنجليزيتان في `architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md:109` و`:112` — و`backoff` فيهما **سلوك اتصال بمزوّد نماذج** عند فشل الاكتشاف أو بلوغ حدّ المعدل (يتبعه fallback)، لا سقف إعادة محاولة لبند workflow متجاوز المهلة. يسكن الصف القائم ⇒ **مؤجَّل بصف قائم**.

<a id="absence-b2-rar005-015"></a>
### ABSENCE-B2-RAR005-015
- **البندان [30] و[31]:** Who can change SLA · Audit of manual override.
- **السؤال:** هل يقنِّن المستودع مالكَ تغيير سياسة SLA وتدقيقَ تجاوزها اليدوي؟
- **المصطلحات (EN):** `who can change` · `manual override` · `override audit`. **(AR):** `من يغيّر` · `تعديل يدوي` · `تجاوز يدوي مدقَّق`.
- **الأمر (EN):** `grep -rInE 'who can change|manual override|override audit' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'من يغيّر|تعديل يدوي|تجاوز يدوي مدقَّق' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البندين:** القيد العام قائم وسيسري لاحقاً — م3 (`constitution.md:11`) تُلزم بتدقيق **append-only** لكل عملية مهمة «(قراءة حرجة/إنشاء/تعديل/حذف/تصدير/اعتماد/**تغيير إعداد** أو علم أو نموذج أو profile)» (قُرئ السطر كاملاً) — لكنه لا يسمّي مالك سياسة SLA ولا يعرّف «التجاوز اليدوي» بوصفه عملية. ولا سياسة SLA قائمة أصلاً ليكون لها مالك (`absence-b2-rar005-000`). يسكنان الصف القائم ⇒ **مؤجَّل بصف قائم**.

<a id="absence-b2-rar005-016"></a>
### ABSENCE-B2-RAR005-016
- **البند [33]:** Reopen بصلاحية عالية وسبب إلزامي.
- **السؤال:** هل تبنّى المستودع إعادة فتح بندٍ محسوم؟
- **المصطلحات (EN):** `reopen` · `re-open a decision` · `revert a decision`. **(AR):** `إعادة فتح بند` · `إعادة فتح قرار` · `نقض قرار`.
- **الأمر (EN):** `grep -rInE 'reopen|re.open a decision|revert a decision' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **الأمر (AR):** `grep -rInE 'إعادة فتح بند|إعادة فتح قرار|نقض قرار' . --include='*.md' | grep -viE '<المستثنى>'` — **النتيجة: 0**
- **لماذا لا يثبت الموجود البند — ولماذا هو بلا أساس لا مؤجَّل:** المستودع **تبنّى الخيار المقابل** صراحةً (البند [32]): OD-WF-1 يقفل أن «**الرفض يُنهي البند نهائياً**» (`phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md:37`)؛ وعقد `workflow.approve` يعلن `rollback = لا` (`ui/UI_ACTION_BUTTON_MODEL.md:66`) وكذلك `approval.escalate` (`:89`)؛ وكتالوج الأفعال المغلق (`ui/UI_FIELD_NAMING.md:43`) **لا يضم `reopen`** ويمنع المرادفات. ولا صف تأجيل لإعادة الفتح في `decisions/DEFERRED_IMPLEMENTATION.md` ولا في `phases/BACKLOG_DEFERRED_SCOPE.md` (فُحصا كاملين). فبقاعدة `SUG` — «لم يُتبنَّ ⇒ مصطنع أو بلا أساس» ⇒ **مصطنع أو بلا أساس**. *(حكمٌ على البند مقيساً بالمستودع عند HEAD؛ تبنّيه لاحقاً يحتاج قرار مالك يضيف الفعل إلى الكتالوج ويفتح OD-WF-1.)*

---

**Related:** `RECONCILIATION-RAR-005.md` · `CANONICAL-ITEM-UNIVERSE.md` (`188ad37`) · `NORMALIZATION-AND-ATOMIC-MAP.md` (`188ad37`) · `phases/BACKLOG_DEFERRED_SCOPE.md` · `methodology/RECONCILIATION_ROADMAP.md` · `methodology/PHASE_EXECUTION_STANDARD.md`
