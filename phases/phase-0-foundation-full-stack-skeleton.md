# Phase 0 — Foundation &amp; Full-Stack Skeleton
## تصميم المرحلة (Vision → Specify → Clarify → Plan → Tasks) — بلا كود

> **Document Title:** Phase 0 Design — Foundation &amp; Full-Stack Skeleton · **Version:** 2.1 — Final (A3/A8 + D1–D9 مدمجة؛ C1–C5 وC8 مُغلقة) · **Status:** Current / **Accepted for Design** (التنفيذ لاحقاً) · **Date:** 2026-07-04
> **Supersedes:** v1.0 + `Phase-0-Prompt.md` القديم (Superseded)
> **Related:** constitution.md · Methodology · Catalog · open-decisions.md · phase-roadmap.md · handoff.md
> **Authority Order:** المرتبة 6 (تصميم مرحلة معتمد). · **Purpose:** مواصفة المرحلة الأولى في الخريطة — **تأسيس الهيكل الكامل والإعداد والحدود، لا تنفيذ خصائص المنتج**.
> **تسمية المراحل (C8 — مُغلق):** تُسمّى المراحل دائماً بالرقم + الاسم؛ هذه هي **Phase 0**، وPhase 1 = Governed Core + Screen Builder (تُصمَّم لاحقاً في محادثة مستقلة).

---

## أولاً — Vision (رؤية المرحلة)

**الهدف:** أساس **مفروض تقنياً** قبل أي منطق أعمال: هيكل repo بحدود مُنفَّذة (CI)، نظام إعداد هرمي بـ fail-fast، **كل الطبقات والخدمات حاضرة** بإعدادات demo خفيفة، Profiles/Bundles، Health، وقواعد تمنع الوكلاء من الكود العشوائي أو النداء الخارجي — مع إثبات وعد المشروع الأول: **portable configuration-driven deployment**.

**المستخدمون في المرحلة:** SA · AI Coding Agents · Operations لاحقاً. **لا مستخدم نهائي.**
**البيئة:** MSI Titan · Docker/Compose · شبكة مغلقة (الاستثناء الوحيد: سحب صور/حزم مُراجَعة الترخيص أثناء التطوير الأولي، ثم مسار offline bundle).

**ما يدخل:** هيكل repo + constitution/specs مزروعة + سقالات **36 module** (بما فيها `chat` كسقالة) + عقود التجريد + Config Registry + Feature Flags + Service Registry (حد أدنى حقيقي) + Compose (فعّال: Postgres×4 · Qdrant · OpenSearch؛ ومعرّف مطفأ: cache-queue · object-storage · Neo4j) + Profiles/Bundles + Health end-to-end + قشرة Web (i18n/RTL/tokens) + Worker skeleton + **lockfiles/digest pinning** + اختبارات portability/offline + license-review مُعبّأ + handoff.
**ما لا يدخل (صراحةً):** Auth حقيقي · صلاحيات مُنفَّذة · شاشات أعمال · توليد/migrations أعمال · وكلاء · LLM/RAG/Media فعلي · تكاملات · تقارير · متجر. (حضورها = **سقالات وعقود فقط**.)

**المبادئ الموروثة:** كل مواد constitution.md (خاصة 1–5، 7–15، 19).
**تعريف النجاح (قابل للقياس):** (1) compose بالـ Local profile يُقلع كل الخدمات **الفعّالة** (postgres×4/qdrant/opensearch/api/worker/web) و`/health` أخضر لتبعياتها، والخدمات الاختيارية تظهر **معرّفة-مطفأة** بوضوح؛ (2) تبديل profile يغيّر السلوك **دون تعديل كود** وproduction يجتاز الـ validation؛ (3) الـ 36 سقالة موجودة وCI boundaries **يرفض** الصاعد/الدوري/العابر؛ (4) **no-external-call** ينجح؛ (5) كل تغيير config/flag/profile مدقَّق + versioned + قابل للـ rollback؛ (6) license-review يغطي كل dependencies المرحلة ولا شيء خارجه؛ (7) **lockfiles + digest pinning** مطبّقة.
**حدود المرحلة:** سقالات وعقود وبنية — صفر منطق أعمال؛ أي إضافة خارج الـ FRs تُرفض.
**مخاطر المرحلة:** over-engineering (حد أدنى معرّف) · ثقل OpenSearch/Qdrant (demo limits + قياس الإقلاع ≤~3 دقائق) · فجوة ترخيص توقف compose (حسم فئة 3 قبل P0.4) · انحراف بيئات (profile tests + صورة واحدة) · انجراف الحزم مغلقاً (pinning).

## ثانياً — Specify

**الوصف:** مستودع واحد يحوي Modular Monolith (FastAPI) بكل الـ modules كسقالات، قشرة Enterprise UI (React + Vite — D1، ar/en، RTL)، Worker skeleton، بنية Compose كاملة الخدمات بإعدادات demo، نظام إعداد هرمي عامل، اختبارات تثبت النقل والعمل المغلق، وسقالة حوكمة كاملة — **دون أي منطق أعمال**.

**FRs:**
| # | المتطلب |
|---|---|
| FR-0.1 | هيكل الـ repo وفق Methodology §6 + constitution.md + README + handoff. |
| FR-0.2 | زرع `specs/` من حزمة الوثائق النهائية (README/vision/constitution/methodology/catalog/open-decisions/roadmap/هذا التصميم) + `adr/` بالترقيم الكنسي (adr/README.md) بحالاتها. |
| FR-0.3 | Monolith skeleton: `apps/api` يسجّل الـ modules؛ **36 module** بسقالة قياسية (api/service/repository/events/migrations/tests + manifest: الاسم/Tier/Deps/namespace) — بلا وظائف مجال. |
| FR-0.4 | `backend/shared` عقود فقط: **CacheProvider · QueueProvider · LockProvider** (افتراضي memory/PostgreSQL — D4) · **ObjectStorageProvider (fs|s3)** (افتراضي filesystem — D5) · LLMProvider (OpenAI-compatible) · IdentityProvider · DatabaseRouter · EventBus (in-process) · MediaProcessor + تنفيذات دنيا للإقلاع. |
| FR-0.5 | نظام الإعداد: defaults→profile→bundles→runtime→secrets · namespaces · static/dynamic · validation + **fail-fast** برسالة تذكر المفتاح الناقص. |
| FR-0.6 | Config Registry في platform_db: قيم dynamic + **versioning** + واجهة داخلية + حدث audit لكل تغيير. |
| FR-0.7 | Feature Flags: نطاقات (global/module/capability/env) + **protected flags** (auth/permissions/audit/config/flags/registry/datastores) + تغيير dynamic مدقَّق. |
| FR-0.8 | Service Registry (حد أدنى): manifest (core/optional/disabled + تبعيات) + تجميع `/health` في تقرير واحد + حدث service.health_alert. |
| FR-0.9 | **Compose (تصميم تصوري — لا ملفات في هذه الوثيقة):** base + override(dev) + prod؛ الخدمات: api · worker · web · postgres (القواعد الأربع + **مستخدم least-privilege لكل قاعدة**) · qdrant · opensearch؛ وخدمات **معرّفة role=optional وdisabled**: cache-queue (Valkey) · object-storage (MinIO|SeaweedFS) · neo4j · (Ollama/vLLM حسب C7). الافتراضيات (D4/D5/D6): Cache/Queue/Lock = memory/PostgreSQL · Storage = local filesystem · المراقبة = الخط الأساسي بلا خادم. **Qdrant وOpenSearch حاضران في Local** بحدود demo (heap/mem). لا بوابة فئة 3 على الصور الفعّالة (صف شكلي)؛ البوابة عند **تفعيل** أي صورة اختيارية. **كل الصور بـ digest pinning.** |
| FR-0.10 | Profiles كملفات: `configs/local|demo|staging|production` + `configs/bundles/` (low-resource · full-stack · media-enabled · security-enabled · graph-enabled · integration-enabled كـ presets أعلام)؛ Local يعمل فعلياً؛ البقية تجتاز validation. |
| FR-0.11 | **Health (تصوري):** `/health` تجميعي + نقاط فرعية `/health/db` · `/health/qdrant` · `/health/opensearch` · `/health/llm` (عقد الـ Gateway — يُبلّغ disabled بوضوح) (+cache/objstore عند تفعيلهما)؛ healthchecks لكل حاوية فعّالة؛ صفحة صحة في web تُظهر الفعّال والمطفأ؛ ملاحظة: كشف `/health` في production خلف حماية (تُنفَّذ مع Auth في Phase 1). |
| FR-0.12 | Web shell: React + Vite + TypeScript (D1) + i18n (ar/en) + **RTL/LTR صحيح** + design tokens (white-label) + صفحة صحة + صفحة دخول placeholder (بلا مصادقة). |
| FR-0.13 | Worker skeleton: عملية مستقلة تستهلك مهمة no-op من **QueueProvider** (تنفيذ PostgreSQL `FOR UPDATE SKIP LOCKED` أو memory — D4) + graceful shutdown + عددها بالإعداد. |
| FR-0.14 | Baseline platform migrations (أداة الترحيل، **مراجعة PR — مسار منفصل ومسمّى عن «التوليد المحكوم» للتطبيقات**): config_registry · config_versions · feature_flags · service_manifest · audit_log (حد أدنى: actor/action/target/old/new/ts). |
| FR-0.15 | إنفاذ الحدود في CI: قواعد استيراد تطابق Dependency Matrix + فحص secrets + تشغيل no-external-call. |
| FR-0.16 | Offline/Portability: سكربتات placeholders لحزمة النقل (images/wheels/models) + مسودة offline-install + مفاتيح backup paths. |
| FR-0.17 | license-review مُعبّأ بكل dependencies/صور المرحلة؛ **قاعدة: لا dependency خارج القائمة**. |
| FR-0.18 | **(A8)** سياسة إعادة البناء المغلق: **lockfiles لكل مديري الحزم + digest pinning للصور**، موثّقة في coding-standards ومُتحقَّق منها في CI وofflne scripts. |

| FR-0.19 | **(D6)** Observability Baseline: JSON logs منظّمة (stdout/ملف بدوّار — **لا تُخزَّن app logs في Postgres**) + Error Code Catalog أولي + request/correlation IDs بكل طلب + **/metrics اختياري بعلَم** + تمييز صريح: Audit (أحداث أعمال، في PG) ≠ App logs (تشخيص). Admin Log Viewer يُبنى مع الواجهة الإدارية (Phase 1+). |

**NFRs:** stateless api · JSON logs · fail-fast إقلاع · زمن إقلاع Local ≤~3 دقائق (يُقاس ويوثَّق) · حدود موارد demo لكل حاوية · RTL سليم (فحص snapshot/بصري) · **لا نداء شبكي خارجي وقت التشغيل (مُختبر)** · أسرار env فقط · رسائل أخطاء إعداد واضحة.
**القيود:** لا منطق أعمال/شاشات أعمال · لا استدعاء LLM (عقد فقط) · لا external APIs · لا hardcoded · Qdrant/OpenSearch لا يُستبدلان في Local (pgvector/PG-FTS ضمن low-resource bundle الصريح فقط) · Neo4j حاضر تعريفاً مطفأ · معرّفات ASCII · الالتزام بـ §6/§8/§9 من المنهجية.
**مصادر الحقيقة/الصلاحيات/التدقيق في المرحلة:** المصدر المفعّل الوحيد platform_db (إعداد/أعلام/manifest/audit)؛ الصلاحيات **سقالة وعقد فقط** (الإنفاذ في Phase 1)؛ **Audit يبدأ الآن** على أحداث الإعداد فقط (config.changed / feature_flag.changed / profile.changed) — والـ spine الكامل في Phase 1 (A6).
**بوابات License Review في المرحلة:** فئة 2 قبل أول كود = صفوف الستاك المعتمد (React/Vite/TS/Tailwind/shadcn/FastAPI/Pydantic/SQLAlchemy/Alembic/uv/pnpm)؛ **الفئة 3 لا تحجب P0.4** — الصور الفعّالة (Postgres/Qdrant/OpenSearch) متساهلة وتمرّ بصف شكلي، والبوابة تنطبق عند **تفعيل** أي صورة اختيارية (Valkey/MinIO|SeaweedFS/monitoring-server) في أي مرحلة.

## ثالثاً — Clarify (استيضاحات المرحلة)

| # | القرار | الخيارات | الفئة | موعد الحسم | الحالة |
|---|---|---|---|---|---|
| C1 | cache/queue | **مُغلق (D4):** لا حاوية في P0/P1؛ الافتراضي memory/PostgreSQL؛ Valkey optional-ready | كان 3 → بوابة تفعيل | عند أول حاجة (غالباً P5/P6) | **مُغلق 2026-07-04** |
| C2 | Object storage | **مُغلق (D5):** filesystem افتراضاً؛ MinIO|SeaweedFS يُحسم بمرحلة الملفات | كان 3 → بوابة تفعيل | قبل تفعيل صورة التخزين | **مُغلق 2026-07-04** |
| C3 | مراقبة Local | **مُغلق (D6):** الخط الأساسي (JSON logs + Health + Error Catalog + IDs + /metrics اختياري)؛ لا خادم مراقبة | مُغلق | التوسعة P8 | **مُغلق 2026-07-04** |
| C4 | مضيف Git | **مُغلق (D7):** GitHub الآن؛ Git داخلي (Gitea/GitLab) = Backlog + قناة نقل موقّعة | مُغلق | — | **مُغلق 2026-07-04** |
| C5 | معايير الأدوات | **مُغلق (D3):** uv + pnpm | مُغلق | — | **مُغلق 2026-07-04** |
| C6 | بنية Postgres في Local | **instance واحد ×4 قواعد** | 5 | افتراض معتمد | مُعتمد كافتراض |
| C7 | Ollama/vLLM في compose | **تعريف مطفأ** (توصية) | 5 | مع P0.4 | مفتوح (غير مُعطِّل) |
| C8 | تسمية المراحل | الرقم + الاسم دائماً | 1 (تأكيدي) | — | **مُغلق** |

## رابعاً — Plan

**الترتيب:** P0.1 Repo &amp; Governance → P0.2 Configuration Core (+baseline migrations) → P0.3 Monolith Skeleton &amp; Boundaries → P0.4 Infra &amp; Compose (الصور الفعّالة؛ الاختيارية معرّفة مطفأة) → P0.5 Health &amp; Service Registry → P0.6 Web Shell → P0.7 Worker → P0.8 Portability &amp; Offline (+pinning) → P0.9 Docs/Gates/Handoff.
**ADRs المفعّلة:** ADR-0001 (Accepted) يُطبَّق؛ 0006/0007 (config-only، License gate) حاكمة؛ التجريدات (cache/objstore/observability/gateway-contract) تُختبر عملياً — أي انحراف ⇒ تحديث ADR.
**المخاطر والتخفيف:** كما في Vision + بوابة CI تمنع كسر الحدود من أي وكيل.
**خطة الاختبار:** unit (config/flags) · profile validation (الأربعة + bundles) · flags (المحمية ترفض) · audit (أحداث الإعداد) · migration (apply/rollback) · smoke/health · boundary (استيراد ممنوع يُفشل CI) · **offline/no-external-call** · RTL snapshot · قياس زمن الإقلاع.
**خطة الترحيل:** baseline platform migrations فقط عبر PR (لا علاقة بخط التوليد المحكوم — يبدأ Phase 1+).
**النشر والتحقق:** تشغيل Local على الجهاز؛ prod عبر validation فقط؛ توثيق أوامر التشغيل لكل profile.
**التراجع:** git revert · compose down (حذف volumes صراحةً لبيئة demo فقط) · rollback قيمة config من versions.
**DoD:** بنود «تعريف النجاح» السبعة + كل اختبارات الخطة خضراء + Quality Gates (Methodology §11) + لا منطق أعمال + زمن الإقلاع موثّق + handoff كامل.

## خامساً — Tasks (بطاقات بلا كود؛ كل بطاقة بحجم جلسة وكيل واحدة)

**E0.1 Repo &amp; Governance:** T-0.1.1 تهيئة الهيكل (القبول: مطابقة §6 حرفياً) · T-0.1.2 وضع constitution.md (النسخة المعتمدة من الحزمة) · T-0.1.3 **زرع specs/ وadr/** من الحزمة النهائية (ADR-0001 Accepted؛ البقية بحالاتها) · T-0.1.4 زرع license-review (كل dependencies المرحلة لها صف) · T-0.1.5 CI skeleton (lint/test + فحص secrets يمسك سراً تجريبياً) + قالب handoff.
**E0.2 Configuration Core:** T-0.2.1 config loader الهرمي (unit: ترتيب الغلبة؛ ناقص حرج ⇒ fail-fast بالمفتاح) · T-0.2.2 baseline migrations (apply/rollback نظيفان) · T-0.2.3 Config Registry + versioning + حدث config.changed (audit test) · T-0.2.4 Feature Flags + protected (المحمية ترفض؛ الحدث يُسجَّل) · T-0.2.5 ملفات profiles/bundles + توثيق المفاتيح (الأربعة تجتاز validation).
**E0.3 Skeleton &amp; Boundaries:** T-0.3.1 قالب module + مولّد سقالة (module تجريبي يمر CI) · T-0.3.2 توليد **36 سقالة** بالـ manifests (apps/api يقلع بها) · T-0.3.3 عقود shared + تنفيذات دنيا · T-0.3.4 EventBus داخلي (نشر/استقبال حدث تجريبي) · T-0.3.5 قواعد الحدود في CI (استيراد ممنوع مُتعمَّد يُفشل CI).
**E0.4 Infra &amp; Compose (الصور الفعّالة + تعريفات مطفأة):** T-0.4.1 صور api/worker/web موحّدة (لا فروع بيئة) · T-0.4.2 compose base/override/prod + حدود demo + healthchecks + **digest pinning** (compose config صالح للثلاثة) · T-0.4.3 تهيئة Postgres ×4 + **مستخدم least-privilege لكل قاعدة** + DatabaseRouter بالإعداد (health يرى الأربع) · T-0.4.4 تشغيل Qdrant/OpenSearch بإعداد demo + تعريف cache-queue/object-storage/Neo4j (+Ollama/vLLM حسب C7) **مطفأةً** — health يعرضها disabled بوضوح · T-0.4.5 الخط الرقابي الأساسي (D6): JSON logs + Error Code Catalog + correlation IDs + /metrics اختياري — لا خادم مراقبة.
**E0.5 Health &amp; Registry:** T-0.5.1 `/health` تجميعي + الفرعية db/qdrant/opensearch/llm (أخضر للفعّال؛ يحدد المتعطل؛ يعرض المطفأ disabled) · T-0.5.2 Service Registry (التقرير يطابق core/optional/disabled) · T-0.5.3 حدث service.health_alert.
**E0.6 Web Shell:** T-0.6.1 سقالة React+Vite + tokens · T-0.6.2 i18n ar/en + RTL (snapshot) · T-0.6.3 صفحتا الصحة والدخول-placeholder.
**E0.7 Worker:** T-0.7.1 عملية worker + no-op job + إيقاف نظيف · T-0.7.2 العدد بالإعداد فقط.
**E0.8 Portability &amp; Offline:** T-0.8.1 profile validation tests · T-0.8.2 no-external-call test (يفشل عند نداء خارجي تجريبي) · T-0.8.3 سكربتات offline placeholders + مسودة offline-install (dry-run موثَّق) · T-0.8.4 قياس زمن الإقلاع وتوثيقه · T-0.8.5 **lockfiles + digest pinning** ملتزمة ومُتحقَّق منها في CI.
**E0.9 Docs/Gates/Handoff:** T-0.9.1 تحديث configuration.md/README/troubleshooting أولي · T-0.9.2 اجتياز Quality Gates + تعبئة handoff (المنجز/الملفات/المخاطر/**تحذيرات Phase 1**).

**متطلبات الـ Handoff للمرحلة:** لا تُغلق المرحلة قبل handoff كامل الحقول + أرشفة نسخة + قائمة «ما لا يُلمس» لوكيل Phase 1 (خاصة: عقود shared، وقواعد CI، وbaseline migrations).

## إضافات خط الأساس v1.0 (2026-07-10) — بنود تسليم/قيود إضافية (كتلة إضافية لا تعيد تصميم المرحلة)
1. **حزمة الحد الأدنى المغلقة من Phase 0 (D14):** مستودع المصدر · lockfiles · Python wheelhouse/cache · pnpm offline store · صور Docker بأرقام digest · قوالب الإعداد · سكربت تثبيت · سكربت تحقق · checksums · **بيان سلامة (integrity manifest)** · إشعارات التراخيص · **بيان النماذج (model manifest) متى وُجدت نماذج** · تعليمات النسخ الاحتياطي/الاستعادة · إجراء التحديث · إجراء التراجع. **مؤجَّل قابل للإضافة (لا يُحذف موطؤه):** SBOM متقدم · بنية توقيع artifacts · مراقبة مؤسسية موسّعة · تصليب سلسلة التوريد المتقدم.
2. **مستخدم قاعدة التدقيق (D11):** مستخدم قاعدة بيانات **مخصص** لجداول التدقيق؛ دور التطبيق يملك **INSERT فقط** على جداول التدقيق (لا UPDATE ولا DELETE) — يُرسَّخ في baseline migrations (يوسّع FR-0.14).
3. **السجلات والعارض (D11):** JSON logs مهيكلة إلى stdout/stderr (تدوير عبر Docker)؛ عارض السجلات الإداري **لا يقرأ ملفات السجلات** — مصدره **LogRepository / مخزن أحداث تشغيلية مُهيكل** (تنفيذ v1: جدول `ops_events` صغير في PG)؛ الـ stack traces الكاملة للمشغّلين المخوّلين فقط (يوسّع FR-0.19).
4. **المراقبة (D11):** health + **readiness/liveness** + `/metrics` اختياري بعلَم + **OpenTelemetry-ready** (بلا Grafana/Loki/Graylog/Elastic ابتداءً) — يوسّع FR-0.11.
5. **موضع سقالة الواجهة (D4):** سقالة الواجهة في `/frontend` داخل مستودع المنصة `local-rag-enterprise-platform` (monorepo-lite)؛ أي فصل لاحق بمستودع مستقل = ADR.
6. **خريطة التغليف (D3):** يجوز أن يُنتج تصميم مرحلةٍ **خريطة تغليف (packaging map)** تجمع أكثر من وحدة منطقية في حزمة/وحدة نشر واحدة — **الخريطة أثر تنفيذي يتغيّر دون ADR**؛ الثابت المعماري: الحدود المنطقية وملكية الجداول لكل وحدة (لا قراءة جداول عبر الوحدات أياً كان التغليف)، وإنفاذ import-lint يبدأ بحبيبية الحزم ويشتد نحو حبيبية الوحدات مع نضج الكود.

---
**بعد اعتماد التنفيذ لاحقاً:** تُنفَّذ البطاقات بأي Coding Agent وفق Methodology §18. **الخطوة التصميمية التالية:** Phase 1 — Governed Core + Screen Builder (محادثة مستقلة).
