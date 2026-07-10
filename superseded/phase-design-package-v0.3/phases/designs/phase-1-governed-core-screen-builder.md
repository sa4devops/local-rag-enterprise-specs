# Phase 1 — Governed Core + Screen Builder

> **Version:** 1.0 — Proposed (تصبح **Accepted for Design** باعتماد v0.3) · **Date:** 2026-07-06 · **Authority عند الاعتماد:** المرتبة 6
> **Inherits:** Common Phase Baseline — PHASE_MASTER_PLAN §4 (الثوابت/NFRs/Security/Audit/Testing/DoD المشتركة لا تُكرَّر هنا).
> **Predecessor:** Phase 0 منفَّذة بكامل DoD. **بطاقات المهام تُولَّد عند التفعيل** (جلسة Tasks) — هذا التصميم حتى مستوى Epics.

## 1. Purpose
إثبات جوهر المشروع end-to-end تحت الحوكمة (Walking Skeleton): هوية وتنظيم وصلاحيات مُنفَّذة default-deny، وAudit spine كامل، ودورة **توليد شاشة محكومة** (تعريف→migration→فحص→اعتماد→تطبيق→توثيق→CRUD) عبر Admin shell عربي RTL — بلا أي ذكاء اصطناعي.

## 2. Scope
Local Auth عبر IdentityProvider (IdP-adapter جاهز) · Organization (قطاعات/إدارات/عضوية) · Permission spine (أدوار أساسية + فحص على screen/action/record الأساسي، default-deny) · Metadata Registry (screens/fields تعريفاً) · خط التوليد المحكوم لشريحة رأسية واحدة كاملة · Records CRUD أساسي على الكيانات المولّدة · **Audit spine كامل** (الكتالوج §11 لأحداث هذه الوحدات) · Admin shell (ar/en، RTL، تنقّل حسب الصلاحية) · Admin Log Viewer v1 (قراءة JSON logs + Audit بقناع أسرار).

## 3. Out of Scope
RAG/فهرسة/وسائط/LLM بأي شكل · Workflows/Approvals-كوحدة (اعتماد الـ migration هنا آلية مبسطة داخل خط التوليد) · RLS/FLS الكاملان (P2) · ABAC/ReBAC/التصنيف (P4) · أنواع الحقول المتقدمة (P2) · Entity Profile · تكاملات · تقارير · متجر.

## 4. Required Inputs
Phase 0 DoD مستوفى · specs release المعتمد (v0.3) · صفوف ترخيص الستاك مُقرّة · هذا التصميم Accepted · بطاقات مهام مولّدة عند التفعيل.

## 5. Expected Outputs
نظام يدخل إليه مستخدم محلي، يرى ما تسمح به صلاحياته فقط، وأدمن يعرّف شاشة فتتولّد migration تُفحص وتُعتمد وتُطبَّق وتُوثَّق، ثم CRUD مدقَّق عليها — مع سجل audit كامل وLog Viewer.

## 6. Functional Requirements
| # | المتطلب |
|---|---|
| FR-1.1 | Local Auth: تسجيل دخول/خروج، جلسات JWT، سياسة كلمة مرور وقفل محاولات **من الإعداد**، عبر IdentityProvider حصراً. |
| FR-1.2 | إدارة مستخدمين: إنشاء/تعطيل/إعادة تعيين — الحقول الثوابت (الرقم الوظيفي/username/المرجعي) **immutable** بمستوى DB. |
| FR-1.3 | Organization: شجرة قطاعات/إدارات + عضوية المستخدمين + أدوار على مستوى الوحدة التنظيمية. |
| FR-1.4 | Permission spine: أدوار أساسية (SuperAdmin/Admin/Manager/User قابلة للتوسعة) + PermissionAPI واحد تمر به كل الطلبات + **default-deny** + قرارات قابلة للتفسير (سبب السماح/المنع). |
| FR-1.5 | Metadata Registry: تعريف screen (اسم ASCII + label عربي/إنجليزي + الحقول الأساسية: text/number/date/select/boolean + إلزامية/فريد) + **Navigation/Menu Registry**: عناصر التنقّل metadata (ترتيب/أيقونة/الشاشة الهدف/الصلاحية المطلوبة) تُغذّي القائمة ديناميكياً. |
| FR-1.6 | خط التوليد المحكوم: من التعريف تتولّد migration مقترحة → فحص تعارض/مخاطر (أسماء محجوزة، تصادم، حذف عمود) → **اعتماد بشري داخل الواجهة** → تطبيق → versioning → حدث audit لكل خطوة → صفحة توثيق أولية. **لا DDL من LLM ولا DDL يدوي خارج الخط.** |
| FR-1.7 | Records CRUD أساسي على الكيان المولّد: list/create/read/update/soft-delete + فحص صلاحية لكل عملية + audit. |
| FR-1.8 | Admin shell: تنقّل ديناميكي حسب الصلاحية، ar/en + RTL، شاشات: المستخدمون/التنظيم/الأدوار/الشاشات/الترحيلات/السجلات/العارض. |
| FR-1.9 | Admin Log Viewer v1: عرض/بحث/تصفية Audit (permission-aware) وقراءة JSON app logs بقناع للأسرار. |
| FR-1.10 | Error Code Catalog يبدأ فعلياً: كل خطأ endpoint بحقل error_code + request_id (عقد coding-standards §10). |
| FR-1.11 | Feature Flags تُستخدم فعلياً: إخفاء قدرات غير مفعّلة من التنقّل دون كسر. |

## 7. Non-Functional Requirements (الخاصة بالمرحلة)
زمن قرار الصلاحية للطلب الواحد لا يتجاوز حدوداً معقولة (يُقاس ويوثَّق baseline) · تطبيق migration معتمدة أثريّ الأثر (idempotent-safe عبر أداة الترحيل) · واجهات الأدمن قابلة للاستخدام RTL بلا كسور تخطيط.

## 8. User Stories
بصفتي موظفاً: أدخل بحسابي فأرى الشاشات المسموحة فقط · أُنشئ سجلاً في شاشة مسموحة ويُرفض في غيرها برسالة واضحة · أرى سبب الرفض العام دون كشف سياسات حساسة.

## 9. Admin Stories
بصفتي أدمن: أعرّف شاشة جديدة فأحصل على migration مقترحة بمخاطرها · أعتمدها فتُطبَّق وتظهر شاشة CRUD تلقائياً · أرجع نسخة تعريف سابقة (rollback بالتوليد العكسي الآمن أو تعطيل) · أفتح الـ Log Viewer فأرى من فعل ماذا ومتى.

## 10. Main Modules + Epics (Plan Skeleton)
**Modules (Tier F/1/2):** config · feature-flags · audit · security-policy(حد أدنى) · identity · organization · permissions · admin · screens · fields · migrations · database-generation · records(basic).
**Epics:** E1.1 Identity&amp;Sessions → E1.2 Organization&amp;Roles → E1.3 Permission Spine → E1.4 Audit Spine → E1.5 Metadata Registry → E1.6 Governed Generation Pipeline → E1.7 Records CRUD → E1.8 Admin Shell (RTL) → E1.9 Log Viewer → E1.10 Hardening&amp;Docs&amp;Handoff.

## 11. Data Model Notes (indicative — platform_db ما لم يُذكر)
users, user_credentials, sessions · org_units, org_membership · roles, role_assignments, permissions_matrix(الأساسية) · screen_definitions(+versions), field_definitions, navigation_items · migration_proposals(status: draft/checked/approved/applied/rejected), migration_versions · generated entities في **apps_db** (schema-per-app) · audit_log (قائمة من P0، تتوسع أحداثاً).

## 12. API Notes (OpenAPI عبر FastAPI — مجموعات)
/auth/* · /users/* · /org/* · /roles/* · /screens/* (تعريف/إصدارات) · /migrations/* (proposal/check/approve/apply/history) · /records/{entity}/* · /audit/* (قراءة مصفّاة) · /logs/* (viewer) — كلها خلف Permission Gate، وأخطاء بعقد error_code.

## 13. UI Notes (React+Vite SPA — من كتالوج الشاشات)
Login · Users · Org tree · Roles · Screen Builder (نموذج تعريف + معاينة) · Migration Review (diff مفهوم + مخاطر + اعتماد) · Generated-Screen CRUD renderer v1 · Audit/Logs Viewer · إطار تنقّل حسب الصلاحية + مبدّل ar/en.

## 14. Security &amp; Permissions
كل endpoint خلف PermissionAPI (deny-by-default) · لا تجاوز للـ Gate من أي مسار داخلي · اعتماد الـ migration يتطلب دوراً مخوّلاً **يختلف عن مقترحها** (بذرة SoD) · الثوابت immutable · صفحات الأدمن لا تكشف secrets/endpoints (حدود D9).

## 15. Audit &amp; Logging
أحداث إلزامية: auth.login/logout/failed · user.created/disabled/reset · org.changed · role.assigned/revoked · permission.decision(denied فقط تلقائياً + allowed للحساسة) · screen.defined/versioned · migration.proposed/checked/approved/applied/rolled_back · record.created/updated/deleted · config/flag.changed (من P0). JSON logs بعقد §10 مع request/correlation IDs عبر الواجهة والخادم.

## 16. Configuration / Environment Impact
مفاتيح: AUTH_* (سياسات) · SESSION_* · ORG_* defaults · GENERATION_* (قواعد الفحص) · تفعيل شاشات الأدمن flags — كلها defaults+validation؛ لا مفاتيح بنية جديدة (الافتراضيات D4/D5 كما هي، بلا حاويات اختيارية).

## 17. Provider Abstractions Impact
IdentityProvider: تنفيذ Local كامل + العقد جاهز لـ LDAP/AD/OIDC لاحقاً · DatabaseRouter مستخدم فعلياً (platform/apps) · Cache/Queue/Lock تبقى memory/Postgres · لا LLM/Embedding/OCR إطلاقاً.

## 18. Database / Migration Notes
Baseline migrations (عبر PR) لجداول المنصة أعلاه · **خط التوليد المحكوم** ينتج migrations كيانات apps_db فقط، بأداة الترحيل نفسها، بمسار الاعتماد داخل المنتج — المساران مسمّيان لا يختلطان (constitution م10).

## 19. Testing Strategy (إضافات المرحلة فوق الأساس)
Permission: deny test **لكل endpoint** + محاولة تجاوز مباشرة للـ repository تفشل بالحدود · Generation: اقتراح خطر (حذف عمود/تصادم) يُرفض قبل الاعتماد؛ apply/rollback نظيفان · Audit: كل حدث بقائمة §15 يُنشأ بحقوله · E2E: سيناريو الأدمن الكامل (تعريف→اعتماد→CRUD) · RTL snapshot لكل شاشة جديدة · Logging-contract.

## 20. Acceptance Criteria
1) مستخدم بلا صلاحية يُمنع من كل شيء افتراضياً (مُثبت بالاختبارات). 2) دورة توليد كاملة تعمل من الواجهة وكل خطوة مدقَّقة وموثَّقة. 3) لا يمكن تطبيق migration غير معتمدة بأي مسار. 4) CRUD يعمل بفحص صلاحية لكل عملية. 5) الثوابت غير قابلة للتعديل حتى بمحاولة مباشرة. 6) Log Viewer يعرض Audit مصفّى بصلاحية الناظر. 7) كل شاشات المرحلة سليمة RTL. 8) صفر استدعاء LLM في الشيفرة.

## 21. Risks
تعقيد خط التوليد يبتلع المرحلة (تخفيف: شريحة رأسية واحدة + أنواع حقول أساسية فقط) · تسريب صلاحية عبر مسار جانبي (تخفيف: Gate واحد + boundary tests) · إغراء بناء workflow عام مبكراً (تخفيف: اعتماد مبسّط داخلي فقط).

## 22. Open Decisions
| OD | الموضوع | التوصية | البوابة |
|---|---|---|---|
| OD-P1-1 | قيم سياسة كلمة المرور/القفل الافتراضية | defaults معقولة قابلة للضبط config (لا تشفير مخصص — مكتبات قياسية بعد صف ترخيص) | Clarify التفعيل |
| OD-P1-2 | حبيبية إصدارات تعريف الشاشة | snapshot كامل لكل نسخة + diff محسوب | Clarify التفعيل |

## 23. Definition of Done
Baseline المشترك + معايير القبول 1–8 خضراء + توثيق شاشة التوليد محدَّث + handoff بقائمة "ما لا يُلمس" لوكيل P2 (عقود permissions/audit والـ generation pipeline).

## 24. Coding Agent Prompt
> استخدم القالب الموحّد في `methodology/agent-execution-model.md §6` مع: **PHASE=1 · DESIGN=phases/designs/phase-1-governed-core-screen-builder.md · RELEASE=v0.3-phase-design-package** — والتزم حرفياً بأقسام 2/3/14/22 من هذا التصميم.
