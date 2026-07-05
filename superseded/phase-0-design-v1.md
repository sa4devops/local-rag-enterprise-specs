> ⚠️ SUPERSEDED — لا يُستخدم للتنفيذ. المرجع الحالي: حزمة v2.0 (انظر superseded/README.md). تاريخ الوسم: 2026-07-03.

# تصميم المرحلة الأولى — Phase 0: Foundation &amp; Full-Stack Skeleton
## حزمة تصميم كاملة بمنهجية Vision → Specify → Clarify → Plan → Tasks
> **لا كود · لا تنفيذ · لا برومبتات تنفيذ.** مبنية على الوثيقتين المعتمدتين: **Feature &amp; Technical Architecture Catalog** و**Spec-driven Development &amp; Modular Monolith Build Methodology** (ADR-0001: Accepted)، وعلى ملحق **تصنيف القرارات المفتوحة**.

**لماذا هذه هي «المرحلة الأولى»:** في الـ Roadmap المعتمد، أول مرحلة قابلة للبناء هي Phase 0؛ ومنهجية Spec-driven تصمّم بترتيب البناء. لا يمكن تنفيذ Phase 1 (Governed Core + Screen Builder) قبل وجود هذا الأساس. عند اعتماد هذه الحزمة، تُصمَّم Phase 1 في محادثة مستقلة بنفس المنهجية.

**خريطة النقل إلى المستودع لاحقاً:** القسم «أولاً» → `specs/vision-phase0.md` · «ثانياً» → `specs/spec-phase0.md` · «ثالثاً» → `specs/clarification-phase0.md` · «رابعاً» → `specs/plan-phase0.md` · «خامساً» → `specs/tasks/phase0/`.

---

# أولاً — Vision (رؤية المرحلة)

**المشكلة التي تحلّها المرحلة:** لا يمكن السماح لأي Coding Agent بكتابة أي module قبل وجود: هيكل repo بحدود **مفروضة تقنياً** (لا اتفاقاً شفهياً)، ونظام إعداد هرمي مع validation وfail-fast، وحضور **كل الطبقات والخدمات** (بإعدادات demo خفيفة)، وآلية Profiles/Bundles، وفحوص صحة، وقواعد CI تمنع كسر الحدود والاعتماد الصاعد والنداء الخارجي. غياب هذا الأساس = كود عشوائي غير قابل للنقل، وهو ما تمنعه قواعدك.

**لماذا المرحلة مهمة:** تحوّل المنهجية المعتمدة من وثيقة إلى **قالب مفروض بالأدوات** (boundaries في CI، config validation، license-review gate)، وتُثبت مبكراً أهم وعد في المشروع: **portable configuration-driven deployment** (نفس الكود من MSI Titan إلى الإنتاج بتغيير إعداد فقط).

**المستخدمون في هذه المرحلة:** مالك المشروع (SA)، والـ AI Coding Agents التي ستنفّذ لاحقاً، وفريق العمليات مستقبلاً. **لا مستخدم نهائي في هذه المرحلة.**

**البيئة:** جهاز MSI Titan (RTX 5090 Laptop ~24GB VRAM / 64GB RAM)، Docker / Docker Compose، **شبكة مغلقة** — لا إنترنت وقت التشغيل (الاستثناء الوحيد: سحب الصور/الحزم أثناء التطوير الأولي من مصادر مُراجَعة الترخيص، ثم توثيق مسار offline bundle).

**ما تحلّه المرحلة:** هيكل repo كامل بالمنهجية · Modular Monolith skeleton بكل الـ modules كسقالات محدودة الحدود · shared abstractions (عقود) · نظام Config/Registry/Flags/Service-Registry عامل (حد أدنى حقيقي) · Docker Compose بكل خدمات البنية (Postgres×4، Qdrant، OpenSearch، Object Storage، Cache/Queue، Neo4j معرّفاً مطفأً) · Environment Profiles + Capability Bundles · Health end-to-end · قشرة Web (i18n/RTL/white-label tokens) · Worker skeleton · اختبارات portability وoffline · سقالة license-review · handoff.

**ما لا تحلّه (صراحةً):** لا Auth حقيقي، لا صلاحيات، لا شاشات ديناميكية، لا توليد/migrations أعمال، لا وكلاء، لا LLM/RAG/Media فعلي، لا تكاملات، لا تقارير، لا متجر. (كلها مراحل لاحقة — حضورها هنا **سقالات وعقود فقط**.)

**المبادئ غير القابلة للتفاوض (موروثة من constitution):** منتج واحد portable (config-only للإنتاج، لا fork) · النظام منصة لا chatbot · LLM ليس مصدر حقيقة · الواجهة النهائية Enterprise UI (لا Open WebUI) · كل الطبقات حاضرة (enabled/disabled/lightweight لا محذوفة) · الوسائط جاهزة معمارياً (عقود/سقالات من الآن) · لا dependency بلا License Review · Modular Monolith حقيقي (لا وصول عابر للحدود) · default-deny وAudit من أول جدول يُنشأ.

**تعريف نجاح المرحلة (قابل للقياس):**
1. `docker compose` بالـ Local profile يُقلع **كل** الخدمات على MSI Titan، و`/health` أخضر لكل التبعيات.
2. تبديل profile (Local→Demo/Staging/Production كملفات إعداد) يغيّر السلوك **دون أي تعديل كود**، وProduction profile يجتاز config validation.
3. كل الـ modules (~37) موجودة كسقالات ببنية قياسية، وفحص boundaries في CI **يرفض** اعتماداً صاعداً/دورياً أو وصولاً عابراً.
4. اختبار **no-external-call** ينجح (لا نداء شبكة خارجية وقت التشغيل).
5. تغيير أي config/flag يُسجَّل في audit (config.changed / feature_flag.changed) مع versioning وإمكانية rollback للقيمة.
6. `specs/license-review.md` يحتوي صفوف كل dependencies المرحلة، **ولا dependency في المشروع خارج القائمة**.

**حدود المرحلة (Phase-MVP):** سقالات وعقود وبنية — **صفر منطق أعمال**. أي إغراء لإضافة ميزة = خارج النطاق ويُرفض.

**مخاطر المرحلة:** Over-engineering للسقالات (التخفيف: حد أدنى معرّف بدقة في Specify) · ثقل OpenSearch/Qdrant على الجهاز (التخفيف: حدود موارد demo في compose) · فجوات ترخيص توقف compose (التخفيف: بنود الفئة 3 محسومة قبل P0.4) · انحراف dev/prod (التخفيف: profile validation tests + صورة واحدة) · تضخم زمن الإقلاع (التخفيف: قياس زمن الإقلاع كمعيار قبول).

---

# ثانياً — Specify (مواصفة المرحلة)

## 2.1 الوصف عالي المستوى
مخرَج المرحلة: **مستودع واحد** يحتوي Modular Monolith (FastAPI) بكل الـ modules كسقالات، وقشرة Enterprise UI (Next.js) بدعم ar/en وRTL، وWorker skeleton، وبنية Docker Compose كاملة الخدمات بإعدادات demo، ونظام إعداد هرمي عامل (Config Registry + Feature Flags + Service Registry)، واختبارات تثبت قابلية النقل والعمل المغلق، وسقالة حوكمة (constitution، specs، ADRs، license-review، handoff) — **دون أي منطق أعمال**.

## 2.2 المتطلبات الوظيفية (FR)
| # | المتطلب |
|---|---|
| FR-0.1 | إنشاء هيكل الـ repo وفق §6 من المنهجية: `apps/ (web, api, worker)` · `backend/ (modules, shared)` · `packages/ (ui, sdk, shared-types)` · `infrastructure/ (docker, db, observability, scripts)` · `specs/ (كل الملفات + adr/ + tasks/ + handoffs/)` · `configs/ (local, demo, staging, production, bundles)` · `tests/ (unit, integration, e2e, security, permission, migration, offline)` · `docs/` · `constitution.md` · `handoff.md`. |
| FR-0.2 | تعبئة `specs/` بالوثائق المعتمدة (Catalog، Methodology، هذا التصميم، ملحق التصنيف) وإنشاء `specs/adr/` بالـ ADRs (0001=Accepted، البقية Proposed). |
| FR-0.3 | Monolith skeleton: تطبيق `apps/api` يُحمّل الـ modules عبر تسجيل موحّد؛ **كل module** من كتالوج الـ Modules (~37) موجود كسقالة ببنية قياسية: `api/ · service/ · repository/ · events/ · migrations/ · tests/` + manifest (الاسم، الطبقة Tier، التبعيات المسموحة، config namespace) — بلا وظائف مجال (endpoint حالة/عقد فقط حيث يلزم). |
| FR-0.4 | `backend/shared`: **عقود التجريد فقط**: CacheQueue · ObjectStorage · LLMProvider (OpenAI-compatible contract) · IdentityProvider · DatabaseRouter · EventBus (in-process) · MediaProcessor — مع تنفيذات دنيا/no-op تكفي للإقلاع، ودون أي منطق مزوّد حقيقي عدا الاتصال الأساسي حيث يلزم للـ health. |
| FR-0.5 | نظام الإعداد: هرمية defaults → environment profile → capability bundles → runtime overrides (Registry) → secrets؛ namespaces لكل module؛ توصيف كل مفتاح static/dynamic؛ **validation + fail-fast** عند نقص مفتاح حرج؛ لا قيمة حرجة hardcoded. |
| FR-0.6 | Config Registry في `platform_db`: تخزين القيم dynamic + **versioning لكل تغيير** + واجهة قراءة/تعديل داخلية؛ كل تغيير يولّد حدث audit. |
| FR-0.7 | Feature Flags: حلّ الأعلام بنطاقات (global/module/capability/env)، قائمة **protected flags** (auth/permissions/audit/config/db لا تُعطَّل)، تغييرها dynamic ومدقَّق. |
| FR-0.8 | Service Registry (حد أدنى): manifest ثابت للخدمات/الـ modules (الحالة core/optional/disabled، التبعيات) + تجميع `/health` التبعيات في تقرير واحد. |
| FR-0.9 | Docker Compose: `base` + `override(dev)` + `prod`، بخدمات: api · worker · web · postgres (تهيئة القواعد الأربع: platform/apps/integration/reporting) · qdrant · opensearch · object-storage · cache-queue · (neo4j **معرّفاً role=optional وdisabled**) · مراقبة حسب حسم C3 — **Qdrant وOpenSearch حاضران في Local** بإعدادات خفيفة (حدود ذاكرة/heap demo). *(اختيار صور cache/object-storage/monitoring رهن حسم بنود الفئة 3 قبل P0.4.)* |
| FR-0.10 | Environment Profiles كملفات إعداد: `configs/local|demo|staging|production` + `configs/bundles/` (low-resource · full-stack · media-enabled · security-enabled · graph-enabled · integration-enabled كـ presets أعلام)؛ Local يُشغَّل فعلياً؛ البقية تجتاز schema/validation tests. |
| FR-0.11 | Health: `/health` للـ api يفحص (postgres×4 · cache · qdrant · opensearch · object-storage) ويُرجع تقريراً مفصّلاً؛ healthchecks في compose لكل خدمة؛ صفحة صحة في web تعرض التقرير. |
| FR-0.12 | Web shell (`apps/web`): Next.js/React/TS + i18n (ar/en) + **RTL/LTR صحيح** + design tokens قابلة للـ white-label + صفحة صحة + صفحة دخول **placeholder** (بلا مصادقة حقيقية) — دون أي شاشة أعمال. |
| FR-0.13 | Worker skeleton (`apps/worker`): عملية مستقلة بنفس الـ codebase تستهلك مهمة no-op من CacheQueue abstraction وتُنهي بأمان (graceful shutdown) — لإثبات فصل الـ workers. |
| FR-0.14 | Baseline platform migrations (عبر أداة الترحيل المعتمدة): جداول `config_registry` · `config_versions` · `feature_flags` · `service_manifest` · `audit_log` (حد أدنى بحقول: actor/action/target/old/new/ts) — **تنبيه حدودي:** هذه migrations مطوّر تُراجَع عبر PR/code-review، وهي **غير** خط «التوليد المحكوم بالاعتماد» الذي يخص app schemas في المراحل اللاحقة. |
| FR-0.15 | إنفاذ الحدود في CI: قواعد استيراد تطابق **Module Dependency Matrix** (منع الصاعد/الدوري/العابر للحدود) + فحص «لا secrets في المستودع» + تشغيل اختبار no-external-call. |
| FR-0.16 | Offline/Portability scaffolding: سكربتات placeholders لحزمة النقل (images/wheels/models) + مسودة `docs/offline-install.md` + مفاتيح backup paths في الإعداد. |
| FR-0.17 | `specs/license-review.md` مُعبّأ بصفوف كل dependencies/صور المرحلة بحالاتها (Needs Review/Needs Legal Review/…)، وقاعدة عمل: لا dependency خارج القائمة. |

## 2.3 المتطلبات غير الوظيفية (NFR)
Stateless api (لا حالة محلية؛ الجلسات مستقبلاً في cache/JWT) · سجلات JSON منظّمة · إقلاع fail-fast عند إعداد ناقص · زمن إقلاع Local مقبول (هدف ≤ ~3 دقائق للكومبوز كاملاً على الجهاز، يُقاس ويوثَّق) · حدود موارد demo لكل خدمة في compose · RTL سليم في القشرة (فحص بصري + snapshot) · **لا نداء شبكي خارجي وقت التشغيل** (مُختبر) · الأسرار عبر env فقط (لا تُلتزم في git) · رسائل أخطاء الإعداد واضحة تذكر المفتاح الناقص.

## 2.4 القيود (Constraints)
لا منطق أعمال ولا شاشات أعمال · لا استدعاء LLM (العقد فقط) · لا external APIs في runtime · لا hardcoded (secrets/endpoints/model names/paths/resources) · **Qdrant وOpenSearch لا يُستبدلان في Local** (pgvector/PG-FTS حصراً ضمن low-resource bundle الصريح) · Neo4j حاضر تعريفاً ومطفأ · لا يدخل dependency/صورة بلا صف مراجعة ترخيص · معرّفات تقنية ASCII (العربية labels) · الالتزام الحرفي بهيكل §6 وقواعد §8 و§9 من المنهجية.

## 2.5 مصادر الحقيقة والصلاحيات والتدقيق في هذه المرحلة
مصدر الحقيقة الوحيد المُفعّل: `platform_db` (إعداد/أعلام/manifest/audit). الصلاحيات: **لا إنفاذ بعد** — يوجد عقد `IdentityProvider` وسقالة `permissions` فقط (الإنفاذ في Phase 1). التدقيق: **يبدأ من هذه المرحلة** على أحداث الإعداد فقط: `config.changed` · `feature_flag.changed` · `profile.changed` (append-only).

## 2.6 النشر والقيود المغلقة واللغة
النشر: Local profile يعمل فعلياً على الجهاز؛ prod profile يُتحقق منه إعدادياً (بلا سيرفرات في هذه المرحلة). المغلق: no-external-call test + سقالة offline bundle + توثيق مصادر الصور المُراجَعة. اللغة/RTL: القشرة ar/en وRTL كامل من اليوم الأول. الأمن: أسرار env، وprotected flags، وفحص secrets في CI.

## 2.7 خارج النطاق (تأكيد نهائي)
Auth حقيقي · Organization · Permission enforcement · Screen/Field Builder · Records · Workflows · Notifications · RAG/Media/OCR فعلي · SQL Agent · وكلاء/Orchestrator · Model Registry UI · تكاملات/MCP/متجر · تقارير · Deployment Controller التشغيلي · HA.

---

# ثالثاً — Clarify (استيضاحات المرحلة)

| # | السؤال/القرار | الخيارات | المالك | الفئة | الأثر | موعد الحسم |
|---|---|---|---|---|---|---|
| C1 | مزوّد cache/queue الافتراضي وصورته | Redis أم **Valkey** (توصيتي: Valkey لوضوح الترخيص، مع بقاء التجريد) | SA | 3 | صورة compose + license-review | قبل P0.4 |
| C2 | Object storage للـ demo | **MinIO** (بقبول AGPL داخلياً مؤقتاً بانتظار المراجعة) أم بديل S3-compatible | SA | 3 | صورة compose + license-review | قبل P0.4 |
| C3 | مراقبة Local | **Prometheus + سجلات JSON فقط** (توصيتي الآن) أم Grafana/Loki كاملة | SA | 3 | حجم compose + license | قبل P0.4 |
| C4 | مضيف Git داخلي وسياسة الفروع | bare git محلي / Gitea / بديل | SA | 2 | مكان الـ repo وworkflow | قبل أول commit |
| C5 | معايير الأدوات | Python 3.12 + (uv أو poetry)، Node LTS + (pnpm أو npm) — توصيتي: uv + pnpm | SA | 2 | coding-standards.md | قبل P0.2 |
| C6 | بنية Postgres في Local | **instance واحد بأربع قواعد** (توصيتي) مقابل 4 instances | SA | 5 (configurable عبر DatabaseRouter) | موارد الجهاز | افتراض الآن، قابل للتغيير |
| C7 | حضور Ollama/vLLM في compose هذه المرحلة | **تعريفهما بعلم مطفأ** (توصيتي: حضور معماري بلا تشغيل) أم تأجيل التعريف لمرحلة النماذج | SA | 5 | لا تشغيل نماذج بأي حال في Phase 0 | مع P0.4 |
| C8 | تأكيد تسمية: «المرحلة الأولى» = Phase 0 | تأكيد، أو اعتبارها Phase 1 وتُصمَّم تالياً فوق هذه | SA | 1 (تأكيدي غير مُعطِّل) | ترقيم الحزم القادمة | مع اعتماد هذه الحزمة |

---

# رابعاً — Plan (خطة المرحلة)

## 4.1 ترتيب البناء الداخلي والتبعيات
`P0.1` Repo &amp; Governance Scaffolding → `P0.2` Configuration Core (config/registry/flags + baseline migrations) → `P0.3` Monolith Skeleton &amp; Boundaries (modules + shared + CI rules) → `P0.4` Infra &amp; Compose (رهن حسم C1–C3) → `P0.5` API Health &amp; Service Registry → `P0.6` Web Shell → `P0.7` Worker Skeleton → `P0.8` Portability &amp; Offline (profiles/bundles/no-external-call/offline scripts) → `P0.9` Docs, Quality Gates &amp; Handoff.
التبعيات: P0.2 يعتمد على P0.1؛ P0.3 على P0.2؛ P0.5 على P0.3+P0.4؛ P0.6/P0.7 على P0.3 (وP0.4 للتشغيل)؛ P0.8 على P0.4+P0.5؛ P0.9 أخيراً.

## 4.2 القرارات المعمارية المفعّلة
ADR-0001 (Accepted) يُطبَّق هنا. تُختبر عملياً وتبقى Proposed حتى اعتمادك: ADR-0008 (config-driven deployment) · ADR-0010 (Flags/Registry أساسية) · ADR-0012 (تجريد cache/queue) · ADR-0013 (تجريد object storage) · ADR-0014 (Observability قابلة للتبديل) · ADR-0015 (LLM Gateway على عقد OpenAI-compatible — **عقد فقط** في هذه المرحلة). أي انحراف أثناء التنفيذ ⇒ تحديث ADR أولاً.

## 4.3 إدارة المخاطر
| الخطر | التخفيف |
|---|---|
| Over-engineering للسقالات | حد أدنى معرّف في FR؛ أي إضافة خارج FR تُرفض في المراجعة |
| ثقل OpenSearch/Qdrant على الجهاز | حدود موارد demo (heap/mem) + قياس زمن الإقلاع كمعيار قبول |
| تعطّل P0.4 بانتظار قرارات الفئة 3 | حسم C1–C3 مبكراً؛ وبنية compose تُكتب حول abstractions بحيث يكون تبديل الصورة تغيير إعداد |
| انحراف بيئات | profile validation tests لكل الملفات الأربعة + صورة واحدة لكل خدمة |
| كسر حدود من وكيل تنفيذ لاحقاً | قواعد CI (boundaries/secrets/no-external-call) تفشل الدمج تلقائياً |

## 4.4 خطة الاختبار (لهذه المرحلة)
unit (config hierarchy/validation/flags resolution) · configuration profile tests (الملفات الأربعة + bundles تُحلَّل وتُتحقق) · feature flag tests (تفعيل/تعطيل + protected flags ترفض التعطيل) · audit tests (config/flag/profile change يولّد حدثاً بحقوله) · migration tests (baseline apply/rollback) · smoke/health (إقلاع + /health أخضر) · boundary checks (سيناريو اعتماد ممنوع يفشل CI) · **offline/no-external-call** · فحص RTL للقشرة (snapshot/بصري).

## 4.5 خطة الترحيل (بيانات)
baseline platform migrations فقط (FR-0.14) بأداة الترحيل المعتمدة، مراجعتها عبر PR/code-review، مع اختبار apply→rollback. **لا** app-schema migrations في هذه المرحلة، و**لا** علاقة لخط «التوليد المحكوم» بعد (يبدأ Phase 1+).

## 4.6 خطة النشر والتحقق
تشغيل Local profile على MSI Titan (compose up → health أخضر → فحص الصفحات) · التحقق من Demo/Staging/Production عبر config validation فقط · توثيق أمر التشغيل لكل profile في README/docs.

## 4.7 خطة التراجع (Rollback)
git revert للتغييرات · `compose down` (مع الاحتفاظ بالـ volumes افتراضياً؛ الحذف صراحةً لبيئة demo فقط) · استعادة قيمة config من `config_versions` (rollback القيمة) · لا بيانات أعمال في هذه المرحلة فالمخاطرة منخفضة.

## 4.8 معايير قبول المرحلة (Definition of Done)
1) بنود «تعريف النجاح» الستة في Vision كلها محققة. 2) كل اختبارات §4.4 خضراء في CI. 3) Quality Gates (§11 من المنهجية) مستوفاة: لا secrets، لا external calls، توثيق محدّث، license-review محدّث، handoff محدّث. 4) لا وجود لأي منطق أعمال (مراجعة scope). 5) زمن الإقلاع الموثّق ضمن الهدف. 6) `handoff.md` يصف الحالة النهائية وتحذيرات المرحلة التالية.

---

# خامساً — Tasks (تفكيك العمل)

> **بنية:** Epics → Tasks. كل task صغير ومحدد الملفات والقبول، مناسب لجلسة Coding Agent واحدة، **بلا كود هنا**. الأعمدة: ID · العنوان · التسليم (Scope) · المسارات المسموحة · القبول/الاختبار · يعتمد على.

## E0.1 — Repo &amp; Governance Scaffolding
| ID | العنوان | التسليم | المسارات | القبول/الاختبار | يعتمد |
|---|---|---|---|---|---|
| T-0.1.1 | تهيئة الـ repo والهيكل | إنشاء شجرة المجلدات كاملة وفق FR-0.1 + README أولي | الجذر كاملاً (إنشاء فقط) | الشجرة مطابقة حرفياً لـ §6 | — |
| T-0.1.2 | constitution.md | صياغة الدستور من المبادئ غير القابلة للتفاوض المعتمدة | constitution.md | يغطي القائمة في Vision §المبادئ؛ مراجعة SA | T-0.1.1 |
| T-0.1.3 | زرع specs/ وADRs | نقل الوثائق المعتمدة + إنشاء ADR-0001..0015 بحالاتها | specs/** | ADR-0001=Accepted؛ البقية Proposed بالصيغة القياسية | T-0.1.1 |
| T-0.1.4 | license-review seed | تعبئة `specs/license-review.md` بصفوف dependencies/صور المرحلة (حالات Needs Review/Legal) | specs/license-review.md | كل تقنية في FR-0.9/التقنيات المرشحة لها صف | T-0.1.3 |
| T-0.1.5 | CI skeleton + handoff template | إعداد CI أولي (lint/test placeholders + فحص secrets) + قالب handoff | infrastructure/**, handoff.md | CI يعمل على commit فارغ؛ فحص secrets يمسك سراً تجريبياً | T-0.1.1 |

## E0.2 — Configuration Core
| ID | العنوان | التسليم | المسارات | القبول/الاختبار | يعتمد |
|---|---|---|---|---|---|
| T-0.2.1 | Config loader الهرمي | تحميل defaults→profile→bundles→runtime→secrets + namespaces + static/dynamic typing | backend/modules/config/**, backend/shared/** | unit: ترتيب الغلبة صحيح؛ مفتاح ناقص حرج ⇒ fail-fast برسالة تذكر المفتاح | T-0.1.5 |
| T-0.2.2 | Baseline platform migrations | جداول FR-0.14 عبر أداة الترحيل + apply/rollback | backend/modules/{config,feature_flags,service_registry,audit}/migrations/** | migration test: apply ثم rollback نظيفان | T-0.2.1 |
| T-0.2.3 | Config Registry + versioning + audit hook | قراءة/تعديل dynamic + تسجيل نسخة + حدث config.changed | backend/modules/config/**, backend/modules/audit/** | audit test: تعديل قيمة يولّد حدثاً بحقوله + نسخة قابلة للاسترجاع | T-0.2.2 |
| T-0.2.4 | Feature Flags service | حلّ الأعلام بالنطاقات + protected flags + حدث feature_flag.changed | backend/modules/feature_flags/** | flag tests: التعطيل يعمل؛ protected يرفض؛ الحدث يُسجَّل | T-0.2.3 |
| T-0.2.5 | profiles/bundles files | ملفات `configs/local|demo|staging|production` + `configs/bundles/*` بمفاتيح موثّقة | configs/**, specs/configuration.md | profile tests: الأربعة تجتاز validation؛ التوثيق يطابق المفاتيح | T-0.2.1 |

## E0.3 — Monolith Skeleton &amp; Boundaries
| ID | العنوان | التسليم | المسارات | القبول/الاختبار | يعتمد |
|---|---|---|---|---|---|
| T-0.3.1 | قالب module قياسي + مولّد سقالة | بنية module موحّدة (api/service/repository/events/migrations/tests + manifest) | backend/modules/_template/**, infrastructure/scripts/** | إنشاء module تجريبي من القالب يمر بالـ CI | T-0.2.1 |
| T-0.3.2 | سقالات الـ modules (~37) | توليد كل modules الكتالوج بسقالة + manifest (Tier/deps/namespace) | backend/modules/** | كل module موجود؛ apps/api يسجّلها ويقلع | T-0.3.1 |
| T-0.3.3 | shared abstractions (عقود) | واجهات FR-0.4 + تنفيذات دنيا للإقلاع | backend/shared/** | unit: العقود مستوردة من modules دون كسر حدود | T-0.3.1 |
| T-0.3.4 | EventBus داخلي | ناقل in-process + عقد نشر/اشتراك | backend/shared/** | unit: نشر/استقبال حدث تجريبي | T-0.3.3 |
| T-0.3.5 | إنفاذ الحدود في CI | قواعد استيراد تطابق Dependency Matrix + منع الصاعد/الدوري/العابر | infrastructure/**, tests/** | boundary test: استيراد ممنوع مُتعمَّد يُفشل CI | T-0.3.2 |

## E0.4 — Infra &amp; Compose *(بوابة: حسم C1–C3)*
| ID | العنوان | التسليم | المسارات | القبول/الاختبار | يعتمد |
|---|---|---|---|---|---|
| T-0.4.1 | Dockerfiles للخدمات الثلاث | api/worker/web صور موحّدة (تعمل بكل البيئات) | apps/**, infrastructure/docker/** | build ينجح؛ لا فروع بيئة في الصور | T-0.3.2 |
| T-0.4.2 | compose base/override/prod | تعريف كل خدمات FR-0.9 + حدود موارد demo + healthchecks | infrastructure/docker/** | compose config صالح للملفات الثلاثة | T-0.4.1, C1–C3 |
| T-0.4.3 | تهيئة Postgres ×4 | سكربت تهيئة القواعد الأربع + اتصال DatabaseRouter بالإعداد | infrastructure/db/**, backend/shared/** | health يرى القواعد الأربع | T-0.4.2 |
| T-0.4.4 | تشغيل Qdrant/OpenSearch/Object/Cache بإعداد demo | تفعيل الخدمات بحدود خفيفة + Neo4j معرّفاً مطفأً (+Ollama/vLLM حسب C7 كتعريف مطفأ) | infrastructure/docker/**, configs/** | compose up كامل؛ خدمات health خضراء؛ neo4j لا يعمل | T-0.4.2 |
| T-0.4.5 | مراقبة حسب C3 | Prometheus (+ما يُحسم) بسجلات JSON | infrastructure/observability/** | مقاييس أساسية تُجمع؛ لا خدمة غير مُراجَعة الترخيص | T-0.4.2 |

## E0.5 — API Health &amp; Service Registry
| ID | العنوان | التسليم | المسارات | القبول/الاختبار | يعتمد |
|---|---|---|---|---|---|
| T-0.5.1 | /health مفصّل | فحص postgres×4/cache/qdrant/opensearch/object + تقرير JSON | backend/modules/monitoring/** | smoke: أخضر عند اكتمال البيئة؛ يحدد الخدمة المتعطلة عند إسقاط واحدة | T-0.4.4 |
| T-0.5.2 | Service Registry (حد أدنى) | manifest الخدمات/الـ modules + تجميع الصحة + endpoint تقرير | backend/modules/service_registry/** | التقرير يطابق الواقع (core/optional/disabled) | T-0.5.1 |
| T-0.5.3 | حدث service.health_alert (حد أدنى) | تسجيل تنبيه عند فشل تبعية في التقرير | backend/modules/{service_registry,audit}/** | إسقاط خدمة ⇒ حدث مسجَّل | T-0.5.2 |

## E0.6 — Web Shell
| ID | العنوان | التسليم | المسارات | القبول/الاختبار | يعتمد |
|---|---|---|---|---|---|
| T-0.6.1 | سقالة Next.js + tokens | مشروع web + design tokens white-label + بنية صفحات | apps/web/**, packages/ui/** | build ينجح؛ tokens موثّقة | T-0.4.1 |
| T-0.6.2 | i18n ar/en + RTL | تبديل لغة كامل + اتجاه صحيح | apps/web/**, packages/ui/** | فحص RTL (snapshot/بصري) للعربية | T-0.6.1 |
| T-0.6.3 | صفحتا الصحة والدخول-placeholder | صفحة صحة تستهلك تقرير /health + صفحة دخول شكلية | apps/web/** | الصحة تعرض حالة كل تبعية؛ لا auth حقيقي | T-0.5.2, T-0.6.2 |

## E0.7 — Worker Skeleton
| ID | العنوان | التسليم | المسارات | القبول/الاختبار | يعتمد |
|---|---|---|---|---|---|
| T-0.7.1 | عملية worker | تشغيل مستقل + استهلاك مهمة no-op من CacheQueue + graceful shutdown | apps/worker/**, backend/shared/** | مهمة تجريبية تُستهلك؛ إيقاف نظيف | T-0.4.4 |
| T-0.7.2 | فصل التوسع بالإعداد | عدد workers/queues من config | configs/**, apps/worker/** | تغيير العدد بالإعداد فقط | T-0.7.1 |

## E0.8 — Portability &amp; Offline
| ID | العنوان | التسليم | المسارات | القبول/الاختبار | يعتمد |
|---|---|---|---|---|---|
| T-0.8.1 | profile validation tests | اختبارات الملفات الأربعة + bundles | tests/** | الأربعة تجتاز؛ كسر مفتاح ⇒ فشل واضح | T-0.2.5 |
| T-0.8.2 | no-external-call test | اختبار يمنع أي نداء شبكي خارجي وقت التشغيل | tests/offline/** | يفشل عند إدخال نداء خارجي تجريبي | T-0.5.1 |
| T-0.8.3 | offline bundle placeholders | سكربتات (export images/wheels/models placeholders + verify/restore) + مسودة offline-install.md | infrastructure/scripts/**, docs/** | تشغيل جاف (dry-run) للسكربتات يوثّق الخطوات | T-0.4.4 |
| T-0.8.4 | قياس زمن الإقلاع | قياس وتوثيق زمن compose up كاملاً على الجهاز | docs/** | ضمن الهدف الموثّق أو مبرَّر | T-0.4.4 |

## E0.9 — Docs, Quality Gates &amp; Handoff
| ID | العنوان | التسليم | المسارات | القبول/الاختبار | يعتمد |
|---|---|---|---|---|---|
| T-0.9.1 | تحديث التوثيق | configuration.md + README لكل profile + troubleshooting أولي | specs/**, docs/**, README.md | Quality Gate «التوثيق محدّث» مستوفى | E0.1–E0.8 |
| T-0.9.2 | مراجعة البوابات + handoff | تشغيل قائمة Quality Gates + تعبئة handoff.md (المنجز/غير المنجز/الملفات/المخاطر/تحذيرات Phase 1) | handoff.md, specs/handoffs/** | كل بوابات §11 خضراء؛ handoff كامل الحقول | T-0.9.1 |

---

## اعتماد المرحلة والخطوة التالية
عند اعتمادك هذه الحزمة (وحسم C1–C5، وخاصة الفئة 3 قبل P0.4): تكون Phase 0 جاهزة للتنفيذ لاحقاً بأي Coding Agent وفق §18 من المنهجية. **الخطوة التصميمية التالية** (في محادثة مستقلة): تصميم **Phase 1 — Governed Core + Screen Builder** بنفس المنهجية Vision → Specify → Clarify → Plan → Tasks.
