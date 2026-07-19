# منصة تشغيل معرفي مؤسسي مغلق — Enterprise Knowledge Operations Platform (Air-Gapped)

> **Document Title:** README — نقطة الدخول للحزمة الوثائقية
> **Version:** 1.3 — (Δ 2026-07-19 دفعة G1: +`AUTHORITY.md` في ترتيب القراءة الإلزامي · إحالة ترتيب السلطة إليه نصاً كنسياً وحيداً · تحديث ستاك الواجهة وفق ADR-0031) · (1.2: v1.0-architecture-baseline — سطر الهوية + تحديث حالة المشروع) · **Status:** Current / Accepted · **Date:** 2026-07-19 (الأصل 2026-07-10)
> **Purpose:** تعريف المشروع وتوجيه أي قارئ أو AI Coding Agent إلى ترتيب القراءة الصحيح.

الهوية المعتمدة: Enterprise AI Platform with Progressive Implementation — المنصة هي المنتج؛ معماريةٌ كاملة موثقة من البداية، وتنفيذٌ وتفعيلٌ مرحليان. (لا يُستخدم مسمى Product-led Platform رسمياً.)
Local RAG Enterprise هي منصة تطبيقات مؤسسية، ليست تطبيق أعمال واحداً.

## ما هو المشروع
**منصة تشغيل معرفي مؤسسي كاملة** (Enterprise AI / Local RAG / Local LM Platform) تعمل **داخل شبكة مغلقة (air-gapped)** في Docker، بنظام **metadata-driven**: شاشات ديناميكية، صلاحيات مؤسسية (RBAC+ABAC+ReBAC+تصنيف خماسي)، workflows باعتماد، مستندات/OCR/RAG، وسائط متعددة، تقارير طويلة، متجر تطبيقات مؤسسي، وتدقيق شامل. تستهدف 20,000–30,000 مستخدم مسجّل لكل مؤسسة، وتُطوَّر أولاً كـ Local Demo على جهاز واحد ثم تنتقل إلى الإنتاج **بتغيير configuration فقط**.

## ما الذي **ليس** هو المشروع
- **ليس chatbot** — الدردشة سطح واحد من منصة كاملة.
- **الـ LLM ليس Source of Truth** — مصادر الحقيقة: قواعد البيانات الرسمية + المستندات المعتمدة + الـ APIs الداخلية + السجلات الرسمية. دور النموذج: تحليل/تلخيص/تفسير/تنفيذ مهام/طلب توضيح.
- **الواجهة النهائية ليست Open WebUI** — الواجهة **Enterprise UI خاصة** (Arabic/English، RTL كامل، white-label). Open WebUI مرجع دراسة، **ويجوز استخدامه داخلياً واجهةَ محادثة مؤقتة ضمن شرط المادة م6 وحدود ADR-0030** — لا واجهةً نهائية بحال.
- **لا اتصال خارجي وقت التشغيل** — أي أداة/نموذج/موصل يحتاج الخارج ممنوع ما لم يُنص ويُعتمد صراحة.
- **لا نسخة إنتاج منفصلة** — نفس الكود/الـ repo/الصور؛ الانتقال للإنتاج configuration-only، ممنوع تعديل الكود أو fork.

## كيف يُبنى
**Modular Monolith أولاً** (ADR-0001 — Accepted) بحدود modules مفروضة وقابلية فصل لاحقة، بمنهجية **Spec-driven Development متوافقة مع GitHub Spec Kit / Spacekit**:
`Vision → Specify → Clarify → Plan → Tasks → Implement`
**التنفيذ (Implement) ليس الآن** — كل مرحلة تُصمَّم في محادثة مستقلة ثم تُنفَّذ لاحقاً مرحلةً مرحلة وفق `phase-roadmap.md`.
**الستاك المعتمد:** واجهة العميل الأساسي **Next.js client-only + TypeScript + Tailwind** عبر قناة Rocket المحكومة (**ADR-0031** — الحراس الأربعة وبوابات `pnpm typecheck/lint/build`؛ ‏ADR-0017 خالفَه ADR-0031 **في نطاق اختيار الإطار فقط** ومبادئه باقية، وعميل **React + Vite** مصغر يبقى اختبارَ الاستبدال المؤجل — م23) · الخادم **Python + FastAPI** — **خلفية المنصة ومصدر منطق الأعمال والتحقق والصلاحيات حصراً** (D2 · ‏ADR-0025/0029) · أدوات **uv + pnpm**. **سياسة المراجع (D8):** Reference-aware clean implementation — قراءة كود OSS للتعلم مسموحة، والنسخ المباشر محكوم بـ License Gate (النص الملزم في `methodology/coding-standards.md`). **لا يبدأ الوكيل كوداً إذا كان قرار لازم غير محسوم.**

## ترتيب القراءة لأي AI Coding Agent (إلزامي)
1. `README.md` (هذا الملف) → 2. `constitution.md` → 3. `AUTHORITY.md` (السلم الكنسي الموحد لترتيب السلطة) → 4. `methodology/Spec_Driven_Modular_Monolith_Methodology.md` → 5. `catalogs/Feature_Technical_Architecture_Catalog.md` → 6. `decisions/open-decisions.md` → 7. `phases/phase-roadmap.md` → 8. تصميم المرحلة المكلَّف بها فقط (`phases/…`) → 9. `handoff/handoff.md` → 10. بطاقة المهمة المحددة.
**قاعدة:** الوكيل ينفّذ **ما هو مكتوب فقط**، لا يضيف dependency بلا صف في `decisions/license-review.md`، ولا يلمس ملفات خارج بطاقة مهمته، ويحدّث handoff قبل الإنهاء.

## ترتيب مرجعية الوثائق عند التعارض (Authority Order)
**النص الكنسي الوحيد لترتيب السلطة هو `AUTHORITY.md`** (السلم الموحد — 13 مرتبة، بخريطة الأرقام التاريخية وقواعد الحسم واعتماده ببوابة G1)؛ لا يُكرَّر الترتيب هنا ولا في أي ملف آخر. آلية م20 باقية كما هي: أي وثيقة/برومبت قديم يخالف = **Superseded**.

## حالة المشروع الآن
**المعمارية مُغلقة عند خط الأساس الموسوم `v1.0-architecture-baseline` بتاريخ 2026-07-10 وفق constitution م21.** كل حزم المواصفات v0.4–v0.7 (وما بعدها حتى v0.8) مدموجة ومُصدَرة. **لا كود بعد**. الخطوة التالية: **«تصميم تفعيل Phase 1 — Governed Core + Screen Builder»** في محادثة مستقلة **ولا يبدأ إلا ببطاقة مهمة معتمدة صراحة من SA**؛ مدخلاته الإلزامية: تصميم v0.3 المستعاد (بلافتة حالته) + دلتا `phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md` + قراءة Tier-0 والقرارات الأحدث (ومنها `decisions/DEFERRED_IMPLEMENTATION.md`) — **لا بدءَ من الصفر ولا تنفيذَ مباشراً من ملف v0.3**. مسار التغيير بعد الخط: أي تعديل معماري عبر **ADR** حصراً (م21 — `decisions/adr/README.md`)؛ التوضيحات والتفاصيل غير المعمارية لا تعيد فتح المعمارية.
