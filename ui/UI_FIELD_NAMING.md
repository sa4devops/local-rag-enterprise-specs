# UI_FIELD_NAMING.md — نظام التسمية الصارم (Identifiers &amp; Naming Convention)

> **Version:** 1.0 — Proposed · **Date:** 2026-07-06 · **الموضع الهدف:** `ui/UI_FIELD_NAMING.md`
> **المراجع الحاكمة:** constitution م18 (ASCII) · coding-standards §6 · UI_ACTION_BUTTON_MODEL (العقد) · UI_SCREEN_INVENTORY (الاصطلاح المطبَّق فعلاً).
> **المبدأ:** المعرّف التقني ASCII ثابت لا يُعاد تسميته بعد الإصدار (التغيير = نسخة جديدة)؛ العربية/الإنجليزية **labels** عبر i18n فقط. **معرّفٌ واحد لمعنى واحد** — ولا خلط بين طبقات التسمية الثماني أدناه.

## 1) الأنواع الثمانية — القاعدة والنمط
| النوع | الاصطلاح | النمط | نطاق التفرد | أمثلة من النظام | أمثلة خاطئة (ممنوعة) |
|---|---|---|---|---|---|
| `screen_id` | dot.notation صغير | `{area}.{screen}` | فريد عالمياً | auth.login · ws.main · run.form · admin.record_types · queue.approval_detail | AdminUsers · شاشة_الدخول · admin-users |
| `route` | kebab-case مسار URL | `/{segment}/…/{param}` | فريد عالمياً | /workspace · /me/approvals/{id} · /admin/metadata/screens · /app/{entity}/{id} | /Admin/Users · /مستخدمين · /adminUsers |
| `action_id` | dot.notation | `{noun}.{verb}` أو `{noun}.{sub}.{verb}` — الفعل من **كتالوج أفعال مغلق** (§5) | فريد في Action Registry | record.create · workflow.approve · migration.apply · connector.tool.act · safe_mode.enter | createRecord · record_create · POST /records (**هذا endpoint لا action**) |
| `permission` | dot.notation | `{resource}[.{scope}].{operation}` | فريد في Permission Registry | records.{entity}.create · admin.users.manage · approvals.decide · audit.view | can_create · RECORD.CREATE · record.create (**التباس مع action**) |
| `api_operation` | **operationId** بـ snake_case + مسار REST kebab/جمع | operationId: `{resource}_{verb}` · المسار: `/api/v1/{resources}/…` | فريد في OpenAPI | records_create ⇦ POST /api/v1/records/{entity} · migrations_approve ⇦ POST /api/v1/migrations/{id}/approve | record.create كـ endpoint · /api/createRecord |
| `audit_event` | UPPER_SNAKE_CASE | `{SUBJECT}_{VERB_PAST}` | فريد في كتالوج §11 | RECORD_CREATED · MIGRATION_APPROVED · SAFE_MODE_ENTERED · INVOCATION_EXECUTED | recordCreated · RECORD-CREATE · تم_الإنشاء |
| `field_name` | snake_case مفرد | لواحق دلالية: `_id` `_at` `_by` `is_/has_` `_count` `_level` | فريد داخل الكيان | employee_ref_number · org_unit_id · created_at · approved_by · is_active · classification_level | CreatedAt · empNo · رقم_الموظف · flag1 |
| `component_name` | مستويان | **توثيقي/Stitch:** dot.notation (`card.action_preview`) · **كودي (React لاحقاً):** PascalCase (`ActionPreviewCard`) | فريد في طبقته | panel.citations ⇄ CitationsPanel · ws.composer ⇄ WorkspaceComposer | actionpreviewcard · Card_Action |

## 2) الفصل الحاسم: action_id ≠ API endpoint
`action_id` = **عقد حوكمة** في الـ Registry (صلاحية/تحقق/تأكيد/اعتماد/تدقيق). `api_operation` = **عملية تنفيذ** يستدعيها العقد عبر `effect=api`. العلاقة **N→1 ممكنة** (أكثر من فعل يستدعي نفس العملية بسياسات مختلفة)، والعكس ممنوع (فعل واحد لا يستدعي عمليتين). الواجهة لا تنادي endpoints مباشرة لأفعال الأعمال — تنادي **تنفيذ الفعل** بمعرّفه، والخادم يحلّه إلى عمليته.

## 3) سلسلة الربط القياسية (أمثلة كاملة من النظام — المرجع عند أي التباس)
| المفهوم | screen (سطحاه) | route | action_id | permission | api_operation (endpoint) | audit_event | حقول أساسية | مكوّن |
|---|---|---|---|---|---|---|---|---|
| إنشاء سجل | run.form + بطاقة ws.main | /app/{entity}/new | record.create | records.{entity}.create | records_create ⇦ POST /api/v1/records/{entity} | RECORD_CREATED | حسب schema + created_at/by | card.action_preview / RecordForm |
| اعتماد ترحيل | admin.migrations | /admin/migrations | migration.approve | admin.migrations.approve | migrations_approve ⇦ POST /api/v1/migrations/{id}/approve | MIGRATION_APPROVED | proposal_id · risk_report · approved_by | MigrationReviewPanel |
| قرار اعتماد | queue.approval_detail | /me/approvals/{id} | workflow.approve / workflow.reject | approvals.decide | approvals_decide ⇦ POST /api/v1/approvals/{id}/decision | APPROVAL_DECIDED | decision · comment · decided_by/at | ApprovalDecisionBar |
| تغيير ربط قدرة | admin.capabilities | /admin/models/capabilities | capability.binding_change | admin.models.manage | capability_bindings_update ⇦ PUT /api/v1/capabilities/{cap}/binding | CAPABILITY_BINDING_CHANGED | capability · provider_ref · model_ref · fallback_ref | BindingEditor |
| فتح مصدر استشهاد | ws.main (لوحة) | — (فعل سياقي) | source.open | حسب تصنيف المصدر (records.{e}.read / files.read) | sources_resolve ⇦ GET /api/v1/sources/{ref} | DOC_VIEWED (للحساس) | source_ref · locator | panel.citations |
| بحث سجلات (كبير→Renderer) | ws.main → run.list | /app/{entity}?f=… | record.search | records.{entity}.read | records_query ⇦ GET /api/v1/records/{entity} | — | فلتر مُسلسل f | card.result / DataTable |
| تعطيل مستخدم | admin.user_detail | /admin/users/{id} | user.disable | admin.users.manage | users_disable ⇦ POST /api/v1/users/{id}/disable | USER_DISABLED | user_id · reason | UserStatusActions |
| فعل موصل كاتب | ws.main + queue.approvals (HITL) | — | connector.tool.act | صلاحية المنصة ∩ الحساب المربوط | invocations_execute ⇦ POST /api/v1/invocations | INVOCATION_APPROVED/EXECUTED | connector_id · tool_id · payload_masked · on_behalf_of | HitlPreviewDialog |

## 4) قواعد i18n وقواعد البيانات (الملاصقة للواجهة)
- **مفاتيح i18n:** dot.notation بفضاء الشاشة: `{screen_id}.{element}` — مثل `ws.main.composer_placeholder` · `admin.migrations.approve_confirm` · قيم الرسائل للأخطاء تُفهرس بـ `errors.{error_code}`. لا نص مضمّن في المكوّنات.
- **error_code:** UPPER_SNAKE بنطاق الوحدة: `RECORDS_VALIDATION_FAILED` · `PERM_DENIED` · `LLM_UNAVAILABLE` (كتالوج الأخطاء مصدره).
- **جداول DB:** snake_case جمع (`screen_definitions`, `workflow_instances`)؛ كيانات apps_db باسم الكيان ASCII من الـ Builder؛ الفهارس/المفاتيح باصطلاح coding-standards (خارج نطاق هذا الملف).
- **قيم Enum:** snake_case صغيرة (`pending_approval`, `rolled_back`) — عرضها العربي عبر i18n.

## 5) كتالوج الأفعال المغلق (v1 — أي فعل جديد يُضاف بقرار في الـ Registry)
create · update · delete · restore · search · open · view · export · submit · approve · reject · return · assign · revoke · grant · enable · disable · activate · rollback · generate · review · ingest · retry · cancel · link · renew · test · enter · exit · act · read · simulate · reorder · reclassify.
**ممنوع:** أفعال مركّبة (create_and_notify — الإشعار effect مرافق) · مرادفات (add/new/insert ⇒ create) · أفعال بلا فاعل واضح.

## 6) محظورات عامة
لا عربية/مسافات/شرطات في المعرّفات · لا camelCase في field_name · لا إعادة استخدام معرّف محذوف · لا اختصارات غامضة (`usr`, `tbl`) · لا خلط مفرد/جمع داخل الطبقة الواحدة · لا permission يبدأ بفعل UI (`click_`, `show_`).

## 7) الإنفاذ (حوكمة لا شرفية)
خط التوليد المحكوم (P1) يفحص الأنماط والكلمات المحجوزة والتصادم **قبل الاعتماد** · Action/Permission Registries ترفض المخالف بقاعدة معلنة · CI لاحقاً يفحص operationId/audit_event ضد الكتالوجات · أي استثناء ⇒ قرار موثَّق لا تجاوز صامت.

## 8) Open Decisions
| OD | الموضوع | التوصية |
|---|---|---|
| OD-NM-1 | إقفال قائمة كتالوج الأفعال v1 | القائمة في §5 تُثبَّت مع Clarify تفعيل P3 (مالك الـ Registry) |
| OD-NM-2 | بادئة إصدار الـ API | `/api/v1` ثابتة؛ كسر التوافق ⇒ v2 بقرار ADR |
