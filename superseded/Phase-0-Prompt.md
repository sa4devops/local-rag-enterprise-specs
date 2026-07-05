> ⚠️ SUPERSEDED — لا يُستخدم للتنفيذ. المرجع الحالي: حزمة v2.0 (انظر superseded/README.md). تاريخ الوسم: 2026-07-03.

# PHASE 0 PROMPT — Skeleton & Portable Deployment Foundation
> برومبت مستقل. الصقه في محادثة جديدة مع أي Coding Agent (Claude Code / Codex / Cursor / Cline / Aider / OpenHands …). نفّذ **ما هو مكتوب فقط**. **لا منطق أعمال في هذه المرحلة.**

---

## السياق (Context)
نبني منصة تشغيل معرفي مؤسسي تعمل في **شبكة مغلقة (air-gapped)** داخل Docker. النظام **ليس chatbot**، والـ LLM **ليس مصدر الحقيقة**، والواجهة النهائية **واجهة مؤسسية خاصة** (لا Open WebUI). القاعدة الحاكمة: **منتج واحد قابل للنقل** — نفس الكود/الـ repo/الصور ينتقل من جهاز التطوير إلى سيرفرات الإنتاج **بتغيير configuration فقط**، دون تعديل كود أو إعادة بناء معمارية أو fork للإنتاج.

## هدف المرحلة (Goal)
إنشاء **الهيكل والبنية القابلة للنقل** فقط: repository منظّم + Spec Kit + Docker Compose يقلع بكل الخدمات الأساسية (بحدّها الأدنى) + **ثلاثة بروفايلات نشر** مدفوعة بالإعداد + نظام إعداد موحّد + فحوص صحّة. **إثبات أن المنظومة تقلع وتتصل خدماتها ببعضها فقط** — بلا شاشات ولا صلاحيات ولا وكلاء.

## داخل النطاق (In Scope)
1. **Repository structure** واضح ومقسّم للخدمات (انظر الهيكل أدناه).
2. **Spec Kit** (github/spec-kit): تهيئة `constitution.md` (القواعد غير القابلة للتفاوض) + بنية `specs/` للمراحل + قوالب specify/plan/tasks. لو تعذّرت الأداة، أنشئ نفس البنية يدوياً بملفات markdown.
3. **Docker Compose** بخدمات: `backend` (FastAPI hello + health)، `postgres` (يهيّئ القواعد الأربع الفارغة: platform_db, apps_db, integration_db, reporting_db)، `qdrant`، `opensearch`، `minio`، `redis`. (`neo4j` معطّل خلف feature flag). `frontend` (قشرة Enterprise UI فارغة تعرض شاشة صحة/دخول لاحقاً).
4. **Deployment profiles**: `docker-compose.yml` (أساس) + `docker-compose.override.yml` (Local Dev) + `docker-compose.prod.yml` (Production overrides: replicas/resources/TLS/external endpoints) + `.env.example` مع `.env.local` / `.env.staging` / `.env.production`.
5. **نظام إعداد موحّد (Config/Settings loader)**: يقرأ من environment؛ هرمية defaults → profile env → secrets؛ **تحقّق عند الإقلاع (fail-fast)** إن نقص إعداد حرج.
6. **طبقات تجريد كـ interfaces فارغة (contracts فقط، بلا تنفيذ فعلي)**: `LLMProvider`، `IdentityProvider`، `ObjectStorage`، `DatabaseRouter`. الهدف تثبيت العقود ليُبنى عليها لاحقاً دون كسر.
7. **Health checks** لكل خدمة + endpoint `GET /health` في الـ backend يفحص الاتصال بـ postgres/redis/qdrant/opensearch/minio ويُرجع حالتها.
8. **README** يشرح الإقلاع لكل بروفايل + **خطة النقل المغلق** (كيف تُبنى/تُنقل الصور والاعتماديات offline: images + wheels + models placeholders).

## خارج النطاق صراحةً (Out of Scope — لا تنفّذها الآن)
مصادقة حقيقية، صلاحيات، شاشات ديناميكية، migrations للأعمال، RAG/OCR، وكلاء، LLM فعلي، متجر، تكاملات، تقارير، أي منطق أعمال.

## القيود التقنية (Constraints)
- Backend: Python + FastAPI. Frontend: إطار حديث يدعم RTL (مثل Next.js/React) — قشرة فقط.
- كل شيء **configuration-driven**؛ لا قيم مضمّنة (hardcoded) للـ endpoints/الأسرار/الموارد.
- **صورة واحدة لكل خدمة** تعمل في كل البيئات؛ **ممنوع** كود أو فرع خاص ببيئة.
- Backend **عديم الحالة (stateless)**؛ أي حالة جلسة مستقبلية في Redis/JWT.
- توافق التشغيل المغلق: لا اعتماد على أي خدمة سحابية أو إنترنت وقت التشغيل.

## هيكل المجلدات المقترح (Repository Structure)
```
/ (repo root)
├─ constitution.md
├─ specs/                      # Spec Kit: specs per phase
├─ docker-compose.yml
├─ docker-compose.override.yml # dev
├─ docker-compose.prod.yml     # prod overrides
├─ .env.example  .env.local  .env.staging  .env.production
├─ backend/
│  ├─ app/ (main.py, health, config/settings.py, interfaces/{llm,identity,storage,db_router}.py)
│  ├─ Dockerfile   requirements.txt
├─ frontend/
│  ├─ app/ (shell only, i18n/RTL scaffold)
│  ├─ Dockerfile   package.json
├─ deploy/ (offline-bundle/ scripts placeholders, tls/ placeholders)
└─ README.md
```

## معايير القبول (Acceptance Criteria)
- `docker compose --env-file .env.local up` يقلع كل الخدمات، و`GET /health` يُرجع حالة خضراء لكل التبعيات.
- القواعد الأربع تُنشأ فارغة تلقائياً.
- تبديل البروفايل إلى production يغيّر السلوك (replicas/resources/endpoints) **عبر الإعداد فقط** دون أي تعديل كود.
- الـ interfaces الأربعة موجودة كعقود بلا تنفيذ فعلي.
- README يشرح الإقلاع لكل بروفايل وخطة النقل المغلق.
- لا يوجد أي منطق أعمال. لا شيء خارج هذا الـ scope.

## تعليمات للـ Coding Agent
نفّذ الـ scope حرفياً. لا تُضِف ميزات غير مطلوبة. عند أي غموض، **اسأل قبل الافتراض**. سجّل أي قرار تقني في `specs/phase-0/notes.md`.
