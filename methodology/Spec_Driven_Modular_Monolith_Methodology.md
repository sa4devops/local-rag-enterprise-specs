# Spec-driven Development &amp; Modular Monolith Build Methodology
## منهجية تحويل المعمارية إلى مواصفات وكود بأسلوب Modular Monolith

> **Document Title:** Spec-driven Development &amp; Modular Monolith Build Methodology
> **Version:** 2.1 — Final (A1–A11 + D1–D9 مدمجة) · **Status:** Current / Accepted · **Date:** 2026-07-04
> **Supersedes:** v1.0 من هذه الوثيقة
> **Related:** constitution.md · Feature_Technical_Architecture_Catalog.md · open-decisions.md · phase-roadmap.md · coding-standards.md · testing-strategy.md · license-review.md · adr/README.md · handoff.md
> **Authority Order:** المرتبة **2** (بعد constitution.md مباشرة). عند التعارض داخل مستواها: النسخة المرجعية للقواعد التشغيلية الموسّعة هي coding-standards.md وtesting-strategy.md.
> **Intended Audience:** SA · AI Coding Agents · المراجعون
> **Last Reviewed By:** Final Consistency Review (2026-07-02) — اعتُمد من SA
> **Purpose:** منهجية البناء والتنظيم الرسمية قبل أي تنفيذ — **لا كود في هذه الوثيقة**.

**جدول المصطلحات (إلزامي — يمنع الالتباس):**
| المصطلح | المقصود |
|---|---|
| **module** | bounded-context داخلي في الـ Modular Monolith (backend واحد قابل للنشر). |
| **worker** | عملية خلفية غير متزامنة (agents/media/queue consumers) — نفس الـ codebase، عملية منفصلة. |
| **infra service / container** | خدمة بنية تحتية كحاوية مستقلة (Postgres, Qdrant, OpenSearch, Object Storage, Cache/Queue, Neo4j). |
| **connector** | تكامل مع نظام خارجي (MCP / Internal API / Webhook / DB connector). |
| **provider** | مزوّد نموذج (Ollama / vLLM …) خلف LLM Gateway. |
| **datastore** | قاعدة بيانات أو تخزين (ضمن infra services). |

عند ورود «service» دون تحديد، فالمقصود **module**.

---

## 1. Executive Summary

نعتمد **Spec-driven Development بسير عمل متوافق مع GitHub Spec Kit / Spacekit**:
**`Vision → Specify → Clarify → Plan → Tasks → Implement`** — و**Implement ليس الآن**؛ كل مرحلة تُصمَّم في محادثة مستقلة ثم تُنفَّذ لاحقاً، وأي Coding Agent يلتزم **بالملفات والمواصفات فقط**. ونعتمد **Modular Monolith حقيقياً** (ADR-0001: **Accepted**): backend واحد قابل للنشر، modules واضحة الحدود ومفروضة بالأدوات، microservice-ready. **التراخيص Open Decisions** ولا يدخل أي dependency/image/model قبل **License Review** (`decisions/license-review.md`).

## 2. Why Spec-driven Development

يمنع الانحراف (الكود ينفّذ مواصفة معتمدة لا اجتهاد نموذج) · قابل للتسليم عبر جلسات ووكلاء متعددين (specs ثابتة + handoff) · يحفظ القرارات (constitution + ADRs) · قابل للمراجعة (acceptance + Quality Gates) · محايد للأداة (Claude Code/Codex/Cursor/Windsurf/Cline/Aider/OpenHands/Continue…).

**محتوى ملفات المنهجية:**
- **vision.md:** المشكلة · الأهمية · المستخدمون · البيئة (شبكة مغلقة) · ما يحلّه/لا يحلّه · مبادئ غير قابلة للتفاوض · تعريف النجاح · حدود MVP · حدود المنتج · المخاطر.
- **spec.md (لكل نطاق/مرحلة):** وصف عالي المستوى · متطلبات وظيفية/غير وظيفية · قيود · مصادر الحقيقة · صلاحيات · Audit · RAG · Media · Admin · Deployment · قيود offline · لغة/RTL · أمن · «لا LLM كمصدر حقيقة» · «لا external APIs في runtime» · «لا hardcoded configuration».
- **clarification.md:** الأسئلة المفتوحة · الخيارات · مالك القرار · blocker؟ (بفئات تصنيف القرارات) · موعد الحسم · الأثر.
- **plan.md:** الترتيب · التبعيات · قرارات معمارية · مخاطر · خطة اختبار · خطة ترحيل بيانات · خطة نشر · خطة تراجع · معايير قبول.
- **tasks:** Epics → Features → User/Technical Stories → Tasks → Subtasks + Acceptance + Tests؛ كل task صغير بحجم جلسة وكيل واحدة وبمسارات مسموحة.
- **handoff.md / review:** القسمان 13–14 أدناه.

## 3. Why Modular Monolith First

**الفرق:** Monolith عشوائي (تشابك بلا حدود) ↔ **Modular Monolith المعتمد** (backend واحد، modules بحدود مفروضة، لكل module: domain/service/api/repository/events/migrations/tests، لا وصول مباشر لجداول الغير، dependencies معلنة، microservice-ready) ↔ Microservices (تعقيد شبكي/معاملاتي/تشغيلي سابق لأوانه).
**لماذا الآن:** يعمل على MSI Titan · مناسب لـ Local Demo · أقل تعقيداً وأسرع بناءً واختباراً وdebugging · يقلّل مشاكل الشبكة والمعاملات · يُبقي كل الخدمات حاضرة كـ modules · يسمح بالفصل لاحقاً.
**شروط أن يكون حقيقياً:** boundaries مفروضة (CI) · module interfaces معلنة · لا coupling عشوائي · لا direct table access عابر · config namespace لكل module · events + audit hooks · tests · migrations منظمة لكل module.

## 4. Future Microservices Extraction Strategy

الفصل خيار مستقبلي عند الحاجة (حجم/حِمل/عزل)، مصمَّم من الآن ليتم **دون إعادة كتابة**: نداءات عبر **contracts** في `backend/shared` (تُستبدل بـ RPC/REST) · **Events** عبر ناقل in-process قابل للترقية إلى message bus · schema + config namespace مستقلان لكل module (الاستخراج = نقل schema + نشر خدمة + تبديل الواجهة بالإعداد) · **مرشحون أوائل:** media, rag/search, llm-gateway, sql-agent · **باقون طويلاً:** identity/permissions/metadata/records (معاملاتية) · شرط الفصل: ADR + contract tests.

## 5. Required Specification Files

vision.md · spec.md · clarification.md · plan.md · architecture.md وفروعها (data/permission/agent/orchestration/media/integration/deployment) · configuration.md · feature-catalog / service-catalog · coding-standards.md · testing-strategy.md · license-review.md · adr/ · tasks/ · handoff.md · runbooks/ (troubleshooting, backup-restore, offline-install). وظيفة كل ملف وتوقيت تحديثه في §12. **القاعدة الذهبية:** الـ specs تسبق الكود؛ أي انحراف يتطلب تحديث spec/ADR أولاً.

## 6. Recommended Repository Structure (المستودع الموحّد للمنتج)

```
repo/
  apps/            # web (Enterprise UI) · api (Monolith/FastAPI) · worker
  backend/
    modules/       # 36 module — كلٌّ: api/ service/ repository/ events/ migrations/ tests/ + manifest
    shared/        # contracts فقط: cache, queue, lock, object-storage(fs|s3), llm-provider, identity-provider, db-router, event-bus, media-processor
  packages/        # ui (RTL-ready) · sdk · shared-types (API contracts)
  infrastructure/  # docker/ · db/ · observability/ · scripts/ (offline bundle, verify, restore)
  specs/           # كل المواصفات + adr/ + tasks/ + handoffs/  (تُزرع من حزمة docs هذه — مهمة T-0.1.3)
  configs/         # local/ demo/ staging/ production/ + bundles/
  tests/           # unit/ integration/ e2e/ security/ permission/ migration/ offline/
  docs/            # runbooks, troubleshooting, offline-install
  constitution.md  · handoff.md · README.md
```
**تفسيرات:** migrations **داخل كل module** لضبط الملكية، بأداة موحّدة تجمّعها · profiles/bundles في `configs/` (env فقط) · العقود المشتركة في `packages/shared-types` و`sdk` · برومبتات وكلاء **النظام** (لا Coding Agents) تُدار كـ metadata/OKF لا في الكود · OKF bundles ملفات markdown+YAML محلية · handoff حالي في الجذر + أرشيف في `specs/handoffs/`.

## 7. Module Catalog — **36 module** (35 الأصلية + `chat` المضاف بمراجعة A5)

**الطبقات (Tiers) — الاعتماد هابط فقط:** F (Foundational/Cross-cutting) → 1 (Governance) → 2 (Metadata &amp; Records &amp; Operations) → 3 (Knowledge &amp; AI) → 4 (Integration). العابرة (config/flags/service-registry/audit/monitoring/security-policy) يعتمد عليها الجميع ولا تعتمد على modules المجال.
**ممنوع افتراضياً:** أي اعتماد صاعد أو دوري · وصول مباشر لجداول module آخر · استدعاء LLM خارج llm-gateway · تجاوز permissions/audit. **Audit events** لكل module في الكتالوج §11؛ **tests** في testing-strategy.md.

| Module | Tier | يملك / لا يملك | Schema | واجهة | Deps مسموحة | فصل؟ | أولوية |
|---|---|---|---|---|---|---|---|
| config | F | الإعداد الفعّال/namespaces / لا منطق أعمال | platform | ConfigAPI | (base) | لا | P0 |
| feature-flags | F | أعلام القدرات + protected list / لا business rules | platform | FlagAPI | config | لا | P0 |
| service-registry | F | كتالوج/صحة/تبعيات / لا lifecycle حاويات | – | RegistryAPI | config | لا | P0 |
| audit | F | سجل append-only / لا تعديل بيانات مجال | platform | AuditSink | config | لا | P0 |
| monitoring | F | مقاييس/صحة / لا business | – | MetricsAPI | config, service-registry | جزئي | P0 |
| security-policy | F | سياسات أمن/بوابات / لا إنفاذ مباشر | platform | PolicyAPI | config, audit | لا | P1 |
| license-about | F | التراخيص/attribution | platform | AboutAPI | config | لا | P0 |
| identity | 1 | مستخدمون/مصادقة/IdP-adapter / لا org | platform | IdentityAPI | config, audit | جزئي | P1 |
| organization | 1 | قطاعات/إدارات/عضوية / لا أدوار | platform | OrgAPI | identity, config, audit | جزئي | P1 |
| permissions | 1 | إنفاذ RBAC/ABAC/ReBAC/تصنيف | platform | PermissionAPI (Gate) | identity, organization, security-policy, config, audit, feature-flags | لا | P1 |
| admin | 1 | تجميع عمليات الأدمن / **لا يملك بيانات مجال** | – | AdminAPI (يفوّض) | واجهات الـ modules | لا | P1 |
| screens | 2 | تعريفات الشاشات / لا بيانات السجلات | platform | ScreenMetaAPI | permissions, config, audit, feature-flags | جزئي | P1 |
| fields | 2 | تعريفات الحقول / لا القيم | platform | FieldMetaAPI | screens, permissions, audit | جزئي | P1 |
| migrations | 2 | آلية الترحيل المحكوم / لا DDL من نموذج | platform | MigrationAPI | config, audit | لا | P1 |
| database-generation | 2 | توليد schema من الميتاداتا عبر migrations | platform/apps | GenAPI | screens, fields, migrations, permissions, audit, config | جزئي | P1 |
| records | 2 | CRUD الكيانات + RLS/FLS / لا تعريف الشاشات | apps (schema-per-app) | RecordAPI | screens, fields, permissions, audit, config | جزئي | P1 |
| workflows | 2 | دورة حياة workflows / لا اعتماد نهائي | platform | WorkflowAPI | records, screens, permissions, audit, config, feature-flags | جزئي | P2 |
| approvals | 2 | بوابات الاعتماد + SoD / لا منطق workflow | platform | ApprovalAPI | workflows, permissions, audit, notifications | جزئي | P2 |
| tasks | 2 | مهام/قوالب | platform | TaskAPI | permissions, audit, config, (llm-gateway) | جزئي | P2 |
| projects | 2 | تجميع محادثات/ملفات | platform | ProjectAPI | permissions, files, audit | جزئي | P2 |
| notifications | 2 | إشعارات/قنوات | platform | NotifyAPI | permissions, audit, config | جزئي | P2 |
| files | 2/3 | إدارة الملفات/الوصول للتخزين / لا معالجة | apps + Obj | FileAPI | permissions, audit, config | نعم | P3 |
| okf | 3 | كتالوج معرفة/قاموس / **ليس مصدر حقيقة** | platform + bundles | KnowledgeAPI | config, audit | نعم | P3 |
| model-registry | 3 | كتالوج نماذج + capability mapping / لا تشغيل | platform | ModelRegAPI | config, audit | جزئي | P3 |
| provider-registry | 3 | المزوّدون/endpoints / لا اختيار النموذج | platform | ProviderRegAPI | config, audit | جزئي | P3 |
| llm-gateway | 3 | توجيه/تنفيذ الاستدعاء (OpenAI-compatible) — **البوابة الوحيدة** | – | GatewayAPI | model-registry, provider-registry, config, audit | نعم | P3 |
| search | 3 | فهرسة/بحث نصي وهجين | apps + infra | SearchAPI | config, permissions, audit | نعم | P3 |
| rag | 3 | استرجاع مصفّى بالصلاحية + provenance / لا توليد نهائي | apps + Vec | RagAPI | files, search, permissions, model-registry, llm-gateway, audit, okf | نعم | P3 |
| sql-agent | 3 | SQL قراءة فقط (allow-list/RLS) / لا DDL/DML | apps (read) | SqlAgentAPI | permissions, audit, config, llm-gateway | نعم | P3 |
| media | 3 | pipeline الوسائط (OCR/vision/audio/video) / لا تخزين خام | Obj + apps | MediaAPI | files, model-registry, llm-gateway, audit, permissions, config | نعم | P3 |
| **chat (A5)** | 3 | **المحادثات/الجلسات وسياقها ورسائلها** / لا المعرفة ولا النماذج | platform | ChatAPI | permissions, llm-gateway, rag, projects, audit, config | نعم | P4 (Phase 6) |
| reports | 3 | تقارير قسماً قسماً + استشهاد | reporting | ReportAPI | records, rag, sql-agent, files, permissions, audit, llm-gateway | جزئي | P4 |
| integrations | 4 | تسجيل/حوكمة الموصلات | integration | IntegrationAPI | permissions, config, audit, feature-flags | نعم | P4 |
| mcp-connectors | 4 | جسر MCP للأدوات | integration | McpAPI | integrations, permissions, audit, config | نعم | P4 |
| app-store | 4 | متجر المستخدم + ربط الحسابات | integration | StoreAPI | integrations, permissions, audit, feature-flags | نعم | P4 |
| backup-restore | Ops | نسخ/استعادة (Ops) | Obj + DB | BackupAPI | config, audit | نعم | P5 |

## 8. Module Dependency Matrix

- **قاعدة الاتجاه:** هابط فقط عبر الطبقات (4→3→2→1→F). **A11 (نصية):** الاعتماد **داخل نفس الطبقة مسموح فقط إذا كان مُدرَجاً صراحةً في manifest الـ module وغير دوري** (أمثلة معتمدة: approvals→workflows، rag→search/files، chat→rag/llm-gateway).
- **Allowed:** عمود «Deps مسموحة» في §7 هو المصدر الرسمي.
- **Forbidden:** الصاعد/الدوري · الوصول المباشر لجداول الغير · LLM خارج llm-gateway · تجاوز permissions/audit · اعتماد الطبقة F على modules المجال · اعتماد أي module على okf كمصدر حقيقة.
- **قواعد النداء الداخلي:** عبر contracts في `backend/shared` فقط · الأحداث عبر event bus داخلي قابل للترقية · الوصول للبيانات عبر repository/service للـ module المالك.
- **منع الدورات:** فحص آلي (import-linter/boundary checks) في CI يرفض أي مخالفة؛ كسر القاعدة يتطلب **ADR** أولاً.

## 9. Coding Rules for AI Agents (النسخة المرجعية الموسّعة: `methodology/coding-standards.md`)

لا كود خارج scope المهمة ولا تعديل خارج قائمة ملفاتها · لا تغيير معمارية دون ADR · لا dependency دون License Review · لا external API في runtime · لا hardcoded (secrets/localhost/endpoints/model names/paths) · لا direct DB access خارج repository/service المالك · لا LLM call خارج llm-gateway · لا bypass لـ Permission/Audit · لا DDL من LLM؛ migrations عبر خط الحوكمة · كل feature ⇒ tests؛ كل permission ⇒ **deny test**؛ كل audit event ⇒ test؛ كل config ⇒ default + validation · احترام boundaries · أخطاء typed قابلة للتتبع · **عند الغموض: اسأل ولا تكتب** · **Reference-aware clean implementation (D8):** قراءة كود OSS للفهم والمقارنة مسموحة؛ ممنوع النسخ المباشر (ملفات/مقاطع طويلة/إعادة تسمية متغيّرات) دون License Review وامتثال ترخيص — النص الكامل الملزم في `methodology/coding-standards.md`.

## 10. Testing Strategy (النسخة المرجعية الموسّعة: `methodology/testing-strategy.md`)

unit · integration · e2e · permission (deny لكل endpoint + RLS/FLS) · audit · migration (apply/rollback) · rag (لا تسريب خارج الصلاحية) · sql-agent safety (رفض DDL/DML/خارج allow-list) · media pipeline · configuration profile · feature flag (المحمية ترفض) · connector · **offline/no-external-call** · backup/restore · smoke/health. لكل نوع: هدف + موضع + مثال قبول + مرحلة البدء (الجدول الكامل في الملف المرجعي).

## 11. Quality Gates (قبل أي merge/قبول)

الاختبارات ذات الصلة خضراء · permission checks + deny tests موجودة · audit events مُنفَّذة · لا secrets ولا external calls · migrations معتمدة · License Review لأي dependency جديد · التوثيق محدّث · handoff محدّث · config defaults + validation · rollback مأخوذ بالاعتبار · RTL/accessibility للواجهة · error handling · **boundaries CI أخضر** · **lockfiles/digest pinning محدّثة**.

## 12. Documentation Strategy

كل ملف من §5 له مالك وتوقيت تحديث (بداية/عند التغيير/مستمر/بعد كل جلسة). **قاعدة:** التوثيق جزء من Definition of Done — لا feature مكتمل بلا تحديث المستندات المعنية + handoff. مواقع الملفات في `github-docs-structure.md` (حزمة الوثائق) ثم `specs/` (المستودع الموحّد).

## 13. ADR Strategy

مجلد `decisions/adr/`. صيغة كل ADR: العنوان · السياق · القرار · البدائل · السبب · المخاطر · الأثر · التاريخ · الحالة (Proposed/Accepted/Superseded). **السجل الكنسي للقائمة والترقيم: `decisions/adr/README.md`** (الترقيم المعتمد ADR-0001..0010 + التكميلية 0011+؛ الترقيم القديم في v1.0 من هذه الوثيقة **Superseded**). أي قرار معماري مهم أو كسر لقاعدة boundaries يتطلب ADR **قبل** التنفيذ.

## 14. Handoff Strategy

`handoff/handoff.md` إلزامي بعد كل جلسة/مرحلة (القالب الرسمي في الملف نفسه): التاريخ · المرحلة · المهمة · الهدف · المنجز · غير المنجز · الملفات المعدّلة · القرارات · المشاكل · المخاطر · الاختبارات · الخطوة التالية · **ما لا يُلمس** · ملاحظات للوكيل التالي. أرشفة بتاريخها في `handoff/archive/` (وفي المستودع الموحّد: `specs/handoffs/`). لا تُغلق مهمة دون handoff + قائمة اختبارات + تقرير مختصر.

## 15. License Review Workflow

**المبدأ (دستوري):** لا يدخل أي dependency/repository/container image/**model weights** قبل صف مراجعة معتمد في `decisions/license-review.md` **للإصدار/الصورة المحددة**؛ الترقية تعيد المراجعة؛ البوابة **متكررة** لكل إضافة. السير: اقتراح → تعبئة صف → مراجعة (تقنية + قانونية عند اللزوم) → قرار (Approved / Conditional / Rejected / Needs Legal Review) → الدخول عند Approved/Conditional فقط (+attribution إن لزم). **الحساسة المعروفة (Needs License Review):** Redis/Valkey · MinIO · Grafana/Loki · PyMuPDF · ffmpeg · أوزان النماذج. القالب والصفوف المزروعة في `decisions/license-review.md`.

## 16. Configuration-driven Development Rules

هرمية: defaults → environment profile → capability bundles → runtime overrides (Config Registry) → secrets · **لا hardcoded** إطلاقاً · namespace لكل module ولا يقرأ إعداد غيره · كل مفتاح: default + validation + fail-fast للحرِج · توثيق static (restart) مقابل dynamic (live) · flags بنطاقات + protected · secrets عبر آلية أسرار خارج المستودع (طبقة العمليات) · **abstractions قابلة للتبديل بالإعداد:** Cache/Queue/Lock (افتراضي **memory/PostgreSQL**؛ Valkey optional-ready — D4) · ObjectStorage (افتراضي **filesystem**؛ MinIO|SeaweedFS|S3 لاحقاً — D5) · Observability (الخط الأساسي الآن؛ التوسعة P8 — D6) · LLM provider (Ollama|vLLM) · identity provider · db-router · **Qdrant وOpenSearch حاضران افتراضاً في Local Demo** (pgvector/PG-FTS ضمن low-resource bundle الصريح فقط) · **lockfiles لكل مديري الحزم + digest pinning للصور** (A8) قاعدة أساسية لإعادة البناء مغلقاً.

## 17. Deployment Portability Rules

صورة واحدة لكل خدمة تُبنى مرة وتعمل في كل البيئات · ممنوع كود/فرع بيئة وممنوع production fork · الفرق configuration فقط (env/config/resources/model-selection/provider-endpoints/paths/hosts/workers/secrets/TLS/backup/monitoring/profile) · backend عديم الحالة (جلسات cache/JWT) · workers تتوسّع مستقلة · inference على عُقد GPU بالإعداد · نفس migrations في كل البيئات · **مستخدم DB بأدنى صلاحية لكل قاعدة من التهيئة الأولى (A8)** · Environment Profiles × Capability Bundles · offline bundle (Docker images + Python wheels/uv cache + pnpm store + model files) موقّعة + استعادة + تحقق + **قناة نقل الكود** (git bundle/حزمة إصدار موقّعة من GitHub إلى الشبكة المغلقة — D7) · **مسار K8s/OpenShift لاحقاً = إضافة manifests تحت `infrastructure/` دون أي تعديل كود** · الترقية Local→Production = تغيير إعداد فقط (مُختبرة).

## 18. How to Use This Methodology with Any Coding Agent

لكل مهمة في محادثة مستقلة: (١) يقرأ الوكيل بالترتيب: README → constitution → هذه المنهجية → الكتالوج → open-decisions → phase-roadmap → تصميم مرحلته → handoff → بطاقة المهمة؛ (٢) يؤكد الفهم و**يسأل عند الغموض ولا يكتب**؛ (٣) يُخرج patch محدوداً ضمن المسارات المسموحة فقط، ولا يلمس ADRs؛ (٤) يكتب/يشغّل الاختبارات المطلوبة (deny + audit + unit)؛ (٥) يجتاز Quality Gates + License Review عند أي dependency؛ (٦) يحدّث handoff + تقرير مختصر. **قواعد منع التشتت:** محادثة = task واحد · scope واضح · ملفات محددة قراءةً وتعديلاً · patch محدود · لا تعديل خارج القائمة · لا تغيير ADR دون طلب · الإنهاء بـ handoff + اختبارات + تقرير. الأداة محايدة، وCoding Model (Qwen/DeepSeek/GLM Coder…) منفصل عنها.

## 19. Open Decisions — مرجع مُلزم

**المرجع الوحيد:** `decisions/open-decisions.md` (الفئات الخمس + جدول تفصيلي لكل قرار). لا تُكرَّر هنا. الحالة: **لا Blockers قبل التصميم**؛ ADR-0001 **Accepted**.

## 20. Final Recommendation

المنهجية الرسمية: **Spec-driven (Spec Kit/Spacekit-compatible) + Modular Monolith حقيقي microservice-ready**. قبل أي تنفيذ: زرع `specs/` من حزمة الوثائق هذه، وتفعيل بوابات CI (boundaries/secrets/offline)، وحسم بنود الفئتين 2 و3 في مواعيدها. ثم: تصميم كل مرحلة في محادثة مستقلة وفق `phase-roadmap.md`، والتنفيذ لاحقاً مرحلةً مرحلة بأي Coding Agent ملتزم بهذه الوثيقة. بعد خط الأساس المعماري (م21 — `v1.0-architecture-baseline`): حلقة Specify/Clarify **للمعمارية** لا تُفتح من جديد إلا عبر ADR؛ التوضيحات والتفاصيل غير المعمارية لا تعيد فتحها.
