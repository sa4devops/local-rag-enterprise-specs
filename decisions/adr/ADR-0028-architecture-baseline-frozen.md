# ADR-0028 — سياسة خط الأساس المعماري المجمَّد (v1.0-architecture-baseline)

**السياق (Context):** اكتملت مرحلة المعمارية والمواصفات عبر الحزم v0.1→v0.8 وقرارات D1–D16، ويلزم إغلاق رسمي يمنع إعادة فتح المعمارية عرضياً مع كل جلسة، دون تحويل الوثائق إلى نص متحجر يعيق التوضيح والتصحيح.

**الوضع السابق (Previous state):** المواصفات «Current/Accepted» بلا مفهوم خط أساس مسمى؛ التعديل يجري بدفعات معتمدة من SA (آخرها v0.8) دون قاعدة دستورية تحدد متى يُعد التغيير معمارياً يستوجب ADR ومتى لا.

**القرار (Decision):**
1. **المواصفات المعمارية مجمَّدة كخط أساس معتمد** عند الوسم **`v1.0-architecture-baseline`** (constitution **م21**).
2. **مجمَّد ≠ غير قابل للتغيير:** أي تغيير معماري لاحق يمر **حصراً عبر ADR** وفق سياسة decisions/adr/README.md (D15).
3. **لا يعيد فتح المعمارية:** التوضيحات · تصحيح الأخطاء الكتابية · إصلاحات الاتساق · التفاصيل التنفيذية غير المعمارية.
4. **موجبات ADR** (D15): ما يمس المعمارية أو حدود الوحدات أو العقود العامة أو التخزين أو الأمن أو نموذج البيانات أو النشر أو الاعتماديات الاستراتيجية أو تقنية يصعب استبدالها أو الاستخراج إلى خدمات أو معمارية المزوّدات أو عقد الواجهة/الخادم.
5. **بوابة الإغلاق:** لا يُوسم ADR بـ Accepted حتى تُنفَّذ تحديثات «الوثائق المتأثرة» الخاصة به.

**البدائل (Alternatives):** إبقاء الوضع بلا خط أساس (مرفوض — كل جلسة تعيد التفاوض على المعمارية) · تجميد مطلق بلا مسار تغيير (مرفوض — غير واقعي ويولّد انحرافاً صامتاً خارج الوثائق) · خط أساس لكل ملف على حدة (مرفوض — يفتت المرجعية؛ الوسم الواحد يحدد الحزمة كاملة).

**السبب (Rationale):** خط أساس موسوم يعطي نقطة مرجعية واحدة للتنفيذ وللمقارنة، ويحوّل التغيير المعماري من نقاش مفتوح إلى إجراء موثق له كلفة وسجل.

**العواقب (Consequences):** constitution م21/م22 نافذتان؛ README (حالة المشروع) وarchitecture/README يشيران إلى الوسم؛ platform/docs/SPEC_SOURCE.md يشير إليه كمرجع نافذ؛ تصميم Phase 1 يبدأ فوق هذا الخط دون إعادة فتح ما قبله.

**خطة الانتقال (Migration plan):** لا انتقال — الوسم يُنشأ على commit الإغلاق؛ أي دفعة مواصفات لاحقة تصدر بوسم جديد فوق الخط عبر مسار ADR/الدفعات المعتمدة.

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10
**الوثائق المرتبطة (Related documents):** ../../constitution.md (م21/م22) · ../adr/README.md (سياسة D15) · ../../README.md (حالة المشروع) · ../../architecture/README.md · ADR-0023-enterprise-ai-platform-progressive-implementation.md · ADR-0017-frontend-stack-react-vite-typescript.md · ADR-0024-backend-stack-python-fastapi.md · ADR-0025-api-contract-rest-openapi-sse.md · ADR-0026-module-boundaries-packaging-extraction.md · ADR-0027-provider-capability-registry-architecture.md · ADR-0019-object-storage-seaweedfs-production-default.md · ADR-0018-cache-queue-lock-valkey-scale-profile.md · ADR-0004-search-architecture-postgres-qdrant-opensearch.md · ADR-0020-observability-audit-logs-baseline.md · ADR-0021-reference-aware-clean-implementation.md · ADR-0022-github-development-airgapped-delivery.md
