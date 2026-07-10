# decisions/adr/README.md — استراتيجية وسجل قرارات المعمارية (ADRs)

> **Version:** 1.2 (v1.0-architecture-baseline: سياسة D15 كاملة + زرع الملفات الفردية + ADR-0023..0028) · **Status:** Current / Accepted · **Date:** 2026-07-10 (الأصل 2026-07-04)
> **Authority:** هذا الملف هو **السجل الكنسي** لترقيم الـ ADRs وحالاتها. الترقيم الوارد في Methodology v1.0 (القديم) **Superseded**.
> **Purpose:** كل قرار معماري مهم يُوثَّق كـ ADR قبل تنفيذه؛ كسر أي قاعدة boundaries أو تغيير معماري بلا ADR **ممنوع** (constitution م8/م20/م21، Methodology §13).

## سياسة الـ ADR (D15 — v1.0-architecture-baseline)

**متى يلزم ADR (الموجبات):** كل قرار يمس: المعمارية · حدود الوحدات (modules) · العقود العامة (public contracts) · التخزين · الأمن · نموذج البيانات · النشر · الاعتماديات الاستراتيجية · تقنية يصعب استبدالها · الاستخراج إلى خدمات · معمارية المزوّدات · عقد الواجهة/الخادم.
**متى لا يلزم:** تصحيح الأخطاء الكتابية · تحسين الصياغة/التنسيق · التفاصيل غير المعمارية · refactor محدود يحفظ العقود.
**الحقول العشرة الإلزامية في كل ملف ADR:** السياق (Context) · **الوضع السابق (Previous state)** · القرار (Decision) · البدائل (Alternatives) · السبب (Rationale) · العواقب (Consequences) · **خطة الانتقال (Migration plan — إن وُجدت)** · الحالة (Status: Proposed/Accepted/Superseded) · التاريخ (Date) · **الوثائق المرتبطة (Related documents)**.
**قواعد إضافية:** قرار واحد لكل ADR · التجاوز يكون بوسم Superseded مع رابط الخالف (supersedes linkage) لا بالحذف · **بوابة الإغلاق:** لا يُوسم ADR بـ Accepted حتى تُنفَّذ تحديثات «الوثائق المتأثرة» الخاصة به.
**الملفات الفردية:** اعتباراً من v1.0-architecture-baseline (2026-07-10) تُزرع ملفات ADR فردية تحت `decisions/adr/` بنمط `ADR-XXXX-kebab-title.md` — الصفوف الموسومة بملف أدناه لها ملف مستقل؛ الصفوف التاريخية بلا ملف يبقى هذا السجل مرجعها حتى زرعها عند الحاجة.

## السجل الكنسي

| # | العنوان | الحالة | ملاحظة |
|---|---|---|---|
| ADR-0001 | Modular Monolith + Spec-driven Development (Spec Kit/Spacekit-compatible) | **Accepted** | اعتمده SA صراحةً |
| ADR-0002 | Enterprise UI بدلاً من Open WebUI كواجهة نهائية | **Accepted** | Open WebUI مرجع دراسة فقط؛ أي استخدام داخلي = Needs Legal Review |
| ADR-0003 | PostgreSQL + القواعد الأربع + schemas + RLS/FLS | **Accepted** | نموذج database.docx؛ ثلاث درجات فصل |
| ADR-0004 | Qdrant + OpenSearch حاضران في Local Demo | **Accepted** | pgvector/PG-FTS ضمن low-resource bundle الصريح فقط · **ملف مزروع (v1.0):** [ADR-0004-search-architecture-postgres-qdrant-opensearch.md](ADR-0004-search-architecture-postgres-qdrant-opensearch.md) (+بروفايلات D10) |
| ADR-0005 | Capability-to-Model Mapping (لا أسماء نماذج ثابتة) | **Accepted** | Model/Provider Registry + تغيير من الأدمن + fallbacks |
| ADR-0006 | Configuration-only Production Deployment | **Accepted** | لا تعديل كود/لا fork؛ profiles+bundles |
| ADR-0007 | License Review Gate إلزامي ومتكرر | **Accepted** | يشمل model weights؛ بوابة فئة 2/3 |
| ADR-0008 | فصل مستويات التحكم Admin / Super Admin / Operations | **Accepted** | capabilities للأدمن؛ lifecycle للعمليات؛ خدمات محميّة |
| ADR-0009 | OKF كطبقة metadata/knowledge محلية — ليست مصدر حقيقة | **Accepted** | توليد الحزم محلياً فقط |
| ADR-0010 | معمارية جاهزة للوسائط/Multimodal من البداية | **Accepted** | pipeline+Registry+Gateway؛ الثقيل بالإعداد حسب العتاد |
| ADR-0011 | Local Auth أولاً مع IdP-Adapter (LDAP/AD/Keycloak/OIDC/SAML لاحقاً) | **Accepted** | الرقم الوظيفي/اسم المستخدم immutable |
| ADR-0012 | تجريد Cache/Queue (Redis|Valkey عبر الإعداد) | **Accepted (المبدأ)** | خُصِّص بـ ADR-0018: الافتراضي الآن memory/PostgreSQL؛ Valkey optional-ready |
| ADR-0013 | تجريد Object Storage (MinIO|بديل S3-compatible) | **Accepted (المبدأ)** | خُصِّص بـ ADR-0019: الافتراضي الآن filesystem؛ المزوّد يُحسم بمرحلة الملفات |
| ADR-0014 | طبقة Observability قابلة للتبديل | **Accepted (المبدأ)** | Grafana/Loki رهن مراجعة؛ البدء بالأبسط في Local |
| ADR-0015 | LLM Gateway بعقد OpenAI-compatible — البوابة الوحيدة للنماذج | **Accepted** | لا استدعاء نموذج خارجه |
| ADR-0016 | مجموعة الـ Modules = 36 (35 + `chat`) بطبقات F→1→2→3→4 وقاعدة same-tier المعلنة | **Accepted** | مراجعة A5/A11 |
| ADR-0017 | Frontend = React + Vite + TypeScript + Tailwind + shadcn-style (SPA مستقلة؛ لا Next.js ولا SvelteKit) | **Accepted** | قرار D1 (2026-07-04) · **ملف مزروع (v1.0):** [ADR-0017-frontend-stack-react-vite-typescript.md](ADR-0017-frontend-stack-react-vite-typescript.md) (+موضع `/frontend` مقفل) |
| ADR-0018 | Cache/Queue/Lock Providers بافتراضي memory/PostgreSQL؛ Valkey optional-ready | **Accepted** | D4؛ يخصّص ADR-0012 · **ملف مزروع (v1.0):** [ADR-0018-cache-queue-lock-valkey-scale-profile.md](ADR-0018-cache-queue-lock-valkey-scale-profile.md) (D9c: Valkey افتراضي التوسع؛ Redis مقفل + محفزات الانتقال) |
| ADR-0019 | ObjectStorageProvider بافتراضي local filesystem؛ حسم المزوّد بمرحلة الملفات | **Accepted** | D5؛ يخصّص ADR-0013 · **ملف مزروع (v1.0):** [ADR-0019-object-storage-seaweedfs-production-default.md](ADR-0019-object-storage-seaweedfs-production-default.md) (D8: SeaweedFS افتراضي الإنتاج؛ MinIO مشروط) |
| ADR-0020 | Observability Baseline (Audit-PG + JSON logs + Health + Error Catalog + IDs + /metrics اختياري) | **Accepted** | D6؛ التوسعة P8 · **ملف مزروع (v1.0):** [ADR-0020-observability-audit-logs-baseline.md](ADR-0020-observability-audit-logs-baseline.md) (D11: مستخدم تدقيق INSERT-only · LogRepository/ops_events · لا hash chaining الآن) |
| ADR-0021 | Reference-aware Clean Implementation Policy | **Accepted** | D8؛ النص الملزم في coding-standards · **ملف مزروع ومعدَّل (v1.0):** [ADR-0021-reference-aware-clean-implementation.md](ADR-0021-reference-aware-clean-implementation.md) (D12: معايير الحكم بدل عتبة الأسطر + Reference Log) |
| ADR-0022 | GitHub الآن + قناة نقل مغلقة موقّعة؛ Git داخلي = Backlog | **Accepted** | D7 · **ملف مزروع (v1.0):** [ADR-0022-github-development-airgapped-delivery.md](ADR-0022-github-development-airgapped-delivery.md) (D13/D14: الحد الأدنى المغلق + بوابة البروفة) |
| ADR-0023 | الهوية: Enterprise AI Platform with Progressive Implementation + سلّم الجاهزية | **Accepted** | 2026-07-10 · [ADR-0023-enterprise-ai-platform-progressive-implementation.md](ADR-0023-enterprise-ai-platform-progressive-implementation.md) (D1/D16 — م22) |
| ADR-0024 | Backend = Python + FastAPI + Pydantic + SQLAlchemy + Alembic + PostgreSQL بطبقات أربع | **Accepted** | 2026-07-10 · [ADR-0024-backend-stack-python-fastapi.md](ADR-0024-backend-stack-python-fastapi.md) (يوثّق D2/D5) |
| ADR-0025 | عقد الواجهة/الخادم: REST + OpenAPI رسمي + SSE للبث؛ types مولّدة + غلاف fetch رفيع؛ WebSocket بشرط ADR | **Accepted** | 2026-07-10 · [ADR-0025-api-contract-rest-openapi-sse.md](ADR-0025-api-contract-rest-openapi-sse.md) (D6) |
| ADR-0026 | حدود منطقية لا عدد نهائياً · خريطة تغليف كأثر تنفيذي · إنفاذ متدرج · شروط الاستخراج الخمسة | **Accepted** | 2026-07-10 · [ADR-0026-module-boundaries-packaging-extraction.md](ADR-0026-module-boundaries-packaging-extraction.md) (D3 — لا يتجاوز ADR-0001) |
| ADR-0027 | معمارية سجلات القدرات والمزوّدات: سلسلة Capability→…→Audit ووحدات registry داخل الـ Monolith | **Accepted** | 2026-07-10 · [ADR-0027-provider-capability-registry-architecture.md](ADR-0027-provider-capability-registry-architecture.md) (D7 — يجمع ويُحيل) |
| ADR-0028 | سياسة خط الأساس المعماري المجمَّد v1.0-architecture-baseline (م21) | **Accepted** | 2026-07-10 · [ADR-0028-architecture-baseline-frozen.md](ADR-0028-architecture-baseline-frozen.md) (D2) |

**قرارات مستقبلية تتطلب ADR جديداً (أمثلة):** تفعيل Graph (AGE/Neo4j) · فصل أي module إلى microservice · اعتماد K8s/OpenShift · إدخال تكامل خارجي عبر proxy · تغيير التصنيف الخماسي · اعتماد WebSocket (شرط ADR-0025) · فصل مستودع الواجهة (شرط ADR-0017).
