# ABSENCE-EVIDENCE-B1-RAR001 — B1 Commit 2

> **مخرج traceability/تحليلي غير حاكم** — لا سلطة موازية. حزمة أدلة غياب **قابلة لإعادة التنفيذ** لبنود RAR-001 المصنَّفة «دلتا حقيقية». كل حالة بمرساة HTML صريحة بأحرف صغيرة. **HEAD المنفَّذ عليه البحث:** `188ad379d04b07ca9e1b4eeee38dc68ecca29914`.
> **نطاق مشترك مستثنى من «الحاكم»:** `references/analysis-inputs/**` (مدخل غير حاكم) · `traceability/rar-reconciliation/**` (مخرجات B1) · `superseded/**` (تاريخي). **الأمر القياسي:** `grep -rInE "<terms>" . --include='*.md' | grep -viE 'references/analysis-inputs/|traceability/rar-reconciliation/|superseded/'`. النتيجة الصفرية تعني: لا مصدر حاكم نافذ يقنِّن البند عند HEAD أعلاه. غياب العثور **ليس إثباتاً وجودياً**؛ يُقرأ ضمن نطاق البحث المذكور فقط.

<a id="absence-b1-rar001-001"></a>
### ABSENCE-B1-RAR001-001
- **البند:** عقود Schedule وAutomation (ضمن «Contracts للأنواع الأربعة»، الصف #9). Task/Workflow لهما تغطية جزئية (`ui/UI_ACTION_BUTTON_MODEL.md:67` · `contracts/screens/admin.workflows.md:19`).
- **المصطلحات/المرادفات:** `schedule.` · `contracts/screens/schedule` · `Schedule Contract` · `automation.` · `Automation Contract`.
- **النطاق:** كل `.md` حاكم (contracts/ · ui/ · catalogs/ · decisions/ · phases/) عدا المستثنى.
- **الأمر:** `grep -rInE 'schedule\.(create|list)|contracts/screens/schedule|Schedule Contract' … ` و`… 'automation\.(create|list)|contracts/screens/automation|Automation Contract' …`
- **النتيجة:** **0** لكلٍّ. **لماذا لا يكفي الموجود:** task.create/admin.workflows يغطيان نوعين فقط؛ Schedule/Automation بلا عقد. ⇒ دلتا حقيقية → R3.

<a id="absence-b1-rar001-002"></a>
### ABSENCE-B1-RAR001-002
- **البند:** Lifecycles رسمية لـTask/Schedule/Automation (الصف #10). workflow lifecycle موجود (`contracts/screens/admin.workflows.md:22`).
- **المصطلحات:** `task lifecycle` · `schedule lifecycle` · `automation lifecycle` · `دورة حياة (مهمة/جدولة/أتمتة)`.
- **الأمر:** `grep -rInE 'lifecycle|دورة حياة' contracts/ ui/ | grep -iE 'task|schedule|automation'` (خارج المستثنى).
- **النتيجة:** **0** لدورات حياة رسمية لهذه الأنواع الثلاثة (الموجود يخص workflow/records). ⇒ دلتا حقيقية → R3.

<a id="absence-b1-rar001-003"></a>
### ABSENCE-B1-RAR001-003
- **البند:** API Operation Contracts للأنواع الأربعة (الصف #11). النمط العام معرَّف (`decisions/adr/ADR-0025-api-contract-rest-openapi-sse.md:7`) لكن لا عقود عمليات مُصنَّفة لكل نوع.
- **المصطلحات:** `API Operation Contract` · `api_operation` لكل نوع · `OpenAPI operation` لـtask/schedule/automation.
- **الأمر:** `grep -rInE 'API Operation Contract|api_operation' … | grep -iE 'task|schedule|automation'`.
- **النتيجة:** **0** عقود عمليات مخصّصة (الموجود: نمط ADR-0025 + أفعال UI متفرقة). ⇒ دلتا حقيقية → R3.

<a id="absence-b1-rar001-004"></a>
### ABSENCE-B1-RAR001-004
- **البند:** نموذج موارد موحّد أو فصل واضح بين الأنواع الأربعة (الصف #17).
- **المصطلحات:** `نموذج موارد موحد` · `unified resource model` · `Resource Model`.
- **الأمر:** `grep -rInE 'نموذج موارد موحد|unified resource model|Resource Model' …`.
- **النتيجة:** **0**. ⇒ دلتا حقيقية → R3.

<a id="absence-b1-rar001-005"></a>
### ABSENCE-B1-RAR001-005
- **البند:** Intent Interpretation Contract (الصف #19).
- **المصطلحات:** `Intent Interpretation` · `Intent Contract` · `intent_interpretation`.
- **الأمر:** `grep -rInE 'Intent Interpretation|Intent Contract' …`.
- **النتيجة:** **0**. ⇒ دلتا حقيقية → R3.

<a id="absence-b1-rar001-006"></a>
### ABSENCE-B1-RAR001-006
- **البند:** Resolution Contract للأشخاص/السجلات/الوحدات (الصف #20).
- **المصطلحات:** `Resolution Contract` · `resolution_contract`.
- **الأمر:** `grep -rInE 'Resolution Contract|resolution_contract' …`.
- **النتيجة:** **0**. ⇒ دلتا حقيقية → R3.

<a id="absence-b1-rar001-007"></a>
### ABSENCE-B1-RAR001-007
- **البند:** Recurrence (تكرار الجدولة) (الصف #24).
- **المصطلحات:** `Recurrence` · `RRULE` · `cron` · `تكرار`.
- **الأمر:** `grep -rInE 'Recurrence|RRULE|cron' …`.
- **النتيجة:** **0** حاكم. ⇒ دلتا حقيقية → R5.

<a id="absence-b1-rar001-008"></a>
### ABSENCE-B1-RAR001-008
- **البند:** Timezone في الجدولة (الصف #25).
- **المصطلحات:** `Timezone` · `time zone` · `منطقة زمنية` (في سياق جدولة/تشغيل).
- **الأمر:** `grep -rInE 'Timezone|time zone|منطقة زمنية' …`.
- **النتيجة:** **0** حاكم لسياسة توقيت الجدولة. ⇒ دلتا حقيقية → R5.

<a id="absence-b1-rar001-009"></a>
### ABSENCE-B1-RAR001-009
- **البند:** Business Calendar (الصف #26).
- **المصطلحات:** `Business Calendar` · `business_calendar` · `تقويم العمل` · `holidays`.
- **الأمر:** `grep -rInE 'Business Calendar|business_calendar|تقويم العمل' …`.
- **النتيجة:** **0**. ⇒ دلتا حقيقية → R5.

<a id="absence-b1-rar001-010"></a>
### ABSENCE-B1-RAR001-010
- **البند:** Event Trigger abstraction (الصف #27).
- **المصطلحات:** `Event Trigger` · `event_trigger` · `Trigger abstraction`.
- **الأمر:** `grep -rInE 'Event Trigger|event_trigger|Trigger abstraction' …`.
- **النتيجة:** **0** حاكم (جاهزية Event Contracts مسارها R10). ⇒ دلتا حقيقية → R10.

<a id="absence-b1-rar001-011"></a>
### ABSENCE-B1-RAR001-011
- **البند:** Audit Event Catalogue **موحّد** (الصف #35). حقل `audit_event` معرَّف لكل عقد (`ui/UI_FIELD_NAMING.md:23`)، لكن لا كتالوج أحداث تدقيق مُجمَّع.
- **المصطلحات:** `Audit Event Catalog` · `كتالوج أحداث التدقيق` · `audit event catalogue`.
- **الأمر:** `grep -rInE 'Audit Event Catalog|كتالوج أحداث' …`.
- **النتيجة:** **0** لكتالوج موحّد (الموجود: أحداث لكل شاشة/عقد). ⇒ دلتا حقيقية → R3.

## أدلة غياب أسئلة §14 المفتوحة (تصحيح Commit 2 — الصفوف [39][40][41][42][44][45][46][49][53])
> نُفِّذت البحوث عند HEAD `9450a3b39457c116069f4ce26c29ac1cb0c71f82`. أثبتت أن **المستودع الحاكم لا يحسم** كل سؤال (Path A)؛ لم يظهر تعارض حاكم فعلي (Path B) لأيٍّ منها. **لا يُستشهد بـ`references/analysis-inputs/**` في العمود الرابع** — بديله مرساة الغياب أدناه.

<a id="absence-b1-rar001-012"></a>
### ABSENCE-B1-RAR001-012
- **البند [39]:** هل Task مورد مستقل أم تجسيد مبسط لـWorkflow؟ (تعريف علاقة Task↔Workflow).
- **النطاق/المصطلحات:** `Task vs Workflow` · `مورد مستقل` · `projection/تجسيد` · `علاقة Task`. **الأمر:** `grep -rInE 'Task.*(مورد مستقل|projection|تجسيد)|Task vs Workflow|علاقة Task' . --include='*.md' | grep -viE 'references/analysis-inputs/|traceability/rar-reconciliation/|superseded/'`.
- **النتيجة:** **0** حاكم. task.create وadmin.workflows يتعايشان دون نصٍّ يحسم استقلالية Task عن Workflow. **⇒ لا حسم حاكم؛ التزام تصميمي صالح غير مقنَّن ⇒ دلتا حقيقية → R3.**

<a id="absence-b1-rar001-013"></a>
### ABSENCE-B1-RAR001-013
- **البند [40]:** الحد بين Schedule وAutomation Trigger. **المصطلحات:** `Schedule Automation` · `Automation Trigger boundary` · `حد Trigger`. **الأمر:** `grep -rInE 'Schedule.*Automation|حد.*Trigger|Automation Trigger boundary' … `.
- **النتيجة:** **0** حاكم (Schedule/Automation غير مقنَّنين أصلاً — قارن ABSENCE-001). **⇒ دلتا حقيقية → R3.**

<a id="absence-b1-rar001-014"></a>
### ABSENCE-B1-RAR001-014
- **البند [41]:** أين تخزَّن صياغة المستخدم الأصلية؟ **المصطلحات:** `صياغة المستخدم الأصلية` · `original utterance` · `user phrasing` · `raw user input`. **الأمر:** `grep -rInE 'صياغة المستخدم الأصلية|original utterance|user phrasing|raw user input' …`.
- **النتيجة:** **0** حاكم. **⇒ متطلب تخزين صالح غير مقنَّن ⇒ دلتا حقيقية → R3.**

<a id="absence-b1-rar001-015"></a>
### ABSENCE-B1-RAR001-015
- **البند [42]:** تخزين خطة LLM الوسيطة (الجزء الذرّي غير «منع اعتبارها حقيقة» المقنَّن بم1). **المصطلحات:** `خطة LLM` · `LLM plan` · `intermediate plan` · `الخطة الوسيطة`. **الأمر:** `grep -rInE 'خطة LLM|LLM plan|intermediate plan|الخطة الوسيطة' …`.
- **النتيجة:** **0** حاكم لآلية التخزين. **⇒ دلتا حقيقية → R3.**

<a id="absence-b1-rar001-016"></a>
### ABSENCE-B1-RAR001-016
- **البند [44]:** نموذج التحقق Deterministic لمخرجات LLM. **المصطلحات:** `Deterministic verification` · `نموذج التحقق` · `deterministic check`. **الأمر:** `grep -rInE 'Deterministic verification|نموذج التحقق|deterministic check' …`.
- **النتيجة:** **0** حاكم (م1 يمنع اعتبار LLM مصدر حقيقة لكنه لا يعرّف نموذج تحقق حتمياً). **⇒ دلتا حقيقية → R3.**

<a id="absence-b1-rar001-017"></a>
### ABSENCE-B1-RAR001-017
- **البند [45]:** ربط Preview بنسخة العقود المتحقَّق عليها. **المصطلحات:** `Preview نسخة العقود` · `preview contract version` · `contract version pin`. **الأمر:** `grep -rInE 'Preview.*نسخة العقود|preview.*contract version|contract version pin' …`.
- **النتيجة:** **0** حاكم (توجد بطاقة معاينة لكن بلا ربط بنسخة عقد). **⇒ دلتا حقيقية → R3.**

<a id="absence-b1-rar001-018"></a>
### ABSENCE-B1-RAR001-018
- **البند [46]:** سياسة «كل تعديل ينتج Version جديداً». **المصطلحات:** `كل تعديل Version` · `version per edit` · `version-on-edit`. **الأمر:** `grep -rInE 'كل تعديل.*Version|version per edit|version-on-edit' …`.
- **النتيجة:** **0** حاكم (ADR-0032 يعرّف التخزين الهجين/UUIDv7 لا سياسة versioning-per-edit). **⇒ دلتا حقيقية → R3.**

<a id="absence-b1-rar001-019"></a>
### ABSENCE-B1-RAR001-019
- **البند [49]:** Dry Run للمهام/الأتمتة قبل التشغيل الحي. **المصطلحات:** `Dry Run` · `dry-run` · `تشغيل تجريبي`. **الأمر:** `grep -rInE 'Dry Run|dry-run|تشغيل تجريبي' …`.
- **النتيجة:** المطابقة الوحيدة `phases/phase-0-foundation-full-stack-skeleton.md:93` تخص **offline-install dry-run** (مفهوم بناء/تشغيل مختلف) لا Dry-Run تنفيذ الأتمتة. **⇒ لا حسم حاكم لـDry-Run الأتمتة ⇒ دلتا حقيقية → R3.**

<a id="absence-b1-rar001-020"></a>
### ABSENCE-B1-RAR001-020
- **البند [53]:** تمثيل «عندما يكتمل الجميع» بشكل قابل للاختبار (دلالة join). **المصطلحات:** `عندما يكتمل الجميع` · `all complete` · `join semantics` · `wait for all`. **الأمر:** `grep -rInE 'عندما يكتمل الجميع|all complete|join semantics|wait for all' …`.
- **النتيجة:** **0** حاكم (admin.workflows جدول حالات/انتقالات لكن بلا دلالة join «all-of» قابلة للاختبار). **⇒ دلتا حقيقية → R5.**

---
**ملاحظات إنفاذ:** 20 مرساة صريحة فريدة (`absence-b1-rar001-001..020`) · كل مرساة تخدم بنداً واحداً · لا إعادة استخدام مرساة واحدة لعدة صفوف · كل استشهاد في `RECONCILIATION-RAR-001.md` يحلّ إلى مرساة موجودة هنا · لا مرجع مكسور. **قاعدة (تصحيح §4):** العمود الرابع لا يستشهد بـ`references/analysis-inputs/**` إطلاقاً — دليل حاكم أو مرساة غياب أو سلطتان متعارضتان فقط.
