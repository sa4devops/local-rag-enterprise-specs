# ADR-0024 — ستاك الخادم: Python + FastAPI + Pydantic + SQLAlchemy + Alembic + PostgreSQL

**السياق (Context):** إغلاق خط الأساس يتطلب توثيق ستاك الخادم كقرار معماري مستقل بملف ADR (كان محمولاً في صفوف D2 وسجل ADR-0001/0003 دون ملف مخصص لستاك الخادم ذاته).

**الوضع السابق (Previous state):** D2 (2026-07-04) أكّد الستاك في open-decisions/coding-standards؛ ADR-0001 يغطي Modular Monolith وADR-0003 يغطي PostgreSQL والقواعد الأربع — ولا يوجد ADR مفرد يجمع ستاك الخادم وطبقاته.

**القرار (Decision):** ستاك الخادم الملزم: **Python + FastAPI + Pydantic + SQLAlchemy + Alembic + PostgreSQL** مع workers غير متزامنة من نفس الـ codebase. الطبقات: **API / Application / Domain / Infrastructure** داخل كل module. **الواجهة لا تلمس قاعدة البيانات إطلاقاً** — كل وصول بيانات عبر الخادم وعقوده.

**البدائل (Alternatives):** Node.js/NestJS (مرفوض — نظام Python أنضج لـ AI/RAG/OCR والوكلاء) · Django (مرفوض — إطار كامل الرأي يعيق بنية modules المخصصة وOpenAPI-first) · Go (مرفوض — سرعة تنفيذ ممتازة لكن تكلفة نظام الذكاء/المكتبات أعلى).

**السبب (Rationale):** منظومة Python هي مركز ثقل RAG/LLM/OCR؛ FastAPI يولّد OpenAPI أصلاً (أساس العقد D6)؛ Pydantic يعطي validation صارمة fail-closed؛ Alembic يخدم مسار الترحيلات المزدوج (baseline عبر PR، والتوليد المحكوم للتطبيقات).

**العواقب (Consequences):** لا ORM ثانٍ ولا إطار ويب ثانٍ؛ طبقة Domain خالية من استيرادات FastAPI/SQLAlchemy المباشرة حيث أمكن (قابلية اختبار)؛ صفوف ترخيص FastAPI/Pydantic/SQLAlchemy/Alembic قبل أول كود؛ إصدارات Python تُثبَّت في lockfiles عند تنفيذ Phase 0.

**خطة الانتقال (Migration plan):** لا كود سابق — يبدأ الالتزام من سقالة Phase 0.

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10 (يوثّق قرار D2 بتاريخ 2026-07-04)
**الوثائق المرتبطة (Related documents):** ../open-decisions.md (D2) · ../../methodology/coding-standards.md (§2) · ../../methodology/Spec_Driven_Modular_Monolith_Methodology.md (§6/§7) · ADR-0001 (السجل الكنسي) · ADR-0003 (السجل الكنسي) · ADR-0025-api-contract-rest-openapi-sse.md
