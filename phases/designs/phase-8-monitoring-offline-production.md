# Phase 8 — Production Readiness: Observability, Offline Packaging &amp; Hardening

الحالة: Accepted v0.3 (2026-07-06) — مدخل تصميم ما-قبل-الأساس (استُعيد 2026-07-10 ضمن إغلاق F-3). هذه الوثيقة هي تصميم المرحلة المعتمد تاريخياً والموطن التعريفي لمعرفات FR الخاصة بها. عند تفعيل المرحلة يُنتَج «تصميم التفعيل» النهائي وفق قاعدة phase-roadmap بادئاً من هذه الوثيقة؛ وكل ما استجد في حزم v0.4 حتى v1.0-architecture-baseline والـ ADRs يعلوها عند أي تعارض (سلسلة م20). لا تنفيذ مباشر من هذه الوثيقة دون بطاقة مهمة وتصميم تفعيل.

> **Version:** 1.0 — Proposed (Accepted باعتماد v0.3) · **Date:** 2026-07-06 · **Authority عند الاعتماد:** المرتبة 6
> **Inherits:** Common Phase Baseline — PHASE_MASTER_PLAN §4. **Predecessor:** Phase 7 بكامل DoD. بطاقات المهام عند التفعيل.
> **بوابات دخول (فئة 4 — قبل التوزيع):** موقف AGPL النهائي · أوزان النماذج (بوابة 2: التضمين في الحزمة) · TLS/PKI + آلية توقيع الحزمة · اكتمال Attribution/About. **وفئة 3** لأي صورة مراقبة تُفعَّل.

## 1. Purpose
إثبات وعد المشروع نهائياً: منظومة مكتملة الوظائف تُراقَب بخط أساس موسَّع، وتُحزَّم **offline موقَّعة** وتُستعاد وتُرقَّى من Local إلى Production **بالإعداد فقط** — مع تصلّب أمني وجاهزية HA، وواجهة Ops ضمن حدود D9.

## 2. Scope
Observability: تفعيل /metrics افتراضاً في الإنتاج + قرار مكوّنات المراقبة (Prometheus-server/بديل، لوحات) **بعد المراجعة القانونية** (Grafana/Loki=Legal؛ بدائل Apache-2 مرشّحة) + OTel adapter اختياري · Ops Surface (قراءة): حالة الخدمات/الصحة/الإصدارات/آخر نسخ احتياطي + روابط runbooks — **دورة حياة الحاويات تبقى خارج الواجهة (D9)** · **Offline Bundle Builder**: حزمة نقل (صور بـ digests، wheels/uv cache، pnpm store، أوزان معتمدة-بوابة2، configs examples، install/verify scripts، docs/handoff) + **توقيع وتحقق** · Backup/Restore منفَّذة ومُجرَّبة: PG (القواعد الأربع) + ObjectStorage + استراتيجية الفهارس (استعادة أو إعادة بناء معلنة) + تمرين استعادة موثَّق · **Promotion Rehearsal**: ترقية Local→Production عبر profiles فقط، موثّقة خطوة-خطوة كإجراء (لا سكربتات داخل الوثيقة) · HA Readiness: replicas للـ api/workers، PgBouncer، فصل GPU nodes — **كلها config** + وثيقة sizing · Security Hardening Pass: رؤوس أمان، حدود معدل عامة، مراجعة أسرار، فحص تبعيات بثغرات معروفة ضمن CI (بأداة معتمدة الصف) · إغلاق فئة 4 + شاشة About/Attribution مكتملة من license-review · (اختياري معلَّق) مسار تفعيل Graph موثَّق دون تفعيله · runbooks: troubleshooting / backup-restore / offline-install / promotion.

## 3. Out of Scope
K8s/OpenShift manifests (Backlog — الانتقال لاحقاً بلا تعديل كود) · Git داخلي (Backlog) · مراقبة SaaS خارجية · أدوات أمن هجومية بالمتجر (Backlog بقرار) · أي ميزة وظيفية جديدة للمستخدم.

## 4. Required Inputs
P7 DoD · هذا التصميم Accepted · قرارات فئة 4 مقفلة · اختيار مكوّنات المراقبة بعد Legal · بيئة production-like للتمرين.

## 5. Expected Outputs
حزمة نقل موقَّعة قابلة للتثبيت المغلق والتحقق؛ استعادة كاملة ناجحة موثَّقة؛ ترقية config-only مُثبتة بتقرير؛ مراقبة وتنبيه أساسي يعملان؛ منصة مصلَّبة جاهزة للتسليم.

## 6. Functional Requirements
| # | المتطلب |
|---|---|
| FR-8.1 | تجميع مقاييس المنصة عبر /metrics لكل عملية + مقاييس أعمال أساسية (طوابير/فهرسة/بوابات) خلف علم. |
| FR-8.2 | مكوّن مراقبة/لوحات معتمد المراجعة يعرضها + تنبيهات أساسية (صحة/امتلاء/فشل نسخ) — أو تأكيد الاكتفاء بالخط الأساسي بقرار موثَّق. |
| FR-8.3 | Ops Surface للقراءة: صحة مفصّلة، إصدارات، حالة النسخ، مؤشرات الموصلات — بلا أزرار lifecycle. |
| FR-8.4 | Bundle Builder: تجميع كل المكوّنات بمداخل موقَّعة (manifest بالـ digests) + أداة تحقق قبل التثبيت. |
| FR-8.5 | Backup مجدول (config) للقواعد الأربع + التخزين + نسخ الميتاداتا الحرجة؛ وRestore إجراء مُختبر بتمرين حقيقي. |
| FR-8.6 | Promotion: production profile يجتاز validation ويشغّل نفس الصور بالإعداد فقط؛ تقرير تمرين موثَّق. |
| FR-8.7 | HA: تشغيل api/workers بنسخ متعددة خلف موازن (config) دون كسر الجلسات (JWT) — يُثبت بتجربة. |
| FR-8.8 | Hardening: رؤوس/معدل/مراجعة أسرار/فحص ثغرات تبعيات في CI (أداة بصف ترخيص). |
| FR-8.9 | About/Attribution مكتملة آلياً من license-review (كل Approved/Conditional له سطره). |
| FR-8.10 | Runbooks الأربعة مكتملة ومختبرة بمن ينفّذها غير كاتبها. |

## 7. NFRs (الخاصة)
زمن استعادة مستهدف موثَّق (يُقاس بالتمرين) · حجم الحزمة وخطوات تثبيتها موثَّقان · فقدان مقبول (RPO) معلن من جدولة النسخ.

## 8. User Stories
بصفتي موظفاً: لا يتغير شيء في تجربتي بعد الترقية — نفس النظام أسرع/أثبت · أرى إشعار صيانة مجدولة قبلها.

## 9. Admin Stories
بصفتي Ops: أبني حزمة النقل وأتحقق من توقيعها · أنفّذ استعادة كاملة على بيئة تجربة بنجاح موثَّق · أرقّي بالإعداد فقط وأوقّع تقرير التمرين · أرى التنبيه عند فشل نسخة احتياطية. بصفتي SuperAdmin: أفتح About فأجد كل التراخيص والإسنادات.

## 10. Main Modules + Epics
**Modules:** monitoring(توسعة) · backup-restore · service-registry(نضج) · ops-surface (ضمن admin بحدود D9) (+scripts تحت infrastructure/ كأصول تنفيذ لاحقاً).
**Epics:** E8.1 Metrics+Alerts → E8.2 Monitoring Component (بعد Legal) → E8.3 Ops Surface → E8.4 Bundle Builder+Signing → E8.5 Backup/Restore+Drill → E8.6 Promotion Rehearsal → E8.7 HA Enablement → E8.8 Hardening+Dep-Scan → E8.9 Attribution/About → E8.10 Runbooks+Handoff النهائي.

## 11. Data Model Notes
backup_catalog(runs,status,checksums) · bundle_manifests(digests,signature-ref) · ops_status views — platform_db؛ لا بيانات أعمال جديدة.

## 12. API Notes
/metrics (علَم) · /ops/status/* (قراءة) · /backups/* (سجل/حالة — التشغيل جدولة config) · /about/licenses — خلف صلاحيات Ops/SuperAdmin.

## 13. UI Notes
Ops dashboard (قراءة) · Backup status · About/Attribution · لافتة وضع الصيانة — RTL.

## 14. Security &amp; Permissions
أسطح Ops خلف أدوار Ops/SuperAdmin حصراً · /metrics و/health في الإنتاج خلف حماية شبكية/صلاحية · لا سر يظهر في أي شاشة/سجل · التوقيع/المفاتيح بيد Ops خارج التطبيق.

## 15. Audit &amp; Logging
backup.run/succeeded/failed · restore.performed(بيئة/نتيجة) · bundle.built/verified · promotion.rehearsed(تقرير) · maintenance.mode_changed · alert.raised — إضافة لسجلات المراحل كلها.

## 16. Configuration / Environment Impact
BACKUP_SCHEDULE/RETENTION · METRICS_ENABLED=true(prod) · ALERT_* · MAINTENANCE_MODE flag محمي · production profile مفعَّل فعلياً — كل الفروق بالإعداد حصراً (constitution م5).

## 17. Provider Abstractions Impact
لا مزوّدات جديدة · إن فُعِّلت Valkey/S3 هنا لأحمال الإنتاج ⇒ ببوابة فئة 3 + Provider-Equivalence tests قبل الاعتماد.

## 18. Database / Migration Notes
لا تغييرات كيانات · جداول platform التشغيلية أعلاه عبر baseline · تمرين الاستعادة يشمل التحقق من migrations state.

## 19. Testing Strategy (إضافات)
تمرين استعادة كامل = اختبار قبول (وليس وثيقة) · تحقق الحزمة يرفض حزمة مُعدَّلة (توقيع/digest) · promotion rehearsal بنجاح validation وتشغيل كامل · اختبار HA (إسقاط نسخة api لا يقطع الخدمة) · فحص الثغرات في CI أخضر أو مستثنى بقرار موثَّق · no-external-call يسري على كل الجديد.

## 20. Acceptance Criteria
1) حزمة موقَّعة تُثبَّت مغلقاً وتجتاز التحقق. 2) استعادة كاملة ناجحة موثَّقة بتوقيت. 3) ترقية Local→Prod بالإعداد فقط مُثبتة بتقرير. 4) HA للـ api/workers مُثبت عملياً. 5) مراقبة/تنبيه أساسي يعملان (أو قرار اكتفاء موثَّق). 6) About مكتملة من السجل. 7) بنود فئة 4 كلها مقفلة. 8) runbooks مختبرة بغير كاتبها.

## 21. Risks
تضخم نطاق المراقبة (تخفيف: قرار Legal أولاً + الخط الأساسي يكفي وظيفياً) · تمرين استعادة شكلي (تخفيف: بيئة مستقلة + منفّذ مختلف) · مفاجآت ترخيص عند التوزيع (تخفيف: فئة 4 بوابة قبل أي release).

## 22. Open Decisions
| OD | الموضوع | التوصية | البوابة |
|---|---|---|---|
| OD-P8-1 | تركيبة المراقبة النهائية | Prometheus-server + بديل لوحات Apache-2 إن رُفض Grafana قانونياً؛ وإلا الاكتفاء بالخط الأساسي + تنبيهات بسيطة | بعد Legal، قبل تفعيل أي صورة (فئة 3) |
| OD-P8-2 | آلية توقيع الحزمة | توقيع منفصل بمفاتيح PKI المؤسسة يديره Ops | مع فريق العمليات قبل أول bundle |
| OD-P8-3 | أداة فحص ثغرات التبعيات | مرشّح متساهل الترخيص بصف مراجعة | قبل تفعيلها في CI |

## 23. Definition of Done
Baseline المشترك + AC 1–8 خضراء + كل runbooks معتمدة + **Handoff نهائي للتشغيل** (وثيقة تسليم Ops) — وبهذا يكتمل مسار التنفيذ الأول للمنصة.

## 24. Coding Agent Prompt
> القالب الموحّد §6 مع: **PHASE=8 · DESIGN=phases/designs/phase-8-monitoring-offline-production.md · RELEASE=v0.3-phase-design-package** — لا صورة مراقبة قبل صفها؛ الإثبات بالتمارين لا بالوثائق؛ التزم بأقسام 3/14/19/22.
