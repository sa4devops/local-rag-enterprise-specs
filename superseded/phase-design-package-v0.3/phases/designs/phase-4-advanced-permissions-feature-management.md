# Phase 4 — Advanced Permissions &amp; Feature Management (+Full Entity Profile)

> **Version:** 1.0 — Proposed (Accepted باعتماد v0.3) · **Date:** 2026-07-06 · **Authority عند الاعتماد:** المرتبة 6
> **Inherits:** Common Phase Baseline — PHASE_MASTER_PLAN §4. **Predecessor:** Phase 3 بكامل DoD. بطاقات المهام عند التفعيل.

## 1. Purpose
اكتمال نموذج الوصول المؤسسي قبل فتح المعرفة: **RBAC+ABAC+ReBAC + التصنيف الخماسي + Need-to-know + SoD** كسياسات مركّبة مُنفَّذة ومُفسَّرة، وEntity Profile كامل، و**حوكمة المزايا** (Feature/Module Management بSafe Mode وقائمة A10 للمحمي)، وسياسات أمن، وتصدير محكوم.

## 2. Scope
ABAC: شروط سمات (مستخدم/وحدة/سجل/تصنيف/زمن) بصيغ معلنة تُقيَّم في الـ Gate · ReBAC: منح علاقات (owner/manager-of/delegate بمدة) · التصنيف الخماسي على screen/field/record مع إنفاذ في الاستعلام والواجهة والتصدير · Need-to-know كوسم إضافي فوق التصنيف · SoD مصفوفة أدوار متعارضة تُفحص عند الإسناد وعند الفعل · **مفسّر القرار** (لماذا سُمح/مُنع — بمستوى كشف مضبوط) + وضع محاكاة للأدمن · **Entity Profile الكامل** (مصادر موسّعة + خط زمني + حساسية موروثة) · **Feature/Module Management**: تفعيل/تعطيل قدرات بمخطط تبعيات + **Safe Mode** + **قائمة A10 الحصرية لغير القابل للتعطيل** (identity/permissions/audit/config/flags/service-registry/db-router/health) · Security Policies screen (جلسات/محاولات/تصدير) · تصدير CSV/طباعة محكومان بالتصنيف مع وسم ومُدقَّقان · مراجعة وصول أساسية (تقرير مَن-يصل-إلى-ماذا).

## 3. Out of Scope
فهرسة/ملفات/RAG (P5) · watermark/DLP متقدم (Backlog) · IdP خارجي (configurable لاحقاً) · أي LLM.

## 4. Required Inputs
P3 DoD · هذا التصميم Accepted · قائمة A10 مثبتة نصاً (OD-P4-2 عند التفعيل).

## 5. Expected Outputs
سياسة مركّبة تُطبَّق وتُفسَّر وتُختبر؛ إدارة مزايا لا يمكنها كسر النظام؛ تصدير لا يتجاوز التصنيف؛ ملف كيان كامل محكوم.

## 6. Functional Requirements
| # | المتطلب |
|---|---|
| FR-4.1 | محرك ABAC: سمات قياسية seeded + صيغ معلنة (بنية شرطية metadata، **لا تعبيرات كود حر**) تُقيَّم داخل PermissionAPI. |
| FR-4.2 | ReBAC: علاقات مُعلنة بمنح محدودة المدة والقنوات، وتُلغى بانتهاء العلاقة. |
| FR-4.3 | التصنيف: خمس درجات على العناصر الثلاثة؛ قاعدة الغالب الأشد عند التجميع (Entity Profile/القوائم/التصدير). |
| FR-4.4 | Need-to-know: وسم يتطلب منحاً صريحاً إضافياً فوق أي سياسة أخرى. |
| FR-4.5 | SoD: مصفوفة تعارض أدوار تمنع الإسناد المتعارض وتمنع الفعل المزدوج (كمُعرِّف/مُعتمِد). |
| FR-4.6 | مفسّر القرار + محاكاة: الأدمن يختبر «ماذا يرى X؟» بنتيجة مفسَّرة، بصلاحية خاصة ومدقَّقة. |
| FR-4.7 | Entity Profile كامل: مصادر إضافية، خط زمني، إخفاء تجميعي بحسب الأشد، وتدقيق عرض الحساس. |
| FR-4.8 | Feature Management: شاشة flags بمخطط تبعيات (من manifests) — تعطيل قدرة يُخفيها ويُعطّل مساراتها بلطف؛ **A10 يرفض التعطيل بمستوى الخادم**. |
| FR-4.9 | Safe Mode: وضع تشغيل بأدنى القدرات (A10 + قراءة) للتعافي، تفعيله/إنهاؤه Ops/SuperAdmin ومدقَّق. |
| FR-4.10 | Security Policies: جلسات (مدة/تزامن)، محاولات وقفل، سياسة تصدير (مَن/أي تصنيف/بوسم إلزامي). |
| FR-4.11 | تصدير محكوم: فحص تصنيف كل حقل/صف قبل التضمين + وسم الملف + audit، والمرفوض لا يُصدَّر. |
| FR-4.12 | تقرير مراجعة وصول أساسي قابل للتصفية والتصدير المحكوم. |

## 7. NFRs (الخاصة)
زمن قرار السياسة المركّبة يُقاس baseline ويُحسَّن بذاكرة قرارات قصيرة العمر **مفاتيحها تشمل نطاق الصلاحية** (constitution م16) · المفسّر لا يكشف نص السياسات لغير المخوّل.

## 8. User Stories
بصفتي موظفاً: يظهر لي الحقل السري مقنَّعاً حتى لو ظهر السجل · أطلب تصديراً فيخرج المسموح فقط بوسمه · أفقد وصول «مدير-عن» تلقائياً بانتهاء التفويض.

## 9. Admin Stories
بصفتي سوبر أدمن: أعرّف سياسة ABAC بشرط وحدة+تصنيف+وقت فتُنفَّذ فوراً · أحاكي رؤية مستخدم وأحصل على تفسير · أعطّل ميزة فأرى أثر التبعيات قبل التأكيد ويستحيل تعطيل A10 · أفعّل Safe Mode في حادثة ثم أنهيه بتوثيق.

## 10. Main Modules + Epics
**Modules:** permissions (اكتمال) · security-policy · feature-flags (شاشة) · entity-profile (اكتمال) · admin.
**Epics:** E4.1 ABAC → E4.2 ReBAC → E4.3 Classification+NtK → E4.4 SoD → E4.5 Explainer+Simulation → E4.6 Entity Profile Full → E4.7 Feature Mgmt+A10+Safe Mode → E4.8 Security Policies → E4.9 Governed Export+Access Review → E4.10 Hardening/Docs/Handoff.

## 11. Data Model Notes
attributes_registry · abac_policies(بنية شرطية) · rebac_relations(+expiry) · classifications على التعريفات والسجلات (عمود موحّد عبر التوليد) · ntk_grants · sod_matrix · export_policies/export_log · feature manifests (من P0) + protected_list ثابتة كوداً-إعداداً مقروءة لا قابلة للتحرير من UI.

## 12. API Notes
/policies/abac|rebac|sod/* · /classifications/* · /permissions/simulate · /features/* (+dependencies) · /safe-mode (Ops-scope) · /export/{entity} · /access-review — خلف الـ Gate بعقد error_code.

## 13. UI Notes
Policy Studio (ABAC/ReBAC/SoD بنماذج معلنة) · Classification badges موحّدة · Simulation panel · Entity Profile v2 (خط زمني) · Feature Management (رسم تبعيات، تحذيرات، A10 رمادية) · Security Policies · Export dialog بوسم إلزامي — كلها RTL.

## 14. Security &amp; Permissions
كل السياسات تُقيَّم في PermissionAPI الواحد (لا محرك ثانٍ) · default-deny يبقى الأصل عند غياب سياسة · القرارات الحساسة (سماح على Secret/NtK) تُدقَّق allowed صراحة · A10 مفروضة خادمياً (رفض 403 بمعرّف سبب) لا واجهياً فقط.

## 15. Audit &amp; Logging
policy.created/changed/deleted (نسخ) · relation.granted/revoked/expired · classification.changed · sod.violation_blocked · permission.simulated · feature.enabled/disabled(+dependency_impact) · safe_mode.entered/exited · export.performed/denied · access_review.generated.

## 16. Configuration / Environment Impact
SESSION_*/LOCKOUT_* تُدار من Security Policies (dynamic ضمن حدود config) · EXPORT_* defaults · SAFE_MODE flag محمي · لا بنية جديدة.

## 17. Provider Abstractions Impact
لا مزوّدات جديدة · Cache قرارات الصلاحية عبر CacheProvider (memory) بمفاتيح تشمل نطاق الصلاحية وإبطال عند تغيّر سياسة.

## 18. Database / Migration Notes
Baseline migrations لجداول السياسات · عمود التصنيف على الكيانات عبر **خط التوليد** (ترحيل معتمد يضيفه للموجود) · فهارس لمسارات القرار الساخنة.

## 19. Testing Strategy (إضافات)
مصفوفة سيناريوهات سياسات مركّبة (سماح/منع متوقع) كاختبارات ثابتة · SoD: إسناد متعارض يفشل · A10: محاولة تعطيل عبر API تفشل 403 · Safe Mode: القدرات خارج A10 معطلة فعلاً · تصدير: حقل Secret لا يظهر بالملف (فحص محتوى) · مفسّر لا يسرّب نص سياسة لغير المخوّل · إبطال كاش القرار عند تغيير سياسة.

## 20. Acceptance Criteria
1) سياسات ABAC/ReBAC/تصنيف/NtK/SoD تُنفَّذ معاً بقرار واحد مفسَّر. 2) استحالة تعطيل A10 من أي واجهة (إثبات اختباري). 3) Safe Mode يعمل ويُدقَّق. 4) تصدير لا يتجاوز التصنيف أبداً. 5) محاكاة الرؤية تعمل بصلاحية ومدقَّقة. 6) Entity Profile الكامل يطبّق «الأشد». 7) كل أحداث §15 مسجلة. 8) baseline زمن القرار موثَّق. 9) RTL سليم.

## 21. Risks
انفجار تعقيد السياسات (تخفيف: بنية شرطية معلنة محدودة + مكتبة سيناريوهات) · قفل ذاتي بالخطأ (تخفيف: Safe Mode + حساب كسر-زجاج مدقَّق بإجراء Ops) · أثر أداء (تخفيف: كاش قرارات مضبوط الإبطال).

## 22. Open Decisions
| OD | الموضوع | التوصية | البوابة |
|---|---|---|---|
| OD-P4-1 | مجموعة السمات وصيغ ABAC الافتراضية | seed: (unit, sub-tree, clearance, classification, time-window, employment-status) وصيغ أمثلة قابلة للتحرير | Clarify التفعيل |
| OD-P4-2 | النص النهائي لقائمة A10 | القائمة المقترحة في §2 تُثبَّت حرفياً | Clarify التفعيل |
| OD-P4-3 | حساب كسر-الزجاج (break-glass) | حساب Ops خاص بتفعيل مزدوج وتدقيق مشدد | Clarify التفعيل |

## 23. Definition of Done
Baseline المشترك + AC 1–9 خضراء + توثيق Policy Studio/Feature Mgmt + handoff بقائمة "لا يُلمس" (PermissionAPI ومصفوفاته وA10) لوكيل P5.

## 24. Coding Agent Prompt
> القالب الموحّد §6 مع: **PHASE=4 · DESIGN=phases/designs/phase-4-advanced-permissions-feature-management.md · RELEASE=v0.3-phase-design-package** — التزم بأقسام 6/14/22؛ ممنوع أي محرك سياسات ثانٍ خارج PermissionAPI.
