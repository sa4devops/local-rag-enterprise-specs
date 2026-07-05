# decisions/adr/README.md — استراتيجية وسجل قرارات المعمارية (ADRs)

> **Version:** 1.1 (ADR-0017..0022 مضافة) · **Status:** Current / Accepted · **Date:** 2026-07-04
> **Authority:** هذا الملف هو **السجل الكنسي** لترقيم الـ ADRs وحالاتها. الترقيم الوارد في Methodology v1.0 (القديم) **Superseded**.
> **Purpose:** كل قرار معماري مهم يُوثَّق كـ ADR قبل تنفيذه؛ كسر أي قاعدة boundaries أو تغيير معماري بلا ADR **ممنوع** (constitution م8/م20، Methodology §13).

## صيغة كل ADR (ملف مستقل `ADR-XXXX-title.md` يُنشأ عند زرع specs)
العنوان · السياق · القرار · البدائل المدروسة · السبب · المخاطر · الأثر · التاريخ · الحالة (**Proposed / Accepted / Superseded**).

## السجل الكنسي

| # | العنوان | الحالة | ملاحظة |
|---|---|---|---|
| ADR-0001 | Modular Monolith + Spec-driven Development (Spec Kit/Spacekit-compatible) | **Accepted** | اعتمده SA صراحةً |
| ADR-0002 | Enterprise UI بدلاً من Open WebUI كواجهة نهائية | **Accepted** | Open WebUI مرجع دراسة فقط؛ أي استخدام داخلي = Needs Legal Review |
| ADR-0003 | PostgreSQL + القواعد الأربع + schemas + RLS/FLS | **Accepted** | نموذج database.docx؛ ثلاث درجات فصل |
| ADR-0004 | Qdrant + OpenSearch حاضران في Local Demo | **Accepted** | pgvector/PG-FTS ضمن low-resource bundle الصريح فقط |
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
| ADR-0017 | Frontend = React + Vite + TypeScript + Tailwind + shadcn-style (SPA مستقلة؛ لا Next.js ولا SvelteKit) | **Accepted** | قرار D1 (2026-07-04) |
| ADR-0018 | Cache/Queue/Lock Providers بافتراضي memory/PostgreSQL؛ Valkey optional-ready | **Accepted** | D4؛ يخصّص ADR-0012 |
| ADR-0019 | ObjectStorageProvider بافتراضي local filesystem؛ حسم المزوّد بمرحلة الملفات | **Accepted** | D5؛ يخصّص ADR-0013 |
| ADR-0020 | Observability Baseline (Audit-PG + JSON logs + Health + Error Catalog + IDs + /metrics اختياري) | **Accepted** | D6؛ التوسعة P8 |
| ADR-0021 | Reference-aware Clean Implementation Policy | **Accepted** | D8؛ النص الملزم في coding-standards |
| ADR-0022 | GitHub الآن + قناة نقل مغلقة موقّعة؛ Git داخلي = Backlog | **Accepted** | D7 |

**قرارات مستقبلية تتطلب ADR جديداً (أمثلة):** تفعيل Graph (AGE/Neo4j) · فصل أي module إلى microservice · اعتماد K8s/OpenShift · إدخال تكامل خارجي عبر proxy · تغيير التصنيف الخماسي.
