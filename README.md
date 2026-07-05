# منصة تشغيل معرفي مؤسسي مغلق — Enterprise Knowledge Operations Platform (Air-Gapped)

> **Document Title:** README — نقطة الدخول للحزمة الوثائقية
> **Version:** 1.1 (D1–D9 مدمجة) · **Status:** Current / Accepted · **Date:** 2026-07-04
> **Purpose:** تعريف المشروع وتوجيه أي قارئ أو AI Coding Agent إلى ترتيب القراءة الصحيح.

## ما هو المشروع
**منصة تشغيل معرفي مؤسسي كاملة** (Enterprise AI / Local RAG / Local LM Platform) تعمل **داخل شبكة مغلقة (air-gapped)** في Docker، بنظام **metadata-driven**: شاشات ديناميكية، صلاحيات مؤسسية (RBAC+ABAC+ReBAC+تصنيف خماسي)، workflows باعتماد، مستندات/OCR/RAG، وسائط متعددة، تقارير طويلة، متجر تطبيقات مؤسسي، وتدقيق شامل. تستهدف 20,000–30,000 مستخدم مسجّل لكل مؤسسة، وتُطوَّر أولاً كـ Local Demo على جهاز واحد ثم تنتقل إلى الإنتاج **بتغيير configuration فقط**.

## ما الذي **ليس** هو المشروع
- **ليس chatbot** — الدردشة سطح واحد من منصة كاملة.
- **الـ LLM ليس Source of Truth** — مصادر الحقيقة: قواعد البيانات الرسمية + المستندات المعتمدة + الـ APIs الداخلية + السجلات الرسمية. دور النموذج: تحليل/تلخيص/تفسير/تنفيذ مهام/طلب توضيح.
- **الواجهة النهائية ليست Open WebUI** — الواجهة **Enterprise UI خاصة** (Arabic/English، RTL كامل، white-label). Open WebUI مرجع دراسة فقط.
- **لا اتصال خارجي وقت التشغيل** — أي أداة/نموذج/موصل يحتاج الخارج ممنوع ما لم يُنص ويُعتمد صراحة.
- **لا نسخة إنتاج منفصلة** — نفس الكود/الـ repo/الصور؛ الانتقال للإنتاج configuration-only، ممنوع تعديل الكود أو fork.

## كيف يُبنى
**Modular Monolith أولاً** (ADR-0001 — Accepted) بحدود modules مفروضة وقابلية فصل لاحقة، بمنهجية **Spec-driven Development متوافقة مع GitHub Spec Kit / Spacekit**:
`Vision → Specify → Clarify → Plan → Tasks → Implement`
**التنفيذ (Implement) ليس الآن** — كل مرحلة تُصمَّم في محادثة مستقلة ثم تُنفَّذ لاحقاً مرحلةً مرحلة وفق `phase-roadmap.md`.
**الستاك المعتمد (D1–D3):** واجهة **React + Vite + TypeScript + Tailwind + shadcn-style** (SPA مستقلة) · خادم **Python + FastAPI** · أدوات **uv + pnpm**. **سياسة المراجع (D8):** Reference-aware clean implementation — قراءة كود OSS للتعلم مسموحة، والنسخ المباشر محكوم بـ License Gate (النص الملزم في `methodology/coding-standards.md`). **لا يبدأ الوكيل كوداً إذا كان قرار لازم غير محسوم.**

## ترتيب القراءة لأي AI Coding Agent (إلزامي)
1. `README.md` (هذا الملف) → 2. `constitution.md` → 3. `methodology/Spec_Driven_Modular_Monolith_Methodology.md` → 4. `catalogs/Feature_Technical_Architecture_Catalog.md` → 5. `decisions/open-decisions.md` → 6. `phases/phase-roadmap.md` → 7. تصميم المرحلة المكلَّف بها فقط (`phases/…`) → 8. `handoff/handoff.md` → 9. بطاقة المهمة المحددة.
**قاعدة:** الوكيل ينفّذ **ما هو مكتوب فقط**، لا يضيف dependency بلا صف في `decisions/license-review.md`، ولا يلمس ملفات خارج بطاقة مهمته، ويحدّث handoff قبل الإنهاء.

## ترتيب مرجعية الوثائق عند التعارض (Authority Order)
1) constitution.md → 2) Methodology → 3) Feature &amp; Technical Architecture Catalog → 4) تصنيف القرارات المفتوحة → 5) phase-roadmap.md → 6) تصاميم المراحل المعتمدة → 7) superseded/ (تاريخية). أي وثيقة/برومبت قديم يخالف الترتيب = **Superseded**.

## حالة المشروع الآن
الوثائق التأسيسية والتصميمية معتمدة (بما فيها تصميم Phase 0). **لا كود بعد**. الخطوة التالية: تصميم **Phase 1 — Governed Core + Screen Builder** في محادثة مستقلة، ثم التنفيذ مرحلةً مرحلة.
