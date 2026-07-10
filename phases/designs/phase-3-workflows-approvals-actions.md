# Phase 3 — Workflows, Approvals &amp; Action Buttons (+Tasks · Projects · Notifications)

الحالة: Accepted v0.3 (2026-07-06) — مدخل تصميم ما-قبل-الأساس (استُعيد 2026-07-10 ضمن إغلاق F-3). هذه الوثيقة هي تصميم المرحلة المعتمد تاريخياً والموطن التعريفي لمعرفات FR الخاصة بها. عند تفعيل المرحلة يُنتَج «تصميم التفعيل» النهائي وفق قاعدة phase-roadmap بادئاً من هذه الوثيقة؛ وكل ما استجد في حزم v0.4 حتى v1.0-architecture-baseline والـ ADRs يعلوها عند أي تعارض (سلسلة م20). لا تنفيذ مباشر من هذه الوثيقة دون بطاقة مهمة وتصميم تفعيل.

> **Version:** 1.0 — Proposed (Accepted باعتماد v0.3) · **Date:** 2026-07-06 · **Authority عند الاعتماد:** المرتبة 6
> **Inherits:** Common Phase Baseline — PHASE_MASTER_PLAN §4. **Predecessor:** Phase 2 بكامل DoD. بطاقات المهام عند التفعيل.

## 1. Purpose
تحويل الشاشات إلى **عمليات مؤسسية محكومة**: محرك workflows بنوعيه (نظامي/مُعرَّف من الأدمن) بدورة حياة كاملة، اعتمادات بفصل مهام (SoD)، أزرار إجراء/CTA معلنة metadata، ومنظومة إشعارات ومهام ومشاريع — **بلا أي تنفيذ عبر LLM**.

## 2. Scope
تعريف workflow metadata: حالات/انتقالات/شروط (على قيم الحقول والنطاق)/مكلَّفون (دور/وحدة/فرد) · **دورة حياة تعريف الـ workflow**: Draft → Validation → Permission-check → Risk-check → Approval → Activation → Versioning → Rollback → Audit (تعريف المستخدم لا يُفعَّل قبل اعتماد مخوَّل — SoD) · تشغيل الـ instances على السجلات (transition بصلاحية + شرط) · Approvals inbox (موافقة/رفض/إرجاع بتعليق) · **Action/CTA buttons**: زر معلن (label ar/en، صلاحية، تأكيد، الأثر: transition/تحديث حقول/إشعار) يُدار من Builder · Notifications: مركز داخل التطبيق + تفضيلات + **دردشة/نقاش لكل إشعار أو بند اعتماد** (thread تعليقات بشرية مرتبط بالبند — ليست LLM chat) · Tasks: إنشاء/تكليف/حالة/استحقاق + توليد مهمة من انتقال · Projects: تجميع مهام/سجلات (+ملفات لاحقاً) بعضوية وصلاحية · تذكيرات استحقاق عبر QueueProvider (Postgres).

## 3. Out of Scope
أي تنفيذ/صياغة عبر LLM (P6) · قنوات إشعار خارجية email/SMS (Backlog — الطبقة مجرّدة) · مؤقتات SLA وتصعيد متقدم (Backlog) · تكاملات خارجية (P7) · مصفوفات SoD/ABAC الكاملة (P4 — هنا SoD الأساسي للاعتمادات).

## 4. Required Inputs
P2 DoD · هذا التصميم Accepted · لا بوابات ترخيص (لا dependencies جديدة متوقعة).

## 5. Expected Outputs
عملية كاملة قابلة للعرض: تعريف workflow من الواجهة → اعتماده → تشغيله على شاشة → انتقالات بصلاحية → اعتمادات → إشعارات ومهام — بكل خطوة مدقَّقة وبقابلية rollback للتعريف.

## 6. Functional Requirements
| # | المتطلب |
|---|---|
| FR-3.1 | Workflow Registry: تعريف الحالات/الانتقالات/الشروط/المكلَّفين metadata، مرتبط بشاشة/كيان. |
| FR-3.2 | دورة حياة التعريف التسعينية أعلاه مُنفَّذة حرفياً؛ **مُعرِّف ≠ مُعتمِد ≠ مُفعِّل** (قابل للضبط، افتراضه صارم). |
| FR-3.3 | Runtime: transition ينفَّذ فقط إذا (صلاحية + شرط + حالة صحيحة)؛ التعارض يُرفض برسالة مفسّرة. |
| FR-3.4 | Approvals: بند اعتماد لكل انتقال مُعلَّم؛ inbox موحّد؛ قرارات موافقة/رفض/إرجاع بتعليق إلزامي عند الرفض. |
| FR-3.5 | Action Buttons: تعريف metadata + ظهور حسب الصلاحية والحالة + تأكيد اختياري + أثر معلن فقط (لا كود حر). |
| FR-3.6 | Notifications: أحداث النظام (تكليف/اعتماد/انتقال/استحقاق) تولّد إشعارات؛ مركز قراءة/تمييز؛ تفضيلات بسيطة. |
| FR-3.7 | Notification/Approval Thread: نقاش بشري لكل بند، بصلاحية أطرافه، ويُحفظ ضمن سياق البند. |
| FR-3.8 | Tasks: CRUD + تكليف + حالات + استحقاق + توليد تلقائي من انتقال مُعلَّم + تذكير استحقاق (queue). |
| FR-3.9 | Projects: إنشاء/عضوية/ربط مهام وسجلات + رؤية بحسب العضوية والصلاحية. |
| FR-3.10 | Versioning/Rollback لتعريفات الـ workflow: تفعيل نسخة سابقة معتمدة؛ الـ instances الجارية تُعامل بسياسة معلنة (تكمل على نسختها). |

## 7. NFRs (الخاصة)
قرار transition ضمن زمن معقول يُقاس baseline · لا فقدان إشعار عند إعادة تشغيل worker (اختبار at-least-once على Postgres-queue).

## 8. User Stories
بصفتي موظفاً: أرى المهام والاعتمادات المكلَّف بها في مكان واحد · أنفّذ زر إجراء مسموحاً فيتغير السجل ويُشعر المعنيون · أناقش بند اعتماد في thread قبل قراري.

## 9. Admin Stories
بصفتي أدمن: أرسم workflow لشاشة وأرسله للاعتماد فلا يعمل قبل موافقة مخوَّل غيري · أضيف زر CTA بأثر معلن دون كود · أسترجع نسخة workflow سابقة عند مشكلة · أرى أثر التعريف قبل تفعيله (أي شاشات/أدوار يمس).

## 10. Main Modules + Epics
**Modules:** workflows · approvals · tasks · projects · notifications (+توسعات screens/records للأزرار).
**Epics:** E3.1 Workflow Registry → E3.2 Definition Lifecycle+SoD → E3.3 Runtime Transitions → E3.4 Approvals Inbox → E3.5 Action Buttons → E3.6 Notifications+Threads → E3.7 Tasks → E3.8 Projects → E3.9 Versioning/Rollback → E3.10 Hardening/Docs/Handoff.

## 11. Data Model Notes
workflow_definitions(+versions,status) · workflow_states/transitions/conditions/assignees · workflow_instances(+history) · approval_items(+decisions) · action_buttons · notifications(+reads,prefs) · notification_threads/messages · tasks · projects(+members,links) — في platform_db؛ instances تشير لسجلات apps_db بمفاتيح.

## 12. API Notes
/workflows/* (تعريف/دورة حياة) · /workflows/{id}/instances/* (transition) · /approvals/* · /actions/{button}/invoke · /notifications/* (+threads) · /tasks/* · /projects/* — خلف الـ Gate، أخطاء بعقد error_code.

## 13. UI Notes
Workflow Builder (canvas مبسّط v1: حالات/انتقالات كقائمة/مخطط بسيط — بلا مكتبات جديدة دون صف ترخيص؛ xyflow مرشّح بصف مسبق) · Approvals Inbox · إعداد الأزرار داخل Screen Builder · Notification Center + Thread panel · Tasks board/list · Projects.

## 14. Security &amp; Permissions
كل transition/زر خلف الـ Gate بحالته وشرطه · SoD الاعتماد إلزامي (لا اعتماد ذاتي) · threads مرئية لأطراف البند فقط · لا تفعيل workflow مستخدمٍ بلا اعتماد (منع بمستوى الحالة لا الواجهة فقط).

## 15. Audit &amp; Logging
workflow.defined/validated/approved/activated/rolled_back · instance.transitioned(من/إلى/بواسطة/شرط) · approval.decided(قرار/تعليق) · action_button.invoked · task.created/assigned/completed · project.changed · notification.sent/read (الحساسة) — بحقول actor/target/old/new/ts.

## 16. Configuration / Environment Impact
WF_SOD_STRICT=true افتراضاً · REMINDER_* (فترات) · NOTIF_* defaults — defaults+validation؛ لا بنية جديدة (queue=Postgres كما هو).

## 17. Provider Abstractions Impact
QueueProvider يُستخدم فعلياً (تذكيرات/تسليم إشعارات) — تنفيذ Postgres `SKIP LOCKED`؛ **لا Valkey** (بوابة فئة 3 عند حاجة مستقبلية) · لا مزوّدات أخرى.

## 18. Database / Migration Notes
Baseline migrations لجداول platform أعلاه (PR) · أي أعمدة حالة على كيانات apps عبر خط التوليد المحكوم · فهارس على instances/approvals للاستعلامات الساخنة ضمن الاعتماد.

## 19. Testing Strategy (إضافات)
دورة حياة التعريف: كل قفزة غير مشروعة تُرفض (اختبارات حالة) · SoD: الاعتماد الذاتي يفشل · transition بلا صلاحية/شرط يفشل ولا يغيّر شيئاً (atomicity) · at-least-once للتذكيرات مع منع الازدواج المنطقي · rollback تعريف مع instances جارية يعمل بالسياسة · threads: طرف خارجي لا يرى النقاش.

## 20. Acceptance Criteria
1) workflow مستخدمٍ لا يعمل قبل اعتماد شخص مختلف. 2) انتقالات محكومة صلاحيةً وشرطاً وحالةً بإثبات اختباري. 3) زر CTA يظهر ويعمل حسب الصلاحية/الحالة فقط وبأثر معلن. 4) inbox يجمع الاعتمادات والقرارات موثّقة بتعليقات. 5) إشعار+thread لكل بند لأطرافه فقط. 6) مهمة تُولَّد من انتقال وتذكيرها يصل. 7) rollback نسخة تعريف يعمل. 8) كل أحداث §15 مدقَّقة. 9) RTL سليم.

## 21. Risks
حلقات/تعارض تعريفات (تخفيف: Validation يكشف الدورات والحالات الميتة) · انفجار إشعارات (تخفيف: تجميع وتفضيلات) · إغراء أزرار بأثر "كود حر" (مقفول: الأثر المعلن فقط).

## 22. Open Decisions
| OD | الموضوع | التوصية | البوابة |
|---|---|---|---|
| OD-P3-1 | مصفوفة الاعتماد الافتراضية (مَن يعتمد ماذا) | بذرة config قابلة للتحرير من الأدمن؛ الافتراض: مدير الوحدة + دور Governance | Clarify التفعيل |
| OD-P3-2 | مكتبة الـ canvas للـ Builder | v1 بدون مكتبة رسم (قائمة/مخطط بسيط)؛ xyflow لاحقاً بصف ترخيص | قبل أول كود واجهة للـ canvas |
| OD-P3-3 | سياسة الـ instances عند rollback | تكمل على نسختها (grandfathering) | Clarify التفعيل |

## 23. Definition of Done
Baseline المشترك + AC 1–9 خضراء + توثيق Builder/Inbox محدّث + handoff بقائمة "لا يُلمس" (محرك الحالات وعقد approvals) لوكيل P4.

## 24. Coding Agent Prompt
> القالب الموحّد §6 مع: **PHASE=3 · DESIGN=phases/designs/phase-3-workflows-approvals-actions.md · RELEASE=v0.3-phase-design-package** — التزم بأقسام 3/14/22، وتذكّر: لا LLM في هذه المرحلة إطلاقاً.
