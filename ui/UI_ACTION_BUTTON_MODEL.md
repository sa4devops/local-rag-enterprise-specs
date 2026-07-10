# UI_ACTION_BUTTON_MODEL.md — عقد الفعل المحكوم (Governed Action Contract)

> **Version:** 1.1 — (Δ v0.8: +§2.1 متغيّر العرض «inline message action» — عرضي فقط) · **Date:** 2026-07-10 (الأصل 2026-07-06) · **الموضع الهدف:** `ui/UI_ACTION_BUTTON_MODEL.md`
> **المراجع الحاكمة:** Phase 3 FR-3.5 (Action Registry — أثر معلن فقط) · Phase 4 (تصنيف/تصدير/SoD) · Phase 6 (Validation fail-closed) · Phase 7 (HITL) · A-UX-1/2 · constitution م2/م3/م16.
> **الثابت:** «الزر» ليس عنصر UI — هو **عرضٌ لعقد فعل** مخزَّن في `admin.actions`. السطحان (Renderer وWorkspace) يعرضان **نفس العقد بنفس `action_id`**، والخادم وحده يقيّمه وينفّذه.

## 1) مخطط العقد (حقول التعريف في الـ Registry)
| الحقل | النوع/القيم | إلزامي | مصدر الحقيقة | ملاحظات |
|---|---|---|---|---|
| `action_id` | dot.notation فريد (مثل record.create) | ✔ | Registry | ASCII؛ يظهر في التدقيق والـ API |
| `label_ar` / `label_en` | نص i18n | ✔ | Registry | لا نصوص مضمّنة في الواجهة |
| `icon` | رمز من نظام التصميم | — | Registry | دلالي لا زخرفي |
| `surface` | both \| renderer \| workspace \| console | ✔ | Registry | أفعال **الإعداد الإداري = console** حصراً (§7) |
| `target` | entity/screen/workflow/connector-tool | ✔ | Registry | ما الذي يعمل عليه الفعل |
| `permission` | معرّف صلاحية dot.notation | ✔ | PermissionAPI | **الخادم الحكم**؛ الواجهة تشذيب فقط |
| `required_inputs` | قائمة حقول (مرجعها field_definitions) | ✔ عند وجود مدخلات | Metadata Registry | نفس schema الـ Renderer — مصدر بطاقة المعاينة (A-UX-4) |
| `validation` | مرجع مجموعات تحقق معلنة | ✔ | محرك تحقق الخادم | لا تعبيرات كود حرة |
| `confirmation` | none \| simple \| typed \| dual | ✔ | Registry (مشتق من risk) | typed/dual للحرِج (OD-AB-3) |
| `approval_required` | none \| policy-ref (مصفوفة P3/P4) \| hitl (P7) | ✔ | سياسات الاعتماد | التنفيذ **بعد** القرار فقط |
| `effect` | **معلن**: api_operation \| workflow.transition \| notify \| open | ✔ | Registry | لا «كود حر» أبداً (P3) |
| `backend_operation` | اسم عملية API (مثل POST records.{entity}) | ✔ عند effect=api | عقد OpenAPI | تنفيذ idempotent بمفتاح للبطاقات |
| `audit_event` | UPPER_SNAKE (+حقول الحمولة) | ✔ | كتالوج §11 | يشمل proposal→execution كسلسلة correlation |
| `visible_when` | شروط سياق معلنة (حالة السجل/الدور/العلَم) | ✔ | تقييم خادمي | غير المرئي لا يُرسَل للواجهة أصلاً |
| `disabled_when` | شروط معلنة + **سبب i18n** | — | تقييم خادمي | المعطَّل يظهر بسبب (tooltip) — شفافية دون تسريب سياسات |
| `risk_level` | low \| medium \| high \| critical | ✔ | Registry | يقود التأكيد/الاعتماد/إسهاب التدقيق (§4) |
| `data_classification` | يرث **الأشد** من الهدف والفعل | ✔ (محسوب) | P4 | يقيّد التصدير/العرض ويُظهر الشارة على البطاقة |
| `rollback_supported` | true(+`undo_action_id`+نافذة) \| false | ✔ | Registry | false ⇒ سطر «لا يمكن التراجع» في المعاينة (§5) |
| `success_msg` / `failure_map` | i18n + خريطة error_code→رسالة | ✔ | Error Catalog | كل فشل يحمل error_code + request_id |

## 2) دورة حياة الزر وقت التشغيل (على السطحين)
`HIDDEN` (فشل visible_when/الصلاحية — لا يصل للمتصفح) → `VISIBLE_ENABLED` أو `VISIBLE_DISABLED(+سبب)` → عند النقر/الاقتراح: `PREVIEW` (بطاقة/نافذة من required_inputs) → `VALIDATED` خادمياً → `CONFIRMING` (حسب confirmation) → `PENDING_APPROVAL` (إن لزم — بند في queue.approvals/HITL) → `EXECUTING` → `SUCCEEDED` (+`UNDO_WINDOW` إن مدعوماً) أو `FAILED(+error_code)`.
**في الـ Renderer:** المعاينة نافذة تأكيد فوق الشاشة. **في الـ Workspace:** المعاينة هي `card.action_preview` نفسها — نفس الحالات حرفياً (خريطة S3–S9 في نموذج الـ Workspace).

### 2.1) متغيّر العرض «inline message action» — (Δ v0.8 · عرضي فقط · معتمد بقرار SA 2026-07-10)
**التعريف:** طريقة عرض مضغوطة للزر داخل رسائل **وضع المحادثة** في `ws.main` (OD-WS-4 — نموذج الـ Workspace §14): صف أزرار مصغّرة (أيقونة دلالية + label i18n) بذيل رسالة المساعد بدل بطاقة كاملة.
**القاعدة القطعية — لا عقد جديد ولا حقل جديد:** هذا **متغيّر عرض (presentational variant) فقط**؛ الزر يعرض **نفس عقد الفعل** بحقوله الـ13+ (§1) حرفياً، ويمر **بنفس دورة الحياة** (§2) **ونفس ترتيب التقييم الخادمي** (§3) دون أي اختصار: النقر يفتح المعاينة (`card.action_preview` أو نافذة التأكيد حسب risk/confirmation) — **لا تنفيذ مباشر من النقر إطلاقاً**.
**أحكام العرض:** يلتزم حدود الإظهار التدريجي (≤3 أزرار ظاهرة والباقي خلف «⋯») · HIDDEN-SERVER يسري كما هو (غير المخوَّل لا يستقبل الزر) · `VISIBLE_DISABLED` يظهر بسببه المقتضب · شارات المخاطر/التصنيف تُعرض مصغّرةً عند مستوى ≥ medium · أفعال `surface=console` لا تُعرض بهذا المتغيّر (قاعدة §7 كما هي).

## 3) ترتيب التقييم (الخادم مرجع؛ الواجهة مرآة)
visible_when → permission → disabled_when → validation(required_inputs) → **إعادة تحقق حية للسياق** (نسخة السجل/السياسة — م16) → confirmation → approval routing → execute(effect) → audit (سلسلة كاملة). أي محاولة استدعاء `backend_operation` مباشرة تخضع لنفس السلسلة — **لا مسار واجهة مميز**.

## 4) دلالات `risk_level` (أثر موحّد عبر النظام)
| المستوى | التأكيد | الاعتماد الافتراضي | التدقيق | أمثلة |
|---|---|---|---|---|
| low | none/simple | لا | قياسي | record.search · source.open |
| medium | simple | حسب المصفوفة | قياسي+ | record.create/update · task.create |
| high | typed | غالباً نعم | مُسهَب (قبل/بعد) | record.delete · workflow.approve · user.disable |
| critical | dual (+فاصل زمني قصير) | نعم + HITL/مزدوج | مُسهَب + إشعار مراقبة | connector.tool.act الكاتب · safe_mode.enter |

`data_classification` يرفع المتطلبات تلقائياً (فعل medium على بيانات Secret يُعامل high على الأقل)، وأفعال التصدير محكومة بسياسة P4 دائماً.

## 5) دلالات التراجع
`rollback_supported=true`: زر «تراجع» في `card.result` خلال النافذة، ينفّذ `undo_action_id` بعقده الكامل (صلاحية/تدقيق تعويضي UNDO_*) — **التراجع فعلٌ محكوم لا زر سحري**. `false`: المعاينة تتضمن تحذير اللارجعة، والحرِج منه يرفع التأكيد درجة.

## 6) أمثلة عقود (قيم مختصرة — المرجع التفصيلي عند بناء الـ Registry)
### 6.a أفعال المستخدم الأساسية
| action_id | permission | inputs/validation | confirm | approval | effect/backend | audit | risk | rollback |
|---|---|---|---|---|---|---|---|---|
| record.create | records.{e}.create | schema الكيان كاملاً | simple | حسب نوع الكيان | api: create | RECORD_CREATED | med | نعم (حذف ناعم خلال نافذة) |
| record.update | records.{e}.update | الحقول المتغيرة + cross-field | simple | حسب الحقول الحساسة | api: update | RECORD_UPDATED(old/new) | med | نعم (نسخة سابقة) |
| record.delete | records.{e}.delete | سبب إلزامي | **typed** | غالباً نعم | api: soft-delete | RECORD_DELETED | high | نعم (restore) |
| record.search | records.{e}.read | فلتر معلن | none | لا | api: query (RLS) | — (قياسي) | low | — |
| file.ingest | files.upload (+نطاق) | ملف + تصنيف موروث | simple | لا | api: ingest→pipeline P5 | FILE_UPLOADED | med | لا (نسخ جديدة بدلاً) |
| report.generate | reports.generate | قالب + نطاق | simple | اعتماد **التقرير** لاحقاً لا التوليد | async job (P6) | REPORT_SECTION_GENERATED | med | — (نسخ) |
| workflow.submit | wf.{id}.submit | مدخلات الانتقال | simple | يفتح بند اعتماد | workflow.transition | INSTANCE_TRANSITIONED | med | حسب التعريف |
| workflow.approve | approvals.decide (SoD: ≠ المُقدِّم) | تعليق عند الرفض | typed | هو ذاته القرار | workflow.transition | APPROVAL_DECIDED | high | لا |
| task.create | tasks.create | عنوان/مكلَّف/استحقاق | none | لا | api: create | TASK_CREATED | low | نعم (إلغاء) |
| source.open | وفق تصنيف المصدر | — | none | لا | open (سياق) | ENTITY/DOC_VIEWED للحساس | low | — |

### 6.b أفعال إدارية وتكاملية (surface=console أو HITL)
| action_id | permission | confirm | approval | effect | audit | risk | ملاحظات |
|---|---|---|---|---|---|---|---|
| user.disable | admin.users.manage | typed | حسب السياسة | api | USER_DISABLED | high | console فقط |
| role.assign | admin.users.manage | simple | SoD يفحص التعارض | api | ROLE_ASSIGNED | med | فشل sod ⇒ SOD_VIOLATION_BLOCKED |
| migration.approve | admin.migrations.approve (≠المقترِح) | typed | هو القرار | api: approve→apply | MIGRATION_APPROVED/APPLIED | critical | بوابة P1 |
| capability.binding_change | admin.models.manage | simple | **نعم في الإنتاج** | api | CAPABILITY_BINDING_CHANGED | high | يعرض خطة إعادة الفهرسة |
| connector.tool.read | صلاحية المنصة ∩ الحساب المربوط | none | لا | api عبر adapter | INVOCATION_EXECUTED | low/med | نتيجة موسومة «نظام: X» |
| connector.tool.act | كما فوق | typed | **HITL إلزامي** (معاينة payload) | api بعد الموافقة | INVOCATION_APPROVED/EXECUTED | high/critical | P7 FR-7.6 |
| provider.test_connection | admin.models.manage | none | لا | api (بلا كشف endpoint) | PROVIDER_TESTED | low | نتيجة نجاح/فشل فقط — D9 |
| feature.disable | admin.features.manage | typed | حسب الأثر | api (+dependency impact) | FEATURE_DISABLED | high | A10 يرفضها الخادم دائماً |

### 6.c أفعال التشغيل والمقارنة والتصعيد (Δ v0.6 — الأفعال المعتمدة: run · escalate · compare)
| action_id | permission | inputs/validation | confirm | approval | effect/backend | audit | risk | rollback |
|---|---|---|---|---|---|---|---|---|
| run.start | runs.start + صلاحية التعريف | definition_ref + معاملات معلنة | simple/**typed** بخطورة التعريف | بوابات داخل التعريف | api: runs_start ⇦ POST /api/v1/runs | RUN_STARTED | med/high | لا (الإلغاء بديلاً) |
| run.cancel | runs.cancel (مالك/نطاق) | سبب اختياري | **typed** | لا | api: runs_cancel ⇦ POST /api/v1/runs/{id}/cancel | RUN_CANCELLED | med | — |
| run.retry | runs.retry | — (يرث معاملات الأصل) | typed عند أثر act | كما التعريف | api: runs_retry ⇦ POST /api/v1/runs/{id}/retry | RUN_RETRIED | med/high | — |
| run.retry_step | runs.retry | step_ref | typed عند أثر act؛ **HITL يُعاد** لغير القابلة للإعادة | كما التعريف | api: runs_retry_step ⇦ POST /api/v1/runs/{id}/retry-step | RUN_RETRIED(from_step) | med/high | — |
| approval.escalate | approvals.escalate (SoD: ≠ المقدِّم) | تعليق إلزامي | **typed** | يرفع البند لمستوى أعلى بالمصفوفة | api: approvals_escalate ⇦ POST /api/v1/approvals/{id}/escalate | APPROVAL_ESCALATED | high | لا |
| version.compare | runs.read أو *.view للهدف | مرجعا المقارنة | none (قراءة) | لا | open: drawer diff | — | low | — |

## 7) الحوكمة والتسجيل
تعريف/تعديل العقود من `admin.actions` فقط، **بأثر معلن من كتالوج effects** (لا كود)، مع versioning وأحداث ACTION_DEFINED/CHANGED، ومحاكاة «مَن سيرى هذا الزر؟» قبل التفعيل (P4 simulator). أفعال الإعداد الإداري تُقيَّد `surface=console` عمداً: سطوح رسمية بأدوات محاكاة وSoD — الدردشة تستعلم ولا تُعيد تشكيل النظام.

## 8) حواف مقفلة
تعدد التحديد (bulk): **مؤجل** — العقد v1 مفرد الهدف؛ الجماعي لاحقاً بعقد multiplicity + معاينة مجمعة + تأكيد أشد (OD-AB-2). بطاقة قديمة/تعارض تزامني ⇒ إعادة التحقق الحية ترفض وتطلب «تحديث المعاينة». انقطاع أثناء EXECUTING ⇒ idempotency-key يمنع الازدواج وبطاقة الحالة تُستكمل من السجل.

## 9) Open Decisions
| OD | الموضوع | التوصية |
|---|---|---|
| OD-AB-1 | نافذة التراجع الافتراضية | معطّلة افتراضاً؛ تُفعَّل لكل عقد صراحة بمدة config |
| OD-AB-2 | نطاق bulk actions | خارج v1؛ تصميم مصغّر بعد P4 |
| OD-AB-3 | صياغة التأكيد المكتوب | موحَّدة مع OD-WS-1 — تُحسم في Clarify تفعيل P6 |
| OD-AB-4 | template.create («حفظ كقالب») | **Optional غير معتمد بقرار المالك 2026-07-08** — لا يدخل الكتالوج ولا العقود إلا بقرار صريح لاحق (مرجعه OD-TPL-1 في UI_RUN_EXECUTION_MODEL) |
