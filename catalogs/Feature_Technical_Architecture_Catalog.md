# Feature &amp; Technical Architecture Catalog
## منصة تشغيل معرفي مؤسسي تعمل في شبكة مغلقة — الكتالوج التقني والوظيفي المرجعي

> **Document Title:** Feature &amp; Technical Architecture Catalog
> **Version:** 2.1 — Final (A1–A11 + قرارات ما قبل التنفيذ D1–D9 مدمجة)
> **Status:** Current / Accepted
> **Date:** 2026-07-04
> **Supersedes:** v1.0 من هذه الوثيقة + الأقسام المقابلة في «الدراسة المعمارية الكاملة» و«system-design-v1.md» (تاريخية) + أي مخطط يُظهر Open WebUI كسطح رئيسي (Superseded)
> **Related Documents:** constitution.md · Spec_Driven_Modular_Monolith_Methodology.md · open-decisions.md · phase-roadmap.md · phase-0-foundation-full-stack-skeleton.md
> **Authority Order (عند التعارض):** 1) constitution.md → 2) Methodology → 3) هذا الكتالوج → 4) تصنيف القرارات المفتوحة → 5) phase-roadmap.md → 6) تصاميم المراحل المعتمدة → 7) superseded/ (تاريخية). أي وثيقة/برومبت قديم يخالف هذا الترتيب يُعد Superseded.
> **Intended Audience:** مالك المشروع (SA) · AI Coding Agents · المراجعون التقنيون/القانونيون
> **Last Reviewed By:** Final Architecture &amp; Methodology Consistency Review (2026-07-02) — اعتُمد من SA
> **Purpose:** المرجع الرسمي للميزات والخدمات والشاشات والتقنيات وسيناريوهات التدفق وأحداث التدقيق، قبل أي تصميم مرحلة أو تنفيذ.

**رموز:** DB=PostgreSQL · Vec=Qdrant · Srch=OpenSearch · Obj=Object Storage (MinIO|بديل — Needs License Review) · Cache=Cache/Queue (Redis|Valkey — Needs License Review) · LLM=نموذج · RAG=استرجاع · MCP=تكامل. الحالة: Core · Opt · 🔒=محميّة. الأدوار: U=User · A=Admin · SA=Super Admin · Ops=Operations.
**قاعدة قراءة (A9):** أي ورود حرفي لـ «Redis» أو «MinIO» في هذه الوثيقة أو الوثائق التاريخية يُقرأ: «مزوّد cache/queue أو object-storage **المجرّد** رهن License Review».

---

## 1. Executive Summary

النظام **Enterprise AI / Local RAG / Local LM Platform** يعمل داخل **شبكة مغلقة**، **ليس chatbot** وليس RAG بسيطاً وليس Open WebUI. الـ **LLM ليس مصدر الحقيقة** (دوره تحليل/تلخيص/تفسير/تنفيذ مهام/طلب توضيح)؛ **مصادر الحقيقة**: قواعد البيانات الرسمية + المستندات المعتمدة + الـ APIs الداخلية + السجلات الرسمية + الأنظمة المرتبطة رسمياً. **الواجهة النهائية Enterprise UI خاصة** (Arabic/English، RTL كامل، white-label) — **Open WebUI ليس الواجهة النهائية** وأي وثيقة/مخطط قديم يُظهره كسطح رئيسي **Superseded**. النظام **metadata-driven** ويُبنى مرة واحدة كمنتج **قابل للنقل من MSI Titan إلى الإنتاج بتغيير configuration فقط دون تعديل كود**.

**الأسلوب المعتمد (ADR-0001: Accepted):** **Modular Monolith أولاً** — backend واحد قابل للنشر بحدود modules واضحة ومفروضة، مع workers غير متزامنة وحاويات بنية منفصلة، وقابلية فصل modules إلى microservices لاحقاً. **كل الطبقات والخدمات حاضرة من البداية** بحالات (enabled/disabled/lightweight/demo/production/optional/protected)، و**دعم Media/Video/Multimodal جاهز معمارياً من البداية** عبر configuration وModel/Provider Registry (المؤجَّل فقط تشغيل النماذج الثقيلة حسب العتاد). العمل بمنهجية **Spec-driven Development متوافقة مع GitHub Spec Kit / Spacekit**: Vision → Specify → Clarify → Plan → Tasks → (Implement لاحقاً فقط).

---

## 2. Confirmed Decisions

منصة لا chatbot · **LLM ليس Source of Truth** ومصادر الحقيقة هي القواعد الرسمية/المستندات المعتمدة/APIs الداخلية/السجلات الرسمية · Enterprise UI خاصة (لا Open WebUI كوجه؛ ما خالف ذلك Superseded) · Arabic/English + RTL كامل · 20,000–30,000 مستخدم مسجل/مؤسسة · Local Demo على MSI Titan ثم **production عبر configuration فقط** (لا تعديل كود، لا fork) · **Modular Monolith أولاً** (ADR-0001 Accepted) بحدود مفروضة وقابلية فصل لاحقة · نموذج قواعد `database.docx`: platform/apps/integration/reporting + Qdrant/OpenSearch/Obj/Cache + Neo4j اختياري · **Qdrant وOpenSearch حاضران في Local Demo** (pgvector/PG-FTS **fallback ضمن low-resource bundle صريح فقط**) · ثلاث درجات فصل (Logical/Schema/Physical) · التوليد محكوم بالاعتماد (لا DDL من نموذج؛ migrations + review + approval + versioning + audit + شاشة توثيق) · معرّفات تقنية ASCII والعربية labels · صلاحيات RBAC+ABAC+ReBAC + تصنيف خماسي + field/row/screen/action + Need-to-know + SoD + Least Privilege **قبل أي استرجاع** وdefault-deny · **كل تغيير مهم يُسجَّل في Audit Log** · النماذج مربوطة بـ **capabilities** لا أسماء ثابتة (Model/Provider Registry، تغيير من الأدمن دون كود) · OKF طبقة معرفة محلية **ليست مصدر حقيقة** · Local Auth مع IdP-adapter · **لا dependency/صورة/موديل بلا License Review** (Redis/Valkey · MinIO · Grafana/Loki · PyMuPDF · ffmpeg وأمثالها = **Needs License Review** حتى حسم ترخيص الإصدار المستخدم) · فصل **Admin / Super Admin / Operations**: الأدمن يدير features/modules (capabilities)، أما تشغيل/إيقاف services/containers الأساسية فـ **Operations فقط** · **قاعدة الشبكة المغلقة:** أي tool أو model أو connector **لا يعمل خارج الشبكة المغلقة** إلا إذا نُصّ عليه ووفق عليه صراحةً · **lockfiles + digest pinning** قاعدة أساسية لإعادة البناء مغلقاً · **DB users بأدنى صلاحية لكل قاعدة من التهيئة الأولى** · تمييز مصطلح «service» إلزامي (module / worker / infra container / connector / provider / datastore — جدول المصطلحات في المنهجية §المقدمة).

**قرارات ما قبل التنفيذ (D1–D9 — معتمدة 2026-07-04):** **D1 Frontend = React + Vite + TypeScript + Tailwind + shadcn/ui-style** (SPA مستقلة تستهلك OpenAPI/SDK فقط؛ **لا Next.js** — لا حاجة SSR/SEO داخلياً؛ SvelteKit دُرس ورُفض) · **D2 Backend مؤكَّد** = Python + FastAPI + Pydantic + SQLAlchemy + Alembic + PostgreSQL (+workers منفصلة) · **D3 C5 محسوم** = uv + pnpm + lockfiles + pinned versions + reproducible builds + offline caches لاحقاً + install/verify scripts · **D4 Cache/Queue/Lock** = ثلاث واجهات (CacheProvider / QueueProvider / LockProvider) بافتراضي **memory/PostgreSQL**؛ **Valkey optional-ready** لاحقاً (مفضَّل على Redis ترخيصياً، رهن License Review) — ليس إلزامياً في Phase 0/1 · **D5 ObjectStorageProvider** بافتراضي **local filesystem** في dev/demo؛ MinIO/SeaweedFS/S3-compatible يُحسم في مرحلة الملفات/الوسائط (تخزين فقط — ليس OCR/استخراجاً) · **D6 Observability Baseline** = Audit في PostgreSQL (append-only، permission-aware) + **JSON app logs خارج قاعدة البيانات** + Admin Log Viewer + Health endpoints (/health، /health/db، /health/qdrant، /health/opensearch، /health/llm) + Error Code Catalog + request/correlation IDs + **/metrics اختياري** — لا Grafana/Loki/Graylog الآن؛ OpenTelemetry adapter مستقبلاً فقط · **D7 GitHub الآن** للتطوير + نموذج نقل مغلق (repo/git-bundle + Docker images + model files + package caches + install/verify scripts + docs/handoff)؛ Git داخلي (Gitea/GitLab) خيار مستقبلي فقط · **D8 Reference-aware clean implementation** — قراءة كود OSS للتعلم مسموحة؛ النسخ المباشر محكوم بـ License Gate (النص الملزم في coding-standards) · **D9 حدود Admin UI مؤكدة:** capabilities/models/providers/flags/workflows/connectors/الصلاحيات من الواجهة؛ endpoints/secrets/keys/replicas/GPU/profiles تبقى config/Ops — وكل تغيير حساس مدقَّق وقد يتطلب approval حسب السياسة.

---

## 3. Technology Evaluation Table

> تقييم كاقتراحات لا قرارات نهائية. **كل بند يمرّ بـ License Review للإصدار/الصورة المحددة قبل دخوله التنفيذ** (البنود الحساسة ⚠️ = Needs License Review / Needs Legal Review).

### 3.1 قواعد البيانات والتخزين
| التقنية | الدور | Offline / الترخيص | الملاءمة (dev / scale / portable) | الحالة · الآن/لاحقاً | التوصية / البديل |
|---|---|---|---|---|---|
| PostgreSQL | مصدر الحقيقة العلائقي | نعم · PostgreSQL | ممتاز/ممتاز/نعم | Core · الآن | **اعتماد**. مستخدم DB بأدنى صلاحية **لكل قاعدة** من التهيئة الأولى. |
| Qdrant | vector search | نعم · Apache-2 | جيد/ممتاز/نعم | **Core · حاضر في Local Demo** بإعدادات خفيفة | **اعتماد**؛ لا يُستبدل افتراضياً في dev. |
| pgvector | متجهات داخل Postgres | نعم · PostgreSQL | ممتاز/محدود/نعم | Opt | **fallback ضمن low-resource bundle الصريح فقط** — ليس بديلاً افتراضياً يحذف Qdrant. |
| OpenSearch | بحث نصي/هجين + logs | نعم · Apache-2 | ثقيل RAM (يُضبط demo heap)/ممتاز/نعم | **Core · حاضر في Local Demo** بإعدادات خفيفة | **اعتماد**؛ PG-FTS **fallback ضمن low-resource bundle فقط**. تجنّب Elasticsearch (SSPL). |
| Redis / Valkey ⚠️ | cache/queue/sessions/locks (scale) | نعم · Redis متغيّر (RSAL/SSPL) / Valkey BSD | ممتاز/ممتاز/نعم | **Optional-ready · ليس إلزامياً في P0/P1 (D4)** | ثلاث واجهات (Cache/Queue/Lock) بافتراضي **memory/PostgreSQL**؛ Valkey مفضَّل على Redis عند الحاجة (scale/sessions/queues/locks)، رهن License Review — بوابة فئة 3 عند أول تفعيل للصورة. |
| MinIO ⚠️ / SeaweedFS | object storage (S3-compatible — تخزين فقط، ليس OCR/استخراجاً) | نعم · AGPL v3 / Apache-2 | ممتاز/ممتاز/نعم | **Deferred-provider · يُحسم بمرحلة الملفات (D5)** | **ObjectStorageProvider بافتراضي local filesystem** في dev/demo؛ حسم المزوّد قبل تفعيل صورته (فئة 3) — MinIO رهن Legal Review (AGPL؛ بلا توزيع نسخ معدّلة — فئة 4)، SeaweedFS بديل Apache-2. |
| Neo4j ⚠️ | graph | نعم · Community=GPLv3 | جيد/محدود/نعم | Opt (off) · لاحقاً | إن لزم Graph: **فضّل Apache AGE** (Apache-2). |
| SQLite | embedded/tests | نعم · Public Domain | ممتاز/—/نعم | Opt | محلي/اختبار فقط، ليس مصدراً رئيسياً. |
| Alembic | migration tooling | نعم · MIT | ممتاز/ممتاز/نعم | Core · الآن | **اعتماد** داخل غلاف الحوكمة (review/approval/versioning). |

### 3.2 المعرفة والـ metadata
| التقنية | الدور | التوصية |
|---|---|---|
| OKF | Knowledge Catalog / Data Dictionary / Glossary / agent-instructions | **اعتماد بدور محدود** من البداية؛ توليد الحزم بأدوات **محلية** (لا BigQuery/Gemini)؛ **ليس مصدر حقيقة** ولا بديلاً عن DB/الصلاحيات/Audit/RAG. |
| YAML/Markdown metadata | تعريفات مقروءة للوكلاء والبشر | اعتماد لصيغ OKF والتعريفات. |
| Screen/Field/Entity/Model/Permission/Workflow metadata | جوهر metadata-driven | تُخزَّن في `platform_db` (المصدر الرسمي) وتُصدَّر إلى OKF كتوثيق. |

### 3.3 واجهة المستخدم
| التقنية | الدور | الترخيص | التوصية |
|---|---|---|---|
| **React + Vite + TypeScript** | ستاك Enterprise UI — SPA مستقلة تستهلك OpenAPI/SDK | MIT | **معتمد نهائياً (D1)** — لا حاجة SSR/SEO داخل شبكة مغلقة؛ الأقوى لـ Screen/Workflow Builders (dnd-kit، xyflow، TanStack، react-hook-form) والأنسب للوكلاء. **Next.js غير معتمد** (تعقيد بلا مقابل)؛ SvelteKit دُرس ورُفض (ecosystem أصغر + قربه من OpenWebUI يرفع خطر النسخ). |
| Tailwind CSS + shadcn/ui | نظام تصميم copy-in | MIT | **اعتماد**؛ RTL عبر logical properties + `dir`. |
| Open WebUI ⚠️ | **مرجع UX فقط** | v0.6.6+ قيود branding/عدد مستخدمين | **ليس الواجهة النهائية**؛ v0.6.5 (BSD-3) للدراسة فقط بمراجعة قانونية؛ أي وثيقة قديمة تُظهره كسطح رئيسي = **Superseded**. |
| LibreChat / NextChat / LobeChat / FastGPT ⚠️ | مراجع أفكار | MIT/متفاوت | مراجع فقط؛ راجع ترخيص FastGPT. |

### 3.4 النماذج وLLM Gateway
| التقنية | الدور | الترخيص | التوصية |
|---|---|---|---|
| Ollama | تشغيل dev + تبديل نماذج | MIT | **اعتماد لـ dev/Local Demo**. |
| vLLM | inference إنتاجي | Apache-2 | **اعتماد للإنتاج**. |
| SGLang / llama.cpp | بدائل serving / CPU | Apache-2 / MIT | Opt حسب الحاجة/low-resource. |
| **OpenAI-compatible endpoint** | **العقد الموحّد للـ Gateway** | — | **الثابت هو العقد** (ADR-0015)؛ المزوّد configurable. **لا استدعاء LLM خارج الـ Gateway.** |
| Model/Provider Registry | capability→model mapping + per-agent overrides | — | **اعتماد**؛ تغيير النموذج من الأدمن دون كود؛ hardware-aware selection + fallbacks. |

### 3.5 RAG والبحث
Hybrid RAG (Qdrant + OpenSearch + reranker) **اعتماد** · Embedding/Reranking عبر capabilities في الـ Registry · Chunking + metadata filtering + **permission-aware retrieval قبل الاسترجاع** + source citation إلزامي + document versioning + cache invalidation بالنسخ/الصلاحية · **مخرجات الوسائط (OCR/تفريغ/أوصاف) تدخل نفس فهرس RAG المحكوم بالصلاحية مع ربطها بالمصدر (RAG-over-media)**.

### 3.6 الوسائط
| التقنية | الدور | الترخيص | التوصية |
|---|---|---|---|
| Tesseract / PaddleOCR / docTR | OCR (عربي) | Apache-2 | **capability قابلة للتبديل من الأدمن**؛ اختيار المحرك = قرار configurable + مراجعة ترخيص قبل تنفيذ مرحلته؛ قياس جودة عربي ضمن الاختيار. |
| Apache Tika · pdfplumber/pypdf · python-docx/openpyxl | استخراج PDF/Office | Apache-2/MIT/BSD | اعتماد. |
| PyMuPDF ⚠️ | parsing PDF قوي | AGPL/تجاري | **Needs License Review**؛ البديل الافتراضي pdfplumber/pypdf. |
| faster-whisper | تفريغ صوتي | MIT | **اعتماد** (capability: audio transcription). |
| ffmpeg ⚠️ | استخراج صوت/keyframes | LGPL/GPL حسب البناء | **Needs License Review** لبناء الصورة المستخدم. |
| Vision / Video / Multimodal models ⚠️ | فهم صور/فيديو | حسب النموذج | عبر الـ Registry؛ **جاهزية معمارية كاملة من البداية**، التشغيل الثقيل بالإعداد حسب العتاد؛ **تراخيص الأوزان بوابة مزدوجة** (قبل تنفيذ Phase 5 + قبل التوزيع). |

### 3.7 التكاملات
MCP **اعتماد** كطبقة أدوات موحّدة · Internal APIs / Webhooks / DB connectors (الأساس **داخلي**) · Connector Registry + per-user / service-account authorization · Internal OIDC/OAuth عند توفره داخلياً · Integration logs + sync jobs (كل استدعاء مدقَّق) · External SaaS **اختياري لاحقاً عبر proxy/gateway فقط وبموافقة صريحة** (قاعدة الشبكة المغلقة).

### 3.8 التشغيل والمراقبة
Docker / Docker Compose (+profiles) **اعتماد** أساس النشر · **lockfiles + container digest pinning إلزامية** لإعادة البناء مغلقاً · Config files + env vars + health checks (Twelve-Factor) · **Observability Baseline (D6 — المعتمد للبداية):** Audit في PostgreSQL + **JSON app logs خارج قاعدة البيانات** (stdout/ملفات بدوّار) + Admin Log Viewer (permission-aware، بقناع أسرار) + Health endpoints (/health، /health/db، /health/qdrant، /health/opensearch، /health/llm) + Error Code Catalog + request/correlation IDs + **/metrics اختياري** · Prometheus-server/Grafana ⚠️/Loki ⚠️/Graylog **مؤجلة إلى P8** (Grafana/Loki: Needs Legal Review؛ بديل مقاييس: VictoriaMetrics) · OpenTelemetry **adapter مستقبلاً فقط** · Backup/Restore + **offline bundle** (images+wheels+models، موقّعة/متحقَّقة) · Kubernetes/OpenShift **لاحقاً فقط** — الانتقال إليها إضافة manifests **دون تعديل كود** (stateless + config-driven + healthchecks) · **نموذج التطوير والنقل (D7):** التطوير online على GitHub الآن؛ النقل إلى الشبكة المغلقة عبر حزمة موقّعة (repo/git-bundle + Docker images + model files + package caches uv/pnpm + install/verify scripts + docs/handoff)؛ Git داخلي (Gitea/GitLab) خيار مستقبلي فقط عند نشوء تطوير داخل الشبكة.

---

## 4. Feature Catalog

> أعمدة: الميزة · المستفيد · الظهور · C/O · تعطيل أدمن؟ · موافقة؟ · يحتاج · Phase · القبول (مختصر) · المخاطر (مختصر).

| الميزة | المستفيد | الظهور | C/O | تعطيل أدمن؟ | موافقة؟ | يحتاج | Phase | القبول | المخاطر |
|---|---|---|---|---|---|---|---|---|---|
| Chat | U | User Workspace | Core | نعم (capability) | لا | LLM,RAG,DB | 6 | إجابة مسنودة بمصدر + provenance (module: `chat`) | هلوسة → No-Guessing/Validation |
| User Workspace | U | Home | Core | لا | لا | DB | 1 | يعرض المسموح فقط | تسريب صلاحيات |
| Projects | U | Workspace | Core | نعم | لا | DB,Obj | 3 | تجميع محادثات/ملفات بالصلاحية | خلط نطاقات |
| Tasks | U/A | Workspace/Admin | Core | نعم | أحياناً | DB,LLM | 3 | قوالب/مهام تُنفَّذ بالصلاحية | تنفيذ غير مصرّح |
| Notifications (+دردشة/إشعار) | U | Workspace | Core | نعم | لا | DB | 3 | إشعار تفاعلي مدقَّق | إزعاج/تسريب |
| Screen Builder | A | Admin | Core | لا (أساسي) | ينتج migration يحتاج موافقة | DB | 1 | تعريف شاشة→ميتاداتا | تعريف خاطئ |
| Field Builder | A | Admin | Core | لا | لا | DB | 1/2 | أنواع/تحققات حقول | فقد سلامة |
| Records Engine | U/A | Screens | Core | لا | حسب workflow | DB | 1/2 | CRUD مع RLS/FLS | تجاوز صفوف/حقول |
| Database Generation Review | A | Admin | Core | لا | نعم | DB | 1/2 | فحص تعارض/مخاطر قبل الاعتماد | تطبيق ضار |
| Migration Approval | A/SA | Admin | Core | لا | نعم | DB | 1/2 | لا تطبيق بلا اعتماد | كسر توافق |
| Workflow Builder | A | Admin | Core | نعم | — | DB | 3 | بناء workflow مربوط | حلقات/تعارض |
| User-created Workflows (approval) | U | Workspace | Core | نعم | **نعم** | DB | 3 | لا تفعيل قبل اعتماد | تفعيل غير آمن |
| Admin-created Workflows | A | Admin | Core | نعم | — | DB | 3 | ربط مسبق يعمل | أثر واسع |
| Action Buttons | U/A | Screens | Core | نعم | حسب الفعل | DB | 3 | فعل محكوم بالصلاحية | فعل خطير |
| CTA Buttons | U | UI | Core | نعم | لا | — | 3 | إجراء موجَّه | — |
| Entity Profile | U | Workspace | Core | نعم | لا | DB,RAG | **2 (مبدئي) / 4 (كامل)** | تجميع كيان بالصلاحية | تجميع مفرط |
| Reports | U/A | Reports | Core | نعم | لا | DB | 6 | تقرير من مصادر الحقيقة | بيانات قديمة |
| Long Reports | U/A | Reports | Core | نعم | لا | LLM,RAG,DB | 6 | بناء قسماً قسماً + استشهاد | تكلفة/هلوسة |
| File Upload | U | Workspace | Core | نعم | لا | Obj | 5 | رفع مدقَّق إلى Obj | ملفات ضارة |
| PDF/Office Processing | U/A | Media | Core | نعم | لا | Obj,Srch,Vec | 5 | استخراج/فهرسة | parsing رديء |
| OCR | U/A | Media | Core | نعم | لا | Obj | 5 | نص من صور/مسح | جودة عربي |
| Image Understanding | U/A | Media | Opt | نعم | لا | LLM(vision),Obj | 5 | وصف/تصنيف صورة | عتاد ثقيل |
| Audio Transcription | U/A | Media | Core | نعم | لا | LLM(ASR),Obj | 5 | صوت→نص | لهجات |
| Video Understanding | U/A | Media | Opt | نعم | لا | LLM,Obj | 5 (معماري)/لاحقاً (ثقيل) | صوت+keyframes الآن؛ فيديو كامل عند توفر العتاد | عتاد ثقيل جداً |
| RAG | U/A | Chat/Reports | Core | نعم | لا | Vec,Srch,LLM | 5 | استرجاع مصفّى بالصلاحية | تسريب/هلوسة |
| SQL Agent | U/A | Chat/Reports | Core | نعم | لا | DB | 6 | SELECT آمن ضمن الصلاحية | حقن/تسريب |
| App Store | U | Workspace | Core | نعم | حسب التطبيق | MCP,DB | 7 | يرى المسموح فقط | وصول واسع |
| MCP/API Integrations | U/A | Store/Admin | Core | نعم | نعم (إجراءات) | MCP | 7 | استدعاء ضمن الصلاحية + بوابة | تنفيذ خطير |
| Connector Management | A/SA | Admin | Core | نعم | نعم | MCP,DB | 7 | تسجيل/اختبار/تفعيل موصل | ربط ضار |
| Model/Provider Management | A/SA | Admin | Core | جزئي (capability) | حسب السياسة | DB | 5/6 | تغيير نموذج من الواجهة | نموذج غير آمن |
| Feature Flags | A/SA | Admin | 🔒Core | لا (الخدمة نفسها) | حسب العلم | DB | 0/4 | تفعيل/تعطيل قدرة مدقَّق | تعطيل خاطئ |
| Profiles | SA/Ops | Admin/Ops | 🔒Core | لا | نعم (بيئة) | DB | 0 | تبديل profile بالإعداد | انقطاع |
| Configuration Management | SA/Ops | Admin/Ops | 🔒Core | لا | نعم | DB | 0 | تغيير مدقَّق + versioning | كسر إقلاع |
| Audit Viewer | A/SA | Admin | 🔒Core | لا | لا | DB | 1+ | عرض/بحث السجل | كشف حسّاس |
| Monitoring View | A/SA/Ops | Admin/Ops | Core | لا | لا | — | 0/8 | صحة الخدمات | إنذار كاذب |
| License/About | U/A | UI | Core | لا | لا | — | 0 | attribution صحيح | خرق ترخيص |
| Backup/Restore | Ops | Ops | Core | لا | نعم | Obj,DB | 8 | نسخ/استعادة متحقَّقة | فقد بيانات |
| Security/Policy | SA | Admin | 🔒Core | لا | نعم | DB | 4 | سياسات تُنفَّذ | سوء ضبط |
| Permission Management | A/SA | Admin | 🔒Core | لا | حسب التغيير | DB | 1/4 | سياسات مدقَّقة | تصعيد صلاحية |
| Organization Management | A/SA | Admin | Core | لا | حسب التغيير | DB | 1 | قطاعات/إدارات/عضوية | خلط تنظيمي |
| User Management | A/SA | Admin | Core | لا | حسب التغيير | DB | 1 | تعطيل/تفعيل/تغيير كلمة | تصعيد/تعطيل خاطئ |

> **ملاحظة (A10):** القائمة الحصرية للميزات **غير القابلة للتعطيل** من الواجهة تُثبَّت نصياً في تصميم Phase 4 (Feature/Module Management)؛ المبدأ الآن: الأساسيات 🔒 لا زر تعطيل لها إطلاقاً.

---

## 5. Service Catalog (modules داخل Modular Monolith ما لم يُذكر خلاف — انظر جدول المصطلحات في المنهجية)

| الخدمة | الدور | C/O | يعطّلها | تبعيات | config keys | Health | Local→Prod | توصية |
|---|---|---|---|---|---|---|---|---|
| Enterprise UI | واجهة U/A — **React+Vite SPA مستقلة (D1)** | Core | – | Backend (OpenAPI/SDK فقط) | UI_BASE_URL, LOCALE, THEME | تحميل الأصول | 1 → N + CDN داخلي | اعتماد |
| Backend API (Monolith) | مدخل/تنسيق | Core | – | Postgres (+Cache/Queue/Lock Providers) | APP_PROFILE, DB_URL, CACHE_BACKEND=memory|postgres|valkey | /health (+فرعية db/qdrant/opensearch/llm) | 1 → N خلف LB | اعتماد |
| Admin Console (module/UI) | إدارة | Core | – | Backend | – | – | – | اعتماد |
| Auth Service | مصادقة + IdP-adapter | 🔒Core | – | platform_db | AUTH_PROVIDER, JWT_SECRET | – | Local→LDAP/OIDC بالإعداد | اعتماد |
| Organization Service | تنظيم | Core | – | platform_db | – | – | – | اعتماد |
| Permission Service | محرّك صلاحيات | 🔒Core | – | platform_db | POLICY_CACHE_TTL | – | نفسه + كاش | اعتماد |
| Screen Metadata Service | تعريفات شاشات/حقول | Core | – | platform_db | – | – | – | اعتماد |
| Record Service | CRUD الكيانات | Core | – | apps_db | DB_ROUTER_MAP | – | schema→physical بالإعداد | اعتماد |
| Migration/Generation Service | توليد محكوم | Core | – | platform/apps_db | MIGRATION_APPROVAL=on | – | – | اعتماد |
| Workflow Service | دورة حياة workflows | Core | A (capability) | platform_db | – | – | – | اعتماد |
| Task Service | مهام/قوالب | Core | A | platform_db | – | – | – | اعتماد |
| Project Service | مشاريع | Core | A | platform_db,Obj | – | – | – | اعتماد |
| Notification Service | إشعارات | Core | A | platform_db, QueueProvider | – | – | Postgres-queue → Valkey بالإعداد | اعتماد |
| **Chat Service (module `chat` — A5)** | محادثات المستخدم وجلساتها وسياقها | Core (قدرة flaggable) | A (capability) | permissions, llm-gateway, rag, projects, audit | CHAT_* | – | workers للدردشة | **اعتماد (مضاف بمراجعة A5، Phase 6)** |
| Audit Service | تدقيق append-only | 🔒Core | – | platform_db | AUDIT_RETENTION | – | partition/archival | اعتماد |
| Config Service (Registry) | إعداد/profiles | 🔒Core | – | platform_db | APP_PROFILE, BUNDLES | – | – | اعتماد |
| Feature Flag Service | أعلام القدرات | 🔒Core | – | platform_db | FLAG_SCOPES | – | – | اعتماد |
| Service Registry | كتالوج/صحة/تبعيات | 🔒Core | – | – | – | يجمع /health | يتكامل مع orchestrator | اعتماد (خفيف) |
| Deployment/Operations Controller | lifecycle/ترقية (طبقة عمليات) | Core (Ops) | Ops | orchestrator | OPS_MODE | – | scripts → controller | اعتماد رفيع |
| LLM Gateway | توجيه النماذج (OpenAI-compatible) | Core | – | Ollama/vLLM | LLM_ENDPOINTS | فحص endpoints | Ollama→vLLM بالإعداد | اعتماد — **البوابة الوحيدة للـ LLM** |
| Model Registry / Provider Registry | كتالوج نماذج/مزوّدين + capability mapping | Core | – | platform_db | PROVIDER_ENDPOINTS | – | – | اعتماد |
| RAG Service | فهرسة/بحث هجين | Core | A | Qdrant,OpenSearch | EMBED_CAP, RERANK_CAP | فحص المخازن | عناقيد | اعتماد |
| SQL Agent Service | SQL آمن للقراءة | Core | A | apps_db(RLS) | SQL_ALLOWLIST | – | read-replica | اعتماد |
| Media/OCR Service | pipeline الوسائط | Core (قدرات flaggable) | A (capability) | Obj,Gateway,Registry | MEDIA_CAPS | – | workers/عُقد GPU | اعتماد — **جاهز معمارياً من البداية** |
| File Service | إدارة الملفات | Core | – | Obj | S3_ENDPOINT | فحص Obj | bucket/erasure | اعتماد |
| Report Service | تقارير/تصدير | Core | A | reporting_db,LLM | – | – | – | اعتماد |
| Integration Service | موصلات | Core (قدرات flaggable) | A/SA | integration_db | CONNECTORS | – | – | اعتماد |
| App Store Service | متجر المستخدم | Core (قدرات flaggable) | A | integration_db | – | – | – | اعتماد |
| MCP Connector Service | جسر MCP | Core | A | Integration | MCP_SERVERS | فحص الخوادم | – | اعتماد |
| PostgreSQL ×4 | مصدر الحقيقة | Core | – | – | DB_URL, POOL + **مستخدم least-privilege لكل قاعدة** | فحص اتصال | single→HA+PgBouncer+replicas | اعتماد |
| Qdrant | متجهات | **Core · في Local** | – | – | QDRANT_URL | فحص | single→cluster | اعتماد |
| OpenSearch | بحث/logs | **Core · في Local** | – | – | OS_URL (demo heap) | فحص | single→cluster | اعتماد |
| Cache/Queue/Lock Providers | تجريد ثلاثي؛ افتراضي memory/PostgreSQL؛ Valkey ⚠️ optional-ready | Core (التجريد) · الحاوية Opt-off | – | – | CACHE_BACKEND, QUEUE_BACKEND, LOCK_BACKEND | فحص عند تفعيل الحاوية | Postgres→Valkey بالإعداد | لا حاوية في P0/P1 (D4)؛ التفعيل ببوابة فئة 3 |
| ObjectStorageProvider (FS افتراضاً؛ MinIO ⚠️|SeaweedFS لاحقاً) | تخزين ملفات (ليس معالجة) | Core (التجريد) · الحاوية Opt-off حتى مرحلة الملفات | – | – | STORAGE_BACKEND=fs|s3, S3_* | فحص عند التفعيل | FS→S3-compatible بالإعداد | حسم المزوّد قبل تفعيل صورته (D5، فئة 3) |
| Neo4j/Graph | علاقات | Opt (off) | A/SA (flag) + Ops (تشغيل) | – | GRAPH_ENABLED=false | فحص | – | فضّل Apache AGE إن لزم |
| Observability Baseline (D6) | Audit(PG) + JSON logs + Log Viewer + Health + Error Catalog + IDs + /metrics اختياري | Core | – | platform_db | LOG_LEVEL, METRICS_ENABLED | ذاتي | + Prometheus-server/Grafana/Loki/OTel في P8 (رهن مراجعة) | اعتماد الخط الأساسي |
| Backup/Restore tools | تعافٍ/نقل | Core | Ops | Obj,DB | BACKUP_PATH | – | – | اعتماد + offline bundle موقّعة |

**العدد المرجعي للـ modules: 36** (قائمة المنهجية §7: 35 + `chat` المضاف بمراجعة A5).

---

## 6. Admin Screens Catalog

| الشاشة | الوصول | العمليات | صلاحيات | تُغيّر منها | Ops-only | Audit | القبول | مخاطر |
|---|---|---|---|---|---|---|---|---|
| Admin Dashboard | A/SA | ملخصات/تنبيهات | admin.view | – | – | – | حالة عامة | كشف مؤشرات |
| Users | A/SA | إضافة/تعطيل/دور | user.manage | بيانات مستخدم (لا الرقم الوظيفي/اسم المستخدم) | – | user.* | تعطيل/تفعيل يعمل | تصعيد |
| Organization/Sectors/Departments | A/SA | CRUD تنظيمي | org.manage | الهيكل | – | org.* | عضوية صحيحة | خلط |
| Roles | A/SA | CRUD أدوار | role.manage | الأدوار | – | role.* | ربط صلاحيات | تصعيد |
| Permissions | SA | سياسات RBAC/ABAC/ReBAC | perm.manage | السياسات | – | perm.* | تُنفَّذ فعلاً | ثغرة |
| Data Classification | SA | مستويات/قواعد | class.manage | التصنيفات | – | class.* | تُطبَّق | تسريب |
| Screens / Fields | A | تعريف شاشات/حقول | screen.manage / field.manage | الميتاداتا | – | screen.created/field.added | تُخزَّن صحيحة | خطأ تعريف |
| Database Generation Review | A/SA | فحص migration | migration.review | عرض/تعليق | – | migration.generated | فحص تعارض/مخاطر | تطبيق ضار |
| Migration Approval | A/SA | اعتماد/رفض | migration.approve | حالة الاعتماد | – | migration.approved/rejected/applied | لا تطبيق بلا اعتماد | كسر |
| Records Admin | A | إدارة سجلات | record.admin | سجلات بالصلاحية | – | record.* | RLS/FLS مطبّق | تجاوز |
| Workflows / Workflow Approvals | A / A+Manager | بناء/اعتماد | workflow.manage/approve | التعريف/الحالة | – | workflow.* | SoD (منشئ≠معتمِد) | أثر واسع |
| Tasks Templates / Projects Admin / Notifications Admin | A | قوالب/مشاريع/قنوات | task/project/notif.manage | – | – | task/project/notif.* | تعمل بالصلاحية | – |
| App Store Management | A | نشر/إتاحة | store.manage | الإتاحة | – | app.* | يرى المسموح فقط | وصول واسع |
| MCP/API Connectors | A/SA | تسجيل/اختبار/تفعيل | connector.manage | الموصلات | endpoints/secrets → **Ops** | connector.* | اختبار اتصال | ربط ضار |
| Model/Provider Management | A/SA | نموذج لكل capability | model.manage | خريطة capability→model | provider endpoints البنيوية → **Ops** | model/provider.changed | تغيير من الواجهة | نموذج غير آمن |
| Media/OCR Settings | A | نماذج/حدود وسائط | media.manage | capability flags/حدود | عُقد GPU → **Ops** | media.* | تبديل نموذج نوع وسائط | عتاد |
| RAG Settings | A | chunking/rerank/فهرسة | rag.manage | معاملات RAG | – | rag.* | استرجاع محسّن | جودة |
| Feature Flags | A/SA | تفعيل/تعطيل **قدرة** | flag.manage | الأعلام غير المحميّة | الأساسية محميّة؛ lifecycle الخدمات → **Ops** | feature_flag.changed | قدرة لا خدمة | تعطيل خاطئ |
| Profiles / Configuration Registry | SA | defaults/قيم dynamic | profile/config.manage | القيم dynamic | static/secrets/تبديل بيئة → **Ops** | profile/config.changed | versioning/rollback | كسر إقلاع |
| Service Health | A/SA/Ops | **عرض فقط** | health.view | – | lifecycle (start/stop/scale) → **Ops** | service.health_alert | حالة/تبعيات صحيحة | إنذار كاذب |
| Audit Logs | A/SA | عرض/بحث/تصدير | audit.view | – | – | export.requested | بحث دقيق | كشف حسّاس |
| Reports Admin | A | قوالب/جدولة | report.admin | القوالب | – | report.* | من الحقيقة | قديم |
| Backup/Restore | **Ops** | نسخ/استعادة | ops.backup | – | كامل → **Ops** | backup/restore.* | متحقَّقة | فقد |
| About/Licenses | A/U | عرض تراخيص | – | – | – | – | attribution صحيح | خرق |
| Security Policies | SA | سياسات/بوابات | security.manage | السياسات | – | security.* | تُنفَّذ | سوء ضبط |

---

## 7. User Screens Catalog

| الشاشة | المستخدم | العمليات | صلاحيات | المصادر | LLM | RAG | Store | Audit | القبول |
|---|---|---|---|---|---|---|---|---|---|
| User Home | U | تصفح/اختصارات | user.view | platform/apps_db | لا | لا | لا | جزئي | يعرض المسموح فقط |
| Chat | U | سؤال/أمر طبيعي | chat.use | DB/docs/APIs | نعم | نعم | نعم | نعم | مسنود بمصدر + No-Guessing |
| Projects | U | إنشاء/تجميع | project.use | apps_db,Obj | اختياري | اختياري | لا | نعم | نطاق بالصلاحية |
| Tasks | U | إنشاء/تنفيذ | task.use | DB | نعم | اختياري | نعم | نعم | تنفيذ مصرّح |
| Notifications | U | قراءة/تفاعل/دردشة | notif.use | DB | اختياري | لا | لا | نعم | إشعار مدقَّق |
| App Store / My Connected Apps | U | تصفح/ربط/فصل/تفويض | store.use / app.link | integration_db | لا | لا | نعم | نعم | المسموح فقط؛ ربط ضمن الصلاحية |
| Screens/Applications | U | استخدام الشاشات المولّدة | screen.use | apps_db | اختياري | اختياري | حسب التطبيق | نعم | RLS/FLS مطبّق |
| Records | U | CRUD بالصلاحية | record.use | apps_db | لا | لا | لا | نعم | عزل صفوف/حقول |
| Entity Profile | U | عرض كيان مجمّع | entity.view | DB,RAG | اختياري | نعم | لا | نعم | تجميع بالصلاحية (مبدئي P2/كامل P4) |
| Files | U | رفع/عرض | file.use | Obj | لا | لا | لا | نعم | رفع مدقَّق |
| Reports | U | توليد/تصدير | report.use | DB,RAG | نعم | نعم | لا | نعم | من مصادر الحقيقة |
| Workflow Inbox / Approvals | U / Manager | متابعة/اعتماد | workflow.use/approve | platform_db | لا | لا | لا | نعم | SoD مطبّق |
| Search | U | بحث موحّد | search.use | DB,Vec,Srch | اختياري | نعم | لا | نعم | نتائج مصفّاة بالصلاحية |
| Settings | U | تفضيلات/لغة/كلمة مرور | self.manage | platform_db | لا | لا | لا | نعم | لا تغيير للرقم الوظيفي/اسم المستخدم |

---

## 8. Configuration &amp; Profiles Matrix

**Environment Profiles (واحد نشط):**
| Profile | يتغيّر | لا يتغيّر | خدمات | نموذج افتراضي | resources | logging | monitoring | يغيّره | restart؟ | approval؟ |
|---|---|---|---|---|---|---|---|---|---|---|
| Local | endpoints محلية، بلا TLS، replica=1 | **الكود/المعمارية** | **كلها حاضرة** (demo، Neo4j off) | خفيف (Ollama) | منخفض | debug | أساسي | Ops/SA | نعم (static) | لا |
| Demo | بيانات عرض، 1–2 مستخدم | الكود | كلها (demo) | خفيف | منخفض-متوسط | info | أساسي | Ops/SA | نعم | لا |
| Staging | إعدادات أكبر، اختبار شامل | الكود | كلها | متوسط | متوسط | info | متوسط | Ops/SA | نعم | نعم |
| Production | عناقيد، TLS، replicas=N، عُقد GPU | الكود | كلها | vLLM موزّع | عالٍ | warn/audit | كامل | Ops | نعم | نعم |

**Capability Bundles (قابلة للتركيب فوق البيئة):**
| Bundle | يفعّل | ملاحظات | يغيّره | restart؟ | approval؟ |
|---|---|---|---|---|---|
| Low-resource | نماذج خفيفة؛ **pgvector/PG-FTS كـ fallback صريح** | لا يحذف Qdrant/OpenSearch من التصميم؛ استخدامه استثناء معلن | SA | جزئي | لا |
| Full-stack | كل القدرات | staging/prod | SA | جزئي | نعم |
| Media-enabled | OCR/vision/audio/video pipeline | **الجاهزية المعمارية دائمة**؛ الثقيل حسب العتاد | A/SA | لا (flags) | حسب السياسة |
| Security-enabled | سياسات/بوابات مشدّدة | فرق الأمن/CERT | SA | لا | نعم |
| Graph-enabled | Graph module | Neo4j/AGE | SA | نعم (تشغيل الخدمة=Ops) | نعم |
| Integration-enabled | موصلات/متجر واسع | حسب الأنظمة الداخلية | A/SA | لا | نعم |

**قواعد:** static → restart (Ops)؛ dynamic → live عبر الـ Registry. الأساسية محميّة. كل تغيير مدقَّق + versioned + قابل للـ rollback. **lockfiles + digest pinning** لكل الاعتماديات والصور.

---

## 9. Capability-to-Model Mapping

> النظام مربوط بـ **capabilities** لا أسماء نماذج؛ الأمثلة توضيحية. تغيير أي capability→model من الأدمن عبر الـ Registry، مع hardware-aware selection وfallback معرّف، وكل استخدام مدقَّق. **تراخيص أوزان النماذج بوابة مزدوجة:** قبل تنفيذ Phase 5 (تشغيلها) وقبل التوزيع (تضمينها في bundle).

| Capability | نوع النموذج | GPU؟ | dev؟ | يغيّره الأدمن؟ | C/O | Fallback | مخاطر |
|---|---|---|---|---|---|---|---|
| chat | LLM عام | مفضّل | نعم (خفيف) | نعم | Core | نموذج أصغر | هلوسة |
| reasoning | LLM قوي | نعم | محدود | نعم | Core | chat model | تكلفة |
| summarization | LLM متوسط | مفضّل | نعم | نعم | Core | chat | فقد دقة |
| long report | سياق طويل | نعم | محدود | نعم | Core | تقسيم أدق | تكلفة |
| SQL generation | LLM/coder | مفضّل | نعم | نعم | Core | قوالب SQL | حقن |
| code generation | coder | نعم | محدود | نعم | Opt | – | كود ضار |
| embedding | embedder | مفضّل | نعم | نعم | Core | embed أصغر | جودة استرجاع |
| reranking | reranker | مفضّل | نعم | نعم | Core | بلا rerank | ترتيب أضعف |
| OCR | OCR engine | لا/مفضّل | نعم | نعم | Core | Tesseract | جودة عربي |
| document understanding | multimodal/LLM | نعم | محدود | نعم | Opt | استخراج نصي | عتاد |
| image understanding | vision | نعم | محدود | نعم | Opt | OCR فقط | عتاد |
| audio transcription | ASR | مفضّل | نعم | نعم | Core | أصغر | لهجات |
| video understanding | video/multimodal | نعم (ثقيل) | لا (لاحقاً) | نعم | Opt | صوت+keyframes | عتاد جداً |
| classification / validation | LLM/قواعد | مفضّل | نعم | نعم | Core | قواعد/citations (**validation لا تفشل مفتوحة**) | خطأ/fail-open ممنوع |
| translation / Arabic enhancement | LLM | مفضّل | نعم | نعم | Opt | بلا/نموذج عام | دقة/أسلوب |

---

## 10. Data Flow Scenarios (20)

1. **سؤال عن بيانات داخلية:** UI→API(auth)→Orchestrator(تصنيف+سياق+**Permission Gate قبل الاسترجاع**)→Retrieval/SQL بالصلاحية→Validation→Reasoning→إجابة+provenance. Audit: rag/sql + record.viewed. فشل: نقص أدلة→No-Guessing.
2. **سؤال غامض:** كشف الغموض→**طلب توضيح** (لا تخمين).
3. **رفض صلاحية:** Gate=deny→رسالة بلا استرجاع. Audit: permission_denied. default-deny.
4. **الأدمن ينشئ شاشة:** ميتاداتا في platform_db. Audit: screen.created/field.added.
5. **توليد migration:** ملف + فحص تعارض/مخاطر (لا DDL من نموذج). Audit: migration.generated.
6. **اعتماد migration:** approve (SoD)→تطبيق داخل schema + versioning. Audit: approved/applied. فشل: rollback نسخة.
7. **إدخال بيانات:** Record Service مع RLS/FLS + ownership. Audit: record.created/updated.
8. **إنشاء workflow (مستخدم):** Draft→Validation→Permission→Risk. **لا تفعيل**.
9. **اعتماد workflow (Manager):** approve (SoD)→Activation. فشل: rejected+سبب.
10. **App Store:** يرى المسموح فقط. غير المسموح يُخفى.
11. **ربط حساب بتطبيق داخلي:** تفويض عبر Integration؛ رموز مُعمّاة في integration_db. Audit: app.connected.
12. **رفع PDF:** Obj→Media pipeline (استخراج/OCR)→chunk→embed→**فهرسة محكومة الصلاحية مع provenance**. Audit: file.uploaded/ocr.completed/media.processed.
13. **رفع صورة:** Obj→vision (إن مفعّل) أو OCR→نتيجة مربوطة بالمصدر. fallback: OCR.
14. **رفع فيديو:** Obj→استخراج صوت+transcription+keyframes→(فهم كامل إن توفّر العتاد)؛ **المخرجات تدخل فهرس RAG نفسه** بالصلاحية والمصدر. fallback: صوت+keyframes.
15. **تقرير طويل:** بناء قسماً قسماً من المصادر مع استشهاد؛ قسم بلا دليل→يُعلَّم.
16. **تغيير نموذج في الـ Registry:** capability→model من الأدمن؛ الـ Gateway يحلّه وقت التشغيل. Audit: model.changed. فشل: fallback المعرّف.
17. **تغيير feature flag:** **قدرة لا خدمة**؛ الأساسية محميّة. Audit: feature_flag.changed.
18. **Ops يغيّر profile/config:** عبر سطح العمليات؛ static→restart؛ fail-fast + rollback. Audit: profile/config.changed.
19. **فشل خدمة:** Service Registry يكتشف→تنبيه؛ الأدمن يرى (قراءة)، **Ops يتصرّف**. Audit: service.health_alert. تدهور رشيق.
20. **إبطال كاش:** تغيّر نسخة مستند/فهرس/سكيم/**نطاق صلاحية**→المفتاح يبطل + إعادة تحقق live قبل الحرِج. Audit: cache_invalidated.

---

## 11. Audit Events Catalog

> **قاعدة:** كل تغيير مهم يُسجَّل. retention أمثلة قابلة للضبط.

| الحدث | الفاعل | الهدف | خطورة | حقول لازمة | احتفاظ | موافقة؟ | للأدمن؟ |
|---|---|---|---|---|---|---|---|
| login / logout | user | session | Info | user,ip,ts | 1y | لا | نعم |
| failed_login | user? | auth | Warn | attempt,ip,ts | 1–2y | لا | نعم |
| permission_denied | user | resource | Warn | user,resource,policy,ts | 2y | لا | نعم |
| role_assigned / role_removed | admin | user/role | High | actor,target,role | 3y | حسب السياسة | نعم |
| user_disabled | admin | user | High | actor,target,reason | 3y | حسب السياسة | نعم |
| screen_created / field_added | admin | screen/field | Info | actor,obj | 2y | لا | نعم |
| migration_generated | system/admin | migration | Info | migration,diff | 3y | لا | نعم |
| migration_approved / rejected | approver | migration | High/Med | approver,reason | 3y | نعم | نعم |
| migration_applied | system | schema | High | migration,version | 3y | بعد اعتماد | نعم |
| record_viewed | user | record | Info | user,record,class | 6–12m | لا | نعم |
| record_created / updated | user | record | Info | user,record(,diff) | 2y | حسب workflow | نعم |
| record_deleted | user/admin | record | High | actor,record | 3y | غالباً | نعم |
| export_requested | user | dataset | High | user,scope,class | 3y | حسب السياسة | نعم |
| workflow_created | user | workflow | Info | user,wf | 2y | لا | نعم |
| workflow_approved / rejected | approver | workflow | High/Med | approver(,reason) | 3y | نعم | نعم |
| workflow_activated | system | workflow | High | wf,version | 3y | بعد اعتماد | نعم |
| connector_added / disabled | admin | connector | High/Med | actor,connector | 3y | نعم/سياسة | نعم |
| app_connected / disconnected | user | app | Med/Info | user,app | 2y | حسب التطبيق | نعم |
| model_changed / provider_changed | admin/ops | capability/provider | High | actor,old,new | 3y | حسب السياسة | نعم |
| feature_flag_changed | admin | flag | High | actor,flag,old,new | 3y | حسب العلم | نعم |
| profile_changed | ops/sa | profile | Critical | actor,old,new | 5y | نعم | نعم |
| config_changed | ops/sa | config key | High | actor,key,old,new | 5y | نعم | نعم |
| file_uploaded | user | file | Info | user,file,class | 2y | لا | نعم |
| media_processed / ocr_completed | system | media/doc | Info | obj,type,model/engine | 1–2y | لا | نعم |
| rag_query_executed | user | query | Info | user,scope | 6–12m | لا | نعم |
| sql_query_generated / executed | system | query/db(read) | Info/Med | user,query(,rows) | 1y | لا | نعم |
| report_generated | user | report | Info | user,report | 2y | لا | نعم |
| cache_invalidated | system | cache key | Info | key,reason | 3–6m | لا | جزئي |
| service_health_alert | system | service | Warn/High | service,state | 1y | لا | نعم |
| backup_created / restore_executed | ops | backup/system | High/Critical | actor,target/source | 3–5y | نعم | Ops |

---

## 12. Risks and Trade-offs

Modular Monolith مقابل Microservices (محسوم للمونوليث المعياري microservice-ready) · سهولة مقابل أمان في إدارة الخدمات (محسوم: capabilities للأدمن، lifecycle للعمليات، خدمات محميّة + Safe Mode + رسم تبعيات) · Ollama-dev/vLLM-prod عبر عقد OpenAI-compatible · تراخيص AGPL/متغيّرة (**تبقى Needs License Review**؛ بدائل جاهزة: Valkey/SeaweedFS/pdfplumber/VictoriaMetrics) · ذاكرة البحث على dev (demo limits؛ low-resource bundle **fallback صريح** لا افتراضي) · الوسائط الثقيلة (جاهزية معمارية دائمة + تشغيل بالإعداد + fallback صوت/keyframes) · الهلوسة (No-Guessing + Validation-with-citations كاختبارات) · تعقيد metadata-driven (خط ترحيل صارم) · قابلية النقل (صورة واحدة + فرق إعداد فقط + اختبارات profile + **lockfiles/digest pinning**).

---

## 13. Open Decisions — مرجع مُلزم

القرارات المفتوحة **مصنّفة إلى خمس فئات** (Blockers قبل التصميم / قبل التنفيذ / قبل Docker Compose / قبل التوزيع النهائي / Configurable) — **المرجع المُلزم الوحيد:** وثيقة `open-decisions.md` (open-decisions). لا تُكرَّر هنا لمنع الانحراف. خلاصة الحالة: **لا Blockers قبل التصميم**؛ التراخيص الحسّاسة (Redis/Valkey · MinIO · Grafana/Loki · PyMuPDF · ffmpeg) **Needs License Review** ولا تدخل التنفيذ قبل الحسم.

---

## 14. Roadmap — مرجع مُلزم

خريطة المراحل الكاملة (Phase 0 → Phase 8 + Backlog) بأهدافها ونطاقها وشروط قبولها وبواباتها — **المرجع المُلزم الوحيد:** `phase-roadmap.md`. ملخص الترتيب: 0 Foundation &amp; Full-Stack Skeleton → 1 Governed Core + Screen Builder → 2 Advanced Screen/Records/Initial Entity Profile → 3 Workflows + Approvals + Action Buttons → 4 Advanced Permissions + Full Entity Profile → 5 RAG + Files + OCR + Media Pipeline → 6 LLM Gateway + Agents + SQL Agent + Reports → 7 MCP/API Integrations + Enterprise App Store → 8 Monitoring + Offline Deployment + Production Readiness → Backlog. **قاعدة:** كل مرحلة تُصمَّم في محادثة مستقلة (Vision→Tasks) ثم تُنفَّذ لاحقاً؛ تُسمّى المراحل دائماً بالرقم + الاسم.

---

## 15. Final Recommendation

الأسلوب المعتمد نهائياً: **Modular Monolith حقيقي (microservice-ready) + Spec-driven Development متوافقة مع GitHub Spec Kit / Spacekit** (ADR-0001: **Accepted**). الثوابت المفعّلة مبكراً: Config Registry + Feature Flags + Service Registry · LLM Gateway بعقد OpenAI-compatible (البوابة الوحيدة) · Model/Provider Registry بالـ capabilities · Media pipeline جاهزة معمارياً · الحوكمة قبل القدرة (الصلاحية قبل الاسترجاع، default-deny، Audit شامل) · Three Control Planes (Capability=Admin · Configuration=Super Admin · Operations=Ops) · License Review إلزامية · lockfiles + digest pinning · نقل إلى production بالإعداد فقط. الستاك المعتمد نهائياً: **React + Vite + TS + Tailwind (SPA مستقلة)** و**Python/FastAPI**، مع التجريدات الثلاث (Cache/Queue/Lock بافتراضي memory/PostgreSQL) وObjectStorageProvider (بافتراضي filesystem) وObservability Baseline وGitHub-الآن بنقل مغلق موقّع وسياسة Reference-aware. **الخطوة التالية:** تصميم **Phase 1 — Governed Core + Screen Builder** في محادثة مستقلة، بلا كود.
