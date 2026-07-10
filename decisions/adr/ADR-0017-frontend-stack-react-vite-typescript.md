# ADR-0017 — ستاك الواجهة: React + Vite + TypeScript + Tailwind + shadcn/ui-style

> **ملاحظة زرع:** هذا الرقم قائم في السجل الكنسي منذ 2026-07-04 (قرار D1)؛ يُزرع ملفه هنا ضمن إغلاق خط الأساس v1.0 **مع تحديث تكميلي واحد**: حسم موضع الواجهة داخل مستودع المنصة (بتفويض من SA — 2026-07-10).

**السياق (Context):** المشروع يحتاج SPA مؤسسية عربية-أولاً (RTL كامل، i18n، white-label) تستهلك عقود OpenAPI حصراً، وتعمل داخل شبكة مغلقة دون SSR/SEO.

**الوضع السابق (Previous state):** السجل الكنسي يحمل صف ADR-0017 (Accepted — D1) منذ 2026-07-04 بلا ملف مستقل؛ موضع كود الواجهة (نفس المستودع أم مستودع منفصل) بقي غير محسوم نصاً.

**القرار (Decision):** ستاك الواجهة الملزم: **React + Vite + TypeScript + Tailwind + مكوّنات بنمط shadcn/ui** (تُنسخ copy-in وتُدار بصف ترخيص). i18n عربي/إنجليزي وRTL منذ اليوم الأول. الواجهة **مستقلة منطقياً** على مستوى العقد (contract-level): لا تلمس قاعدة البيانات وتستهلك OpenAPI/SDK فقط. **الموضع (مقفل بتفويض):** `/frontend` داخل مستودع `local-rag-enterprise-platform` (نمط monorepo-lite)؛ أي فصل لاحق إلى مستودع مستقل لا يتم إلا عبر ADR جديد.

**البدائل (Alternatives):** Next.js (مرفوض — SSR/تعقيد لا يلزم لنظام داخلي مغلق) · SvelteKit (مرفوض كخيار أساسي — نضج نظام مكوّنات المؤسسة والعمالة المتاحة أقل لهذا السياق) · مستودع واجهة منفصل من الآن (مؤجل — يعقّد الحوكمة والإصدار قبل وجود كود فعلي).

**السبب (Rationale):** بيئة SPA خالصة خلف بوابة مؤسسية؛ Vite أسرع دورة تطوير؛ TypeScript يفرض العقود المولدة من OpenAPI؛ نمط shadcn يعطي تملّكاً كاملاً للمكوّنات (white-label) بلا dependency ثقيلة.

**العواقب (Consequences):** توليد types من OpenAPI (ADR-0025)؛ صفوف ترخيص React/Vite/TS/Tailwind/shadcn إلزامية قبل أول كود؛ فحص RTL ضمن قبول كل شاشة؛ سقالة `/frontend` ضمن Phase 0 (إضافات خط الأساس).

**خطة الانتقال (Migration plan):** لا يوجد كود سابق؛ عند أي فصل مستقبلي للمستودع: ADR + نقل تاريخ git + تثبيت خط CI للعقود.

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10 (الأصل: قرار D1 بتاريخ 2026-07-04)
**الوثائق المرتبطة (Related documents):** ../open-decisions.md (D1) · ../../methodology/coding-standards.md (§2/§7) · ../license-review.md (صفوف الستاك) · ../../phases/phase-0-foundation-full-stack-skeleton.md (FR-0.12 + إضافات v1.0) · ADR-0025-api-contract-rest-openapi-sse.md
