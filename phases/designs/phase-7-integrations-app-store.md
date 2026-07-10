# Phase 7 — Integrations &amp; Enterprise App Store

الحالة: Accepted v0.3 (2026-07-06) — مدخل تصميم ما-قبل-الأساس (استُعيد 2026-07-10 ضمن إغلاق F-3). هذه الوثيقة هي تصميم المرحلة المعتمد تاريخياً والموطن التعريفي لمعرفات FR الخاصة بها. عند تفعيل المرحلة يُنتَج «تصميم التفعيل» النهائي وفق قاعدة phase-roadmap بادئاً من هذه الوثيقة؛ وكل ما استجد في حزم v0.4 حتى v1.0-architecture-baseline والـ ADRs يعلوها عند أي تعارض (سلسلة م20). لا تنفيذ مباشر من هذه الوثيقة دون بطاقة مهمة وتصميم تفعيل.

> **Version:** 1.0 — Proposed (Accepted باعتماد v0.3) · **Date:** 2026-07-06 · **Authority عند الاعتماد:** المرتبة 6
> **Inherits:** Common Phase Baseline — PHASE_MASTER_PLAN §4. **Predecessor:** Phase 6 بكامل DoD. بطاقات المهام عند التفعيل.
> **بوابات دخول (فئة 2):** **جرد الأنظمة الداخلية وعقودها** + مراجعة ترخيص/أمن **لكل connector** قبل بنائه — لا تكامل بلا جرد.

## 1. Purpose
تحويل المنصة إلى **مشغّل لأنظمة المؤسسة**: إدارة تكاملات داخلية (MCP / Internal REST / Webhook / DB-readonly)، متجر تطبيقات مؤسسي يعرض المسموح فقط، ربط حسابات وتفويض لكل مستخدم أو عبر service-accounts، واستخدام الأدوات داخل Chat/Tasks/Workflows/Reports/Notifications — مع **بوابة بشرية لكل فعل مُغيِّر للحالة** وتدقيق كامل، وكل الشبكة داخلية حصراً.

## 2. Scope
Connector Registry: تعريف موصل (نوع MCP/REST/Webhook/DB-ro، القدرات/الأدوات المعلنة، مخطط المدخلات/المخرجات، مستوى الخطورة لكل أداة read/act) · **فصل D9**: Ops يضبط endpoints/secrets عبر config/آلية أسرار؛ الأدمن يفعّل القدرة ويحدد الجمهور · Account Linking: ربط هوية المستخدم بحساب النظام الهدف (رموز مُعمّاة، انتهاء، إلغاء) + **service-accounts** بتفويض لكل مستخدم مسجَّل (OD-P7-1) · App Store: كتالوج التطبيقات/الأدوات المفعّلة **المرشّح بصلاحية الناظر**، تفعيل شخصي، حالة الربط · Tool-invocation عبر الـ Gateway/Orchestrator: أدوات **read** ضمن الصلاحية مباشرة؛ أدوات **act** (تُنشئ/تعدّل في نظام هدف) تمر **إلزامياً** ببوابة human-in-the-loop (معاينة الفعل→موافقة→تنفيذ) · dry-run/sandbox للموصلات حيث أمكن · حدود معدل لكل connector/مستخدم · Webhooks واردة موقَّعة ومقيدة المصدر تُحوَّل أحداثاً داخلية · استخدام النتائج داخل chat (مسنودة كمصدر «نظام») والتقارير والمهام والإشعارات.

## 3. Out of Scope
أي SaaS خارجي (Backlog عبر proxy معتمد بنص صريح) · موصلات تكتب في قواعد بيانات أنظمة أخرى مباشرة (DB = قراءة فقط) · أتمتة بلا موافقة للأفعال المُغيِّرة · متجر عام/طرف ثالث.

## 4. Required Inputs
P6 DoD · هذا التصميم Accepted · جرد الأنظمة + عقود APIs موثّقة · صف مراجعة لكل connector (ترخيص أدواته إن وُجدت + أمن) · نموذج service-accounts محسوم (OD-P7-1).

## 5. Expected Outputs
متجر يعرض للمستخدم تطبيقاته المسموحة؛ ربط حساب آمن؛ سؤال في الدردشة يستدعي أداة نظام داخلي ضمن صلاحية الحساب المربوط؛ فعل مُغيِّر يُنفَّذ فقط بعد معاينة وموافقة؛ وكل نداء مدقَّق.

## 6. Functional Requirements
| # | المتطلب |
|---|---|
| FR-7.1 | Connector Registry بتعريف معلن للأدوات (schema مدخلات/مخرجات + تصنيف read/act + خطورة). |
| FR-7.2 | حدود D9: لا endpoint/secret في UI؛ الأدمن يرى الحالة والقدرات فقط ويفعّل/يوجّه الجمهور. |
| FR-7.3 | Account Linking لكل مستخدم: بدء ربط، تخزين رموز مُعمّى at-rest، انتهاء/تجديد، إلغاء ذاتي وإداري. |
| FR-7.4 | Service-accounts: هوية موصل + سجل تفويض لكل مستخدم (مَن نُفِّذ باسمه) — **لا فعل باسم مجهول**. |
| FR-7.5 | App Store مرشّح بالصلاحية + تفعيل شخصي + حالة الربط + وصف القدرات ثنائي اللغة. |
| FR-7.6 | Invocation pipeline: تحقق صلاحية المنصة → تحقق ربط/تفويض → تنفيذ read أو **بوابة موافقة لـ act** (معاينة payload مقروءة) → تنفيذ → تسجيل. |
| FR-7.7 | بوابة human-in-the-loop قابلة للربط بمصفوفة اعتماد P3/P4 (فعل حساس = موافقة إضافية). |
| FR-7.8 | حدود معدل + مهل + قواطع دائرة لكل connector مع إبلاغ صحي في /health/integrations. |
| FR-7.9 | Webhooks واردة: تحقق توقيع/مصدر + تحويلها أحداث notifications/workflows. |
| FR-7.10 | DB-connector قراءة فقط عبر مستخدم DB بأدنى صلاحية وallow-list كائنات، بنفس ضوابط SQL-Agent. |
| FR-7.11 | إتاحة الأدوات داخل Chat/Reports/Tasks/Workflows كمصادر/أفعال معلنة — النتائج توسم «نظام: X» وتدخل الإسناد. |

## 7. NFRs (الخاصة)
فشل موصل لا يسقط المنصة (عزل/قاطع) · زمن الأداة يُقاس ويُعرض · أسرار الربط لا تظهر في أي log (فحص قناع).

## 8. User Stories
بصفتي موظفاً: أفتح المتجر فأرى تطبيقات صلاحيتي فقط · أربط حسابي في نظام المراسلات وألغيه متى شئت · أطلب في الدردشة «أنشئ مذكرة في النظام Y» فأرى معاينة وأوافق قبل التنفيذ · أرى في سجل نشاطي كل ما نُفِّذ باسمي.

## 9. Admin Stories
بصفتي أدمن: أفعّل موصلاً وأحدد جمهوره دون رؤية أسراره · أجعل أداة «act» تتطلب موافقة مدير · أعطّل موصلاً متعثراً فتتوقف أدواته بلطف مع إشعار · أراجع تدقيق نداءات موصل بمدخلاته المُقنَّعة.

## 10. Main Modules + Epics
**Modules:** integrations · mcp-connectors · app-store (+توسعات chat/workflows/notifications للاستهلاك).
**Epics:** E7.1 Connector Registry+D9 → E7.2 Secrets/Ops wiring (config فقط) → E7.3 Account Linking → E7.4 Service-accounts+Delegation → E7.5 App Store UI → E7.6 Invocation+HITL Gate → E7.7 Rate/Breaker/Health → E7.8 Webhooks In → E7.9 DB-ro Connector → E7.10 Chat/Reports Consumption → E7.11 Hardening/Docs/Handoff.

## 11. Data Model Notes
connectors(+tools,schemas,risk) · connector_enablement(audience) · account_links(+expiry,status) · delegation_log · invocation_log(مدخلات مُقنَّعة/نتيجة/زمن/قرار البوابة) · webhook_endpoints(+signature policy) — integration_db حسب نموذج القواعد؛ الرموز مُعمّاة بمفتاح تديره طبقة Ops.

## 12. API Notes
/connectors/* · /store/* · /links/* · /invoke/{connector}/{tool} (مع مسار preview/approve للأفعال) · /webhooks/{id} (وارد) — خلف الـ Gate؛ عقود الأدوات من الـ Registry حصراً.

## 13. UI Notes
App Store (بطاقات ثنائية اللغة، حالة الربط) · My Connections · Approval preview dialog (payload مقروء قبل الموافقة) · Admin connector console (بلا أسرار) · مؤشرات صحة الموصلات — RTL كاملة.

## 14. Security &amp; Permissions
مبدأ مزدوج: **صلاحية المنصة ∩ صلاحية الحساب المربوط** — الأضيق يسود · لا invocation بلا هوية مستخدم نهائي مسجّلة (حتى عبر service-account) · act بلا موافقة = مرفوض بنيوياً · تعقيم مخرجات الأدوات قبل دخولها سياق النموذج (حقن) · webhooks بتوقيع إلزامي · كل الشبكات داخلية (no-external-call يسري).

## 15. Audit &amp; Logging
connector.registered/enabled/disabled · link.created/renewed/revoked · invocation.requested/previewed/approved/denied/executed/failed (بهوية المنفَّذ باسمه) · webhook.received/verified/rejected · rate.limited/breaker.opened — correlation يربط سلسلة chat→tool→نتيجة.

## 16. Configuration / Environment Impact
CONNECTOR_{X}_ENDPOINT/SECRET_REF (config/أسرار — Ops) · RATE_*/TIMEOUT_*/BREAKER_* · HITL_POLICY defaults · WEBHOOK_* — defaults+validation؛ لا حاويات جديدة إلا إن تطلب موصل bridge محلياً (يمر فئة 3 حينها).

## 17. Provider Abstractions Impact
لا مزوّد نماذج جديد · طبقة Connector-Adapter لكل نوع (MCP/REST/Webhook/DB-ro) داخل integrations حصراً — أي SDK نظام هدف داخل الـ adapter فقط.

## 18. Database / Migration Notes
Baseline migrations لجداول integration_db · DB-ro connectors عبر مستخدمي قراءة بأدنى صلاحية يُنشئهم Ops (خارج الكود) · لا كتابة عابرة للأنظمة من قاعدة المنصة.

## 19. Testing Strategy (إضافات)
act بلا موافقة يفشل بنيوياً (اختبار سلبي إلزامي) · تنفيذ باسم مستخدم غير مفوَّض يفشل · أسرار لا تظهر في logs (قناع) · webhook بتوقيع خاطئ يُرفض · breaker يفتح عند فشل متكرر ويُبلغ الصحة · حقن عبر مخرجات أداة لا يغيّر تعليمات النظام (اختبار حقن) · تقاطع الصلاحيتين مُثبت (منصة تسمح/هدف يمنع ⇒ منع، والعكس).

## 20. Acceptance Criteria
1) المتجر يعرض المسموح فقط لكل ناظر. 2) ربط/إلغاء الحساب يعمل والرموز مُعمّاة ولا تظهر أبداً. 3) أداة read تعمل ضمن التقاطع؛ وأداة act لا تُنفَّذ إلا بعد معاينة وموافقة (وموافقة إضافية للحساس). 4) كل نداء مسجَّل بهوية مَن نُفِّذ باسمه وسلسلة correlation كاملة. 5) فشل موصل معزول ولا يسقط غيره. 6) webhook موقَّع فقط يُقبل. 7) DB-connector قراءة فقط ضمن allow-list. 8) RTL سليم.

## 21. Risks
فعل خطير رغم الضوابط (تخفيف: HITL إلزامي + مصفوفة P4 + dry-run) · تسرب رموز (تخفيف: تعمية + قناع + مراجعة) · موصل بطيء يخنق الدردشة (تخفيف: مهل/قاطع/غير متزامن) · اتساع الجرد (تخفيف: موصل-تلو-موصل ببوابته).

## 22. Open Decisions
| OD | الموضوع | التوصية | البوابة |
|---|---|---|---|
| OD-P7-1 | نموذج service-accounts | حساب خدمة لكل موصل + سجل تفويض لكل مستخدم + انتهاء دوري | Clarify التفعيل |
| OD-P7-2 | آلية تعمية الرموز at-rest | مفتاح تديره طبقة Ops (خارج UI/DB-config) عبر آلية الأسرار المعتمدة | قبل أول ربط فعلي |
| OD-P7-3 | سياسة HITL الافتراضية | كل act = موافقة؛ الحساس = موافقة مزدوجة عبر مصفوفة P3/P4 | Clarify التفعيل |

## 23. Definition of Done
Baseline المشترك + AC 1–8 خضراء + توثيق المتجر/الموصلات + دليل إضافة موصل جديد (إجرائي) + handoff بقائمة "لا يُلمس" (invocation pipeline وبوابة HITL) لوكيل P8.

## 24. Coding Agent Prompt
> القالب الموحّد §6 مع: **PHASE=7 · DESIGN=phases/designs/phase-7-integrations-app-store.md · RELEASE=v0.3-phase-design-package** — لا موصل بلا صف جرد ومراجعة؛ التزم بأقسام 3/14/19/22.
