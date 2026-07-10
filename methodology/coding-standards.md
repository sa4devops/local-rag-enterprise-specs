# coding-standards.md — معايير الكود وقواعد AI Coding Agents

> **Version:** 1.2 — Final (D1–D9 مدمجة + §9 مُحدَّث وفق D12 في v1.0-architecture-baseline: معايير الحكم بدل عتبة الأسطر + سجل المراجع + التزامات التراخيص المتساهلة) · **Status:** Current / Accepted · **Date:** 2026-07-10 (الأصل 2026-07-04)
> **Authority:** النسخة المرجعية الموسّعة لـ Methodology §9 و§16؛ تُطبَّق حرفياً على كل جلسة تنفيذ. **لا كود في هذه الوثيقة — قواعد فقط.**

## 1) قواعد النطاق والانضباط (Scope)
- ترتيب القراءة الإلزامي قبل أي عمل: README → constitution → Methodology → Catalog → open-decisions → phase-roadmap → تصميم المرحلة → handoff → بطاقة المهمة.
- محادثة/جلسة = **task واحد** ببطاقة واضحة (scope + ملفات مسموحة + acceptance + tests).
- **لا يبدأ الوكيل كوداً إذا كان قرار لازم غير محسوم** (راجع open-decisions) — يسأل ولا يفترض.
- **لا كود خارج scope المهمة**، ولا تعديل ملف خارج قائمة البطاقة، ولا لمس `decisions/adr/` أو `constitution.md` دون طلب صريح، **ولا لمس Phase 1 حتى تُطلب صراحة**.
- الإخراج: patch محدود + قائمة اختبارات + تقرير مختصر + تحديث `handoff/handoff.md`.

## 2) قواعد المعمارية والحدود (Boundaries)
- **الستاك ملزم (D1/D2):** الواجهة React + Vite + TypeScript + Tailwind + shadcn-style (SPA مستقلة تستهلك OpenAPI/SDK فقط) · الخادم Python + FastAPI + Pydantic + SQLAlchemy + Alembic + PostgreSQL. أي انحراف = ADR أولاً.
- احترام Module Dependency Matrix حرفياً: الاعتماد هابط عبر الطبقات؛ same-tier فقط إذا كان مُدرَجاً في الـ manifest وغير دوري (A11).
- **لا direct DB access** خارج repository/service للـ module المالك؛ النداء بين الـ modules عبر contracts في `backend/shared` فقط.
- **لا ربط provider مباشرة دون abstraction:** استيراد SDK أي مزوّد بنية (valkey/redis/boto3/minio-sdk/s3fs…) **محصور داخل تنفيذ الـ Provider المقابل** في `backend/shared` — يُمنع في modules المجال.
- **لا استدعاء نموذج خارج LLM Gateway** (OpenAI-compatible)؛ **لا bypass** لـ Permission/Audit؛ **اللLM ليس مصدر حقيقة** (constitution م1/م2/م11).
- **لا DDL من LLM**؛ ترحيلات التطبيقات عبر خط التوليد المحكوم، وbaseline migrations عبر PR — مساران مسمّيان لا يختلطان.

## 3) قواعد الإعداد (Configuration)
- **لا hardcoded إطلاقاً:** لا secrets، لا endpoints، لا model names، لا paths — كلها من الإعداد الهرمي (defaults → profile → bundles → runtime → secrets) بـ namespace لكل module.
- مفاتيح الـ backends القياسية: `CACHE_BACKEND=memory|postgres|valkey` · `QUEUE_BACKEND=memory|postgres|valkey` · `LOCK_BACKEND=postgres|valkey` · `STORAGE_BACKEND=fs|s3` (+`S3_*` عند التفعيل). الافتراضيات: **memory/PostgreSQL وfilesystem** (D4/D5).
- كل مفتاح: default + validation + توصيف static/dynamic + fail-fast للحرِج برسالة تذكر اسم المفتاح؛ protected flags لا تُعطَّل من الواجهة.
- الأسرار عبر آلية أسرار خارج المستودع (فحص CI يمنع تسريبها).

## 4) قواعد الشبكة المغلقة وإعادة البناء
- **لا external API/network call وقت التشغيل** (اختبار no-external-call إلزامي)؛ أي استثناء بنص وموافقة صريحة (constitution م4).
- **lockfiles** لكل مديري الحزم + **digest pinning** لكل الصور — تُفحص في CI؛ **package caches** (uv cache + pnpm store) تُجهَّز ضمن حزمة النقل مع install/verify scripts (D3/D7).
- لا dependency/image/model جديدة قبل صف معتمد في `decisions/license-review.md` — البوابة متكررة.

## 5) قواعد الجودة والاختبار
- كل feature ⇒ اختبارات (وفق testing-strategy)؛ كل permission ⇒ **deny test**؛ كل audit event ⇒ اختبار حقوله؛ كل config ⇒ default+validation.
- **Validation fail-closed**؛ أخطاء **typed** بـ error_code قابل للتتبع؛ لا ابتلاع استثناءات صامت.
- عند إدخال تنفيذ ثانٍ لأي Provider ⇒ **Provider Equivalence tests** قبل اعتماده.
- المرور بكل **Quality Gates** (Methodology §11) شرط الدمج، وتحديث audit/logging جزء من DoD لكل feature مهمة.

## 6) قواعد التسمية واللغة والواجهة
- **المعرّفات التقنية ASCII**؛ العربية labels في الميتاداتا والواجهة؛ ثنائية ar/en مع **RTL/LTR صحيح** (logical properties + `dir`)؛ فحص RTL ضمن قبول أي شاشة؛ نصوص الواجهة i18n keys لا نصوصاً مضمّنة.

## 7) معايير الأدوات — **محسومة (D3)**
- Python: **uv** (إصدار Python يُثبَّت هنا عند بدء التنفيذ) · Frontend: Node LTS + **pnpm**.
- lockfiles إلزامية (uv.lock / pnpm-lock.yaml) + pinned versions + reproducible builds؛ أدوات lint/format موحّدة تُحدَّد عند تنفيذ Phase 0 (بصفوف مراجعة أولاً).

## 8) قواعد Git والتسليم
- **GitHub الآن (D7)**؛ فروع لكل task؛ رسائل commit تُشير إلى معرّف البطاقة (T-X.Y.Z)؛ لا دمج بدون CI أخضر؛ كل جلسة تُختتم بتحديث الوثائق المعنية + handoff كامل الحقول (+ ذكر أي مرجع OSS استُخدم).

## 9) Reference-aware Clean Implementation — **سياسة مُلزمة (D8 / ADR-0021)**
**المبدأ:** الفهم من المراجع مفتوحة المصدر مشروع ومطلوب؛ **النسخ بلا امتثال ممنوع**.

**يُسمح للوكيل أن:** يقرأ كود OSS ويدرسه · يفهم architecture/flows/API usage/dependency patterns/edge cases · يقارن أكثر من مشروع · يستخرج **design notes/summary** · ثم يبني **implementation أصلياً** وفق مواصفاتنا.

**لا يُسمح له أن:** ينسخ ملفات كاملة · ينسخ **نسخاً جوهرياً** (substantial copying) دون امتثال ترخيص صريح عبر صف license-review · يكتفي بإعادة تسمية سطحية (تغيير أسماء المتغيّرات) ويعتبر الناتج كوداً جديداً · **يعامل مخرَج «ذاكرة النموذج» كأصلي وهو مشابه جوهرياً لكود خارجي معروف** · يزيل notices/attribution يفرضها الترخيص · يُدخل كود AGPL/SSPL/commercial/copyleft أو أي كود حسّاس دون **Legal Review** · يخالف تراخيص المراجع · يربط النظام بمشروع خارجي دون قرار معماري (ADR).

**معيار الحكم — لا قاعدة عدّ أسطر (Δ v1.0-baseline / D12):** لا يُعتمد أي حد أسطر ثابت **معياراً وحيداً** للنسخ؛ المعايير الحاكمة: **التشابه الجوهري** (substantial similarity) · **التزامات الترخيص** · **المنشأ** (provenance) · **التمييز بين إعادة الاستخدام المباشرة والنمط المُتعلَّم**.
**سجل المراجع إلزامي (Reference Log):** كل مرجع OSS دُرس لأي مهمة يُسجَّل في handoff المهمة / سجل المراجع / ملاحظات التنفيذ — الدراسة بلا تسجيل مخالفة.
**التراخيص المتساهلة ليست بلا التزامات:** حتى MIT/BSD/Apache تحمل التزامات إشعار/إسناد (notice/attribution) تُحفظ ولا تُزال.

**الخطوات الإلزامية عند استخدام مرجع OSS:** (1) تحديد المشروع وسبب استخدامه → (2) مراجعة ترخيصه → (3) كتابة summary لما تعلّمه (لا نسخ) → (4) implementation خاص بنا وفق المواصفات → (5) ذكر المرجع في handoff/سجل المراجع → (6) أي استخدام مباشر لكود/مكتبة ⇒ عبر License Review → (7) موافقة صريحة حسب الترخيص والسياسة قبل الدمج.
**OpenWebUI خصوصاً:** مرجع UX/معماري فقط — لا يُنسخ كوده (قيود branding في 0.6.6+).

## 10) قواعد Observability (D6)
- **تمييز صارم:** **Audit Log** = أحداث أعمال/أمن (create/update/delete/approve/reject/permission/model-config/file-upload/وصول حسّاس…) **append-only داخل PostgreSQL**، permission-aware، قابل للبحث من Admin UI، مرتبط بـ user/session/request/action/entity. **Application logs** = تشخيص تقني **JSON خارج PostgreSQL** (stdout/ملف بدوّار).
- حقول الـ JSON logs الإلزامية: `ts, level, module, endpoint, user_id?, request_id, correlation_id, error_code?, duration_ms, message, stack?` — **لا أسرار ولا PII غير لازمة** (قناع + فحص CI).
- **Error Code Catalog** يُحدَّث مع كل feature؛ كل خطأ يحمل error_code + request_id.
- Health: `/health` تجميعي + `/health/db` `/health/qdrant` `/health/opensearch` `/health/llm` (المطفأ يظهر disabled).
- **/metrics** خلف علم `METRICS_ENABLED` (اختياري)؛ **OpenTelemetry adapter مستقبلاً فقط**؛ لا Grafana/Loki/Graylog قبل P8 وبمراجعة.
