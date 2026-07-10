# agent-execution-model.md — نموذج تنفيذ الوكلاء للمراحل

> **Version:** 1.0 — Proposed (Accepted باعتماد v0.3) · **Date:** 2026-07-06 · **Authority:** يمدّ Methodology §18 تشغيلياً؛ عند التعارض تحكم Methodology ثم هذا الملف.
> **Purpose:** كيف تُسلَّم كل مرحلة لاحقاً لأي AI Coding Agent مستقل وتُنفَّذ بانضباط — **لا تنفيذ الآن**.

## §1 ترتيب القراءة الإلزامي قبل أي عمل
1) platform: `README.md` → 2) `AGENTS.md` → 3) `docs/SPEC_SOURCE.md` (يحدد **الإصدار المعتمد** — المصدر الوحيد للرقم) → 4) specs بالإصدار المعتمد: `README.md` → `constitution.md` → `methodology/` (المنهجية + coding-standards + testing-strategy) → `catalogs/Feature_Technical_Architecture_Catalog.md` → `decisions/open-decisions.md` → `decisions/license-review.md` → `phases/PHASE_MASTER_PLAN.md` (+`phase-roadmap.md`) → **تصميم مرحلته فقط** في `phases/designs/` → `references/OSS_REFERENCE_CATALOG.md` (عند حاجة دراسة) → `handoff/handoff.md` → **بطاقة المهمة**. القراءة خارج ذلك (تصاميم مراحل أخرى) للاطلاع لا للتنفيذ.

## §2 نموذج الجلسة والفروع
جلسة واحدة = **task واحدة** ببطاقة (Goal/Allowed paths قراءةً وكتابةً/Acceptance/Tests/Non-goals) · فرع: `phase-N/T-x.y.z-slug` · **ممنوع الكتابة على main** · الدمج عبر PR يجتاز Quality Gates (Methodology §11) + CI boundaries · رسالة الـ commit تتضمن معرّف البطاقة.

## §3 دورة حياة المهمة
(١) يعيد الوكيل صياغة فهمه للبطاقة في سطور؛ (٢) **أي غموض ⇒ توقّف واسأل، لا تفترض ولا تكتب**؛ (٣) patch محدود داخل Allowed paths فقط؛ (٤) اختبارات المهمة (deny/audit/unit + أنواع المرحلة من تصميمها §19)؛ (٥) اجتياز البوابات؛ (٦) تحديث الوثائق المعنية؛ (٧) إدخال handoff كامل الحقول (المنجز/غير المنجز/الملفات/القرارات/المخاطر/الاختبارات/الخطوة التالية/**ما لا يُلمس**/المراجع المستخدمة).

## §4 منع scope-creep
البطاقة تحدد **Non-goals** صراحة · لا endpoint/جدول/شاشة غير واردة في تصميم المرحلة · CI يرفض كسر الحدود (import rules) وأي ملف خارج Allowed paths يُرفض في المراجعة · الأفكار الإضافية تُدوَّن **اقتراحاً في handoff** لا كوداً.

## §5 منع نسخ open-source (تشغيل سياسة D8/ADR-0021)
المراجع = المدرجة في `OSS_REFERENCE_CATALOG.md` حصراً؛ غير المدرج ⇒ **توقف واسأل** · **جلسة دراسة ≠ جلسة تنفيذ**: الدراسة تُخرج **design-notes artifact** (مفاهيم/تدفقات، بلا كود) يُرفق بالبطاقة · أي إعادة استخدام مباشرة (ملف/مقتطف >~10 أسطر/بنية بأسماء مبدَّلة/استنساخ حرفي من الذاكرة) ⇒ صف license-review وموافقة قبل الدمج · حفظ notices إلزامي · Dify/NocoDB وأمثالهما: **UX-behavior فقط دون قراءة الشيفرة** · ذكر كل مرجع استُخدم في handoff.

## §6 قالب Coding Agent Prompt الموحّد (يُملأ عند التكليف — لا يُنفَّذ الآن)
> أنت وكيل تنفيذ لمهمة واحدة في منصة Local RAG Enterprise Platform.
> **PHASE:** {N} · **DESIGN:** {path} · **APPROVED SPECS RELEASE:** {tag من SPEC_SOURCE} · **TASK:** {T-x.y.z} · **BRANCH:** phase-{N}/T-{x.y.z}-{slug} · **ALLOWED PATHS:** {قائمة} · **NON-GOALS:** {قائمة}
> اقرأ بترتيب §1 من agent-execution-model قبل أي شيء، ونفّذ **المكتوب فقط** في التصميم والبطاقة.
> ثوابت مُلزمة: المنصة ليست chatbot · **اللLM ليس مصدر حقيقة** · الصلاحية قبل أي وصول (default-deny) وAudit لكل مهم · لا استدعاء نموذج خارج LLM Gateway · لا ربط مزوّد بلا abstraction (SDKs داخل التنفيذات فقط) · لا DDL من LLM؛ كيانات الأعمال عبر خط التوليد المحكوم · لا dependency/image/model بلا صف license-review · الستاك ثابت: React+Vite+TS+Tailwind+shadcn-style / FastAPI+Pydantic+SQLAlchemy+Alembic+PostgreSQL / uv+pnpm · Qdrant+OpenSearch حاضران · ar/en+RTL لكل شاشة · لا نداء خارجي وقت التشغيل.
> المراجع المفتوحة: وفق OSS_REFERENCE_CATALOG وسياسة Reference-aware — الدراسة للتعلم، والنسخ محكوم بالبوابة.
> إن صادفت **Open Decision** أو غموضاً أو حاجة لمخالفة أي قاعدة: **توقف واسأل** ولا تكتب.
> أنهِ بـ: اختبارات المهمة خضراء (deny/audit أولاً) + تحديث الوثائق + إدخال handoff كامل + قائمة «ما لا يُلمس» للتالي. لا تلمس main ولا ملفات خارج ALLOWED PATHS.

## §7 إنفاذ الدستور والصلاحيات والتدقيق
Validation وأبواب الأمن **fail-closed** دائماً · لكل endpoint جديد deny-test قبل قبوله · لكل حدث بكتالوج §11 اختبار حقوله · أي حاجة لكسر قاعدة معمارية ⇒ **ADR أولاً** (يتوقف الوكيل ويطلبه) · محاولات الالتفاف (وصول جداول عابر، نداء نموذج مباشر) يكشفها CI وتُرفض.

## §8 التعامل مع Open Decisions
قبل بدء مرحلة: بنود **فئة 2** الخاصة بها مقفلة، وODs تصميمها تُحسم في **جلسة Clarify التفعيل** (خفيفة) ثم تُولَّد بطاقات المهام (جلسة Tasks) · أثناء التنفيذ: مصادفة OD غير محسوم ⇒ توقف، اذكر معرّفه (OD-Px-n)، اطلب القرار، وثّق الحسم في open-decisions + handoff · **فئة 3** بوابة متكررة عند تفعيل أي صورة اختيارية · **فئة 4** قبل أي توزيع.
