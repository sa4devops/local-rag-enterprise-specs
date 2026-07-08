# PROVIDER_MODEL_SECRET_CONFIG_SPEC.md — مواصفة المزوّدات والنماذج والأسرار (Backend/Config)

> **Version:** 1.0 — Proposed (v0.7) · **Date:** 2026-07-08 · **الموضع الهدف:** `architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md`
> **المراجع الحاكمة:** D9/ADR-0008 (حدود الواجهة) · D1/D2 (الستاك) · Phase-5 (القدرات + بوابة ترخيص الأوزان) · Phase-6 (Gateway/fallback/الوكلاء) · v0.6: `ui/UI_PROVIDER_MODEL_MANAGEMENT.md` + `ui/UI_RUN_EXECUTION_MODEL.md` (الخيار A المقفل 2026-07-08) · constitution (fail-closed · correlation · config profiles).
> **الطبيعة:** مواصفة مفاهيمية **بلا كود** — تعرّف العقد بين Config/Ops والـ Backend والواجهة كي لا يبدأ أي Coding Agent باستنتاجات ناقصة حول الأسرار والمزوّدات.

## §1 الغرض (Purpose)
1. v0.6 عرّفت **سطح الواجهة** لإدارة المزوّدات (قراءة + طلب تغيير) وفق الخيار A؛ هذا الملف يعرّف **الطرف الخلفي المقابل**: من أين تأتي الأسرار وendpoints، ومن يحلّها، وكيف تُختبر وتُكتشف النماذج وتُوجَّه وتُدقَّق — دون أن يلمس أيٌّ من ذلك الواجهة.
2. يمنع ثلاث ثغرات تنفيذ متوقعة: (أ) إضافة حقول أسرار/URL في UI «لتسهيل الإعداد»؛ (ب) قراءات env متناثرة بلا نموذج موحّد؛ (ج) fallback صامت بلا أثر تدقيق.
3. أي تعارض بين هذا الملف وملفات UI v0.6 يُحسم لصالح **حدود D9** أولاً ثم هذا الملف (تفصيل backend) ثم ملفات UI (تفصيل عرض).

## §2 حدود D9 (D9 Boundary) — قائمة قطعية
| ممنوع وصوله إلى الواجهة (بأي DTO/رد API للواجهة) | ما تستقبله الواجهة بدلاً منه |
|---|---|
| قيم الأسرار / API Keys / tokens / كلمات مرور | **secret_ref بالاسم فقط** (معرّف غير حساس) |
| Base URL الحقيقي / hosts / ports / مسارات | provider_alias + provider_type (+ endpoint_ref بالاسم إن سمح OD-PSC-2) |
| ترويسات Authorization أو ما يعادلها | لا شيء — لا تُسلسل إطلاقاً |
| مسارات ملفات الأوزان / إعدادات GPU/replicas | حالة/عدّادات فقط |
| أخطاء خام تكشف عناوين أو أسراراً | error_code + رسالة عامة + request_id |
**قاعدة إنفاذ خادمية:** كل DTO موجَّه للواجهة يمرّ بمُسلسِل **قائمة سماح** (whitelist) صريحة الحقول؛ الحقول المحظورة أعلاه ليست «تُخفى» بل **لا تُعرَّف في المخطط أصلاً** (HIDDEN-SERVER بنيوي — يطابق قاعدة v0.5/v0.6). الواجهة لا تُنشئ عملاء مزوّدين ولا تحمل بيانات اتصال — كل الاختبار/الاكتشاف عبر أفعال backend تعيد نتائج معقّمة.

## §3 نموذج تهيئة المزوّد (Provider Configuration Model)
مصدر الحقيقة: **config المُدار من Ops** (بروفايلات P8)؛ الـ backend يقرأه ويشتق منه كتالوجاً تشغيلياً؛ `admin.config_profiles` تبقى قراءة-فقط مع قناع وفق OD-PSC-2.
| الحقل | النوع/القيم | مَن يضبطه | يظهر في UI؟ | ملاحظات |
|---|---|---|---|---|
| provider_id | مفتاح snake_case ثابت | Ops (config) | لا (داخلي) | لا يُعاد استخدامه بعد الحذف |
| provider_alias | نص عرضي (i18n-قابل) | Ops | **نعم** | هوية العرض في بطاقة v0.6 §3 |
| provider_type | ollama \| openai_compatible \| custom_internal | Ops | **نعم** | يحدد عائلة السلوك (§5) |
| provider_family | وصف المحرك (ollama/vllm/tgi/custom…) | Ops | لا (تشغيلي) | يضبط دلالات المهلات/warm |
| config_source | env \| file \| encrypted_config \| vault(مستقبلاً) | Ops | لا | مصدر حلّ secret_ref/endpoint_ref |
| secret_ref | اسم مرجع | Ops | **الاسم فقط** | §4 |
| endpoint_ref | اسم مدخل عنوان | Ops | حسب OD-PSC-2 (افتراضياً: لا) | الحلّ خادمي حصراً |
| capabilities | قائمة معلنة (embedding/rerank/ocr/asr/vision_caption/chat…) | Ops | نعم (وسوم) | تُقارن بالمكتشف (§6.5) |
| enabled | true/false (config) | Ops | نعم (كحالة) | مستقل عن التوافر اللحظي |
| environment_scope | dev \| staging \| prod (قائمة) | Ops | لا | المزوّد خارج نطاق البيئة = غير موجود لها |
| health_state | healthy \| degraded \| unreachable \| misconfigured \| disabled | Backend (مشتق) | **نعم (chip)** | §6.7 |
| last_checked_at | طابع زمني | Backend | **نعم** | — |
| model_discovery_policy | auto \| manual_allowlist \| disabled (+TTL مرجع OD-PSC-3) | Ops | لا (أثره يظهر كعدّادات) | §9 |
**إعادة التحميل:** الـ backend يلتقط تغيّر إصدار config (نشر Ops) ويعيد بناء الكتالوج ويصدر `PROVIDER_CONFIG_APPLIED_BY_OPS` بحمولة (provider_id? أو all، config_version-hash) — **بلا قيم**.

## §4 نموذج مرجع السر (Secret Reference Model)
1. **secret_ref ليس السر** — اسمٌ يشير إلى قيمة يديرها Ops داخل `config_source`.
2. **المصادر المدعومة:** متغير بيئة · ملف سر محلي (صلاحيات مقيّدة، mounted) · config مُعمّى (مفتاح فكّه عبر env) · **مستقبلاً**: مدير أسرار/Vault عبر مهايئ محجوز الواجهة (OD-PSC-1 يحدد باكورة التنفيذ).
3. **الحلّ (resolution):** عند بناء عميل المزوّد؛ القيمة تعيش **في الذاكرة فقط** مع صلاحية قصيرة، وتُبطل عند تغيّر إصدار config. **لا تُخزَّن في قاعدة البيانات إطلاقاً.**
4. **قواعد قطعية:** لا تُعرض القيم في UI · لا تُكتب في السجلات (§12) · لا تُرسل إلى الواجهة بأي شكل · لا تظهر في رسائل الأخطاء · لا تدخل حمولات التدقيق (§11).
5. **الفشل:** secret_ref غير قابل للحل ⇒ المزوّد `misconfigured` **معزولاً** (بقية المزوّدين يعملون)، fail-closed لأي توجيه نحوه، وحدث تغيّر حالة (§11) — الواجهة ترى chip عام «غير متصل — خطأ تهيئة» بلا تفاصيل.
6. **التدوير (rotation):** Ops يبدّل القيمة في المصدر ⇒ نشر/إشارة ⇒ إعادة حلّ ⇒ فحص صحة يؤكد ⇒ الحدث الاعتيادي؛ لا مسار تدوير من الواجهة.

## §5 أنواع المزوّدين (Provider Types)
| النوع | المصادقة | الاكتشاف الافتراضي | حالات مميزة | ملاحظات |
|---|---|---|---|---|
| **Ollama (محلي)** | عادةً بلا سر (endpoint_ref داخلي فقط) | auto (واجهة النماذج المحلية) | needs_loading (cold→warm) ذات معنى | البيئة مغلقة: **لا سحب نماذج من الخارج** — التوريد Ops + بوابة الترخيص |
| **OpenAI-compatible (داخلي)** | secret_ref ⇒ ترويسة مصادقة تُبنى خادمياً | auto إن توفرت قائمة نماذج، وإلا manual_allowlist | rate-limit/context_error واردة | «متوافق» يعني الشكل لا الخدمة السحابية — **لا اتصال خارج الشبكة المغلقة** |
| **Custom internal** | حسب العقد (secret_ref اختياري) | غالباً disabled/manual | حسب المهايئ | مهايئ لكل عائلة يلتزم نفس الواجهات الداخلية (test/discover/invoke) |
كل الأنواع تلتزم: نفس نموذج الحقول (§3)، نفس مسار الحل (§4)، نفس أحداث التدقيق (§11)، ونفس التعقيم نحو الواجهة (§2).

## §6 مسؤوليات الـ Backend
1. **حلّ secret_ref/endpoint_ref** (§4) وبناء العملاء — حصرياً هنا.
2. **اختبار الاتصال:** فحص خادمي يعيد للواجهة {status: ok/fail، latency_class، checked_at} فقط — **لا صدى للعنوان ولا لنص الخطأ الخام**؛ التفصيل التقني إلى سجلات Ops المقنّعة.
3. **اكتشاف النماذج** وفق سياسة المزوّد (§9) — **محلي فقط**، لا فهارس خارجية.
4. **تخزين ميتاداتا المكتشف** في كتالوج DB: model_ref، context_window، وسوم القدرة، discovered_at — **القابل للاستخدام = المكتشف ∩ المعتمد ترخيصياً** (بوابة أوزان P5) دائماً.
5. **مطابقة القدرات:** المعلن (§3.capabilities) مقابل المكتشف؛ عدم تطابق ⇒ health=degraded + تدقيق.
6. **الصحة:** مجدول فحوص + فحص عند الطلب؛ **التدقيق عند تغيّر الحالة أو الفحص اليدوي فقط** (لا ضجيج لكل نبضة).
7. **إنفاذ التوافر:** الموجّه يرفض التوجيه إلى disabled/unreachable/misconfigured؛ إشارات التدهور تصل ws (الوضع الحتمي) وruns (توقف خطوات الوكلاء المعلَّل — v0.6).
8. **تطبيق سياسة التوجيه:** مصفوفة capability×agent (registry) ⊕ سياسة المشروع ⊕ Model Profile للمستخدم — ترتيب الحسم في §10.
9. **إنفاذ fallback:** سلسلة مرتبة لكل ربط؛ التقدم فيها يصدر `MODEL_FALLBACK_USED` **مرة لكل طلب** بسبب مُعدَّد.
10. **تعقيم السجلات** (§12) و**تدقيق العمليات الحساسة** (§11) و**DTOs معقّمة** للواجهة (§2).

## §7 مسؤوليات الواجهة (UI) — قائمة مقفلة (تطابق v0.6/الخيار A)
تعرض فقط: provider_alias · provider_type · حالة الاتصال/الصحة + last_checked_at · **secret_ref بالاسم** · عدّادات النماذج (مكتشفة/معتمدة/قابلة) · نتيجة اختبار الاتصال (chip) · Model Profiles (طبقة الاختيار المنسّقة) · ملخص مصفوفة التوجيه · **workflow «طلب تهيئة/تعديل مزوّد»**. ولا تملك أي مسار كتابة نحو config أو الأسرار — التحرير الوحيد لديها: عناصر الحوكمة (الربط/الملفات-التعريفية) عبر عقود الأفعال القائمة.

## §8 مسؤوليات التشغيل (Ops)
الأسرار الفعلية وقيم endpoints · **التدوير** (§4.6) · نشر config لكل بيئة (environment_scope) · إقفال بنود `wf.provider_change` بمرجع تنفيذ (⇒ `PROVIDER_CONFIG_APPLIED_BY_OPS`) · **التعافي عند كسر تهيئة مزوّد**: الإصلاح في المصدر (config/secret) حصراً — **لا مسار تجاوز من UI أو DB بالتصميم** (يمنع سيناريو «عنوانٌ محفوظ يقفل الواجهة») · توثيق runbook لكل نوع مزوّد ضمن وثائق P8.

## §9 اكتشاف النماذج (Model Discovery)
- **القابل للاكتشاف:** auto ⇒ استعلام دوري/يدوي لواجهة المزوّد المحلية؛ **غير القابل:** manual_allowlist ⇒ قائمة model IDs بميتاداتا معلنة في config؛ disabled ⇒ لا كتالوج لهذا المزوّد.
- **التخزين المؤقت:** TTL من config (OD-PSC-3) + **تحديث يدوي دائم** عبر الفعل القائم `discovery.run`.
- **زوج أحداث موحَّد:** `PROVIDER_DISCOVERY_RUN` (بدء العملية: الفاعل، provider_id، الوضع auto/manual) ثم `MODEL_DISCOVERY_REFRESHED` (الاكتمال: فروق العدّادات، المدة، status) — الأول «تشغيل» والثاني «نتيجة»؛ لا ازدواج تسمية.
- **حالات النموذج التشغيلية (enum خادمي — تطابق chips v0.6 واحداً لواحد):** `connected` · `disconnected` · `slow` (عتبة زمن config) · `needs_loading` (= «تسخين/warm-cold» في v0.6) · `context_error` · `permission_restricted` (خارج Profiles دور الناظر — تُحسب لحظياً لكل ناظر ولا تُخزَّن كحالة عامة).

## §10 الملفات التعريفية والتوجيه (Model Profiles &amp; Routing)
- **Model Profile:** كيان تعريف محكوم (v0.6 §6): ربط + معاملات + نطاق معرفة افتراضي + أدوار مسموحة + labels — بدورة الاعتماد الموحّدة.
- **ترتيب حسم النموذج لطلبٍ ما:** (1) Profile صريح اختاره المستخدم **إن كان ضمن (أدواره ∩ المسموح في مشروعه)** ← (2) Profile الافتراضي للمشروع ← (3) افتراضي النظام للوكيل/القدرة من المصفوفة. **سقف الأدمن دائم**: ما عُطِّل مركزياً لا يُفعَّل من أي طبقة أدنى.
- **الافتراضي حسب المهمة:** صفوف المصفوفة نفسها (embedding/rerank/ocr/asr/vision_caption + chat/report/sql-agent/validation) — لا قناة موازية.
- **fallback:** سلسلة الربط ثم سقوط Profile→Default-Profile (v0.6) — كلاهما بشارة/حدث.
- **تدقيق الاختيار:** `model_ref + profile_key` يُختمان في حمولة أحداث التقديم (CHAT_ANSWER_SERVED وما شابه) وفي كل فعل منفَّذ بمساعدة نموذج بخطورة ≥ medium، وفي أحداث خطوات runs (v0.6 §10).

## §11 أحداث التدقيق (بلا أسرار في أي حمولة — endpoint بالمرجع الاسمي فقط)
| الحدث | متى | حمولة نموذجية |
|---|---|---|
| PROVIDER_HEALTH_CHECKED | **تغيّر حالة** أو فحص يدوي (لا كل نبضة) | provider_id · old→new · latency_class · checked_by? |
| PROVIDER_DISCOVERY_RUN | بدء اكتشاف (يدوي/مجدول) | provider_id · mode · actor |
| MODEL_DISCOVERY_REFRESHED | اكتمال الاكتشاف | provider_id · counts(before→after) · duration · status |
| PROVIDER_TESTED (قائم) | زر اختبار الاتصال | provider_id · result · latency_class |
| PROVIDER_CHANGE_REQUESTED (قائم) | submit للـ workflow | الحقول التصريحية للطلب |
| **PROVIDER_CONFIG_APPLIED_BY_OPS** | إقفال Ops لتغيير/نشر config | provider_id/all · config_version · request_ref? — **الاسم الكنسي**؛ يوحَّد معه اسم v0.6 السابق PROVIDER_CHANGE_COMPLETED (Patch P-4 في مراجعة v0.7) |
| MODEL_PROFILE_DEFINED/CHANGED/ACTIVATED/ROLLED_BACK (قائمة v0.6) | دورة حياة الـ Profile | profile_key · diff-مرجعي |
| (التوجيه) | تغييرات المصفوفة تُدقَّق بالحدثين القائمين **CAPABILITY_BINDING_CHANGED / AGENT_BINDING_CHANGED** — لا حدث مظلي مكرر باسم MODEL_ROUTING_CHANGED | — |
| **MODEL_FALLBACK_USED** | تقدّم فعلي في سلسلة fallback (مرة/طلب) | correlation_id · from_ref→to_ref · reason(rate_limit/timeout/unreachable/context) · profile_key? |

## §12 السجلات والتعقيم (Logging &amp; Redaction)
مرشّح تعقيم مركزي إلزامي على كل مخرجات السجل: قائمة منع مفاتيح (api_key · authorization · token · secret · password · base_url وفق OD-PSC-2) ⇒ **[REDACTED]** · **لا تُسجَّل ترويسات Authorization إطلاقاً** ولا أجسام نداءات النماذج في الإنتاج (ملخصات وصفية فقط) · سطر سجل نداء المزوّد = ميتاداتا: provider_id · model_ref · latency · status · **correlation_id · request_id** (انتشارهما إلزامي طرفاً-لطرف — constitution) · محرك قناع `admin.logs` (P1) هو نقطة العرض الوحيدة للمخوّلين.

## §13 أنماط الفشل (Failure Modes)
| النمط | سلوك الـ Backend | إشارة الواجهة | التدقيق |
|---|---|---|---|
| مزوّد غير متاح | health=unreachable · الموجّه يتخطاه · fallback | chip disconnected · banner عند شمول القدرة الحوارية | HEALTH_CHECKED (تغيّر) · FALLBACK_USED |
| secret_ref غير صالح | misconfigured **معزولاً** · fail-closed · تنبيه Ops | chip «غير متصل — خطأ تهيئة» (عام) | HEALTH_CHECKED |
| فشل الاكتشاف | إبقاء آخر كتالوج + وسم قِدَم · backoff | عدّادات بوسم «قديم منذ…» | DISCOVERY_RUN/REFRESHED(status=failed) |
| نموذج غير محمَّل | needs_loading · تسخين محكوم بمهلة (حسب العائلة) | chip «تحميل/تسخين» | — (حالة لا حدث) |
| تجاوز نافذة السياق | error_code `LLM_CONTEXT_EXCEEDED` — **لا اقتصاص صامت** (السياسة: رفض مفسَّر في v1) | رسالة مفسَّرة على البطاقة/الخطوة | ضمن حدث التقديم/الخطوة |
| Rate limit | backoff ثم fallback | شارة «نموذج بديل» عند السقوط | FALLBACK_USED(reason=rate_limit) |
| Timeout | مهلات لكل قدرة (P6 config) · إعادة بحسب السياسة ثم fallback | كما فوق | FALLBACK_USED(reason=timeout) |
| استنفاد سلسلة fallback | `LLM_UNAVAILABLE` fail-closed | ws: الوضع الحتمي (v0.4 §9) · runs: توقف خطوات الوكلاء معلَّلاً (v0.6) | حدث فشل التقديم/RUN_STEP |

## §14 قرارات مفتوحة
| OD | الموضوع | التوصية |
|---|---|---|
| OD-PSC-1 | مخزن الأسرار لأول تنفيذ | **env + ملفات أسرار محلية** (mounted بصلاحيات مقيّدة)؛ encrypted_config اختياري؛ Vault مؤجل بواجهة مهايئ محجوزة |
| OD-PSC-2 | حساسية endpoint_ref | **حساس افتراضياً**: يُقنَّع في السجلات ولا يظهر في UI إلا كاسم مرجع (حتى في admin.config_profiles)؛ علم استثناء لكل مدخل بيد Ops |
| OD-PSC-3 | مدة كاش الاكتشاف | مفتاح config بمهلة معتدلة + تحديث يدوي متاح دائماً (`discovery.run`)؛ القيمة تُثبَّت عند تفعيل P5/P6 |
