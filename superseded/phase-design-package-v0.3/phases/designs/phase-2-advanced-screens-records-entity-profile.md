# Phase 2 — Advanced Screens, Records &amp; Initial Entity Profile

> **Version:** 1.0 — Proposed (تصبح Accepted باعتماد v0.3) · **Date:** 2026-07-06 · **Authority عند الاعتماد:** المرتبة 6
> **Inherits:** Common Phase Baseline — PHASE_MASTER_PLAN §4. **Predecessor:** Phase 1 بكامل DoD. بطاقات المهام عند التفعيل.

## 1. Purpose
نضج محرك الشاشات والسجلات إلى مستوى إنتاجي: كل أنواع الحقول والتحققات والعلاقات، وإنفاذ العزل **صفاً (RLS)** و**حقلاً (FLS)** فعلياً، وشاشة توثيق توليد كاملة، وEntity Profile مبدئي للقراءة المجمّعة.

## 2. Scope
أنواع حقول كاملة: text/longtext/number/decimal/date/datetime/select/multiselect/boolean/**relation(FK)**/lookup-display/attachment-**تعريفاً فقط** (التخزين P5) · تحققات: required/unique/regex/range/cross-field/conditional-visibility · List Engine: بحث/فرز/تصفية/ترقيم عبر PostgreSQL · **RLS**: سياسات نطاق (own/org-unit/subtree/all) تُولَّد ضمن خط التوليد وتُنفَّذ في الاستعلام + طبقة repository (دفاع مزدوج) · **FLS**: إخفاء/قناع حقول حسب الدور في API والواجهة معاً · شاشة توثيق التوليد الكاملة (النسخ/الفروق/مَن اعتمد/متى) · **Entity Profile v1**: عرض مجمّع للقراءة لكيان (شخص/جهة) من شاشات مُعلَّمة، مُشذَّب بصلاحيات الناظر · Soft-delete/restore موحّد.

## 3. Out of Scope
Workflows/Approvals (P3) · ABAC/ReBAC/التصنيف الخماسي والتصدير المحكوم (P4) · تخزين مرفقات فعلي وOCR (P5) · حقول محسوبة معقدة (OD) · أي LLM.

## 4. Required Inputs
P1 DoD · هذا التصميم Accepted · لا بوابات ترخيص جديدة (لا dependencies جديدة متوقعة؛ أي مكتبة تحقق إضافية ⇒ صف license-review أولاً).

## 5. Expected Outputs
بناء شاشات معقدة من الواجهة بعلاقات وتحققات، وسجلات معزولة صفاً/حقلاً بإثبات اختباري، وتوثيق تلقائي كامل لكل توليد، وملف كيان مبدئي.

## 6. Functional Requirements
| # | المتطلب |
|---|---|
| FR-2.1 | توسيع Field Registry بكل الأنواع أعلاه + خصائص لكل نوع (precision/format/options-source ثابتة أو من شاشة أخرى). |
| FR-2.2 | Relation fields: FK محكومة بخط التوليد + سلوك حذف مضبوط (restrict افتراضاً) + عرض lookup-label. |
| FR-2.3 | محرك تحققات معلن metadata يعمل خادمياً (المصدر) وواجهياً (تجربة) — الخادم هو الحكم. |
| FR-2.4 | List Engine بقدرات بحث/فرز/تصفية معلنة لكل شاشة، مع فهارس تُقترح ضمن migration الاعتماد. |
| FR-2.5 | RLS: تعريف سياسة النطاق لكل شاشة عند التعريف؛ التوليد ينتج سياسات PostgreSQL RLS + scoping بالـ repository؛ **تعطيل RLS ممنوع من الواجهة**. |
| FR-2.6 | FLS: مصفوفة حقل×دور (view/edit/hidden/masked)؛ الحقول المحجوبة **لا تغادر الخادم** أصلاً. |
| FR-2.7 | شاشة توثيق التوليد: لكل كيان — التعريف الحالي، سلسلة النسخ، diffs، المعتمِدون، حالة السياسات. |
| FR-2.8 | Entity Profile v1: تعليم شاشات كمُغذّية لملف الكيان + مفتاح الربط (الرقم المرجعي) + عرض مجمّع read-only مُرشَّح بصلاحيات الناظر حقلاً وصفاً. |
| FR-2.9 | Soft-delete/restore موحّد + إظهار المحذوف لدور مخوّل فقط. |
| FR-2.10 | كل ما سبق يمر بخط التوليد المحكوم نفسه (لا مسار جانبي). |

## 7. NFRs (الخاصة)
استعلامات القوائم مع RLS ضمن حدود مقبولة على بيانات demo (يُقاس baseline ويوثَّق) · رسائل التحقق ثنائية اللغة من i18n keys.

## 8. User Stories
بصفتي موظفاً: أرى في القائمة سجلات نطاقي فقط دون أن أعرف بوجود غيرها · أرى الحقول المسموحة لي فقط والحقول الحساسة مقنَّعة · أستعيد سجلاً حذفته بالخطأ إن كنت مخوّلاً.

## 9. Admin Stories
بصفتي أدمن: أضيف حقل علاقة بين شاشتين فيُولَّد FK باعتماد · أضبط سياسة النطاق (own/org/all) لكل شاشة · أفتح توثيق أي كيان فأرى تاريخه كاملاً · أعلّم شاشات تُغذّي Entity Profile وأعاينه بصلاحيات مستخدم آخر (impersonated preview مقيد ومدقَّق).

## 10. Main Modules + Epics
**Modules:** screens · fields · records · database-generation · permissions (توسعة RLS/FLS) · **entity-profile (جديد — انظر OD-P2-1)** · admin.
**Epics:** E2.1 Field Types&amp;Validation → E2.2 Relations → E2.3 List Engine → E2.4 RLS → E2.5 FLS → E2.6 Generation Docs Screen → E2.7 Entity Profile v1 → E2.8 Hardening/Docs/Handoff.

## 11. Data Model Notes
field_definitions (توسعة أنواع/خصائص) · screen_policies (rls_scope, fls_matrix) · entity_profile_sources (screen_id, join_key, weight/ترتيب) · soft-delete أعمدة موحّدة (deleted_at/by) على الكيانات المولّدة · لا جداول بيانات جديدة في platform_db سوى المذكور.

## 12. API Notes
/records/{entity}: توسعة query (search/sort/filter/page) · /screens/{id}/policy · /entity-profile/{key} (read) · /screens/{id}/docs (documentation) — كلها خلف الـ Gate وبعقد error_code.

## 13. UI Notes
Screen Builder v2 (أنواع/تحققات/علاقات/سياسات) · Renderer v2 (قوائم متقدمة + قناع FLS) · Generation Documentation screen · Entity Profile viewer · كل الجداول RTL-سليمة مع أرقام/تواريخ محلية.

## 14. Security &amp; Permissions
لا نتيجة استعلام تغادر قبل تطبيق RLS scope · FLS تقليم خادمي · Entity Profile يُرشَّح بنفس محركي RLS/FLS للناظر (لا امتياز تجميعي) · معاينة-كمستخدم تتطلب صلاحية خاصة وتُدقَّق حدثاً صريحاً.

## 15. Audit &amp; Logging
إضافات: screen.policy_changed · record.restored · entity_profile.source_added/removed · entity_profile.viewed (للحساسة) · export لا يوجد بعد (P4). بقية أحداث P1 تسري.

## 16. Configuration / Environment Impact
مفاتيح: LIST_PAGE_SIZE defaults · VALIDATION_* حدود · PROFILE_JOIN_KEY افتراضي (الرقم المرجعي) — defaults+validation؛ لا تغيير على حاويات/بنية.

## 17. Provider Abstractions Impact
لا مزوّدات جديدة؛ attachment fields تعرّف الحقل فقط وتربط لاحقاً بـ ObjectStorageProvider في P5 (fs الافتراضي كما هو).

## 18. Database / Migration Notes
كل تغييرات الكيانات عبر خط التوليد (يشمل توليد سياسات RLS وfهارس القوائم) · baseline migrations فقط لجداول platform الجديدة أعلاه · rollback policy: سياسة نسخة سابقة قابلة لإعادة التطبيق.

## 19. Testing Strategy (إضافات)
RLS: مستخدمان بنطاقين لا يرى أحدهما سجل الآخر (list/read/update/delete) + محاولة IDOR تفشل · FLS: الحقل المحجوب غائب من JSON فعلاً · تحققات cross-field خادمياً · Entity Profile: التجميع لا يتجاوز صلاحيات الناظر (اختبار سلبي إلزامي) · أداء قائمة baseline موثَّق.

## 20. Acceptance Criteria
1) بناء شاشة بعلاقات وتحققات كاملة من الواجهة تعمل CRUD. 2) إثبات اختباري لعزل RLS وFLS (سلبية وإيجابية). 3) الحقول المقنَّعة لا تظهر في أي استجابة API. 4) توثيق التوليد يعرض النسخ والفروق والمعتمِدين. 5) Entity Profile يعرض المجمّع المسموح فقط ويُدقَّق عند الحساسية. 6) لا مسار توليد خارج الخط المحكوم. 7) RTL سليم لكل شاشات المرحلة.

## 21. Risks
تعقيد مصفوفة FLS (تخفيف: مصفوفة بسيطة حقل×دور v1) · أداء RLS على استعلامات معقدة (تخفيف: فهارس مقترحة بالاعتماد + قياس) · زحف نطاق نحو حقول محسوبة (مقفول بـ OD).

## 22. Open Decisions
| OD | الموضوع | التوصية | البوابة |
|---|---|---|---|
| OD-P2-1 | ملكية Entity Profile | module مستقل `entity-profile` (Tier 2) يعتمد على records/permissions — لا داخل records | Clarify التفعيل |
| OD-P2-2 | الحقول المحسوبة server-side | تأجيل إلى Backlog (عرض تركيبي بسيط فقط الآن) | Clarify التفعيل |

## 23. Definition of Done
Baseline المشترك + AC 1–7 خضراء + توثيق شاشتي Builder/Docs محدّث + handoff بقائمة "لا يُلمس" (محركا RLS/FLS وعقد policies) لوكيل P3.

## 24. Coding Agent Prompt
> القالب الموحّد §6 في `methodology/agent-execution-model.md` مع: **PHASE=2 · DESIGN=phases/designs/phase-2-advanced-screens-records-entity-profile.md · RELEASE=v0.3-phase-design-package** — التزم حرفياً بأقسام 3/5/14/22.
