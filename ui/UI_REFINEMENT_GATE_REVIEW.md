# UI_REFINEMENT_GATE_REVIEW.md — بوابة فحص حزمة v0.5

> **Version:** 1.0 — Proposed (v0.5) · **Date:** 2026-07-07 · **الموضع الهدف:** `ui/UI_REFINEMENT_GATE_REVIEW.md`
> **الغرض:** بوابة قبول **إلزامية** قبل رفع ملفات v0.5 إلى `local-rag-enterprise-specs` وإصدار `v0.5-ui-interaction-visibility-refinement`.
> **علاقة بـ v0.4:** لا تُغني هذه البوابة عن `UI_GATE_REVIEW_CHECKLIST.md` (v0.4)؛ تُستكمل معها. أي بند ❌ في الأقسام A–H يمنع الرفع.

## A) الاكتمال (7 ملفات — بنيان فوق v0.4 لا استبداله)
- [ ] `ui/UI_INTERACTION_MODEL.md` موجود
- [ ] `ui/UI_VISIBILITY_RULES.md` موجود
- [ ] `ui/UI_PROGRESSIVE_DISCLOSURE.md` موجود
- [ ] `ui/UI_COMPONENT_STATES.md` موجود
- [ ] `ui/UI_SCREEN_BEHAVIOR_CARDS.md` موجود
- [ ] `ui/UI_STITCH_REFINED_PROMPTS.md` موجود
- [ ] `ui/UI_REFINEMENT_GATE_REVIEW.md` (هذا الملف) موجود
- [ ] الملفات الاثنا عشر من v0.4 **لم تُعدَّل ولم تُحذف** (بنيان لا استبدال)

## B) النقاء (لا كود — لا أوامر — لا أسرار)
- [ ] لا أسيجة كود (ثلاث علامات اقتباس مائلة متتالية) في أي ملف من ملفات v0.5 السبعة
- [ ] لا أسطر أوامر طرفية (أنماط: $ · sudo · pip · npm · pnpm · docker · git · bash · curl · wget)
- [ ] لا endpoints/secrets/tokens/مفاتيح في أي مثال
- [ ] أسماء ملفات ASCII بالكامل (المادة 18)
- [ ] لا صور/أصول منتجات خارجية مضمّنة داخل الحزمة

## C) الاتساق مع v0.3 و v0.4 (لا كسر للمعتمد — لا تغيير معماري)
- [ ] لا تغيير في ترتيب المراحل P0→P8
- [ ] لا إضافة/حذف من صلاحيات معتمدة، ولا محرك سياسات ثانٍ خارج PermissionAPI
- [ ] لا إعادة تعريف لـ Dual-Surface أو Action Layer أو Runtime Renderer أو Workspace-من-P6
- [ ] لا شاشة جديدة تُضاف خارج جرد v0.4 v1.1 (بطاقات الشاشات تعمل على الجرد القائم فقط)
- [ ] كل معرّف screen_id/action_id/permission/audit_event مذكور في v0.5 مطابق لـ v0.4 (لا تسمية جديدة)
- [ ] كل إحالات OD-* (IX/VZ/PD إضافةً لسابقاتها) مُعرَّفة داخل ملفات v0.5 نفسها

## D) عالج المشكلات التي دفعت لـ v0.5 (الأثر المرجو)
### D1) هل قلّلت الازدحام؟
- [ ] `UI_PROGRESSIVE_DISCLOSURE §3` منصوصة الحدود: ≤3 أزرار header · ≤5 شارات · ≤7 حقول/أعمدة · تبويب واحد نشط افتراضياً
- [ ] بطاقات الشاشات في `UI_SCREEN_BEHAVIOR_CARDS` تحدد لكل شاشة **افتراضياً يظهر** مقابل **مطويّ** صراحة
- [ ] `UI_STITCH_REFINED_PROMPTS §1.5` تُلصق قواعد الإظهار التدريجي في كل prompt

### D2) هل حدّدت الظهور والإخفاء؟
- [ ] `UI_VISIBILITY_RULES` يحوي الدرجات الأربع (HIDDEN-SERVER / HIDDEN-CLIENT / DISABLED-WITH-REASON / VISIBLE) وقاموس الوسوم الـ15
- [ ] «لاتماثل مقصود» منصوص: صمت للبيانات (RLS)، وضوح للأفعال (رفض مع سبب عام)
- [ ] `panel.audit` رأس التبويب مخفي كلياً لغير المخوّل — منصوص في IM/VZ/SBC/RP
- [ ] الحقول الحساسة تظهر «•••» + قفل — منصوص في كل ملف عملي

### D3) هل حدّدت التفاعل؟
- [ ] `UI_INTERACTION_MODEL §1` يعرّف الأسطح الستة بدقة (page/tab/drawer/modal/panel/inline) بلا التباس
- [ ] `§4` يقدّم مصفوفة حسم مُلزمة لكل حالة تفاعل شائعة
- [ ] قاعدة عدم التكرار: لا مضمون يُكرَّر في أكثر من سطح لنفس الغرض
- [ ] فتح شاشة إدارية من ws.main = تبويب متصفح جديد (لا يفقد الحوار)

### D4) هل منعت خروج Stitch عن السياق (الفشل الأصلي)؟
- [ ] `UI_STITCH_REFINED_PROMPTS §1.1 Project Identity Lock` مكتوب EN ومقفل الهوية
- [ ] القائمة السلبية الصريحة: لا city planning · لا municipal · لا marketing landing · لا public SaaS · لا شعارات · لا chatbot استهلاكي · لا low-code للمستخدم النهائي
- [ ] `§1.7 Forbidden Outputs` تُلصق **حرفياً في نهاية كل prompt** من الـ7 مجموعات
- [ ] كل prompt يذكر «static reference only — code will not be used»
- [ ] كل prompt يذكر «fictitious Arabic enterprise sample data»
- [ ] **Tool-Agnostic Prompt Rule** (`§1.8`) مُدرجة في الديباجة وتُلصق قبل كل prompt
- [ ] Tool names are interpreted as workflow tools only, not product features, branding, UI labels, or mandatory dependencies
- [ ] Prompts remain usable in any design generation tool, not only Google Stitch

### D5) هل الحالات المطلوبة كافية للتصميم الرصين؟
- [ ] `UI_COMPONENT_STATES` يعرّف الحالات الـ15 موحّدةً ويطبّقها على 13 مكوّناً
- [ ] كل مكوّن يحدد N/A صراحة للحالات غير المنطبقة (لتجنّب اختراع تصاميم)
- [ ] كل prompt في `UI_STITCH_REFINED_PROMPTS` يذكر الحد الأدنى الست: default · loading · empty · error · permission-denied · disabled

## E) حفظ الثوابت الحاكمة
### E1) Dual-Surface
- [ ] كل عملية أعمال لها سطحان (ws-card + renderer) بنفس `action_id` — منصوص في IM/PD/SBC/RP
- [ ] بطاقات الشاشات لـ `run.*` و`ws.main` تُظهر التقاطع (المكافئ المحادثي/الحتمي)
- [ ] النتائج >10 صفوف تحوَّل إلى `run.list` بفلتر مُسلسل (منصوص في IM §5، PD §7)

### E2) Action Layer واحد
- [ ] كل زر/بطاقة فعل مربوطة بعقد `action_id` من Registry — لا تنفيذ مباشر
- [ ] بطاقات ws لا «تخترع» أفعالاً خارج الـ Registry
- [ ] تنفيذ فعل high/critical يمر بـ typed/dual + approval

### E3) الصلاحيات والتدقيق
- [ ] عمود `permissions` أو ما يعادله غير فارغ لكل بطاقة شاشة/مكوّن
- [ ] عمود `audit_events` أو ما يعادله مذكور حيث يوجد فعل
- [ ] `audit-visible` كحالة مستقلة موجودة في `UI_COMPONENT_STATES` لكل مكوّن يستحقها
- [ ] `admin.audit` بطاقتها تنص على «ضمن نطاق الناظر» + استثناء OD-VZ-3 المعلن

### E4) LLM يقترح ولا ينفّذ
- [ ] بطاقات ws لا تنفّذ من مخرَج النموذج مباشرة — دائماً proposal → preview → confirm → (approve) → execute
- [ ] بطاقة `card.refusal_evidence` (No-Guessing) موجودة كحالة أولى مصمَّمة، لا كخطأ

### E5) حدود D9 محفوظة
- [ ] لا endpoints/secrets/GPU في `admin.capabilities` أو أي بطاقة أخرى
- [ ] «اختبار الاتصال» يعرض chip نجاح/فشل فقط — لا تفاصيل مزوّد
- [ ] بطاقة `admin.connectors` تنص على عدم عرض أسرار
- [ ] أسطح Ops/config قراءة فقط بلا أزرار lifecycle

## F) اتساق التسمية والمصطلحات (يورث v0.4)
- [ ] كل `screen_id` مذكور موجود في جرد v0.4 v1.1
- [ ] كل `action_id` مذكور بصيغة dot.notation ومن كتالوج الأفعال المغلق (v0.4 §5)
- [ ] كل `audit_event` مذكور بصيغة UPPER_SNAKE_CASE
- [ ] عدم خلط `action_id` مع API endpoint
- [ ] المعرّفات LTR-isolated في النص العربي

## G) نطاق v0.5 (لا تجاوز)
- [ ] لا تصميم جديد للمعمارية — v0.5 قواعد تفاعل/ظهور/حالات فقط
- [ ] لا Phase جديدة — v0.5 لا يمس Phase Master Plan
- [ ] لا مكتبات أو dependencies جديدة مقترحة (الخط والأيقونات تبقى بوابتها OD-DS-2 من v0.4)
- [ ] لا تنفيذ ولا كود ولا terminal
- [ ] لا تعديل GitHub داخل هذه الحزمة

## H) خطة الرفع والإصدار (تُنفَّذ بعد Accept — بيد المالك حصراً)
- [ ] الوجهة: مجلد `ui/` في specs بجانب ملفات v0.4 (بلا حذف أو استبدال)
- [ ] commits مقترحة:
  - (1) `Add ui interaction and visibility rules` [INTERACTION_MODEL + VISIBILITY_RULES + PROGRESSIVE_DISCLOSURE]
  - (2) `Add ui component states and screen behavior cards` [COMPONENT_STATES + SCREEN_BEHAVIOR_CARDS]
  - (3) `Add refined stitch prompts and refinement gate` [STITCH_REFINED_PROMPTS + REFINEMENT_GATE_REVIEW]
  - (4) `Update package checklist, docs structure and handoff for ui refinement v0.5`
- [ ] التحديثات الوصفية المرافقة (commit 4):
  - `PACKAGE_CHECKLIST.md → v1.4` بصفوف ملفات v0.5 السبعة
  - `github-docs-structure.md` بإضافة إشارة إلى أن `ui/` تحوي الآن حزمتَي v0.4 + v0.5
  - `handoff/handoff.md` بإدخال **H-0005** (إنتاج حزمة UI Interaction & Visibility Refinement واعتمادها)
- [ ] إنشاء Release: **`v0.5-ui-interaction-visibility-refinement`** — Title: *UI Interaction &amp; Visibility Refinement Package v0.5* — **Pre-release** — الوصف: قواعد تفاعل وظهور وحالات مكوّنات وبطاقات سلوك شاشات و prompts محسّنة لـ Stitch؛ يبني فوق v0.4 ولا يستبدله؛ بلا كود وبلا تنفيذ وبلا تغيير معماري
- [ ] بعد الإصدار: تحديث `platform/docs/SPEC_SOURCE.md` إلى `v0.5-ui-interaction-visibility-refinement` **فقط** (المصدر الوحيد للرقم — لا تغيير آخر في platform، لا إصدار platform جديد)

## قرار البوابة
| النتيجة | ☐ Accept | ☐ Accept with minor edits | ☐ Reject |
|---|---|---|---|

| البند | الملف | الملاحظة | الإجراء المطلوب |
|---|---|---|---|
|  |  |  |  |

المراجِع: ____________ · التاريخ: ____________ · مرجع الجلسة/الفحص الآلي: ____________
