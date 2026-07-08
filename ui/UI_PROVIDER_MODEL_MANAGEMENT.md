# UI_PROVIDER_MODEL_MANAGEMENT.md — إدارة المزوّدات والنماذج (الخيار A — متوافق مع D9)

> **Version:** 1.0 — Proposed (v0.6) · **Date:** 2026-07-08 · **الموضع الهدف:** `ui/UI_PROVIDER_MODEL_MANAGEMENT.md`
> **مبنيّ فوق (لا يستبدل):** تصاميم P5 (capabilities/بوابة الأوزان) وP6 (agents/Gateway/fallback) · v0.4 (ACTION_BUTTON §6.b · ADMIN_CONSOLE مجموعة F · DESIGN_SYSTEM شارات · FIELD_NAMING) · v0.5 (INTERACTION/VISIBILITY/STATES) · مراجعة الأنماط الخارجية §8–§9.
> **قرارات المالك المقفلة (2026-07-08):** الخيار **A حصراً** — D9 يبقى كما هو: **لا Base URL حقيقي، لا API Key، لا أسرار، لا endpoints حقيقية داخل الواجهة إطلاقاً**؛ أي تعديل فعلي للمزوّد يتم عبر Ops/config/secret_ref خارج الواجهة. الأفعال المضافة للكتالوج: run · escalate · compare (لا غيرها).
> **Tool-Agnostic:** أي ذكر لأداة توليد تصميم يخضع لقاعدة §1.8 في `UI_STITCH_REFINED_PROMPTS.md`.

## §1 التموضع والنطاق
هذه المواصفة **توسّع شاشة `admin.capabilities` القائمة** (لا شاشة جديدة — لا Δ على الجرد لهذا الملف) إلى سطح Control-Plane بأربعة تبويبات: **Providers (قراءة) · Models · Routing · Profiles**، مع إحالة إلى `admin.agents` من رأس تبويب Routing. الجمهور: أدمن النماذج فقط. الغرض: رؤية تشغيلية كاملة وحوكمة ربط/توجيه/ملفات-تعريف — **دون أي مسار كتابة نحو config**.

## §2 قيود D9 (قائمة منع صلبة — تسبق كل ما بعدها)
| لا يُعرض أبداً | لا يُحرَّر أبداً من الواجهة | أين يُدار |
|---|---|---|
| Base URL / hosts / ports الفعلية | تعريف مزوّد أو حذفه | config بيد Ops |
| قيم الأسرار / المفاتيح / tokens | secret_ref (القيمة أو الوجهة) | مخزن أسرار خارجي + config |
| مسارات ملفات الأوزان | تحميل/جلب نماذج من الخارج | عملية توريد Ops + **بوابة ترخيص الأوزان** |
| GPU / replicas / lifecycle حاويات | أي معامل نشر | بروفايلات النشر (P8) |
**قاعدة مصدر الحقيقة:** config هو المرجع؛ الواجهة **مرآة قراءة + طلبات تغيير** (§8). (مسوّغ عملي موثَّق من مراجعة الأنماط: نمط حفظ عناوين الاتصال من الواجهة إلى قاعدة البيانات لدى Open WebUI قد يقفل الواجهة عند عنوان خاطئ ويستلزم إجراء استرداد — وهو ما يتجنبه بقاء config مصدراً وحيداً.)

## §3 تبويب 1 — Providers (قراءة)
بطاقة لكل مزوّد معلن في config. **حقول البطاقة (القائمة المقفلة من المالك — لا إضافات):**
| الحقل | العرض | ملاحظات |
|---|---|---|
| provider alias | مثل ollama-local (LTR mono) | معرّف عرضي؛ ليس عنواناً |
| provider type | ollama \| openai-compatible \| vllm \| custom | من config |
| secret_ref | **الاسم فقط** + أيقونة قفل | لا قيمة، لا وجهة |
| connection status | chip: connected / disconnected / degraded | من إشارات الصحة الخادمية |
| last health check | طابع زمني | — |
| model counts | مكتشفة N · معتمدة M · **قابلة للاستخدام K** | K = المكتشفة ∩ المعتمدة ترخيصياً (§4) |
| test connection | زر ⇒ **نتيجة chip نجاح/فشل فقط** | action: provider.test_connection (قائم) · audit: PROVIDER_TESTED · بلا أي تفاصيل شبكية في النتيجة |
| request provider change | زر ⇒ workflow §8 | الحالة «طلب معلّق #» تظهر على البطاقة |
**التفاعل:** نقر البطاقة ⇒ **drawer end** «تفاصيل المزوّد» (نفس الحقول موسّعة + تاريخ فحوصات مختصر + طلبات التغيير المرتبطة) — **بلا أي حقل حساس حتى داخل الـ drawer**.
**الحالات:** default · loading (skeleton بطاقات) · **empty**: «لا مزوّدات معلنة — تُعرَّف عبر config» + زر «طلب تهيئة مزوّد» (§8) · error (فشل قراءة الحالة) · disabled (Safe Mode: زر الاختبار والطلب معطَّلان بسبب) · audit-visible (drawer «تاريخ التغييرات» للمخوّل).

## §4 تبويب 2 — Models
جدول نماذج (≤7 أعمدة ظاهرة؛ الباقي column picker):
| العمود | القيم |
|---|---|
| model_ref | LTR mono |
| provider alias | — |
| اكتشاف | discovered_at (اكتشاف **خادمي محلي فقط** من المزوّد الداخلي — action: **discovery.run** بالفعل المعتمد run · audit: MODEL_DISCOVERY_REFRESHED) |
| **الترخيص** | approved / pending / rejected — من بوابة أوزان P5؛ **rejected/pending ⇒ غير قابل للاستخدام مهما اكتُشف** |
| قابل للاستخدام | ✔ فقط عند (مكتشف ∧ معتمد) |
| حالة التحميل | warm / cold |
| نافذة السياق · وسوم القدرة | قراءة |
**مفردات حالات النموذج (chips جديدة — تنضم لتصنيف الشارات في نظام التصميم):**
| الحالة | اللون (برموز النظام) | مصدر الإشارة | رسالة i18n نمط |
|---|---|---|---|
| connected | success | فحص صحة المزوّد + استجابة النموذج | — |
| disconnected | danger | فشل الفحص | errors.MODEL_DISCONNECTED |
| slow | warning | تجاوز عتبة زمن من config (OD-MX-4) | errors.MODEL_SLOW |
| loading (تسخين) | info نابض | cold→warm جارٍ | errors.MODEL_WARMING |
| context-error | برتقالي (classification.l4 **لا** — يُستخدم semantic warning-strong منفصل) | الطلب > نافذة السياق (خريطة أخطاء الـ Gateway) | errors.MODEL_CONTEXT_EXCEEDED |
| permission-restricted | رمادي + قفل | النموذج خارج Profiles المسموحة لدور الناظر | errors.MODEL_RESTRICTED |
> ملاحظة تنفيذية للشارات: معرَّفة كعائلة سادسة في §5 من UI_DESIGN_SYSTEM (Δ ما-بعد الدمج)؛ **ممنوع** استعمال ألوان التصنيف الخمسة المحجوزة لها.
**أفعال هذا التبويب:** discovery.run (admin.models.manage · simple · MODEL_DISCOVERY_REFRESHED) فقط. **لا زر تنزيل/سحب نماذج** (بيئة مغلقة — نمط «التنزيل من المحدد» لدى المراجع الخارجية **مرفوض** هنا؛ التوريد عبر Ops + بوابة الترخيص). التفريغ/التسخين اليدوي (نمط Eject) ⇒ **OD-MX-3** (افتراضياً قراءة فقط).

## §5 تبويب 3 — Routing (المصفوفة الموحّدة capability×agent → model)
| الصف (من التصاميم المعتمدة) | الأعمدة |
|---|---|
| قدرات P5: embedding · reranker · ocr · asr · vision-caption | النموذج الأساسي (model_ref) · **سلسلة fallback مرتّبة** · معاملات ضمن حدود config (سياق/رموز قصوى/مهلة/إعادة) · شارة **«يتطلب اعتماداً في الإنتاج»** · آخر تعديل (مَن/متى) |
| وكلاء P6: chat/reasoning · report · sql-agent · validation | كما فوق |
**تدفق التعديل:** تغيير خلية ⇒ drawer end «أثر التغيير» (لتغيير embedding: **خطة إعادة الفهرسة** من P5 إلزامية القراءة) ⇒ تأكيد **typed** ⇒ اعتماد في الإنتاج حسب السياسة — العقود القائمة: capability.binding_change / agent.binding_change (v0.4 §6.b) **بلا أفعال جديدة**.
**نزاهة نطاق:** لا صف «coding» — وكيل برمجة خارج نطاق المسار الأول (Backlog بقرار مستقل).
رأس التبويب يحمل رابط «التفصيل لكل وكيل ⇒ admin.agents» (لا ازدواج محتوى).

## §6 تبويب 4 — Profiles (طبقة الاختيار المنسّقة)
**التعريف:** Model Profile = تغليف مُدار = { ربط (agent/capability) + معاملات مسبقة + نطاق معرفة افتراضي + أدوار مسموحة + label ar/en + وصف }. **المستخدم لا يرى أسماء نماذج خام أبداً — يرى Profiles فقط.**
**الحوكمة:** كائن تعريف يتبع دورة الحياة الموحّدة Draft→Validated→Approved→Active→RolledBack (نمط §3.2 من نموذج الـ Console) — المحرر **drawer end** مضغوط (≤7 حقول، v0.5) بشريط دورة الحياة؛ الاعتماد عبر بند قياسي.
| الحقل | النمط |
|---|---|
| profile_key | snake_case فريد (default · fast · precise …) — قيمة بيانات لا معرّف نظام |
| label_ar/label_en · الوصف | i18n |
| binding_ref + معاملات | ضمن حدود config |
| default_scope_ref | يضبط ws.scope_selector مبدئياً عند التفعيل |
| allowed_roles | قائمة أدوار |
**سطح المستخدم:** مكوّن `ws.model_profile_selector` بجوار محدد النطاق — **مخفي افتراضياً للمستخدم العادي** (يعمل بالافتراضي بصمت)، ويُفعَّل لأدوار محددة بسياسة (**OD-MX-1**). سياسة المشروع (تُفصَّل في Δ المشاريع لاحقاً): default profile + قائمة مسموحة على مستوى المشروع.
**السقوط:** مزوّد Profile ساقط ⇒ الخيار disabled-with-reason في المحدد + سقوط تلقائي إلى Default Profile مع شارة «نموذج بديل» (آلية P6 القائمة) — banner.model_down يبقى الحاكم الكلي.
**التدقيق:** MODEL_PROFILE_DEFINED / CHANGED / ACTIVATED / ROLLED_BACK؛ **وتعديل حمولة**: إضافة `model_ref + profile_key` إلى CHAT_ANSWER_SERVED وإلى كل فعل منفَّذ بمساعدة نموذج بمستوى خطورة ≥ medium (يُثبَّت في كتالوج التدقيق عند التفعيل).

## §7 الصلاحيات
| الصلاحية | تخوّل |
|---|---|
| admin.models.view | قراءة التبويبات الأربعة |
| admin.models.manage | test_connection · discovery.run · تعديل Routing · تعريف Profiles |
| (سياسة الإنتاج) | اعتماد تغييرات الربط approval-in-prod |
| ops (دور) | صف اعتماد طلبات تغيير المزوّد (§8) وتنفيذها خارجياً |
| audit.view (بنطاق) | drawers التاريخ والسلاسل |
عناصر خارج الصلاحية: **HIDDEN-SERVER**؛ Safe Mode: كل أفعال التبويبات disabled-with-reason موحّد.

## §8 Workflow «طلب تهيئة/تعديل مزوّد» (بديل الإدخال المباشر — قلب الخيار A)
**النمذجة:** تعريف workflow مسبق `wf.provider_change`؛ زر الطلب = **workflow.submit** القائم (لا فعل جديد). 
**حقول نموذج الطلب (تصريحية فقط — يُمنع جمع أي URL/سر):** الهدف (مزوّد قائم بالـ alias / «جديد») · النوع المطلوب · القدرات المطلوبة (اختيار من كتالوج القدرات) · الغرض/المسوّغ · الأولوية. 
**المسار:** submit ⇒ بند في صف Ops (queue.approvals بجمهور ops) ⇒ قرار ⇒ **التنفيذ الفعلي خارج المنصة** (config + secret_ref عبر القناة الآمنة) ⇒ Ops يقفل البند بمرجع تنفيذ ⇒ بطاقة المزوّد تعكس الحالة الجديدة تلقائياً من config/health.
**الحالة على البطاقة:** «طلب معلّق #» → «نُفِّذ #» / «رُفض (سبب عام)». 
**التدقيق:** PROVIDER_CHANGE_REQUESTED (عند submit، بحمولة الحقول التصريحية) · INSTANCE_TRANSITIONED (قرارات المسار) · PROVIDER_CONFIG_APPLIED_BY_OPS (إقفال Ops بمرجع — الاسم الكنسي الموحّد مع مواصفة v0.7). 
**SoD:** مقدِّم الطلب ≠ معتمِده؛ ومنفّذ Ops يوثَّق بالمرجع.

## §9 خريطة التفاعل والظهور (التزام v0.5)
تبويب واحد نشط · تفاصيل المزوّد/الخطوات = drawer end · تعديل Routing = drawer أثر + modal typed · محرر Profile = drawer end بدورة حياة · **لا modal فوق modal** · L0 لكل تبويب = عدّادات + chips فقط، والتفصيل عند الطلب (حدود 3/5/7 سارية) · وسوم الظهور: admin-only (الشاشة) · by-permission (الأفعال) · safe-mode-gated (التحرير) · audit-visible (التواريخ/السلاسل) · state-gated (اعتماد قبل تفعيل Profile).

## §10 جدول أحداث التدقيق (المستعمل هنا)
**قائم:** PROVIDER_TESTED · CAPABILITY_BINDING_CHANGED · AGENT_BINDING_CHANGED · INSTANCE_TRANSITIONED. 
**جديد بهذه الحزمة:** MODEL_DISCOVERY_REFRESHED · MODEL_PROFILE_DEFINED/CHANGED/ACTIVATED/ROLLED_BACK · PROVIDER_CHANGE_REQUESTED · PROVIDER_CONFIG_APPLIED_BY_OPS. 
**تعديل حمولة:** (§6) model_ref/profile_key على CHAT_ANSWER_SERVED والأفعال ≥ medium.

## §11 توجيه أداة توليد التصميم (لتحديث G10 لاحقاً — إشارة فقط هنا)
**يجب أن يظهر:** التبويبات الأربعة · بطاقة مزوّد بحقول §3 المقفلة حرفياً · جدول نماذج فيه chips الحالات الست (بينها context-error وpermission-restricted) وعمود الترخيص · مصفوفة Routing بشارة اعتماد-الإنتاج ودrawer خطة إعادة الفهرسة · محرر Profile بدورة الحياة · نموذج طلب التغيير التصريحي · حالة empty «لا مزوّدات معلنة». 
**يجب ألا يظهر أبداً:** URL/مفاتيح/منافذ · أزرار تنزيل نماذج · GPU/lifecycle · شعارات مزوّدين حقيقيين · terminal.

## §12 قرارات مفتوحة
| OD | الموضوع | التوصية |
|---|---|---|
| OD-MX-1 | إظهار ws.model_profile_selector للمستخدم العادي | **مخفي افتراضياً**؛ تفعيل بأدوار عبر سياسة |
| OD-MX-3 | تحكم يدوي warm/unload للنماذج | قراءة فقط في v1؛ أي تفعيل لاحق بقرار Ops-gated |
| OD-MX-4 | عتبة slow ومصدرها | مفتاح config خادمي (يُسمّى في مواصفة config عند التفعيل) — الواجهة تستهلك الإشارة فقط |
