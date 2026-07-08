# UI_V06_DELTA_AMENDMENTS.md — سجل تعديلات Δ على v0.4/v0.5 (مقترح — غير مطبَّق)

> **Version:** 1.0 — Proposed (v0.6) · **Date:** 2026-07-08 · **الموضع الهدف:** `ui/UI_V06_DELTA_AMENDMENTS.md`
> **الطبيعة:** patches نصية دقيقة (مِرساة الموضع + النص الجاهز للإدراج/الاستبدال). **لا يُعدَّل أي ملف أصلي في هذه الدفعة** — التطبيق الفعلي يتم في commits التطبيق بعد اجتياز بوابة v0.6، ويبقى هذا الملف مرفوعاً كسجل Δ للتتبع.
> **قرارات المالك النافذة على كل بند:** v0.6 إضافية فوق v0.4+v0.5 · D9/الخيار A (لا Base URL/API Key/أسرار/endpoints حقيقية في UI) · الأفعال المعتمدة: run · escalate · compare · **template.create يبقى OD غير معتمد** · المعرّفان runs.list/runs.detail نهائيان · لا سايبر ولا terminal.

---

## Δ-1 — `UI_SCREEN_INVENTORY.md` ← v1.2 (إضافة runs.list / runs.detail)

**أ) ترقية الرأس** — استبدال سطر الإصدار في الترويسة:
> **قبل:** `Version: 1.0` (أو `1.1` إن كانت الترقية الضمنية مطبَّقة)
> **بعد:** `Version: 1.2 — Proposed (Δ v1.1: +admin.retrieval_tester من تصميم P5 · Δ v1.2: +runs.list/+runs.detail من UI_RUN_EXECUTION_MODEL v0.6)`

**ب) الجدول A** — مِرساة: **بعد صف `admin.retrieval_tester` مباشرة** — الصفان الجاهزان (بنفس أعمدة الجدول):
| runs.list | تشغيلاتي | /me/runs | 6 (يمتد P7) | مستخدم (+مراقب بنطاق) | me-runs | ✖ | G14 | Med |
| runs.detail | تفصيل تشغيل | /me/runs/{id} | 6 (يمتد P7) | مستخدم (+مراقب بنطاق) | me-runs | ✖ | G14 | High |
> عمود Dual = ✖ لأنهما سطحا **مراقبة** حتميان؛ التكامل مع ws يكون بربط (chip حالة + «فتح التشغيل») لا بازدواج فعل.

**ج) الجدول B** — مِرساة: **بعد صف `admin.retrieval_tester` مباشرة** — الصفان الجاهزان:
| runs.list | متابعة تشغيلات المستخدم (تقارير/خطوط/تسلسلات موصلات) وحالاتها | التعريف · الحالة · التقدم x/y · المدة · النوع | run.start (إطلاق جديد) · run.cancel (من الصف) | runs.read (ملكية + نطاق) · runs.start | RUN_STARTED · RUN_CANCELLED | RLS بالمُطلِق؛ **ليست terminal ولا سطح تنفيذ حر** |
| runs.detail | مراقبة تنفيذ محكوم: خط زمني · بوابات اعتماد/HITL · أدلة/مخرجات · إعادة/إلغاء | خطوات وحالاتها · عقد البوابات · لوحة المخرجات · سلسلة correlation | run.cancel · run.retry(+_step) · version.compare · فتح البند (queue) | runs.read/cancel/retry · تبويب التدقيق audit-visible | مجموعة RUN_* (مواصفة §10) | يقرأ سلسلة التدقيق القائمة (مصدر واحد)؛ القرارات على queue.approval_detail |

**د) سطر مرافق في `UI_SITEMAP.md`** (جزء من نفس الـ Δ كي لا يتيه القسم) — مِرساة: داخل قسم «/me» بعد بند الاعتمادات:
> - **تشغيلاتي** `/me/runs` (P6+): قائمة وتفصيل التشغيلات المحكومة — سمة UF، مراقبة فقط، Dual ✖.

---

## Δ-2 — `UI_SCREEN_BEHAVIOR_CARDS.md` (v0.5): أربع بطاقات جديدة

**مِرساة:** بعد البطاقة 19 (`admin.health`) وقبل قسم «قواعد عامة لـ Stitch». الترقيم يستمر 20–23 (لا إعادة ترقيم للقائم).

### 20) `projects.main` — المشاريع (حاوية سياق وصلاحية)
- **افتراضياً يظهر:** رأس المشروع (الاسم/الوصف/عدّاد الأعضاء/شارة تصنيف أقصى) + شريط تبويبات (نظرة عامة · المحادثات · الملفات · المهام والاعتمادات · التقارير · الإعدادات) — «نظرة عامة» نشط بعدّادات وآخر نشاط + زر **«فتح في الـ Workspace»**.
- **مطويّ:** بقية التبويبات؛ تفاصيل السياسات داخل «الإعدادات».
- **حسب الصلاحية:** العضوية شرط الرؤية أصلاً (غير العضو: HIDDEN/403)؛ تبويب الإعدادات لمدير المشروع؛ محتوى كل تبويب مرشَّح بصلاحيات عناصره (ملف بتصنيف أعلى لا يظهر لعضو أدنى).
- **drawer:** إضافة/تفاصيل عضو · معاينة عنصر (ملف/مهمة).
- **modal:** أرشفة المشروع (typed).
- **page:** فتح محادثة ⇒ ws.main بجلسة مروَّسة بسياق المشروع (نطاق المعرفة الافتراضي + Model Profile الافتراضي من إعدادات المشروع) · سجل ⇒ run.detail · تقرير ⇒ reports.review · تشغيل ⇒ runs.detail.
- **متى إلى Renderer:** عناصر التبويبات تفتح أسطحها الأصلية دائماً — المشروع لا يعرض بديلاً موازياً.
- **يجب أن يراه Stitch:** الرأس + 6 تبويبات (واحد نشط) + تبويب «الإعدادات» يعرض: نطاق معرفة افتراضي · Model Profile افتراضي · قائمة Profiles المسموحة (أسماء وهمية) + زر «فتح في الـ Workspace».
- **يجب ألا يراه Stitch:** kanban ضخم · إحصاءات BI · «مشاركة عامة/رابط عام» · شعارات · أي إيحاء بأن المشروع «ذاكرة ذكاء» (هو حاوية حوكمة).
- **الحالات المطلوبة:** default · loading · empty (مشروع جديد بإرشاد) · error · permission-denied · audit-visible (سجل نشاط المشروع للمخوّل).

### 21) `reports.review` — مراجعة التقرير (اعتماد المحتوى)
- **افتراضياً يظهر:** ترويسة (القالب/النسخة/الحالة/شارة تصنيف) + قائمة الأقسام (start) + القسم المحدد بمحتواه **بشارة «مُولَّد»** واستشهاداته المرقّمة + شريط قرار المراجعة (اعتماد · إرجاع قسم للتوليد · رفض).
- **مطويّ:** تعليقات المراجعة لكل قسم (inline expand) · تاريخ النسخ (drawer).
- **حسب الصلاحية:** القرار لـ reports.review؛ قسم مصادره خارج نطاق الناظر ⇒ محتواه محجوب بعلامة «محتوى مقيّد».
- **drawer:** استشهادات القسم التفصيلية · ملخص التشغيل («عرض التشغيل» المختصر).
- **modal:** الاعتماد النهائي (typed) · اعتماد تقرير **جزئي** مع placeholder ⇒ **typed-ack** (OD-RUN-2).
- **page:** «عرض التشغيل الكامل» ⇒ runs.detail · بعد الاعتماد ⇒ نسخة نهائية للقراءة.
- **متى إلى Renderer:** فتح سجلات مصدر الاستشهاد ⇒ run.detail/profile.entity.
- **يجب أن يراه Stitch:** قسم مكتمل (مُولَّد + استشهادات + حقل تعليق) وقسم placeholder «قسم لم يُولَّد (سبب)» وشريط القرار وحالة typed-ack للجزئي.
- **يجب ألا يراه Stitch:** تحرير حر للنص المولَّد بلا أثر نسخة · تصدير بلا وسم · مشاركة خارجية · «إعادة توليد» بلا سبب مسجَّل.
- **الحالات المطلوبة:** default · loading · empty (بانتظار التوليد) · error · disabled (القرار لغير المخوّل/SoD) · approval · success · failed · audit-visible.

### 22) `admin.agents` — ربط الوكلاء (per-agent)
- **افتراضياً يظهر:** جدول الوكلاء الأربعة (chat/reasoning · report · sql-agent · validation): النموذج الحالي · fallback · آخر تعديل (مَن/متى) · شارة «يتطلب اعتماداً في الإنتاج».
- **مطويّ:** معاملات كل وكيل (تُفتح في drawer التحرير).
- **حسب الصلاحية:** admin.models.manage؛ العرض admin.models.view.
- **drawer:** تحرير ربط وكيل (معاملات ضمن حدود config) + «أثر التغيير».
- **modal:** تأكيد **typed** للحفظ في الإنتاج.
- **page:** رجوع إلى مصفوفة Routing في admin.capabilities (المصدر الموحّد).
- **متى إلى Renderer:** N/A (Console).
- **يجب أن يراه Stitch:** 4 وكلاء بأسمائهم الوظيفية فقط + drawer تحرير واحد مفتوح + شارة اعتماد-الإنتاج + حالة فشل حفظ برسالة مفسَّرة.
- **يجب ألا يراه Stitch:** أسماء/شعارات نماذج تجارية كعلامات · endpoints · معاملات GPU · «إحصاءات استهلاك».
- **الحالات المطلوبة:** default · loading · empty · error · disabled (Safe Mode) · confirmation · approval · success · failed · audit-visible.

### 23) `runs.detail` — تفصيل التشغيل (مرجعها الكامل: UI_RUN_EXECUTION_MODEL)
- **افتراضياً يظهر:** الرأس (≤3 أزرار سياقية: إلغاء أثناء التشغيل / إعادة عند الفشل) + **الخط الزمني** (خطوات L0) + لوحة المخرجات بتبويبات مطوية.
- **مطويّ:** تبويبا الاستشهادات والتدقيق · تفاصيل كل خطوة (Step Drawer) · السجل المُهيكل.
- **حسب الصلاحية:** تبويب التدقيق **بلا رأس** لغير audit.view؛ كل رابط دليل يعيد فحص صلاحية الناظر على العنصر (لا توسيع وصول).
- **drawer:** Step Drawer · diff المقارنة (version.compare) · فلاتر السجل المُهيكل.
- **modal:** إلغاء (typed) · إعادة عند أثر act خارجي (typed).
- **page:** هذه الشاشة page · «فتح البند» ⇒ queue.approval_detail (**القرار هناك حصراً**) · «فتح في التدقيق» ⇒ admin.audit بفلتر correlation.
- **متى إلى Renderer:** فتح مخرَج (سجل ⇒ run.detail · تقرير ⇒ reports.review · ملف ⇒ إدارة الملفات).
- **يجب أن يراه Stitch:** فرعان متوازيان بعقدة دمج · عقدة بوابة paused برابط البند · Step Drawer بمدخل مقنَّع · Tool Call Row بحالة «مخرَج كبير — ملف» · حالة partial بملخصها · modal الإلغاء.
- **يجب ألا يراه Stitch:** **أي console/terminal/سطر أوامر** · صياغات أمنية (فحص/ثغرات/هدف) · خرائط attack-surface · progress استعراضي.
- **الحالات المطلوبة:** حالات الـ run (§2) + حالات الخطوة (§6) من المواصفة.

---

## Δ-3 — `UI_COMPONENT_STATES.md` (v0.5): أربعة مكوّنات جديدة (14–17)

**مِرساة:** بعد المكوّن 13 (Audit Log Row) وقبل «§14 قواعد الاستخدام في Stitch». (تصحيح ترقيم القسم الأخير إلى §18 عند التطبيق.)

### 14) Provider Card (بطاقة مزوّد — admin.capabilities/تبويب Providers)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | حقول القائمة المقفلة (§3 من مواصفة المزوّدات): alias · type · secret_ref-بالاسم+قفل · chip الحالة · آخر فحص · العدّادات الثلاثة · زر اختبار · زر طلب تغيير |
| S2 | collapsed | صف مضغوط في القائمة (alias + chip + عدّاد قابل للاستخدام) |
| S3 | expanded | drawer end تفاصيل — **بلا أي حقل حساس حتى هنا** |
| S4 | loading | skeleton بطاقة |
| S5 | empty | «لا مزوّدات معلنة — تُعرَّف عبر config» + زر «طلب تهيئة مزوّد» |
| S6 | error | تعذّر قراءة الحالة ⇒ chip رمادي متقطع + إعادة محاولة |
| S7 | permission-denied | الشاشة admin-only — لا بطاقة تصل لغير المخوّل |
| S8 | disabled | Safe Mode: زرا الاختبار والطلب معطَّلان بسبب موحّد |
| S9 | hidden | N/A (كل المعلن في config يظهر للمخوّل) |
| S10 | masked | **تقنيع بنيوي دائم**: secret_ref اسماً فقط؛ لا وجود أصلاً لقيم URL/سر |
| S11 | confirmation | N/A (لا فعل خطر مباشر — التغيير عبر workflow) |
| S12 | approval | شارة «طلب معلّق #» عند وجود wf.provider_change مفتوح |
| S13 | success | اختبار الاتصال ⇒ chip نجاح فقط |
| S14 | failed | اختبار ⇒ chip فشل + رسالة عامة قابلة للنسخ بمرجع correlation |
| S15 | audit-visible | drawer «تاريخ الفحوصات/الطلبات» للمخوّل |

### 15) Model Profile Selector (`ws.model_profile_selector`)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | **مخفي للمستخدم العادي** (الافتراضي يعمل بصمت — OD-MX-1)؛ للدور المخوَّل: chip باسم الـ Profile الحالي بجوار محدد النطاق |
| S2 | collapsed | chip فقط |
| S3 | expanded | قائمة Profiles المسموحة لدوره (label + سطر وصف) — **لا أسماء نماذج خام أبداً** |
| S4 | loading | skeleton خفيف |
| S5 | empty | N/A (Default Profile موجود دائماً) |
| S6 | error | تعذّر الجلب ⇒ الإبقاء على الحالي + إشعار خفيف |
| S7 | permission-denied | الخيارات خارج الدور HIDDEN-SERVER |
| S8 | disabled | Profile بمزوّد ساقط ⇒ خيار معطَّل بسبب؛ Safe Mode ⇒ المحدد كله معطَّل |
| S9 | hidden | حالة S1 للمستخدم العادي |
| S10 | masked | N/A |
| S11 | confirmation | التبديل فوري بلا تأكيد (نطاق الجلسة) |
| S12 | approval | N/A (الاعتماد على تعريف الـ Profile في الـ Console) |
| S13 | success | تطبيق فوري + تأشير بصري |
| S14 | failed | رجوع للسابق + رسالة |
| S15 | audit-visible | model_ref/profile_key ضمن حمولة أحداث الجلسة للمخوّل |

### 16) Run Timeline Step (خطوة الخط الزمني — runs.detail)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | صف L0: رقم · اسم · أيقونة نوع (وكيل/Validation/فعل/موصل) · chip حالة · مدة |
| S2 | collapsed | كما S1 (الصف مضغوط أصلاً) |
| S3 | expanded | inline ملخص سطرين ⇒ «تفاصيل» يفتح Step Drawer |
| S4 | loading | running بنبض |
| S5 | empty | N/A |
| S6 | error | failed + error_code (السبب المفسَّر في الـ Drawer) |
| S7 | permission-denied | **بنية الخط مرئية لصاحب التشغيل دائماً؛ التقنيع للمحتوى**: خطوة بمحتوى فوق clearance تُظهر العنوان والحالة ومحتواها «مقيّد» |
| S8 | disabled | «إعادة من هنا» معطَّل لغير المؤهلة بسبب (نجحت/غير قابلة للإعادة) |
| S9 | hidden | N/A (انظر S7) |
| S10 | masked | digest المدخل/المخرج مقنَّع بحسب التصنيف |
| S11 | confirmation | retry_step ⇒ typed عند أثر act |
| S12 | approval | awaiting_approval: عقدة بوابة مميّزة + «فتح البند» (القرار على queue) |
| S13 | success | succeeded |
| S14 | failed | failed؛ والتوابع skipped بملاحظة «تخطٍّ بسبب فشل الخطوة N» |
| S15 | audit-visible | مراجع أحداث الخطوة داخل الـ Drawer للمخوّل |

### 17) Run Output Panel (لوحة الأدلة/المخرجات — runs.detail)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | تبويبات مطوية: المخرجات (بعدّاد) · الاستشهادات · التدقيق |
| S2 | collapsed | رؤوس فقط؛ **رأس «التدقيق» غائب كلياً** لغير audit.view |
| S3 | expanded | تبويب واحد مفتوح؛ «المخرجات» يفتح تلقائياً عند أول ناتج (قياس OD-IX-2) |
| S4 | loading | skeleton عناصر |
| S5 | empty | «لا مخرجات بعد» |
| S6 | error | صف عنصر تعذّر جلبه + إعادة |
| S7 | permission-denied | عنصر بتصنيف أعلى من الناظر ⇒ يظهر «عنصر مقيّد» **بلا فتح** (القاعدة الذهبية §9) |
| S8 | disabled | زر فتح معطَّل بسبب حالة العنصر (قيد اعتماد) |
| S9 | hidden | لغير المخوّل بالـ run لا لوحة أصلاً |
| S10 | masked | مقتطفات الاستشهاد الحساسة «•••» |
| S11 | confirmation | N/A |
| S12 | approval | عنصر تقرير بانتظار مراجعة ⇒ شارة + رابط reports.review |
| S13 | success | فتح العنصر في سطحه |
| S14 | failed | ملف offload مفقود/محذوف ⇒ رسالة بديلة + مرجع |
| S15 | audit-visible | تبويب التدقيق: سلسلة correlation للـ run بنفس محرك admin.audit |

---

## Δ-4 — `UI_ACTION_BUTTON_MODEL.md` (v0.4): جدول عقود جديد 6.c

**مِرساة:** بعد جدول 6.b مباشرة وقبل §7. **النص الجاهز:**

### 6.c أفعال التشغيل والمقارنة والتصعيد (v0.6 — الأفعال المعتمدة: run · escalate · compare)
| action_id | permission | inputs/validation | confirm | approval | effect/backend | audit | risk | rollback |
|---|---|---|---|---|---|---|---|---|
| run.start | runs.start + صلاحية التعريف | definition_ref + معاملات معلنة | simple/**typed** بخطورة التعريف | بوابات داخل التعريف | api: runs_start ⇦ POST /api/v1/runs | RUN_STARTED | med/high | لا (الإلغاء بديلاً) |
| run.cancel | runs.cancel (مالك/نطاق) | سبب اختياري | **typed** | لا | api: runs_cancel ⇦ POST /api/v1/runs/{id}/cancel | RUN_CANCELLED | med | — |
| run.retry | runs.retry | — (يرث معاملات الأصل) | typed عند أثر act | كما التعريف | api: runs_retry ⇦ POST /api/v1/runs/{id}/retry | RUN_RETRIED | med/high | — |
| run.retry_step | runs.retry | step_ref | typed عند أثر act؛ **HITL يُعاد** لغير القابلة للإعادة | كما التعريف | api: runs_retry_step ⇦ POST /api/v1/runs/{id}/retry-step | RUN_RETRIED(from_step) | med/high | — |
| approval.escalate | approvals.escalate (SoD: ≠ المقدِّم) | تعليق إلزامي | **typed** | يرفع البند لمستوى أعلى بالمصفوفة | api: approvals_escalate ⇦ POST /api/v1/approvals/{id}/escalate | APPROVAL_ESCALATED | high | لا |
| version.compare | runs.read أو *.view للهدف | مرجعا المقارنة | none (قراءة) | لا | open: drawer diff | — | low | — |
> **سطر مرافق يُلحق بقسم §9 (Open Decisions):** «OD-AB-4 — template.create («حفظ كقالب»): **Optional غير معتمد بقرار المالك 2026-07-08** — لا يدخل الكتالوج ولا العقود إلا بقرار صريح لاحق (مرجعه OD-TPL-1 في UI_RUN_EXECUTION_MODEL).»

---

## Δ-5 — `UI_FIELD_NAMING.md` (v0.4): توسعة الكتالوج + منطقة runs

**أ) استبدال صف OD-NM-1 في §8:**
> **قبل:** «OD-NM-1 | إقفال قائمة كتالوج الأفعال v1 | القائمة في §5 تُثبَّت مع Clarify تفعيل P3 (مالك الـ Registry)»
> **بعد:** «OD-NM-1 | كتالوج الأفعال | **وُسِّع بقرار المالك 2026-07-08 بثلاثة أفعال: run · escalate · compare**؛ بقية القائمة تُثبَّت مع Clarify تفعيل P3. **دلالة run مؤسسية حصراً**: تنفيذ تعريف معلن (تقرير/خط orchestrator/تسلسل موصل) — لا تعني terminal ولا cybersecurity run ولا جلسة أوامر»

**ب) إلحاق بعد قائمة §5 (كتالوج الأفعال):**
> **إضافة معتمدة (2026-07-08):** run · escalate · compare. (template ليس noun معتمداً — انظر OD-AB-4.)

**ج) إلحاق صف بسلسلة الربط §3 (بعد صف «فعل موصل كاتب»):**
| إطلاق تشغيل ومتابعته | runs.list / runs.detail | /me/runs · /me/runs/{id} | run.start | runs.start | runs_start ⇦ POST /api/v1/runs | RUN_STARTED | run_id · definition_ref · correlation_id | RunTimeline / StepDrawer |
> **وسطر توثيق منطقة:** «المنطقة `runs` (شاشتا runs.list/runs.detail) **مثبَّتة بقرار المالك** — يُمنع استخدام بدائل مثل agent_runs أو execution_console.»

---

## Δ-6 — `UI_UX_ASSUMPTIONS.md` (v0.4): A-UX-15

**مِرساة:** بعد A-UX-14 مباشرة. **النص الجاهز:**
> **A-UX-15 — تجربة المزوّد/النموذج/التشغيل (v0.6):** (أ) إدارة المزوّدات **قراءةً** وفق D9/الخيار A — لا Base URL ولا API Key ولا أسرار ولا endpoints حقيقية في الواجهة؛ التغيير الفعلي عبر Ops/config/secret_ref وworkflow «طلب تهيئة/تعديل مزوّد» فقط. (ب) اختيار المستخدم عبر **Model Profiles** منسّقة مُدارة بدورة اعتماد — لا أسماء نماذج خام؛ وإعداد الأدمن سقفٌ دائماً. (ج) عارض التشغيل (runs.list/runs.detail) **سطح مراقبة مؤسسي يقرأ سلسلة التدقيق القائمة** — ليس terminal ولا cyber console ولا سطح تنفيذ حر؛ القرارات تبقى على سطح الاعتماد الرسمي. (القرارات المفتوحة المرتبطة: OD-MX-1/3/4 · OD-RUN-1..3 · OD-TPL-1 في مواصفتَي v0.6.)

---

## Δ-7 — سطور قصيرة في ملفَّي v0.5

**أ) `UI_INTERACTION_MODEL.md` — إلحاق أربعة صفوف بمصفوفة الحسم §4** (بعد صف «dashboard admin»):
| تفصيل تشغيل (runs.detail) | **page** | مراقبة طويلة تستحق مساراً ورجوع متصفح |
| تفصيل خطوة تشغيل | **drawer end** (Step Drawer) | قراءة موازية للخط الزمني |
| مخرَج خطوة ضخم | **offload إلى ملف محكوم** — يُعرض من لوحة المخرجات (لا inline dump ولا console) |
| تفاصيل مزوّد/نموذج | **drawer end** | قراءة D9-آمنة بلا حقول حساسة |

**ب) `UI_VISIBILITY_RULES.md` — فقرة قصيرة تُلحق بنهاية §1** (بعد «قاعدة الأمن الحاسمة»):
> **قاعدة D9 البنيوية (v0.6):** الأسرار وendpoints الحقيقية **HIDDEN-SERVER دائماً وبنيوياً** — لا تُخزَّن في طبقة الواجهة ولا تصل إليها في أي حالة من الحالات الخمس عشرة؛ `secret_ref` يظهر **بالاسم فقط** (تقنيع بنيوي S10). وحالة التشغيل `paused_awaiting_approval` تُعامل وسمياً كـ `after-approval` على مستوى الـ run (البند يُقرَّر على سطح الاعتماد الرسمي).

---

## Δ-8 — `UI_ADMIN_CONSOLE_MODEL.md` (v0.4): ملاحظة المجموعة F

**مِرساة:** نهاية فقرة «F) Models &amp; Providers — G10». **النص الجاهز:**
> **(v0.6)** وُسِّعت `admin.capabilities` إلى أربعة تبويبات: **Providers (قراءة) · Models · Routing · Profiles** وفق `UI_PROVIDER_MODEL_MANAGEMENT.md`، مع بقاء **قائمة منع D9 نافذة حرفياً** (لا endpoints/أسرار/GPU في أي تبويب)؛ أي تغيير فعلي للمزوّد يمر حصراً عبر workflow «طلب تهيئة/تعديل مزوّد» إلى Ops (config/secret_ref خارج المنصة)، والواجهة مرآة قراءة لحالته.

---

## Δ-9 — `UI_REFERENCE_USAGE_POLICY.md` (v0.4): صفّان في جدول §7

**مِرساة:** بعد صف «Microsoft Admin Center / Linear / GitHub». **الصفان الجاهزان (بنفس أعمدة الجدول):**
| PentAGI | دراسة أنماط **عرض التشغيل والإشراف** (خط زمني، إشراف خطوات، تقارير من تشغيل) **من الصور والوثائق فقط — ليس في كتالوج الكود** | أي كود · أي ميزة سايبر/أدوات هجومية · terminal · نسخ layout حرفي · الهوية |
| RedAmon | دراسة أنماط **بنية المشروع/Presets/موافقات لكل خطوة/تفريغ المخرجات الضخمة** **صوراً وويكي فقط — ليس في كتالوج الكود** | أي كود · أي ميزة سايبر (recon/exploit/shell) · terminal · نسخ layout حرفي · الهوية |

---

## الملفات التي ستتغير لاحقاً عند تطبيق هذا السجل (11)
| # | الملف | Δ | طبيعة التغيير |
|---|---|---|---|
| 1 | UI_SCREEN_INVENTORY.md → **v1.2** | Δ-1 | +4 صفوف (A/B) + ترويسة |
| 2 | UI_SITEMAP.md | Δ-1(د) | سطر واحد /me |
| 3 | UI_SCREEN_BEHAVIOR_CARDS.md | Δ-2 | +4 بطاقات (20–23) |
| 4 | UI_COMPONENT_STATES.md | Δ-3 | +4 مكوّنات (14–17) |
| 5 | UI_ACTION_BUTTON_MODEL.md | Δ-4 | +جدول 6.c + OD-AB-4 |
| 6 | UI_FIELD_NAMING.md | Δ-5 | OD-NM-1 + §5 + صف §3 |
| 7 | UI_UX_ASSUMPTIONS.md | Δ-6 | +A-UX-15 |
| 8 | UI_INTERACTION_MODEL.md | Δ-7(أ) | +4 صفوف §4 |
| 9 | UI_VISIBILITY_RULES.md | Δ-7(ب) | فقرة §1 |
| 10 | UI_ADMIN_CONSOLE_MODEL.md | Δ-8 | ملاحظة F |
| 11 | UI_REFERENCE_USAGE_POLICY.md | Δ-9 | +صفّان §7 |
**لن يتغير:** بقية ملفات v0.4/v0.5 · أي تصميم مرحلي · المعمارية · D9. **التطبيق:** بعد بوابة v0.6 وبأمر المالك، ويُرفع هذا السجل معها للتتبع.
