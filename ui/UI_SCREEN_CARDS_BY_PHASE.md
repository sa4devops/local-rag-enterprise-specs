# UI_SCREEN_CARDS_BY_PHASE.md — بطاقات الشاشات حسب المراحل

> **Version:** 1.0 — Proposed · **Date:** 2026-07-06 · **الموضع الهدف:** `ui/UI_SCREEN_CARDS_BY_PHASE.md` · +runs (Δ ما-بعد الدمج 2026-07-08)
> **المراجع الحاكمة:** PHASE_MASTER_PLAN + designs/phase-1..8 (الترتيب **ثابت لا يُمس**) · UI_SCREEN_INVENTORY (المعرّفات) · نماذج الدفعة الثانية.
> **الغرض:** بطاقة موجزة لكل شاشة (جديدة New / مطوَّرة Enh) في مرحلتها، بربط الأفعال والصلاحيات وأحداث التدقيق — **مدخلات مباشرة لدفعة الـ Stitch prompts**. لا تنفيذ الآن؛ التنفيذ ببطاقات مهام عند تفعيل كل مرحلة.

## 0) تطوّر «بيت المستخدم» والأسطح (الخلاصة الزمنية)
| المرحلة | أسطح المستخدم النهائية المتاحة | البيت الافتراضي |
|---|---|---|
| P0 | لا شيء (صفحة صحة تقنية فقط) | — |
| P1–P2 | Runtime Renderer (run.*) + profile.entity(P2) عبر تنقّل مرشّح | بوابة تنقّل بسيطة (الشاشات المسموحة) |
| P3–P5 | + Work Queue (queue.* / notif / projects) (+مرفقات فعلية P5) | **queue.tasks** |
| P6+ | + **ws.main** + reports | **ws.main** (علَم لكل دور — OD-UX-1) |

**خيط العقود (لماذا لا يتغير الترتيب):** P1/P2 يبنيان **schema الحقول والتحققات وRLS/FLS** — وهي ذاتها التي تولّد بطاقات معاينة الـ Workspace في P6 (A-UX-4) · P3 يبني **عقود الأفعال** التي تظهر أزراراً في الـ Renderer فوراً وبطاقاتٍ في الدردشة لاحقاً **بنفس action_id** · P4 سياساته تشذّب كل السطوح · P5 استرجاعه يغذّي إجابات P6. **الـ Workspace في P6 لا يضيف حوكمة جديدة — يركّب ما بُني.**

## Phase 0 — أساس تقني (لا شاشات مستخدم)
| screen_id | حالة | أبرز العناصر | action_ids | permissions | audit_events | Stitch |
|---|---|---|---|---|---|---|
| admin.health (v0) | New | بلاطات الفعّال/المطفأ (disabled بوضوح) | health.refresh | health.view | — | G12 |

يُزرع هنا أيضاً: قشرة i18n/RTL + رموز التصميم — لا واجهة أعمال.

## Phase 1 — Governed Core + Screen Builder
| screen_id | حالة | أبرز العناصر | action_ids | permissions | audit_events | Stitch |
|---|---|---|---|---|---|---|
| auth.login + auth.first_login | New | دخول + حالات القفل/الخطأ + فرض تغيير الكلمة | auth.login · auth.change_password | عام | AUTH_LOGIN/FAILED · AUTH_PASSWORD_CHANGED | G2 |
| admin.dashboard | New | مدخل + مؤشرات دنيا (OD-AC-1) | تنقّل | admin.access | — | G5 |
| admin.users + user_detail | New | حسابات + ثوابت مقفلة + أدوار | user.create/disable/reset · role.assign/revoke | admin.users.manage | USER_* · ROLE_* | G6 |
| admin.org · admin.roles · admin.permissions | New | الشجرة/الأدوار/المصفوفة الأساسية | org.* · role.* · permission.grant/revoke | admin.org/roles/permissions.manage | ORG_/ROLE_/PERMISSION_CHANGED | G6 |
| admin.record_types (v1) | New | تعريف نوع/شاشة بالحقول الأساسية | screen.define/version | admin.metadata.manage | SCREEN_DEFINED/VERSIONED | G7 |
| **admin.migrations** | New (حرجة) | الاقتراح + تقرير المخاطر + الاعتماد (SoD) | migration.check/approve/apply/rollback | admin.migrations.approve (≠المقترِح) | MIGRATION_* | G7 |
| admin.navigation | New | عناصر التنقّل بصلاحية لكل عنصر | nav.add/reorder | admin.metadata.manage | NAV_CHANGED | G7 |
| run.list / run.form / run.detail (v1) | New | Renderer الحتمي الأساسي (أنواع P1) | record.create/update/delete/search (أساسي) | records.{e}.* | RECORD_* | **G13 قوالب** |
| مجموعة الرقابة: admin.audit · admin.logs · admin.error_catalog · admin.config_profiles(ro) | New | عارضات التدقيق/السجلات/الأخطاء/الإعداد-قراءة | audit.search · logs.search | audit.view · logs.view · admin.config.view | AUDIT_EXPORTED† | G12 |

**عقود تُبنى هنا:** schema v1 + خط التوليد + Audit spine — أساس كل السطوح اللاحقة.

## Phase 2 — Advanced Screens, Records &amp; Entity Profile v1
| screen_id | حالة | أبرز العناصر | action_ids | permissions | audit_events | Stitch |
|---|---|---|---|---|---|---|
| admin.record_types (v2) | Enh | كل الأنواع + تبويب الحقول + سياسات RLS/FLS | screen.define/version · policy.set | admin.metadata.manage | SCREEN_POLICY_CHANGED | G7 |
| run.* (v2) | Enh | list engine كامل + قناع FLS + استعادة | record.search المتقدم · record.restore | records.{e}.read/restore | RECORD_RESTORED | G13 |
| admin.generation_docs | New | النسخ/الفروق/المعتمِدون | docs.view | admin.metadata.view | — | G7 |
| profile.entity (v1) | New | تجميع للقراءة مشذَّب بالناظر | profile.view · open_source_record | entity_profile.view | ENTITY_PROFILE_VIEWED† | G13 |

**عقود تُبنى هنا:** schema المكتمل + العزل صفاً/حقلاً — **هو مصدر بطاقات المعاينة في P6 حرفياً**.

## Phase 3 — Workflows, Approvals &amp; Action Buttons (البيت ⇒ queue.tasks)
| screen_id | حالة | أبرز العناصر | action_ids | permissions | audit_events | Stitch |
|---|---|---|---|---|---|---|
| queue.tasks · notif.center · projects.main | New | مهامي/الإشعارات(+threads)/المشاريع | task.* · thread.post · project.* | tasks.view_own · projects.* | TASK_* · PROJECT_CHANGED | G8 |
| queue.approvals + queue.approval_detail | New | الصندوق + سطح القرار الرسمي | workflow.approve/reject/return | approvals.decide (SoD) | APPROVAL_DECIDED · THREAD_POSTED | G8 |
| **admin.actions** | New | **Action Registry** (عقد الفعل كاملاً) | action.define/edit · action.simulate_visibility | admin.actions.manage | ACTION_* | G7 |
| admin.workflows + workflow_detail | New | التعريف + دورة الحياة التسعينية + الاعتماد | wf.define/validate/submit/approve/activate/rollback | admin.workflows.manage · wf.approve | WORKFLOW_* | G8 |
| run.detail | Enh | **أزرار الـ Registry تظهر على السطح الحتمي** | حسب العقود | حسب العقد | INSTANCE_TRANSITIONED | G13 |

**ملاحظة توفيقية موثَّقة:** تصميم P3 أشار لإعداد الأزرار «داخل الـ Builder»؛ حزمة الواجهة تُفرد `admin.actions` مستقلةً مع نقطة دخول من الـ Builder — يُثبَّت في Clarify تفعيل P3 (لا أثر معمارياً: نفس الـ Registry).

## Phase 4 — Advanced Permissions &amp; Feature Management
| screen_id | حالة | أبرز العناصر | action_ids | permissions | audit_events | Stitch |
|---|---|---|---|---|---|---|
| admin.policies | New | ABAC/ReBAC/SoD + محاكاة «ماذا يرى X؟» | policy.create/edit · permissions.simulate | admin.policies.manage | POLICY_CHANGED · PERMISSION_SIMULATED | G6 |
| admin.classification · admin.security_policies | New | الدرجات الخمس + جلسات/قفل/تصدير | classification.assign · security.policy_update | admin.classification/security.manage | CLASSIFICATION_/SECURITY_POLICY_CHANGED | G6 |
| admin.features | New | المزايا + التبعيات + Safe Mode + A10 رمادية | feature.enable/disable · safe_mode.enter/exit | admin.features.manage (SafeMode=Ops) | FEATURE_* · SAFE_MODE_* | G5 |
| profile.entity | Enh | كامل + خط زمني + «الأشد يسود» | — | (+NtK) | ENTITY_PROFILE_VIEWED | G13 |
| run.* | Enh | شارات تصنيف + **تصدير محكوم** | record.export | + سياسة تصدير P4 | RECORD_EXPORTED | G13 |
| admin.user_detail · admin.audit | Enh | ReBAC + مفسّر القرار / لوحات محاكاة | rebac.grant · permissions.simulate | admin.users/policies.manage | RELATION_GRANTED | G6/G12 |

## Phase 5 — Knowledge: Files, RAG, OCR &amp; Media
| screen_id | حالة | أبرز العناصر | action_ids | permissions | audit_events | Stitch |
|---|---|---|---|---|---|---|
| admin.rag_sources · admin.ingestion · files.manager · admin.okf | New | المصادر/مراقبة الخط/حوكمة الملفات/OKF | source.* · job.retry/cancel · file.reclassify/delete · okf.load | admin.knowledge/files.manage | SOURCE_/INGESTION_/FILE_/OKF_* | G9 |
| **admin.retrieval_tester** | New (Δ على الجرد — من تصميم P5) | استعلام تجريبي + provenance + قرار الكفاية | rag.simulate_query | admin.knowledge.manage | RAG_QUERY_SIMULATED | G9 |
| admin.capabilities | New | capability→model + fallback + خطة إعادة فهرسة | capability.binding_change · provider.test_connection | admin.models.manage (+approval بالإنتاج) | CAPABILITY_BINDING_CHANGED | G10 |
| run.form/detail · notif.center | Enh | مرفقات فعلية + حالات معالجة | file.ingest | files.upload | FILE_UPLOADED · INGESTION_* | G13/G8 |

## Phase 6 — Intelligence: Workspace, Reports, Agents (البيت ⇒ ws.main)
| screen_id | حالة | أبرز العناصر | action_ids | permissions | audit_events | Stitch |
|---|---|---|---|---|---|---|
| **ws.main** | New | الخط S1–S9 كاملاً + الاستشهادات + SQL panel + الوضع الحتمي | **كل عقود P3 كبطاقات** + record.search · report.generate · source.open | حسب كل عقد | CHAT_ANSWER_SERVED · VALIDATION_BLOCKED · +أحداث الأفعال | G3+G4 |
| reports.list + reports.review | New | تقاريري + المراجعة القسمية بالاستشهاد والاعتماد | report.generate/approve/return · section.regenerate | reports.* | REPORT_* | G4 |
| admin.agents | New | per-agent bindings + معاملات + fallback | agent.binding_change | admin.models.manage (+approval) | AGENT_BINDING_CHANGED | G10 |
| run.list | Enh | استقبال الفلاتر المسلسلة من بطاقات النتائج | record.search | records.{e}.read | — | G13 |
| runs.list | — | مراقبة تشغيلات المستخدم (قائمة) | — | — | — | G14 |
| runs.detail | — | الخط الزمني والبوابات والأدلة | — | — | — | G14 |

> (Δ ما-بعد الدمج: الصفان مضافان اتساقاً مع الجرد v1.2 و`UI_RUN_EXECUTION_MODEL.md`؛ يمتدان إلى P7.)

**نقطة الالتقاء:** هنا تركّب واجهة P6 عقودَ P1/P2 (schema) وP3 (actions) وP4 (سياسات) وP5 (استرجاع) — دون أي حوكمة جديدة.

## Phase 7 — Integrations &amp; App Store
| screen_id | حالة | أبرز العناصر | action_ids | permissions | audit_events | Stitch |
|---|---|---|---|---|---|---|
| store.catalog + store.connections | New | المتجر المرشّح + ربط/إلغاء حساباتي | app.enable_for_me · link.start/renew/revoke | store.view + جمهور الموصل | LINK_* | G11 |
| admin.connectors | New | القدرات/الخطورة/الجمهور/سياسة HITL — بلا أسرار | connector.enable/disable · audience.set · hitl.policy_set | admin.integrations.manage | CONNECTOR_* | G11 |
| ws.main · queue.approvals · notif.center | Enh | بطاقات الأدوات + **HITL preview/موافقة** + أحداث webhooks | connector.tool.read/act | المنصة ∩ الحساب المربوط | INVOCATION_* · WEBHOOK_RECEIVED | G3/G8 |

## Phase 8 — Production Readiness
| screen_id | حالة | أبرز العناصر | action_ids | permissions | audit_events | Stitch |
|---|---|---|---|---|---|---|
| ops.status | New | نسخ/إصدارات/صحة موصلات — قراءة | view · runbook.open | ops.view | — | G12 |
| about.licenses | New | Attribution آلي من license-review | view | عام | — | G12 |
| admin.health + لافتات الصيانة | Enh | تنبيهات + maintenance banner | health.refresh | health.view | ALERT_RAISED · MAINTENANCE_MODE_CHANGED | G12 |

## قواعد إقفال
1) الترتيب المعتمد ثابت — هذا الملف يعرضه ولا يعدّله. 2) أي شاشة جديدة مستقبلاً تدخل الجرد أولاً ثم بطاقتها هنا. 3) الأولويات High في الجرد = ترتيب مجموعات Stitch في الدفعة الرابعة. 4) لا تنفيذ من هذا الملف — التنفيذ ببطاقات مهام كل مرحلة عند تفعيلها.
