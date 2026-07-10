# ADR-0027 — معمارية سجلات القدرات والمزوّدات (Provider/Capability Registry)

**السياق (Context):** تعدد النماذج والمزوّدات (Ollama/vLLM وغيرها) مع حظر ربط كود الأعمال بأداة، وحظر الأسرار في الواجهة (D9)، يستوجب توثيق سلسلة التنفيذ الموحدة ووحدات السجلات كقرار معماري واحد مجمِّع.

**الوضع السابق (Previous state):** ADR-0005 (Capability-to-Model Mapping) وADR-0015 (LLM Gateway بوابة وحيدة) قائمان؛ التفصيل المعياري الكامل ورد في ui/UI_PROVIDER_MODEL_MANAGEMENT.md (v0.6) وarchitecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md (v0.7) — دون ADR يجمع السلسلة ووحداتها.

**القرار (Decision):** تُعتمد سلسلة التنفيذ الموحدة: **Capability → Provider → Model/Engine → Configuration → Execution Profile → Normalized Result → Audit**. وتُدار عبر **وحدات سجلات منطقية داخل الـ Monolith — ليست خدمات مستقلة**: Capability Registry · Provider Registry · Model Registry · Configuration · Health · Execution (+سياسات Fallback والاعتماد Approval policy، وتوافق الإصدارات version compatibility، ومعالجة الأسرار secret handling بالمرجع فقط، والتدقيق). **كود الأعمال لا يربط اسم أداة/مزوّد مباشرة أبداً** — الوصول عبر القدرات والعقود حصراً. **هذا الملف يجمع ويُحيل ولا يكرر**: التفصيل المعياري يبقى في المواصفتين المذكورتين.

**البدائل (Alternatives):** ربط مباشر بأسماء النماذج في الكود (مرفوض — يقتل قابلية التبديل ويخالف constitution م11) · خدمة registry مستقلة من الآن (مرفوضة — استخراج سابق لأوانه؛ تخضع لسياسة ADR-0026 لاحقاً) · إدارة المزوّدات من الواجهة بصلاحيات موسّعة (مرفوضة — تكسر D9؛ التغيير الفعلي config/Ops عبر workflow).

**السبب (Rationale):** السلسلة الموحدة تجعل كل تنفيذ نموذجٍ قابلاً للتتبع والتدقيق والتبديل؛ والوحدات المنطقية تحفظ بساطة النشر الحالي مع جاهزية الفصل المستقبلي.

**العواقب (Consequences):** أي قدرة جديدة تُسجَّل في الـ Registry قبل استخدامها؛ fallback وسياسات الاعتماد جزء من تعريف الربط لا من الكود؛ الواجهة مرآة قراءة (الخيار A) وتغيير المزوّد الفعلي عبر Ops.

**خطة الانتقال (Migration plan):** لا يوجد تنفيذ سابق؛ سقالات model-registry/provider-registry/llm-gateway في Phase 0 والتفعيل التدريجي وفق المراحل (P5 الحد الأدنى، P6 الاكتمال).

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10
**الوثائق المرتبطة (Related documents):** ../../ui/UI_PROVIDER_MODEL_MANAGEMENT.md · ../../architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md · ADR-0005 (السجل الكنسي) · ADR-0015 (السجل الكنسي) · ../../constitution.md (م11/م14) · ../../methodology/Spec_Driven_Modular_Monolith_Methodology.md (§7 — model-registry/provider-registry/llm-gateway)
