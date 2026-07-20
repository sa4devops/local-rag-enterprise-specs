# UI_SCREEN_GOVERNANCE_STANDARD.md — معيار حوكمة الشاشات (Capstone)

> **Version:** 1.0 — Accepted — G1-B 2026-07-20 (merge dd098dff9bed7a1f267ec5552b0e3366e368883d · tag v1.2-governance-baseline) · **Date:** 2026-07-19 · **الموضع:** `ui/UI_SCREEN_GOVERNANCE_STANDARD.md`
> **Authority:** قائد المرتبة 8 (`AUTHORITY.md`) — **طبقة ربط وإلزام رقيقة فوق المنظومة القائمة، لا تكرر محتواها** (‏EC-11)؛ عند أي تعارض داخل ui/ يُقرأ عبر جدول الإلزام أدناه ثم قواعد الحسم في `AUTHORITY.md §2`.
> **Purpose:** تنفيذ متطلب حوكمة الشاشات (§18) بالربط والإلزام والاختبارية: من يُلزم بماذا، وأي نمط تُشتق منه معايير القبول، وأين حدود حرية أدوات التوليد (Rocket).

## (أ) جدول الإلزام — تصنيف منظومة ui/ (24 ملفاً)
| التصنيف | الملفات | الأثر |
|---|---|---|
| **ملزم-معياري** | هذا الملف · ‏UI_SCREEN_INVENTORY (**السجل المركزي الوحيد للشاشات/المسارات**) · ‏UI_FIELD_NAMING (**المصدر الكنسي للتسمية**) · ‏UI_INTERACTION_MODEL · ‏UI_VISIBILITY_RULES · ‏UI_PROGRESSIVE_DISCLOSURE · ‏UI_COMPONENT_STATES ‏(S1–S20) · ‏UI_SCREEN_BEHAVIOR_CARDS · ‏UI_ACTION_BUTTON_MODEL · ‏UI_DESIGN_SYSTEM · ‏UI_UX_ASSUMPTIONS · ‏UI_ADMIN_CONSOLE_MODEL · ‏UI_AI_WORKSPACE_MODEL · ‏UI_RUN_EXECUTION_MODEL · ‏UI_PROVIDER_MODEL_MANAGEMENT · ‏UI_REFERENCE_USAGE_POLICY · ‏UI_V06_DELTA_AMENDMENTS | مخالفتها عيب يُرد؛ التغيير عبر دفعة موثقة فقط |
| **ملزم-عند-التفعيل** | UI_SCREEN_CARDS_BY_PHASE (حِزم كل مرحلة تنفَذ مع تفعيلها) · ‏UI_GATE_REVIEW_CHECKLIST (بوابة جودة UI لكل تسليم واجهة) | تفعيل مرحلي/بوابي |
| **مرجع-تصميمي** | UI_SITEMAP (تصوّر مشتق — الجرد يحكم عند أي فرق) | استرشاد لا إلزام |
| **تاريخي-سجلّي** | UI_REFINEMENT_GATE_REVIEW · ‏UI_V06_GATE_REVIEW (سجلا بوابتين منجزتين) | قراءة تاريخية؛ نتائجهما المدمجة نافذة في مواضعها |
| **تاريخي-informative** | UI_STITCH_PROMPTS_BY_PHASE · ‏UI_STITCH_REFINED_PROMPTS | **يُعاد تصنيفهما بلا مساس بمحتواهما**: برومبتات جيل أدواتٍ سابق؛ لا تُقرأ كمتطلبات — البديل الحي: هذا المعيار + العقود + `ROCKET_OPERATING_MODEL` |

**قاعدة حياد الأدوات — إعادة توجيه رسمية:** كل نص في المنظومة خاطب «Stitch» يُقرأ اليوم مخاطِباً **قناة Rocket وأي أداة توليد** — أسماء الأدوات مراجع سير عمل لا متطلبات منتَج (القاعدة القائمة أصلاً في المنظومة، تُعمَّم هنا).

## (ب) الأنماط الثمانية (Archetypes) وقاعدة الاشتقاق
| Archetype | التعريف السطري | أمثلة (الإسناد الكامل للـ52 شاشة في عمود `archetype` بالجرد v1.4 — لا يُكرر هنا) |
|---|---|---|
| **List** | جداول/قوائم كيانات بترقيم وفلاتر وأفعال صفوف | run.list · queue.tasks · admin.users |
| **Detail** | عرض سجل/بند واحد بسياقه وأفعاله | run.detail · queue.approval_detail |
| **Form** | إدخال/تحرير بحقول وvalidation | run.form · auth.login |
| **Builder** | تأليف تعريفات وبنى (schemas/عقود/شجرات/مصفوفات) بدورة اعتماد | admin.record_types · admin.workflows · admin.policies |
| **Canvas** | سطح تفاعلي تجريبي حر (playground/لوحات بصرية) | admin.retrieval_tester (والـ workflow canvas إن فُتح OD-P3-2) |
| **Dashboard** | نظرة مجمّعة مؤشرات/بطاقات | admin.dashboard · admin.health · ops.status |
| **Monitor** | متابعة حية لعمليات جارية (خطوط/تشغيلات) | admin.ingestion · runs.detail |
| **Conversational** | السطح المحادثي المحكوم | ws.main |

**قاعدة الاشتقاق:** **معايير القبول والاختبارات تُشتق من الـ Archetype (§هـ)؛ والسلوك الفعلي من بطاقة الشاشة/عقدها** — النمط لا يلغي البطاقة أبداً. *(ملاحظة تقنين: «Renderer-template» المقترح تاسعاً في تقرير v2.0 تحقق بعمود `type=renderer` القائم + الـ archetype — فلا نمط تاسع منفصل؛ انحراف موثق في تقرير تنفيذ G1.)*

## (ج) قرارات السطح والتنقل
1. **شاشة جديدة أم Tab/Drawer/Dialog/Subview؟** الحسم **حصراً** بشجرة القرار ومصفوفة الحسم في `UI_INTERACTION_MODEL §1–§4` — ملزمة لكل أداة توليد.
2. **إنشاء شاشة جديدة = صف جرد جديد بقرار Specification Architect** (بتفويض SA) — ليس قرار منفذ ولا أداة؛ يستلزم: ‏screen_id + route + archetype + بطاقة سلوك ثم عقداً عند مرحلة شاشته.
3. **Deep-Link عام:** كل سطح `page` قابل للفتح بمساره الكنسي مباشرة (تعميم لقاعدة `queue.approval_detail` القائمة)؛ فقدان السياق عند الفتح المباشر يعوَّض من المسار والخادم لا من ذاكرة العميل؛ سلوك الرجوع بقواعد `INTERACTION_MODEL §7` كما هي.
4. **سياق السجل:** أي تمرير/عرض سجل يلتزم رباعية `contracts/identity/RECORD_IDENTITY.md` — ‏`reference_number` ظاهر دائماً في سياق السجل؛ الربط التقني بـ`internal_id` حصراً؛ لا تمرير بالاسم.

## (د) دلتا حالات الشاشة S16–S20
التعريفات والجداول الكاملة (ما يظهر/ما يُخفى/مصدر التبديل) ومصفوفة الانطباق حسب الـ Archetype: **في `UI_COMPONENT_STATES.md` v1.1 §S16–S20 حصراً** (البيت الطبيعي للكتالوج — لا تكرار هنا). الإلزام: كل شاشة تصرّح في عقدها بانطباق كلٍّ من S16–S20 عليها أو استثنائها المعلَّل.

## (هـ) معايير القبول لكل Archetype (المحتوى الجديد الصافي)
**عام لكل الأنماط (يُورَّث):** ‏RTL سليم بالكامل + مفاتيح i18n لكل نص (**صفر نص مضمّن** بعد نفاذ المعيار على الشاشة) · لقطتا Light/Dark · ‏Responsive وفق `DESIGN_SYSTEM` · تنقل لوحة مفاتيح للمسار الرئيس · حالات البطاقة كلها مصمَّمة (قاعدة «غير المذكور لا يُصمَّم» بالعكس أيضاً: المذكور كله يُصمَّم) · ‏HIDDEN-SERVER للأفعال غير المخوَّلة · صفر أسرار/endpoints ‏(D9).
- **List:** ‏S1/S4/S5/S6/S7 مصممة · تمييز **«فارغ»** عن **«فارغ بفلتر مطبَّق»** · ‏pagination أو virtual-scroll معلن · فرز أعمدة RTL سليم · تنقل لوحة مفاتيح للصفوف · ‏bulk-selection إن وُجد فبسقف وسلوك معلنين · صفوف خارج RLS لا تظهر **ولا تُعدّ** · ‏`reference_number` في كل صف.
- **Detail:** رأس ثابت بالرباعية (‏reference_number بارز) · أفعال الرأس ≤3 والبقية تحت ⋯ · سلسلة تدقيق للمخوّل · حقول FLS مقنَّعة لا محذوفة صمتاً · ‏deep-link يفتح كاملاً بلا سياق سابق.
- **Form:** ‏validation خادمية المرجع تُعرض حقلاً-بحقل · تعطيل مزدوج-الإرسال (‏S19) · حفظ/إلغاء بسلوك رجوع `§7` · القيم من التعريف/القاموس لا من كود الشاشة · نجاح/فشل حالتان صريحتان.
- **Builder:** شريط دورة حياة ظاهر دائماً · ‏SoD مرئي ومفروض (المعرِّف لا يعتمد) · ‏Validation قبل التقديم بأخطاء مفسَّرة · ‏diff بين النسخ · كل تفعيل قبل اعتماد = ‏disabled بتفسير · التعريف يُنتج metadata حصراً (‏OD-BLD-1).
- **Canvas:** وسم «تجريبي/أدمن» ظاهر · لا يكتب على بيانات إنتاج · نتائجه قابلة للنسخ/التصدير المحكوم · حدود الموارد معلنة.
- **Dashboard:** كل بطاقة تعلن مصدرها وطابع تحديثها (‏S17 stale ظاهر عند التقادم) · لا أرقام بلا وحدة/سياق · التفاصيل بالنقر إلى شاشتها لا بتكديس هنا.
- **Monitor:** بث/تحديث حي معلن الآلية (‏SSE) مع مؤشر اتصال (‏S16) · خط زمني للأحداث · إيقاف/استئناف المتابعة بيد المستخدم · التقادم يظهر لا يُخفى.
- **Conversational:** حوكمة `UI_AI_WORKSPACE_MODEL` كاملة (بطاقات أفعال بنفس `action_id` · استشهادات · هوية A-UX-17) · لا فعل يُنفَّذ من النص مباشرة بل عبر سلسلة الفعل المحكومة · وضعا العرض (بطاقات/محادثة) وفق OD-WS-4.

## (و) حرية Rocket وحدودها (تفصيل التشغيل في `methodology/ROCKET_OPERATING_MODEL.md`)
**حر** في: التركيب البصري المحلي · ‏micro-interactions · أنماط العرض ضمن `DESIGN_SYSTEM` · تنظيم الكود داخل حدود ADR-0031. **ممنوع قطعياً:** اختراع حقول أو enums أو صلاحيات أو routes أو API shapes أو Business Rules أو نصوص خارج مفاتيح i18n · تعديل عقد/جرد/بطاقة (التغيير يُرفع Decision Request) · **قاعدة الدسترة:** ما يخص شاشةً لا يعدّل النظام العام؛ وما يلزم النظامَ يذهب لمصدره الحاكم أولاً. **كل «Fixed/تم» من أداة = ‏Claimed حتى أدلة البوابة** (‏claimed ≠ published).

## (ز) دلالات البيانات
الافتراض **pessimistic** (الكتابة تُقر من الخادم قبل انعكاسها) · ‏**optimistic** استثناء يُعلَن في عقد الشاشة مع مسار تراجع صريح · نزاع الإصدار = ‏S20 ‏(version-check عند الحفظ؛ عرض النسختين وقرار المستخدم) · ‏validation خادمية المرجع والواجهة مرآة (`VISIBILITY_RULES` كما هي) · لا offline-write في v1 (‏S16 عرضٌ وإعادة محاولة فقط).

## (ح) جدول تغطية §18 بنداً-ببند (EC-4 — صفر بند بلا موضع)
| بند §18 | الموضع الملزم |
|---|---|
| تصنيف أنواع الشاشات | عمود `type` القائم + عمود `archetype` ‏v1.4 + ‏§ب |
| شاشة جديدة مقابل Tab/Drawer/Dialog | ‏`INTERACTION_MODEL §1–§4` + ‏§ج-1/2 |
| التنقل/المسارات/الرجوع/Deep-Link | ‏`INTERACTION_MODEL §7` + الجرد (route) + ‏§ج-3 |
| ربط الشاشة بالكيانات/الأفعال/الصلاحيات/التدقيق/API | جدول الجرد B + عقد الشاشة §2/§7 (روابط عقدية تتصلب مع نشوء العقود) |
| معرفات ثابتة لا أسماء | ‏`UI_FIELD_NAMING` + ‏screen_id بالجرد + ‏§ج-4 (الهوية) |
| حالات الشاشة القياسية | ‏`UI_COMPONENT_STATES` ‏S1–S15 + دلتا S16–S20 ‏(§د) |
| ‏Action Bar/جداول/بحث/نماذج/تأكيدات | ‏`UI_ACTION_BUTTON_MODEL` + ‏`INTERACTION_MODEL §4/§8` + بطاقات المكونات |
| RTL/i18n/Light-Dark/Responsive/a11y | ‏`DESIGN_SYSTEM §§9–11` + الوراثة العامة في §هـ (صيغة قابلة للاختبار) |
| مصدر البيانات/validation/optimistic/التعارضات | ‏`VISIBILITY_RULES` + ‏§ز + ‏S19/S20 |
| حدود حرية أداة التوليد | ‏§و + ‏`ROCKET_OPERATING_MODEL` |
| معايير قبول قابلة للاختبار لكل نمط | ‏§هـ (جديد صافٍ) |
| ‏Screen Contract موحد + جرد مركزي | ‏`contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` + الجرد v1.4 (‏contract_status/ref) |
| معيار تنفيذ المراحل (§18-د) | ‏`methodology/PHASE_EXECUTION_STANDARD.md` ‏(E-1/E-2) |
| حدود الـ Coding Agent (§18-هـ) | ‏`methodology/agent-execution-model.md` ‏v2.0 §§12–17 |

**Related:** `UI_SCREEN_INVENTORY.md` · `UI_COMPONENT_STATES.md` · `UI_INTERACTION_MODEL.md` · `../contracts/screens/SCREEN_CONTRACT_TEMPLATE.md` · `../contracts/identity/RECORD_IDENTITY.md` · `../methodology/ROCKET_OPERATING_MODEL.md` · `../AUTHORITY.md` · `../decisions/adr/ADR-0031-primary-ui-client-nextjs-client-only-rocket.md`
