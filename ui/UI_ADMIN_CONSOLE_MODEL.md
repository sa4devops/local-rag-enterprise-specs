# UI_ADMIN_CONSOLE_MODEL.md — نموذج وحدة الإدارة (Control Plane)

> **Version:** 1.0 — Proposed · **Date:** 2026-07-06 · **الموضع الهدف:** `ui/UI_ADMIN_CONSOLE_MODEL.md`
> **المراجع الحاكمة:** ADR-0008/D9 (حدود الإدارة) · تصاميم P1–P8 (شاشات كل مرحلة) · UI_SCREEN_INVENTORY (معرّفات الشاشات) · UI_ACTION_BUTTON_MODEL (§7: أفعال الإعداد surface=console).
> **التموضع:** الـ Console هو **مستوى التحكم** (metadata · actions · workflows · permissions · providers/models · RAG sources · audit/ops) — **ليس** واجهة تشغيل يومية للمستخدم العادي؛ العمل اليومي في Workspace/Renderer/Work Queue.

## 1) الجمهور والوصول
| الدور | يرى | لا يرى |
|---|---|---|
| Admin | مجموعات B/C/D (metadata/actions/workflows) + Users/Org الأساسية + Audit ضمن نطاقه | سياسات P4 المتقدمة، النماذج، الموصلات (إلا بتخويل) |
| SuperAdmin | كل المجموعات A–H | أسرار/endpoints (لا أحد يراها — D9) |
| Knowledge Admin | مجموعة E فقط | البقية |
| Ops (قراءة) | G (observability) + ops.status | أي إعداد قابل للتحرير |
الدخول من `admin.dashboard`؛ كل عنصر تنقّل مرشّح بالصلاحية (Navigation Registry نفسه).

## 2) الصدفة (Shell — مجموعة Stitch G5)
Sidebar بمجموعات §4 · Topbar: بحث إداري موحّد (يقفز لشاشة/مستخدم/تعريف) · **مؤشر البيئة/البروفايل** (Local/Prod ولون مميز لغير الإنتاج) · لافتة **Safe Mode** إن فُعّل · مبدّل ar/en · لا أرقام حساسة في الرأس افتراضياً.

## 3) أنماط عرضية موحّدة (تلتزم بها كل شاشات الـ Console — مرجع دفعة 3 وG5)
1. **List + Detail** (قائمة يسار/تفصيل يمين منطقياً — RTL-aware).
2. **نمط التعريف المُدار بالإصدارات** — لغة بصرية واحدة لدورة (Draft → Validate → Approve → Active → Rollback) تُستخدم في: الشاشات (P1/P2)، الأفعال (P3)، الـ Workflows (P3)، السياسات (P4) — شريط حالة + مَن اعتمد + diff للنسخ.
3. **لوحات محاكاة**: مخاطر الترحيل (P1) · Validation للـ workflow (P3) · «ماذا يرى X؟» (P4) · «مَن سيرى هذا الزر؟» (الأفعال) — المحاكاة صلاحية خاصة ومدقَّقة.
4. **حوار أثر التبعيات** قبل أي تعطيل/تغيير واسع (Features P4 · Connectors P7 · تغيير embedding مع خطة إعادة الفهرسة P5).
5. **أسطح القراءة D9**: طراز بصري مميز «قراءة فقط» (config_profiles، ops.status) — بلا أزرار تحرير إطلاقاً.
6. **شارة اعتماد-في-الإنتاج**: الأفعال الموسومة approval-in-prod تُظهرها قبل النقر.

## 4) المجموعات والشاشات (المعرّفات من الجرد؛ الأعمدة: الغرض · أهم الحقول · أهم الأفعال action_id · الصلاحية · أحداث التدقيق · Stitch)
### A) Platform Config — G5
| الشاشة | الغرض | أهم الحقول | أهم الأفعال | الصلاحية | Audit | Stitch |
|---|---|---|---|---|---|---|
| admin.dashboard | مدخل ومؤشرات دنيا | اعتمادات معلّقة · مهام فاشلة · ملخص صحة | تنقّل | admin.access | — | G5 مستقل |
| admin.features | حوكمة المزايا + Safe Mode | العلَم/الحالة/التبعيات/A10 | feature.enable/disable · safe_mode.enter/exit | admin.features.manage (SafeMode=Ops) | FEATURE_* · SAFE_MODE_* | G5 |

### B) Security &amp; Access — G6
| الشاشة | الغرض | أهم الحقول | أهم الأفعال | الصلاحية | Audit | Stitch |
|---|---|---|---|---|---|---|
| admin.users / user_detail | الحسابات وأدوارها | الثوابت (مقفلة) · الحالة · الأدوار · علاقات ReBAC | user.create/disable/reset · role.assign/revoke · rebac.grant | admin.users.manage | USER_* · ROLE_* | G6 (شاشتان) |
| admin.org | الشجرة والعضوية | الوحدات/العضوية/أدوار الوحدة | org.unit_create/move · membership.change | admin.org.manage | ORG_CHANGED | G6 |
| admin.roles / admin.permissions | الأدوار والمصفوفة الأساسية | role · permission grants | role.create/edit · permission.grant/revoke | admin.roles/permissions.manage | ROLE_/PERMISSION_CHANGED | G6 (مجمّعة) |
| admin.policies | Policy Studio (ABAC/ReBAC/SoD) | بنية شرطية معلنة · نسخ | policy.create/edit · permissions.simulate | admin.policies.manage | POLICY_CHANGED · PERMISSION_SIMULATED | G6 مستقل |
| admin.classification / admin.security_policies | التصنيف وسياسات الأمن | الدرجات · جلسات/قفل/تصدير | classification.assign · security.policy_update | admin.classification/security.manage | CLASSIFICATION_/SECURITY_POLICY_CHANGED | G6 (مجمّعة) |

### C) Metadata &amp; Actions (قلب المنصة) — G7
| الشاشة | الغرض | أهم الحقول | أهم الأفعال | الصلاحية | Audit | Stitch |
|---|---|---|---|---|---|---|
| admin.record_types (+fields تبويب) | بناء الأنواع/الشاشات وschema السطحين | الحقول/التحققات/RLS-FLS/الإصدارات | screen.define/version · policy.set | admin.metadata.manage | SCREEN_* | G7 مستقل (أهم شاشة إدارية) |
| admin.actions | **Action Registry** | عقد الفعل كاملاً (نموذج الأزرار §1) | action.define/edit · action.simulate_visibility | admin.actions.manage | ACTION_* | G7 مستقل |
| admin.migrations | بوابة الترحيلات | الاقتراح/المخاطر/المعتمِد | migration.check/approve/apply/rollback | admin.migrations.approve (SoD) | MIGRATION_* | G7 |
| admin.navigation / admin.generation_docs | التنقّل والتوثيق | عناصر القائمة · النسخ/diff | nav.add/reorder · docs.view | admin.metadata.manage/view | NAV_CHANGED | G7 (مجمّعة) |

### D) Workflow Configuration — G8-admin
admin.workflows / admin.workflow_detail: تعريف الحالات/الانتقالات/المكلَّفين + **دورة الحياة التسعينية** بنمط §3.2 + تبويب مصفوفة الاعتماد (OD-P3-1) · الأفعال: wf.define/validate/submit/approve/activate/rollback (SoD) · الصلاحيات admin.workflows.manage / wf.approve · Audit: WORKFLOW_* · Stitch: G8.

### E) Knowledge &amp; RAG — G9
admin.rag_sources (النطاقات=وسوم الصلاحية للفهرسة) · admin.ingestion (خطوات/إعادة محاولة/error_code) · files.manager (إعادة تصنيف/حذف محكوم) · admin.okf (حِزم موسومة «ليست مصدر حقيقة») — الصلاحية admin.knowledge/files.manage · Audit: SOURCE_/INGESTION_/FILE_/OKF_* · Stitch G9 (ingestion monitor مستقل، البقية مجمّعة).

### F) Models &amp; Providers — G10 (حدود D9 مشددة)
admin.capabilities (capability→provider/model + fallback + **provider.test_connection** بنتيجة فقط + خطة إعادة فهرسة عند تغيير embedding) · admin.agents (per-agent + معاملات + fallback) — approval-in-prod ظاهرة · الصلاحية admin.models.manage · Audit: CAPABILITY_/AGENT_BINDING_CHANGED · Stitch G10. **ممنوع في هذه الشاشات:** endpoints · secrets · GPU/replicas — تُدار config/Ops حصراً.

### G) Integrations Admin — G11-admin
admin.connectors: القدرات/الخطورة/الجمهور/سياسة HITL/صحة الموصل — **بلا أسرار**؛ الأفعال connector.enable/disable · audience.set · hitl.policy_set · الصلاحية admin.integrations.manage · Audit: CONNECTOR_* · Stitch G11 (مع سطح المتجر الإداري).

### H) Observability &amp; Ops — G12
admin.audit (permission-aware بنطاق الناظر) · admin.logs (قناع إلزامي) · admin.health (يعرض المطفأ disabled) · admin.error_catalog · admin.config_profiles (**قراءة**) — وP8: ops.status/about خارج صدفة الأدمن كأسطح ops-read بنفس اللغة البصرية.

## 5) ما لا يحتويه الـ Console أبداً (قائمة منع صريحة)
endpoints/secrets/مفاتيح تعمية · إدارة حاويات/replicas/GPU/بروفايلات النشر (config/Ops فقط) · أي «كود حر» (تعبيرات/سكربتات) في أي معرِّف · عمل المستخدم اليومي على السجلات (مكانه Renderer/Workspace) · تعطيل قائمة A10 (يرفضها الخادم) · تحرير سجلات التدقيق (append-only).

## 6) علاقة الأدمن بالـ Workspace
الأدمن يستخدم الـ Workspace للاستعلام والتحليل كأي مستخدم؛ لكن **كل أفعال الإعداد الإداري `surface=console`** (نموذج الأزرار §7): تغيير سياسة/نوع/نموذج لا يتم من الدردشة — لأن سطوح الإعداد الرسمية تحمل المحاكاة وأثر التبعيات وSoD وشارات approval-in-prod. الدردشة قد **تفتح** شاشة الإعداد المعنية (effect=open) ولا تنفّذ التغيير.

## 7) Open Decisions
| OD | الموضوع | التوصية |
|---|---|---|
| OD-AC-1 | مؤشرات admin.dashboard | الحد الأدنى: اعتمادات معلّقة · مهام معالجة فاشلة · ملخص صحة · آخر تغييرات سياسات — بلا أرقام أعمال حساسة |
| OD-AC-2 | ضوابط «المعاينة كمستخدم» | لافتة دائمة + مدة قصوى + حدث تدقيق صريح (P2/P4) — تُثبَّت مع Clarify P4 |
| OD-AC-3 | تجميع شاشات G6 في Stitch | policies مستقلة؛ (roles+permissions) شاشة مركّبة واحدة — يُحسم بدفعة الـ prompts |
