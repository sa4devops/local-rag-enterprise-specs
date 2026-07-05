> ⚠️ SUPERSEDED — لا يُستخدم للتنفيذ. المرجع الحالي: حزمة v2.0 (انظر superseded/README.md). تاريخ الوسم: 2026-07-03.

# Spec-driven Development &amp; Modular Monolith Build Methodology
## منهجية تحويل المعمارية إلى مواصفات وكود بأسلوب Modular Monolith
> وثيقة **منهجية بناء وتنظيم فقط**. لا كود · لا Phase-0/1 Prompts · لا implementation. تأتي **بعد** Feature &amp; Technical Architecture Catalog و**قبل** أي تنفيذ.

**توضيح مصطلح «service» (تصحيح 1.7) — تُستخدم هذه المصطلحات بدقة في كامل الوثيقة:**
| المصطلح | المقصود |
|---|---|
| **module** | bounded-context داخلي في الـ Modular Monolith (backend واحد قابل للنشر). |
| **worker** | عملية خلفية غير متزامنة (agents/media/queue consumers) — نفس الـ codebase، عملية منفصلة. |
| **infra service / container** | خدمة بنية تحتية كحاوية مستقلة (Postgres, Qdrant, OpenSearch, MinIO, Redis/Valkey, Neo4j). |
| **connector** | تكامل مع نظام خارجي (MCP / Internal API / Webhook / DB connector). |
| **provider** | مزوّد نموذج (Ollama / vLLM …) خلف LLM Gateway. |
| **datastore** | قاعدة بيانات أو تخزين (من ضمن infra services). |

عند ورود «service» دون تحديد، فالمقصود **module** ما لم يُذكر خلاف.

---

## 1. Executive Summary

نعتمد **Spec-driven Development** (شبيه GitHub Spec Kit): لا يكتب أي AI Coding Agent كوداً قبل أن تمرّ الفكرة عبر Vision → Specify → Clarify → Plan → Tasks، ثم Implement/Test/Review/Handoff/Improve لاحقاً. ونعتمد **Modular Monolith حقيقياً** (backend واحد قابل للنشر، modules واضحة الحدود، dependencies مضبوطة، لا وصول عشوائي بين modules، وكل module **microservice-ready** قابل للفصل لاحقاً). الغاية: منع الكود العشوائي، وضبط الحدود، وضمان قابلية النقل والاختبار والتوثيق والتسليم عبر عدة محادثات ووكلاء. **التراخيص تبقى Open Decisions** ولا يدخل أي dependency/repo/image إلى المنتج إلا بعد **License Review**.

---

## 2. Why Spec-driven Development

- **يمنع الانحراف:** الكود ينفّذ مواصفة مُتفقاً عليها، لا اجتهاد نموذج.
- **قابل للتسليم عبر جلسات متعددة:** كل جلسة تقرأ specs ثابتة وتخرج patch محدوداً.
- **يحافظ على القرارات المثبتة:** constitution + ADRs تمنع كسر المبادئ (LLM ليس مصدر حقيقة، صلاحية قبل الاسترجاع، لا Open WebUI كوجه، config-only deployment…).
- **قابل للمراجعة والقبول:** لكل مهمة acceptance criteria واختبارات قبل الدمج.
- **محايد للأداة:** أي Coding Agent (Claude Code/Codex/Cursor/Windsurf/Cline/Aider/OpenHands/Continue) ينفّذ نفس المواصفات.

**التدفق (بدون دخول implementation هنا):**
1. **Vision** — لماذا ولمن وما الحدود.
2. **Specify** — ماذا (وظيفي/غير وظيفي/قيود/مصادر حقيقة).
3. **Clarify** — الأسئلة والقرارات المفتوحة ومالكوها.
4. **Plan** — الترتيب/التبعيات/المخاطر/الاختبار/الترحيل/النشر/التراجع.
5. **Tasks** — Epics→Features→Stories→Tasks→Subtasks صغيرة قابلة للتنفيذ.
6. **Implement** (لاحقاً فقط).
7. **Test** — حسب Testing Strategy.
8. **Review** — كود/معمارية/صلاحيات/تراخيص/اختبارات/أمن/قابلية نقل/لا hardcoded.
9. **Handoff** — تحديث handoff.md بعد كل جلسة.
10. **Improve** — تحسين تكراري بمراجعة ADRs.

**محتوى الملفات (كما طلبت):**
- **vision.md:** المشكلة · أهمية النظام · المستخدمون · البيئة (شبكة مغلقة) · ما يحلّه/لا يحلّه · مبادئ غير قابلة للتفاوض · تعريف النجاح · حدود MVP · حدود المنتج النهائي · مخاطر المشروع.
- **spec.md:** وصف عالي المستوى · متطلبات وظيفية/غير وظيفية · قيود · مصادر الحقيقة · صلاحيات · Audit · RAG · Media · Admin · Deployment · قيود offline · لغة/RTL · قيود أمن · «لا LLM كمصدر حقيقة» · «لا external APIs في runtime» · «لا hardcoded configuration».
- **clarification.md / questions.md:** الأسئلة المفتوحة · القرارات غير المحسومة · الخيارات · مالك القرار · blocker؟ · موعد الحسم · أثر القرار على المعمارية.
- **plan.md:** الترتيب العام · المراحل · dependencies · architecture decisions · إدارة مخاطر · testing plan · data migration plan · deployment plan · rollback plan · acceptance criteria.
- **tasks:** Epics/Features/User Stories/Technical Stories/Tasks/Subtasks + Acceptance Criteria + Tests؛ كل task **صغير ومحدد** لا يتجاوز سياق الوكيل.
- **handoff.md** و**review**: مفصّلان في الأقسام 13 و2 أعلاه.

---

## 3. Why Modular Monolith First

**الفرق (تصحيح 1.6):**
- **Monolith عشوائي:** كل شيء متشابك، وصول مباشر للجداول، لا حدود → دَين تقني.
- **Modular Monolith (المعتمد):** backend واحد قابل للنشر، **modules واضحة الحدود**، لكل module domain/service/API/tests/migrations، **لا وصول مباشر لجداول module آخر** (فقط عبر خدمته/واجهته الداخلية)، dependencies مضبوطة، **microservice-ready**.
- **Microservices:** خدمات منفصلة عبر الشبكة → تعقيد networking/transactions/ops غير مناسب الآن لجهاز واحد.

**لماذا الآن:** يعمل على MSI Titan · مناسب لـ Local Demo · أقل تعقيداً · أسرع بناءً · أسهل اختباراً/debugging · يقلّل مشاكل الشبكة والمعاملات · يُبقي كل الخدمات كـ modules حاضرة · يسمح لاحقاً بفصل module إلى microservice.

**شروط أن يكون حقيقياً:** boundaries واضحة · module interfaces · لا coupling عشوائي · لا direct table access بين modules · config namespaces لكل module · events + audit hooks · tests · migrations منظمة لكل module.

---

## 4. Future Microservices Extraction Strategy

الفصل خيار **مستقبلي عند الحاجة** (حجم/حِمل/عزل تنظيمي)، ويُصمَّم من الآن ليتم **دون إعادة كتابة**:
- كل module يتواصل عبر **واجهة داخلية (internal interface/contract)** لا عبر جداول الغير → استبدالها بـ RPC/REST لاحقاً بلا تغيير المنطق.
- **Events** بين modules عبر ناقل داخلي (in-process) قابل للترقية إلى message bus (queue) دون تغيير المُنتِج/المستهلك.
- **config namespace** و**schema** مستقلان لكل module → استخراج module يعني نقل schema + نشر الخدمة + تبديل الواجهة بالإعداد.
- **مرشحون أوائل للفصل** (عند التوسع): media، rag/search، llm-gateway، sql-agent (أحمال حسابية عالية). **مرشحون للبقاء** في المونوليث طويلاً: identity/permissions/metadata/records (معاملاتية ومترابطة).
- شرط الفصل: توثيق ADR + الحفاظ على الحدود + اختبارات تعاقد (contract tests).

---

## 5. Required Specification Files

| الملف | الوظيفة | متى يُحدَّث |
|---|---|---|
| specs/vision.md | لماذا/لمن/الحدود/المبادئ | بداية المشروع + عند تغيّر جوهري |
| specs/spec.md | ماذا (وظيفي/غير وظيفي/قيود) | عند تغيّر المتطلبات |
| specs/clarification.md | الأسئلة/القرارات المفتوحة | مستمر حتى الحسم |
| specs/plan.md | الترتيب/التبعيات/المخاطر/الاختبار/النشر/التراجع | لكل مرحلة |
| specs/architecture.md | المعمارية العامة | عند قرار معماري |
| specs/data-architecture.md | القواعد/الفصل/الترحيل | عند تغيّر البيانات |
| specs/permission-architecture.md | RBAC/ABAC/ReBAC/التصنيف/الإنفاذ | عند تغيّر الصلاحيات |
| specs/agent-architecture.md | الوكلاء/العقود/النماذج لكل وكيل | عند تغيّر الوكلاء |
| specs/orchestration.md | Orchestrator/Router/Gates/No-Guessing | عند تغيّر التنسيق |
| specs/media-architecture.md | pipeline الوسائط/التوجيه/الفهرسة | عند تغيّر الوسائط |
| specs/integration-architecture.md | MCP/API/Webhook/DB/App Store | عند تغيّر التكامل |
| specs/deployment-architecture.md | Portability/Profiles/Bundles | عند تغيّر النشر |
| specs/configuration.md | مفاتيح الإعداد/الأعلام/الـ namespaces | مستمر |
| specs/feature-catalog.md · service-catalog.md | مرجع الميزات/الوحدات (من الوثيقة السابقة) | عند إضافة/تعديل |
| specs/coding-standards.md | معايير الكود + قواعد الوكلاء | مستمر |
| specs/testing-strategy.md | أنواع الاختبار والقبول | مستمر |
| specs/license-review.md | مراجعة تراخيص كل dependency | قبل أي dependency/image جديد |
| specs/adr/ADR-XXXX.md | قرارات معمارية | لكل قرار |
| specs/tasks/*.md | Epics/Stories/Tasks | لكل مهمة |
| handoff.md | تسليم بين الجلسات | بعد كل جلسة/مرحلة |
| docs/runbooks/ · troubleshooting.md · backup-restore.md · offline-install.md | تشغيل | عند نضج التشغيل |

> **قاعدة ذهبية:** الـ specs تسبق الكود دائماً، والكود لا يخالف spec؛ أي انحراف يتطلب تحديث spec/ADR أولاً.

---

## 6. Recommended Repository Structure

هيكل مقترح (محسّن عن مثالك، مضبوط لـ Modular Monolith + Python/FastAPI backend + Next.js frontend + workers):

```
repo/
  apps/
    web/                      # Enterprise UI (Next.js/React/TS) — الوجه النهائي
    api/                      # Modular Monolith (FastAPI) — نقطة النشر الرئيسية
    worker/                   # workers (agents/media/queue) — نفس الـ codebase
  backend/
    modules/                  # كل module: domain/ service/ api/ repository/ events/ migrations/ tests/
      config/  feature_flags/  service_registry/  audit/  monitoring/  security_policy/   # foundational/cross-cutting
      identity/  organization/  permissions/                                             # governance
      admin/                                                                             # admin API/UI composition (لا يملك domain data)
      screens/  fields/  records/  database_generation/  migrations/                     # metadata & records
      workflows/  approvals/  tasks/  projects/  notifications/  files/                   # domain
      okf/  model_registry/  provider_registry/  llm_gateway/  rag/  search/  sql_agent/  media/  reports/   # knowledge & AI
      integrations/  mcp_connectors/  app_store/                                          # integration
      backup_restore/                                                                     # ops-facing
    shared/                   # abstractions/contracts فقط (cache, object-storage, llm-provider, identity-provider, db-router, event-bus)
  packages/
    ui/                       # مكوّنات UI مشتركة (RTL-ready)
    sdk/                      # عميل API مُولّد من العقود
    shared-types/             # أنواع مشتركة (contracts) بين web/api
  infrastructure/
    docker/                   # Dockerfiles + compose (base/override/prod)
    db/                       # تهيئة القواعد الأربع + سياسات
    observability/            # إعداد Prometheus/بدائل (قابل للتبديل)
    scripts/                  # offline-bundle / restore / verify
  specs/                      # كل ملفات المواصفات + adr/ + tasks/
  configs/
    local/  demo/  staging/  production/    # Environment Profiles (env only)
    bundles/                                # Capability Bundles (low-resource/full-stack/media/security/graph/integration)
  tests/
    unit/  integration/  e2e/  security/  permission/  migration/  offline/
  docs/                       # runbooks/ troubleshooting/ backup-restore/ offline-install
  constitution.md             # القواعد غير القابلة للتفاوض (Spec Kit)
  handoff.md                  # سجل التسليم الحالي
  README.md
```

**تفسير القرارات:**
- **specs/** جذرية ومركزية (مصدر الحقيقة للتصميم)؛ **adr/** و**tasks/** بداخلها.
- **migrations** *داخل كل module* (`backend/modules/<m>/migrations/`) لضبط الملكية والحدود، مع أداة ترحيل موحّدة تجمّعها؛ لا migrations متناثرة عابرة للـ modules.
- **config profiles** في `configs/` مفصولة عن الكود (env فقط)؛ **bundles** منفصلة عن **environments**.
- **tests** مصنّفة حسب النوع + مرايا داخل كل module لاختباراته الوحدوية.
- **shared types / API contracts** في `packages/shared-types` و`packages/sdk` (عقد واحد بين الواجهة والـ API).
- **UI components** في `packages/ui` (RTL-ready) و`apps/web`.
- **agent prompts** (لمهام الوكلاء داخل النظام، لا برومبتات الـ Coding Agent) تُخزَّن كـ **metadata/OKF** لا في الكود، وتُدار من model/agent config؛ نُسخها التوثيقية في `specs/agent-architecture.md`.
- **OKF bundles** في مسار معرفة (مثل `configs/okf/` أو `backend/modules/okf/bundles/`) — ملفات markdown+YAML محلية.
- **handoff logs** في `handoff.md` (الحالي) + أرشيف في `specs/handoffs/` إن رغبت بالتأريخ.
- **license-review** في `specs/license-review.md` (إلزامي قبل أي dependency/image).

---

## 7. Module Catalog

> أعمدة: Module · Tier · المسؤولية (يملك / لا يملك) · Schema · واجهات · Deps المسموحة · Events · قابل للفصل · أولوية. **الممنوع افتراضياً** = أي dependency خارج المسموح + أي اعتماد «صاعد» بين الطبقات + أي وصول مباشر لجداول module آخر أو استدعاء LLM خارج llm-gateway أو تجاوز permissions/audit. **audit events** لكل module موثّقة في Audit Events Catalog (الوثيقة السابقة). **tests** لكل module في Testing Strategy (قسم 10).

**الطبقات (Tiers) — الاعتماد يتجه للأسفل فقط:** F (Foundational/Cross-cutting) → 1 (Governance) → 2 (Metadata &amp; Records) → 3 (Knowledge &amp; AI) → 4 (Integration). العابرة (config/feature-flags/service-registry/audit/monitoring/security-policy) يعتمد عليها الجميع، ولا تعتمد على modules المجال.

| Module | Tier | يملك / لا يملك | Schema | واجهات | Deps مسموحة | Events | فصل؟ | أولوية |
|---|---|---|---|---|---|---|---|---|
| config | F | إعداد فعّال/namespaces / لا منطق أعمال | platform | ConfigAPI | (base) | config.changed | لا (foundational) | P0 |
| feature-flags | F | أعلام القدرات / لا business rules | platform | FlagAPI | config | flag.changed | لا | P0 |
| service-registry | F | كتالوج/صحة/تبعيات / لا lifecycle حاويات | – | RegistryAPI | config | service.health_alert | لا | P0 |
| audit | F | سجل append-only / لا يعدّل بيانات المجال | platform | AuditSink | config | (يستقبل) | لا | P0 |
| monitoring | F | مقاييس/صحة / لا business | – | MetricsAPI | config, service-registry | – | جزئي | P0 |
| security-policy | F | سياسات أمن/بوابات / لا إنفاذ صلاحيات مباشر | platform | PolicyAPI | config, audit | security.* | لا | P1 |
| identity | 1 | مستخدمون/مصادقة/IdP-adapter / لا org logic | platform | IdentityAPI | config, audit | login/logout/failed_login/user_disabled | جزئي | P1 |
| organization | 1 | قطاعات/إدارات/عضوية / لا أدوار | platform | OrgAPI | identity, config, audit | org.* | جزئي | P1 |
| permissions | 1 | إنفاذ RBAC/ABAC/ReBAC/تصنيف / لا يعرّف سياسات الأمن الخام | platform | PermissionAPI (Gate) | identity, organization, security-policy, config, audit, feature-flags | role_assigned/removed, permission_denied | لا | P1 |
| admin | 1 | تجميع عمليات الأدمن (API/UI) / **لا يملك بيانات مجال** | – | AdminAPI (يفوّض) | modules عبر واجهاتها | – | لا | P1 |
| screens | 2 | تعريفات الشاشات / لا بيانات السجلات | platform | ScreenMetaAPI | permissions, config, audit, feature-flags | screen.created | جزئي | P1 |
| fields | 2 | تعريفات الحقول / لا القيم | platform | FieldMetaAPI | screens, permissions, audit | field.added | جزئي | P1 |
| migrations | 2 | آلية الترحيل المحكوم / لا DDL من نموذج | platform | MigrationAPI | config, audit | migration.generated/approved/rejected/applied | لا | P1 |
| database-generation | 2 | توليد schema من الميتاداتا عبر migrations | platform/apps | GenAPI | screens, fields, migrations, permissions, audit, config | (يستخدم migration events) | جزئي | P1 |
| records | 2 | CRUD الكيانات المولّدة + RLS/FLS / لا تعريف الشاشات | apps (schema-per-app) | RecordAPI | screens, fields, permissions, audit, config | record.* | جزئي | P1 |
| workflows | 2 | دورة حياة الـ workflows / لا اعتماد نهائي | platform | WorkflowAPI | records, screens, permissions, audit, config, feature-flags | workflow.created/activated | جزئي | P2 |
| approvals | 2 | بوابات الاعتماد + SoD / لا منطق الـ workflow | platform | ApprovalAPI | workflows, permissions, audit, notifications | workflow.approved/rejected | جزئي | P2 |
| tasks | 2 | مهام/قوالب / لا workflows | platform | TaskAPI | permissions, audit, config, (llm-gateway) | task.* | جزئي | P2 |
| projects | 2 | تجميع محادثات/ملفات / لا ملكية الملفات | platform | ProjectAPI | permissions, files, audit | project.* | جزئي | P2 |
| notifications | 2 | إشعارات + قنوات / لا محتوى المجال | platform | NotifyAPI | permissions, audit, config | (يرسل) | جزئي | P2 |
| files | 2/3 | إدارة الملفات/الوصول للتخزين / لا معالجة الوسائط | apps + Obj | FileAPI | permissions, audit, config | file.uploaded | نعم | P3 |
| okf | 3 | كتالوج معرفة/قاموس/مسرد / **ليس مصدر حقيقة** | platform + bundles | KnowledgeAPI | config, audit | – | نعم | P3 |
| model-registry | 3 | كتالوج النماذج + خريطة capability→model / لا تشغيل | platform | ModelRegAPI | config, audit | model.changed | جزئي | P3 |
| provider-registry | 3 | المزوّدون/endpoints / لا اختيار النموذج | platform | ProviderRegAPI | config, audit | provider.changed | جزئي | P3 |
| llm-gateway | 3 | توجيه/تنفيذ الاستدعاء (OpenAI-compatible) / **البوابة الوحيدة للـ LLM** | – | GatewayAPI | model-registry, provider-registry, config, audit | – | نعم | P3 |
| search | 3 | فهرسة/بحث نصي/هجين (OpenSearch/Qdrant) / لا embeddings policy | apps + infra | SearchAPI | config, permissions, audit | – | نعم | P3 |
| rag | 3 | استرجاع مصفّى بالصلاحية + provenance / لا توليد نهائي | apps + Vec | RagAPI | files, search, permissions, model-registry, llm-gateway, audit, okf | rag_query_executed | نعم | P3 |
| sql-agent | 3 | SQL قراءة فقط ضمن allow-list/RLS / لا DDL/DML | apps (read) | SqlAgentAPI | permissions, audit, config, llm-gateway | sql_query_generated/executed | نعم | P3 |
| media | 3 | pipeline الوسائط (OCR/vision/audio/video) / لا تخزين خام | Obj + apps | MediaAPI | files, model-registry, llm-gateway, audit, permissions, config | media_processed/ocr_completed | نعم | P3 |
| reports | 3 | تقارير قسماً قسماً + استشهاد / لا مصدر حقيقة | reporting | ReportAPI | records, rag, sql-agent, files, permissions, audit, llm-gateway | report.generated | جزئي | P4 |
| integrations | 4 | تسجيل/حوكمة الموصلات / لا تنفيذ منطق النظام الخارجي | integration | IntegrationAPI | permissions, config, audit, feature-flags | connector.added/disabled | نعم | P4 |
| mcp-connectors | 4 | جسر MCP للأدوات / لا صلاحيات خاصة | integration | McpAPI | integrations, permissions, audit, config | – | نعم | P4 |
| app-store | 4 | متجر المستخدم + ربط الحسابات / لا تسجيل فني | integration | StoreAPI | integrations, permissions, audit, feature-flags | app.connected/disconnected | نعم | P4 |
| license-about | F | عرض التراخيص/attribution / لا منطق | platform | AboutAPI | config | – | لا | P0 |
| backup-restore | Ops | نسخ/استعادة (Ops) / لا وصول مجال مباشر | Obj + DB | BackupAPI | config, audit | backup.created/restore.executed | نعم | P5 |

---

## 8. Module Dependency Matrix

**قاعدة الاتجاه (Cycle Prevention):** الاعتماد يتجه للأسفل عبر الطبقات فقط (4→3→2→1→F)؛ **ممنوع الاعتماد الصاعد**، وممنوع أن تعتمد الطبقة العابرة (F) على modules المجال. الأمثلة التي اقترحتها متوافقة مع هذا النموذج (identity لا يعتمد على screens؛ permissions يعتمد على identity+organization؛ records يعتمد على screens+permissions+audit؛ rag يعتمد على files+search+permissions+model-registry؛ media يعتمد على files+model-registry+llm-gateway+audit؛ integrations يعتمد على permissions+config+audit؛ audit/config عابرة/أساسية).

**Allowed dependencies:** كما في عمود «Deps مسموحة» أعلاه (المصدر الرسمي).

**Forbidden dependencies (عامة):**
- أي اعتماد **صاعد** بين الطبقات، أو أي **دورة** (A→B→A).
- **وصول مباشر لجداول/schema module آخر** — فقط عبر واجهته الداخلية.
- **استدعاء LLM خارج llm-gateway**.
- **تجاوز permissions أو audit**.
- اعتماد **config/feature-flags/service-registry/audit/monitoring** على أي module مجال.
- اعتماد **okf** كمصدر حقيقة، أو اعتماد أي module عليه كبديل عن القاعدة/الصلاحيات.

**قواعد الاستدعاء الداخلي:** كل نداء بين modules عبر **interface/contract** معرّف في `backend/shared` (لا استيراد داخلي عابر للحدود)؛ الأحداث عبر **in-process event bus** قابل للترقية لاحقاً؛ الوصول للبيانات عبر **repository/service layer** للـ module المالك فقط.

**Circular dependency prevention:** فحص آلي (import-linter/boundary checks) في CI يرفض أي اعتماد صاعد أو دوري؛ أي حاجة لكسر القاعدة تتطلب **ADR** أولاً.

---

## 9. Coding Rules for AI Agents

- لا كود خارج **scope** المهمة، ولا تعديل ملفات خارج قائمة المهمة.
- لا تغيير معمارية دون **تحديث/إضافة ADR**.
- لا إضافة **dependency** دون **License Review** معتمد.
- **لا external API** في runtime · **لا hardcoded secrets** · **لا hardcoded localhost/endpoints** · **لا hardcoded model names**.
- **لا direct DB access** خارج repository/service للـ module المالك · **لا direct LLM call** خارج llm-gateway.
- **لا bypass** للـ Permission Service ولا Audit Service · **لا DDL مباشر من LLM** · migrations فقط عبر workflow الترحيل مع review.
- كل feature ⇒ **tests**؛ كل permission ⇒ **deny test**؛ كل audit event ⇒ **test**؛ كل config ⇒ **default + validation**.
- كل module يحترم **boundaries**؛ كل خطأ **واضح وقابل للتتبع** (typed errors + معرّف تتبع).
- لا يكتب الوكيل كوداً إذا كانت المتطلبات **غير واضحة** → يسأل أولاً.

---

## 10. Testing Strategy

| النوع | الهدف | أين | مثال قبول | المرحلة |
|---|---|---|---|---|
| unit | صحة المنطق داخل module | داخل كل module | دالة صلاحية تُرجع deny افتراضاً | P0+ |
| integration | تفاعل modules عبر واجهاتها | tests/integration | screen→migration→apply يعمل مع audit | P1+ |
| e2e | مسار مستخدم كامل | tests/e2e | دخول→إنشاء شاشة→CRUD عبر UI | P1+ |
| permission | إنفاذ الصلاحية | tests/permission | كل endpoint له **deny test** + RLS/FLS | P1+ |
| audit | تسجيل الأحداث | tests | كل event ينشأ بحقوله اللازمة | P1+ |
| migration | سلامة الترحيل/التراجع | tests/migration | apply ثم rollback بلا فقد | P1+ |
| rag | استرجاع مصفّى + provenance | tests | لا تسريب مقاطع خارج الصلاحية | P3+ |
| sql-agent safety | SQL آمن | tests/security | رفض DDL/DML وخارج allow-list | P3+ |
| media pipeline | معالجة الوسائط | tests | PDF/صوت→فهرسة + audit | P3+ |
| configuration profile | صحة البروفايلات | tests | تبديل profile يغيّر السلوك بالإعداد | P0+ |
| feature flag | تفعيل/تعطيل قدرة | tests | تعطيل قدرة يخفيها دون كسر خدمة | P0+ |
| connector | سلامة التكامل | tests | استدعاء ضمن الصلاحية + بوابة | P4+ |
| offline deployment | لا اتصال خارجي | tests/offline | **no-external-call test** ينجح | P0+ |
| backup/restore | تعافٍ | tests | نسخ ثم استعادة متحقَّقة | P5 |
| smoke / health | إقلاع/صحة | CI | /health أخضر لكل التبعيات | P0+ |

---

## 11. Quality Gates (قبل أي merge/قبول feature)

- الاختبارات تمرّ (unit/integration/permission/audit ذات الصلة).
- **permission checks** موجودة (+ deny tests) · **audit events** مُنفَّذة.
- **لا hardcoded secrets** · **لا external network calls**.
- **migrations reviewed** ومعتمدة · **License Review** تمّت لأي dependency جديد.
- **documentation محدّثة** · **handoff محدّث**.
- **config defaults valid** (+ validation) · **rollback** مأخوذ بالاعتبار.
- UI: **RTL/accessibility** روعيت · **error handling** مُضمَّن.
- **boundaries** غير مكسورة (فحص الاعتماديات في CI أخضر).

---

## 12. Documentation Strategy

| الملف | الوظيفة | متى يُحدَّث |
|---|---|---|
| vision.md | الرؤية والحدود | بداية + تغيّر جوهري |
| spec.md | المتطلبات والقيود | تغيّر المتطلبات |
| architecture.md | المعمارية العامة | قرار معماري |
| data / permission / agent / orchestration / media / integration / deployment -architecture.md | معماريات فرعية | عند تغيّر المجال المعني |
| configuration.md | مفاتيح/أعلام/namespaces | مستمر |
| feature-catalog.md · service-catalog.md | مرجع الميزات/الوحدات | إضافة/تعديل |
| coding-standards.md | معايير + قواعد الوكلاء | مستمر |
| testing-strategy.md | أنواع الاختبار | مستمر |
| license-review.md | مراجعة التراخيص | قبل أي dependency/image |
| adr/ | القرارات المعمارية | لكل قرار |
| handoff.md | التسليم الحالي | بعد كل جلسة |
| runbooks/ · troubleshooting.md · backup-restore.md · offline-install.md | التشغيل | عند نضج التشغيل |

**قاعدة:** التوثيق **جزء من تعريف الإنجاز (Definition of Done)** — لا feature مكتمل بلا تحديث المستند/المستندات المعنية + handoff.

---

## 13. ADR Strategy

مجلد `specs/adr/`. **صيغة كل ADR:** العنوان · السياق · القرار · البدائل · السبب · المخاطر · الأثر · التاريخ · الحالة (Proposed / Accepted / Superseded). **قاعدة:** أي قرار معماري مهم أو أي كسر لقاعدة boundaries يتطلب ADR **قبل** التنفيذ.

**ADRs مبدئية مقترحة (كلها Proposed حتى تعتمدها):**
| # | العنوان | الحالة |
|---|---|---|
| ADR-0001 | Modular Monolith أولاً (microservice-ready) | Proposed |
| ADR-0002 | PostgreSQL كمصدر حقيقة علائقي | Proposed |
| ADR-0003 | Qdrant للـ vector search (في Local Demo) | Proposed |
| ADR-0004 | OpenSearch للبحث النصي/الهجين (في Local Demo) | Proposed |
| ADR-0005 | OKF كطبقة معرفة لا مصدر حقيقة | Proposed |
| ADR-0006 | Enterprise UI بدل Open WebUI كوجه | Proposed |
| ADR-0007 | Local Auth أولاً مع IdP-adapter | Proposed |
| ADR-0008 | Configuration-driven deployment (config-only للإنتاج) | Proposed |
| ADR-0009 | ربط النماذج بالـ capabilities (Capability-to-Model) | Proposed |
| ADR-0010 | Feature Flags + Config Registry أساسية | Proposed |
| ADR-0011 | فصل Admin / Super Admin / Operations (Three Control Planes) | Proposed |
| ADR-0012 | تجريد cache/queue (Redis/Valkey عبر config) | Proposed |
| ADR-0013 | تجريد object storage (MinIO/بديل S3-compatible) | Proposed |
| ADR-0014 | Observability قابلة للتبديل (Grafana/Loki/بدائل) | Proposed |
| ADR-0015 | LLM Gateway على عقد OpenAI-compatible | Proposed |

---

## 14. Handoff Strategy

العمل عبر **عدة محادثات ووكلاء**، لذا `handoff.md` **إلزامي** ويُحدَّث بعد كل جلسة/مرحلة. **محتواه:** التاريخ · المرحلة · الهدف · ما أُنجز · ما لم يُنجز · الملفات المعدّلة · القرارات · المشاكل · المخاطر · الاختبارات (ناجح/فاشل) · الخطوة التالية · **تحذيرات للوكيل التالي** · روابط specs ذات الصلة · **ما الذي يجب عدم لمسه**. أرشفة النسخ في `specs/handoffs/` بتاريخها. **قاعدة:** لا تُختتم أي مهمة دون تحديث handoff + قائمة اختبارات + تقرير مختصر.

---

## 15. License Review Workflow

**مبدأ إلزامي:** *لا يدخل أي dependency أو repository أو container image إلى المنتج إلا بعد License Review.* التراخيص **Open Decisions** ولا تُعتمد نهائياً إلا بعد مراجعة **الإصدار المحدد** والصورة/الحزمة التي ستُستخدم فعلاً.

**سير العمل:** اقتراح أداة → تعبئة صف في `specs/license-review.md` → مراجعة (تقنية + قانونية عند اللزوم) → قرار (Approved / Conditional / Rejected / Needs Legal Review) → عند Approved/Conditional فقط تُدخَل الأداة (مع attribution إن لزم). أي ترقية إصدار تعيد المراجعة.

**قالب `license-review.md`:**
| الأداة | الإصدار | الرابط الرسمي | نوع الترخيص | تعديل؟ | إعادة توزيع؟ | white-label؟ | استخدام مؤسسي؟ | شبكة مغلقة؟ | AGPL/SSPL/RSAL/قيود؟ | dependency فقط أم تعديل؟ | attribution؟ | القرار |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| PostgreSQL | (حدِّد) | postgresql.org | PostgreSQL | – | – | – | – | – | لا | dependency | لا | Needs Review |
| Qdrant | (حدِّد) | qdrant.tech | Apache-2 | – | – | – | – | – | لا | dependency | – | Needs Review |
| OpenSearch | (حدِّد) | opensearch.org | Apache-2 | – | – | – | – | – | لا | dependency | – | Needs Review |
| Redis / Valkey ⚠️ | (حدِّد) | redis.io / valkey.io | متغيّر / BSD | – | – | – | – | – | نعم (Redis) | dependency | – | Needs Legal Review |
| MinIO ⚠️ | (حدِّد) | min.io | AGPL v3 | – | – | – | – | – | AGPL | dependency | نعم | Needs Legal Review |
| Grafana / Loki ⚠️ | (حدِّد) | grafana.com | AGPL v3 | – | – | – | – | – | AGPL | dependency | – | Needs Legal Review |
| PyMuPDF ⚠️ | (حدِّد) | pymupdf.io | AGPL/تجاري | – | – | – | – | – | AGPL | dependency | – | Needs Legal Review |
| Ollama / vLLM | (حدِّد) | ollama.com / docs.vllm.ai | MIT / Apache-2 | – | – | – | – | – | لا | dependency | – | Needs Review |
| Next.js/React/Tailwind/shadcn/ui | (حدِّد) | – | MIT | نعم | نعم | نعم | نعم | نعم | لا | dependency (shadcn: copy-in) | – | Needs Review |
| OCR (Tesseract/PaddleOCR/docTR) | (حدِّد) | – | Apache-2 | – | – | – | – | – | لا | dependency | – | Needs Review |
| Whisper / faster-whisper · ffmpeg ⚠️ | (حدِّد) | – | MIT · LGPL/GPL | – | – | – | – | – | ffmpeg: LGPL/GPL | dependency | – | Needs Review |

> **يمكنني التحقق من التراخيص الحالية لكل إصدار عبر البحث عند طلبك** لتحويلها من Needs Review إلى قرار.

---

## 16. Configuration-driven Development Rules

- **هرمية الإعداد:** defaults (في الكود، آمنة) → environment profile → capability bundle → runtime overrides (Config Registry) → secrets.
- **لا hardcoded:** لا secrets، لا localhost/endpoints، لا model names، لا paths، لا resource values — كلها من الإعداد.
- **namespace لكل module** في الإعداد؛ لا يقرأ module إعداد module آخر.
- **كل مفتاح:** له **default + validation** و**fail-fast** عند الإقلاع إن كان حرجاً وناقصاً.
- **static vs dynamic:** static (يُقرأ عند الإقلاع، تغييره يحتاج restart) مقابل dynamic (Registry، يتغيّر live). وثّق نوع كل مفتاح.
- **feature flags** بنطاقات (global/module/capability/role/env) وأعلام محميّة.
- **secrets** عبر آلية أسرار (env/secret store)، لا في المستودع، تُدار في طبقة العمليات.
- **abstractions قابلة للتبديل بالإعداد:** cache/queue (Redis|Valkey)، object storage (MinIO|بديل)، observability (Grafana/Loki|بدائل)، LLM provider (Ollama|vLLM)، identity provider، db-router. **Qdrant وOpenSearch افتراضيان حاضران** (pgvector/PG-FTS فقط كـ low-resource bundle صريح، لا افتراضياً).

---

## 17. Deployment Portability Rules

- **صورة واحدة لكل خدمة تُبنى مرة**، تعمل في كل البيئات؛ **ممنوع** كود أو فرع خاص ببيئة، وممنوع production fork.
- الفرق بين البيئات **configuration فقط**: env vars · config files · resource limits · model/provider endpoints · storage/database paths · secrets · TLS · workers · backup paths · monitoring settings · deployment profile.
- **backend عديم الحالة** (جلسات في Redis/Valkey أو JWT) → توسّع أفقي؛ **workers** تتوسّع مستقلة؛ **inference** على عُقد GPU منفصلة يُشار إليها بالإعداد.
- **نفس migrations** في كل البيئات.
- **Environment Profiles** (Local/Demo/Staging/Production) × **Capability Bundles** (composable) — كلها config.
- **offline bundle** (images + wheels + models) + استعادة + تحقق.
- **الترقية Local→Production = تغيير إعداد فقط** (اختبار `configuration profile` + `offline` يضمنه).

---

## 18. How to Use This Methodology with Any Coding Agent

**لكل مهمة (task) في محادثة مستقلة:**
1. الوكيل يقرأ: `constitution.md` + الـ specs ذات الصلة + `handoff.md` + بطاقة المهمة (scope + ملفات مسموح لمسها + acceptance + tests).
2. يؤكد فهم الـ scope؛ **إن كانت المتطلبات غير واضحة → يسأل ولا يكتب كوداً**.
3. يُخرج **patch محدوداً** ضمن الملفات المسموحة فقط؛ لا يلمس ADRs أو ملفات خارج القائمة.
4. يكتب/يشغّل الاختبارات المطلوبة (permission deny + audit + unit ذات الصلة).
5. يمرّ عبر **Quality Gates** + **License Review** إن أضاف dependency.
6. يحدّث **handoff.md** + يكتب **تقريراً مختصراً** (أُنجز/لم يُنجز/الملفات/المخاطر/التالي).

**قواعد تقليل التشتت (14):** محادثة = task واحد · scope واضح · ملفات محددة للقراءة/التعديل · patch محدود · لا تعديل خارج القائمة · لا تغيير ADR دون طلب · إنهاء بـ handoff + اختبارات + تقرير · لا كتابة عند غموض.

**محايد للأداة:** نفس البطاقات/الـ specs تعمل مع Claude Code/Codex/Cursor/Windsurf/Cline/Aider/OpenHands/Continue؛ و**Coding Model** (Qwen/DeepSeek/GLM Coder…) منفصل عن الأداة.

---

## 19. Open Decisions

1. **التراخيص (تبقى مفتوحة):** حسم Redis/Valkey، MinIO/بديل، Grafana-Loki/بدائل، PyMuPDF/بديل، ffmpeg — عبر License Review للإصدار/الصورة المحددة. (أستطيع التحقق بالبحث.)
2. **مزوّد cache/queue** الافتراضي (Redis أم Valkey) — مع بقاء الطبقة مجرّدة.
3. **مزوّد object storage** (MinIO أم بديل S3-compatible مثل SeaweedFS).
4. **stack المراقبة** ومستواه في Local Demo (أساسي أم كامل).
5. **محرك OCR العربي** (PaddleOCR/docTR/Tesseract).
6. **نطاق Graph** (تأجيل أم Apache AGE) — Neo4j يبقى optional off.
7. **النماذج الفعلية لكل capability** وسياسة تشغيل الثقيل حسب العتاد.
8. **تأكيد Modular Monolith + Spec-driven** رسمياً (ADR-0001).
9. النواقص السابقة (العدد المتزامن/عتاد الإنتاج/الأحجام/جرد الأنظمة/الـ IdP/مصفوفات الاعتماد وSoD) — تُحسم كإعدادات/قياسات.

---

## 20. Final Recommendation

اعتمد **Spec-driven Development** + **Modular Monolith حقيقي (microservice-ready)** كمنهجية بناء رسمية. الخطوات التمهيدية (بلا كود): (١) تثبيت `constitution.md` بالمبادئ غير القابلة للتفاوض؛ (٢) إنشاء هيكل `specs/` وملفاتها + `specs/adr/` بالـ ADRs الخمسة عشر (Proposed)؛ (٣) إنشاء `specs/license-review.md` وإبقاء البنود الحسّاسة **Needs Legal Review**؛ (٤) تثبيت **Module Catalog + Dependency Matrix** وقاعدة الاتجاه (فحص boundaries في CI لاحقاً)؛ (٥) تثبيت **Testing Strategy + Quality Gates + Handoff template**؛ (٦) تثبيت **قواعد الإعداد والنقل** وطبقات التجريد القابلة للتبديل (cache/queue، object storage، observability، LLM provider) مع **إبقاء Qdrant/OpenSearch حاضرين في Local Demo**.

بعد اعتماد هذه المنهجية وحسم Open Decisions الحرجة (خاصة ADR-0001 وبنود التراخيص)، ننتقل لاحقاً — في محادثة مستقلة — إلى تصميم **المرحلة الأولى وحدها** (Vision→Specify→Clarify→Plan→Tasks لها)، دون أي كود في هذه المرحلة.
