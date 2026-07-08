# UI_SCREEN_INVENTORY.md — جرد الشاشات الشامل

> **Version:** 1.2 — Proposed (Δ v1.1: +admin.retrieval_tester من تصميم P5 · Δ v1.2: +runs.list/+runs.detail من UI_RUN_EXECUTION_MODEL v0.6) · **Date:** 2026-07-06 · **الموضع الهدف:** `ui/UI_SCREEN_INVENTORY.md`
> **بنية الجرد:** الحقول الـ15 المطلوبة كاملة، مقسومة لجدولين مترابطين بـ `screen_id` حفاظاً على قابلية القراءة والصيانة: **A = التعريف والتموضع** (screen_id, name, route, phase, audience, type, visible_to_end_user, stitch_prompt_required, priority) · **B = الغرض والحوكمة** (screen_id, purpose, primary_data, main_actions, permissions, audit_events, notes).
> **اصطلاحات:** type ∈ {auth, workspace, queue, renderer, business, admin-config, admin-security, admin-knowledge, admin-models, admin-integrations, admin-ops, ops-read} · stitch = رقم مجموعة G أو «قالب G13» أو «لا (حالة/تبويب)» · الأولوية = ترتيب التصميم في Stitch.
> **قاعدة Dual-Surface في الجرد:** أي عملية سجلات تُذكر مرتين فقط: بطاقة في ws (P6+) وأزرار في الـ Renderer — **نفس action_id**؛ ولا توجد شاشة مخصصة لكل نوع سجل.

## الجدول A — التعريف والتموضع

| screen_id | screen_name | route | phase | audience | type | end_user? | stitch | priority |
|---|---|---|---|---|---|---|---|---|
| auth.login | تسجيل الدخول | /login | 1 | الجميع | auth | ✔ | G2 | High |
| auth.first_login | أول دخول/تغيير كلمة | /first-login | 1 | الجميع | auth | ✔ | G2 | High |
| ws.main | AI Workspace | /workspace | 6 | مستخدم | workspace | ✔ | G3+G4 | High |
| queue.tasks | مهامي | /me/tasks | 3 | مستخدم | queue | ✔ | G8 | High |
| queue.approvals | اعتماداتي | /me/approvals | 3 | مستخدم | queue | ✔ | G8 | High |
| queue.approval_detail | تفصيل بند اعتماد | /me/approvals/{id} | 3 | مستخدم مخوّل | queue | ✔ | G8 | High |
| notif.center | مركز الإشعارات | /me/notifications | 3 | مستخدم | queue | ✔ | G8 | Med |
| projects.main | المشاريع | /projects | 3 | مستخدم | business | ✔ | G8 | Med |
| run.list | Renderer — قائمة كيان | /app/{entity} | 1→2 | مستخدم حسب الصلاحية | renderer | ✔ | قالب G13 | High |
| run.form | Renderer — نموذج إنشاء/تعديل | /app/{entity}/new · /{id}/edit | 1→2 | مستخدم حسب الصلاحية | renderer | ✔ | قالب G13 | High |
| run.detail | Renderer — تفاصيل سجل | /app/{entity}/{id} | 1→2 | مستخدم حسب الصلاحية | renderer | ✔ | قالب G13 | High |
| profile.entity | Entity Profile | /entity/{key} | 2→4 | مستخدم مخوّل | business | ✔ | قالب G13 | Med |
| reports.list | تقاريري | /me/reports | 6 | مستخدم | business | ✔ | G4 | Med |
| reports.review | مراجعة تقرير (رسمي) | /reports/{id}/review | 6 | مراجع/معتمِد | business | ✔ | G4 | High |
| store.catalog | متجر التطبيقات | /store | 7 | مستخدم | business | ✔ | G11 | Med |
| store.connections | ارتباطاتي | /me/connections | 7 | مستخدم | business | ✔ | G11 | Med |
| admin.dashboard | لوحة الأدمن | /admin | 1 | أدمن | admin-config | ✖ | G5 | High |
| admin.users | المستخدمون | /admin/users | 1 | أدمن | admin-security | ✖ | G6 | High |
| admin.user_detail | ملف مستخدم | /admin/users/{id} | 1 | أدمن | admin-security | ✖ | G6 | High |
| admin.org | الهيكل التنظيمي | /admin/org | 1 | أدمن | admin-security | ✖ | G6 | High |
| admin.roles | الأدوار | /admin/roles | 1 | أدمن | admin-security | ✖ | G6 | High |
| admin.permissions | مصفوفة الصلاحيات | /admin/permissions | 1 | أدمن | admin-security | ✖ | G6 | High |
| admin.policies | Policy Studio (ABAC/ReBAC/SoD) | /admin/policies | 4 | سوبر أدمن | admin-security | ✖ | G6 | High |
| admin.classification | التصنيف والحساسية | /admin/classification | 4 | سوبر أدمن | admin-security | ✖ | G6 | Med |
| admin.security_policies | سياسات الأمن | /admin/security | 4 | سوبر أدمن | admin-security | ✖ | G6 | Med |
| admin.features | إدارة المزايا + Safe Mode | /admin/features | 4 | سوبر أدمن | admin-config | ✖ | G5 | Med |
| admin.record_types | Screen/Record-Type Builder | /admin/metadata/screens | 1→2 | أدمن | admin-config | ✖ | G7 | High |
| admin.fields | تعريف الحقول | (تبويب داخل الـ Builder) | 1→2 | أدمن | admin-config | ✖ | لا (تبويب ضمن G7) | High |
| admin.actions | Action Registry | /admin/metadata/actions | 3 | أدمن | admin-config | ✖ | G7 | High |
| admin.navigation | Navigation Registry | /admin/metadata/navigation | 1 | أدمن | admin-config | ✖ | G7 | Med |
| admin.migrations | مراجعة/اعتماد الترحيلات | /admin/migrations | 1 | أدمن معتمِد | admin-config | ✖ | G7 | High |
| admin.generation_docs | توثيق التوليد | /admin/metadata/screens/{id}/docs | 2 | أدمن | admin-config | ✖ | G7 | Med |
| admin.workflows | تعريفات الـ Workflows | /admin/workflows | 3 | أدمن | admin-config | ✖ | G8 | High |
| admin.workflow_detail | تفصيل Workflow ودورة حياته | /admin/workflows/{id} | 3 | أدمن + معتمِد | admin-config | ✖ | G8 | High |
| admin.rag_sources | مصادر المعرفة | /admin/knowledge/sources | 5 | أدمن معرفة | admin-knowledge | ✖ | G9 | High |
| admin.ingestion | مهام المعالجة/الفهرسة | /admin/knowledge/ingestion | 5 | أدمن معرفة | admin-knowledge | ✖ | G9 | High |
| files.manager | إدارة الملفات | /admin/knowledge/files | 5 | أدمن معرفة | admin-knowledge | ✖ | G9 | Med |
| admin.okf | حِزم OKF | /admin/knowledge/okf | 5 | أدمن معرفة | admin-knowledge | ✖ | G9 | Low |
| admin.retrieval_tester | مختبر الاسترجاع (أدمن) | /admin/knowledge/tester | 5 | أدمن معرفة | admin-knowledge | ✖ | G9 | Med |
| runs.list | تشغيلاتي | /me/runs | 6 (يمتد P7) | مستخدم (+مراقب بنطاق) | me-runs | ✖ | G14 | Med |
| runs.detail | تفصيل تشغيل | /me/runs/{id} | 6 (يمتد P7) | مستخدم (+مراقب بنطاق) | me-runs | ✖ | G14 | High |
| admin.capabilities | ربط القدرات بالنماذج | /admin/models/capabilities | 5 | سوبر أدمن | admin-models | ✖ | G10 | High |
| admin.agents | نماذج الوكلاء (per-agent) | /admin/models/agents | 6 | سوبر أدمن | admin-models | ✖ | G10 | Med |
| admin.connectors | الموصلات (تعريف/تفعيل/جمهور) | /admin/integrations/connectors | 7 | سوبر أدمن | admin-integrations | ✖ | G11 | Med |
| admin.audit | عارض التدقيق | /admin/audit | 1 | أدمن مخوّل | admin-ops | ✖ | G12 | High |
| admin.logs | عارض السجلات (بقناع) | /admin/logs | 1 | أدمن مخوّل | admin-ops | ✖ | G12 | Med |
| admin.health | الصحة التفصيلية | /admin/health | 0→1 | أدمن/Ops | admin-ops | ✖ | G12 | Med |
| admin.error_catalog | كتالوج الأخطاء | /admin/errors | 1 | أدمن | admin-ops | ✖ | G12 | Low |
| admin.config_profiles | البروفايلات والأعلام (قراءة) | /admin/config | 1 | أدمن/Ops | admin-ops | ✖ | G12 | Low |
| ops.status | سطح التشغيل (قراءة) | /ops | 8 | Ops | ops-read | ✖ | G12 | Med |
| about.licenses | About / Attribution | /about | 8 | الجميع | ops-read | ✔ | G12 | Low |

## الجدول B — الغرض والحوكمة

| screen_id | purpose | primary_data | main_actions | permissions | audit_events | notes |
|---|---|---|---|---|---|---|
| auth.login | دخول آمن | جلسة | auth.login | عام | AUTH_LOGIN / AUTH_FAILED | حالات القفل/الخطأ ضمن الشاشة |
| auth.first_login | فرض تغيير الكلمة | credentials | auth.change_password | جلسة أولى | AUTH_PASSWORD_CHANGED | سياسة الكلمة من OD-P1-1 |
| ws.main | السطح المحادثي المركزي | sessions/messages/citations/action-proposals | كل الأفعال عبر Action Cards (record.* / report.generate / workflow.submit / file.ingest / task.create / source.open …) | صلاحيات كل action_id عند التنفيذ | CHAT_ANSWER_SERVED · VALIDATION_BLOCKED · +أحداث كل action منفَّذ | حالات أولى: PERMISSION_DENIED / INSUFFICIENT_EVIDENCE / EXEC_ERROR — بطاقة نتائج &gt;10 صفوف تُحوَّل إلى run.list (OD-UX-4)؛ لوحة audit للمخوّلين |
| queue.tasks | إنجاز المهام | tasks | task.update_status · task.open_target | tasks.view_own | TASK_COMPLETED… | تفاصيل المهمة درج داخلي |
| queue.approvals | صندوق الاعتمادات | approval_items | approve/reject/return | approvals.decide | APPROVAL_DECIDED | البنود من workflows وHITL (P7) معاً |
| queue.approval_detail | قرار رسمي + نقاش | البند + thread + الأثر | workflow.approve/reject/return · thread.post | approvals.decide + طرف البند | APPROVAL_DECIDED · THREAD_POSTED | الرفض بتعليق إلزامي؛ سطح ثابت للمراجعة |
| notif.center | متابعة الإشعارات | notifications+threads | mark_read · thread.post · open_target | ذاتي | NOTIFICATION_READ(للحساس) | لوحة مصغّرة داخل ws |
| projects.main | تجميع العمل | projects/members/links | project.create · link.add · member.manage | projects.* | PROJECT_CHANGED | ربط الملفات يظهر من P5 |
| run.list | قائمة أي كيان (حتمي) | صفوف الكيان (RLS-مرشّحة) | record.create(زر) · record.search/filter/export† | records.{entity}.read (+export بسياسة P4†) | RECORD_EXPORTED† | †التصدير يظهر من P4؛ **المكافئ المحادثي: بطاقة بحث/إنشاء في ws (P6+) بنفس action_id** |
| run.form | إنشاء/تعديل (حتمي) | حقول من schema | record.create / record.update | records.{entity}.create/update | RECORD_CREATED/UPDATED | نفس التحققات التي تستخدمها بطاقة المعاينة (A-UX-4) |
| run.detail | عرض سجل + أفعاله | السجل + FLS-مقنَّع + أزرار Action Registry | record.update/delete · workflow.submit · action.custom | حسب كل action_id | RECORD_* · INSTANCE_TRANSITIONED | لوحة audit جانبية بصلاحية؛ الأزرار نفسها تظهر بطاقاتٍ في ws |
| profile.entity | الملف المجمّع لكيان | مصادر الملف (مشذّبة) | profile.view · open_source_record | entity_profile.view (+الأشد) | ENTITY_PROFILE_VIEWED(للحساس) | التجميع لا يتجاوز صلاحيات الناظر |
| reports.list | حالة تقاريري | reports+versions | report.open · report.export† | reports.view_own (+سياسة تصدير) | REPORT_EXPORTED† | الإنشاء يبدأ من ws (Action Card) |
| reports.review | مراجعة قسمية واعتماد | أقسام+استشهادات | report.approve/return · section.regenerate‡ | reports.review | REPORT_REVIEWED/APPROVED | ‡إعادة توليد قسم = action محكوم؛ قسم بلا مصدر يفشل آلياً |
| store.catalog | اكتشاف المسموح | connectors/apps مرشّحة | app.enable_for_me · link.start | store.view (+جمهور الموصل) | LINK_CREATED | لا يظهر غير المسموح إطلاقاً |
| store.connections | إدارة ارتباطاتي | account_links | link.renew/revoke | ذاتي | LINK_REVOKED | الرموز لا تُعرض أبداً |
| admin.dashboard | مدخل الإدارة | مؤشرات مختصرة | تنقّل | admin.access | — | بلا أرقام حساسة افتراضياً |
| admin.users | إدارة الحسابات | users | user.create/disable/reset | admin.users.manage | USER_CREATED/DISABLED/RESET | الثوابت immutable ظاهرة كقفل |
| admin.user_detail | حساب واحد + أدواره | user+roles+relations | role.assign/revoke · rebac.grant(P4) | admin.users.manage | ROLE_ASSIGNED/REVOKED | يعرض قرارات صلاحية أخيرة (مفسّر P4) |
| admin.org | الشجرة التنظيمية | org_units/membership | org.unit_create/move · membership.change | admin.org.manage | ORG_CHANGED | سحب-إفلات ضمن قواعد |
| admin.roles | تعريف الأدوار | roles | role.create/edit | admin.roles.manage | ROLE_CHANGED | SoD يمنع التعارض (P4) |
| admin.permissions | المصفوفة الأساسية | permissions_matrix | permission.grant/revoke | admin.permissions.manage | PERMISSION_CHANGED | القرارات المفسَّرة تظهر هنا وفي user_detail |
| admin.policies | سياسات مركّبة | abac/rebac/sod | policy.create/edit/simulate | admin.policies.manage | POLICY_CHANGED · PERMISSION_SIMULATED | بنية شرطية معلنة — لا تعبيرات حرة |
| admin.classification | درجات التصنيف | classifications | classification.assign | admin.classification.manage | CLASSIFICATION_CHANGED | «الأشد يسود» مرئي |
| admin.security_policies | جلسات/قفل/تصدير | security policies | security.policy_update | admin.security.manage | SECURITY_POLICY_CHANGED | ضمن حدود config (D9) |
| admin.features | تفعيل/تعطيل قدرات | flags+manifest deps | feature.enable/disable · safe_mode.enter/exit | admin.features.manage (SafeMode=Ops) | FEATURE_ENABLED/DISABLED · SAFE_MODE_* | قائمة A10 رمادية ويرفضها الخادم |
| admin.record_types | بناء الأنواع والشاشات | screen_definitions+versions | screen.define/version · policy.set(RLS/FLS) | admin.metadata.manage | SCREEN_DEFINED/VERSIONED · SCREEN_POLICY_CHANGED | مصدر schema للسطحين معاً |
| admin.fields | خصائص الحقول | field_definitions | field.add/edit | admin.metadata.manage | (ضمن أحداث الشاشة) | تبويب داخل الـ Builder |
| admin.actions | تعريف الأزرار/الأفعال | action_buttons registry | action.define/edit (أثر معلن فقط) | admin.actions.manage | ACTION_DEFINED/CHANGED | **قلب Dual-Surface** — الزر يُعرض على السطحين |
| admin.navigation | قوائم التنقّل | navigation_items | nav.add/reorder | admin.metadata.manage | NAV_CHANGED | صلاحية لكل عنصر |
| admin.migrations | بوابة اعتماد الترحيلات | proposals+risk report | migration.check/approve/apply/rollback | admin.migrations.approve (≠ المقترِح) | MIGRATION_PROPOSED/APPROVED/APPLIED/ROLLED_BACK | SoD مدمج؛ لا apply لغير المعتمد |
| admin.generation_docs | تاريخ التوليد | versions+diffs+approvers | docs.view | admin.metadata.view | — | قراءة توثيقية |
| admin.workflows | حوكمة التعريفات | workflow_definitions | wf.define/validate/submit | admin.workflows.manage | WORKFLOW_DEFINED/VALIDATED | التفعيل يتطلب معتمِداً غير المعرِّف |
| admin.workflow_detail | التعريف التفصيلي | states/transitions/assignees | wf.approve/activate/rollback | wf.approve (SoD) | WORKFLOW_APPROVED/ACTIVATED/ROLLED_BACK | canvas مبسّط v1 (OD-P3-2) |
| admin.rag_sources | مصادر الفهرسة | sources+scopes | source.add/enable/rescope | admin.knowledge.manage | SOURCE_CHANGED | النطاق يحدد وسوم الصلاحية للفهرسة |
| admin.ingestion | خط المعالجة | ingestion_jobs+steps | job.retry/cancel | admin.knowledge.manage | INGESTION_RETRIED/FAILED | حالة كل خطوة + error_code |
| files.manager | حوكمة الملفات | files+versions+classification | file.reclassify · file.delete | admin.files.manage | FILE_RECLASSIFIED/DELETED | رفع المستخدم من ws/renderer لا من هنا |
| admin.okf | حِزم المعرفة المحلية | okf_bundles | okf.load/disable | admin.knowledge.manage | OKF_BUNDLE_LOADED | موسومة «ليست مصدر حقيقة» |
| admin.retrieval_tester | فحص جودة الاسترجاع وقرار الكفاية (No-Guessing) قبل التشغيل وأثناءه | استعلام تجريبي + النتائج + provenance + قرار العتبة | rag.simulate_query | admin.knowledge.manage | RAG_QUERY_SIMULATED | لا يتجاوز صلاحيات المُجرِّب؛ أُضيفت استكمالاً من تصميم P5 §13 (Δ v1.1) |
| runs.list | متابعة تشغيلات المستخدم (تقارير/خطوط/تسلسلات موصلات) وحالاتها | التعريف · الحالة · التقدم x/y · المدة · النوع | run.start (إطلاق جديد) · run.cancel (من الصف) | runs.read (ملكية + نطاق) · runs.start | RUN_STARTED · RUN_CANCELLED | RLS بالمُطلِق؛ **ليست terminal ولا سطح تنفيذ حر** (Δ v1.2) |
| runs.detail | مراقبة تنفيذ محكوم: خط زمني · بوابات اعتماد/HITL · أدلة/مخرجات · إعادة/إلغاء | خطوات وحالاتها · عقد البوابات · لوحة المخرجات · سلسلة correlation | run.cancel · run.retry(+_step) · version.compare · فتح البند (queue) | runs.read/cancel/retry · تبويب التدقيق audit-visible | مجموعة RUN_* (المواصفة §10) | يقرأ سلسلة التدقيق القائمة (مصدر واحد)؛ القرارات على queue.approval_detail (Δ v1.2) |
| admin.capabilities | توجيه القدرات | capability_bindings | binding.change · provider.test_connection | admin.models.manage (+approval بالإنتاج) | CAPABILITY_BINDING_CHANGED | بلا endpoints/secrets (D9)؛ خطة إعادة فهرسة عند تغيير embedding |
| admin.agents | نماذج الوكلاء | agent_bindings+params | agent.binding_change | admin.models.manage (+approval) | AGENT_BINDING_CHANGED | fallback ظاهر لكل وكيل |
| admin.connectors | إدارة الموصلات | connectors+tools+risk | connector.enable/disable · audience.set · hitl.policy_set | admin.integrations.manage | CONNECTOR_ENABLED/DISABLED | الأسرار Ops فقط؛ صحة الموصل ظاهرة |
| admin.audit | البحث في التدقيق | audit_log | audit.search/filter/export† | audit.view (نطاقي) | AUDIT_EXPORTED† | permission-aware؛ لا يرى الناظر خارج نطاقه |
| admin.logs | تشخيص تقني | JSON app logs | logs.search | logs.view | — | قناع أسرار إلزامي |
| admin.health | صحة التبعيات | health endpoints | health.refresh | health.view | — | يعرض المطفأ disabled بوضوح |
| admin.error_catalog | مرجع الأخطاء | error codes | catalog.view | admin.access | — | يتحدث مع كل feature |
| admin.config_profiles | شفافية الإعداد | profiles/flags الحالية | view فقط | admin.config.view | — | **قراءة فقط** — التغيير config/Ops (D9) |
| ops.status | تشغيل للقراءة | backups/versions/connectors | view · runbook.open | ops.view | — | لا أزرار lifecycle |
| about.licenses | الشفافية القانونية | attribution من license-review | view | عام | — | تكتمل آلياً (P8) |

## ملاحظات إقفال الجرد
1) **لا شاشات لكل نوع سجل** — أي طلب مستقبلي لشاشة كيان يُلبّى بتعريف metadata يلبس قوالب G13، لا بتصميم جديد. 2) عمليات المستخدم على السجلات لها دائماً السطحان (ws-card + renderer) بنفس `action_id` — أي إضافة مستقبلية تُسجَّل في `admin.actions` فتظهر تلقائياً على السطحين. 3) الشاشات ذوات الأولوية High = نطاق دفعات Stitch الأولى. 4) هذا الجرد مرجع `UI_SCREEN_CARDS_BY_PHASE.md` (دفعة 3) و`UI_STITCH_PROMPTS_BY_PHASE.md` (دفعة 4).
